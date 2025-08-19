---
title: "Geolocating with IIIF Presentation API 3.0: Part 3"
date: "2020-08-10"
categories: 
  - "experiments"
  - "iiif"
  - "technology"
tags: 
  - "geojson"
author: "Bryan Haberberger"
excerpt: "Testing IIIF Presentation API 3.0 services for GeoJSON-LD support, implementing geographic data through service objects attached to Manifests."
---

Having found success with [IIIF Presentation API 3](https://iiif.io/api/presentation/3.0/) Annotation, we look to see if services can support [GeoJSON-LD](https://geojson.org/geojson-ld/).

##### Implementation Description

Below you will see an empty Manifest geolocated via a GeoJSON service. The body of that service is a GeoJSON-LD Point.

##### Example JSON

```json
{
    "@context":[
       "http://geojson.org/geojson-ld/geojson-context.jsonld",
       "http://iiif.io/api/presentation/3/context.json"
    ],
    "id":"http://www.example.org/manifest/3",
    "type":"Manifest",
    "label":{
       "en":[
          "Example IIIF Presentation API 3.0 Manifest III"
       ]
    },
    "summary":{
       "en":[
          "Example Manifest geolocated to Paris, France via a IIIF Presentation API 3 Service."
       ]
    },
    "items":[],
    "service":[
        {
            "@id":"https://example.org/geo/service/point-coordinates(48.86,2.34)&format=geojson",
            "profile":"http://geojson.org/geojson-spec.html",
            "type":["Feature", "GeoJSON_Service"],
            "properties":{
                "label":"Paris, France"
            },
            "geometry":{
                "type":"Point",
                "coordinates":[
                    2.34,
                    48.86
                ]
            }
        }
    ]
}
```
##### Important Implementation Notes

- To support interoperability through Linked Data, the [IIIF Presentation API 3.0](http://iiif.io/api/presentation/3/context.json) and [GeoJSON-LD 1.0](http://geojson.org/geojson-ld/geojson-context.jsonld) context are included at the top of the document.
- An unintended yet beneficial consequence of this paring is that these contexts are [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/). This is because the IIIF Presentation API 3 context contains the [@version tag](https://www.w3.org/TR/json-ld11/#dfn-processing-mode) set to 1.1 which tells JSON-LD processors what version to use for processing the JSON.
- A single [GeoJSON Feature](https://tools.ietf.org/html/rfc7946#section-3.2) was used to assert the coordinates. Since service can be an array of service objects, multiple Features can be supported all at once. GeoJSON also has [Feature Collection](https://tools.ietf.org/html/rfc7946#section-3.3), which can contain an array of Features. In this way, it is possible to represent multiple Features under a single Feature Collection object. Our experience with user interfaces that consume GeoJSON is that they will draw a single Feature Collection of points the same way as an array of multiple Feature objects. Since user interfaces support either, without preference, we chose to represent the single Feature as simply as possible without wrapping it inside a Feature Collection object.
- IIIF Presentation API 3.0 dictates that [services must have a type](https://iiif.io/api/presentation/3.0/#service).

##### Restrictive Outcomes

After creating this example and studying how processors interpret it, and furthering this example through slight variations, we noticed critical points of incompatibility.

1. It is difficult to represent the "type" clash of GeoJSON-LD and IIIF Presentation API 3.0. Each type comes from a different context, and most processors expect that type is a string, not an array. It is likely that processors would not be able to process type, which would cause them to ignore this service JSON.
2. Manifests and Services do not have [motivation](https://www.w3.org/TR/annotation-vocab/#motivation). Motivation is important for determining the functionality and outcome expected of the syntax used.

##### Conclusion

The IIIF Cookbook Community Group, in coordination with the IIIF Maps Community Group, considers GeoJSON-LD incompatible with IIIF Presentation API 3.0 services. Linked Data processors will have trouble process service types in cases where they clash with other Linked Data type requirements, and are likely to ignore that which they cannot process.

##### Next Step

Continue to push for standards in the geospatial communities by improving the specifications they rely on.  There are other methods being used to transmit and render coordinate data over the Web and other systems.  Though some may be specialized enough to require their own syntax, interoperability can only be improved through standardization of these geospatial data practices.
