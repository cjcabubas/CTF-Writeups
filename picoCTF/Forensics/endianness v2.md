# endiannessv2

In this challenge, we are given a file called `challengefile`, and from inspecting it we can tell that it contains JFIF data. The problem is that the bytes are all messed up somehow.

We are also told that the data came from a **32-bit system**, which felt like the main clue here.

Since 32 bits is 4 bytes:

```
32 bits = 4 bytes
```

I figured the data might have been reordered in groups of 4 bytes.

So I wrote a small Python script to reverse every 4-byte chunk:

```
with open("challengefile", "rb") as f:
    data = bytearray(f.read())

while len(data) % 4 != 0:
    data.append(0)

for i in range(0, len(data), 4):
    data[i], data[i+1], data[i+2], data[i+3] = (
        data[i+3],
        data[i+2],
        data[i+1],
        data[i]
    )

with open("fixed_image.jpg", "wb") as f:
    f.write(data)
```

Basically, every group like:

```
AA BB CC DD
```

gets turned into:

```
DD CC BB AA
```

After running the script, the output becomes a proper JPEG/JFIF image again.

I also tried doing the same thing in CyberChef.

First, I converted the whole file into hex and copied it:

```
xxd -p challengefile | tr -d '\n' | xclip -selection clipboard
```

Then in CyberChef I used:

```
From Hex
↓
Swap Endianness
```

Since the clue says 32-bit, I set the word length to:

```
4 bytes
```

After swapping the endianness, I copied the resulting hex and turned it back into a file:

```
xclip -selection clipboard -o | xxd -r -p > output.bin
```

Then I checked it with:

```
file output.bin
```

and it was identified as a JPEG/JFIF image.

From there, I just renamed it:

```
mv output.bin recovered.jpg
```

The main clue was really the **32-bit system** part. Once I connected that to 4-byte chunks, reversing the byte order made the file readable again.
