---
layout: post
title: "How to solve the error: no decode delegate for this image format"
category:
tags:
- Linux
- ImageMagick
---
{% include JB/setup %}

Today I am trying to use CarrierWave to convert image's format, from png to jpg, then I MiniMagick::Invalid error.
When I use command line tool to detect the format, it shows "identify: no decode delegate for this image format `xxx.png' @ error/constitute.c/ReadImage/544." After I googled a litte while, I found "convert -list configure" command could show all image processing delegate, like "DELEGATES     bzlib jpeg jp2 lcms tiff xml zlib", then it miss PNG, so after I use "brew tap homebrew/versions/libpng12", it works then.
