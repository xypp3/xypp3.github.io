---
title: 'printing with linux'
pubDate: 2025-08-28 16:58
description: 'TLDR; tools and tricks for setting up pages to print'
author: 'xypp3'
tags: ['linux', 'tips']
---

After facing open book exams for the past year and I was faced with the lack of printing options (that I could find) in Ubuntu 22LTS. These tools helped me format slides, reduce page counts and apply greyscale filters to avoid being like some whose turn forests to slide decks.


## Cut down slides
1. Use firefox `Save as PDF`
2. Select custom page ranges (this is the biggest paper saver)
3. (note) firefox can also squish many digital pages into one physical page in the print options

## Combine pdfs
Usually you have multiple slide pdfs that you want to combine. The following will make a mega pdf.

```bash
$ pdfunite 1.pdf 2.pdf 3.pdf out.pdf
```

## Check real paper size
I've had experience that when scaling slides to fit more per page, sometimes your scales get out of whack. This command shows you the real paper size of your documents.
```bash
$ pdfinfo out.pdf
```

## Resize to A4
If your documents have become gnome or oogre sized, the following command should transmute it to a average human size.
```bash
$ pdfjam --outfile out.pdf --paper a4paper --landscape in.pdf
```
- this utility is downloaed from `texlive-extra-utils`

## Greyscale
In many ways color is what bring joy to our lives. Not with printing. To turn your documents greyscale try the following command.

```bash
$ gs \
     -sOutputFile=output.pdf \
     -sDEVICE=pdfwrite \
     -sColorConversionStrategy=Gray \
     -dProcessColorModel=/DeviceGray \
     -dCompatibilityLevel=1.4 \
     -dNOPAUSE \
     -dBATCH \
     -dAutoRotatePages=/None \
     input.pdf
```

## P.S.
Thanks for reading all this way. And also ignore the absolute chaotic mix of American and British spelling.
