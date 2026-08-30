# MacroHead WeakEdge

In this challenge, we are presented with a file called:

```
forensics_is_fun.pptm
```

Even though this is technically just a PowerPoint presentation, `.pptm` files can contain macros, so I did not immediately open it. With files like this, I would rather inspect them first instead of finding out the hard way why that `m` is there.

I started with some simple recon:

```
file forensics_is_fun.pptm
```

and:

```
exiftool forensics_is_fun.pptm
```

Nothing really stood out yet, so I moved on to `strings`:

```
strings forensics_is_fun.pptm
```

This immediately filled the terminal with different paths from inside the PowerPoint file:

```
ppt/slides/_rels/slide42.xml.relsPK
ppt/slides/_rels/slide43.xml.relsPK
ppt/slides/_rels/slide44.xml.relsPK
ppt/slides/_rels/slide45.xml.relsPK
ppt/slideMasters/slideMaster1.xmlPK
ppt/slideLayouts/slideLayout1.xmlPK
ppt/theme/theme1.xmlPK
docProps/thumbnail.jpegPK
ppt/vbaProject.binPK
ppt/presProps.xmlPK
ppt/viewProps.xmlPK
ppt/tableStyles.xmlPK
docProps/core.xmlPK
docProps/app.xmlPK
ppt/slideMasters/hiddenPK
```

Most of these looked like normal PowerPoint files and directories.

One entry, however, stood out immediately:

```
ppt/slideMasters/hidden
```

Compared to everything else, a file simply called `hidden` sitting inside `slideMasters` looked way too suspicious to ignore.

So I used `binwalk` to extract the contents of the PowerPoint file and started going through the extracted directories until I reached:

```
ppt/slideMasters/hidden
```

Once there, I used:

```
cat hidden
```

The contents looked like Base64, except every character was separated by spaces:

```
Z w a ...
```

Since Base64 normally should not have spaces between every character, I first removed them using `tr`, then passed the result straight into `base64`:

```
cat hidden | tr -d ' ' | base64 -d
```

And that gives us the flag.

The main thing I got from this challenge was that Office files are worth inspecting before opening. Running something as simple as `strings` already showed the internal file structure, and from there the oddly named `hidden` file basically pointed us in the right direction.
