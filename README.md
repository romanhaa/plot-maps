# Plot maps

## Maps

### Braunschweig (DE)
[![RLB-01](braunschweig/rlb-01/map_thumbnail.jpg)](braunschweig/rlb-01/README.md)

## Trieste (IT)

[![RDS-01](trieste/rds-01/map_decorated_thumbnail.jpg)](trieste/rds-01/README.md)
[![RLB-01](trieste/rlb-01/map_thumbnail.jpg)](trieste/rlb-01/README.md)

## Nomenclature

- `RDS`: roads
- `RLB`: roads, landscape, buildings

## Create thumbnails

```sh
for IMAGE in $(find . -type f -name "*_full.png"); do
  FILE=$(echo "$IMAGE" | sed 's/_full.png//g')
  sips -s format jpeg $IMAGE --out ${FILE}_thumbnail.jpg --resampleHeight 300 -s formatOptions 80
  sips -s format jpeg $IMAGE --out ${FILE}_large.jpg --resampleWidth 1000 -s formatOptions 80
done
```
