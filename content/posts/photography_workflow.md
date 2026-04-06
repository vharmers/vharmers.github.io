---
title: "Photography Workflow"
date: 2026-04-06T16:48:10+02:00
author: "Valentijn Harmers"
draft: true
showtoc: true
description: "My Photography Workflow explained"
categories: ["Photography"]
tags: ["editing", "advise", "beginner"]
---

# Photography Workflow
Some time ago, I published the post (Shooting for the edit)[/posts/shooting_for_the_edit]. Here I explained that I often shoot in JPEG instead of RAW. I now had the opportunity to focus my effort on practicing photography and building a good set of habits.

It therefore became time to revisit the RAW file format again. I was however lacking one important thing: a proper workflow. Simply importing all my RAW file into Apple Photos was not going to work. I needed to have control on the culling, editing, export and storage process.

![Workflow Diagram](photography_workflow.excalidraw.png)

## Import
The first step is to get the photos of the camera. Camera manufacturers do often provide their own tools for this. Nikon provides its Transfer Utility, which is part of the NX Studio software package.

Apple Photos can also import photos from camera’s but offers limited culling options. You therefore end up storing a lot of photo’s that you don’t want to keep. You can delete these photos after the import of course, but all of them first get send to iCloud. My Macbook ends up using up a lot of processing power to prepare and upload photos that I am going to delete later on.

I would rather store the imported images in a separate folder on my local storage and only upload the photos that I want to keep. I eventually ended up using the Image Capture application, which is preinstalled on macOS. This application can pull the photo of the camera and dump them in a given folder—just what I needed.

I also played around with Nikon’s Wireless Transmitter Utility. This application allows you to transmit your photos over your local wireless network. You have to install the utility on your computer and set the camera up to connect to your local WiFi.

I had to fiddle around a bit, but I eventually managed to pair the camera to my Macbook. The major advantage of this setup is that you don’t have to connect the camera to your computer with a cable. It is however impractical for transferring a large amount of photos because the transfer speeds are not that fast and you have to manually select the photos you want to transfer.

There is an option to automatically mark new photos, but this didn’t end up working that well for me. It’s probably because I have the camera paired with my Smartphone while in the field. Maybe the photos get marked for Smartphone transfer instead of PC transfer. Anyway, I ended up having to go into the preview menu of the camera and mark every image I took that day.

I now use Image Capture application for large imports and the Transfer Utility for small ones.

## Cull
Not all taken images are worth keeping. It is therefore handy to have the ability to quickly shift through your images and get rid of the ones you don’t like. I like to divide my images into three groups: delete, keep and keepsakes. The photos in the delete group get deleted, while the ones in the keep group get more attention in the editing process and stored afterwards. The keepsake group sits between these two.

The images in this group aren’t special enough to be put in the keep group, but I still want to keep them as a reminder of that day. These images get a simple edit and are exported to a more highly compressed format like JPEG or HEIF before being stored.

Nothing stops you from using the default image viewer of your Operating System for the culling process. It is, however, not the best way to go at it. You will need something that allows you to flag, rate and compare your images side by side. There are dedicated applications for this task, but a lot of photo editing products also come with these features.

I tried out different products, but struggled to find something that suited my needs. Open Source products like Darktable and RawTherapee are free to use, but difficult to use because of their complexity. Commercial solutions like Lightroom or Luminar Neo are easier to use, but are too expensive for a hobbyist like me. I eventually settled for Nitro.

Nitro is only available for the Apple ecosystem and integrates with Apple Photos. It also makes use to Apple’s RAW engine instead of using their own. My transition to Nitro was easy since it behaves same as Apple Photos.

A lifetime license of Nitro will cost you around a 60 euros, which is quite a reasonable price when compared to other commercial alternatives. I presume this is because they built on top of Apple’s RAW engine and only develop for the Apple ecosystem which greatly reduces complexity.

Nitro is however far from perfect; The sidebar often won’t properly expand or collapse, the filter option is buggy, keyboard shortcuts don’t work sometimes, and the UI contains a lot of duplicate components. Luckily, you can customize the top toolbar and remove all the buttons up there.

![Nitro Screenshot](nitro.jpg)

After importing all the files, going over the images. I usually take a couple of photos of the same scene and aim to flag all but one for discartion. There are enough times where I don’t like any of them and discart all of them. Then I set the filter to only show me photos that are not flagged and the second round of the culling process begins.

