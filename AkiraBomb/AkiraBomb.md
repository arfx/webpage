---
layout: default
title: Akira Bomb - Breakdown
nav_order: 2
---


# Akira Bomb - Breakdown


<p align="center"> 
   <img src="Source/Final/Akira-Bomb-UE5-verysmall.gif" width="1200"> 
</p>



<div class="code-example" markdown="1">

<span class="fs-4">
[High-Quality Gif](Source/Final/Akira-Bomb-UE5.gif){: .btn .btn-green}
[Video with Audio](https://twitter.com/antonsfx/status/1684897440166502400){: .btn .btn-purple}
[Artstation](https://antonrichardt.artstation.com/projects/YB4NRb){: .btn .btn-blue}
</span>

</div>


<!--- ![Final - Video with Audio](Source/Final/Akira-Bomb-UE5.mov) --->


---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

# Introduction

I have recreated a version of the famous Akira Sphere Bomb Sequence from the film "Akira" using Unreal Engine 5. This version showcases the breathtaking depiction of destructive power, as a massive energy wave engulfs the city of Neo-Tokyo in a stunning combination of light and destruction.

# Background-Story

To say that this theme has haunted me for years would be an understatement.

I believe anyone who has seen the film "Akira" was deeply impacted by this particular scene. This feeling intensified when I finally decided to read the manga years after watching the movie. (In short, I highly recommended it, as it offers a much more extensive experience than the film.)

Since then, this special shot has never left my mind. I often find myself using that Sequence for small test projects or to explore new techniques and styles. It has become my go-to reference.

<p align="center" width="100%">
    <img width="24%" src="Source/BS/BS-01.gif">
    <img width="24%" src="Source/BS/BS-02.png">
    <img width="24%" src="Source/BS/BS-03.png">
    <img width="24%" src="Source/BS/BS-04.gif">
</p>

This time, I set out with a clear goal in mind

> [!GOAL] 🥅 To complete that **Akira Bomb Shot** + learn new technics and share my process.

# Pre-production

As mentioned before, this is not my first time working on this shot, so I had a clear vision in my mind and plenty of references stored.

I always envisioned an isometric camera angle, with the buildings starting, the sphere central, and occupying the frame over time. Portraying the immense size and power behind this explosion was crucial to me. Hence, I quickly decided to add a second camera angle to increase and see the buildings in closer view when they dissolving.

I knew early on that I wanted to use procedural skyscrapers for this shot, focusing on large shapes rather than intricate designs due to their sheer quantity.

Furthermore, I had always imagined a genuine distortion and resolution of the buildings, which I planned to achieve using the World Position Offset. I also aimed to delve deeper into realistic cloud and smoke behavior, as I had experimented with them in previous versions using Houdini. However, now having the opportunity to work in real-time, I wanted to test the Niagara Fluids System, which I hadn't explored before.

<details>
<summary>

## 🎞 References - Overall Scene
</summary>
    
Akira Movie
<p align="center" width="100%">
    <img width="29%" src="Source/References/ROS-01.gif">
    <img width="40%" src="Source/References/ROS-02.gif">
    <img width="29%" src="Source/References/ROS-03.gif">
</p>

Akira Manga
<p align="center" width="100%">
    <img width="39%" src="Source/References/ROS-04.jpg">
    <img width="59%" src="Source/References/ROS-05.jpg">
</p>

others
<p align="center" width="100%">
    <img width="52%" src="Source/References/ROS-06.png"> 
    <img width="28%" src="Source/References/ROS-07.gif">
    <img width="18%" src="Source/References/ROS-08.gif">
</p>

*[Blade Runner 2033 Labyrinth Game Trailer - Building Windows Size](https://youtu.be/l_tfihRqBnI?t=17)*  - 
*[FickleSwimming - experiments in the Year 2020](https://twitter.com/FickleSwimming/status/1344636130172563456)*  - 
*[Miguel Rodriguez - Akira-Style Explosion](https://80.lv/articles/a-beautiful-akira-style-explosion-made-in-blender/)* 

</details>

# Production

My approach was very basic but as I start with all projects, tackle the unknown task first. Which meant getting that Deformation working.

## 🌍 World Position Offset - Building Deformation


- set position from 3D Sphere Mask for the Building Position via [Collection Parameter](https://www.unrealengine.com/en-US/blog/material-parameter-collections) which was then via Blueprint Construction Script set where the white Sphere is

![3D Sphere Mask colored on Collum via white Sphere Object](Source/WPO/WPO-01-sphere-mask.gif) 3D Sphere Mask colored on Collum via white Sphere Object

![Collum (Building) Material - Sphere Mask](Source/WPO/WPO-02-SphereMask.png)
Collum (Building) Material - Sphere Mask

![Sphere (Target) Blueprint - Position - Construction Script](Source/WPO/WPO-03.png)
Sphere (Target) Blueprint - Position - Construction Script

- next was to get the Sphere Mask also affection the Point and move them away from the Sphere. But how smooth that looks depends on the Polygon Resolution of the Mesh.

![WPO-04-deformation.gif](Source/WPO/WPO-04-deformation.gif)

![Collum (Building) Material - Sphere Mask Deformation Outwards](Source/WPO/WPO-05.png)
Collum (Building) Material - Sphere Mask Deformation Outwards

- affecting the radius of the 3D Sphere Mask when changing the size of the white Sphere.

![adding another parameter (float1) for the radius * RadiusMultipler](Source/WPO/WPO-06.png)
adding another parameter (float1) for the radius * RadiusMultipler

![adding in the Sphere (Target) Blueprint - Construction Script - the Radius (only one axis because I know it increases uniformly)](Source/WPO/WPO-07.png)
adding in the Sphere (Target) Blueprint - Construction Script - the Radius (only one axis because I know it increases uniformly)

- This is all put together in a Level Sequence and animated via Material Parameter + Scale.

![WPO-07.gif](Source/WPO/WPO-08.gif)

---

## 🏬 Procedural City Generation


For the buildings, I quickly know that I wanted/need to have a procedural approach. Since I was interested in procedural buildings before, I was already familiar with some methods.

### multiple Methods

[Procedural Content Generation Overview](https://docs.unrealengine.com/5.2/en-US/procedural-content-generation-overview/)
In Engine Procedural Creation (UE5)

Prebuild Asset in Houdini / Blender (Geo Nodes)
![PB-01-3.png](Source/PB/PB-01-3.png)

WFC - Wave Function Collapse Algorithm

[Wave Function Collapse - Mixed Initiative Demo](https://bolddunkley.itch.io/wfc-mixed)
Online Demo from Martin Donald

[Labs Wave Function Collapse](https://sidefxlabs.artstation.com/projects/DAB6lO)
Houdini to UE5 a direct method

### In Engine Procedural Creation (UE5)

![ueicon](https://external-content.duckduckgo.com/ip3/www.unrealengine.com.ico) 
UE5 {: .label .label-blue }

For the In Engine Procedural City Generation, I needed to upgrade from Unreal 4.27 to Unreal 5.2 which I did in the End anyway.

![PB-06.png](Source/PB/PB-06.png)

[a good starting point for PCG in UE5 - I used it as well](https://youtu.be/aoCGLW53fZg)

In the beginning, it was really stunning how fast I got something. Here I scatter over the whole landscape (by grabbing the landscape Z Height Position) my default building Blocks (3 different higher poly Boxes with some random height)

---

It's in general quite simple, you place a PCGVolume in your scene and create a PCG Graph in which you can similar to Blueprints (but very reduced and different nodes).

An extremely good point on that is how you can Debug each node. By hovering a node a pressing “D”, you get a cyan Dot on your Node which is then shown in the viewport as cubes, redoing that same step, disables the Debug Mode.

Similar to that you can also by pressing “E” when hovering over a node Enable/Disable a node.

In the End, may was very simple.

![PB-08.png](Source/PB/PB-08.png)

![PB-07.gif](Source/PB/PB-07.gif)

ℹ️ But a very big Learning for Unreal Procedural Creation → Enable on all Meshes Nanite

- Issues without Nanite
  
    Before it was all the time laggy as hell + also then it was hiding objects by distance which result in weird popping.

---

![PB-09.gif](Source/PB/PB-09.gif)

The result was already very satisfying, especially when moving the sphere around in the whole scene. But I didn´t find some ways, that I could achieve some major points for me:

- more control over the random height
- more control over the space between the buildings
- rotation to a center point

Why I moved on to the next section.

### Prebuild Asset

#### Blender (GeoNodes)

{: .note }
> ![icon](https://external-content.duckduckgo.com/ip3/www.blender.org.ico)

Some weeks before the start of the whole Unreal Akira Bomb Project, I did already a very rudimentary version of this Building Setup in Blender with Geometry Nodes, which grow my interest in a proper animated scene of that.

That was the spark of that whole Unreal Project.

![2023-04-01 - Blender Geometry Node - Building Setup](Source/PB/PB-03.png)
2023-04-01 - Blender Geometry Node - Building Setup

In short, it was only scattering three different kinds of Boxes (which were also randomized in scale) on a circle object + making some center orientation + stepped 90-degree rotation.

![PB-05.gif](Source/PB/PB-05.gif)

[Source File of the Geometry Node Building](Source/quick_building_geonode.blend)
Source File of the Geometry Node Building

---

#### Houdini

![icon](https://external-content.duckduckgo.com/ip3/www.sidefx.com.ico) HOUDINI {: .label .label-orange }

Because in Blender everything still overlapped and had no easy way to increase the polycount ([what I need for the deformation of the WPO](AkiraBomb-Breakdown.md#World%20Position%20Offset%20-%20Building%20Deformation)) by the height of the Buildings or add later UV for each of these Buildings. I decided I recreated this in Houdini in a very similar approach.

- Build 3 different 1x1 Box House
- created already a Separation of roof UV and Walls(Height) UV
- scatter some points on a plane
- set point to direction to center
- added steeped 90degree rotation
- added randomized pscale/scale attributes to point
- copied box house to points
- created a second scatter point with the same steps but different randomize
- used first result to check for overlaps with the second scatter result
- removed these and combined but results
- fill in between spaces with smaller building (same method) +combined that again
- new added on the highest buildings some additional deco stuff (which was also boxes)
- adjusted Height UVs by the pscale + height scale
- Done

![step through the Houdini Building process](Source/PB/PB-11.gif)

step through the Houdini Building process

## ☁️ Niagara Fluids - Clouds Motion

One completely new item I never got around to trying out in the last few years was the Niagara Fluids from the last Unreal Engine versions.

I have always liked to play around with other fluids systems whether in Cinema 4D, Maya, Max, Realflow, Houdini or Blender and so I gave me a limitation only use the Unreal Engine Niagara Fluids to make all smoke / clouds in the complete sequence.

First, I opened some Niagara Fluids templates and changed some values to see how they behaved. Surprisingly, I found that they were divided into two different emitters. One for source emitters and the other for the whole fluid behavior. Thanks to my previous long experience in Unreal Niagara System, it was very easy to create a source emitters to create any kind of motion.

![Niagara Fluid - both Emitter](Source/NF/NF-01.png)

Niagara Fluid - both Emitter

Mainly I used Forces to drive the Source Emitters Particle and animated these over the Sequence Timeline.

More Issues I had in the beginning with that the Startframes where all only points that wasn´t merged like real clouds, which I tried by making longer sims before they are pre-moved via Force. But I got this later in the process solved by spawning the particle from a static mesh (which was only some place planes), before I use the Torus Location with additional Curl Noise Offset.

![Final Source Emitter Spawn Mesh](Source/NF/NF-04.png)

Final Source Emitter Spawn Mesh

![Niagara Cache](Source/NF/NF-03.png)

Niagara Cache

Also helped later on the Sequencer the Niagara Fluid Cache function. Where you bake you simulation down and can modify a bit this Cache in stretching, offsetting, etc.

In general I struggelt in

![iterations over the Niagara Fluid System](Source/NF/NF-02.gif)

iterations over the Niagara Fluid System

In general, I struggled with the resolution and detail from the clouds in both shots.

Especially since this goes very fast on the GPU depending on I increased the “Resolution Max Axis” of the Niagara System (which are the voxel of the sim). At the beginning I still used the Uniform World Size, but I notice at the latest with the second shot that I should split them into the individual axes.

For the second shot I use a different Niagara Fluid System from the beginning, because I don't have to calculate the full circle around the sphere. But above all, the World Space for the different axes has helped a lot because this shot is very long, but not veryhigh.

Which was perfect to reduce the Z Axis and increase the X Axis.

![Sideview of the second Shot](Source/NF/NF-05.png)
Sideview of the second Shot

---


# Challenges - Struggle

## 🎵 SFX
For the final release, the video would need audio or sound effects (SFX). However, this is an area where I had my weaknesses and lack of experience. So, I recognize in the process of that Sequence that this poses another completely new challenge for me.

 🆓 For that I looked into some free SFX sites

| [Mixkit](https://mixkit.co/free-sound-effects/) | [Freesound](https://freesound.org/) | [Pixabay](https://pixabay.com/sound-effects/) |
|--|--|--|

I started by putting some random SFX together in the Blenders Sequencer together, but I haven´t found everything that I wanted. Also, they definitely needed some tweaking because some were why to long or short in length and I think too high (if that is the right term in that context), etc. Also, I needed really fast some rough timing which I did in Blender by importing the Image Sequence from the Export Unreal Scene via Movie Render Queue.

After that, I looked at some tools that can create SFX and audacity came right to my mind. (With worries and fears because I was often struggling that tool. ) But with a bit of help from a Friend (programmer + musician, best combo for that) we create something in it. But he moved me a bit away from that so that we ended up in [Reaper](https://www.reaper.fm/download.php), we I created most of these ending noise/beep(peep) SFX.

---

## 💥 Impact Frames

Since I love Impact Frames, I was very early ready to invest more time in it as well.

I had also been playing around with post FX shaders for a few weeks before, especially for impact frame moments. Even if I had a good first approach with it, these results were always too static for me. Which is why I switched to hand-drawn impact frames during the course of the progress.

Or better I mix of both , I made my drawing with transparent background and used the invert flip from the post FX shader and the InEngine footage.


<details>
<summary>

### Reference - Impact Frame
</summary>

<p align="center" width="100%">
  <img width="32%" src="Source/IF/IF-04.png">
  <img width="35%" src="Source/IF/IF-11.jpg">
  <img width="19.6%" src="Source/IF/IF-07.png">
</p>

*2023-05-02 - previous created Post Shader* |
*[Diana Lott - "Impact Frames" Shader Effect](https://www.artstation.com/artwork/mDAly9)* |
*[VFX Apprentice - Drawing](https://youtu.be/mcOozpmIxLw?t=199)*


<p align="center" width="100%">
  <img width="32%" src="Source/IF/IF-08.png">
  <img width="32%" src="Source/IF/IF-10.jpg">
  <img width="32%" src="Source/IF/IF-09.png">
</p>

*[Impact Frames Bot](https://twitter.com/impactframesbot/status/1286222816254328833/photo/3)* | 
*[https://www.sakugabooru.com/post/show/2313](https://www.sakugabooru.com/post/show/2313)* | 
*[kViN](https://twitter.com/Yuyucow/status/775398621030252545/photo/2)*


</details>

### Engine Shader - Post Effect

![Shader Graph - for the Invert Post FX Shader + additional Parameter for contrast, saturation, etc](Source/IF/IF-05.png)
Shader Graph - for the Invert Post FX Shader + additional Parameter for contrast, saturation, etc

![Black without EyeAdaption - White with EyeAdaption](Source/IF/IF-06.gif)
Black without EyeAdaption - White with EyeAdaption

In the beginning it was very important for me that I could animated some of these values also over the sequence, which I shared some parameters and added then in the Global Post Process as “Post Process Material”.

### Drawing

The Drawing Process was quite I started with a still inverted Frame from the Engine and drew over it.


<p align="center" width="100%">
  <img width="32%" src="Source/IF/IF-02.gif">
  <img width="32%" src="Source/IF/IF-06.gif">
  <img width="23.4%" src="Source/IF/IF-01.gif">
</p>

<!-- ![drawing process - starting with one rendered frame - first version](Source/IF/IF-02.gif)
![final version - with out Sequence blow](Source/IF/IF-03.gif)
![quick tablet drawing test](Source/IF/IF-01.gif) -->

drawing process - starting with one rendered frame - first version |
final version - with out Sequence blow |
quick tablet drawing test

---

## ⛅ Scene Lighting
For the Scene Lighting, I had at the beginning really a direction in my mind. From the original Scene Reference, there is a different version already. The Movie has a more daylight approach and gets darker over the sequence. For the Manga, it´s always quite dark but still, there are some shades visible.

This is why I started to collect some different City Lighting Reference. Still, after that, I wasn´t so sure which road to go.

<details>
<summary>

### Reference - Lightning
</summary>

<p align="center" width="100%">
    <img width="32%" src="Source/References/lighting/SL02.jpg"> 
    <img width="32%" src="Source/References/lighting/SL11.jpg">
    <img width="24%" src="Source/References/lighting/SL14.jpg">
</p>

<p align="center" width="100%">
    <img width="26%" src="Source/References/lighting/SL04.jpg"> 
    <img width="23%" src="Source/References/lighting/SL13.jpg">
    <img width="22%" src="Source/References/lighting/SL10.jpg">
    <img width="22%" src="Source/References/lighting/SL15.jpg">
</p>

<p align="center" width="100%">
    <img width="20.5%" src="Source/References/lighting/SL05.jpg"> 
    <img width="24.2%" src="Source/References/lighting/SL12.jpg">
    <img width="21%" src="Source/References/lighting/SL03.jpg">
    <img width="24.7%" src="Source/References/lighting/SL09.jpg">
</p>
<p align="center" width="100%">
    <img width="18%" src="Source/References/lighting/SL06.jpg"> 
    <img width="24%" src="Source/References/lighting/SL08.jpg">
    <img width="25%" src="Source/References/lighting/SL07.jpg">
    <img width="26%" src="Source/References/lighting/SL01.jpg">
</p>

</details>

<!-- ![SL02.jpg](Source/References/lighting/SL02.jpg)
![SL11.jpg](Source/References/lighting/SL11.jpg)
![SL14.jpg](Source/References/lighting/SL14.jpg)

![SL04.jpg](Source/References/lighting/SL04.jpg)
![SL13.jpg](Source/References/lighting/SL13.jpg)
![SL10.jpg](Source/References/lighting/SL10.jpg)
![SL15.jpg](Source/References/lighting/SL15.jpg)

![SL05.jpg](Source/References/lighting/SL05.jpg)
![SL12.jpg](Source/References/lighting/SL12.jpg)
![SL03.jpg](Source/References/lighting/SL03.jpg)
![SL09.jpg](Source/References/lighting/SL09.jpg)

![SL06.jpg](Source/References/lighting/SL06.jpg)
![SL08.jpg](Source/References/lighting/SL08.jpg)
![SL07.jpg](Source/References/lighting/SL07.jpg)
![SL01.jpg](Source/References/lighting/SL01.jpg) -->

### Lightning

Why I played a bit around in Unreal with the AWESOME Lighting Shortcut. You need to have DirectionalLight placed in your Scene.

<aside> 👌 press **Ctrl + L** and hold while moving the mouse

</aside>

With that, you can find fast and easy your right Light Direction/Mood and continue on that.

In the end, I used some Light from behind but also daytime because the Bloom and Eye Adaption made the rest of the Scene anyway dark next to the Bright White Sphere.

![SC-01.gif](Source/SC/SC-01.gif)

---

# Post Production

Because it was all done in Unreal there was not much Post Production, I only add in Davinci Resolve a bit more Zoom + Motion Blur around the Impact Point and replace the inverted Post FX frame to the still painted Impact Frames, extended the Start + End Full Frame Color and added the SFX.
