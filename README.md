# CTF Writeups

Welcome!

This repository is where I host pretty much every CTF writeup I thought was worth writing about. Lol.

A lot of these challenges were solved while I was still learning the concepts behind them, while others are more recent and hopefully show that I am, in fact, getting better at this.

Instead of making every writeup look like:


&emsp;&emsp;***"I immediately knew exactly what was happening, ran one command, got the flag, and definitely did not spend 40 minutes investigating something completely irrelevant."***


I try to document what actually happened.

That means most of my writeups include what I noticed, what I initially thought was happening, what I tried, what completely failed, the random rabbit holes I somehow convinced myself were important, and eventually the thing that made everything click.

Basically, these writeups show not only **how I solved the challenge**, but also **how I thought while solving it**.

And yes, sometimes that thought process is:

```text
"This looks suspicious."
        ↓
*spends 30 minutes investigating it*
        ↓
"It was not suspicious."
```

That is part of the learning process too.

---

## Why This Repository Exists

CTFs have been one of the main ways I practice cybersecurity.

They force me to deal with unfamiliar applications, strange files, broken implementations, network traffic, obscure vulnerabilities, and occasionally something that makes me question every decision that led me to studying cybersecurity.

But that is exactly what makes them useful.

A challenge usually starts with:

```text
I have no idea what this is.
```

and hopefully ends with:

```text
Ohhhhhhh.
```

This repository documents everything between those two moments.

I wanted somewhere I could keep track of the techniques I learned, the mistakes I made, and the reasoning that eventually led me to a solution.

It also gives me a way to look back at older challenges and see how my approach has changed over time.

Some of the earlier writeups may be simpler or slightly chaotic.

That is intentional.

They are part of the progression.

---

## What You Will Find Here

The writeups in this repository cover different areas of CTFs and cybersecurity, although **Web Exploitation is the category I enjoy the most**.

### Web Exploitation

Web exploitation is probably where I have the most fun.

I enjoy taking an application apart mentally, figuring out how data moves through it, understanding what assumptions the developer made, and then seeing whether those assumptions actually hold up.

There is something extremely satisfying about going from:

&emsp;&emsp;***"This application looks completely normal."***

to:

&emsp;&emsp;***"Oh. You definitely should not have trusted that input."***

What I enjoy most is when a challenge forces me to understand the application instead of just remembering a payload. I would rather understand **why** something is exploitable than know one string that happens to work.

The more web challenges I solve, the more I find myself looking beyond individual vulnerabilities and thinking about how the application's components interact as a whole.

And sometimes the solution still ends up being one character I somehow did not notice for an hour.

Naturally.

---

### Digital Forensics

Forensics is another area I spend a lot of time practicing.

What I enjoy about it is the investigative side. You are often given an artifact with very little context and have to slowly figure out what happened from whatever evidence was left behind.

Forensics has gradually changed the way I approach files.

Instead of immediately asking:

&emsp;&emsp;***"Where is the flag?"***

I try to ask:

&emsp;&emsp;***"What is this supposed to look like, and what looks wrong?"***

That mindset tends to get me much further.

Sometimes the interesting part is obvious. Sometimes the entire file looks completely normal and the challenge author has decided that happiness is optional.

Either way, I enjoy the process of narrowing things down until one small detail starts making sense.

---

### Cryptography

Crypto and I have an interesting relationship.

I enjoy it when I can understand the underlying weakness and work through why the system fails. There is something satisfying about taking something that initially looks like complete mathematical nonsense and slowly reducing it into something understandable.

Crypto has also taught me an important lesson:

Sometimes something that looks insanely complicated becomes very simple once you understand the underlying idea.

Other times it is actually insanely complicated.

You win some, you lose some.

---

### Network Analysis

Network challenges have taught me that staring at thousands of packets at once is generally not a productive strategy.

I like reconstructing what happened from network traffic, narrowing down conversations, following the right pieces of data, and eventually finding the activity that actually matters.

A packet capture can look completely overwhelming at first, but once you start asking specific questions instead of trying to understand everything at once, it becomes much more manageable.

Filters are a wonderful invention.

---

### Everything Else

CTFs are weird, so not every challenge fits neatly into one category.

Sometimes I end up dealing with reversing, scripting, automation, OSINT, source code, some strange custom format, or whatever else the challenge author decided would ruin my afternoon.

Sometimes a challenge starts as web, becomes crypto, somehow turns into scripting, and ends with me wondering how I got there.

Those are usually the fun ones.

Usually.

---

## How I Approach Challenges

I try not to treat cybersecurity tools like magic buttons.

Depending on the problem, I might use Burp Suite, Wireshark, Autopsy, Python, or some Linux utility I discovered five minutes earlier.

The tool itself is usually not the important part.

The important question is:

&emsp;&emsp;***What information am I trying to get, and what is the best way to get it?***

I would rather understand why a command or payload worked than memorize something that happened to give me the flag once.

My investigation process generally looks something like this:

```text
What am I looking at?
        ↓
What do I know about it?
        ↓
What looks unusual?
        ↓
Why could that matter?
        ↓
Form a hypothesis
        ↓
Test it
        ↓
Wrong
        ↓
Adjust the hypothesis
        ↓
Still wrong
        ↓
Question life choices
        ↓
Notice one tiny detail
        ↓
"Oh."
        ↓
Flag
```

Jokes aside, learning to work systematically has probably been one of the biggest things CTFs have taught me.

I try to understand the problem first, identify what I actually control or observe, form a hypothesis, test it, and then use the result to decide what to do next.

It is not always that clean in practice.

Sometimes the real process is:

