# MilkSlap

In this challenge, we are given a link that leads to a website where moving the mouse causes the image on the page to keep updating.

As soon as I saw this, I figured the image itself was probably where the interesting part was, so I opened DevTools, went into the Sources tab, and downloaded the image being used by the page.

The file was called:

```
concat_v.png
```

The name already gave a pretty good clue. `concat` most likely stands for concatenate, meaning multiple things were combined together, while the `v` probably means vertical.

So from there, I started doing my usual checks on the image. Most of them did not really give me anything useful, but one result immediately stood out when I ran `zsteg`.

Instead of giving me normal results, it threw:

```
stack level too deep
```

Since `zsteg` is written in Ruby, this basically meant Ruby was hitting its stack limit while trying to process the image. The image itself was also extremely tall, which matched the whole `concat_v` idea pretty well.

At this point, I figured I could just split the image into smaller pieces and run `zsteg` on those instead.

I opened the image in GIMP first and looked at the borders between each section. From there, I figured out how the image was divided and ended up splitting it into 66 vertical sections.

I used this simple Python script:

```
from PIL import Image

img = Image.open("concat_v.png")

width, height = img.size

crops = 66
slicedheight = height // crops

for i in range(crops):
    upper = i * slicedheight
    lower = (i + 1) * slicedheight

    box = (0, upper, width, lower)

    cropped_img = img.crop(box)
    cropped_img.save(f"crop_vertical_{i}.png")
```

This basically takes the huge image and cuts it into 66 smaller images.

After that, I just started running `zsteg` on the cropped files until one of them returned the flag.

There was also another way to do it without splitting the image. Since the problem was Ruby's stack size, we could increase it before running `zsteg`:

```
RUBY_THREAD_VM_STACK_SIZE=5000000 zsteg concat_v.png
```

That also lets `zsteg` process the full image and gives the same result.

So the main clue here was really the filename `concat_v.png` together with the `stack level too deep` error. Once I realized the image was just a bunch of sections concatenated vertically, splitting it into smaller pieces made the solve pretty simple.
