---
title: "Experimenting with Client-side Line Detection"
date: "2018-06-21"
categories: 
  - "experiments"
tags: 
  - "experiments"
  - "image-manipulation"
  - "thinking-aloud"
  - "transcription"
---

## Does not compute

Using an "old" iPad on a plane to review transcription data was a clarifying task. For all the advances in research technologies, even simple tasks, such as viewing manuscript images on an institution's website can crash a five year old browser, effectively rendering it inaccessible. I am not willing to accept that the very tools and scripts we have been building to make these resources more interactive and discoverable are also rendering them inaccessible on aging (but still functioning) hardware. There is a place for discussing [progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement) design, [progressive web applications](https://en.wikipedia.org/wiki/Progressive_Web_Apps), and emerging mesh-style protocols like [IPFS](https://ipfs.io), but I'm going to be very targeted in this post. The choke point of manuscript image analysis has always been the server-side task of layout analysis (as in our [TPEN](https://blog.ongcdh.org/development/t-pen-development-advance-post/) application) and has been making great advances with the addition of machine learning in computing clusters ([Transkribus](https://transkribus.eu/) and [others](https://amdigital.co.uk) are in the spotlight at the moment). I am calling for an algorithm simple enough to run in the browser of an underpowered machine that can accomplish some simple tasks on "decent" photography.

## WiFi not available

Imagine you are in a [magic tincan](https://youtu.be/q8LaT5Iiwo4?t=2m) that zips through the air at high speeds and connects you simultaneously to all the world's knowledge. From these heights you work away, paging through images of a medieval manuscript and transcribing it into a digital language that encodes it for limitless reuse. You are working at [t-pen.org](http://t-pen.org) not because it is the best at image analysis, but because its servers run an algorithm good enough for your clean document and do so in real time, returning line detection on each page in mere seconds—at least it used to. As the Internet connection gets spottier, the responses become slower. You wait eight seconds... thirty seconds... and then silence. Your mind reels trying to recall that YouTube video you watched on EM waves and to resist blaming this outage on a vengeful god. A full minute without WiFi passes and you realize there is a chemical bomb on your lap that cannot even entertain you. It would have been more reliable to carry a pencil and a sheet from a mimeograph with you than this unusual pile of heavy metals, polymers, and pressure-cooked sand. What else about your life have you failed to question? Do you even really grasp the difference between air speed and ground speed? How planes!?

## Dash blocks and breathe

I was unable to answer all these questions for myself, but I did start to wonder about what minimum effective image analysis might look like. Existing algorithms with which I was familiar used very generic assumptions when looking for lines. The truth is that manuscripts can be quite diverse in form, but photographs of them taken for transcription strongly tend towards some similarities. For this experiment, I am dealing with manuscripts where the text is laid out in rectangular blocks and takes up at least a quarter of the image. I wanted to find something that could deal with the dark mattes, color bars, rulers, and other calibration paraphernalia. Ideally, it would be able to find text boxes and the lines within, even if the original image was slightly askew or distorted. Algorithms that looked only for dark areas were confused by mattes and often rated a red block as equivalent to a column of text. Strictly thresholding algorithms lost faded tan scripts on parchment easily. My solution would need to be good enough to run in a vanilla state and quick enough to calibrate for special cases if needed.

I did not look for dark spots, but for "busyness" in the page. While [some scripts](https://en.wikipedia.org/wiki/Devanagari) may have regions of strong linear consistency, most scripts (even character-based ones) are useful by their contrast to the plainness of the support medium.

[caption id="attachment_807" align="aligncenter" width="520"]![]({{ site.baseurl }}/assets/images/db1-e1529435041314-520x247.jpg) Sample image processed for "busyness"[/caption]

I began, on that airplane ride, to write a simple fork of some canvas element JavaScript filters I had bookmarked a long time ago. Simply, I redrew the image in the browser as a representation of its busyness. What I [dropped on Plunker](http://embed.plnkr.co/BYDuwd/) when I landed took each pixel and rewrote it depending on the difference between itself and the adjacent pixels on the row. I was excited that with three very different samples, the resulting visualization clearly identified the text block and reduced the debris. By then the plane had landed and I put away my childish fears that technology would ever abandon me.

## Finding Value

In the [next post](https://blog.ongcdh.org/uncategorized/exploiting-line-detection/), I will discuss why I opened up this old pile of code again to see if I could teach it a few new tricks. I am curious, though, what snippets or small concepts do you have in a dusty digital drawer that might be useful. Use the comments here to advertise the github repo you haven't contributed in years, but still haven't deleted.