```text
try something
change one thing
try again
stare at response
read source
realize I misunderstood everything
"Oh."
```

But we improve.

---

## Failed Attempts Are Included

A lot of technical writeups make it look like the author knew the solution from the beginning.

I usually did not.

If I went down a path that looked reasonable but turned out to be completely wrong, I may include it.

If I misunderstood how something worked, I may explain what I misunderstood.

If I spent an embarrassing amount of time trying to solve the wrong problem, there is a decent chance that ends up in the writeup too.

Why?

Because failure is useful information.

Knowing:

```text
Approach A → does not work because X
```

can sometimes teach you more than simply seeing:

```text
Approach B → flag
```

The dead ends also make the writeups more honest.

Real problem solving rarely looks like:

```text
Observation → genius realization → flag
```

It is usually more like:

```text
Observation
→ questionable idea
→ failed test
→ better idea
→ another failed test
→ research
→ one useful clue
→ solution
```

And if somebody finds one of these writeups later and avoids the same rabbit hole, then my suffering was at least useful to somebody.

---

## Watching Myself Improve

One thing I like about keeping these writeups is being able to see my progress over time.

Some of my earlier solutions were basically:

```text
try random thing
try another random thing
Google error
?????????
```

while newer challenges are usually approached much more deliberately.

I have gotten better at recognizing what information actually matters, researching concepts without immediately searching for the solution, testing assumptions, writing small scripts when necessary, and documenting why I made certain decisions.

That progression is something I intentionally want this repository to show.

I do not want to rewrite every old writeup to make it look like I understood everything immediately.

I did not.

I learned it challenge by challenge.

And I am still learning.

Probably always will be.

Cybersecurity is slightly inconvenient like that.

---

## For Recruiters and Employers

If you are looking through this repository as part of my portfolio, hi.

I promise the excessive amount of terminal screenshots has a purpose.

CTFs are controlled environments and obviously are not identical to real-world security work, but they give me a place to repeatedly practice something I think matters a lot more than simply memorizing vulnerability names:

**working through technical problems when I do not immediately know the answer.**

These writeups show how I investigate unfamiliar systems, understand application behavior, research concepts I have not encountered before, automate repetitive work when necessary, troubleshoot incorrect assumptions, and communicate how I reached a result.

When I encounter something unfamiliar, my general approach is:

```text
Understand the problem
        ↓
Identify what I do not know
        ↓
Learn enough to test an idea
        ↓
Test it
        ↓
Analyze the result
        ↓
Adapt
        ↓
Document what happened
```

A résumé can tell you that I have used certain technologies.

This repository is where I would rather **show what I actually do with them**.

More importantly, it shows something that is much harder to fit into a skills section:

&emsp;&emsp;***How I think when the answer is not immediately obvious.***

---

## For Other CTF Players

If you found this repository because you are stuck on one of the same challenges, feel free to use my writeups as a reference.

But I recommend trying the challenge yourself first.

Seriously.

Do not immediately scroll straight to:

```text
FLAG:
```

You are robbing yourself of the best part.

A much better way to use a writeup is:

```text
Try challenge
        ↓
Get stuck
        ↓
Figure out what you don't understand
        ↓
Learn that part
        ↓
Try again
        ↓
Use the writeup when you actually need it
```

The goal should not be to memorize:

```text
thing-that-gives-flag
```

The goal should be to understand:

&emsp;&emsp;***Why did that work?***

Because eventually another challenge will use the same idea in a completely different way.

And when you recognize it yourself the next time, that feeling is extremely satisfying.

---

## Ethical Use

Everything documented here is intended for CTF competitions, cybersecurity labs, educational environments, personal systems, and other systems where security testing is explicitly authorized.

Please do not take something from one of these writeups and immediately throw it at some random production website because:

&emsp;&emsp;***"Well technically I was learning."***

That is not how authorization works.

Use what you learn responsibly.

---

## The Point of All This

A flag tells me:

&emsp;&emsp;***I solved the challenge.***

A writeup tells me:

&emsp;&emsp;***I actually understood what happened.***

That distinction matters to me.

I want to be able to open one of these writeups months later and remember what the challenge was doing, which clues mattered, what fooled me, what finally worked, and what I learned from the whole thing.

Every challenge adds another small piece to the way I approach cybersecurity problems.

One challenge teaches me something about web applications.

Another teaches me something about a file format.

Another teaches me a protocol.

Another teaches me that I should probably read the source code more carefully before spending an hour trying increasingly cursed payloads.

Eventually those lessons stack up.

---

## Still Learning

This repository is very much a work in progress.

There are still tons of things I do not know.

There will probably always be tons of things I do not know.

That is also what keeps cybersecurity interesting.

The process usually goes:

```text
"I don't understand this."
        ↓
Learn what it is
        ↓
Experiment
        ↓
Break something
        ↓
Understand it slightly better
        ↓
Experiment again
        ↓
Solve challenge
        ↓
Write about it
        ↓
Encounter something even weirder
```

Repeat forever.

---

## Final Note

If you are another CTF player, I hope something here helps you get unstuck.

If you are learning cybersecurity, I hope these writeups show that you do not need to instantly understand every concept you encounter.

And if you are an employer looking through my GitHub, hopefully this repository gives you a better idea of how I approach unfamiliar technical problems than a résumé line saying:

&emsp;&emsp;***"Familiar with Burp Suite."***

Because I would much rather show the actual investigation.

Thanks for checking out the repository.

Expect more writeups, more scripts, more mistakes, more cursed payloads, more rabbit holes, and hopefully fewer moments where the solution was sitting directly in front of me the entire time.

No promises on that last one.
