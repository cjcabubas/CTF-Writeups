# MSB

In this challenge, we are given an image that already looks pretty corrupted.

![Corrupted image](/picoCTF/Forensics/attachments/Pasted%20image%2020260826001200.png)

Just by looking at it, we can see that the colors look heavily changed and almost inverted in some areas.

From this, I already had a feeling that something had been changed directly in the RGB values of the pixels.

Since the visual change is very noticeable, I figured this probably was not using the Least Significant Bit or LSB. Changing the LSB usually does not affect how the image looks that much.

Instead, this looked more like something involving the **Most Significant Bit**, or MSB.

The MSB has a much bigger effect on the actual pixel value, so changing it can make the image look heavily distorted like this.

At this point, I already had a pretty good idea of where the hidden data was, so I just needed a way to extract those bits.

For this, I used StegSolve.

I downloaded the StegSolve JAR file and ran it using:

```
java -jar stegsolve.jar
```

After opening the image, I went into **Analyse → Data Extract**.

From there, I selected bit `7` for the RGB channels, since bit 7 is the most significant bit.

I left the alpha channel unchecked since there was nothing we needed from it.

After extracting the selected bits, the hidden data became visible and we get the flag.

So this one was mostly about recognizing from the way the image looked that the higher bits of the RGB values had probably been changed, then using StegSolve to pull out the MSB data directly.
