---
title: "Forgetting Deleted Objects in RERUM"
date: "2018-05-08"
categories: 
  - "development"
  - "rerum"
coverImage: "rerum.jpg"
---

At the Walter J. Ong, S.J. Center for Digital Humanities, we have been working hard on [RERUM](http://rerum.io), the public object repository for IIIF, Web Annotation, and other JSON documents. The latest feature we've been diving into for the 1.0 release is **DELETE**. As is covered in the [documentation on Github](https://github.com/CenterForDigitalHumanities/rerum_server), there are a few guiding principles that are relevant here:

1. **As RESTful as is reasonable**—accept and respond to a broad range of requests without losing the map;
2. **As compliant as is practical**—take advantage of standards and harmonize conflicts;
3. **Trust the application, not the user**—avoid multiple login and authentication requirements and honor open data attributions;
4. **Open and Free**—expose all contributions immediately without charge to write or read;
5. **Attributed and Versioned**—always include asserted ownership and transaction metadata so consumers can evaluate trustworthiness and relevance.

## Considering

Setting aside for now some of the nuance of the common REST practices and the [Web Annotation Standard](https://www.w3.org/TR/annotation-protocol/#delete-an-existing-annotation), we needed to determine what type of request we would accept, what transformation would happen to the data, and how the service would respond to the client application. Authentication (covered in depth in [another post](http://ongcdh.org/posts/development/authentication-and-attribution-in-rerum/)) is the first concern, since an **Open and Free** repository is a target for vandalism. Honestly communicating the "deleted" status of an object without breaking all references to it is served by appropriate **Version Control** (see [here](https://blog.ongcdh.org/development/versioning-in-rerum)). Combining these concerns, we realized it was not enough to "just remove" or "delete-flag" an object (specifically, a version of an object)—our repository has to heal the version history tree around it.

Let's start with an abbreviated object (`prime` shown):

{ "@id"     : "http://store.rerum.io/rerumserver/id/01",
  "body"    : "content",
  "\_\_rerum" : {
      "generator" : "Application",
      "isReleased": "",
      "history"   : {
          "prime"    : "root",
          "previous" : "",
          "next"     : \[ "http://store.rerum.io/rerumserver/id/02" \]
      }
  }
}

Whose version history tree (in the simplest complex form) looks like this:

![tree](https://docs.google.com/drawings/d/e/2PACX-1vS_2dxoljSjZaonajp0d17rjOm6sxDBVTGP1fJrX8RQo9-lGWejAG-sQ2XMrnRMPTSd54L8YTeazGSa/pub?h=300)

A single object in 9 versions, updated by 3 different applications (A, B, C)

Before attempting any deletion, there are 3 checks that must be passed:

1. **Is the request coming from the original generator?** In an open system, we offer endless opportunities to extend the work of others, but deleting is destructive, so it may only be done by the application that originally created this version.
2. **Is this version Released?** RERUM offers few promises to client applications, but the immutability of [Released objects](http://uncited.blogspot.com/2017/03/unpublishing-open-sharing-of-half-baked.html) is one of them.
3. **Is this version already deleted?** While it may not have a huge effect to "re-delete" a version of an object, it feels dishonest to the client to do so.

## Deleting

There are three possible positions a version may be in (in ascending complexity):

1. **Leaf** without descendants: 05, 08, 09 above;
2. **Internal** with a parent and at least one child, 02 and 07 being the most complex; and
3. **Root** as the `__rerum.history.prime`value of "root" indicates in node 01.

All these options follow this process:

![](https://docs.google.com/drawings/d/e/2PACX-1vQP2iO8-4bQkvYOMr8mD07HYHPZ4KwyC4-gYLPjRhLiigalQUn9Bjp14jdYf4kaAwNI94Jwa-VD8GDc/pub?w=906&h=726)In the first two cases, where the deleted version is not "root", the healing is fairly straightforward. The chain is simply pinched around the version, removing the object—those listed in the `h.next` array are updated (in `h.previous`) to point to the version from which the deleted version was derived. The `h.next` array in that version is updated to bypass the deleted object. In the case of deleting 02, above, 03 and 06 would now claim 01 as a parent and 01 would now have them as children.

If, however, the deleted object is the original instance, the troubling reality is that every version refers to it as the `__rerum.history.prime` value. Moreover, by deleting it, the client has made an adjustment to reality, removing the timestamped "first moment" of the history. Trusting the client application and holding to our principles of freedom, we must allow this and document it well. For each child of 01, the original tree is broken into a new tree with that node as its root. This feels destructive, but reflects the intent of a client requesting such an action. Within that new tree (02, here), `h.prime` becomes "root" and the @id of the new root must be populated to all the descendants. The new prime also enters an unusual state ([explored more here](https://blog.ongcdh.org/development/editing-remote-objects-in-rerum)) where `h.prime` is "root" and there is a value for `h.previous`. By referring to the deleted object, it remains possible for an enterprising researcher to reconstruct the historical relationships in this tree, though no query will expose it simply.

## Nuking

What of the case where I want to obliterate and entire object, including all versions ever generated? Though a simple case from the perspective of user intention, it becomes logically complex. We have not supplied a shortcut method for this yet, but the logic of the process follows the chart above in iteration. Let's take the applications A, B, C above and attempt to blow away this unwanted object.

#### Application A

This application seems to have the most right to commit this act, as the owner of the "prime" instance. However, there are intervening conditions here. No matter if you burn the tree from leaves to root or root to leaves, the result is the same. Removing 01 simply updates the tree to have 02 as prime and all nodes are updated. Removing 02 does the same with the side-effect of creating a tree from 03(A) and 06(B). Continuing to remove the 03 tree is easy, but an attempt to remove the 06 tree fails immediately, as "A" no longer "owns" it. This is appropriate, since "A" was allowed to purge the history of its contributions, but not those derived from them in the meanwhile. Clients using 08 and 09, will now only see the `h.prime` of 06, though they may traverse the records back to the original prime if they wish.

#### Application B

This application has the reverse problem from "A" as a derivative creator. No attempt to delete anything above 06 will be possible, full stop. Blowing away the 06 branch, however, will meet with similar constraints as "A," since "C" has established a derivative branch on 07. As 07 is deleted, those versions in the `h.next` array will be updated to point to 02 (the result of deleting 06). Once all allowed actions are finished, 09 will have effectively replaced 06 in the 01 tree. No active node within the tree will retain a reference to "B" versions, though (see below) the deleted objects will report their placement.

#### Application C

This application is the most limited, as it has only contributed one version, a leaf, to the tree. While it is unable to impact the major structures, it is also able (like "B") to remove itself from the history completely, leaving the only traces of its original participation in the objects themselves.

## The Debris

What is left after a successful deletion in the history tree is important to clients who continue to depend on the leaves, but what of those consumers who had referenced the deleted object? Following our principles, we intend to make it obvious to consumers that something has changed and that their version of the object is no longer intended to be valid, while offering a way out.

We think our solution is quite clever, but that's [a post for another day](http://ongcdh.org/posts/development/deleted-objects-in-rerum/).
