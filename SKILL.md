---
name: call-to-linkedin-content
description: "Turn a call recording transcript (client call, sales call, coaching call, podcast) into finished, ready-to-post LinkedIn drafts in your own voice. Guided voice setup on first run (upload a voice doc or a 50-question interview, plus 3 of your real posts), asked once and remembered after. No API keys ever, paste a transcript or point at an exported file, or auto-pull from Fireflies if it's already connected in your Claude account. MANDATORY triggers on: call to linkedin, call to content, transcript to linkedin, turn this call into a post, linkedin from transcript, /call-to-linkedin-content."
---

# Call to LinkedIn Content

Turn a call you've already had into LinkedIn posts you can actually publish. Not a list of ideas, not a summary, finished drafts.

**This skill always reminds you: read every draft before posting. It writes in your voice, you still ship it.**

---

## HARD RULES — NEVER BREAK

1. **Never fabricate.** No invented quotes, numbers, names, or outcomes. If it's not in the transcript, it didn't happen. Missing detail on an angle → drop that angle, don't pad it.
2. **Never use a real client or company name in a draft** unless the user explicitly confirmed it's OK in intake Q2. Default to role-based descriptors: "a client I work with," "a SaaS founder on the call."
3. **Never the em dash.** Never bold. Never stacked negatives ("No X. No Y. No Z."). Never "Here's the thing" / "Let's dive in" / "In today's fast-paced world."
4. **Hook ≤ 8 words. Body 120-300 words preferred, 400 hard max.**
5. **Every draft must trace to a specific, concrete transcript detail** — a real quote, number, or moment. A draft that could've been written without reading the transcript is a failed draft, full stop.
6. **One file write per run.** Saves to `./outputs/` in the current working directory, never inside the skill's own installed folder.

---

## STEP 0 — LOAD (every run)

Self-contained. Everything loads from this skill folder. No external dependencies, no API keys.

### Always-load

- `craft-rules.md` — LinkedIn post craft rules
- `voice-template.md` — the user's voice (check `filled_in:` field)
- `voice-reference.md` — fallback voice, used only until voice setup is complete
- `framework.md` — the mining/drafting method
- `intake-questions.md` — one-time setup questions plus the every-run confirm line

### Integrity check

Verify each always-load file exists and is non-empty (>200 bytes). If anything is missing, stop and report which file, the recipient should restore it from the original giveaway zip.

---

## STEP 1 — VOICE SETUP (mandatory, once)

Read `voice-template.md`'s `filled_in:` field.

**If `true`:** voice setup is already done, skip to Step 2.

