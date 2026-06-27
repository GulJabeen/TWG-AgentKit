---
name: higgsfield-product-ads
description: >
  Make smart, cost-friendly product ads with Higgsfield — built for solo founders,
  small brands, and creators who want a few HIGH-IMPACT ads, not a 200-video factory.
  Budget-first: every run starts by asking the user's budget, then picks the cheapest
  Higgsfield model/preset/resolution that still wins, shows a PRE-FLIGHT credit + USD
  cost estimate the user approves BEFORE anything generates, and ends with a real
  cost-per-ad report vs traditional production. Defaults to UGC-style ads (10× higher
  converting than polished) and only spends on cinematic when the product's margin
  justifies it. Walks brief → concept → cost estimate → generate (quality-check 1 first)
  → assets → cost report. Button-driven UX. Trigger on a product image/URL + an ad
  request, or phrases like 'make a product ad', 'create an ad', 'advertise this',
  'turn this into an ad', 'UGC ad', 'cheapest way to make an ad', 'product ad on a budget',
  'how much will this ad cost', 'make me a TikTok/Reels/Meta ad'.
---

# Higgsfield Product Ads — the cost-smart way

**Who this is for.** A solo founder, small e-commerce store, or creator who wants a few
product ads that actually convert — without burning a month's credits or a freelancer
budget. NOT a bulk content factory. The default is **1–5 sharp ads**, made smart, not 200
made cheap. (If the user explicitly wants high volume, you can scale — but never assume it.)

**The one rule that governs everything: spend on purpose.**
Before a single credit is spent, the user sees an estimate and clicks approve. After the run,
they see exactly what it cost and what it would have cost the old way. No surprise credit
drains. Iteration — not generation — is the real money pit (most creators re-roll 3–5× before
a keeper), so this skill is built to get a winner in as few generations as possible:
plan the shot well, quality-check ONE before committing a batch, and reuse winners.

---

## THE MONEY MODEL — read this, it's the whole point

Higgsfield bills in **credits**. Different models cost wildly different amounts, so model
choice is the #1 cost decision. **Always pull live numbers at runtime** (`balance` +
`show_plans_and_credits`) — the table below is a 2026 reference snapshot that drifts.

### Reference cost ladder (verify live — never quote as gospel)

| Tier | Model | ~Credits / clip | Best for | When to use |
|---|---|---:|---|---|
| 💚 Cheapest | `grok_video`, `seedance_2_0` (`mode:"fast"`, 480/720p) | ~5–10 | Drafts, hook tests, simple motion | Testing concepts, tight budgets |
| 💛 Default | **`marketing_studio_video`** ("DTC Ads") 720p | ~15–30 | **Real UGC product ads** | The workhorse — start here |
| 🧡 Premium | `seedance_2_0` (`std`, 1080p), Kling 3.0 | ~30–50 | Multi-SKU, consistent identity | When one model can't hold the product still |
| ❤️ Expensive | Veo 3.1, Sora 2, Cinema Studio | ~40–70+ | Cinematic hero spots, luxury | ONLY when product margin/AOV justifies it |

### Plan & credit-price reference (2026 snapshot — confirm live)

- Plans: **Starter ~$15/mo · Plus ~$49/mo · Ultra ~$129/mo · Business ~$89/seat/mo** (annual is cheaper). Unlimited day-passes exist (7-day / 365-day) — surface via `show_plans_and_credits`.
- Top-up packs: **~$5 per 100 credits (~$0.05/credit)** — note these **expire ~90 days**, so don't over-buy.
- Rough cost-per-usable-ad **after the 3–5× iteration most people hit**:
  - Cheap models: **~$0.60–1.00 / usable clip**
  - Marketing Studio UGC: **~$1–3 / usable ad**
  - Veo/Sora cinematic: **~$3.50–9.50 / usable clip**

### The 6 cost levers (pull these to cut spend without killing quality)

