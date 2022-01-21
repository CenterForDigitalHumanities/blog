---
title: "Geolocating with IIIF Presentation API 2.1 Services"
date: "2020-08-10"
categories: 
  - "experiments"
  - "iiif"
  - "technology"
tags: 
  - "geojson"
  - "geojson-ld"
  - "geolocation"
author: "Bryan Haberberger"
---

The shortcomings of the Annotation syntax meant looking for another option. The other option of intertwining syntax is [IIIF Presentation API 2.1 services](https://iiif.io/api/annex/services/). Initial investigation led to a supported [GeoJSON extension](https://iiif.io/api/annex/services/#geojson), which meant there was already a foundation set for working with GeoJSON under the scope of the API.

##### Implementation Description

Below you will see an empty Manifest. There is a GeoJSON service attached to the Manifest with the coordinates to central Paris, France. The service contains a GeoJSON-LD object within the [service object structure](https://iiif.io/api/annex/services/#requirements).

##### Example JSON

{
   "@context":[
      "http://iiif.io/api/presentation/2/context.json",
      "http://geojson.org/geojson-ld/geojson-context.jsonld"
   ],
   "@id":"http://www.example.org/example2/manifest",
   "@type":"sc:Manifest",
   "label":"Manifest - Example II", 
   "description":"An Empty Manifest that is geolocated to Paris, France via an IIIF Presentation API 2.1 service.",
   "sequences":[],
   "service":{
      "@id":"https://www.example.org/geo/service/point-coordinates(2.34,48.86)&format=geojson",
      "profile":"http://geojson.org/geojson-spec.html",
      "type":"FeatureCollection",
      "features":[
         {
            "@type":"Feature",
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
}

##### Important Implementation Notes

- To support interoperability through Linked Data, the [IIIF Presentation API 2.1](http://iiif.io/api/presentation/2/context.json) and [GeoJSON-LD 1.0](http://geojson.org/geojson-ld/geojson-context.jsonld) context are included at the top of the document.
- The IIIF Presentation API 2.1 and GeoJSON-LD 1.0 context are [JSON-LD 1.0](https://www.w3.org/TR/2014/REC-json-ld-20140116/).
- The assertion is directly on the Manifest.
- A GeoJSON Feature Collection was used to represent the single Feature object.  Since service must be an object, it is best to control expectations and always return a Feature Collection, since it would require a Feature Collection to represent an array of Feature objects.

##### Restrictive Outcomes

After creating this example and studying how processors interpret it, and furthering this example through slight variations, we noticed critical points of incompatibility.

1. The context of GeoJSON-LD is not compatible with with JSON-LD 1.0. JSON-LD 1.0 processing cannot realize arrays of arrays, meaning geometry for Polygons cannot be supported.
2. The properties field of GeoJSON-LD is not well described and has been left to act as a wild card. It can [contain nearly anything](https://tools.ietf.org/html/rfc7946#section-3.2) and is therefore subject to repeat described terms from other contexts, such as label. Linked Data separates the meanings of duplicate keys to their direct definitions.
3. service is a JSON object.  This means it is not possible to represent multiple Features as a simple Array.  To do this, a single Feature Collection JSON object containing the array of Features must be used.
4. Manifests and Services do not have [motivation](https://www.w3.org/TR/annotation-vocab/#motivation). Motivation is important for determining the functionality and outcome expected of the syntax used.

##### Conclusion

The IIIF Cookbook Community Group, in coordination with the IIIF Maps Community Group, deemed that GeoJSON-LD was not compatible with IIIF Presentation API 2.1 services. Linked Data processors will not be able to understand or realize the GeoJSON-LD data syntax used are likely to ignore that which they cannot process.   It is not realistic to expect that existing services will change to only return Feature Collections, and we do not want to restrict what GeoJSON resource types can be used in future development.

##### Next Step

With the release of [IIIF Presentation API 3.0](https://iiif.io/api/presentation/3.0/) looming, we would like to investigate if the improved API could support geographic assertions.

[GO TO PREV BLOG](http://ongcdh.org/experiments/geolocating-with-iiif-presentation-api-2-1-annotation)       [GO TO NEXT BLOG](http://ongcdh.org/experiments/geolocating-with-iiif-presentation-api-3-0-part-1)
