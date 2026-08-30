# Pitter, Patter, Platters

In this challenge, we are given a disk image called `suspicious.dd.sda1`.

The `sda1` part already made me think that this was probably the first partition of a Linux drive, since that naming is pretty common on Linux systems.

Before opening anything though, I still did my usual recon just to make sure I knew what I was dealing with:

```
file suspicious.dd.sda1
exiftool suspicious.dd.sda1
strings suspicious.dd.sda1
```

This basically confirmed that yes, we were dealing with a disk image, so from there I went straight to Autopsy, which is usually my go-to whenever I have to look through disk images.

Once the image was loaded, one of the first files that stood out was:

```
suspicious-file.txt
```

Opening it showed:

```
Nothing to see here! But you may want to look here -->
```

What immediately caught my attention was the empty space after the arrow.

At first, I did not really know what it was pointing to, so I started checking the file itself. I ran some basic recon on it and confirmed that it really was just a normal text file containing that message.

From there, I started looking through the different directories and subdirectories inside the partition.

I found a few files containing MD5-looking hashes, which looked suspicious at first, but after checking them and searching up what those files were for, they did not really lead anywhere.

![Red herring files](/picoCTF/Forensics/attachments/Pasted%20image%2020260830224054.png)

So I went back to the original clue again.

The message basically tells us to look at the blank space next to the file, which made me start thinking about the different places data can be hidden around files on a disk.

After a bit of searching, I found a few possibilities like unallocated space, partition gaps, and **file slack**.

I decided to start with file slack.

File slack is basically the unused space left over in the final disk block assigned to a file. Even if the actual file ends, the rest of that block can still contain leftover or hidden data.

Autopsy hides file slack by default, so I went into the settings and disabled the option that hides file slack.

After doing that, another entry appeared in the same directory with a slack-related name.

Opening it showed what looked like the flag, except it was completely reversed.

![File slack containing reversed flag](/picoCTF/Forensics/attachments/Pasted%20image%2020260830224449.png)

From there, all I had to do was reverse the text back into the correct order and we get the flag.

This one basically came down to taking the blank space in the hint literally. Once the normal files stopped leading anywhere, file slack ended up being exactly where the hidden data was sitting.
