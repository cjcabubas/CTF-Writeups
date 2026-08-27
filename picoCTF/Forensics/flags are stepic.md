In this challenge, we are presented with a website containing a bunch of different flags representing countries, lands, or groups. We are told that one of these flags is not real.

After looking through them, one name immediately stood out to me: `Upanzi`.

Upanzi isn't an actual country, so I figured that was probably the flag I should start looking at.

To check further, I opened the browser's Network tab and looked at the downloaded flag images. I sorted them by size and noticed that the `UPZ` image was much larger than the rest, which made it even more suspicious.

So I downloaded the image and started doing my usual checks:

```id="k9f2xa"
file upz.png
exiftool upz.png
strings upz.png
zsteg upz.png
```

None of these really gave me anything useful.

Since the basic checks didn't work, I tried `binwalk` next:

```id="j3vb8q"
binwalk -e upz.png
```

Binwalk detected a few embedded things inside the image, including what looked like zlib-compressed data.

After extracting it, I tried decompressing the zlib file:

```id="n8rm4c"
pigz -z -d < file.zlib > output.bin
```

That didn't work.

I tried a few other ways of decompressing it as well, but nothing was really getting anywhere.

At this point I started looking at the raw bytes of the extracted file. The beginning looked like a valid zlib header:

```id="fh6m2k"
78 9C
```

so for a while I thought maybe the stream was corrupted or there was something else I was missing.

After spending some time on that with basically no progress, I decided to backtrack.

I looked at the challenge again and realized I had kind of ignored one of the biggest clues sitting right in front of me: the challenge name itself.

```id="wa7k1e"
Stepic Flags
```

I searched up what Stepic was and found that it is a Python steganography library that can hide data inside images.

There is also a command-line tool for decoding images made with it.

So I tried:

```id="tg2x9p"
stepic -d -i upz.png
```

And that immediately gave me the hidden flag.

So all that time I spent fighting the zlib file was basically unnecessary.

The challenge name was pointing directly toward Stepic the whole time, and once I actually followed that clue, the solve was pretty straightforward.