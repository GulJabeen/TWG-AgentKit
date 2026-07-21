# The Loop Cookbook 🔁
### 5 copy-paste Claude Code goals that actually stop when they're done

*Delivered when someone comments **LOOP**. This is the thing that makes a loop safe: a finish line the AI can measure, so it never spins in circles burning your tokens.*

---

## The formula (steal this)

Every good loop condition has **3 parts**:

1. **One measurable end state** — a test result, an exit code, a file count, an empty queue.
2. **The check** — *how* it proves it's done (`npm test exits 0`, `git status is clean`, `returns HTTP 200`).
3. **A guardrail** — what must NOT change, plus a hard stop: `…or stop after 20 turns`.

> Fuzzy goal → infinite loop. Measurable goal → it knows exactly when to quit.

Use `/goal <condition>` when you can name the finish line precisely. Use `/loop` (no interval) when the task is fuzzier and you want Claude to self-pace and stop when it judges the work done.

---

## 1. Fix a failing test suite

```
/goal every test in ./tests passes when I run `npm test`, the command exits 0,
and no test file is modified — or stop after 25 turns and summarize what's left
```

## 2. Verify every source in an article (the reel example)

```
/goal every external link in article.md returns HTTP 200 and its page actually
supports the claim it's cited for. Go link by link. Replace any dead or
mismatched source. Stop when all links pass or after 15 turns.
```

## 3. Migrate to a new API

```
/goal every call site of the old `fetchUser()` API is migrated to `getUser()`,
the project compiles, and `npm test` exits 0 — without changing test expectations.
Stop after 30 turns if not complete.
```

## 4. Generate docs until coverage is real

```
/goal every exported function in ./src has a docstring, `npm run docs` builds
with zero warnings, and the README lists every public module. Stop after 20 turns.
```

## 5. Refactor a giant file to size

```
/goal split ./src/app.js so no file exceeds 200 lines, all imports still resolve,
and `npm test` exits 0. Don't change behavior. Stop after 20 turns.
```

---

## Two rules that save your credits

- **Always add `or stop after N turns`.** It's your seatbelt. Even an impossible goal can't run forever.
- **Pair with auto mode** so the loop runs unattended — otherwise it pauses to ask permission for each command and the "hands-off" magic disappears.

---

*Want the full breakdown — why loops beat prompts, `/loop` vs `/goal`, and the April paper arguing loops themselves are the bug? → [The AI Loop Engineering Guide](./ai-loop-engineering-guide.md)*

*More AI that's actually true → [@techwithgul.ai](https://instagram.com/techwithgul.ai)*
