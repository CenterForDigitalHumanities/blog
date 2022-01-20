---
title: "Deleted Objects in RERUM"
date: "2018-05-08"
categories: 
  - "development"
  - "rerum"
coverImage: "rerum.jpg"
---

In the [last post](http://ongcdh.org/posts/development/forgetting-deleted-objects-in-rerum/), we explored how the tree of the version history is healed around a deleted object. In this post, we look more directly at the transformations to the deleted object itself. Let's take the same abbreviated object to begin:

```json
{ "@id"     : "http://store.rerum.io/rerumserver/id/01",
  "body"    : "content",
  "__rerum" : {
    "generator" : "Application",
    "isReleased": "",
    "history"   : {
      "prime"    : "root",
      "previous" : "",
      "next"     : ["http://store.rerum.io/rerumserver/id/02"]
} } }
```

### The Case for Breadcrumbs

Because we are removing it from the versioning, the original tree structure and its position are irrelevant. However, it must be obvious to consumers that something has changed and that their version of the object is no longer intended to be valid, while offering a way out. Two often used solutions that fail here are removal and flagging. If the object were no longer available at its original `@id`, interfaces (for example, a reference to a transcription annotation in an online article) would simply break and developers would have no way of recovering the data or seeking an alternative. If a property like `deleted:true` were added, it would be so ineffective in updating the object that the interface would continue to render out-of-date information unless the developer had the foresight to specifically check for this flag.

To break the response without stranding the client, we need to disrupt the expectations of the interface without discarding the object data. Our solution is to move the entire object down one level into a `__deleted` property, breaking unaware interfaces, but still allowing developers to access the original object. Consider the deleted version of our sample:

```json
{ "@id" : "http://store.rerum.io/rerumserver/id/01", //same ID
  "__deleted" : {
    "time"   : "1515183834857", //time of deletion
    "object" : {                //snapshot of object at deletion
      "@id" : "http://store.rerum.io/rerumserver/id/01",
      "body" : "content",
      "__rerum" : {
        "generator" : "Application",
        "isReleased": "", 
        "history" : {
          "prime" : "root",
          "previous" : "",
          "next" : ["http://store.rerum.io/rerumserver/id/02"]
} } } } }
```

In a typical interface from a consuming application, the rendered display would resolve the `@id` and bind to `response.body`. This is now undefined, and an aware interface (or a vocal audience) will quickly alert the developer of the change. Even a human who was ignorant of the RERUM API should be able to divine that the "new location" of their data is `__deleted.object.body` and the real-life meaning of that move should feel like plain English. At this point, the developer can choose to update the display to render the deleted object (hopefully with some notice) or replace it with an adjacent version referred to in the `history` property.

### Results

In this system, there is no way, through the API, to actually obliterate an object or any version of it. This is important because of the interrelationships between all the versions and the risk built into true deletions being committed pell-mell. The MongoDB behind our current version of RERUM still supports complete removal, if it becomes required, but we believe the presented solution will break interfaces appropriately without marooning them.

So what do you think? Does our solution stray too far from convention? Are we inviting disaster trying to enforce standards while messing with objects? Let us know in the comments or [submit an issue on GitHub](https://github.com/CenterForDigitalHumanities/rerum_server).