**If `false`:** this is a first run (or the user hasn't finished setup yet). Present the choice explicitly, don't fall back silently:

> "Before I draft anything, let's set up your voice. Two options:
> 1. Paste or point me at a voice/style document you already have.
> 2. I'll interview you, about 50 questions, and build one from your answers.
>
> Either way, I'll also need 3 LinkedIn posts you've actually written, that's the most important part."

- **Option A:** parse the pasted/pointed-to document directly into `voice-template.md`'s sections.
- **Option B:** walk `voice-interview-questions.md`, one question (or small cluster) at a time. The `(core)` tags in that file are for you to know which questions matter most, never say the word "core" to the user. If they're short on time, say it plainly: "if you're short on time, let's start with the most important ones and skip the smaller detail questions." Assemble answers into `voice-template.md`.
- **Either path, always:** collect 3 real LinkedIn posts for Section 9. This is not optional flavor, it's the primary style-match signal used during drafting.

**Also, in this same one-time pass**, capture the call defaults (Section 11 of `voice-template.md`) so they never need to be asked again on future runs:

> "A couple of standing preferences while we're at it, so I don't have to ask every time: should I always anonymize real names and companies by default? Any people or companies that are always off-limits, no matter what's said on a call? And how many drafts do you usually want, 3 unless you say otherwise?"

Show the filled-in `voice-template.md` back to the user, including these defaults, then flip `filled_in: true` and confirm.

**If the user wants to skip voice setup for now:** proceed using `voice-reference.md` as fallback, inject `[VOICE NEEDS CUSTOMIZING]` flags into every draft, and offer again at the end of the run: "Want to set up your own voice before your next run? Takes a few minutes."

---

## STEP 2 — GET THE TRANSCRIPT

**First, check if Fireflies is connected** (Fireflies is the only note-taker with an official Claude connector, this only applies to Fireflies, nothing else has this option):

- If a Fireflies tool is available, offer: "I can pull your most recent Fireflies transcript automatically, or you can paste one from anywhere. Which do you want?" If they want the automatic pull, fetch the most recent transcript and confirm the title/date before proceeding, they can still say "no, a different one" and paste instead.
- If no Fireflies tool is available, offer to walk them through connecting it: "Want me to help you connect Fireflies for one-click pulls next time? Go to claude.ai → Settings → Connectors → Fireflies → Connect. Once that's done, come back and I'll pull it automatically." If they say yes, wait for them to confirm they've connected it, then retry the check. If they say no, or they're not using Fireflies, move straight to paste/file.
- **For every other note-taker** (Otter, Grain, Fathom, Zoom, Read.ai, anything else): there is no live connect option, Claude has no official connector for these. Don't offer one. Go straight to paste/file.

**Paste or file, always available:**

> "Paste the transcript, or give me the path to a `.txt` / `.md` / `.docx` file you've already exported. (See the README if you're not sure how to get one from your note-taker.)"

If the pasted text is under ~500 words, warn there may not be enough raw material for a full batch of distinct angles, ask if they want to proceed anyway.

---

## STEP 3 — INTAKE

**Whose call, always asked fresh** (this genuinely changes call to call): "Whose call is this, and what's your role in it?" Client / sales / internal / podcast, determines which angle types make sense.

**Everything else, defaults from `voice-template.md` Section 11, one-line confirm instead of fresh questions:**

> "Same as usual — anonymize names, {any standing off-limits list}, {default_draft_count} drafts — or anything different for this one?"

If they say "same," proceed with the saved defaults. If they flag something different (a specific name that's OK to use this time, a different draft count), use that for this run only, the saved defaults don't change unless they explicitly ask to update them.

See `intake-questions.md` for the full first-run version of these questions (used once, during Step 1's setup pass) and the confirm-only version used on every run after.

**Exception:** on the very first content-run immediately after Step 1 just set these defaults, skip the confirm question, it would just be re-asking what was answered thirty seconds ago. Only start confirming from the second run onward.

---

## STEP 4 — MINE THE TRANSCRIPT

Per `framework.md`: read the full transcript for emotional moments, concrete details, quotable lines, tension/contrast, and turning points. Produce up to 10 candidate angles, each tagged with a content type (personal story / contrarian take / lesson / case study / behind-the-scenes) and a rough hook idea.

Ideas come only from the transcript. Never blend in outside knowledge or generic advice about the topic.

---

## STEP 5 — SHOW ANGLES, RECOMMEND TOP N

Print the full mined list (1-2 lines each). Mark the recommended subset (default 3, per Step 3's answer) chosen for content-type diversity and specificity, least generic first cut.

Ask:

> "Draft these {N}? Pick different ones, say 'all', or name numbers."

Never silently auto-picks without showing the full list first.

---

## STEP 6 — DRAFT

For each selected angle, write one finished, ready-to-post draft using `craft-rules.md` and the active voice (`voice-template.md` if `filled_in: true`, else `voice-reference.md` with `[VOICE NEEDS CUSTOMIZING]` flags).

**Silent self-check before showing anything** (fix in place, don't narrate the checking):

- Hook ≤ 8 words?
- 120-300 words, 400 hard max?
- No banned words, no em dash, no bold?
- Talks TO the reader ("you") for 50%+ of the post?
- One personality/specific-detail moment, a real quote, number, or scene from the transcript?
- Ends on a question or soft CTA, never "book a call" or fake scarcity?
- Traces to a specific transcript detail, not generic filler?
- No unapproved real client or company name?

**Then, once all drafts in the batch exist, run one more pass across the whole batch:** does any draft share a core line or insight with another draft in this batch (per `craft-rules.md`'s batch rule)? If two drafts converge on the same takeaway, rewrite one around a different mined angle before presenting anything. Never present a batch where two drafts feel interchangeable.

If any check fails, rewrite before presenting.

**Build the gate-check block** (see Step 7) from the results of these checks, this is the one place the checking work becomes visible, everything else about Step 6 stays silent.

---

## STEP 7 — PRESENT

Show a gate-check block first, then all drafts, using the `html-template.html` shell.

**Gate-check block:** one line per check, ✓ if it held across every draft in the batch, ✗ with a one-line reason if a check ever failed and had to be rewritten (never hide a rewrite, show it happened):

```
✓ No fabricated details
✓ No leaked names
✓ No repeated lines across drafts
✓ Hook ≤ 8 words, all drafts
```

This is the only place Step 6's checks become visible. Don't narrate individual rewrites in chat, just report the final state here.

**Then the drafts:** draft number, source angle, hook, word count, full text.

---

## STEP 8 — REVISION PASS

Ask:

> "Tell me what to change on any draft, or say 'ship it.' Up to 5 revision rounds."

State which draft you're rewriting before rewriting it.

---

## STEP 9 — SAVE

On "ship it":

1. **Save location:** `./outputs/` in the current working directory. Create it if missing. Never save inside the installed skill's own folder (resolves to a hidden system path the user can't find). If not writable, fall back to `~/Downloads/`, no asking.
2. **Filename:** `call-to-linkedin-{slug}-{YYYY-MM-DD}.md`, slug from intake Q1, lowercase, dashes, max 40 chars.
3. **Versioning:** if the filename exists, append `-v2`, `-v3`, never overwrite.
4. **Content:** all finished drafts, plus a short "other angles surfaced, not drafted" list at the bottom (single run only, not a persistent cross-session file).
5. **Report:** full path, word counts per draft, voice status (custom / fallback).

---

## PRESENTATION RULES

- Every response starts with `[Step X/9]`.
- Keep messages short, updates not narration.
- Don't announce file loads.
- Do announce: Step 4's mined angle list, Step 5's recommendation, Step 7's gate-check block, Step 9's save report.

---

## What this skill does NOT do

- Does not invent quotes, numbers, or outcomes. Missing material means fewer angles, not padded ones.
- Does not store or ask for an API key from any note-taker. If Fireflies is already connected in your own Claude account, it can pull your latest transcript automatically, that's the one exception. Every other note-taker: you bring the transcript, paste or file.
- Does not write emails, landing pages, or lead magnets. LinkedIn posts only.
- Does not track to-dos or action items from the call. Content only.
- Does not auto-post to LinkedIn. Saves drafts locally. Posting is on you.
- Does not promise virality. It gives your real material the best shot at sounding like you.

---

## File map

| File | Purpose |
|---|---|
| `SKILL.md` | This file, workflow logic |
| `framework.md` | The mining/drafting method |
| `craft-rules.md` | LinkedIn post craft rules |
| `intake-questions.md` | Setup questions (once) plus the every-run confirm line |
| `voice-interview-questions.md` | 50-question voice interview (used if the user picks the interview path) |
| `voice-template.md` | Your voice, filled in via upload, interview, or direct edit |
| `voice-reference.md` | Fallback voice, used only until your own voice setup is complete |
| `html-template.html` | Output shell (plain text/Markdown draft layout) |
| `README.md` | Getting-started guide, including how to get a transcript |
| `outputs/` | Where finished drafts land |
| `templates/` | Optional, your own saved examples |

Everything self-contained. Zero external dependencies.
