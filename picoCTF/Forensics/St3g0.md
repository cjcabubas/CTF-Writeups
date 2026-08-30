# St3g0

In this challenge, we are given a PNG image.

I started with my usual checks using `file`, `exiftool`, `strings`, and `binwalk`, but none of them really gave me anything useful.

Since the file is a PNG, I then tried `zsteg`:

```
zsteg image.png
```

And from that, we get the flag.

The reason `zsteg` works here is because the data is hidden using **LSB**, or Least Significant Bit steganography.

Basically, the RGB values of every pixel are stored as binary numbers. The last bit of those numbers can be changed to hide data without really changing how the image looks.

For example:

```
1101011
      ^
      LSB
```

If that last bit needs to be changed from `1` to `0`, it becomes:

```
1101010
```

The actual value only changes by `1`, so the difference in color is usually too small for us to notice.

The hidden message is basically converted into bits, and those bits are placed into the least significant bits of the pixels throughout the image.

`zsteg` checks these different bit positions and color channels for us, which is why it was able to find the hidden data without us having to manually extract every bit.