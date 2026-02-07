# 👤 Profile
<img src="https://i.imgur.com/6FshBBs.png" width="100" style="border-radius;" />
My name is Xavier William, I am an Indonesian undergraduate student at the University of Toulouse Jean-Jaurès, where I study Geography, Spatial Planning, and Environmental Studies. My interests include geomatics, GIS, and geospatial data analysis.

## 💻 Specialties 
![Google Earth](https://img.shields.io/badge/Google%20Earth-4285F4?style=for-the-badge&logo=google-earth&logoColor=white)
![QGIS](https://img.shields.io/badge/QGIS-589632?style=for-the-badge&logo=qgis&logoColor=white)
![SketchUp](https://img.shields.io/badge/SketchUp-005F9E?style=for-the-badge&logo=sketchup&logoColor=white)
![ArcGIS](https://img.shields.io/badge/ArcGIS-F57F20?style=for-the-badge&logo=arcgis&logoColor=white)
![Python](https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![JavaScript](https://img.shields.io/badge/JavaScript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![SQL](https://img.shields.io/badge/SQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Photoshop](https://img.shields.io/badge/Photoshop-31A8FF?style=for-the-badge&logo=adobe-photoshop&logoColor=white)

## 🗣️ Languages
![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8%20English-1F77B4?style=for-the-badge)
![🇫🇷 French](https://img.shields.io/badge/%F0%9F%87%AB%F0%9F%87%B7%20French-F03C5B?style=for-the-badge)
![🇨🇳 Mandarin](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3%20Mandarin-FFCD00?style=for-the-badge)
![🇮🇩 Indonesian](https://img.shields.io/badge/%F0%9F%87%AE%F0%9F%87%A9%20Indonesian-DA251D?style=for-the-badge)

# 🗂️ Portfolio
A personal collection of geospatial projects analyzing environmental and socio-economic disparities across territories, using maps and analytical diagrams to explore spatial patterns, global issues, and GIS methodologies.
## Overview
- [Lyon Healthcare Accessibility](#lyon-healthcare-accessibility)
- [Warsaw Public Transport](#warsaw-public-transport)
- [North American Biomes](#north-american-biomes)
- [U.S. Wildfires](#us-wildfires) 
- [Continental U.S. Tornadoes](#continental-us-tornadoes)

## Lyon Healthcare Accessibility
<p align="center">
    <img src="pharm_distrib_lyon.png" alt="Pharmacies in Lyon Metropole" width="600">
  <br>
</p>

<p align="center">
    <img src="hosp_distrib_lyon.png" alt="Hospitals in Lyon Metropole" width="600">
  <br>
</p>

<p align="center">
    <img src="health_density_lyon.png" alt="Healthcare Establishment Density Lyon" width="600">
  <br>
</p>

<p align="center">
    <img src="demographics_lyon.png" alt="Demography Lyon Metropole" width="600">
  <br>
</p>

#### 1. Pharmacy Index
$$\text{Pharmacy Index} = \begin{cases} 0 & \text{if pharmacy count} = 0 \\ \frac{\text{pharmacy count}}{\text{population}} \times 1000 & \text{otherwise} \end{cases}$$

`CASE WHEN "pharm_count" = 0 THEN 0 ELSE ("pharm_count" / "population") * 1000 END`

#### 2. Hospital Index
$$\text{Hospital Index} = \begin{cases} 0 & \text{if hospital count} = 0 \\ \frac{\text{hospital count}}{\text{population}} \times 10000 & \text{otherwise} \end{cases}$$

`CASE WHEN "hosp_count" = 0 THEN 0 ELSE ("hosp_count" / "population") * 10000 END`

</p>

#### 3. Spatial Coverage Index
$$\text{Spatial Coverage} = \begin{cases} 0 & \text{if (pharmacy count + hospital count)} = 0 \\ \frac{\text{pharmacy count} + \text{hospital count}}{\text{area km}^2} & \text{otherwise} \end{cases}$$

`CASE WHEN ("pharm_count" + "hosp_count") = 0 THEN 0 ELSE ("pharm_count" + "hosp_count") / "area_km2" END`

</p>

#### 4. Healthcare Access Index
$$
\begin{aligned}
\text{Access Index} \ &= 0.50 \times \left( \frac{\text{hospital index} - \min(\text{hospital index})}{\max(\text{hospital index}) - \min(\text{hospital index})} \times 100 \right) \\
& + 0.35 \times \left( \frac{\text{pharmacy index} - \min(\text{pharmacy index})}{\max(\text{pharmacy index}) - \min(\text{pharmacy index})} \times 100 \right) \\
& + 0.15 \times \left( \frac{\text{spatial coverage} - \min(\text{spatial coverage})}{\max(\text{spatial coverage}) - \min(\text{spatial coverage})} \times 100 \right)
\end{aligned}
$$

`(
  0.50 * (("hosp_index" - minimum("hosp_index")) / (maximum("hosp_index") - minimum("hosp_index")) * 100) +
  0.35 * (("pharm_index" - minimum("pharm_index")) / (maximum("pharm_index") - minimum("pharm_index")) * 100) +
  0.15 * (("spatial_cov_index" - minimum("spatial_cov_index")) / (maximum("spatial_cov_index") - minimum("spatial_cov_index")) * 100)
)`

#### 5. Healthcare Access Score
$$\text{Access Score} = \begin{cases} 
   \text{No Facilities} & \text{if pharmacy count} = 0 \land \text{hospital count} = 0 \\
   \text{Very Low} & \text{if } 0 < \text{access index} \leq 15 \\
   \text{Low} & \text{if } 15 < \text{access index} \leq 25 \\
   \text{Moderate} & \text{if } 25 < \text{access index} \leq 35 \\
   \text{High} & \text{if } 35 < \text{access index} \leq 45 \\
   \text{Very High} & \text{if access index} > 45
   \end{cases}$$

`CASE WHEN "pharm_count" = 0 AND "hosp_count" = 0 THEN 'No Facilities' WHEN "access_index" <= 15 THEN 'Very Low' WHEN "access_index" <= 25 THEN 'Low' WHEN "access_index" <= 35 THEN 'Moderate' WHEN "access_index" <= 45 THEN 'High' ELSE 'Very High' END`
</p>
<br>

<p align="center">
    <img src="access_score_lyon.png" alt="Healthcare Access Lyon Metropole" width="600">
  <br>
</p>

## Warsaw Public Transport
<p align="center">
    <img src="warsaw_transport_map.png" alt="Public Transport Map Warsaw" width="600">
  <br>
</p>

<p align="center">
    <img src="warsaw_bus.png" alt="Bus Map Warsaw" width="600">
  <br>
</p>

<p align="center">
    <img src="warsaw_demographics.png" alt="Demographics Warsaw" width="600">
  <br>
</p>


<p align="center">
    <img src="warsaw_stops_density.png" alt="Stops Density Comparison Warsaw" width="900">
  <br>
</p>

### Indices Formulas to Calculate Public Transport Adequacy Score

#### 1. Bus Index

$$\text{Bus Index} = \begin{cases} 0 & \text{if bus count} = 0 \\ \frac{\text{bus count}}{\text{population}} \times 10000 & \text{otherwise} \end{cases}$$

`CASE WHEN "bus_count" = 0 THEN 0 ELSE ("bus_count" / "population") * 10000 END`

#### 2. Tram Index

$$\text{Tram Index} = \begin{cases} 0 & \text{if tram count} = 0 \\ \frac{\text{tram count}}{\text{population}} \times 10000 & \text{otherwise} \end{cases}$$

`CASE WHEN "tram_count" = 0 THEN 0 ELSE ("tram_count" / "population") * 10000 END`
</p>

#### 3. Metro Index

$$\text{Metro Index} = \begin{cases} 0 & \text{if metro count} = 0 \\ \frac{\text{metro count}}{\text{population}} \times 10000 & \text{otherwise} \end{cases}$$

`CASE WHEN "metro_count" = 0 THEN 0 ELSE ("metro_count" / "population") * 10000 END`

#### 4. Rail Index 

$$\text{Rail Index} = \begin{cases} 0 & \text{if rail count} = 0 \\ \frac{\text{rail count}}{\text{population}} \times 10000 & \text{otherwise} \end{cases}$$

`CASE WHEN "rail_count" = 0 THEN 0 ELSE ("rail_count" / "population") * 10000 END`
</p>

#### 5. Public Transport Index 

$$
\begin{aligned}
\text{Public Transport Index} \ &= 0.30 \times \left( \frac{\text{metro index} - \min(\text{metro index})}{\max(\text{metro index}) - \min(\text{metro index})} \times 100 \right) \\
& + 0.25 \times \left( \frac{\text{rail index} - \min(\text{rail index})}{\max(\text{rail index}) - \min(\text{rail index})} \times 100 \right) \\
& + 0.25 \times \left( \frac{\text{tram index} - \min(\text{tram index})}{\max(\text{tram index}) - \min(\text{tram index})} \times 100 \right) \\
& + 0.20 \times \left( \frac{\text{bus index} - \min(\text{bus index})}{\max(\text{bus index}) - \min(\text{bus index})} \times 100 \right)
\end{aligned}
$$

`(
  0.30 * (("metro_index" - minimum("metro_index")) / (maximum("metro_index") - minimum("metro_index")) * 100) +
  0.25 * (("rail_index" - minimum("rail_index")) / (maximum("rail_index") - minimum("rail_index")) * 100) +
  0.25 * (("tram_index" - minimum("tram_index")) / (maximum("tram_index") - minimum("tram_index")) * 100) +
  0.20 * (("bus_index" - minimum("bus_index")) / (maximum("bus_index") - minimum("bus_index")) * 100)
)`

#### 6. Public Transport Adequacy Grade

$$\text{Transport Score} = \begin{cases} 
   \text{Very Low} & \text{if access index} \leq 20 \\
   \text{Low} & \text{if } 20 < \text{access index} \leq 35 \\
   \text{Moderate} & \text{if } 35 < \text{access index} \leq 50 \\
   \text{High} & \text{if } 50 < \text{access index} \leq 65 \\
   \text{Very High} & \text{if access index} > 65
   \end{cases}$$

`CASE WHEN "access_index" <= 20 THEN 'Very Low' WHEN "access_index" <= 35 THEN 'Low' WHEN "access_index" <= 50 THEN 'Moderate' WHEN "access_index" <= 65 THEN 'High' ELSE 'Very High' END`
</p>
<br>

<p align="center">
    <img src="adequacy_transport_warsaw.png" alt="Transport Adequacy Warsaw" width="900">
  <br>
</p>

## North American Biomes
<p align="center">
    <img src="BIOMES_NA.PNG" alt="North America Biomes" width="600">
  <br>
</p>

I developed this map first to illustrate North America’s principal biomes using Level I Ecoregion data, providing environmental context for the continent’s natural phenomena and demographic patterns. Biome boundaries are displayed alongside national administrative divisions, including Canadian provinces, U.S. states, and Mexican *estados.* The continent encompasses a wide range of biomes. Firstly, the Arctic Cordillera and tundra dominate the far north, with cold, arid polar conditions, while Canada’s expansive boreal forests exist under subarctic climates. Secondly, the northeastern United States is characterized by eastern temperate forests, and the central Great Plains feature grasslands across semi-arid to temperate climatic zones. Thirdly, western regions include Pacific coastal forests with marine climates, mountainous northwestern forests spanning multiple elevations, and California’s Mediterranean zone. Lastly, the Southwest features hot, dry deserts, while southern Mexico hosts tropical wet-dry forests, temperate mountain ranges, and semi-arid plateau regions.

## U.S. Wildfires
<p align="center">
    <img src="conus_wf.png" alt="CONUS Wildfires" width="600">
  <br>
</p>

<p align="center">
    <img src="alaska_wf.png" alt="Alaska Wildfires" width="600">
  <br>
</p>

<p align="center">
    <img src="fire_prop.png" alt="Wildfire Proportion" width="400">
  <br>
</p>

<p align="center">
    <img src="fire_events.png" alt="Wildfire Events" width="400">
  <br>
</p>

<p align="center">
    <img src="fire_surface.png" alt="Wildfire Surface" width="400">
  <br>
</p>

<p align="center">
    <img src="fire_percentage.png" alt="Wildfire Percentage" width="400">
  <br>
</p>

## Continental U.S. Tornadoes

I chose tornadoes as my next primary topic to analyze the spatial distribution of another major natural disaster in the United States, as it highlights the regions that are particularly vulnerable to severe weather. Tornado data were gathered from the National Oceanic and Atmospheric Administration (NOAA), whose records date back to 1950, but the analysis was limited to 2004 - 2024 to reflect improvements in detection technology and reporting accuracy.

<br>
<p align="center">
    <img src="tor_pts.PNG" alt="Tornado points" width="600">
  <br>
    <em>Figure 3.a</em>
</p>

Tornado activity follows a distinct spatial pattern shaped by atmospheric circulation and topography. Hotspots develop where warm, moist air from the Gulf of Mexico interacts with cooler, drier air and strong wind shear, while activity declines sharply in the western United States due to mountainous terrain and less favorable atmospheric conditions. Tornado intensity is classified using the Enhanced Fujita (EF) scale, which ranks events from EF0 (weakest) to EF5 (strongest) based on estimated wind speeds and damage.
* Dense clustering in Oklahoma, Kansas, Nebraska, and southeastern states (Mississippi, Alabama)
* Minimal tornado presence in western states
* EF0 - EF1 events are most numerous, while stronger events are more dispersed
* Points cover roughly two-thirds of the continental U.S., primarily east of the Rocky Mountains

<br>

<p align="center">
    <img src="tor_tracks.PNG" alt="Tornado Tracks" width="600">
  <br>
    <em>Figure 3.b</em>
</p>
This map highlights tornado movement across multiple states, showing both the typical southwest-to-northeast trajectory and variations. It was created by combining the initial and terminal points of each tornado based on their latitude and longitude. Incorporating EF levels along the full tornado tracks provides greater analytical insight than mapping them solely at the initial points, as it allows identification of regions that are more vulnerable to severe tornado impacts.
The tornado tracks show strong, consistent linearity, reflecting the steering influence of mid-latitude westerlies and cold fronts.
</p>

* Consistent influence of mid-latitude westerlies and cold fronts
* Southeast territories have higher concentration of long-track events
* Tracks sometimes form clusters, e.g., North Dakota - Minnesota and parts of the East Coast

<br>
<p align="center">
    <img src="tor_dens.PNG" alt="Tornado Density" width="600">
  <br>
    <em>Figure 3.c</em>
</p>
I created this kernel density map using kernel density estimation (KDE), incorporating both tornado initial points and their tracks. The estimation was also weighted by each tornado’s EF level. This approach produces gradual transitions in tornado density and reveals a strong east–west contrast, with the highest concentrations across the central interior of the United States and much lower densities in the mountainous and coastal regions in the western states.
</p>

* Tornady activity core is centered in the central United States and gradually expands outward into the Southeast
* The Northeast, upper Midwest, and Florida exhibit generally low to moderate densities, with no persistent core activity
* Very low tornado density dominates much of the western United States, particularly across mountainous and coastal regions
* Small, localized clusters of low-level tornado density appear in parts of the western U.S.
<br>
 <p align="center">
    <img src="tor_bar_1.png" alt="Tornado Bar 1" width="400">
     <br>
    <em>Figure 3.d</em>
</p>
This diagram ranks the ten U.S. states with the highest tornado activity over the past two decades, highlighting notable geographic patterns in severe weather occurrence. Tornado events were compiled in Microsoft Excel by summing all occurrences for each state and ranking them accordingly. Texas emerges as a clear outlier with 2,334 recorded events, exceeding the second-ranked state, Kansas, with 1,637 occurrences by a substantial margin. Notably, almost all of these states recorded over 1,000 tornadoes during this period, illustrating the widespread distribution of tornado activity across the Central and Southern United States. Key highlights include:
</p>

* Texas recorded the highest total number of tornadoes (2,334 events)
* Kansas follows with 1,637 tornadoes
* States like Mississippi (1,367 events) and Alabama (1,360 events) rank in the top four, showing that significant tornado activity also occurs outside the traditional "Tornado Alley"
* Nine of the top ten states exceeded 1,000 tornadoes during this period, demonstrating the broad spatial distribution of severe weather

<br>

<p align="center">
    <img src="tor_bar_2.png" alt="Tornado Bar 2" width="400">
    <br>
    <em>Figure 3.e</em>
</p>
This diagram interprets the distribution of only high-intensity tornadoes (EF3-EF5) across the United States, highlighting regional differences in severe tornado occurrence. State-level rankings were generated by filtering tornado event data in Microsoft Excel based on intensity and summing total events per state. Key observations include:
</p>

* Kansas and Texas recorded the highest number of high-intensity tornadoes, with 60 events each.
* Mississippi followed closely with 58 events.
* Arkansas appears among the top ten with 27 events, despite not ranking among the states with the highest overall tornado counts.
* Several states with high total tornado activity, including Illinois, Louisiana, and Florida, are absent from this high-intensity ranking.
<br>

<p align="center">
    <img src="tor_prop_1.png" alt="Tornado Donut 1" width="400">
    <br>
    <em>Figure 3.f</em>
</p>
Tornado activity is dominated by low-intensity events, with EF0 and EF1 ratings accounting for the vast majority of occurrences. In contrast, EF2 and higher-intensity tornadoes are rare, highlighting the relative scarcity of the most severe storms in the overall dataset.
     <p>
         
<p align="center">
    <img src="tor_prop_2.png" alt="Tornado Donut 1" width="400">
  <br>
    <em>Figure 3.g</em>
</p>
Within high-intensity tornadoes, EF3 events dominate, while EF4 and EF5 occurrences are comparatively rare. This highlights that even among severe storms, the most extreme tornadoes are uncommon, making them critical points of study for risk assessment and mitigation.
    </p>
<br>
