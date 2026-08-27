In this challenge, we are given a file called:

```id="a1b2c3"
anthem.flag.txt
```

Opening it shows a huge amount of text, so instead of reading through everything manually, I just searched for anything containing `pico`.

For this I used:

```id="d4e5f6"
grep pico anthem.flag.txt
```

And that immediately gave me the flag.

Pretty simple challenge overall. Since the file was just a large block of text, using `grep` was way faster than manually going through the whole thing.