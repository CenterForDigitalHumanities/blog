---
title: "Structural REform"
date: "2019-01-29"
categories: 
  - "development"
  - "iiif"
  - "rerum"
coverImage: "rerum.jpg"
author: "Patrick Cuba"
excerpt: "Introducing REform, a user-friendly application for creating and managing organizational structures in IIIF Manifests using Canvas and Range elements with standards-based encoding."
---

The world of annotations is one of unstructured targeting.  There is an existing piece of data somewhere in the world and an annotation targets it.  At a higher level we work with data objects called Manifest.  The manifests we work with follow the construct created by the IIIF frame work ([https://iiif.io/api/presentation/2.1/#manifest](https://iiif.io/api/presentation/2.1/#manifest)).  An important attribute of a Manifest is the ability to organize a structure around data in scope of the Manifest ([https://iiif.io/api/presentation/2.1/#range](https://iiif.io/api/presentation/2.1/#range)) using the “structures” property.  In this way, multiple structures can be built to offer different representational hierarchies of the data in scope.

REform is a new application we are working on to give a user-friendly interface to perform these structuring tasks.  For now, we are only considering data types that could be a part of a Manifest structure, namely a Canvas or a Range.  REform does not consider Annotations because Annotations have no role in structuring the data of a Manifest, nor does REform consider other linked open data aggregation types like List or Collection.  The beginning goal of the application is to provide a place where a user can come in with a Manifest and set up an organizational structure around the data contained in the Manifest encoded to standards so the user can view the manifest in any viewer that supports those standards.

REform will allow the user to update manifests they own in RERUM directly.  Users can also work with manifests they own that exist outside of RERUM and even manifests they don't own thanks to the RERUM inbox ([http:// inbox-docs.rerum.io](http:// inbox-docs.rerum.io)).  Instead of updating the manifest object, a user could instead announce to the Manifest that a new structural arrangement exists.  The owner of the Manifest can choose whether or not to absorb suggested structural arrangements from RERUM inbox using their own application to update their Manifest using the announcement.  If the user/owner chooses not to absorb the suggested structure into their Manifest, that structure could still be found from the inbox and rendered in a UI, but it would not be official in the original Manifest.

In the future we plan to incorporate other aggregation types so users can create varying types of aggregations, even those that may not belong to a Manifest or that may contain other data types beyond Canvas or  Range.  Of course, these will be encoded to standards that would allow viewers that support those standards to view those newly created aggregations.  You can view the demo by visiting [http://reform.rerum.io](http://reform.rerum.io/reform)
