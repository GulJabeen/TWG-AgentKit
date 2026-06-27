# Claude Tag — the free alternative (beginner-friendly guide)

> **In one sentence:** Claude Tag is Anthropic's paid feature that lets you tag `@Claude` in Slack so it does real work for you — and it charges you for every task. This guide shows you how to build the *same thing* for about **$0–$5 a month**, step by step, even if you've never written a line of code.

**Time to set up:** about 60–90 minutes the first time.
**Skill level:** none required. If you can sign up for a website and copy-paste, you can do this.
**What it costs:** $0 if you run it on your own laptop, or about **$5/month** if you want it running 24/7.

---

## Part 1 — Understand what you're replacing (2-minute read)

### What Claude Tag does
Inside Slack, you type `@Claude summarize this thread` or `@Claude draft a reply to this client`, and it does it. It:

- **Remembers** what happened in the channel, even days later
- **Acts on its own** — can schedule follow-ups and check back in
- Runs as **your company's account**, not a personal login

### Why it costs money
- It's only available on **Slack Team and Enterprise plans** (the paid business tiers).
- It uses **"consumption billing"** — fancy words for *"the more you use it, the more you pay."* Every task quietly spends credits.
- There is **no free version.**

### The trick this guide teaches
A "tag-it-in-Slack AI" is really just **two simple pieces glued together:**

1. **A bot** — a small program that sits inside Slack and listens for your messages.
2. **A brain** — an AI model (like Gemini or Llama) that the bot sends your message to and gets an answer back.

Anthropic charges you because *they* run both pieces for you. If **you** run them, the same magic costs almost nothing. That's the whole secret.

> **Analogy:** Claude Tag is like ordering coffee at a café every day — easy, but you pay each cup. This guide is buying a $5 coffee machine. A little setup once, then free coffee forever.

---

## Part 2 — The scary words, explained simply

You'll see these words below. Don't skip — they're easy:

| Word | What it actually means |
|---|---|
| **Bot** | A small program that lives in Slack and answers when you tag it. |
| **AI model / LLM** | The "brain." It reads your message and writes a reply. Gemini, Llama, etc. are all brains. |
| **API key** | A long secret password that lets your bot talk to the AI brain. You copy it once and paste it in. Like a house key — keep it private. |
| **Token** | The free brains let you ask a certain number of questions per day. "Tokens" are just how they count usage. The free amounts are generous. |
| **Server / VPS** | A computer in the cloud that's always on, so your bot works even when your laptop is closed. You rent one for ~$5/month. **Optional** — you can skip this and run it on your own laptop to start. |
| **Terminal** | The black text window where you type commands. We give you the exact lines to copy-paste. You don't need to understand them. |

That's it. Now let's build.

---

## Part 3 — Build it (follow these in order)

We'll do the **easiest reliable path**: a free Slack bot called **OpenClaw**, powered by **Google Gemini** (free), running first on your own computer (so you can test it for $0), then optionally moved to a $5 server.

> Prefer **zero code** with drag-and-drop boxes instead? Skip to **Part 6 — The no-code path (n8n)**. Both give you the same result; pick the one that sounds friendlier to you.

---

### Step 1 — Get your free AI brain (Google Gemini) · ~10 min

This is the easiest part, so we do it first to build confidence.

1. Go to **https://aistudio.google.com** and sign in with any Google account.
2. Click **"Get API key"** (left sidebar or top-right).
3. Click **"Create API key"** → **"Create API key in new project."**
4. A long string appears (it starts with `AIza...`). Click **Copy.**
5. Paste it somewhere safe for a minute — a Notes file or sticky note. **This is your brain's password. Never share it publicly or post it online.**

✅ **You now have a free AI brain.** Gemini's free tier is generous (over a million words of context, multiple requests per minute). For most people it never costs a cent.

> **Backup brains (optional):** You can grab free keys from **Groq** (groq.com — very fast) or **OpenRouter** (openrouter.ai — many models, one key) the same way. Having a second key means if one hits its daily free limit, you switch to the other. Not needed to start.

---

### Step 2 — Create your bot in Slack · ~15 min

