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

_Colors of Ozu_ is an on-going film analysis project that leverages digital tools and technologies to novelly and creatively examine the final six films of Japanese filmmaker [Yasujirō Ozu](https://en.wikipedia.org/wiki/Yasujir%C5%8D_Ozu). These works--which include _Equinox Flower_ (1958), _Good Morning_ (1959), _Floating Weeds_ (1959), _Late Autumn_ (1960), _The End of Summer_ (1961), and _An Autumn Afternoon_ (1962)--are also unique in his oeuvre for being the only films the prolific director and screenwriter even produced in color. While his films have been widely regarded and studied for their nuanced story-telling, universally resonant characters, and distinctive visual style, little critical attention has been given to investigating Ozu's use of color at the end of his career. _Colors of Ozu_ seeks a dual purpose in adding this element to the existing, broad field of criticism around Ozu's work and applying the tools and methods of digital humanities (DH) research to strengthen the bond between DH and film/media studies. The hope of this project is to inspire media scholars to explore research methods beyond traditional audio-visual analysis and DH practitioners to expand their purview into new cultural heritage domains by applying digital scholarship methods to the study of filmic texts.


## Theory/Context


[coming soon]

## Methods/Tools


Tools and applications used in this project include:

  * [FFmpeg](https://www.ffmpeg.org/)
  * [ImageJ](https://imagej.nih.gov/ij/)
  * [Imj](http://www.zachwhalen.net/pg/imj/)

These tools are all free and open-source. FFmpeg perhaps carries the steepest learning curve in that its use requires familiarity with the command-line and knowledge of FFmpeg structure and syntax. Alternatively, ImageJ, a GUI-based image analysis application developed by the National Institute of Health, has a multitude of functionalities, options, and settings which may not be immediately intuitive to novice users. Information and resources related to using these tools can be found in the "Resources & Learning Tools" section at the bottom of this page.

### Extracting a series of stills from a digital video file

A number of methods exist for transforming a digital video file into a series of still images. As Ferguson describes in ["Digital Surrealism"](http://www.digitalhumanities.org/dhq/vol/11/1/000276/000276.html), the Export feature built into the Quicktime Media Player (native to Mac OSX) can accomplish this in a fairly straightforward way. Similarly, Mark Sample's ["Sample Reality"](https://www.samplereality.com/) blog provides helpful [step-by-step instructions](https://www.samplereality.com/2017/11/15/image-analysis/) for the same procedure using the VLC media player.

The method I will provide here uses an FFmpeg command to create a series of still images. The benefits of this method are two-fold: 1) it does not rely on access to proprietary, platform-specific software, and 2) unlike the VLC method--which requires a video file be played back in real time--the FFmpeg command will extract stills at a regular interval over any duration in a fraction of the time. Additionally, the FFmpeg method allows for more control over the image output with regard to maintaining important formal characteristics. Namely, the aspect ratio.

The following command, modified from an [example provided on the FFmpeg Wiki](https://trac.ffmpeg.org/wiki/Create%20a%20thumbnail%20image%20every%20X%20seconds%20of%20the%20video) after [consulting with the good folks who run the FFmpeg Twitter account](https://twitter.com/clavilux_of_FL/status/1239969705575636993), was used to create the stills:

```bash
ffmpeg -i inputvideo.mp4 -vf fps=0.5,"scale=iw*sar:ih,setsar=1" directory/outputname_%04d.png
```

This command consists of four key parts:

  * `ffmpeg` = calls ffmpeg to start the command
  * `-i inputvideo.mp4` = specifies the input file (in practice this would be the actual name of the video file)
  * `-vf fps=0.5,"scale=iw*sar:ih,setsar=1"` = this "video filter" samples 1 frame for every 2 seconds of video and scales the output to square pixels (see below for an explanation of why this is an important modification)
  * `directory/outputname_%04d.png` = specifies the directory for the stills to be saved, a sequential naming convention (outputname_0001, outputname_0002, and so on), and file format for the stills (this can, alternatively, be `.jpeg` or another file-type)

After running this command, the output directory will become populated with still images, sequentially numbered and running the length of the video file (for a feature-length film, this will be 3,000-4,000 image files). As written above, the outputted stills will look like this:

{% include figure.html filename="objects/aaa_0090.png" caption="From _An Autumn Afternoon_ (1962)" %}


## Analysis   


[coming soon]


## Resources & Learning Tools

[coming soon]


## Works Cited

[More to come...last updated 2020-03-24]

This site was created and is maintained by Dave Rodriguez, Resident Media Librarian at Florida State University. Send inquiries to dwrodriguez[at]fsu.edu
