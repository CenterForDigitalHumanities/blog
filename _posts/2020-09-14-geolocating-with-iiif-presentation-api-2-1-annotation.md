---
title: "Geolocating with IIIF Presentation API 2.1 Annotation"
date: "2020-09-14"
categories: 
  - "experiments"
  - "iiif"
  - "technology"
tags: 
  - "geojson"
  - "geojson-ld"
  - "geolocation"
---

The experience with Annotation during the initial phases of implementing this syntax was positive. We found it prudent to investigate Annotation again using [IIIF Presentation API 3.0](https://iiif.io/api/presentation/3.0/).

##### Implementation Description

Below you will see an empty Manifest geolocated via a geographic polygon. There is an Annotation Page containing a single Annotation with coordinates to central Paris, France contained in the Manifest. The body of that Annotation is [GeoJSON-LD](https://geojson.org/geojson-ld/).

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
         "Manifest - Example III"
      ]
   },
   "summary":{
      "en":[
         "Example Manifest geolocated to Göttingen, Germany via Annotation."
      ]
   },
   "items":[
      
   ],
   "annotations":[
      {
         "id":"http://www.example.org/annotation_page/1",
         "type":"AnnotationPage",
         "items":[
            {
               "id":"http://www.example.org/annotation/1",
               "type":"Annotation",
               "motivation":"supplementing",
               "label":{
                  "en":[
                     "The coordinates for the main building of the event (Alte Mensa Conference Center)."
                  ]
               },
               "body":{
                  "type":"Feature",
                  "properties":{
                     "label":"Göttingen, Germany"
                  },
                  "geometry":{
                     "type":"Polygon",
                     "coordinates":[
                        [
                           [
                              9.80943,
                              51.570156
                           ],
                           [
                              9.850628,
                              51.579117
                           ],
                           [
                              10.030529,
                              51.590637
                           ],
                           [
                              10.056962,
                              51.532347
                           ],
                           [
                              9.948829,
                              51.481692
                           ],
                           [
                              9.905576,
                              51.513933
                           ],
                           [
                              9.804273,
                              51.524557
                           ]
                        ]
                     ]
                  }
               },
               "target":"http://www.example.org/manifest/3"
            }
         ]
      }
   ]
}
```

##### Important Implementation Notes

- To support interoperability through Linked Data, the [IIIF Presentation API 3.0](http://iiif.io/api/presentation/3/context.json) and [GeoJSON-LD 1.0](http://geojson.org/geojson-ld/geojson-context.jsonld) context are included at the top of the document.
- An unintended yet beneficial consequence of this paring is that these contexts are processed as [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/). This is because the IIIF Presentation API 3 context contains the [@version tag](https://www.w3.org/TR/json-ld11/#dfn-processing-mode) set to 1.1 which tells JSON-LD processors what version to use for processing the JSON.
- IIIF Presentation API 3.0 dictates that resource types be annotated by Annotation Pages as opposed to single Annotations, even in cases where this is only one Annotation.
- A single [GeoJSON Feature](https://tools.ietf.org/html/rfc7946#section-3.2) was used to assert the coordinates. Since an Annotation Page can have an array of items, multiple Features can be supported all at once. GeoJSON also has [Feature Collection](https://tools.ietf.org/html/rfc7946#section-3.3), which can contain an array of Features. In this way, it is possible to represent multiple Features under a single Feature Collection object. Our experience with user interfaces that consume GeoJSON is that they will draw a single Feature Collection of points the same way as an array of multiple Feature objects. Since user interfaces support either, without preference, we chose to represent the single Feature as simply as possible without wrapping it inside a Feature Collection object.
- You can see more description about using this syntax in the [recipe from the IIIF Cookbook](https://preview.iiif.io/cookbook/0195-geolocate-manifest-to-polygon/recipe/0195-geolocate-manifest-to-polygon/), including a link to a working example using the recipe.

##### Restrictive Outcomes

After creating this example and studying how processors interpret it, and furthering this example through slight variations, we noticed critical points of incompatibility.

1. The properties field of GeoJSON-LD is not well described and has been left to act as a wild card. It can [contain nearly anything](https://tools.ietf.org/html/rfc7946#section-3.2) and is therefore subject to repeat described terms from other contexts, such as label.
2. During this phase of research, we learned that the GeoJSON-LD specification and context are receiving limited attention. It is difficult to make suggestions or implement improvements (like making the context JSON-LD 1.1 on its own).

##### Conclusion

The IIIF Cookbook Community Group, in coordination with the IIIF Maps Community Group, considers GeoJSON-LD compatible with IIIF Presentation API 3.0. Linked Data processors are able to expand and compact the GeoJSON-LD data syntax in these Annotations. It is troubling that the GeoJSON-LD specification and context are abandoned. However, IIIF supports extensions within its scope, and the IIIF Maps Community Group is working with the GeoJSON Web Group to bring the specification into an environment where it will be improved upon and maintained.

##### Next Step

The main goal is to ensure we can make all the basic kinds of assertions through IIIF resource types. We know we can geolocate an entire resource to a Polygonal coordinate area. The other basic assertion is to geolocate some fragment of a resource contained within a Manifest.

[GO TO PREV BLOG]({{ site.baseurl }}/geolocating-with-iiif-presentation-api-2-1-services/)   [GO TO NEXT BLOG]({{ site.baseurl }}/geolocating-with-iiif-presentation-api-3-0-part-2/)
