# m00nwalk

In this challenge, we are given a file called `message.wav` that contains some pretty unusual sounds.

As usual, I started by checking if the file was actually what it claimed to be:

```
file message.wav
```

The output showed:

```
message.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 48000 Hz
```

At first, seeing `RIFF` confused me a little, but after looking it up I found that RIFF is basically just a container format. The rest of the output confirms that the file is indeed a normal WAVE audio file.

I then checked the metadata:

```
exiftool message.wav
```

Nothing really stood out there, so I moved on to the challenge hints.

The first hint was:

> **How did pictures from the moon landing get sent back to Earth?**

I searched this up and found out about **Slow-Scan Television**, or SSTV, which is used to transmit images through radio signals.

That made me think the WAV file was probably not just random audio, but an SSTV signal that could be decoded into an image.

So I searched for ways to decode SSTV from a WAV file and found **QSSTV**.

After installing it, I configured it to receive the audio from the file instead of using a live radio input.

I tried decoding the recording, but the image kept losing synchronization and would not fully recover.

That is where the second hint came in:

> **What is the CMU mascot? That might help select a RX option.**

I searched it up and found that Carnegie Mellon University's mascot is the **Scottish Terrier**.

Going back to QSSTV, I noticed that it had detected something called:

```
Scottie 1
```

before eventually showing `No Sync`.

Since `Scottie 1` is also an SSTV receive mode, I manually selected it instead of relying on auto-detection.

After doing that, the synchronization improved a lot.

I made a few small adjustments to the receive settings, and QSSTV was finally able to decode the full transmission into an image containing the flag.

This challenge mostly came down to actually paying attention to the hints. The first hint pointed toward SSTV, while the second one pointed directly toward the correct `Scottie 1` receive mode.
