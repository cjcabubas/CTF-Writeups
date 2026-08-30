# Trivial File Transfer Protocol

In this challenge, we are given a `.pcapng` file containing a bunch of packet captures, and we are simply told to find the flag somewhere inside it.

I started with my usual basic recon first:

```
file tftp.pcapng
exiftool tftp.pcapng
strings tftp.pcapng
```

While running `strings`, I could already see references to files like `instructions.txt`, but at the time it did not really catch my attention. There was a lot of other data mixed in, so I just kept going.

I then opened the capture in Wireshark and started looking at the different packets and protocols being used.

After doing some basic filtering, I figured out that the files were being transferred through **TFTP**, or Trivial File Transfer Protocol. TFTP is a simple file transfer protocol that works over UDP.

So I filtered for:

```
tftp
```

Now the file references I saw earlier in `strings` started making more sense.

Looking through the TFTP traffic showed several transferred files:

```
instructions.txt
plan
picture1.bmp
picture2.bmp
picture3.bmp
program.deb
```

These were the main files transferred in the capture.

I started with `instructions.txt` and `plan`.

Both contained uppercase text that looked pretty random at first. Since it looked like some kind of simple rotation cipher, I tried ROT13.

That gave readable messages.

The first one basically says that TFTP does not encrypt its traffic and that they need to disguise the flag transfer.

The second message says that a program was used to hide something inside the photos, and it also contains the phrase:

```
WITH-DUEDILIGENCE
```

The decoded messages point us toward the images and the program that was used to hide the data.

At this point, the three BMP files became the obvious next place to look.

The transferred program turned out to be related to `steghide`, so I started trying to extract hidden data from the images.

Running:

```
steghide extract -sf picture1.bmp
```

asked for a password.

At first, I was not sure what to use, but then I remembered the phrase from the decoded `plan` file:

```
WITH-DUEDILIGENCE
```

So I tried:

```
DUEDILIGENCE
```

as the password on the different images.

Eventually, using it on:

```
picture3.bmp
```

successfully extracted the hidden file containing the flag. The same password clue and third image are what lead to the extraction in the capture.

What made this challenge click was realizing that the `instructions.txt` reference I had already seen earlier through `strings` actually mattered once I understood that the capture contained TFTP file transfers.

From there, everything connected together pretty quickly: TFTP led to the transferred files, the text files led to ROT13, the decoded message led to the images, and `DUEDILIGENCE` gave the password needed to extract the hidden data from `picture3.bmp`.