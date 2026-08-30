# Disk, disk, sleuth!

In this challenge, we are presented with a disk image compressed using Gzip.

Instead of opening it directly, I first decompressed the file using:

```
pv filename.gz | gunzip > unzipped.img
```

After extracting the disk image, I opened up Autopsy and loaded the `.img` file for analysis.

Once the image was loaded, Autopsy showed two volumes. One of them was unallocated space, while the other contained the actual filesystem and files.

I started browsing through the filesystem and went straight into the root directories since flags in disk image challenges are often hidden somewhere inside user or system files.

After looking through the files near the bottom of the directory, boom, there it was.

The flag was sitting inside one of the files in the filesystem.

Pretty simple challenge overall. The main steps were just decompressing the disk image, loading it into Autopsy, identifying the correct volume, and browsing through the filesystem until the flag showed up.
