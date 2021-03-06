Braunschweig - RDS-02
================

## Result

![Map](map_large.jpg)

## Code

Load packages.

``` r
library(glue)
library(sf)
library(foreign)
library(tidyverse)
library(lwgeom)
library(stringi)
options(stringsAsFactors = FALSE)
```

Cut geographical map of Niedersachsen to the area of Braunschweig.
Cutting a smaller box and adjusting the part of the map we want is a lot
faster than cutting it from the entire Niedersachsen map.

``` r
bbox_coordinates <- st_bbox(c(
  xmin = 10.4407,
  ymin = 52.2168,
  xmax = 10.6188,
  ymax = 52.3204
))
```

Load `.shp` files for region, crop to the area we want to plot, and
store the cropped data for quicker access later.

Skip this step if the data already exists and load it instead.

``` r
map_dir <- 'niedersachsen-latest-free/'
if ( !file.exists('bbox.rds') ) {
  bbox_data <- list(
    coordinates = bbox,
    buildings_a = read_sf(glue('{map_dir}/gis_osm_buildings_a_free_1.shp')) %>% st_crop(bbox_coordinates),
    landuse_a = read_sf(glue('{map_dir}/gis_osm_landuse_a_free_1.shp')) %>% st_crop(bbox_coordinates),
    railways = read_sf(glue('{map_dir}/gis_osm_railways_free_1.shp')) %>% st_crop(bbox_coordinates),
    roads = read_sf(glue('{map_dir}/gis_osm_roads_free_1.shp')) %>% st_crop(bbox_coordinates),
    water_a = read_sf(glue('{map_dir}/gis_osm_water_a_free_1.shp')) %>% st_crop(bbox_coordinates)
  )
  saveRDS(bbox_data, 'bbox.rds')
} else {
  bbox_data <- readRDS('bbox.rds')
}
```

Define recurring theme parameters.

``` r
blankbg <- theme(
  axis.line = element_blank(),
  axis.text.x = element_blank(),
  axis.text.y = element_blank(),
  axis.ticks = element_blank(),
  axis.title.x = element_blank(),
  axis.title.y = element_blank(),
  panel.background = element_blank(),
  panel.border = element_blank(),
  panel.grid.major = element_blank(),
  panel.grid.minor = element_blank(),
  plot.background = element_blank()
)
```

Define which elements we want to be plotted in the different categories.

``` r
railways <- c('rail','subway')
roads_small <- c('living_street','unclassified','service','residential')
roads_tertiary <- c('tertiary','tertiary_link')
roads_secondary <- c('secondary','secondary_link')
roads_primary <- c('primary','primary_link','motorway','motorway_link','trunk','trunk_link')
```

Assign colors to different element categories.

``` r
color_roads <- 'white'
color_background <- '#bc213f'
```

Plot map.

``` r
p <-
  ggplot() +
  geom_sf(data = bbox_data$roads %>% dplyr::filter(fclass %in% roads_small),
          color = color_roads, size = 0.15) +
  geom_sf(data = bbox_data$railways %>% dplyr::filter(fclass %in% railways),
          color = color_roads, size = 0.15) +
  geom_sf(data = bbox_data$roads %>% dplyr::filter(fclass %in% roads_tertiary),
          color = color_roads, size = 0.4) +
  geom_sf(data = bbox_data$roads %>% dplyr::filter(fclass %in% roads_secondary),
          color = color_roads, size = 0.5) +
  geom_sf(data = bbox_data$roads %>% dplyr::filter(fclass %in% roads_primary),
          color = color_roads, size = 0.6) +
  blankbg +
  theme(plot.background = element_rect(fill = color_background, color = NA)) +
  coord_sf(
    xlim = bbox_data$coordinates[c(1,3)],
    ylim = bbox_data$coordinates[c(2,4)],
    expand = FALSE
  )
```

Save map as PNG and PDF.

``` r
ggsave(
  'map_full.png',
  p, scale = 1, width = 20, height = 20, units = 'cm', dpi = 250
)
ggsave(
  'map_full.pdf',
  p, scale = 1, width = 20, height = 20, units = 'cm'
)
```

## Resources

-   [Map of
    Niedersachsen](http://download.geofabrik.de/europe/germany/niedersachsen.html)
    was downloaded from [Geofabrik](https://www.geofabrik.de)
