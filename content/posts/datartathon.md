---
title: "DAT/Artathon EcoRisk Forecasts - California DataViz."
date: 2021-08-09
katex: true
markup: "mmark"
---

# DAT/Artathon EcoRisk Forecasts - California DataViz

As featured in D/A's gallery: [https://datartathon.com/projects/2021-daniel-ecorisk-california](https://datartathon.com/projects/2021-daniel-ecorisk-california)

Made with the support of the [Risk & Resilience DAT/Artathon 2021](https://datartathon.com).

---

“EcoRisk California” visualizes climate change impacts for three of the West Coast’s most beloved tree species during the 21st century. The motion-graphics storyboard visualizes shifts within three species distributions across spatial and climate dimensions, exploring relationships between ecological risk and habitat suitability. To facilitate future experiments, the study is accompanied by an open-sourced Python package containing the class for semi-automated machine learning used in the visualization. 

<img src="/research-outputs/datartathon/knitted-files/ecorisk-vertical-1.png" style="border:0px;margin:0px" alt="vertical 1"/><!--
--><img src="/research-outputs/datartathon/knitted-files/ecorisk-vertical-2.gif" style="border:0px;margin:0px" alt="vertical 2"/><!--
--><img src="/research-outputs/datartathon/knitted-files/ecorisk-vertical-3.png" style="border:0px;margin:0px" alt="vertical 3"/>
<br>


Prior work reveals that species distributions have the potential to shift dramatically across the landscape due to environmental conditions. In this study, a species distribution is defined as the natural range that a species occupies in space at a given time, spanning its realized suitable habitat. Climate change was measured across nineteen bioclimatic features, which together approximate the climatic envelope of relevance to ecological species at a given location within the study area. Climate change impacts may prove to significantly harm California’s ecosystems across the 21st century, threatening to decrease biodiversity in its rich natural corridors. Furthermore, the severity of climate change will likely vary across the state, both due to climatic differences and biophysical ecosystem variation. For example, past and ongoing shifts in the Joshua tree distribution inferred from fossil records reveal that their late Pleistocene distribution (20,000–13,000 BC) was significantly larger than their natural range today. This habitat loss is likely a result of many environmental conditions, including changes in climate, inter-species interactions, and resource availability, as well as discrete instances of natural disasters. Another worrisome impact from a warmer, drier climate is the heightened risk of wildfire. Fire ecologists have shown that Giant sequoia strands have endured more wildfires in the last five years than the entire proceeding century, evidence that climate change has a more severe impact on climate extremes compared to climate averages. 

In this research, I argue that better understanding ecosystem risks facilitates effective biodiversity conservation and better land management. The classification experiment explores how climate features are associated with the three study species distributions. The machine learning inferences forecast a positive association between the magnitude of climate change and the magnitude of future habitat degradation, a result which confirmed the models were working as expected. I then tested whether the magnitude of habitat degradation is more variable at fine-grained scales relative to coarse-grained scales, assuming that the species are limited in dispersal to novel areas. For example, I found that nearly the entire Coast redwood distribution South of San Francisco and North of Big Sur is predicted to shift underlying climate envelope by 2061-2080; yet, coast redwoods fared best on coarser scales relative to Giant sequoias and Joshua trees. Overall, the forecasts reveal a number of macroscopic patterns including future shifts northward for Coast Redwoods and Joshua trees and southward for Giant sequoias.

Equipped with rapidly expanding databases and computational tools, scientists have the potential to integrate accessible and communicable insights in biodiversity conservation, ultimately improving land management strategy and decision-making.



**Code:**

* [Git Repo](https://github.com/daniel-furman/PySDMs)

**Sources:**

* [NYT CA Fires](https://www.nytimes.com/interactive/2020/12/09/climate/redwood-sequoia-tree-fire.html?)<br>
* [IPCC AR6 Report](https://www.ipcc.ch/report/ar6/wg1/)
* [WorldClim2.1](https://www.worldclim.org/data/worldclim21.html)<br>
* [CMIP6 Global Climate Models](https://www.worldclim.org/data/cmip6/cmip6climate.html#)<br>
* [Global Biodiversity Information Facility](https://www.gbif.org)<br>
  
**Data Citations:**
  
* Coast redwood: GBIF.org (2 August 2021) GBIF Occurrence https://doi.org/10.15468/dl.4qgr62
* Giant sequoia: GBIF.org (2 August 2021) GBIF Occurrence https://doi.org/10.15468/dl.baww96
* Joshua tree: GBIF.org (01 November 2020) GBIF Occurrence https://doi.org/10.15468/dl.g6swrm

I used free and open access databases for “EcoRisk Forecasts - California'', with species presence records sourced from the Global Biodiversity Information Facility (gbif.org) and climate features sourced from Worldclim v2.1 (wordclim.org). 

Species presence records were cleaned by multiple steps of preprocessing. Incorrectly classified presences were identified with google earth satellite imagery, primarily locations within urban and suburban areas or presences beyond the species natural range. The records were then grid-sampled to remove spatial biases inherent to survey-based ecological research, with a particular ratio of presences accepted per raster pixel (2.5 arcminutes resolution). Lastly, a balanced binary classification experiment between species presences (1.0) and pseudo-absences (0.0) was initialized by randomly sampling background points and filtering likely false positives drawn within a close proximity to species presences.

Climate features consisted of nineteen bioclimatic features and were represented in spatial rasters at a resolution of 2.5 arcminutes, both with near-current and future time periods scraped across thousands of scenarios. The rasters were cropped to the spatial extent of the given species and written to file as GeoTIFFs. Future climate data were smoothed by taking the average of seven different Global Climate Models, each validated by the most recently updated World Climate Research Programme (CMIP6). These models represented the “regional rivalry” Shared Socio-Economic pathway (SSP3), a narrative centered on a resurgence of nationalism and a focus on competitiveness and security concerns in the 21st century. Lastly, we extracted the nineteen bioclimate features per location of species presence and pseudo-absence from the above pre-processing.


