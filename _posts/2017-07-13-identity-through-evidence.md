---
title: "Identity through Evidence"
date: "2017-07-13"
categories: 
  - "eventities"
---

## The Birth of an Identity

## ![](images/wwi-letters-7-jun-1918001.jpg)

Let's take a real case and find out what it indicates and how it ought to be annotated. This image is the first page of a six page (3 folio) letter from Private Allen Gooch to his family, but let's not get ahead of ourselves.

### Find an artifact

According to [ongrannystrail.com](https://www.google.com/url?q=https://ongrannystrail.com/2012/09/09/i-went-out-of-my-tent-and-saw-about-twenty-flying-machines/&sa=D&ust=1515534612898000&usg=AFQjCNGXXRGQEc2kzwwdax25lwhYVkZEJg), Dayna Gooch Jacobs has a letter from World War I. There are already strong cataloguing and metadata description schemata to make this real thing a well-described lump of matter. At this point, the way in which it is discovered is decidedly analog:

> "Hello, Mrs. Jacobs? Would you mind if I stopped by to look at your WWI letter?"

This is inoffensive, but undiscoverable. As it may be described in print catalogs or included on library databases, some anonymous individual on behalf of an institution may apply metadata that aids in the discovery:

> "M Librarian, could you help me locate WWI letters from Military Police?"

Such a request is possible in many ways, but is already reliant on a vast knowledge of the vocabularies of subject heading and the decisions of the search application. However, the goal is possibility, not perfection, so let's let this be good enough and admit that we have reliably entered this letter into the public record.

### Establish Uniqueness

### ![](images/dsc_0761-002.jpg)

In the human world, there is a lot of fuzziness in definition. This is fine because we are comfortable replacing definition with a preponderance of description. Even with a name "Dayna Gooch Jacobs" and a photo (right), to really find the right person, a researcher may want an address, measurements, occupation, even DNA. The digital world solves this with URIs. If I say, "1" and commit to never referring to that "1" again for any other object, I can reliably reference it over and over. In fact, even if the entire resource vaporizes, the corpus of annotations that point to it can still describe it. In this way, an authority file isn't even necessary, except to assure the uniqueness of the identifier. In JSON-LD, we're looking at something like this:

{ "@id" : "1" }

This is much better if we upgrade the identifier to something resolvable ([or at least unique](http://www.taguri.org/)) like:

{ "@id" : "http://example.org/people/1" } or
{ "@id" : "tag:ongrannystrail.com:DaynaGoochJacobs" }

In the same way, the letter can be identified. There is already a great standard for describing the digital object in IIIF, so if we allow for a URI that stands in for the real object, we can link it to the `sc:Manifest` that represents the digitization of it:

{ "@id" : "http://example.org/manifests/05",
  "@type" : "sc:Manifest",
  "label" : "WWI Letter from Private Gooch",
  "pto:Facsimile" : "http://example.org/item/2a9de-033",
  "sequences" : \[ "http://example.org/sequences/m05" \]
}

So far, so good.

## Discovery and Creation

Until I saw this letter on ongrannystrail.com, I didn't know Dayna Jacobs existed. If a trusted friend or colleague told me she existed, I would conventionally assume personal experience as his evidence unless otherwise clarified. We have filled our human experience with descriptions (beloved by our brains) in place of identifiers and definitions (required by our robots). It is common to make identity-centric decisions such as "Let's mint URIs for the wives of Henry VIII" or "Let's create identifiers for every character in _The Shoemaker's Holiday_."

The conventional approach to this opportunity to describe is idea-first cataloguing. The Thing is described within a schema through data entry and largely anonymous or impersonal assertion. The underlying assumption is that the item is best described in isolation, then allowing the schemata in which it participates to impose discoverability. Robots appreciate this clean and defined style of categorization; it is similar to the discrete properties used on digital objects. The problem is that the human cataloguer is only passing as robot when she attaches metadata to the item record. A robot would insist a play meet all the defined qualities of the vocabulary term (`fabio:play`) that alludes to an English word ("play") before asserting its membership. The human, most likely, is reaching the same conclusion based on a similarity between the tested item and other items already in that same category. The appointment is made based on where others would look for it as much as on any intrinsic properties. In this way, we are _accommodating_ imagined future human researchers and _deceiving_ the computers which rely on the sincerity of our cataloguing.

Then let us reverse the process, requiring some _evidence_ of existence first, and then limiting that identity to an anchor. All the descriptive metadata is promoted to annotations, which can carry with them the attribution of the annotator and the evidence on which it is based. This means that an authoritative catalogue can still identify items which belong within it, but the probabilistic nature of human assertion is honored with multiple and possibly conflicting assertions about various item properties. Two unrelated researchers can annotate a play—one for structure and one for historical locations—without having to dodge each other in a TEI/XML document or create parallel and redundant resources.

Once annotations are easier, scholars can be more fearless in the proliferation of identifiers. New anchors for digital pointers to real things only need some evidence through reference in a known object. At once, the linkages between objects are in place and the next annotation has a reliable place to point to along with some context for the thing. By allowing conflicting descriptions of things, the reliable anchors are flexible and reusable, even as the academic conversation insists on redescribing once obvious facts. Discovery begets creation begets description begets discovery.

## Annotation in Practice

Let us allow that the letter itself is already catalogued and described and that a URI has been minted for it. If I would like to know the author, I could read the description. Some library record, metadata set, or dedicated "description" field in the `sc:Manifest` object is likely to offer the text from the exhibit's HTML document:

> "Letter from Private Allen L. Gooch to his family in Arizona during World War I.  Transcribed by Dayna Gooch Jacobs and in her possession. Slashes indicate line breaks on original letter."

This is helpful to humans, but inaccessible to robots. Moreover, if I wish to criticize any part of this assertion, I have to replace the entire entry or use a selector to carefully tease out the problematic statement. Most importantly, this description is devoid of evidence and attribution, so authority can only be implied from the hosting repository. If this record had already been treated by a cataloguer, it is possible she would have anonymously populated an author field based on the description text alone.

A better description is possible. I would like to add the author as the `dc:creator` of this item and the derivative digital objects. The prevailing convention adds the property as metadata to the objects as a simple key-value pair. This is the simplest way to render these items in a viewer, but the structure cannot allow for any advantages over the description except for the granularity. The best annotation asserts a creator with evidence and attribution. There are three places to find this evidence:

1. Transcription—in Dayna Jacobs's article, the end of the posted transcription reads: "Private Allen L. Gooch Troop A, 314th Military Police, 89th Division.  American Expeditionnary Forces."
2. Image Annotation—The image resource is a great example of the type of specific evidence useful in these types of assertions. If someone wants to criticize, the image explains that I have determined the creator based on the signature on the letter, which may be forged or otherwise untrustworthy. 
3. Scholarly Assertion—Without any other evidence, a scholar should be able to stake an assertion on his own reputation. To do so may weaken the suggestion, but it does not eliminate it. In fact, as in mathematics or Wikipedia, it may serve as a beacon to others to find better evidence for the claim.

What needs to be acknowledged here is that no description is absolute. What had been descriptive metadata is now asserted description by some `foaf:Agent` because of evidence. If I were to resolve the above `sc:Manifest` at the Smithsonian, I would probably trust it. I would feel better knowing that the Smithsonian is actually asserting the particular piece of metadata I am interested in (date, author, etc.) formally, since it is possible this object was just ingested from some other collection and has not been reviewed. It would be even better to know that Carol, a trusted employee for over 25 years, was the metadata librarian who dated this and several other letters of the same period.

## Annotating Discovered Others

This letter this genealogist described, which was written by someone is amazing. Even when only considering its direct content, it has witnessed or is evidence for many discrete nouns.

##### People, Groups, and Corporations

- Private Allen L. Gooch
- The Mother of Private Allen L. Gooch
- The family and acquaintances of Private Allen L. Gooch
- Friend and Sergeant to Private Allen L. Gooch
- Troop A, 314th Military Police, [89th Division](https://www.google.com/url?q=https://en.wikipedia.org/wiki/89th_Infantry_Division_(United_States)&sa=D&ust=1515534612907000&usg=AFQjCNFcrlpybgoYUhL1ubukpUL9cg4zzA)
- U.S. Army
- "Doll" to Private Allen L. Gooch

##### Locations and Landmarks

- Hudson Bay
- About 25 miles up the Hudson Bay
- [Camp Mills](https://www.google.com/url?q=https://en.wikipedia.org/wiki/Camp_Mills&sa=D&ust=1515534612908000&usg=AFQjCNGNO4601wEA1bvVdcURNSbQOXgbpg) on the Bay
- Brooklyn Bridge
- NYC
- Hachita, NM
- Duncan, AZ

##### Materials and Quantifiables

- Shoes (not enough)
- Sixshooters (not enough)
- Flying Machines (about 20)
- Tent (per)
- Ships (3 large)

##### Time and Date

- Friday, 7 June 1918
- A week or a month in place
- When it "rained and rained" just before 7 June
- Shining sun the next morning with the aircraft
- Saturday 8 June, when Private Gooch took his 24 hour pass to NYC (prediction)

The assembly of this circumstance requires at least several digital objects that are just as important for the encoding of this letter:

- sc:Manifest for the ordered images, along with the required `oa:Annotation`, `sc:AnnotationList`, and `sc:Canvas` objects within.
- The Transcription provided on the page is a text resource that could be better encoded and contains annotations for line breaks within the text.
- The `foaf:Agent` object(s) responsible for drafting the blog entry, transcribing, digitizing the letter, and taking responsibility for holding the physical item in collection should have at least one URI to identify them, even if other information is not available.

This is a large, incomplete, and unprioritized set of things that should probably be encoded. Let's take just one poorly _defined_ thing here and start to _describe_ it.

> "This friend of mine/ from hachita is/ a sergeant in my/ troop he is getting/ me a twenty four/ hour pass and I/ am goeing to N.Y./ City tomorrow"

This passage insists that in addition to the author, another fellow exists. From the brief passage, we know:

1. **Male Human Person**: "he" pronoun is used and it would be strange if the male author was commanded by a female or non-human at this time.
2. **Sergeant**: possibly a specific rank, but it could be one of several. Someone knowledgeable in historic ranks may know the most appropriate one for this reference.
3. **Friend**: by the author's own assertion, so it isn't something that can be very narrowly defined.
4. **Hachita**: there is a strong possibility this is Hachita, NM and is suggested as at least a hometown, if not a birthplace for this man. Further research could add evidence to this descriptor.
5. **Location**: we can be confident that as sure as we trust the author, this man is with the troop at Camp Mills on and around Friday, 7 June \[1918\].
6. **Troop A 314th**: through his connection to Private Gooch and "in my/ troop".

Remarkably, without any name or label to speak of in this letter, we can know quite a bit about this man. In most cataloguing cases, only information deemed relevant would have been included (often abandoning evidence and attribution) and imprecise information (such as "hachita" or "sergeant") would be unfortunately removed or inaccurately promoted to categorical metadata. Had we begun with just a name on a list, we may never have found this reference. Approaching it thus, we have found an interesting negative space and may go in search of the 1918 MP sergeant from New Mexico in other documents and connect the reference more completely. A focused project or schema may even induce negative space for certain types of things to point out the unknowns. In this case, a Person may require an annotation for label, date of birth, date of death, or nationality, even if the content of such an annotation were null or unknown.

The relationships are also part of the description and several of the nouns from the list above serve as powerful connecting nodes. Humans are always good connectors because we care so much about their connections. Other aggregating locations, such as Troop A, Camp Mills, or NYC work well because otherwise unrelated data can find kin. Dates and times are also useful because they offer marginal characters a role in dominant history. Rigid structures such as XML hierarchies insist on a preference when encoding these structures; with annotations, they can all be explored _ad hoc_ without disrupting the original resources.

## The Importance of Evidence

When we build applications to consume digital objects or, in a conversation, are asked to describe something, we certainly list properties, often include relationships, and rarely mention evidence. Look again at Private Gooch's passage about his sergeant:

> "This friend of mine \[as his past behaviors align with my definition of friendliness and within the context of this letter\]/ from hachita \[as he has indicated to me\] is/ a sergeant \[as stated by the U.S. Army protocols and promotions\] in my/ troop \[as you can see from his appointment\] he is getting/ me a twenty four/ hour pass \[personal interview\] and I/ am goeing to N.Y./ City tomorrow \[probable future based on personal intentions and access to aforementioned pass\]."

It is clear that spending time with assumed evidence is inefficient and so convention often steps right past it. However, in scholarly criticism, it is often misalignment of interpretation and available evidence that separates minds. The better documented the obvious facts, the more time is available for deep exploration of real gaps in knowledge or important divergences in interpretation.

The simple object for the sergeant is easily constructed (with `@context` omitted):

{ "@id" : "tag:ongrannystrail.com:SergeantA314",
  "@type" : "foaf:Person",
  "label" : "Troop A 314th Sergeant (unnamed)"  
  "gender" : "male",
  "hometown" : "Hachita",
  "rank" : "sergeant" }

Good encoders would agree here that finding a reliable URI for the values in gender, hometown, or rank, would be better, but there is nothing unacceptable about these strings as they are. Let's take just one of these properties and start to encode the conventions.

"hometown" : {
    "@language":"en",
    "@value":"Hachita (N.M.)",
    "@id" : "http://id.loc.gov/authorities/names/no99064312" }

Even with only the Library of Congress link, it is clear that more information is available on this town, which could be helpful in determining if it is the one actually indicated. However, as it is, another researcher would have to reread the original transcription or view the images of the letter to know why Hachita was indicated as the hometown. Since the sergeant URI is discrete from the letter URI, there is no reason that process would be simple or natural. MADS offers a `madsrdf:Source` definition that allows for citation, so we can start there:

"Source": {
    "citationSource" : "tag:ongrannystrail.com:evidence\_03",
    "citationNote" : "my friend from hachita",
    "comment" : "The letter's author is from Arizona and it is very likely that the neighboring mining town of Hachita, NM is the one referred to here." }

This allows us to add a `Source` for the `hometown` assertion without breaking any rules of reference. If there were multiple assertions for `hometown`, the value could easily become an array. Similarly, if there are multiple `Source`s to reference, it may be a `@set` instead. The `comment` property is trouble, though, since it is semantically sensible, but a bit orphaned. The solution may be found either in the value of the `citationSource` or in the `Source` itself, just as description fields in other contexts are often very helpful to humans, but a challenge to parse.

As evidence, the `citationSource` is an `oa:Annotation`, so plenty of description and attribution can be attached to it. However, the `madsrdf:Source` itself is intended as "A resource that represents the source of information about another resource," ([#](https://www.google.com/url?q=http://www.loc.gov/standards/mads/rdf/v1.html%23Source&sa=D&ust=1515534612916000&usg=AFQjCNGoypGIp6yd_6N0s18LI370Y2kSDg)) so it may be simpler to align it with typical `oa:Annotation` structures:

"evidence" : {
    "@type" : \[ "oa:Annotation", "madsrdf:Source \], 
    "citationSource, oa:hasTarget" : "tag:ongrannystrail.com:evidence\_03",
    "citationNote, oa:hasBody" : "The letter's author is from Arizona and it is very likely that the neighboring mining town of Hachita, NM is the one referred to here.",
    "annotatedBy" : "tag:ongrannystrail.com:user\_01",
    "serializedBy" : "tag:rerum.io:annotationTool",
    "motivatedBy" : "oa:describing" }

Obviously, in this case, the keys are demanding simplification in a context file, but they have been expanded here to show their flexibility. In this example, the user who created the assertion that describes the value for `hometown` onto the sergeant's digital anchor is credited, as well as the software that serialized it. The `evidence_03` object is not expanded here, but can be any resource, such as a list that selects both the image segment from the `sc:Canvas` of the specific page and the text of the transcription that details it. Similarly, the `citationNote` is a short string literal, only readable by humans, but could just as well refer to some defined ontology for assertions or comparisons. The power here is that the description is now defended against weak criticism by explaining its description and intention as well as is possible.

Suddenly, `tag:GhostTownWeb:gulino` comes along and introduces a challenge by explaining that [http://www.ohio.edu/people/gulino/Ghosttownweb/New%20Mexico/Hachita/hachita\_nm.html](https://www.google.com/url?q=http://www.ohio.edu/people/gulino/Ghosttownweb/New%2520Mexico/Hachita/hachita_nm.html&sa=D&ust=1515534612919000&usg=AFQjCNETbgrYOCdD61_fUYmyeuWFua-Xcg) shows that Hachita has an adjacent "Old Hachita" that may be the one referred to in this case. His evidence is also valid, but instead of just lobbing criticism at `tag:ongrannystrail.com:user_01`, he must place his dissent into the conversation. If he intends to make a parallel claim, he can offer an alternative value for `hometown` and provide his evidence, letting future scholars decide between them when it is relevant. If he wishes to undermine the assertion `user_01` has made, the discrete nature of annotation means the controversy can be logged directly onto that assertion, without requiring a change to the resulting value of `hometown`. As these annotations chain together, the `@graph` becomes a record of the academic conversation.

## Open Attribution

The idea of citation is not new, but annotation adds an interesting and liberating dimension. Linked Data thrives in a graph, where relationships are equal partners with the nodes they connect. The vast expanse of a Linked Data graph, however, overshadows the significant problem of omitted records and systemic bias. Because annotation can support attribution for claims and creation separately, it is possible to pull nondigital or unwilling records into the graph. In the example above, the assertion that "hachita" meant "Hachita, NM is the sergeant's `hometown`" was novel and correctly attributed to `user_01`. However, this was learned from a transcription on a blog that should be credited to `tag:ongrannystrail.com:DaynaGoochJacobs`. As `user_01`, I can easily create a new transcription object with the content lifted right off the original blog post, but encoded with the page and line annotations that Dayna intended. The resulting annotation is created by me, but attributed to her. If she had no URI before, she will now; if her work was not encoded or discoverable before, it is now. Magic.

Remote attribution becomes particularly powerful when used just as citation. Instead of a simple bibliography, a URI can be discovered or minted for some unphotographed reference book. As the selectors and pointers become more specific, the resolution of information about this completely off-line resource begins to be encoded. The cross-references between archived articles can be encoded and reacted to in a new article and the relationships begin to gain definition retroactively through history. It is a graph without dead-ends.

## Towards a Clear Model for Annotation

Through the decoupling of the URI identity and the descriptions of them that are often conflated as metadata, scholarship may empower the digital anchors for real things to be the supernodes of academic discourse instead of the virtual trading cards of research. Proper annotation and attribution creates verbose and well-documented descriptions of objects, real and digital, that persist when ignored and adapt when challenged. Though technically complex, this graph can and should be simplified through various interfaces for consumers who are interested in only certain aspects of the entire corpus of annotations and description.

The biggest _change_ to data that I suggest is that much of the metadata currently attached to records ought to be upgraded to assertions through annotation. A URI, whether resolvable or not is required for each thing. A label of some sort may be helpful, but isn't sacrosanct. For resources such as digital files, there may be some real metadata to attach, such as modification dates, file format, etc., but nothing that is not encoded in the file itself. Reflexive `seeAlso` and `describedBy` links to contributing resources may be welcome, but since the URI may not be an object at all, it is obviously not required.

Given our working example here, the letter, there are a host of URIs which may be held together or distributed all around the academic world. The encoding of the letter is important, but is just one possible expression of the real thing, so having an authoritative URI—and making sure that it is referenced in the derivative digital objects—avoids confusion or fragmentation of the descriptions. Even what feels like real, physical metadata is often found in error when protocols for taking measurements change, original provenance or dating from historic indices or catalogues is challenged, or descriptors like location or subject change because of political and social revolution.

The URI is the node; the annotations describe the node through assertion. The best assertions identify the agent who makes them and connect to other nodes through their evidence. A well encoded network of annotations creates an environment within which data can be visualized and manipulated in interfaces designed for the specific exploration required. Scholars currently delve into an issue by finding research in a relevant subject area and whose context and approach is congruous to their own research. By recording the academic conversation around these nodes of research, individual scholars are empowered to review scholarship in their own context, even if explicit previous scholarship does not exist, and to explore research in tangential and adjacent fields by making it more accessible and universally described. Instead of encoding for computers what we say about things, we should capture the conventions that pervade our conceptualizations—encode what we are thinking.

The nodes that are the most and least described can be tested by robots for certain qualities—chronological clustering, contradictions and controversy, unexpectedly dominant fields of research, connections to previous research subjects—that may make them interesting to scholars, assisting in discovery. Though nodes are technically equivalent to each other, types representing entities such as events, landmarks, people, corporations, compositions, and abstractions will undoubtedly become as heavy in the graph as they are in the human brain. The challenge to digital humanists is to capture the probabilistic nature of assertion without limiting the ability of any scholar to join the conversation or enter a thought into the public discourse. The natural end of every described resource are literal resources—text, audio, images, visualizations—where humanity is often on display and robots are befuddled for now.
