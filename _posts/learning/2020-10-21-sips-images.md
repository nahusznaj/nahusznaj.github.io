---
layout: article
title: Converting images
categories: learning
modified: 2020-10-21T16:28:11-04:00
tags: [bash]
comments: false
share: true
---

I needed to convert many images to another format, and also change their size.

Here's a page that I found really [cool sips tips page](https://robservatory.com/use-sips-to-quickly-easily-and-freely-convert-image-files/). And I used that to convert my HEIC images to jpg images.

Say that I have the `IMG_2911.jpg` image and I want to have this as `.png`. From a terminal in that folder, do:

```bash
$ sips -s format png IMG_2911.jpg --out image.png
```

For the other way around:

```bash
$ sips -s format jpeg image.png --out IMG_2911_2.jpg
```

If I had a list of images in the folder, and want to do this programatically for each one, cd into that folder from the terminal and run:

```bash
$ for i in *.HEIC; do sips -s format jpeg "${i}" --out "${i%png}.jpg"; done
```

Now, if I wanted to change the dimensions of each image to a smaller file size:

```bash
$ for i in *.HEIC; do sips -Z 600 -s format jpeg "${i}" --out "${i%png}.jpg"; done
```