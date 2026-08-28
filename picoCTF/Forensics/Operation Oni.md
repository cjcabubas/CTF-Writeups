# Operation Oni

In this challenge, we are given another compressed disk image.

Like before, I first extracted it using:

```
pv disk.img.gz | gunzip > disk.img
```

I like using `pv` here since it gives me a progress bar instead of just staring at the terminal wondering if anything is happening.

Once the image was extracted, I loaded it into **Autopsy** and started checking the different volumes.

Eventually, I got to **Volume 4** and looked inside the `/root` directory. From there, I found a `.ssh` folder containing several SSH-related files, including a private key.

One useful thing with Autopsy is that deleted files can still show up under the directory they originally belonged to, so finding the deleted SSH files here was pretty straightforward.

I extracted the private key from the image and saved it locally.

Before using it, I changed the permissions:

```
chmod 600 id_rsa
```

SSH does not like private keys having loose permissions, so this makes sure the key is only readable by me.

After that, I used the recovered key to connect to the challenge server:

```
ssh -i id_rsa -p <port> <username>@<ip>
```

The key worked and I was able to log in.

From there, I looked through the files on the machine until I found the flag.

So this challenge mostly came down to going through the disk image, finding the deleted SSH private key, extracting it, and then using it to access the server.
