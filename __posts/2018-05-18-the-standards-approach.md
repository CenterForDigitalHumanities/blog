---
title: "The Standards Approach"
date: "2018-05-18"
categories: 
  - "development"
  - "iiif"
  - "rerum"
coverImage: "logo.png"
---

As developers in the field we want to follow the standards emerging for the web and for data. For the challenges our field faces, we often combine RESTful API practices, CORS, Web Annotation, Web Components, IIIF, JSON, JSON-LD, and Linked Open Data standards together so that APIs and applications we create are automatically applicable to other APIs and applications built under the same guidelines.  The Walter J. Ong, S.J. Center for Digital Humanities at Saint Louis University are facing these challenges in particular as we develop [RERUM](http://rerum.io).

When combining standards questions begin to arise.  Where should a HTTP(S) request following all these standards fail for the requester?  Is it best to pass when possible with warnings or fail anytime applicable via error?  When considering users (including each other), what is the best experience?  Do we have to also find a way to get intention from the user to know if we should fail or do we calculate intention from other factors of a request?  Can we use intention to morph requests to prevent errors?

These questions hold weight because the intersection of standards isn’t always accommodating.  When a user requests a standards compliant API to save the object \`{hello:world}\`, the request could be compliant with every mentioned standard but fails the IIIF standard.  Likewise, if a user provides a perfectly structured JSON object that feels IIIF but they forgot to include the context then the request fails IIIF, Web Annotations and JSON-LD.  If the user forgets the \`Content-Type\` header with their request (even if the body is JSON) then the request fails all but one standard.  In all cases, the request could be processed and the object could be saved depending on which standards the API considers strict.

For developers hitting these sticky points when coding, the choice made trickles out to every user.  These types of choices dictate the user experience from open source or proprietary products. When the users are other developers, available software starts to trend towards certain bottlenecks.  The hope of web standards is a realm with the freedom to create software individually, the practicality of reusing or sharing software and the interchangeability of available functionality between software.  We must avoid bottlenecks around these standards to realize this hope and come up with best practices when combining standards in public facing software.
