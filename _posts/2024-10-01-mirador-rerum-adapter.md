---
title: "Using the RERUM Adapter for Mirador"
date: "2024-10-01"
categories: 
  - "development"
  - "rerum"
tags:
  - "mirador"
coverImage: "{{ site.baseurl }}/assets/images/mirador-annotations.png"
author: "Patrick Cuba"
---

The Digital Scholarship development team for the Research Computing Group at Saint Louis University is pleased 
to offer a new tool for integrating the RERUM annotation service with the Mirador viewer. The 
[RERUM Adapter for Mirador](##Adapter PR) is a small plugin that allows users of the Mirador Annotation tool 
to save their annotations to the RERUM annotation service. This allows for the annotations to be shared across 
other tools and platforms that use the RERUM service or understand standard Linked Open Data.

![Looks the same to me]({{ site.baseurl }}/assets/images/mirador-annotations.png)

The [Mirador Annotations](https://github.com/ProjectMirador/mirador-annotations) plugin allows users to create 
and edit annotations on images and other media. The [RERUM Adapter](https://github.com/ProjectMirador/mirador-annotations/blob/master/src/RerumAdapter.js) for Mirador extends this functionality by providing a way to save these annotations to 
the RERUM annotation service. Depending on your project, the Adapter can be adjusted to specific needs.

## Sandbox

By default, loading the Adapter as configured connects to the RERUM sandbox service. This is a public service 
that does not promise data integrity or persistence but is reliable over short periods for experimentation. 
This is very useful for testing and development and available without any setup or additional resources.

## TinyThings

The Adapter uses the tinydev.rerum.io sandbox, but there is also available a tiny.rerum.io service that instead 
connects to the production server. This small change to the `endpointUrl` in the code will allow you to save 
annotations in a more permanent location. This can be done directly in the constructor:
  
```javascript
constructor(canvasId, 'https://tiny.rerum.io', 'https://store.rerum.io/v1/id/agent')
```

As you can see, the change can also be made by simply using the TinyThings URL in the annotation configuration. 
[This short code block](https://github.com/ProjectMirador/mirador-annotations/blob/d6f9fca867a1e9795a6b5ffa5468e286d18ab15d/demo/src/index.js#L8-L22) shows how to set up the Adapter with the TinyThings service:

```javascript
const config = {
  annotation: {
    adapter: (canvasId) => new RerumAdapter(canvasId,'https://tiny.rerum.io', 'https://store.rerum.io/v1/id/agent'),
    exportLocalStorageAnnotations: false, // display annotation JSON export button
  },
  id: 'demo',
  window: {
    defaultSideBarPanel: 'annotations',
    sideBarOpenByDefault: true,
  },
  windows: [{
    loadedManifest: 'https://iiif.harvardartmuseums.org/manifests/object/299843',
  }],
};
```

Similar to the sandbox, the TinyThings service is available without any setup or additional resources. However, 
there are a few caveats to be aware of.

1. TinyThings is production data and Linked Open Data. Polluting it with test data or bad data is poor web citizenship.
2. The metadata for the annotations is controlled by the TinyThings service, so your project will not have any reserved control or explicit authentication.
3. The result of this solution is expected to be transitional and is probably not suitable for long-term projects.

## MyThings

TinyThings is designed to be forked. The [GitHub repository](https://github.com/CenterForDigitalHumanities/TinyNode) can be 
cloned and run with your own API key ([register here](https://store.rerum.io/)) so that your project owns the data. 
To implement your solution, simply replace the `endpointUrl` in the Adapter constructor with your own URL as in the 
TinyThings example above. In fact, it is possible to spin up your own instance of the RERUM service as well and still 
use the Adapter with the same configuration without exposing any of your data in an uncontrolled space.

> ## Notes on the Adapter
>
> There is an [outstanding issue](https://github.com/CenterForDigitalHumanities/TinyNode/issues/90) that will add a lot of 
> flexibility to the Adapter. The Bearer token passthrough will allow for the use of the API key with TinyThings. The 
> provided Authorization header will replace the default header that identifies the TinyThings service and so connects 
> the production data to your project. This introduces a lot of concerns about security of tokens, but simplifies the 
> resources needed, if solvable.
> 
> The `creator` field is added to all annotations as a common field within RERUM and other Web Annotations, but has a 
> default value set. For any of the above solutions, you can set the `creator` field to a value that identifies your 
> project or user. Because this is set on initialization, it cannot support multiple users or projects in the same 
> instance.
