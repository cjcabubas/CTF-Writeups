In this challenge, we are given two files: a ZIP file and a PCAP trace file. Trying to extract the ZIP immediately asks for a password, so it is pretty clear that the password is probably hidden somewhere inside the packet capture.

I opened the PCAP and started looking through the traffic. One of the first things that stood out was traffic related to Chromecast.

![Chromecast traffic](/picoCTF/Forensics/attachments/Pasted%20image%2020260825232718.png)

I searched up what the Chromecast traffic was and found that it was related to smart TVs and streaming devices. That gave me some context, but it still did not really tell me where the password was, so I kept looking through the packets.

After taking my time going through them, packet 48 finally caught my attention.

![Packet 48](/picoCTF/Forensics/attachments/Pasted%20image%2020260825232932.png)

Packet 48 contained this string:

```
AABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=
```

Most of it looked like Base64, but the beginning:

```
AABBHHPJGTFRLK
```

looked malformed compared to the rest.

So I removed that part and decoded the remaining string as Base64. That gave me half of the flag.

Since I still had the removed part, I tried using:

```
AABBHHPJGTFRLK
```

as the password for the ZIP file.

It worked, and extracting the ZIP gave me the other half needed to complete the flag.

So the PCAP basically contained both clues at once: the valid Base64 gave one part of the flag, while the extra malformed-looking part turned out to be the ZIP password.
