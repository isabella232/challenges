# Autocorrect

## Language

Anything that takes stdin that I can also run easily.

## Bounty

This is a hurt-me-plenty mission, so a Little Village gyro - and beer - awaits any Skookum challenger who manages to tackle it.
I'll even go out and pick it up for you. In the cold. That's how hard this is.

## Requirements

Someone screwed up a git merge and now the iPhone's autocorrect code has been lost forever.
Shit! Now, when you're sending drunk texts, everyone will know. Unacceptable.

This challenge is to build your own autocorrect algorithm.
It has three levels of difficulty so the Sr. devs don't get an easy beer off me:

### Jr

- accept strings of text via stdin.
- separate words by whitespace (like an iPhone).
- check each word entered against a dictionary (words.txt).
- if the word isn't in the dictionary, find a replacement.
- the replacement should be a dictionary word with the same length and the shortest hamming distance.
- if two replacements share a hamming distance, the one with the higher frequency wins.
- output your corrected string to stdout (don't worry about punctuation or formatting).

### Mid

- your output should exactly match the punctuation of the input string.
- it should also match the formatting (capitalization, white-space) of the input string.

### Sr

- instead of the hamming distance, you'll be using the keyboard distance like a real iPhone.
- all keys on your keyboard are separated by some shortest path (A -> Z = 1, Z -> P = 9).
- for each different symbol, instead of the hamming +1, you'll be adding a +N.
- N is the keyboard distance between the desired key and the one your user fat-fingered.

### Tools at your disposal

- fixtures/words.txt: a dictionary of the top 7.7k English words, sorted by frequency (desc).
- fixtures/test-*.txt: simple test strings with which to run your code.
- fixtures/keymap.json: a map between each relevant keyboard key and its neighbors.

## Jr Example

```
$ node hunter.js fixtures/words.txt < fixtures/test-bill.txt
mersuring => measuring (1)
programmnig => programming (2)
progerss => progress (2)
lihes => lines (1)
measurnig => measuring (2)
aircartf => aircraft (4)
biulding => building (2)
progrses => progress (2)
weught => weight (1)

--- original ---
"Mersuring programmnig progerss by lihes of code is like measurnig aircartf biulding progrses by weught." - Bill Gates



---corrected ---
Measuring programming progress by lines of code is like measuring aircraft building progress by weight Bill Gates

```

## Mid Example

```
node hunter.js fixtures/words.txt < fixtures/test-frequency.txt
cav => can (1)
raq => ran (1)
tun => ten (1)
ne => he (1)

--- original ---
Cav should be 'Can.' raq should be ran. tun should be ten. ne should be he.
This works too, right!?
Numbers: 1, 2, 3. 45678910.


---corrected ---
Can should be 'Can.' ran should be ran. ten should be ten. he should be he.
This works too, right!?
Numbers: 1, 2, 3. 45678910.

```

## Sr Example

```
$ node hunter.js fixtures/words.txt < fixtures/test-difficult.txt
habe => have (1)
alwaus => always (1)
wushed => wished (1)
fir => for (1)
comptuer => computer (4)
easu => easy (1)
ude => use (1)
mt => my (1)
wush => wish (1)
jas => has (1)
vome => come (1)
bwcsusw => because (3)
czm => can (2)
kingrr => longer (3)
dofure => figure (3)
iut => out (1)
yiw => how (2)
yse => use (1)
stroustrup => stroustrup (0)

--- original ---
"I habe alwaus wushed fir my comptuer to be as easu to ude as my telephone; mt wush jas vome true bwcsusw I czm no kingrr dofure iut yiw to yse my telephone." - B. Stroustrup


---corrected ---
"I have always wished for my computer to be as easy to use as my telephone; my wish has come true because I can no longer figure out how to use my telephone." - B. Stroustrup
```