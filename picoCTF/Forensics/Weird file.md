# Weird file

In this challenge, surprisingly, there were only around 2000 solves, which was pretty low compared to some of the other challenges.

We are given a `.docm` file along with a link talking about malicious code inside macro-enabled Office files on macOS.

I did not really know much about `.docm` files at first, so I searched up what they were and found out that they are macro-enabled Microsoft Word documents. Basically, they can contain VBA macros that are able to run code when the document is opened.

With that information, I started doing my usual basic recon:

```
file suspicious.docm
exiftool suspicious.docm
```

Nothing really stood out at first aside from it being a Microsoft Office 2007 document.

Normally, that probably would not have meant much to me, but I had already solved another challenge involving an Office file before, so I already had an idea that there could be a bunch of files stored inside it.

Before extracting anything, I wanted to confirm that first, so I ran:

```
strings suspicious.docm
```

This filled the terminal with a bunch of `.xml` files and directory paths from inside the document.

Seeing all of those internal paths confirmed what I was thinking. The document was basically acting like a container, so instead of opening it normally, I decided to just extract everything inside it.

I used:

```
binwalk -e suspicious.docm
```

After that, I moved into the extracted directory and listed everything recursively:

```
ls -laR
```

While going through the output, I noticed files related to VBA, including names such as:

```
word/vbaProject.bin
word/vbaData.xml
```

Since I had already researched that `.docm` files can contain VBA macros, these immediately looked like the files I should be checking.

At this point, I thought the VBA part might end up being something complicated where I would have to actually understand or reverse the macro code.

That ended up being more of a red herring.

I did not need to execute the macro or fully understand what the VBA was doing. I just kept going through the VBA-related files and checking their contents until something stood out.

Eventually, inside:

```
word/vbaProject.bin
```

I found a Base64-looking string.

That was much more familiar, so instead of going deeper into the VBA itself, I copied the Base64 and decoded it:

```
echo "BASE64_STRING" | base64 -d
```

And that gave me the flag.

So even though the challenge was centered around a macro-enabled Word document and initially made the VBA side look like the main problem, my solve was mostly just recognizing that the Office file could be extracted, going through its internal files, finding the Base64 inside `vbaProject.bin`, and decoding it.