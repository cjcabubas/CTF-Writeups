# Sleuthkit Intro

In this challenge, we are given a disk image along with an `nc` server.

The challenge already gives us a pretty clear hint on what to do, which is to use `mmls` on the disk image and find the length of a specific partition.

So I started with:

```
mmls disk.img
```

This shows the partition layout of the disk image, including things like the start sector and the length of each partition.

From there, I just looked for the partition the challenge was asking about and copied its **length** value.

After getting that, I connected to the provided server using:

```
nc <host> <port>
```

The server then asks for the partition length, so I just pasted the value I got from `mmls`.

And from that, the server gives us the flag.