1. **Model** — biggest lever. Default to Marketing Studio; drop to fast/cheap for tests; climb to cinematic only when justified.
2. **Resolution** — generate at **720p** to approve, upscale only the winner to 1080p. Never draft at max res.
3. **Quality-check ONE first** — generate 1 clip, look, THEN commit the batch. This alone kills most wasted spend.
4. **Audio** — `generate_audio` adds cost; keep it on for UGC/ASMR where it earns its keep, off for silent B-roll.
5. **Reuse the winner** — an `ad_reference` from a clip that worked recreates its structure cheaply instead of re-inventing.
6. **Duration** — Marketing Studio is 12–15s; don't pay for length the platform crops anyway. Hook lives in the first 3s.

> **HARD GATE:** Never call a `generate_*` tool before the user has seen and approved a
> pre-flight cost estimate (see Stage 3). This is the core promise of the skill.

---

## UX RULES (keep these — they make it usable by non-technical people)

- **Button-driven.** Every clarifying question is an `AskUserQuestion` with 2–4 concrete
  buttons + a smart default labeled "(Recommended)". The only non-button inputs are product
  image upload and URL paste (both click-based). Never make the user type a command.
- **Plain language, no internals.** Don't narrate MCP tool names, UUIDs, slug tables,
  "uploading via media_confirm", etc. Those run silently. Send ONE friendly stage banner when
  a stage starts. If the user asks "how does it work," then explain.
- **Show money in plain terms.** Always translate credits → approximate USD and → "what this
  would've cost a freelancer/studio." That framing is why they'll trust the tool.
- **No-pause rule.** Bundle clarifying questions into a single `AskUserQuestion` call.

Stage banners (use these):

| Stage | Banner |
|---|---|
| 1 | **🎯 Stage 1: Ad strategy — starting now.** I'm reading your product and the angle most likely to convert, then proposing the exact ad(s) to make. |
| 2 | **🧮 Stage 2: Pick the cost-smart setup — starting now.** I'm matching your budget to the cheapest Higgsfield setup that still wins. |
| 3 | **💵 Cost check — your approval needed.** Here's exactly what this will cost in credits and dollars before I generate anything. |
| 4 | **🎬 Stage 4: Making your ad — starting now.** I'll make one first so you can check quality, then finish the rest only if you're happy. |
| 5 | **💰 Stage 5: What it cost — starting now.** I'm showing your real spend vs what this would've cost the traditional way. |

---

## ONBOARDING — one message, all buttons (run first, no pauses)

Send ONE `AskUserQuestion` covering A + B + C, plus the product-attach prompt, in the SAME
message. If a product image/URL is already attached, skip D.

**A — Connection check.** "Yes — Higgsfield connected" · "Not yet — I'll connect now" · "Just plan it for me (no generating yet)"

**B — Budget (the most important question).** Frame in dollars; map to credits silently.
- "Tiny — keep it under ~$5 / ~100 credits"
- "Small — around ~$15 / ~300 credits (Recommended)"
- "Standard — around ~$50 / ~1,000 credits"
- *(Other → user types a number or credit count)*

Store as `[BUDGET]`. Everything downstream (model tier, how many ads, resolution) is fit to
this number. If the user is on an **Unlimited** plan, note that volume isn't credit-limited and
re-frame the budget question as "how many ads do you want?" instead.

**C — Goal / where it runs.** (multiSelect) "TikTok" · "Instagram Reels" · "Meta Ads" ·
"Just need the video file". Drives aspect ratio (default **9:16**) and authenticity level.

**D — The product.** "Attach your product image OR paste a product URL — that's all I need."
If an image is attached at trigger, skip D.

After the user answers, go straight into Stage 1 — no extra confirmation.

---

## STAGE 1 — Ad strategy & concept (lightweight, smart, not a 200-idea dump)

> Goal: propose the **smallest number of ads that will actually move the needle**, each with a
> clear angle. For most users that's **1 hero ad + 1–2 variations to test the hook.**

### Step 1 — Read the product (silent auto-detect)

From the image and/or URL (`web_fetch` the URL if given; register via `show_marketing_studio`):
- category, key SKUs/variants, packaging colors, demographic vibe, price/positioning cues.
- Infer **margin tier**: cheap impulse buy → stay UGC/cheap. High-AOV/luxury → cinematic may pay off.

