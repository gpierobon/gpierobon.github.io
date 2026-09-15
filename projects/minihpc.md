---
layout: post
title: 'Mini HPC Cluster with VirtualBox'
---

A step-by-step guide to building a mini High-Performance Computing (HPC) cluster on your own machine using VirtualBox VMs. The end result is a small but functional cluster with:

- Multiple Linux servers (login/head node + compute nodes + storage node)
- An internal cluster network with external internet access
- Passwordless SSH connectivity between nodes
- Shared storage via NFS
- Job scheduling via Slurm

## Cluster at a Glance

| Hostname | Role | Suggested specs |
|---|---|---|---|
| `login-node` | Head node / Slurm controller | 2 CPU, 2 GB RAM |
| `compute-node-1` | Compute | 1 CPU, 2 GB RAM |
| `compute-node-2` | Compute | 1 CPU, 2 GB RAM |
| `storage-node` | NFS server | 1 CPU, 2 GB RAM, extra disk for `/hpc/shared` |

> **Note:** These specs are minimums for a laptop/desktop host and learning purposes.

## Table of Contents

1. [Step 0: VirtualBox VM](#step-0-virtualbox-vm)
2. [Step 1: Create the Golden Image VM](#step-1-create-the-golden-image-vm)
3. [Step 2: Networking Between VMs](#step-2-networking-between-vms)
4. [Step 3: Shared Storage (NFS Server)](#step-3-shared-storage-nfs-server)
5. [Step 4: Install Slurm](#step-4-install-slurm)
6. [Step 5: Configure Slurm](#step-5-configure-slurm-head-node-and-compute-nodes)
7. [Step 6: Test the Cluster](#step-6-test-cluster)

---

## Step 0: VirtualBox VM 

Install VirtualBox on your host machine:

```bash
sudo apt update
sudo apt install virtualbox -y
```

Download **Ubuntu Server 22.04 LTS** and use it to create your first VM. See the [Cluster at a Glance](#cluster-at-a-glance) table above for suggested per-VM specs.

During installation:

- Enable **OpenSSH Server** in the installer 
- Use a simple admin user, e.g. `hpcadmin`

Verify SSH afterward:

```bash
systemctl status ssh
```

This first VM becomes the **golden image**.

---

## Step 1: Create the Golden Image VM

Once your golden image VM is installed and configured, clone it in VirtualBox to create each additional node (`login-node`, `compute-node-1`, `compute-node-2`, `storage-node`, etc.).

When cloning:

- Tick **Reinitialize MAC address** (avoids network conflicts)
- Clone type: **Full clone**

---

## Step 2: Networking Between VMs

The VMs need to talk to each other, so the best option is **Host-only network + NAT**.

For **each VM**, go to `Settings → Network` and enable:

- **Adapter 1:** NAT (internet access)
- **Adapter 2:** Host-only Adapter (cluster network)

#### Set static IPs

Check current IP assignment:

```bash
ip a
```

Edit the netplan config:

```bash
sudo vim /etc/netplan/00-installer-config.yaml
```

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      dhcp4: no
      addresses:
        - 192.168.56.10/24   # replace with this node's IP
```

> **Note:** E.g.`192.168.56.10` for `login-node`, `192.168.56.11` for `compute-node-1`, and so on. 

Apply the config and set the hostname:

```bash
sudo netplan apply
sudo hostnamectl set-hostname <name>
```

Check IP/hostname:

```bash
hostname
hostname -I
```

#### Update `/etc/hosts` on ALL VMs

```bash
sudo nano /etc/hosts
```

Add, for example:

```
192.168.56.10 login-node
192.168.56.11 compute-node-1
192.168.56.12 compute-node-2
192.168.56.13 storage-node
```

#### Verify connectivity

From the login node:

```bash
ping compute-node-1
ssh compute-node-1
```

#### Enable SSH key-based auth on all nodes

```bash
sudo apt update
[sudo apt install openssh-server -y] # might be installed already

ssh-keygen
ssh-copy-id <other_node>
```

> **Note:** Run `ssh-copy-id` once per remote node from `login-node` (e.g. `ssh-copy-id compute-node-1`, then repeat for `compute-node-2` and `storage-node`) so you can SSH everywhere without a password.

---

## Step 3: Shared Storage (NFS Server)

#### On `storage-node`

Install the NFS server:

```bash
sudo apt update
sudo apt install nfs-kernel-server -y
```

Create and prepare the shared directory:

```bash
sudo mkdir -p /hpc/shared
sudo chown nobody:nogroup /hpc/shared
sudo chmod 777 /hpc/shared
```

Export it:

```bash
sudo nano /etc/exports
```

Add:

```
/hpc/shared 192.168.56.0/24(rw,sync,no_subtree_check)
```

Apply the export:

```bash
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

#### On ALL nodes (clients)

Install the NFS client:

```bash
sudo apt install nfs-common -y
```

Mount the shared storage:

```bash
sudo mkdir -p /hpc/shared
sudo mount 192.168.56.13:/hpc/shared /hpc/shared
```

Make the mount persistent by adding this line to `/etc/fstab`:

```
192.168.56.13:/hpc/shared   /hpc/shared   nfs   defaults,_netdev,vers=3   0   0
```

#### Bonus: Shared home directories

```bash
sudo mkdir -p /hpc/home
sudo chmod 755 /hpc/home
```

Add to `/etc/exports`:

```
/hpc/home   192.168.56.0/24(rw,sync,no_subtree_check,no_root_squash)
```

Re-export:

```bash
sudo exportfs -ra
sudo exportfs -v
```

---


---

## Step 4: Install Slurm 

Slurm is what turns your VM collection into an actual job-scheduled cluster.

#### On all nodes

```bash
sudo apt install slurm-wlm munge -y
```

#### Step 4.1: Set up Munge authentication

Munge handles authentication between the Slurm controller and compute nodes — all nodes must share the same key.

On the **head node**, generate the key:

```bash
sudo mungekey -c -k /etc/munge/munge.key
```

Copy it to the other nodes:

```bash
sudo scp /etc/munge/munge.key hpcadmin@compute-node-1:/tmp/
sudo mv /tmp/munge.key /etc/munge/munge.key
sudo chown munge:munge /etc/munge/munge.key
sudo chmod 400 /etc/munge/munge.key
```

> **Note:** Repeat the `scp` + `mv`/`chown`/`chmod` sequence for **every** other node — `compute-node-2` and `storage-node` too. All nodes must end up with the identical key file.

On **all nodes**, enable and start munge:

```bash
sudo systemctl enable munge
sudo systemctl start munge
sudo systemctl status munge
```

Test that authentication works:

```bash
munge -n | unmunge
munge -n | ssh hpcadmin@compute-node-1 unmunge
```

---

## Step 5: Configure Slurm (head node and compute nodes)

Get hardware specs for the node definitions:

```bash
sudo slurmd -C
```

Edit `/etc/slurm/slurm.conf` **on the head node**:

```ini
ClusterName=hpc-cluster
SlurmctldHost=login-node

# Auth / comms
AuthType=auth/munge
CryptoType=crypto/munge
MpiDefault=none

# Ports
SlurmctldPort=6817
SlurmdPort=6818

# State/log locations
StateSaveLocation=/var/spool/slurmctld
SlurmdSpoolDir=/var/spool/slurmd
SlurmctldLogFile=/var/log/slurm/slurmctld.log
SlurmdLogFile=/var/log/slurm/slurmd.log
SlurmctldPidFile=/var/run/slurmctld.pid
SlurmdPidFile=/var/run/slurmd.pid

# Scheduling
SchedulerType=sched/backfill
SelectType=select/cons_tres
SelectTypeParameters=CR_Core_Memory

# Process tracking
ProctrackType=proctrack/linuxproc
TaskPlugin=task/none

# Timers
SlurmctldTimeout=120
SlurmdTimeout=300
InactiveLimit=0
MinJobAge=300
KillWait=30
Waittime=0

# Node definitions
NodeName=compute-node-1 CPUs=1 RealMemory=1900 State=UNKNOWN
NodeName=compute-node-2 CPUs=1 RealMemory=1900 State=UNKNOWN

# Partition
PartitionName=compute Nodes=compute-node-1,compute-node-2 Default=YES MaxTime=INFINITE State=UP
```

> **Note:** `RealMemory` should match what `slurmd -C` reported for each node, not just be copy-pasted. Mismatches here are a common reason nodes show as `DOWN` in `sinfo`.

Copy the finalized config to every compute node (run from `login-node`):

```bash
sudo scp /etc/slurm/slurm.conf hpcadmin@compute-node-1:/tmp/
sudo scp /etc/slurm/slurm.conf hpcadmin@compute-node-2:/tmp/
```

Then on **each compute node**:

```bash
sudo mv /tmp/slurm.conf /etc/slurm/slurm.conf
```

#### Create required directories on all three nodes

```bash
sudo mkdir -p /var/spool/slurmctld /var/spool/slurmd /var/log/slurm
sudo chown slurm:slurm /var/spool/slurmctld /var/spool/slurmd /var/log/slurm
```

#### Start services

On `login-node`:

```bash
sudo systemctl enable slurmctld
sudo systemctl start slurmctld
sudo systemctl status slurmctld
```

On `compute-node-1` and `compute-node-2`:

```bash
sudo systemctl enable slurmd
sudo systemctl start slurmd
sudo systemctl status slurmd
```

#### Verify from `login-node`

```bash
sinfo
scontrol show nodes
```

---

## Step 6: Test cluster

From the head node:

```bash
sinfo
scontrol show nodes
```

Run a test job:

```bash
srun hostname
sbatch test.sh
```

---

