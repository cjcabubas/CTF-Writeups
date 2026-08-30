In this challenge, we are given a `.pcap` file containing packet captures related to a torrenting service.

Our goal is to figure out what file is being downloaded and submit its filename as the flag.

I started by opening the folder using:

```
thunar .
```

and then opened the PCAP with Wireshark.

![Opening the PCAP](/picoCTF/Forensics/attachments/Pasted%20image%2020260825143015.png)

Once inside Wireshark, we can already see that there is BitTorrent traffic going on. Since we specifically want to look at the torrent-related packets, I filtered for BitTorrent DHT traffic using:

```
bt-dht
```

![BitTorrent DHT filter](/picoCTF/Forensics/attachments/Pasted%20image%2020260825143409.png)

After scrolling through the filtered packets, one thing kept showing up over and over again: an `info-hash`.

![Info hash](/picoCTF/Forensics/attachments/Pasted%20image%2020260825143544.png)

The info hash looked like a large random value at first, so I searched up what it was and found that torrent info hashes can be used to create a magnet link.

The format I found was basically:

```
magnet:?xt=urn:btih:<info-hash>
```

So I copied the info hash from the packet, placed it into the magnet link, and pasted that into my browser.

That automatically opened my torrenting software, which in my case was BitTorrent, and from there it showed the file that the user in the packet capture was trying to download.

The filename itself is what the challenge wants us to submit as the flag.