Announce as ONE plain line, not a question: *"Got it — a [niche] aimed at [audience]. For this
kind of product, [UGC-style / a polished hero] ads convert best, so that's where I'll point the budget."*

### Step 2 — Pick the format by what converts (and what's producible)

Default hierarchy (UGC-first — it converts ~10× polished and is the cheapest to make):

1. **UGC product ad** — a real-feeling person + product, problem→solution in 9–15s. *Default.*
2. **Product review** — talking-head honesty, "I tried this." High mid-funnel trust.
3. **Unboxing / ASMR** — premium reveal or sound-led close-ups (great for save/retarget).
4. **Hyper Motion / cinematic hero** — kinetic pour/spin or polished spot. **Only** when margin tier is high.

Map each chosen ad to a Marketing Studio preset (see Appendix). One strong concept per format
the product supports — don't pad. For each proposed ad, give:

```
[Title] — [format]
- Hook (first 3s): [the scroll-stopper, said in plain words]
- What happens: [≤2 sentence scene]
- Why it converts: [tie to the product + a real 2026 pattern]
- Preset: [slug] · Duration: [12–15s] · Aspect: [9:16 default] · Audio: [on/off]
- Est. cost: [pull from Stage 2 ladder — credits + ~USD]
```

### Step 3 (optional, only if it helps) — quick trend sanity check

If the niche is unfamiliar, run **1–2** web searches (`[niche] viral ad hook [month year]`,
`[niche] UGC ad examples`) — NOT eight. Cite only what you actually use. Don't burn time/tokens
researching a product whose winning angle is obvious.

### Step 4 — Approve the plan (buttons)

Present the concept(s) with the per-ad cost, then `AskUserQuestion`:
> "Here's the plan and what it'll cost. Next?"
> - "Looks good — set up the cheapest way to make it (Recommended)"
> - "Make it cheaper / fewer ads"
> - "Go more premium — I have margin for it"
> - "Change the hook or angle"

---

## STAGE 2 — Fit the setup to the budget (the cost-smart engine)

> Goal: choose **model + resolution + count + audio** so the whole run fits inside `[BUDGET]`
> with room for one re-roll. This is where the skill earns its name.

1. **Pull live cost + balance.** `balance` for available credits; `models_explore(action='get')`
   on candidate models for live constraints. Never guess if you can fetch.
2. **Pick the model tier** from the ladder by matching `[BUDGET]` and margin tier:
   - Tiny budget / testing → cheap tier (Seedance `fast` / Grok), 480–720p.
   - Standard UGC ad → **Marketing Studio 720p** (default).
   - High margin + premium goal → cinematic tier, but cap the count.
3. **Compute the count.** `ads_affordable = floor((BUDGET_credits × 0.7) / cost_per_clip)` —
   the 0.7 reserves ~30% for one quality re-roll. Never plan a run with zero re-roll headroom.
4. **Default resolution 720p for approval; upscale only the winner** to 1080p (`upscale_video`).
5. **Set audio** per format (on for UGC/ASMR/review, off for silent hero B-roll).

Output a tiny plain-language setup summary — model, count, resolution, audio — and roll
straight into the Stage 3 cost gate (no separate approval here; the gate is the approval).

---

## STAGE 3 — PRE-FLIGHT COST GATE (the hard stop — never skip)

> ⚠️ This is the skill's core safety promise. **No `generate_*` call happens before the user
> approves this estimate.**

Show a compact estimate card:

```
💵 Before I generate anything:

  • What you'll get: [N] × [format] ad(s), [resolution], [aspect], audio [on/off]
  • Model: [name]  (~[X] credits each)
  • Estimated cost: ~[N×X] credits  ≈  $[usd]   (you have [balance] credits)
  • I reserve ~30% for one quality re-roll, so worst case ~[with_reroll] credits
  • Traditional cost for the same thing: ~$[low]–$[high] (a freelancer/UGC creator)
```

