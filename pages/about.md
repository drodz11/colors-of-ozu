---
title: About
layout: page
permalink: /about.html
# Edit the markdown on in this file to describe your collection
---

{% include about/jumbotron.html %}

## Intro


_"The unexpected humanity of the Ozu film is made possible by the rigor of its construction.
In an Ozu film...one sees all the supports, and all of them are equally essential"_
- Donald Richie, _Ozu_ (1974, University of California Press)

_"No longer should we be bound to cinema as truth that exists only in a fleeting 24 frames-per-second.
We instead should make as many frames as we like, and hold them in our hands for as long as we want"_
- Kevin L. Ferguson, [Volumetric Cinema](http://mediacommons.org/intransition/2015/03/10/volumetric-cinema) (2015)

Begun as a research project in March of 2020 during the COVID-19 pandemic, _Colors of Ozu_ is an on-going film analysis project that leverages digital tools and technologies to novelly and creatively examine the final six films of Japanese filmmaker [Yasujirō Ozu](https://en.wikipedia.org/wiki/Yasujir%C5%8D_Ozu). These works--which include _Equinox Flower_ (1958), _Good Morning_ (1959), _Floating Weeds_ (1959), _Late Autumn_ (1960), _The End of Summer_ (1961), and _An Autumn Afternoon_ (1962)--are also unique in his oeuvre for being the only films the prolific director and screenwriter even produced in color. While his films have been widely regarded and studied for their distinctive visual style, relationship to Japanese society and culture, and other aesthetic and narrative qualities, little critical attention has been given to investigating Ozu's use of color at the end of his career. _Colors of Ozu_ seeks a dual purpose in adding this element to the existing, broad field of criticism around Ozu's work and applying the tools and methods of digital humanities (DH) research to strengthen the bond between DH and film/media studies. The hope of this project is to inspire media scholars to explore research methods beyond traditional audio-visual analysis and DH practitioners to expand their purview into new cultural heritage domains by applying digital scholarship methods to the study of filmic texts.


## Critical and Theoretical Contexts

<br>
<br>
#### _AV in DH_
<br>
As discussed by Susan Hockey in her 2004 chapter "The History of Humanities Computing," the field of DH has tended to put textual sources at "center stage" within the development of the discipline. Using computers to analyze and generate new knowledge about/from textual corpora--either by employing "distant viewing," annotation, or otherwise uniquely digital or computational techniques--has been a mainstay of the field since its earliest incarnations in the mid-20th century. It is only relatively recently that technology with the capacity to run similar computational analysis on moving-images or other visual cultural materials has become accessible to scholars and artists. Beginning in the early 2000s with Lev Manovich's groundbreaking work in [Cultural Analytics](http://lab.culturalanalytics.info/), we have seen a slow rise in this subject area within DH. Scott Weingart's analysis of submissions to the [ADHO Conference](http://adho.org/conference) between 2015-2017 is helpful in quantifying this trend, as his finding shows an uptick from roughly 2% to 9% for submissions within the "film and media studies" subject area, while the "audio, visual, and multimedia" topic jumped from roughly 9% to 13%. While this observational data from one international conference does not necessarily signal a sea change in DH, it does suggest a growing facet of the field that deeply and meaningfully interrogates visual culture, cinematic history, and the massively proliferating network of digital images which surrounds contemporary life.



#### _Deformative Humanities & Digital Surrealism_




#### _The Films of Yasujirō Ozu_


## Methods & Tools


Tools and applications used in this project include:

  * [FFmpeg](https://www.ffmpeg.org/)
  * [ImageJ](https://imagej.nih.gov/ij/)
  * [Imj](http://www.zachwhalen.net/pg/imj/)

These tools are all free and open-source. FFmpeg perhaps carries the steepest learning curve in that its use requires familiarity with the command-line and knowledge of FFmpeg structure and syntax. Alternatively, ImageJ, a GUI-based image analysis application developed by the National Institute of Health, has a multitude of functionalities, options, and settings which may not be immediately intuitive to novice users. Information and resources related to using these tools can be found in the "Resources & Learning Tools" section at the bottom of this page.

#### _Extracting a series of stills or "slices" from a digital video file_

A number of methods exist for transforming a digital video file into a series of still images. As Ferguson describes in ["Digital Surrealism"](http://www.digitalhumanities.org/dhq/vol/11/1/000276/000276.html), the Export feature built into the Quicktime Media Player (native to Mac OSX) can accomplish this in a fairly straightforward way. Similarly, Mark Sample's ["Sample Reality"](https://www.samplereality.com/) blog provides helpful [step-by-step instructions](https://www.samplereality.com/2017/11/15/image-analysis/) for the same procedure using the VLC media player.

The method I will provide here uses an FFmpeg command to create a series of still images. The benefits of this method are two-fold: 1) it does not rely on access to proprietary, platform-specific software, and 2) unlike the VLC method--which requires a video file be played back in real time--the FFmpeg command will extract stills at a regular interval over any duration in a fraction of the time. Additionally, the FFmpeg method allows for more control over the image output with regard to maintaining important formal characteristics. Namely, the aspect ratio.

The following command, modified from an [example provided on the FFmpeg Wiki](https://trac.ffmpeg.org/wiki/Create%20a%20thumbnail%20image%20every%20X%20seconds%20of%20the%20video) after [consulting with the good folks who run the FFmpeg Twitter account](https://twitter.com/clavilux_of_FL/status/1239969705575636993), was used to create the stills:

```bash
ffmpeg -i inputvideo.mp4 -vf fps=0.5,"scale=iw*sar:ih,setsar=1" directory/outputname_%04d.png
```

This command consists of four key parts:

  * `ffmpeg` = calls ffmpeg to start the command
  * `-i inputvideo.mp4` = specifies the input file (in practice this would be the actual name of the video file)
  * `-vf fps=0.5,"scale=iw*sar:ih,setsar=1"` = this "video filter" (`-vf`) samples 1 frame for every 2 seconds of video and scales the output to square pixels (see below for an explanation of why this is an important modification)
  * `directory/outputname_%04d.png` = specifies the directory for the stills to be saved, a sequential naming convention (outputname_0001, outputname_0002, and so on), and file format for the stills (this can, alternatively, be `.jpeg` or another file-type)

After running this command, the output directory will become populated with still images, sequentially numbered and running the length of the video file (for a feature-length film, this will be 3,000-4,000 image files). Executed as written above, the outputted stills will look like this:

{% include feature/item-figure.html objectid="coll006" %}

If, however, we run the command without the `"scale"` option, our stills will look like this:

{% include feature/item-figure.html objectid="coll007" %}


Notice how this second image looks "squished" or "stretched" in comparison to the first. This distortion is caused by the non-square aspect ratio of the pixels in the source video. These need to be re-encoded to square aspect ratio in the stills using the `"scale"` modification. This, in turn, renders the full image in the proper 1.37:1 "Academy" aspect ratio (note that _pixel_ and _image_ aspect ratios are two related, but different, features of a digital image). While the question of pixel or image aspect ratio may seem like a small technical detail, I make a point of this because, for the purposes of analyzing the formal and expressive characteristics of Ozu's work, it is important that our captured data (or [capta](http://www.digitalhumanities.org/dhq/vol/5/1/000091/000091.html), as Johanna Drucker reminds us) align as closely as possible to the films' construction. Unlike many of his contemporaries, Ozu never made feature films using popular widescreen cinematography first introduced in the early 1950s. As accounted by David Bordwell, he is [quoted](http://www.davidbordwell.net/blog/2011/04/07/a-matter-of-scope/) saying that the widescreen frame of Cinemascope reminded him of a roll of toilet paper. He remained committed to the canvas of the Academy aspect ratio throughout his career making sound films. As such, we should strive to minimize distortions and the introduction of other unintended or unwanted artifacts into our dataset by ensuring our stills reflect, as accurately as possible, the way the film is meant to be seen.

For more information on the often very confusing issues related to pixel aspect ratio, see the "Resources & Learning Tools" section.


## Analysis   


[coming soon]


## Resources & Learning Tools

#### FFmpeg

  * [ffmprovisr from the AMIA Open Source Committee](https://amiaopensource.github.io/ffmprovisr/)
  * [Introduction to Audiovisual Transcoding, Editing, and Color Analysis from The Programming Historian](https://programminghistorian.org/en/lessons/introduction-to-ffmpeg)
  * [FFmpeg Bug Tracker & Wiki](https://trac.ffmpeg.org/)
  * [Official Documentation](https://www.ffmpeg.org/documentation.html)

#### CLI (Command Line Interface)

  * [Introduction to the Bash Command Line from The Programming Historian](https://programminghistorian.org/en/lessons/intro-to-bash)

#### Aspect Ratio & Pixel Aspect Ratio

  * [Filmmaker IQ's Epic Lesson in the History of Aspect Ratio](https://nofilmschool.com/2013/06/visual-history-of-aspect-ratio)
  * [Ashley Blewer's primer on pixel aspect ratio](https://training.ashleyblewer.com/presentations/video.html#27)
  * [Wikipedia article on pixel aspect ratio](https://en.wikipedia.org/wiki/Pixel_aspect_ratio)


## Works Cited

Hockey, S. (2004) [“The History of Humanities Computing,”](http://www.digitalhumanities.org/companion/view?docId=blackwell/9781405103213/9781405103213.xml&chunk.id=ss1-2-1) A Companion to Digital Humanities, ed. Susan Schreibman, Ray Siemens, John Unsworth. Oxford: Blackwell

Weingart, S. (2017) “Submissions to DH2017 (pt. 1),” http://scottbot.net/submissions-to-dh2017-pt-1


This site was created and is maintained by Dave Rodriguez, Resident Media Librarian at Florida State University. Send inquiries to dwrodriguez[at]fsu.edu
