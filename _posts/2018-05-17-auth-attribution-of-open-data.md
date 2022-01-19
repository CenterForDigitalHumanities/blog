---
title: "Auth + Attribution of Open Data"
date: "2018-05-17"
categories: 
  - "development"
  - "rerum"
tags: 
  - "authentication"
  - "authorization"
  - "rerum"
coverImage: "logo.png"
---

Open Data is supposed to be accessible without any constraints to availability.   The idea of authentication around Open Data is an oxymoron, but in practice we have found great benefit for keeping track of who can claim ownership to an object and how we can use ownership to put natural restrictions on the openness of data to make it a more comfortable realm for people.

The restrictions to the openness of data are only necessary to alleviate the human concern of "that's mine, not yours".  Even though a piece of data is 'Open', if Person A was the creator of it they do not want Person B to be able to overwrite or delete it as this would destroy any evidence that person A had any semblance of ownership to the idea or claim the object represented.

Person A and Person B can have radically different ideas that both contribute to the source being considered.  The best benefit for the source is to aggregate both Person A and Person B's idea as evidence to itself, while the best benefit for the public is to be able to look at Person A and Person B's ideas separately and consider them (just like Person B did with Person A to start this whole thing).  The fair result for Person A and Person B is to ensure their idea will always be theirs and always exist as theirs, and only they will be able to remove or change their idea as it exists for the public.

At its simplest description, data is a collection of bits that represent something human readable.  It has no existence or purpose beyond that and has no reason to care about its creator because just existing fulfills its purpose for any resource that may need it.  The human construct of individuality has led to a culture of ownership.  This has created a unique responsibility for Data to be more sympathetic towards the human need for ownership, especially for data that represents an Idea from a Person about a specific Source or Sources.

Persons A-Z expect an idea to exist both as {their} idea and part of the public evidence to a fact or physical reality as a whole.  When an idea is released to the public, anyone should be able to know about it so they can use the evidence captured by the Idea to help support a claim around the same source.  If it is {your} public idea, the public should know it is {yours} and not be able to change that or claim it as {their} own.  Public data, open source, public record are all subject to this anomaly.  Although public, it is somehow attributed with restrictions to claims people can make on an idea or statement that was not {theirs}.

It is not under Open Data's purview to authenticate, but it can authorize based on attribution and the idea of ownership.  This supports the very human culture of "that's mine" while also supporting the golden idea of "but I want others to use it freely to help advance themselves" and the human addition of "so long as they continue to credit that it's mine".  As long as the Data knows WHO made it, authentication can rest on the software that uses it and the Data itself can remain free and public while at the same time implementing ownership rights.  Ultimately, people want this type of Data to exist like human Ideas and computers are bad at handling abstraction and require solid logic paths underneath that end with yes or no answers.

With that need, we are attempting to handle attribution abstraction with solid logic structures like history trees and versioning trees and implementations of “working data” versus “released data”.  The goal is to find a best practice to make this data more human friendly.  Link Data holds relationships between nodes of Open Data so that Data nodes can be connected to each other as they are naturally or forcibly related.  Each Data node can hold metadata that describes WHO it came from.  Data Trees can be used to hold Data in unique history order so the same Data can be referenced and reused, yet remain individually connected to WHO contributed to the evolution along the way.  Supporting attribution means always knowing WHO is performing an action on a object, and when each object knows WHO performed the action on it there can be a layer of authorization that confirms the WHO acting is the same WHO that created.