Then `AskUserQuestion`:
> "Good to go?"
> - "Yes — make 1 first as a quality check (Recommended)"
> - "Yes — generate all [N] now"
> - "Cheaper, please — drop resolution / use the budget model"
> - "Hold on — change something"

If the estimate **exceeds the user's balance**, do NOT silently proceed: say so plainly and
offer "Top up credits" (call `show_plans_and_credits` with `intent:'topup'`) or "Make a smaller/cheaper version".

---

## STAGE 4 — Generate (quality-check-first, iteration-disciplined)

> The "make 1 first" path is the default and the single biggest money-saver. Honor it.

### Step 1 — Register the product (silent)
Upload the product image / fetch URL → product UUID via `show_marketing_studio`. Pass it as
`product_ids` on every generation so the real product appears, not a hallucinated one.

### Step 2 — Resolve avatar + hook + setting (silent, UGC family only)
- **Always pass a preset avatar** (`avatar_ids: ['<uuid>']`) so faces stay consistent across an
  ad set — never leave avatars empty (that casts a random face per render). List via
  `show_marketing_studio(action='list', type='avatar')`.
- Resolve `hook_id` / `setting_id` from the picklists (`type='hook'` / `type='setting'`) for the
  chosen scene. These compose the shot; they are NOT caption copy.

### Step 3 — Set `mode` on EVERY call (preset routing — the #1 failure if skipped)
Without an explicit `mode`, Marketing Studio defaults to UGC and rewrites your prompt. Pass the
title-case mode from `presets[].mode`. Watch the slug mismatches:

| Use this `mode` | maps to slug |
|---|---|
| "UGC" | `ugc` |
| "Tutorial" | `ugc_how_to` (NOT `tutorial`) |
| "Unboxing" | `ugc_unboxing` |
| "Hyper Motion" | `product_showcase` (NOT `hyper_motion`) |
| "Product Review" | `product_review` |
| "TV Spot" | `tv_spot` · "Wild Card" | `wild_card` |
| "UGC Virtual Try On" | `ugc_virtual_try_on` · "Pro Virtual Try On" | `virtual_try_on` |

### Step 4 — Build the prompt — ZERO on-screen text
The video must contain **no captions, subtitles, watermarks, or typography**. The caption is
social-post metadata for the upload, NEVER a render instruction.

```
[Scene]. Product: [name + color/packaging/label detail from image].
Style: [UGC: authentic, handheld, natural light · ASMR: intimate close-up, no music, audible handling · cinematic: polished, golden hour].
Negative: no text overlay, no captions, no subtitles, no watermark, no lower-third, no typography. Clean image only.
```

### Step 5 — Generate ONE, then gate the rest
- Generate a single clip at approval resolution. Show it via `job_display`.
- `AskUserQuestion`: "Happy with this one?"
  - "Yes — make the rest" · "Re-roll this one (uses ~[X] more credits)" · "Tweak the prompt" · "Stop here, this is enough"
- Only on "make the rest" do you generate the remaining clips. Track spend; if a re-roll would
  blow the reserved budget, warn before firing.
- **Upscale only keepers** to 1080p with `upscale_video`.

### Step 6 — Optional image assets (only if asked / budget allows)
If the user wants stills too, generate a SMALL pack via `generate_image` (`model:"gpt_image_2"`,
product as reference) — default just 2–4: one social 1:1, one hero 16:9. Estimate cost and gate
it like Stage 3. Don't auto-spew a 20-image pack on a budget run.

### Failure handling
On a failed generation, log which clip failed and offer "Retry / Skip / Stop" buttons. Never
silently eat a charge.

---

## STAGE 5 — What it actually cost (the trust-builder)

After generating, render a short, honest cost report (plain text or a small HTML file in
`/mnt/user-data/outputs/[brand]-ad-cost.html`).

1. **Pull real spend.** `transactions(limit=100)` — sum credits used during this run.
2. **Convert to USD** at the user's plan/top-up rate (disclose the rate; if unknown, show credits only).
3. **Compare to traditional** (2026 industry midpoints — show a low–high range, label as estimates):
   - UGC creator video: **$250–1,500** · Product review: **$300–2,000** · Unboxing: **$300–1,500**
   - Cinematic 15s hero: **$3,000–15,000+** · Social still: **$100–500** · Hero banner: **$1,000–5,000**
