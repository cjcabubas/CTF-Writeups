# Sleuthkit Apprentice

In this challenge, we are once again given a compressed disk image:

```
disk.flag.img.gz
```

Like before, I extracted it using:

```
pv disk.flag.img.gz | gunzip > disk.flag.img
```

Using `pv` is not really needed, but I like having a progress bar when extracting bigger disk images instead of just staring at the terminal wondering if anything is happening.

After extracting it, I loaded:

```
disk.flag.img
```

into **Autopsy**.

From there, I started going through the different volumes and checking the files like I normally would with a disk image.

Eventually, I reached **Volume 4**, which contained the actual Linux filesystem.

I started looking through the directories and eventually made my way into:

```
/root/
```

Inside was a folder containing the flag file.

Opening that file gives us the flag.

The challenge is actually called **Sleuthkit Apprentice**, so it was probably intended to be solved using Sleuth Kit commands like `mmls`, `fls`, and `icat`.

I ended up using Autopsy instead since I am more comfortable navigating disk images through it. Autopsy makes it much easier for me to go through the partitions and directories without having to manually keep track of offsets and file IDs.