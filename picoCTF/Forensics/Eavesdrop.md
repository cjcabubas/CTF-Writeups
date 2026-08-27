In this challenge, we are presented with a `.pcap` file containing a conversation between two users.

As usual, I started by doing some basic checks on the file. Running `strings` gave us a readable conversation:

```
strings capture.flag.pcap
```

While reading through it, one thing that immediately stood out was this command:

```
openssl des3 -d -salt -in enc.enc -out file.txt -k supersecretpassword123
```

So now we already know quite a lot. There is an encrypted file being transferred, it was encrypted using 3DES, and we even have the password needed to decrypt it.

The users also mention that the file was going to be transferred again through port `9002`.

I opened the capture in Wireshark, filtered for port `9002`, and followed its TCP stream. This revealed the encrypted file data being transferred.

The important part here is that we need the actual raw bytes of the encrypted file, not the ASCII representation of them. I switched the TCP stream display to **Raw** so I could get the hexadecimal data.

I then opened wxHexEditor, created a new file, and inserted `48` bytes since the transferred encrypted file was 48 bytes long. From there, I copied the raw hex data from Wireshark into those bytes and saved the file as:

```
enc.enc
```

Once the encrypted file had been reconstructed properly, we could simply use the exact OpenSSL command that was leaked in the conversation:

```
openssl des3 -d -salt -in enc.enc -out file.txt -k supersecretpassword123
```

The decryption worked and produced:

```
file.txt
```

Then we just read it:

```
cat file.txt
```

And boom:

```
picoCTF{nc_73115_411_dd54ab67}
```

The main thing with this challenge was realizing that the conversation basically leaked everything we needed: the encryption method, the password, and even the port where the encrypted file was being transferred. After that, it was just a matter of reconstructing the raw file correctly and decrypting it.