---
title: "IIIF Cookbook: Data Recipes For Humans"
date: "2020-06-22"
categories: 
  - "development"
  - "iiif"
  - "instructional"
author: "Bryan Haberberger"
excerpt: "Contributing to the IIIF Cookbook with GeoJSON recipes for geographic annotations, demonstrating how standards committees create practical examples for implementers."
---

As with any standards committee or best practices group, there is a subgroup tasked with providing examples for the internal community as well as external implementers.  For IIIF, this group is the [Cookbook](https://iiif.io/api/cookbook/) group.  Examples exist in [the public Cookbook](https://iiif.io/api/cookbook/) that properly format data assertions and combine them with resources in order to enhance those resources.  The group is governed by careful guidance for, and strict adherence to, the best practices and standards promoted within.  This is the most helpful and appropriate place to incubate technical application of the standards in the framework.

I went to this group with a defined task: create GeoJSON assertions that supplement IIIF resources.  IIIF uses the JSON format to express data nodes, a common format for communication in web traffic.  GeoJSON is JSON.  IIIF also supports supplementing data through Annotation.  Without getting into too much detail, the Web says that an Annotation has a body (of information) and a target (to assert that information upon).  An Annotation with a body that is GeoJSON and a target to supplement would fit into the language of IIIF, a budding idea for a new geographic flavored recipe.

Through the Cookbook group, I was made aware that Annotation may not be the only way to provide supplemental data and that there are differences between the versions of the framework that exist.  The initial thought was that a recipe should provide coverage over these variations.  In practice, this became unrealistic and unearthed some places where the intersection of standards was more of a clash than a meld.

A recipe imbues with responsibility.  It means “the parts and process of this fabrication will produce the intended artifact.”  As such, it was decided that one specific example crafted with the most up-to-date version of the technical specifications of the framework would be optimal for a published Cookbook recipe.  All else would be categorized as consequential data artifacts of other, perhaps inferior, ways to make the assertion within the framework (with some exceptions).  Though these alternate data artifacts are not appropriate for the Cookbook, they are still important for showing coverage across the framework and as living examples for other implementers.  Some may not be able to upgrade their software pipelines to use the most up-to-date syntax, and they still need to know how to do these assertions properly in their data sets.  Subsequent blogs will share those artifacts as well as the Cookbook working artifacts.
