# Wireshark doo dooo do doo...

In this challenge, we are provided with a `.pcapng` file, which is basically a packet capture containing recorded network traffic.

We are not really given any useful hints here. The challenge pretty much just tells us to find the flag.

I also wanted to solve this one without immediately opening Wireshark since I am still not that comfortable with it, so I started with my usual simple recon first:

```
file capture.pcapng
exiftool capture.pcapng
strings capture.pcapng
```

None of these immediately gave me anything useful.

At this point I thought maybe the flag was simply sitting somewhere in plaintext, so I tried:

```
strings capture.pcapng | grep pico
```

Still nothing.

I was a little stuck here, but then I thought about the possibility that the flag itself might be encoded.

In this case, the flag turned out to be encoded using ROT13. ROT13 changes letters, but characters such as `{` and `}` stay the same.

For example:

```
picoCTF{example}
```

could become:

```
cvpbPGS{rknzcyr}
```

The letters change, but the braces are still there.

So instead of searching for `pico`, I searched for the opening brace:

```
strings capture.pcapng | grep {
```

This gave me a much smaller amount of output to look through, and one of the strings immediately looked like a flag format, just with the letters changed.

Since it looked like ROT13, I decoded it and got the actual flag.

So in the end, I did not even need to open Wireshark for this one. Just `strings`, `grep`, and noticing that the braces were still there was enough to find it.