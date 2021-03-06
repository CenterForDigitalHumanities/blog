---
title: "Tradamus - Materials"
date: "2016-04-19"
categories: 
  - "tradamus"
coverImage: "tradamus.jpg"
---

**[![TRAD_Fullogo]({{ site.baseurl }}/assets/images/TRAD_Fullogo-1024x200.png)](http://ongcdh.org/wp-content/uploads/2016/04/TRAD_Fullogo.png)Material**

This information is not specifically about how to use this web application, but more about understanding the data model and the technical decisions made in its creation. Comprehending all this will help you work more effectively but is not required for basic use.

**Broad Principles**

Each critical edition is an arrangement of editorial materials and the assertions made about them. The most common materials are those that represent various witnesses to the edited text, but there may be supporting texts, images, digital or real objects, and original material generated by the editor without which the edition could not be considered complete.

 

* * *

**Types of Material**

**Witness**

These are copies of a given text from different sources that may or may not vary from other witnesses of the same text. These can be imported From T-PEN, XML or JSON documents, or be manually created.

**Image**

Tradamus supports images and while preferably sc:Canvas,any resolvable image is made annotatable. Images connected to an Project via a T-Pen project allows the relevant area of an image to be viewable with the text.

**Editorial Content**

Chapter headings, introductions, commentaries, analyses or any additional material you wish to add to your Project so as to be able to introduce them into the publication in the order or manner of your choosing.

**Dataset**

Encoded data to generate charts, tables, or publication aids

**Placeholder**

any digital pointer to a non-digital or unavailable resource that needs a hook provided to allow for annotation. If for instance you have access to collation tables for a witness but not the witness and you only wish to capture the variants we generate a placeholder sc:canvas for that so as to allow you to annotate that specific material if you desire to.

 

[![MATERIALS]({{ site.baseurl }}/assets/images/MATERIALS-1024x95.png)](http://ongcdh.org/wp-content/uploads/2016/04/MATERIALS.png)

* * *

**Anatomy of a Material**

The creation of a new material relies on a link/import/upload or a manual process. All a material requires to exist is a title. Tradamus will immediately create a full digital document representing this material and update it with any additional data. This document is available at its URI. When a material is imported from a location that provides a URI which resolves to a SharedCanvas Manifest, that URI will be retained. Otherwise, Tradamus will mint and maintain a new URI.

The interface is designed to facilitate adding, annotating or editing the following elements to the material:

_Title_

A label that provides only a human-readable string. For a manuscript witness, this is often similar to the shelfmark or identifier, though significantly distinct. This is defined by the user and can be edited at any time.

_Siglum_

This is a letter (especially an initial) or other symbol used to to refer to a particular witness of a text. It acts as human readable abbreviated label to aid identification of a witness. This is defined by the user and can be edited at any time.

_Metadata_

annotations that specifically target the base material for the purpose of description. This is defined by the user and can be edited at any time.

_Transcription_

Annotations that attach textual data to the material.

_Manifest_

Sequence of sc:Canvas objects that represent the annotated images and other data of a material.

_Annotations_

List of all other annotations that target the material, but which may not be otherwise classifiable, including those imported from XML or JSON files.

[![project]({{ site.baseurl }}/assets/images/project-1024x200.png)](http://ongcdh.org/wp-content/uploads/2016/04/project.png)

 

* * *

 

 

 

For more information and to create an account go to [tradamus.org](http://tradamus.org/)

 

We will be publishing a series of entries on this blog in the coming weeks on how to use tradamus.

The next blog entry will be on Structuring.
