# PcapPoisoning

In this challenge, we are given a PCAP trace file containing around 1501 packets, and we are told that the flag is somewhere inside the capture.

I started by looking through a few packets individually, but none of them showed anything useful or anything that looked like a flag.

Since checking all 1501 packets manually would take forever, I figured this challenge was probably meant to be solved using some basic filtering.

I started looking at simple things first, such as the packet timings and the different protocols being used.

Nothing really stood out there, so I decided to check the packet lengths instead.

I sorted the packets by length and looked at the largest packet in the capture.

And boom, the flag was sitting right there.

Pretty simple challenge overall, but it was a good reminder that when dealing with a large PCAP, you do not always need some complicated filter. Sometimes just sorting and looking for something that stands out is enough.
