---
layout: post
title: "ADS-B Aircraft Tracking Dashboard"
tags: ["python", "streamlit", "data-viz", "plotly"]
summary: "A live monitoring dashboard for a home ADS-B receiver — tracking, visualizing, and reporting on aircraft traffic in real time."
---

<div style="display: flex; gap: 10px; align-items: flex-end;">
  <div style="flex: 1;">
    {% include image2.html image="projects/adsb/dist.png" max_width="100%" %}
  </div>
  <div style="flex: 1;">
    {% include image2.html image="projects/adsb/map.png" max_width="100%" %}
  </div>
</div>

A live monitoring dashboard for a home ADS-B receiver. Tracking, visualizing, and reporting on aircraft traffic in real time.
Built with **Streamlit**, **Plotly**, and **Altair**, backed by a local SQLite database of full position reports.
 <a href="https://github.com/gpierobon/ADSBtracking" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>

Check out a [Live Demo](https://adsbtracking.streamlit.app).
 


#### Features

- **Live KPIs** — aircrafts tracked, position reports, busiest/quietest day, etc. 
- **Traffic over time** — time series of position reports and unique aircraft
- **Carrier breakdown** — filtering across domestic airlines, private, and international traffic, with matching pie charts and distribution overlays
- **Spatial analysis** — altitude and distance distributions a density heatmap of detected aircraft positions
- **Leaderboards** — most-seen aircrafts and route-level rankings 


---

#### The setup

<div class="image-container" style="display: flex; align-items: flex-start; gap: 1.5rem; flex-wrap: wrap;"> <div style="max-width: 30%;"> {% include image2.html image="projects/adsb/antenna.png" max_width='100%' %} </div> <div style="flex: 1; min-width: 200px;"> <p><strong>Hardware</strong></p> <ul> <li><strong>Raspberry Pi 4</strong> (1GB)</li> <li><strong>RTL-SDR V3</strong> USB dongle</li> <li>Multipurpose Dipole Antenna (tuned to 1090 MHz)</li> </ul> </div> </div>


