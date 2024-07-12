# ogc-wkt2

# Credit
- This repo uses the [wkt-crs package](https://www.npmjs.com/package/wkt-crs) package to determine properties such as `hasZ`, `type` and `flipCoords`.
- The `wkt` definitions are gotten from [SpatialReferenceOrg](https://spatialreference.org). It derives these definitions from 
- There are only ogc-wkt2 wkt definitions from OGC, ESRI and EPSG available on this project because of corresponding default SRIDs available by default. Also only non-deprecated CRSs are included
- The CRS listed here are intended for use with an ORM where you can alter Spatial Properties of data such as AxisOrder, transformations and 
## Structure/Type
### 06-07-2024 
PROJ version: `9.4.1`
This is a JSON file where the
    - `k` is `authority`_`code`.
    - `v` is an object with the following properties
      - `type` is either `GeographicCRS` or `ProjectedCRS`
      - `crs` is a string/url with the format `http://www.opengis.net/def/{authority}/{version}/{code}`
      - `wkt` is the well-known text string from [spatialreference.org](https://spatialreference.org)
      - `version` is the version of the CRS. Uses `0` for all `ESRI/EPSG` CRSs , `0` for [CRS84](http://www.opengis.net/def/crs/OGC/0/CRS84h) and `1.3` for OGC CRSs
      - `authority` is the entity that governs this crs definition.
      - `hasZ` is whether the CRS supports the z-index. Is boolean.
      - `flipCoords` is whether the coordinates returned should have their order reversed. 
        - Given that PostGIS stores coordinates in `x,y` axis order, `flipCoords` for all `type===GeographicCRS` except for those by authority `OGC`. This is because OGC Geographic CRS use `x,y` axis order despite not being planar in definition
        - `srid` Is the Spatial Reference Identifier. Commonly used by PostGIS for almost all operations. One can add theirs but given OGC CRSs are versions of existing ones such as `CRS84->EPSG:4326`, `CRS84h->EPSG:4327`, `CRS83->EPSG:4269` and `CRS27->EPSG:4327`, no need to modify the `spatial_ref_sys` table used by PostGIS
TypeScript Type/Interface: 
```{
type: "GeographicCRS" | "ProjectedCRS"; 
crs?: string; 
wkt?: string; 
version: number; 
code: string | number; 
srid: number; 
authority: string; 
hasZ: boolean;
flipCoords: boolean;
}
```
