# hideme

In this challenge, we are given a PNG image along with the context that the image is being passed between two people. From that alone, I already had a feeling that something was probably being hidden inside the image.

I started with a quick check using `file` just to confirm that it was actually a PNG:

```
file image.png
```

![PNG file check](/picoCTF/Forensics/attachments/Pasted%20image%2020260825234124.png)

The file was identified as a normal PNG image, so I moved on to checking the metadata using:

```
exiftool image.png
```

This time, something immediately stood out.

![ExifTool warning](/picoCTF/Forensics/attachments/Pasted%20image%2020260825234146.png)

ExifTool gave the warning:

```
Trailer data after PNG IEND chunk
```

The `IEND` chunk marks the end of a PNG image, so this basically tells us that there is still extra data sitting after the actual image has already ended.

To look at the end of the file more closely, I used:

```
xxd image.png | tail
```

![Trailer data](/picoCTF/Forensics/attachments/Pasted%20image%2020260825234358.png)

From the hex output, we can confirm that there is indeed something appended to the end of the PNG. Some of the readable data also showed what looked like a folder inside the file.

From there, I used `binwalk` to extract it:

```
binwalk -e image.png
```

After extraction, I went into the extracted directory and found the secret folder along with the file containing the flag.

So once `exiftool` showed that there was data after the `IEND` chunk, it was mostly just confirming it with `xxd` and then extracting it with `binwalk`.
