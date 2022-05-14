# Plot maps

## Maps

### Braunschweig (DE)

#### BLD

[![BLD-01](braunschweig/bld-01/map_thumbnail.jpg)](braunschweig/bld-01/README.md)
[![BLD-02](braunschweig/bld-02/map_thumbnail.jpg)](braunschweig/bld-02/README.md)

#### RDS

[![RDS-01](braunschweig/rds-01/map_thumbnail.jpg)](braunschweig/rds-01/README.md)
[![RDS-02](braunschweig/rds-02/map_thumbnail.jpg)](braunschweig/rds-02/README.md)
[![RDS-03](braunschweig/rds-03/map_thumbnail.jpg)](braunschweig/rds-03/README.md)
[![RDS-04](braunschweig/rds-04/map_thumbnail.jpg)](braunschweig/rds-04/README.md)
[![RDS-05](braunschweig/rds-05/map_thumbnail.jpg)](braunschweig/rds-05/README.md)
[![RDS-06](braunschweig/rds-06/map_thumbnail.jpg)](braunschweig/rds-06/README.md)
[![RDS-07](braunschweig/rds-07/map_thumbnail.jpg)](braunschweig/rds-07/README.md)

#### ROL

[![ROL-01](braunschweig/rol-01/map_thumbnail.jpg)](braunschweig/rol-01/README.md)

#### RLB

[![RLB-01](braunschweig/rlb-01/map_thumbnail.jpg)](braunschweig/rlb-01/README.md)
[![RLB-02](braunschweig/rlb-02/map_thumbnail.jpg)](braunschweig/rlb-02/README.md)
[![RLB-03](braunschweig/rlb-03/map_thumbnail.jpg)](braunschweig/rlb-03/README.md)
[![RLB-04](braunschweig/rlb-04/map_thumbnail.jpg)](braunschweig/rlb-04/README.md)
[![RLB-05](braunschweig/rlb-05/map_thumbnail.jpg)](braunschweig/rlb-05/README.md)
[![RLB-06](braunschweig/rlb-06/map_thumbnail.jpg)](braunschweig/rlb-06/README.md)

#### CMP

[![CMP-01](braunschweig/cmp-01/map_thumbnail.jpg)](braunschweig/cmp-01/README.md)
[![CMP-02](braunschweig/cmp-02/map_thumbnail.jpg)](braunschweig/cmp-02/README.md)
[![CMP-03](braunschweig/cmp-03/map_thumbnail.jpg)](braunschweig/cmp-03/README.md)
[![CMP-04](braunschweig/cmp-04/map_thumbnail.jpg)](braunschweig/cmp-04/README.md)

### Trieste (IT)

#### RDS

[![RDS-01](trieste/rds-01/map_decorated_thumbnail.jpg)](trieste/rds-01/README.md)

#### RLB

[![RLB-01](trieste/rlb-01/map_thumbnail.jpg)](trieste/rlb-01/README.md)
[![RLB-02](trieste/rlb-02/map_thumbnail.jpg)](trieste/rlb-02/README.md)

## Nomenclature

- `BLD`: buildings
- `CMP`: composite
- `RDS`: roads
- `RLB`: roads, landscape, buildings
- `ROL`: roads, landscape

## Create thumbnails

```sh
for IMAGE in $(find . -type f -name "*_full.png"); do
  FILE=$(echo "$IMAGE" | sed 's/_full.png//g')
  sips -s format jpeg $IMAGE --out ${FILE}_thumbnail.jpg --resampleHeight 300 -s formatOptions 80
  sips -s format jpeg $IMAGE --out ${FILE}_large.jpg --resampleWidth 1000 -s formatOptions 80
done
```
