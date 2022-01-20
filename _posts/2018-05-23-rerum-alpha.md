---
title: "Rerum Enters Public Alpha"
date: "2018-05-23"
categories: 
  - "iiif"
  - "news"
  - "rerum"
coverImage: "rerum.jpg"
---

Come one, come all.

![screenshot]({{ site.baseurl }}/assets/images/site.png)

### What is this Rerum of which we Tweet?

**Rerum** is an open and free repository for all sorts of digital things. Digital anchors for real world objects and encoded assertions from real world people are stored without prejudice. It's a data ecosystem to bring those unique digital solutions to scholarly demands closer to reality.

### Who Needs another Annotation Store?

Rerum exists to lower the barriers of entry into digital tool building for the Humanities for as many as possible. Not everyone has easy access to the skill sets required for even the most straightforward proof-of-concept applications and interfaces needed to go for funding. We asked ourselves what we could do to help. We began with the thing we most continually redesigned for each new project: a backbone to store data and an API for interactions. We are building that backbone on web standards because we too often found ourselves bound up in a project trying to munge old data into a new system or wasting effort converting from one proprietary format into another to allow the use of various plugins, visualizations, or analytics. For Rerum, we implement standards so that other APIs and applications do not have to struggle to find a way in and so developers are immediately comfortable.

We designed and built Rerum as free open digital object store to hold your data. Solid APIs and Web Components accelerate your application development. Open web standards ensure the clearest, most reliable path for development with the opportunity to leverage "third-party" standards-compliant tools and components. Use ours freely forever or deploy your own Rerum environment. If you need it, we built this for you.

### Why Do it This Way?

Having committed to provide this service we identified a number of key principles that inform our design and implementation of Rerum:

#### Annotation is everywhere

Scholarly assertions, descriptive annotations, and even the measurements and notes often mistaken for metadata are all possible vertices for standards like Web Annotation. These sorts of declarations should always be atomized as much as possible in their storage, especially when they are simple to recombine for user applications.

#### Attribution is essential

Productive communication between researchers requires reliable attribution. When individual  annotations (as above) are each attributed, collaboration becomes natural, and even complex concerns such as authorization are just acts of filtering.

#### Format is ephemeral

No one can predict the Next Great Format, but history can teach us about what obstacles to migration can be avoided. The simpler it is to abandon, the more likely a format will remain accessible.

#### Knowledge is controversy

Statements of fact are reference material until challenged. The interaction of experts and the collisions of theories, evidence, and educated conjecture or theses enlivens research. Recording both the state and the history of the conversation serves knowledge.

#### Research is decentralized

Experts in any mature field are not only distributed across institutions, but the most influential investigators may move around, as people do. The complex and enforced conventions around citation and Intellectual Property Rights make clear the critical nature of maintaining attribution and encouraging distribution.

#### Standards facilitate openness

The hope of web standards is a realm with the freedom to create software individually, the practicality of reusing or sharing software and the interchangeability of available functionality between software. for these reasons, we as developers in the field strive to follow the standards emerging for the web and for data. For the challenges our field faces, we often combine RESTful API practices, CORS, Web Annotation, Web Components, IIIF, JSON, JSON\-LD, and Linked Open Data standards together so that APIs and applications we create are automatically applicable to other APIs and applications built under the same guidelines.

### Why a Public Alpha?

Although we are moving ahead with several partners to make sure the Rerum design fulfills its promises, this is from us, not for us. Success happens when data is discoverable, accessible, and durable—no matter whose logo is in the footer. We want to give you a space to begin to engage with the service, to start to evaluate how it might prove a useful part of your project.

As an alpha, we should not be a dependency for a production application or exhibit. Our plan is to inspire those dormant ideas that have been idling for lack of resources to spark to a level at which they may seek funding or become otherwise inevitable. For more immediate projects, we have a RERUM version 0, which is currently in use in several projects, but whose API and interactions do not meet the goals we have set for v1 for clarity, flexibility, and time to launch.

### How do I start?

Feel free to read up on Rerum at [rerum.io](http://rerum.io) or get into the weeds with some of the blog posts below. If you already know you need in, register your application at [devstore.rerum.io](http://devstore.rerum.io/v1/), pop your API key into you project (or [clone ours](https://github.com/CenterForDigitalHumanities/TinyThings)), and start saving annotations, transcriptions, commentary, manifests, image collections, and more immediately.

- [Authentication and Attribution in RERUM](https://blog.ongcdh.org/development/authentication-and-attribution-in-rerum/)
- [Deleted Objects in RERUM](https://blog.ongcdh.org/development/deleted-objects-in-rerum/)
- [Forgetting Deleted Objects in RERUM](https://blog.ongcdh.org/development/forgetting-deleted-objects-in-rerum/)
- [Versioning in RERUM](https://blog.ongcdh.org/development/versioning-in-rerum/)
- [Editing Remote Objects in RERUM](https://blog.ongcdh.org/development/editing-remote-objects-in-rerum/)