You're going to create a Slack "app" — that's just Slack's word for a bot. It's free.

1. Go to **https://api.slack.com/apps** and sign in with the Slack workspace you want the bot in.
2. Click **"Create New App"** → **"From scratch."**
3. Name it (e.g. `MyAI`), pick your workspace, click **Create App.**
4. In the left menu, click **"Socket Mode"** → turn the toggle **On.** (Socket Mode just lets your bot work without needing a public website address — perfect for running at home.) When it asks, generate an **App-Level Token**, name it anything, and **copy that token** (it starts with `xapp-`). Save it next to your Gemini key.
5. In the left menu, click **"OAuth & Permissions."** Scroll to **"Scopes" → "Bot Token Scopes"** and click **"Add an OAuth Scope."** Add these (type each name and select it):
   - `app_mentions:read` (lets it see when you tag it)
   - `chat:write` (lets it reply)
   - `channels:history` (lets it read channel messages for context)
   - `im:history` and `im:write` (lets it work in direct messages)
6. Click **"Event Subscriptions"** in the left menu → turn it **On.** Under **"Subscribe to bot events,"** click **Add** and add `app_mention`. Save.
7. Scroll back to the top of **"OAuth & Permissions"** and click **"Install to Workspace"** → **Allow.** A second token appears called the **Bot User OAuth Token** (starts with `xoxb-`). **Copy and save it.**

✅ **You now have three saved secrets:** the Gemini key (`AIza...`), the App token (`xapp-...`), and the Bot token (`xoxb-...`). Keep all three together.

---

### Step 3 — Connect the bot to the brain (OpenClaw) · ~20 min

Now we glue them together. OpenClaw is the free open-source bot that lives in Slack — the same kind of tool this `@techwithgul` account runs.

**First, install the two free tools OpenClaw needs:**

1. **Open your Terminal:**
   - **Mac:** press `Cmd + Space`, type `Terminal`, press Enter.
   - **Windows:** press the Start button, type `PowerShell`, press Enter.
