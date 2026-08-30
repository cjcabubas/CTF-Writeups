# m00nwalk v2

In this challenge, after already completing the first m00nwalk, I already had a pretty good idea that this one was going to involve SSTV again.

We are given another message.wav file, and the audio sounded very similar to the first challenge, so I opened it in QSSTV.

Since I already had problems with auto detection before, I knew that manually selecting the receive mode usually gives a cleaner result. This time though, the challenge also gives us several clue files, and each one is another SSTV transmission.

For each clue, I first used Auto just to see what mode QSSTV detected, then manually selected that mode and decoded it again.

The modes were:

```
Clue 1 - Martin 1
Clue 2 - Scottie 2
Clue 3 - Martin 2
```

After decoding all three clue images, they started pointing toward Alan Eliasen's Future Boy steganography tools.

At this point, I figured there was probably something else hidden inside the WAV file aside from the SSTV transmission itself.

One of the clues also gave us the password:

```
hidden_stegosaurus
```

So I tried extracting hidden data from the WAV file using steghide:

```
steghide extract -sf message.wav -p hidden_stegosaurus
```

This successfully extracted a hidden text file, and inside it was the flag.

Since I had already solved the first m00nwalk challenge, recognizing the SSTV part was much easier this time. The main part was decoding the different clues, figuring out what they were pointing toward, and then using the password with steghide.
