In this challenge, we are given a file named `Flag.pdf`, but trying to open it as a normal PDF does not work.

The first thing I did was check what the file actually was:

```id="a1c2d3"
file Flag.pdf
```

This showed that it was actually a shell archive and not a PDF.

So I copied it into a shell script and ran it:

```id="b2d3e4"
cp Flag.pdf Flag.sh
chmod +x Flag.sh
./Flag.sh
```

Running it extracted another file called `flag`.

I checked that file again using:

```id="c3e4f5"
file flag
```

This time it showed that the file was an `ar` archive.

From here, the challenge basically became a chain of different compressed file formats. I just kept checking the file type, extracting it, and then doing the same thing again with the next file.

The formats I went through were:

```id="d4f5g6"
Shell archive
AR archive
GZIP
LZIP
LZ4
LZMA
LZOP
LZIP
XZ
ASCII text
```

For some of the layers, `binwalk` was enough:

```id="e5g6h7"
binwalk -e flag
```

For others, I had to use their own decompression tools:

```id="f6h7i8"
lzip -d -k file
lz4 -d file output
lzma -d -k file.lzma
lzop -d -k file.lzop -o output
xz -d -k file.xz
```

Some of the tools also needed the file to have the correct extension first, so whenever that happened I just renamed the file and tried again.

After going through all of the different layers, the final file contained a long hex string.

At that point, I converted the hex back into normal text and got the final result.

This challenge was mostly just about not trusting the file extension. Even though the original file was named `Flag.pdf`, it was not actually a PDF at all, so using `file` over and over was basically what carried the whole challenge.