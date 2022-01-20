---
title: "Authentication and Attribution in RERUM"
date: "2018-05-15"
categories: 
  - "development"
  - "rerum"
coverImage: "rerum.jpg"
---

Any new web service or application must take a considered look at authorization, authentication, and attribution—authorization, to make changes to data; authentication, to ensure those making changes are known; and attribution, to apply proper credit for contributions. The prevailing practice is to authenticate users within applications and using appropriate context to make attributions. Popular transcription software, like [TPEN](http://t-pen.org) and [FromThePage](https://fromthepage.com/), rely on user accounts and a private database to authenticate, attaching attribution based on the user's account information in the interface and whenever the data is exported, for example, as a IIIF manifest document. Our goal to make RERUM a potent supplement to the heavier data APIs these type of interfaces rely on forced us to reevaluate the "obvious" choice to create and authenticate users.

#### Data Services and the User Problem

[caption id="" align="alignright" width="173"][![] (/assets/images/default.jpg)](https://dlcs.io/iiif-img/wellcome/1/a93ab63e-a827-45a1-b6d4-73224f09d455/full/full/0/default.jpg) For Example[/caption]

Annotation services like [Hypothes.is](http://hypothes.is) and [Genius](https://genius.com/web-annotator) follow the user authentication model and work well as plug-ins to other applications, but are never truly integrated. They are much more standards-based and reliable than Facebook comments or modules like Discus, but still require a user account to authenticate. The problem with user accounts is that they expire even faster than users themselves. As an example, let's consider how analog records are made more durable. At `[https://wellcomelibrary.org/iiif/b22282804/manifest](https://wellcomelibrary.org/iiif/b22282804/manifest)`, there is a document representing a book published in 1862. The artifact itself claims J.C. Clendon, M.R.C.S is the author, but it does not lean only on that assertion. Immediately following the authorship statement is a qualifier connecting Clendon to Westminster Hospital and the Hospital School. As further authentication, the title page also offers the Greenwich Medical Society as witnesses to its reading. Finally, to lend trust to the assertion of the credentials presented, a publisher is also presented.

![] (/assets/images/default.jpg) Analog attribution and authentication

#### Knowing

In the arc of the history of scholarship, it may be difficult to check the specific credentials of Clendon, or even to establish his uniqueness. However, the historical footprint and trustworthiness of the affiliated institutions may cast a longer shadow. Certainly, the combination of elements creates a useful attribution. As a data service, then, RERUM requires only an application to authenticate itself, allowing it then to assert whatever it may about its own content. In this way, the `__rerum` property is a trustworthy record of the application asserting the content. If the transcription annotation asserting authorship were saved by Wellcome into RERUM, it would be sent in as:

{    
    @id: "https://wellcomelibrary.org/iiif/b22282804/annos/contentAsText/a0t5",
    @type: "oa:Annotation",
    motivation: "sc:painting",
    resource: {
        @type: "cnt:ContentAsText",
        format: "text/plain",
        chars: "J. C. CLENDON, M.R.C.S.,"
    },
    on: "https://wellcomelibrary.org/iiif/b22282804/canvas/c0#xywh=383,1641,931,65"
}

As an external resource ([details](https://blog.ongcdh.org/development/editing-remote-objects-in-rerum/)), this update action will create a derivative of the (coincidentally non-dereferenceable) annotation and assign a new URI:

{
    @id: "http://store.rerum.io/rerumserver/id/198ab3910ea9d",
    @type: "oa:Annotation",
    motivation: "sc:painting",
    resource: {
       @type: "cnt:ContentAsText", 
       format: "text/plain", 
       chars: "J. C. CLENDON, M.R.C.S.," },        
       on: "https://wellcomelibrary.org/iiif/b22282804/canvas/c0#xywh=383,1641,931,65"
    },
    __rerum: {
        // URI to foaf:Agent for Wellcome
        generator: "http://store.rerum.io/rerumserver/id/28ab39ab5ea8f",
    ... }
}

Among other properties in `__rerum`  the generator property points to the Agent that was created for the application when it obtained its API key. Now, there is a dereferenceable location available _and_ anyone consuming the annotation can trust Rerum to authenticate the Wellcome Library as the generator and that the content is from them. If any other application makes additional modifications, those [versions](https://blog.ongcdh.org/development/versioning-in-rerum/) also identify the generator, allowing for branches or filtering as needed by consuming interfaces.

#### Resolution

In this way, no user is ever authenticated by Rerum and attribution is pushed only as far as is possible with certainty and reasonable durability. In this case, Wellcome makes no claim within the annotation itself as to its attribution and even looking up the manifest only offers the backing of the Library (which may be enough for many cases). Another example is from TPEN: [http://t-pen.org/TPEN/line/101083800](http://t-pen.org/TPEN/line/101083800). This line of transcription looks very similar to the Wellcome example, but includes `_tpen_creator`, an undefined, but consistent property. Someone familiar with TPEN's API could use the "637" value with the `[/geti?uid=](http://t-pen.org/TPEN/geti?uid=637)` service to discover public user information. The flexibility of the authentication system in Rerum allows, of course, for the well-attributed document that takes full advantage of RDF and the Linked Data graph to connect to meaningful and dereferenceable IRIs, but it also degrades without breaking as the external links become harder to resolve or understand.
