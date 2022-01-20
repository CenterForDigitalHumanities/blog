---
title: "Geolocating with IIIF Presentation API 3.0: Part 2"
date: "2020-08-10"
categories: 
  - "experiments"
  - "iiif"
  - "technology"
tags: 
  - "geojson"
---

Annotation was successful during the first phase of using IIIF Presentation API 3.0 for geolocating an entire Web entity.  Another piece is to ensure that we could provide geolocated assertion upon an entity fragment, since situations like inset maps are common and need specific geospatial information that does not apply to the entire entity.

##### Implementation Description

Below you will see an IIIF Presentation 3.0 Manifest that contains a single Canvas with an [IIIF Image API 3](https://iiif.io/api/image/3.0/) compliant image painted onto it.  The word “Paris” appears on the image and the region containing the word is targeted by two Annotations. One Annotation supplements the fragment with the text “Paris”. The other Annotation supplies coordinates to a central point in Paris, France.

##### Example JSON

{
  "@context": [
    "http://geojson.org/geojson-ld/geojson-context.jsonld",
    "http://iiif.io/api/presentation/3/context.json"
  ],
  "id": "http://www.example.org/manifest/4",
  "type": "Manifest",
  "label": {
    "en": [
      "Manifest - Example IV"
    ]
  },
  "summary": {
    "en": [
      "A Manifest containing GeoJSON-LD Web Annotations to target the word \\"Paris\\" on the provided resource in order to transcribe it and geolocate it to Paris, France."
    ]
  },
  "items": [
    {
      "id": "http://www.example.org/canvas/1",
      "type": "Canvas",
      "label": {
        "fr": [
          "Page de Couverture du Le Scarabée D'or"
        ]
      },
      "width": 3204,
      "height": 4613,
      "items": [
        {
          "id": "http://www.example.org/content_page/1",
          "type": "AnnotationPage",
          "items": [
            {
              "id": "https://preview.iiif.io/cookbook/0139-geo-annotation/recipe/0139-geolocate-canvas-fragment/content.json",
              "type": "Annotation",
              "motivation": "painting",
              "label": {
                "en": [
                  "The cover page."
                ]
              },
              "body": {
                "id": "https://iiif.io/api/image/3.0/example/reference/59d09e6773341f28ea166e9f3c1e674f-gallica_ark_12148_bpt6k1526005v_f20/full/max/0/default.jpg",
                "type": "Image",
                "format": "image/jpeg",
                "service": [
                  {
                    "id": "https://iiif.io/api/image/3.0/example/reference/59d09e6773341f28ea166e9f3c1e674f-gallica_ark_12148_bpt6k1526005v_f20",
                    "type": "ImageService3",
                    "profile": "level1"
                  }
                ],
                "width": 3204,
                "height": 4613
              },
              "target": "http://www.example.org/canvas/1"
            }
          ]
        }
      ],
      "annotations": [
        {
          "id": "http://www.example.org/annotation_page/1",
          "type": "AnnotationPage",
          "items": [
            {
              "id": "http://www.example.org/annotation/1",
              "type": "Annotation",
              "motivation": "supplementing",
              "label": {
                "en": [
                  "Transcription Text"
                ]
              },
              "body": {
                "type": "TextualBody",
                "value": "Paris",
                "format": "text/plain",
                "language": "en"
              },
              "target": "http://www.example.org/canvas/1#xywh=1300,3370,250,100"
            },
            {
              "id": "http://www.example.org/annotation/2",
              "type": "Annotation",
              "motivation": "supplementing",
              "label": {
                "en": [
                  "Coordinate Data"
                ]
              },
              "body": {
                "type": "Feature",
                "properties": {
                  "label": {
                    "en": [
                      "Paris, France"
                    ]
                  }
                },
                "geometry": {
                  "type": "Point",
                  "coordinates": [2.34, 48.86]
                }
              },
              "target": "http://www.example.org/canvas/1#xywh=1300,3370,250,100"
            }
          ]
        }
      ]
    }
  ]
}

##### Important Implementation Notes

- To support interoperability through Linked Data, the [IIIF Presentation API 3.0](http://iiif.io/api/presentation/3/context.json) and [GeoJSON-LD 1.0](http://geojson.org/geojson-ld/geojson-context.jsonld) context are included at the top of the document.
- An unintended yet beneficial consequence of this paring is that these contexts are processed as [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/). This is because the IIIF Presentation API 3 context contains the [@version tag](https://www.w3.org/TR/json-ld11/#dfn-processing-mode) set to 1.1 which tells JSON-LD processors what version to use for processing the JSON.
- IIIF Presentation API 3.0 dictates that resource types be annotated by Annotation Pages as opposed to single Annotations, even in cases where this is only one Annotation.
- A single [GeoJSON Feature](https://tools.ietf.org/html/rfc7946#section-3.2) was used to assert the coordinates. Since an Annotation Page can have an array of items, multiple Features can be supported all at once. GeoJSON also has [Feature Collection](https://tools.ietf.org/html/rfc7946#section-3.3), which can contain an array of Features. In this way, it is possible to represent multiple Features under a single Feature Collection object. Our experience with user interfaces that consume GeoJSON is that they will draw a single Feature Collection of points the same way as an array of multiple Feature objects. Since user interfaces support either, without preference, we chose to represent the single Feature as simply as possible without wrapping it inside a Feature Collection object.
- See the [fragment of the image](https://iiif.io/api/image/3.0/example/reference/59d09e6773341f28ea166e9f3c1e674f-gallica_ark_12148_bpt6k1526005v_f20/1300,3370,250,100/max/0/default.jpg) targeted by the Annotations! This is thanks to the magic of [IIIF Image API 3](https://iiif.io/api/image/3.0/)!
- You can see more description about using this syntax in the [recipe from the IIIF Cookbook](https://preview.iiif.io/cookbook/0139-geo-annotation/recipe/0139-geolocate-canvas-fragment/), including a link to a working example using the recipe.

##### Restrictive Outcomes

After creating this example and studying how processors interpret it, and furthering this example through slight variations, we noticed critical points of incompatibility.

1. The properties field of GeoJSON-LD is not well described and has been left to act as a wild card. It can [contain nearly anything](https://tools.ietf.org/html/rfc7946#section-3.2) and is therefore subject to repeat described terms from other contexts, such as label.
2. During this phase of research, we learned that the GeoJSON-LD specification and context are receiving limited attention. It is difficult to make suggestions or implement improvements (like making the context JSON-LD 1.1 on its own).

##### Conclusion

The IIIF Cookbook Community Group, in coordination with the IIIF Maps Community Group, considers GeoJSON-LD compatible with IIIF Presentation API 3.0. Linked Data processors are able to expand and compact the GeoJSON-LD data syntax in these Annotations.

##### Next Step

IIIF Presentation API 3.0 also has services. We need to investigate whether or not these services can support GeoJSON-LD.

[GO TO PREV BLOG](https://blog.ongcdh.org/blog/experiments/geolocating-with-iiif-presentation-api-3-0-part-1/)        [GO TO NEXT BLOG](https://blog.ongcdh.org/blog/experiments/geolocating-with-iiif-presentation-api-3-0-part-3/)
