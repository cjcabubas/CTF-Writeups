# Operation Orchid

In this challenge, we are given a compressed disk image:

```
disk.flag.img.gz
```

I first extracted it using:

```
pv disk.flag.img.gz | gunzip > disk.flag.img
```

I like using `pv` here since disk images can take a while to extract, and having a progress bar is better than just staring at the terminal wondering if it froze.

After extracting the image, I loaded it into **Autopsy** and started checking the different partitions.

The first volume was just unallocated space. I also checked some of the hex data there, but nothing really stood out.

The next volume contained a bunch of `.c32` files, which looked like normal SYSLINUX bootloader files. I still looked through them just in case, but there was nothing useful there either.

After another unallocated section, I eventually reached the volume containing the actual Linux filesystem.

While going through it, I made my way into:

```
/root/
```

Inside, I found a few interesting files:

```
flag.txt
flag.txt.enc
.bash_history
```

I first looked at `flag.txt`, which contained some references to Operation Orchid and coordinates somewhere in Kenya.

I thought that was probably part of the challenge, so I spent some time looking into it, but it ended up leading nowhere.

So I went back and checked the other files.

One file I almost ignored was:

```
.bash_history
```

Opening it showed the previous commands that had been run on the machine.

And there it was: the command that was used to encrypt the flag, along with the password/passphrase.

Now that I knew how the file had originally been encrypted, I could use the same settings to decrypt:

```
flag.txt.enc
```

I did mess this part up at first and got:

```
bad decrypt
```

which basically meant I was using the wrong OpenSSL settings.

After going back to `.bash_history` and matching the command properly, the decryption worked.

Then I just read the recovered file:

```
cat flag.txt
```

And that gave me the flag.

Most of this challenge was really just going through the disk image carefully and not overlooking files like `.bash_history`, since that ended up containing exactly what was needed to decrypt the flag.