Now I try to determine which photos belong in the keepsake group and which ones to put in the keep group. I rate the keepsakes at one or two stars, while the keepers get a rating of three stars or more.

## Edit
I usually don’t do anything excessive unless I’m clearly going for a creative edit. De keepsakes get some basic editing work while I spend more time on de keepers. During my edits, I go through the following stages: Cropping, Exposure, Contrast, Saturation/Vibrance, Tone Curve, HSL, and Vignette.

### Cropping
During the cropping stage, my aim is to remove distracting elements from the edges of the composition. Of course I aim to prevent this from happening while taking the photograph in the field, but sometimes it can’t be helped. There are also enough times where I want to use a 4x3 or 16x9 aspect ratio. Some cameras support setting this up while taking the photo, but mine doesn’t.

### Exposure
Just like with composition, my aim is to get the exposure right in camera. But there are times when minor adjustments are needed. Usually, the correction is not more than a single stop though. The aim is to make the image look neutral. I pay special attention to the midtones, since the highlights and the shadows get targeted during the Tone Curve adjustment.

### Contrast
Contrast increases the difference between the brightest and darkest parts of your image. It add more drama. In most cases, I add a little contrast depending on the image. If an image has mostly dark parts or mostly light parts, isn’t better to target the right areas with the Tone Curve adjustment.

### Saturation and Vibrance
Increasing Saturation and Vibrance allows you to create more ‘Color Pop’. While Saturation brightens all the colors in your image, Vibrance only targets the less saturated colors, making it a more subtle adjustment.

I often add a bit of Saturation and Vibrancy with nature photos, but it makes less sense with photos taken in urban environments, since cement and concrete aren’t very colorful. You can also target specific colors with the HSL adjustment tool.

### Tone Curve
The Tone Curve is a powerful tool. It allows you to make precise adjustments to the brightness of specific parts of your image. Using the Tone Curve properly does require to know how to read the histogram.

In your editing program, you should see a little graph. This graph is the histogram and it shows how many dark or bright tones your image has. If you take a photo of a dark subject, then the peak of the graph will be on the left side. If you take a photo of a bright subject, the peak of the graph will be on the right side, and when you take a photo of a neutral subject the peak of the graph will be in the center. Photo’s of landscapes often have two peaks, one representing the bright sky and the other representing the darker landmass.

We can use the Tone Curve to brighten up the landmass and darken de sky or do the exact opposite. Oftentimes, the curve takes on the shape of an S. An S-curve can be used to increase contrast while a reverse S-curve can be used to reduce it.

I often start by placing the center-point in the middle of the graph data. This can be in the middle, but also be more to the left or right depending on where most of the color information is. Then I make two more points. One on the left of the center-point and one on the right. Lastly I manipulate the left and right points until I get the desired effect.

Here are some examples of what that looks like:

![Tone Curve Examples](tone_curve.jpg)

### HSL
The HSL sliders allow you to change the Hue, Saturation and Lightness of particular colors in your image. You can change the hue of your colors set the mood. Pushing the hue to colder colors, such as blue, purple, or green, creates a more gloomy mood. While pushing them to warmer colors, such as red, orange or yellow, creates a more cheerful mood.

Playing around with the saturation and lightness of colors can help you with pushing certain things to the background while highlighting others. I often do this while photographing flowers. Reducing the saturation and lightness of the green leaves and creasing them for the red flower peddels, puts more attention on the main subject of the photo.

### Vignette
A vignette darkens the corners of the photo, pulling the users attention to the center. Most of my photo’s have a vignette applied to them, but with some it’s applied with more subtlety than with others. There is no clear logic here. I guess, that I apply a heavier vignette on photos with a strong subject.

## Export and Store
I prefer storing my photos in Apple Photos so they are easily accessible from any of my devices. Dumping all of my RAW files on there quickly fils up my iCloud storage however. I therefore only store the RAW files of my keepers in Photos. The photos on the keepsake pile get exported in the HEIC format, since this format has better a better compression algorithm and stores more color information than the JPEG format.

The rejected photos are deleted from my system, but are still recoverable from the two SD-cards in my Nikon Z5. The RAW files of the keepers and keepsakes are stored locally and eventually archived to an external drive.

## Closing words
So there you have it, all of my secrets are now laid bare. I hope this post has helped you with coming up with a workflow of your own.
