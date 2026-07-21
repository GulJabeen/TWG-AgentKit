# The AI Loop Engineering Guide 🔁
### Stop writing prompts. Start writing loops that stop when they're done.

*A complete, no-hype guide to running self-checking AI loops in Claude Code — the two commands, the finish-line formula that keeps them from burning your tokens, five copy-paste recipes, and where the field is heading next.*

*By [@techwithgul.ai](https://instagram.com/techwithgul.ai) · Last verified 17 July 2026*

---

## What this guide covers

1. [The shift: a prompt is a dead end](#1-the-shift-a-prompt-is-a-dead-end)
2. [What a loop actually is](#2-what-a-loop-actually-is)
3. [The two commands: `/loop` and `/goal`](#3-the-two-commands-loop-and-goal)
4. [The one skill that matters: a measurable finish line](#4-the-one-skill-that-matters-a-measurable-finish-line)
5. [The trap that burns your tokens](#5-the-trap-that-burns-your-tokens)
6. [The Loop Cookbook — 5 recipes](#6-the-loop-cookbook--5-recipes)
7. [Beyond one loop: routines and swarms](#7-beyond-one-loop-routines-and-swarms)
8. [The frontier: is the loop itself the bug?](#8-the-frontier-is-the-loop-itself-the-bug)
9. [Pre-flight checklist](#9-pre-flight-checklist)
10. [Sources](#10-sources)

---

## 1. The shift: a prompt is a dead end

There's a quiet shift in how the best people use AI, and it hides behind a boring word: **loop**.

You'll hear it framed dramatically — *"I don't write prompts anymore, I write loops"* — and the fair reaction is: isn't a loop just a prompt with extra steps? Kind of. But that extra step is the whole game. It's the difference between AI as a vending machine you keep feeding coins, and AI as a coworker who checks their own work before handing it back.

Think about what happens every time you prompt an AI — Claude, ChatGPT, Codex, it doesn't matter. You ask for something. It responds. **And then it stops.**

That full stop is the problem. The job of *judging the answer* now falls entirely on you. You read it, decide it's not quite right, and type some version of *"no, do it again, shorter and less corporate."* It tries again. You judge again. Repeat until you're happy or exhausted.

Here's the uncomfortable truth: **you are the loop.** The AI does one lap; you are the part that checks the result and sends it back around. For a one-off email, fine. For anything real — fixing a failing test suite, migrating fifty call sites to a new API, checking every link in an article — being the loop yourself is death by a thousand re-prompts.

---

## 2. What a loop actually is

A loop moves the checking *inside* the machine.

Same email example. Instead of *"write me a better email,"* you say something closer to: **"write this email, then grade it against these criteria, and if it doesn't pass, rewrite it — keep going until it passes."**

Now the flow has a return path:

```
        ┌─────────────────────────────┐
        │                             │
   you ─┴─▶  AI writes  ──▶  AI checks it ──▶ good enough? ──▶ you get the answer
                  ▲                         │
                  │            no           │
                  └─────────────────────────┘
```

The AI writes, checks against a standard, and if it falls short it tries again — **on its own** — until the result clears the bar. You step out of the middle and come back only for the finished product.

That's it. That's a loop. Not magic — just a prompt that includes *"and don't stop until this is true."* The whole discipline of running these well — the commands, the finish lines, the scheduled and multi-agent variants — is what people now call **loop engineering**.

---

## 3. The two commands: `/loop` and `/goal`

This isn't theory. Claude Code ships two ways to run a loop, and they're worth telling apart. Both are about five characters. They are **not** the same thing.

### `/loop` — run it again and again

```
/loop edit this article so every claim has three verified sources
```

`/loop` reruns a prompt across turns instead of stopping after one.

- **Give it an interval** — every 5 minutes, say — and it fires on the clock. Perfect for *"poll the deploy until it's live."*
- **Omit the interval and it self-paces.** Claude watches its own output, picks its next delay (anywhere from a minute to an hour), keeps working, checks its own progress each turn, and stops when *it* decides the work is done — or when you stop it.

Reach for `/loop` when the task is fuzzier, long-running, or genuinely time-based.

### `/goal` — work until a *measurable condition* is true

```
/goal every test in the auth folder passes and the lint step is clean
```

`/goal` is the close cousin, and it's the one to reach for the moment you can name your finish line precisely.

Here's the mechanism, and it's clever: after **every turn**, Claude Code hands your condition and the conversation so far to a **separate small, fast model** (Haiku by default). That model returns a yes/no — *is the condition met?*

- If **no**, it hands back a one-line reason and Claude starts another turn to fix it.
- If **yes**, the goal clears and control returns to you.

So Claude writes the code, runs the tests, reads the output, and a *second* model referees whether you're actually done. Tests red? It goes again. You didn't type a thing between rounds.

> ⚙️ **One important nuance:** the evaluator judges *what Claude surfaced in the transcript* — it does **not** run tools itself. So your loop has to actually run the test / print the exit code / show the result, or the referee has nothing to check.

### The difference in one line

**`/loop` decides for itself when it's done; `/goal` hands that judgment to a separate evaluator checking an explicit condition you wrote.**

| | `/goal` | `/loop` |
|---|---|---|
| **Next turn starts when** | the previous turn finishes | a time interval elapses (or self-paced) |
| **Stops when** | a model confirms your condition is met | you stop it, or Claude decides it's done |
| **Reach for it when** | "keep working until X is provably true" | "rerun this every N minutes" / long self-paced work |
| **The self-checking-until-good loop** | ✅ this one | reruns, doesn't judge a named condition |

**Requirements:** `/goal` needs Claude Code **v2.1.139 or newer**. Your condition can be up to **4,000 characters** — long enough to spell out the finish line properly.

---

## 4. The one skill that matters: a measurable finish line

This is the single most important section in the guide.

**A loop is only as good as its finish line — and the finish line has to be measurable.**

Give a loop a fuzzy goal and it never knows when to stop. *"Make this better."* Better than what? Judged how? The evaluator can't tell, so the honest answer is always *"eh, could be better"* — and it loops. And loops. And quietly incinerates your tokens while you're getting coffee.

A good stop condition has **three parts**:

1. **One measurable end state** — a test result, a build exit code, a file count, an empty queue.
2. **A stated check** — *how* the AI should prove it. `npm test exits 0`. `git status is clean`. `every link returns HTTP 200`.
3. **Constraints that matter** — what must *not* change on the way there. `without modifying any other test file`.

Compare:

- ❌ *"Improve the test coverage."* → no finish line. Infinite loop, real money.
- ✅ *"Add tests until `npm run coverage` reports ≥ 90% on `src/auth`, every new test passes, without touching existing tests."* → the referee can definitively say **done**.

The mental shift: you're no longer writing *instructions*, you're writing a **spec with an exit test.** The prompt matters less than the finish line.

---

## 5. The trap that burns your tokens

Even a perfect condition can misbehave if the goal turns out to be impossible (a test that can't pass, a flaky service). So add a hard safety net **inside the condition itself**:

```
…or stop after 20 turns and summarise what's left.
```

Claude reports progress against that clause every turn, so even an unachievable goal can't run forever. Belt and suspenders.

**Two rules that save your credits:**

- **Always add `or stop after N turns`.** It's your seatbelt.
- **Pair loops with auto mode** so the run is genuinely unattended — otherwise it pauses to ask permission for each command and the hands-off magic disappears.

---

## 6. The Loop Cookbook — 5 recipes

Copy-paste `/goal` conditions that actually terminate. (Also in [`loop-cookbook.md`](./loop-cookbook.md) in this folder — the one-pager version.)

**The formula, every time:** one measurable end state + the check + a guardrail and a hard stop.

**1. Fix a failing test suite**
```
/goal every test in ./tests passes when I run `npm test`, the command exits 0,
and no test file is modified — or stop after 25 turns and summarize what's left
```

**2. Verify every source in an article**
```
/goal every external link in article.md returns HTTP 200 and its page actually
supports the claim it's cited for. Go link by link. Replace any dead or
mismatched source. Stop when all links pass or after 15 turns.
```

**3. Migrate to a new API**
```
/goal every call site of the old `fetchUser()` API is migrated to `getUser()`,
the project compiles, and `npm test` exits 0 — without changing test expectations.
Stop after 30 turns if not complete.
```

**4. Generate docs until coverage is real**
```
/goal every exported function in ./src has a docstring, `npm run docs` builds
with zero warnings, and the README lists every public module. Stop after 20 turns.
```

**5. Refactor a giant file to size**
```
/goal split ./src/app.js so no file exceeds 200 lines, all imports still resolve,
and `npm test` exits 0. Don't change behavior. Stop after 20 turns.
```

Notice the pattern in all five: a command or number the referee can objectively check (`exits 0`, `HTTP 200`, `no file exceeds 200 lines`), a guardrail (`without changing test expectations`), and a hard turn cap.

---

## 7. Beyond one loop: routines and swarms

`/loop` and `/goal` are the entry point. "Loop engineering" as a discipline covers two more moves worth knowing:

- **Routines** — a loop on a schedule that runs whether or not you're at the keyboard: *"every morning at 8am, pull open PRs, summarise them, and post the digest."* A `/loop` with an interval is the simplest routine; full routines can run as scheduled cloud agents.
- **Swarms** — multiple agents working in parallel on independent slices of one job, each with its own loop, results merged at the end. The move when the work is big enough that one context can't hold it: audits, migrations across many files, broad sweeps.

The mental model scales cleanly: a **goal** is one measurable finish line, a **routine** is that loop on a clock, and a **swarm** is many loops running at once. Same core idea — *specify the finish line, let it run* — at three sizes.

---

## 8. The frontier: is the loop itself the bug?

Once you've run a few loops you feel the rough edges — especially that unbounded-retry failure mode. You're not the only one who noticed.

In **April 2026**, a paper landed with a provocative argument: **the Agent Loop paradigm is structurally flawed.** It's *"From Agent Loops to Structured Graphs: A Scheduler-Theoretic Framework for LLM Agent Execution"* (Hu Wei, [arXiv 2604.11378](https://arxiv.org/abs/2604.11378)).

Its critique names three weaknesses of the plain loop:

1. **Implicit dependencies** between steps — the order of operations lives in the conversation, not in any structure you can inspect.
2. **Unbounded recovery loops** — exactly the token-burn problem above, with no built-in termination guarantee.
3. **Mutable execution history** — the record keeps changing, which makes debugging and verification miserable.

Its proposed fix is the **Structured Graph Harness (SGH)**: lift the control flow *out of* the conversation and into an **explicit, static graph** (a DAG), with immutable plans per version and a strict escalation protocol so recovery can't spiral.

**Two honest caveats:**

- The author calls it a **position paper and design proposal** — a framework and an argument, **not** a benchmarked, shipped result. Treat it as a direction the field is exploring, not a tool you install tonight.
- The practical takeaway is available to you *right now* without any of the theory: **the more you specify your loop's structure and its exit condition up front, the less it wanders.** SGH is the rigorous version of this whole guide's advice — *give it a measurable finish line.*

---

## 9. Pre-flight checklist

Before you hit enter on a loop:

- [ ] **Is there one measurable end state?** (A number, an exit code, a status — not a vibe.)
- [ ] **Did you state the check?** How the AI proves it's done (`npm test exits 0`).
- [ ] **Does the loop actually surface the result** so the evaluator can see it? (Print the output; the referee doesn't run tools.)
- [ ] **Did you name what must not change?** The guardrail.
- [ ] **Is there a hard stop?** `…or stop after N turns.` Always.
- [ ] **Right command?** `/goal` for "until X is true", `/loop` for "rerun / self-paced".
- [ ] **Auto mode on** for a genuinely hands-off run.
- [ ] **On Claude Code v2.1.139+** for `/goal`.

If all eight are ticked, you've written a spec with an exit test — the actual skill in loop engineering. Write the exit test, then let it run.

---

## 10. Sources

Everything in this guide was verified on 17 July 2026 against primary docs and the paper itself.

| Resource | What it covers | Link |
|---|---|---|
| Claude Code Docs — `/goal` | The command, the Haiku evaluator, how to write a condition | https://code.claude.com/docs/en/goal |
| Claude Code Docs — scheduled tasks (`/loop`) | `/loop` interval + self-pace behaviour | https://code.claude.com/docs/en/scheduled-tasks |
| arXiv 2604.11378 | SGH — the "structured graph harness" paper (Hu Wei, Apr 2026) | https://arxiv.org/abs/2604.11378 |
| Loop Engineering — Definitive Guide | Umbrella framing (goal / loop / routines / swarms) | https://www.developersdigest.tech/blog/loop-engineering-definitive-guide |
| sabrina.dev — Loop Engineering | Practical `/goal` + routines walkthrough | https://www.sabrina.dev/p/loop-engineering-claude-code-goal-routines |
| MindStudio — `/goal` & `/loop` | Autonomous long-running tasks explainer | https://www.mindstudio.ai/blog/claude-code-goal-loop-commands-autonomous-tasks |

---

*Want the one-page version to keep next to your terminal? It's [`loop-cookbook.md`](./loop-cookbook.md) — five recipes and the formula, nothing else.*

*More AI that's actually true — no hype, just what works → [@techwithgul.ai](https://instagram.com/techwithgul.ai)*
