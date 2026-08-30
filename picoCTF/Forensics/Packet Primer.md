# Packet Primer

In this challenge, we are presented with a `.pcap` file.

Whenever I get files like this, I usually like doing some quick checks first just to see if anything obvious is sitting inside before opening Wireshark and going deeper into packet analysis.

This one turned out to be pretty much low-hanging fruit.

Instead of immediately opening the capture in Wireshark, we can just extract the readable strings, search for the flag format, and remove the spaces:

```
strings networkdump.flag.pcap | grep "picoCTF" | tr -d " "
```

The flag inside the packet capture has spaces between each character, so `tr -d " "` just removes those spaces and cleans the output up for us.

After running the command, the flag comes out immediately.

You could also open the file in Wireshark and follow the TCP stream, but for this challenge the command-line approach was enough and much faster.