4. **Headline the result:** *"You made [N] ad(s) for **~$[X]** instead of **$[low]–$[high]** — and
   in minutes, not weeks."*
5. **Add a cost-per-result line** if they ran ads: spend ÷ ads = **$/ad**, and note that the real
   metric is cost-per-conversion once it's live.

Close with `AskUserQuestion`: "Done — close out (Recommended)" · "Make a variation to test the
hook" · "Top up credits for more" · "Run this for another product".

---

## APPENDIX — Higgsfield Marketing Studio ground truth (keep silent; execute)

**Hard limits (Marketing Studio video):** duration **12–15s** · aspect: auto/21:9/16:9/4:3/1:1/3:4/9:16 · resolution 480p/720p/1080p · `generate_audio` optional (default on) · reference: product image (always), avatar image (UGC family).

**Presets:** `ugc` · `tutorial` · `ugc_unboxing` · `hyper_motion` · `product_review` · `tv_spot` · `wild_card` · `ugc_virtual_try_on` · `virtual_try_on`.
**Hook/setting picklists apply to:** UGC, Tutorial, Unboxing, Product Review, UGC Virtual Try On only. Resolve UUIDs live via `show_marketing_studio(action='list', type='hook'|'setting')`.

**Preset relevance by product (default; user can override):**
- Beverage/food → `ugc` · `product_review` · `hyper_motion` (+`tutorial` if recipe-able, +`ugc_unboxing` if gift/multi-SKU)
- Beauty/skincare → `ugc` · `product_review` · `tutorial` · `ugc_unboxing`
- Apparel/eyewear/jewelry → `ugc` · `product_review` · `ugc_virtual_try_on` / `virtual_try_on`
- Electronics/home → `ugc` · `product_review` · `tutorial` · `ugc_unboxing`
- Software/app/service → `ugc` · `product_review` · `tutorial` · `tv_spot` (no Hyper Motion — no physical hero)
- Premium/luxury → `ugc` · `product_review` · `ugc_unboxing` · `hyper_motion` · `tv_spot`

**Marketing Studio CANNOT:** clips >15s · reliable non-human lip-sync · multi-character consistent dialogue across cuts · split-screen/multi-setting single output · off-picklist hook/setting. For those, escape to **Seedance 2.0** (reference/multi-SKU/identity) · **Veo 3.1 / Sora 2** (cinematic+audio) · **Kling 3.0** (multi-shot) — but escaping costs more, so only when the ad genuinely needs it.

**ASMR** is a style, not a preset: `ugc` + `generate_audio:true`, intimate setting (Kitchen/Bathroom/Bedroom), `hook_id` none, close-up product-handling prompt.

**Ad-reference reuse (cheap win):** if a generated clip works, create an `ad_reference` from it
and pass `ad_reference_id` to recreate its structure for a variation — pass `product_ids` /
`avatar_ids` explicitly (they are NOT auto-pulled). Mutually exclusive with `hook_id`/`setting_id`.

---

## GUIDELINES (the non-negotiables)

- **Cost gate is mandatory.** No generation before an approved Stage 3 estimate. Ever.
- **Budget-first.** Every run is sized to fit `[BUDGET]` with ~30% re-roll headroom.
- **Quality-check one before a batch.** The default path, and the biggest money-saver.
- **UGC-first.** It converts ~10× polished and costs the least — go cinematic only when product margin justifies it.
- **720p to approve, 1080p only for keepers.** Never draft at max resolution.
- **Few sharp ads > many cheap ones.** Default 1–5, scale only on explicit request.
- **No on-screen text in the video.** Caption is upload metadata only.
- **Button-driven, plain language, no internals narrated.**
- **Always pull live credit costs** (`balance`, `models_explore`, `show_plans_and_credits`) — the tables here are drifting reference snapshots, not quotes.
- **Translate everything to dollars + "vs traditional"** so a non-marketer understands the value.
