---
title: "T-PEN Development Advance Post"
date: "2015-11-10"
categories: 
  - "development"
  - "news"
  - "tpen"
tags: 
  - "survey"
  - "tpen-2-8"
  - "tpen-3-0"
  - "transcription"
coverImage: "tpen28.jpg"
---

## ![logo] (/assets/images/Screen-Shot-2015-11-10-at-11.20.06-AM-1024x398.png)

The Center for Digital Humanities is excited to announce the resumption of work of the T-PEN project (Transcription for Paleographical and Editorial Notation; [t-pen.org](http://t-pen.org/)). Since T-PEN launched in 2012 with generous funding from the [Andrew W. Mellon Foundation](http://www.mellon.org/) and the [NEH](http://www.neh.gov/), there have been 1500 unique users working on 2000 projects. New feature development, however, has been unfunded and proceeded at a crawl. Thanks to an investment from the Saint Louis University Libraries and coordination with several smaller funding sources, we are now in a position to both develop a significant improvement to the existing application and begin work on the next version (3.0).

At this point, we are looking to the community around T-PEN, digital transcription tools, and digital humanities in general to help prioritize our work. Below, you will find the "must haves" we have already built into our schedule. In addition to possible features and tools we have imagined, we are soliciting your feedback to identify what comes first and what else may be targeted.

## ![T-PEN 2.8] (/assets/images/tpen28.png)

These features do not capsize the existing version of T-PEN, but upgrade the interface with new tools and clean up interactions with distributed resources.

#### RERUM Annotations

Recently, the CDH has quietly launched a completely open and free IIIF object and annotation store. This repository provides simple and open access to standards-conformant objects. As a sign of our confidence in RERUM, all new T-PEN annotations will be stored here. As new tools and modules are introduced to visualize, modify, and query RERUM annotations, all of T-PEN is also available.

#### Load a Project from a Manifest

T-PEN was proud to be in the vanguard of IIIF as the first web application to create new OAC annotations on IIIF objects with a simple user interface. Since then, however, OAC has evolved, SharedCanvas has joined IIIF and matured, and many more examples of native IIIF objects have been spotted in the wild. T-PEN should be able to annotate any sc:Manifest object, whether it is an existing project or not.

#### Browse Manuscript Repositories

At its launch, T-PEN had reached agreements with dozens of institutions to make over 2500 manuscripts available for transcription. Over the last few years, that number has grown to almost 4200. However, IIIF now makes it easier for institutions to self-publish and we would like to support that effort by allowing navigation through IIIF aggregators like [IIIF Universe](https://github.com/ryanfb/iiif-universe).

#### Workspace Tools

Modern browsers now allow for more exciting interactions with images, making it simpler to add things like grayscale filters, brightness and contrast, or color inversion. It is also possible to add better mouse-interactions and touch to make text and image annotation easier.

## ![TPEN 3.0] (/assets/images/Screen-Shot-2015-11-10-at-11.16.38-AM-300x217.png)

Version 3 is designed to separate the front-end of T-PEN from the back-end services it provides. This will allow for the more rapid development of specific interfaces for challenging transcription formats or specialized projects. Once released, 3.0 will replace the version at t-pen.org and existing users will have access to their projects under tthe new interface.

#### Multiple Interface Support

By replicating the vanilla T-PEN experience without relying on the server for rendering pages, we open the door to other specialized interfaces, including right to left or columnar texts, annotation for music or translation, or custom annotation options.

#### Improved Image Analysis

As the original image parsing algorithm has been thrown at a massive number of manuscript images now and two things have become obvious: 1) it does very well on some and very poorly on others; and 2) small adjustments to the images before analysis can lead to major improvements in the accuracy of line detection. Separating the service from the interface will allow users to test several algorithms for automatic parsing and select the best one for use on other pages and make universal adjustments to the images before submission such as contrast, rotation, etc.

#### Simple Text Annotation

In order to annotate text in current T-PEN, users are required to manually encode their text with XML-style tags, which can become cumbersome, introduce errors, and is disingenuous as to the real format of the annotations. The best solution is the use of standoff annotations as implemented in our Tradamus project, to annotate text without contaminating it.

#### T-PEN Services API

If we expect our services to be used, we need to do a better job of documenting and explaining how to connect to them. Some of these (image analysis) will be T-PEN services, while others will be connected to rerum.io (saving annotations). Finally, some may be proxied through t-pen.org or rerum.io for authentication and versioning.

## Let Us Know

Leave a note in the comments, telling us what features are most important to you or leave detailed information (even a Zenhub.io upvote) on the [Github issues page](https://github.com/CenterForDigitalHumanities/TPEN3/issues). As we gather feedback, we will continue to update this blog with our development plans, release dates, and features.

To date, almost 2000 projects have been started by users, comprising over 262,000 lines of transcription annotated precisely onto digital images of manuscripts.
