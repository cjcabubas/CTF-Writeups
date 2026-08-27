In this challenge, we are presented with a file that does not have an obvious file type.

I started with some basic enumeration using:

```
file advanced-potion-making
```

This only came back as a data file, so I decided to look at the actual hex instead.

While looking through the bytes, something immediately stood out:

```
49 48 44 52
```

which translates to:

```
IHDR
```

`IHDR` is one of the main chunks found inside PNG files, so this was a pretty good sign that the file was actually supposed to be a PNG but had been corrupted somehow.

A normal PNG should start with these magic bytes:

```
89 50 4E 47 0D 0A 1A 0A
```

and shortly after that, the first `IHDR` chunk should normally begin with:

```
00 00 00 0D 49 48 44 52
```

Breaking that down:

```
00 00 00 0D    = length of the IHDR chunk
49 48 44 52    = "IHDR"
```

The beginning of our file did not match what a normal PNG should have, so I opened it in a hex editor and started replacing the corrupted bytes with the proper PNG values.

After fixing the PNG magic bytes and saving the file, it still would not open.

So clearly there was still something wrong.

I went back into the hex and compared the beginning of the file again with a normal PNG. This time I noticed that some of the bytes around the `IHDR` chunk were also incorrect.

After fixing those bytes as well and saving the file again, the PNG finally opened.

At this point the image itself still did not immediately show the flag, so I figured there was probably something hidden in the colors or different image channels.

I downloaded StegSolve and opened the repaired image with it.

From there, I started going through the different filters.

After cycling through a few of them, one of the filters finally made the hidden text visible.

And boom, there was the flag.

The main thing I got from this challenge was getting a little more familiar with PNG structure. Seeing:

```
49 48 44 52
```

inside something that is supposedly just a data file is a pretty big hint that it might actually be a broken PNG.