# I Built My Own Teleprompter Without Writing a Single Line of Code. You Can Use It for Free.

## 5 headline options

1. **I Built My Own Teleprompter Without Writing a Single Line of Code. You Can Use It for Free.**
2. 0 Lines of Code: How I Built the Teleprompter I Use for Every Video
3. I Was Tired of Cleaning My Scripts by Hand, So I Asked Claude to Build Me a Tool
4. Stop Waiting for the Perfect App. Here's the Brief I Used to Build My Own.
5. How a Non-Coder Can Build a Real Tool With AI: My Teleprompter, Step by Step

**Chosen headline:** I Built My Own Teleprompter Without Writing a Single Line of Code. You Can Use It for Free.
**Subtitle:** Before every video I was cleaning my script by hand and pasting it into an app. So I explained the problem to Claude. Here's what it built, the exact brief I started with, what broke along the way, and the link so you can use it yourself.

![My teleprompter with the two-minute-rule demo script loaded](https://guljabeen.github.io/TWG-AgentKit/articles/i-built-my-own-teleprompter/images/01-teleprompter.jpg)
*The teleprompter with one of its demo scripts loaded. The table and delivery notes in that script have already been stripped out.*

▶ **Watch the reel (Instagram):** [LINK — to be added]

▶ **Try the teleprompter (free, runs in your browser):**
https://guljabeen.github.io/gul-teleprompter/

▶ **The code (public on GitHub):**
https://github.com/GulJabeen/gul-teleprompter

---

## TL;DR

- **The problem:** before every video I had to clean my script, delete the timings and notes, and copy-paste what was left into a teleprompter app. Every single time.
- **The fix:** I explained that problem to Claude, and it built me a teleprompter that reads my script file as it is and shows only the lines I actually say.
- **What it does:** it scrolls at my real speaking pace (110 words per minute), lets me tap any line to jump there, loops my hook until I get it right, and tells me how long the script runs before I set up the camera.
- **What it is:** one HTML file. There's no app to install and no account. It works on a laptop or a phone.
- **How I built it:** one short brief to start, then one new feature per session. I didn't write any of the code. My job was to explain the problem and test the result.
- **You can use it today**, for free, and the code is public. Both links are above.

---

## AI ke zamane mein bhi itni mazdoori?

I make a lot of videos, and every one of them starts with a script.

My scripts aren't just the words I say. They're working documents. There are beat labels like `[HOOK]` and `[CTA]`, timings like `0:00–0:07`, delivery notes, a scorecard, a sources list, sometimes a whole table of shots.

All of that is useful when I'm writing. None of it should be in front of my eyes when the camera is rolling.

So before every take, I'd do the same boring job. Open the script, delete the timings, delete the tables, delete the notes, copy what's left, open a teleprompter app, paste it in, fix the formatting the app broke, and then finally record.

That's *mazdoori*. Manual labour. In the age of AI, I was doing manual labour to read my own words.

The moment that changed it was a simple question I asked myself: **if AI can build almost anything for me, why am I still bending my workflow around somebody else's app?**

---

## What I built

I'm Gul, Director of Engineering at Hyly and founder of Tech With Gul. Yes, I'm an engineer, but I didn't write a line of this. Claude wrote all of it. I explained what I needed, tested what it built, and told it what to fix.

Here's what the teleprompter does:

- **It reads my script file as it is.** I drop the file in, and it removes the tables, notes, scorecards, sources and checklists on its own. Only the lines I say are left on screen.
- **Beat labels become small chips.** `[HOOK]`, `[EXPLAIN]` and `[CTA]` show up as dim labels above each section, so I always know where I am, but they're never in the way.
- **It scrolls at my speaking speed.** I measured my pace at 110 words per minute, so that's the default. Each line gets time based on how many words are in it, which means a short line doesn't sit on screen as long as a long sentence.
- **Tap any line to jump there.** If I fluff a sentence, I tap it and start again from that point.
- **Loop the hook.** Press `L` and it repeats the current section until I turn it off. The hook is the part I re-record most, so this saves me the most time.
- **Pre-flight check.** Before I record, it shows the word count, how long the script will run at my pace, and whether it's inside my target length. If it's too long, it tells me how many seconds to cut.
- **Filming mode.** Solo mode hides everything except the text. There's a mirror mode for prompter glass, fullscreen, and it keeps my phone screen awake so it doesn't dim halfway through a take.
- **Audio mode.** If I already have a recorded voiceover, I can load it and the text follows the recording instead of a timer.

And all of that is **one HTML file**. Open it in a browser and it works.

---

## How I built it without writing code

### 1. I explained the problem, not the solution

I didn't ask for "a teleprompter app". I described my real situation: my scripts are markdown files full of notes, I only want to see the spoken lines, and I speak at about 110 words per minute.

That's what made the result feel personal. A generic teleprompter wants plain text, and mine reads the exact files I already write.

### 2. I started with one clear brief

This is the brief I started from, cleaned up a little so you can copy it and change it for your own scripts:

> Build me a teleprompter as one self-contained HTML file, no build step, no dependencies. Input: I drop a markdown script on it. Show only the spoken lines: start at the first `[HOOK]`-style beat marker, drop every table, heading, checkbox and code block after the read. Turn beat markers like `[HOOK]` `[EXPLAIN]` `[CTA]` into small dim chips that are never read aloud. Scroll at a speaking pace I set in words per minute (default 110), giving each line time in proportion to its word count. Big type, dark background, a mirror toggle, up/down keys to nudge the eyeline, space to start and stop. Make it work on a phone in the browser.

Notice what's in there: the input, what to remove, what to keep, the speed, and how it should look. That's enough for a first version.

### 3. Then I added one feature per session

The first version was not the version I use today, and it didn't have to be. Every time I filmed with it, I noticed one thing I wanted, and the next session I asked for exactly that one thing:

- loop the current section
- tap a line to jump to it
- swipe or drag to scroll by hand
- follow a recorded audio file instead of a timer
- fullscreen, and keep the screen awake
- a pre-flight panel with the word count and how far over or under my target I am

Small requests are easier to test. If something broke, I knew exactly which change caused it.

### 4. Two plugins made the difference

I build with Claude Code, and two free plugins shaped this project:

- **superpowers** (by obra): it makes Claude brainstorm with me first, write a plan, and then build step by step with tests. I stopped getting 400 lines of code dumped on me with a "good luck".
- **frontend-design** (by Anthropic): it stops every page from looking like the same default AI template. The fonts, spacing and colours in my teleprompter come from this.

If you use Claude Code, here's how to install them:

```
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace

/plugin marketplace add anthropics/claude-code
/plugin install frontend-design@claude-code-plugins
```

### 5. I tested it like a user, and Claude tested it like an engineer

My testing was simple: I filmed with it. Claude's testing went much deeper. It wrote a script that opens the teleprompter in a hidden Chrome browser and checks it automatically: scrolling with a mouse wheel, dragging, tapping lines, swiping with a finger, pressing every key, looping, and playing audio. Each check comes back as pass or fail.

I didn't write that test either. But I did learn to ask for it, and it caught real problems.

---

## What broke along the way

It wasn't magic. Three problems taught me the most:

- **The text and the timer disagreed.** When I first added scrolling by hand, my scrolling and the automatic scrolling fought each other, and the timer showed the wrong position. The fix was to treat my scroll as moving the clock itself, so there's only ever one source of truth about where I am.
- **Safari refused to play audio.** iPhones only allow sound to start from a tap. The audio mode had a countdown before playing, so Safari blocked it. Claude fixed it by quietly unlocking the audio at the moment I tap Start.
- **One update broke the whole page.** At one point the wrong version of the file was published and the page got wrapped twice. Since then there's a written rule in the project's notes about which file gets published, so it doesn't happen again.

None of these needed me to read code. Each time, I described what I saw ("the text jumps back when I let go"), and Claude found the cause.

---

## Try it yourself

You don't need to install anything:

1. Open https://guljabeen.github.io/gul-teleprompter/
2. Click one of the three demo scripts on the left to see how it works. The first one includes a table and delivery notes so you can watch them disappear.
3. Drop in your own script file, or paste your text into the box.
4. Set your speaking speed. If you don't know it, read a paragraph out loud for one minute and count the words.
5. Press Space to start. On your phone, press **Solo** so the screen shows only your text.

Want it offline? Download `index.html` from the GitHub repo and open it in your browser. That's the whole app.

---

## The real point: build the thing you need

I didn't write this article to sell you a teleprompter. It's free.

I wrote it because **you don't need to be a programmer to start building anymore.** Teacher, student, content creator, business owner: you have something that annoys you every single day. A spreadsheet you fix by hand. A report you copy from one place to another. A form you fill in the same way every week.

Stop waiting for someone else to build the perfect app for your exact problem. Explain the problem to AI. Start small. Build the first version, use it, and improve one thing at a time.

*Pehla version perfect nahi hoga. Lekin woh aapka hoga.* The first version won't be perfect, but it will be yours.

Don't just consume AI. Create with it.

---

## Links

- Try the teleprompter: https://guljabeen.github.io/gul-teleprompter/
- Code on GitHub: https://github.com/GulJabeen/gul-teleprompter
- superpowers plugin: https://github.com/obra/superpowers
- frontend-design plugin: https://github.com/anthropics/claude-code

---

**Tags:** Artificial Intelligence · No Code · Claude · Content Creation · Productivity · Tech With Gul
