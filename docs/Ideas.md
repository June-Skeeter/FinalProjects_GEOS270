---
layout: default
title: Project Ideas
nav_order: 2
---

# Project Ideas
{: .no_toc }

The ideas listed below are meant as a starting point, you should flush them out and come up with a suitable approach to analyze the problem.  You are also free develop your own project idea.  I suggest you focused on BC/Vancouver just because we are more familiar with local data sources.  You are free to explore other geographical regions as well, but be advised that we may not be able to privide as much assistance with searching for data.


1. TOC
{:toc}

Project Ideas 
 

# Helpful Data Sources

[Simply Analytics](https://resources.library.ubc.ca/page.php?id=1044)

[Data BC](https://data.gov.bc.ca/)
* Some downloads from this site require you to filter by [Map sheets](https://open.canada.ca/data/en/dataset/055919c2-101e-4329-bfd7-1d0c333c0e62)

[City of Vancouver Data Portal](https://opendata.vancouver.ca/pages/home/)

[Hectares BC](https://www.hectaresbc.org/app/habc/HaBC.html?type=raster&query=climatenormal.map)
* Sometimes students have trouble with downloads from this site.  If your download won't process, feel free to reach out.

[Google Earth Engine](https://developers.google.com/earth-engine/datasets/)
* There are lots of datasets on here we haven't covered, so take a bit of time to explore
* If you'd like a dataset from here, please email me.  I'm happy to help facilitate downloading it.
	* Do not wait until the last minute to contact me asking for help with a download.
* This code can be used to download a DEM from google earth, similar to what we did in Module 3.  But make sure to upload an appropriate boundary file first.  You can reference Module 3

```javascript
var dataset = ee.ImageCollection('NRCan/CDEM').mean();//lterBounds(Boundary);
var elevation = dataset.select('elevation');
var elevationVis = {
  min: -50.0,
  max: 1500.0,
  palette: ['0905ff', 'ffefc4', 'ffffff'],
};


Map.centerObject(Boundary)
Map.addLayer(Boundary)
Map.addLayer(elevation, elevationVis, 'Elevation');

// Export to Google drive
Export.image.toDrive({
  image: elevation,
  description: 'DEM',
  scale: 25,
  region: Boundary
});
````




# Possible Projects

## Access to green space and bicycle infrastructure in Vancouver 
 
**Scenario**: Access to green space and bicycle infrastructure is important for quality of life in urban areas, promoting physical and mental health.  Yet, green space and bike infrastructure are often inequitably distributed around cities. Explore the distribution of green space and bicycle infrastructure in Vancouver in relation to wealth, housing density, transit, etc.  Check out the 
[City of Vancouver Data Portal](https://opendata.vancouver.ca/pages/home/) for data on parks, bicycle lanes, bike racks, trees, etc. that might be useful.  It could also be helpful to incorporate some census data.	
 
Possible Analysis to consider
* Geocoding
* Tabular joins 
* Select by location/attribute
* Buffering to gauge accessibility 
* Intersections to count # bike racks, area of parks, length of bike lanes within census units 
* Data Classification  
 

## Mapping Police Violence
 
Use this dataset of [Police Involved Deaths in Canada](https://police-involved-deaths-ca.github.io/Data/) to map incidents of police violence in a specific region of your choice.  You can choose a province (eg. Saskatchewan), or a specific city (eg. Toronto).  Use census data to complement the analysis.  If you choose this project, you can reach out directly to me for more information on the data.

Possible Analysis to consider 
* Geocoding
* Point in Polygon Analysis
* Data Normalization
* Data classification

## Possible Locations for a Ski Resort

Define a boundary region and download a DEM & other necessary data.  You can use google earth engine to download a DEM as shown above.  Some files from DataBc that might be helpful include [Old Growth Forests](https://catalogue.data.gov.bc.ca/dataset/old-growth-management-areas-legal-current#edc-pow) &  [Streams](https://catalogue.data.gov.bc.ca/dataset/freshwater-atlas-stream-network)

Possible Analysis to consider   
* Slope, Aspect, & Reclassify
* Weighted Overlay or Raster Calculator
* Proximity Analysis


## Landslides in Burn Zones 

Forest fires are also some of the worst natural disasters impacting the province.  Climate change and human activity are changing fire dynamics and leading to costlier fire seasons.  After severe fires, intense precipitation events can trigger landslides.  The burn severity data is available for 2015-2019 for BC.  Select a [Fire Center](https://catalogue.data.gov.bc.ca/dataset/bc-wildfire-fire-centres) (I suggest not doing Coastal Fire Centre).   Find an area that has been impacted by significant fire activity. Use DEM data (google earth) to calculate slope and combine with burn severity and precipitation (hectares bc) to create landslide risk classification.  


Possible Analysis to consider   
* Slope & Reclassify
* Weighted Overlay or Raster Calculator
* Proximity Analysis


## Air Quality in BC 

Poor air quality is a significant health risk for vulnerable populations.  Over recent years there have been serious smoke events impacting air quality province wide.  Additionally, traffic and industrial activities exacerbate air quality issues in urban areas.   
Download census data for the Lower Mainland.  Download and analyze the [air quality data](https://github.com/June-Skeeter/BCAirQuality) (PM 2.5 is the most important for health, but you should also look at one or two other pollutants of interest).  Look at how air quality changes across the region, either monthly or annually.  Are there significant at risk populations (youth and seniors) who might be negatively impacted by air quality?  You will also need the air [quality stations](https://catalogue.data.gov.bc.ca/dataset/air-quality-monitoringunverified-hourly-air-quality-and-meteorologicaldata/resource/7fd21841-b133-4f39-b9b2-6bfa34a7cf6c) for this analysis.
 
Possible Analysis to consider  
* Import tabular (x,y) data 
* Calculating Fields
* Inverse Distance Weighting
* Zonal statistics 
* Tabular joins

