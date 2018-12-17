---
title: "R Markdown and Leaflet"
author: "Bekir YILDIZ"
date: "December 17, 2018"
output:
  html_document:
    keep_md: true
---



### Introduction
Create a web page using R Markdown that features a map created with Leaflet.

Host your webpage on either GitHub Pages, RPubs, or NeoCities.

Your webpage must contain the date that you created the document, and it must contain a map created with Leaflet. We would love to see you show off your creativity!

### Data plotted
The datasource used is from http://worldpopulationreview.com/countries/turkey-population/cities/

It shows the top five populated cities in Turkey.


```r
if(Sys.info()['sysname'] == "Windows") 
{
  setwd("D:/Dropbox (GSC)/SHELTERNFI IM/RScripts/Test/")
} else 
{
  setwd("/Users/bekir/Dropbox (GSC)/SHELTERNFI IM/RScripts/Test/")
}

library("leaflet")
```

```
## Warning: package 'leaflet' was built under R version 3.4.4
```

```r
data <- read.csv(file="City.csv", header=TRUE)
head(data)
```

```
##   No      City Population Latitude Longitude
## 1  1  Istanbul   14804116  41.0053   28.9770
## 2  2    Ankara    3517182  39.9208   32.8541
## 3  3     Izmir    2500603  38.4189   27.1287
## 4  4     Adana    1248988  37.0000   35.3213
## 5  5 Gaziantep    1065975  37.0662   37.3833
```

```r
map <- data %>%
        leaflet() %>%
        addTiles() %>%
        setView(lng = 35.2433, lat = 38.9637, zoom = 5) %>%
        addMarkers(popup = paste("City: ", data$City, "<br>",
                                 "Population: ", data$Population), 
        lng = data$Longitude, lat = data$Latitude)%>% 
        addCircles(weight=1,radius=data$Population/100)
```

```
## Assuming "Longitude" and "Latitude" are longitude and latitude, respectively
```

```r
map
```

<!--html_preserve--><div id="htmlwidget-81af9a3b1a5b04fa2c27" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-81af9a3b1a5b04fa2c27">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":1,"detectRetina":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap<\/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA<\/a>"}]},{"method":"addMarkers","args":[[41.0053,39.9208,38.4189,37,37.0662],[28.977,32.8541,27.1287,35.3213,37.3833],null,null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},["City:  Istanbul <br> Population:  14804116","City:  Ankara <br> Population:  3517182","City:  Izmir <br> Population:  2500603","City:  Adana <br> Population:  1248988","City:  Gaziantep <br> Population:  1065975"],null,null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]},{"method":"addCircles","args":[[41.0053,39.9208,38.4189,37,37.0662],[28.977,32.8541,27.1287,35.3213,37.3833],[148041.16,35171.82,25006.03,12489.88,10659.75],null,null,{"interactive":true,"className":"","stroke":true,"color":"#03F","weight":1,"opacity":0.5,"fill":true,"fillColor":"#03F","fillOpacity":0.2},null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null,null]}],"setView":[[38.9637,35.2433],5,[]],"limits":{"lat":[37,41.0053],"lng":[27.1287,37.3833]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


