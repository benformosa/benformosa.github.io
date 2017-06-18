---
layout: default
title: Windows Spotlight for Desktop Wallpapers
categories:
  - blog
tags:
  - software
  - windows
  - powershell
  - wallpaper
---

![Collage of Windows Spotlight images](/assets/copy-spotlightimages-banner.png)
{: style="text-align: center;"}

I like Windows 10. Something I like about it is that the nice people at Microsoft sometimes change the picture on your lock screen, with a feature called [Windows Spotlight](https://docs.microsoft.com/en-us/windows/configuration/windows-spotlight). These pictures are supposed to be customised to your preferences based on which you give a ❤ t️o️. For me, it's usually a scenic landscape of some far-away place much more beautiful than the town I live in.

## Problem statement
I'd like to use the Windows Spotlight pictures as my desktop wallpaper.

I like having an attractive wallpaper, and I like to have it change occasionally. Often this means searching for a website that aggregates wallpapers, avoiding the ones that seem dodgy and manually downloading some that I like the look of. This isn't great fun, and I still don't get wallpapers I love. Then you have to copy them over to all your computers, or do it all again when you reinstall Windows.

There's quite a few articles on the web about how to find where Windows Spotlight stashes the image files that it downloads, such as this one from [Windows Central](https://www.windowscentral.com/how-save-all-windows-spotlight-lockscreen-images), but this isn't a complete solution to the problem. I don't want to remember to go do this each week, copy and rename all those files and sift out the thumbnails and app logos.
So I wrote a script to do it for me.

## Requirements
* Run silently and non-interactively
* Filter out only the images that will make nice wallpapers, i.e. full size, landscape images
* No dependencies - only use what Windows 10 provides out of the box

## Solution
What I ended up with is [Copy-SpotlightImages.ps1](https://github.com/benformosa/Toolbox/blob/master/Windows/Copy-SpotlightImages.ps1). This is a PowerShell script which uses native PowerShell as well as .Net's [System.Drawing.Image](https://msdn.microsoft.com/en-us/library/system.drawing.image(v=vs.110).aspx) class.
The script checks each file in the Spotlight images directory and copies it to a destination directory, if it meets the following criteria:
* It is an image file. Simply attempting to create a System.Drawing.Image object will confirm this.
* Its dimensions are suitable for a wallpaper. System.Drawing.Image allows the image properties to be queried. Most of the non-wallpaper images in the directory are small thumbnails or icons.
* It hasn't already been copied. The first thing the application does is compute all the file hashes of the images that already exist in the destination directory. File hashes of files which might be copied are compared against that list of hashes. As an additional step, the destination directory is checked to confirm that a file with the same filename doesn't exist there.

Spotlight provides copies of images in both landscape and portrait aspects for use on tablet computers. The script identifies the aspect and can skip copying one aspect or the other. Identifying the aspect is simple, the height and width dimensions of the image are compared.

One of the challenges I had during development of the script was seemingly inconsistent behaviour when creating System.Drawing.Image objects from files. Initially, using the [FromFile](https://msdn.microsoft.com/en-us/library/stf701f5(v=vs.110).aspx) method worked fine. However, I soon ran into out of memory errors. [This StackOverflow answer](https://stackoverflow.com/a/2216338) pointed me towards using [FromStream](https://msdn.microsoft.com/en-us/library/93z9ee4x(v=vs.110).aspx) instead. I suspect the error only occurred when I was running the script against the Spotlight images directory, containing dozens of files, rather than a source directory with only one or two sample images.

Running the script is simple. Here I'm using the defaults for Source and Destination, and only collecting landscape images.
```powershell
Copy-SpotlightImages.ps1 -NoPortrait -NoSubFolders
```

## Outcome
I have Copy-SpotlightImages.ps1 configured with [Task Scheduler](https://blogs.technet.microsoft.com/heyscriptingguy/2012/08/11/weekend-scripter-use-the-windows-task-scheduler-to-run-a-windows-powershell-script/) to run daily, and every day when I log in, I can see a relaxing view from my lock screen and my desktop.

An unexpected additional functionality of this script is that it can be used to find interesting images in any directory. You could run it against your Pictures library, or even your web browser's cache.
```powershell
Copy-SpotlightImages.ps1 `
  -Source "$env:HOMEPATH\AppData\Local\Mozilla\Firefox\Profiles\*.default\OfflineCache\" `
  -Destination "$env:HOMEPATH\Pictures\Firefox-Cache" `
  -NoPortrait -NoSubFolders -Verbose
```

## Banner Image
I used [ImageMagick](https://www.imagemagick.org/) to create the image at the top of this post. This code creates a collage of images the size of one of the original images ([full size here](/assets/copy-spotlightimages-collage.jpg)), and a cropped version with a transparent gradient.

```bash
# Randomly order input files
FILES=$(find Pictures/Spotlight/Landscape/ -type f | sort -R)
# How many images do we have?
NUM=$(find Pictures/Spotlight/Landscape -type f | wc -l)
# Get the width and height of an image. 
# We happen to know that they are all the same.
WIDTH=$(identify -format "%w" \
  $(find Pictures/Spotlight/Landscape -type f | head -n 1))
HEIGHT=$(identify -format "%h" \
  $(find Pictures/Spotlight/Landscape -type f | head -n 1))
# How many images wide and high
TILE=$(echo "sqrt($NUM)" | bc)
# What size should the images in the collage be
TILEW=$(echo "${WIDTH}/${TILE}" | bc)
# Create the collage
montage -resize $TILEW -mode Concatenate \
  -tile "${TILE}x${TILE}" $FILES copy-spotlightimages-collage.jpg

# The banner should be a quarter of the original's height
BANNERH=$(echo "${HEIGHT}/4" | bc)
# We'll offset the banner by half of one image's height
TILEH_HALF=$(echo "${HEIGHT}/${TILE}/2" | bc)
# Create the banner. The content div in my blog theme is 620px wide
convert \( copy-spotlightimages-collage.jpg \
  -crop "${WIDTH}x${BANNERH}+0+${TILEH_HALF}"  +repage \) \
  \( +clone -sparse-color Barycentric '0,0 white 0,%[fx:h-1] black' \
  -level 0x30% -write /tmp/gradient.png \) \
  -alpha off -compose copy_opacity -composite \
  -resize 620 copy-spotlightimages-banner.png
```