2. Install **Node.js** (the engine OpenClaw runs on): go to **https://nodejs.org**, download the big green **"LTS"** button, and run the installer (just keep clicking Next). Done.
3. Back in the Terminal, copy-paste this line and press Enter to install OpenClaw:
   ```
   npm install -g openclaw
   ```
   *(If it complains about permission on Mac, paste `sudo npm install -g openclaw` instead and type your computer password — the typing stays invisible, that's normal.)*

**Now tell OpenClaw your three secrets.** Run:
```
openclaw setup
```
It will ask you, one at a time, to paste:
- your **Slack Bot token** (`xoxb-...`)
- your **Slack App token** (`xapp-...`)
- which **AI brain** to use → choose **Gemini** and paste your **Gemini key** (`AIza...`)

> If your version doesn't have a `setup` wizard, it instead reads a small settings file. Open the file it points you to and paste each secret next to its label (`slackBotToken`, `slackAppToken`, `geminiApiKey`). The wizard is just doing this for you.

**Start the bot:**
```
openclaw start
```
When you see something like **"connected to Slack"**, it's alive. 🎉

---

### Step 4 — Test it · ~2 min

1. In Slack, go to any channel and click **"Add apps"** → add your bot, OR type `/invite @MyAI` in the channel.
2. Type: `@MyAI summarize the last 10 messages in this channel.`
3. Watch it reply.

**It works = you just rebuilt Claude Tag for free.** Tag it for summaries, draft replies, rewrites, brainstorming — anything you'd ask any AI.

> Keep the Terminal window open while you use it. Close the window and the bot sleeps. That's exactly what Step 5 fixes.

---

### Step 5 (optional but recommended) — Keep it running 24/7 for ~$5/month

Right now the bot only works while your laptop is on and the Terminal is open. To make it always-on like the real Claude Tag, move it to a tiny rented cloud computer (a "VPS").

1. Sign up at **Hetzner** (hetzner.com/cloud) or **Contabo** — both around **$5/month** for the smallest size, which is plenty.
2. Create the cheapest **Ubuntu** server. They email you an address and a password.
3. Connect to it from your Terminal:
   ```
   ssh root@YOUR-SERVER-ADDRESS
   ```
   Type the password when asked.
4. Run the **same three commands** from Step 3 on the server (`npm install -g openclaw`, `openclaw setup`, `openclaw start`).
5. To make it survive reboots and keep running after you disconnect, install a tiny keep-alive helper:
   ```
   npm install -g pm2
   pm2 start "openclaw start" --name myai
   pm2 save
   pm2 startup
   ```
   *(Copy-paste the extra line `pm2 startup` prints back, and run it — that locks in auto-start.)*

✅ Now you can close your laptop and the bot keeps working — exactly like Claude Tag, for the price of one coffee a month.

> **Even cheaper / fully private:** a one-time **Raspberry Pi 5** (~$80) sitting at home does the same job for about $3/month in electricity, and your data never leaves your house.

---

## Part 4 — Did I really get the same thing? (honest comparison)

| | **Claude Tag (paid)** | **Your free setup** |
|---|---|---|
| Tag it in Slack, does real work | ✅ | ✅ |
| Remembers channel context | ✅ | ✅ |
| Acts on its own / schedules | ✅ | ✅ (with n8n or OpenClaw rules) |
| Runs as company account | ✅ | ⚠️ Runs as a bot you own |
| Polished, zero-maintenance | ✅ | ⚠️ You run the box |
| **Cost** | **Pay per task, Team/Enterprise only** | **$0–$5/month** |

**What you give up:** Anthropic's hand-holding and automatic spend caps. You're the one who restarts it if it ever stops.

**What you gain:** you stop renting something you can easily own. No per-task meter, no plan upgrade, no surprise bill.

**Bottom line:** Claude Tag is worth it for big companies that *refuse* to touch any setup. If you're a creator, freelancer, or small team, this free version does the same job.

---

## Part 5 — If something breaks (quick fixes)

| Problem | Fix |
|---|---|
| Bot doesn't reply | Make sure the Terminal still says "connected," and that you **invited** the bot to that channel. |
| "Invalid token" error | You pasted the wrong secret. `xoxb-` = Bot token, `xapp-` = App token, `AIza` = Gemini key. Re-check each. |
| "Quota" or "rate limit" from Gemini | You hit the daily free limit. Wait, or add a backup Groq/OpenRouter key (Step 1 note) and switch to it. |
| `npm: command not found` | Node.js didn't install. Redo Step 3 #2 and reopen the Terminal. |
| Bot stops when laptop sleeps | That's normal — do Step 5 to move it to an always-on server. |

---

## Part 6 — The no-code path (n8n) — zero typing of commands

Hate the Terminal? Use **n8n** instead — you build the bot by dragging boxes and connecting them with lines, like a flowchart.

1. Go to **n8n.io** → start a **free** account (or self-host it later for $0).
2. Click **"New Workflow."**
3. Add a **Slack Trigger** box → connect your Slack app (it walks you through it) → set it to fire on **"app_mention."**
4. Add a **Google Gemini** (or "AI Agent") box → paste your Gemini key → feed it the Slack message text.
5. Add a **Slack → Send Message** box → send Gemini's answer back to the channel.
6. Click **"Active."** Done — tag your bot in Slack and it answers.

Same result, no commands. Pick whichever path felt less scary.

---

## Sources

- [What is Claude Tag (Anthropic)](https://support.claude.com/en/articles/15594475-what-is-claude-tag)
- [Google AI Studio — free Gemini keys](https://aistudio.google.com)
- [Slack — create your app](https://api.slack.com/apps)
- [n8n — no-code automation](https://n8n.io)
- [open-source-slack-ai (GitHub)](https://github.com/meetbryce/open-source-slack-ai)
- [Free LLM APIs compared (OpenRouter)](https://openrouter.ai/blog/tutorials/free-llm-apis-compared/)
- [awesome-free-llm-apis (GitHub)](https://github.com/mnfst/awesome-free-llm-apis)

---

*Guide by [@techwithgul](https://www.instagram.com/techwithgul.ai) — the free way to do what they charge for. Stuck on a step? Comment **TAG** on the reel and I'll help.*
