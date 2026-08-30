# Wireshark twoo twooo two twoo...

In this challenge, we are given another `.pcapng` file and are told to find the flag somewhere inside the capture.

I started with my usual basic recon:

```id="nccq6u"
file shark2.pcapng
exiftool shark2.pcapng
strings shark2.pcapng
```

While looking through the `strings` output, something immediately stood out:

```id="rvqy32"
picoCTF{HEXDATA}
```

Obviously that caught my attention since it was already inside the normal flag format.

But right below it, I noticed that it was connected to traffic involving a domain with `herring` in the name. That made me think it might just be a red herring and something meant to send us down the wrong path.

I still decoded the hex anyway just to make sure.

I wrote a small Python script using `unhexlify`, but when I tried decoding the result as UTF-8 I got an error.

I then tried using `latin1` instead, but the output still did not give me anything useful.

After that, I searched for every occurrence of `picoCTF`:

```id="ftfyle"
strings shark2.pcapng | grep picoCTF
```

This gave me even more fake-looking flags containing different hex strings.

At this point, I thought maybe all of the hex strings had to be combined somehow, so I searched up different ways of decoding multiple hex strings into one output and tried messing around with that for a bit.

That also led nowhere.

So I went back to the drawing board again.

While looking through the traffic in Wireshark, something else caught my eye. There were a bunch of DNS requests going to subdomains under:

```id="oghp0b"
redshrimpandherring.com
```

The beginning of each domain looked like random text:

```id="t0azs0"
<random-data>.redshrimpandherring.com
```

After looking at a few of them, the random parts started looking a lot like Base64.

That seemed way more promising.

I filtered the traffic so I could focus on those DNS requests and then collected the unique subdomain values.

Once I removed the duplicates, joined the pieces together, and decoded the Base64 data, the actual flag came out.

So all of the `picoCTF{HEXDATA}` strings I had been looking at earlier really were just red herrings.

The actual flag was being split into Base64-looking chunks and sent through DNS subdomains.

Once I stopped focusing on the hex strings and looked more closely at the DNS traffic, the intended path became a lot clearer.