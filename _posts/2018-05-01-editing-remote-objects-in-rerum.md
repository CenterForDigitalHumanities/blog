---
title: "Editing Remote Objects in RERUM"
date: "2018-05-01"
categories: 
  - "development"
  - "rerum"
tags: 
  - "rerum"
  - "web-annotation"
coverImage: "Western_front._Shipping_art_objects_from_the_imperiled_museum_at_Valenciennes_to_safer_storage._July_1917_-_NARA_-_173909521.jpg"
author: "Patrick Cuba"
---

[![]({{ site.baseurl }}/assets/images/default.jpg "https://wellcomelibrary.org/iiif/b22282804/annos/contentAsText/a18t0")](https://dlcs.io/iiif-img/wellcome/1/9089aa93-610c-436e-8e5d-36aedfd041f0/73,254,1443,64/!1024,1024/0/default.jpg)

![]({{ site.baseurl }}/assets/images/squarelogo64.png) [View full catalogue record](https://search.wellcomelibrary.org/iii/encore/record/C__Rb2228280)

One use case that has recently captured our imagination in the Center is that posed by the updating of otherwise inaccessible objects. For example, if a user found a [transcription annotation](https://wellcomelibrary.org/iiif/b22282804/contentAsText/18) at the Wellcome Library which they wanted to update, but there was no accessible annotation service mentioned, that user may find help in a Rerum-connected application. Without specific accommodations, it is likely that we have just encountered another "cut and paste" disjunction when the annotation is created anew in a system without any organized reference to its provenance.

## Trust and Authentication

Trust is [a complex thing]({{ site.baseurl }}/authentication-and-attribution-in-rerum) on the Internet. Applications generating annotations (or any other object) are free to assert an appropriate `seeAlso` or `derivedFrom` relationship, but it is as easy to mistake as it is to omit. Further, it would only be needed on a newly created RERUM object, meaning there is no automatic way to detect if the relationship should be expected on a new POST.

Within our ecosystem, there is the [`__rerum` property](https://centerfordigitalhumanities.github.io/rerum-cloud/api.html#__rerum), which is reliably added to objects and is a Source of Truth for object metadata, such as creation date, versioning, and the generating application. This, then, is where the connection to a remote version of an object must be made, if it is to be trusted by any consumer. Though the internal assertions in each object may carry much more detail and meaning, the repository must have a way to simply reference the origin of an "external" version.

## Welcoming Guests

[Versioning in Rerum]({{ site.baseurl }}/versioning-in-rerum/) relies on the `__rerum.history` property and the relationships it identifies ([@context](https://github.com/CenterForDigitalHumanities/rerum_server/issues/25)):

- _prime_ is assigned to the first instance of any new object as the root of the version tree—every new version refers to the IRI of this first version;
- _previous_ is the single version from which this version was derived; and
- _next_ is an array of any versions for which this is _previous_.

As all versioning is only maintained through reference, it is critically important that our server accurately process all manipulations to the database to preserve the integrity of the trees. In normal cases, when all versions of an object exist within the same database, there are only three simple configurations (excluding [deletions]({{ site.baseurl }}/forgetting-deleted-objects-in-rerum)):

1. _Version 1_ is the only version generated with the "create" action. It has a value of "root" for `history.prime` and no value for `history.previous`.
2. _Internal Nodes_ always have a value for `history.previous` and `history.next` with the same IRI in `history.prime`. Only an "update" action generates these.
3. _Leaf Nodes_ are the "latest" versions and resemble internal nodes with an empty `history.next` array.

Though a user may consider it obvious that this "update" is connected to the annotation collections and the manifests adjacent to it, without encoding that relationship as a previous version, no automation or digital citation is possible. In the semantic history of the RERUM version of a remote resource, a combination of cases 1 and 2 occurs—the Rerum version is clearly derived from another resource, but no record of it exists among the objects improved with the `__rerum` property.

## Updating an Idea

It is the JSON-LD standard that presents the solution and directs us towards the useful fourth configuration. The @id property, which is usually assigned during a create action, is likely to be present on an external JSON-LD resource and must be on any request to the update actions. Our example above, [`https://wellcomelibrary.org/iiif/b2228system.nos/contentAsText/a18t0`](https://wellcomelibrary.org/iiif/b22282804/annos/contentAsText/a18t0) is demonstrative of the flexibility of this system. This IRI is not dereferenceable, meaning that it is only useful within an ecosystem of resources, such as an sc:AnnotationList and sc:Manifest, and the entire "previous version" of what is saved in RERUM cannot be known (for considering changes, attribution, etc.) with only the IRI available. Because it is not required to be dereferenceable, it also is not required to exist digitally—a reference to an undigitized resource or an _ad hoc_ IRI for a concept may be used if the case calls for it. This is especially useful for fragments of monolithic resources or difficult to parse resources, such as those targeted by the [tag algorithm](http://www.taguri.org/). Even if the updating application is not aware of an authoritative id for the object it is submitting, one could be generated and attached to invoke this "update" protocol.

In support of this, the Rerum "create" action will reject any object submitted with an @id property, requiring an "update" instead. Then, in the case that the resource being updated does not reside within the database, our new hybrid configuration initiates the version tree. Though the prime "root," this version of the object also references the incoming IRI as the previous version of itself, maintaining the connection (as much as is possible) to the external resource, even if no reference is made within the object itself and no descriptive annotation is attached after the fact. The same solution is applied to references to a "root" version that has been deleted after the version tree was established. Deletion takes the version out of the tree effectively making it a remote resource for the new prime version.
