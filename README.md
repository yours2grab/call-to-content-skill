# Call to Content

Turn a call you've already had into an article brief, real quotes with context, structured why-then-steps, ready to hand to an article writer. Paste a transcript, answer a couple of quick questions, get that back in your own voice. Want short, finished LinkedIn drafts instead? Just ask.

This is the exact system used to turn client calls into content, repackaged as a Claude Code skill so you can run it yourself.

---

## Who this is for

Course creators, coaches, consultants, and cohort/workshop organizers who are already having calls (client calls, sales calls, coaching sessions) and want to stop losing the good material in them:
- Course and cohort creators
- Coaches and consultants
- Service providers who sell on calls
- Anyone who has recorded conversations sitting around unused

---

## What you get

1. **The mining/drafting method** ([framework.md](framework.md)) — how a transcript becomes an article brief (or short posts, on request), not just a list of ideas.
2. **LinkedIn craft rules** ([craft-rules.md](craft-rules.md)) — the rules that separate a post that gets read from a post that gets scrolled past, used for the short-draft mode.
3. **Guided voice setup** ([voice-template.md](voice-template.md), [voice-interview-questions.md](voice-interview-questions.md)) — upload your own voice doc, or answer a 50-question interview, plus 3 real posts you've written. The skill writes in your voice, not a generic one.
4. **A bundled fallback voice** ([voice-reference.md](voice-reference.md)) — works out of the box before you've done your own setup, and doubles as an example of what a filled-in voice file looks like.
5. **The skill itself** ([SKILL.md](SKILL.md)) — the workflow that ties it all together.

---

## Quick start

### 1. Install the skill

Drop this entire folder into your Claude Code skills directory:

- **macOS:** `~/.claude/skills/call-to-content/`
- **Or per-project:** `<your-project>/.claude/skills/call-to-content/`

Verify the structure looks like this:

```
call-to-content/
  SKILL.md
  README.md
  framework.md
  craft-rules.md
  intake-questions.md
  voice-interview-questions.md
  voice-template.md
  voice-reference.md
  html-template.html
  outputs/      (generated drafts land here)
  templates/    (empty, for your own examples)
```

### 2. Get a transcript

**If you use Fireflies:** the skill can pull your most recent transcript automatically, no copy-paste needed. If Fireflies isn't connected yet, the skill walks you through it, one-time setup at claude.ai → Settings → Connectors → Fireflies → Connect.

**Every other note-taker** (Otter, Grain, Fathom, Zoom, Read.ai, anything else): there's no live connect option, Claude doesn't have an official connector for these. Paste the text or point at an exported file instead, still no API key, no login screen inside the skill itself. Common sources:

- **Fireflies** — open the meeting → Transcript tab → Export/Download as `.txt`, or copy the text directly.
- **Otter.ai** — open the recording → "···" menu → Export → Export Text file, or copy the conversation.
- **Grain** — open the recording → Transcript panel → Export → Download transcript.
- **Fathom** — open the call → Summary + Transcript → Share/Export, or copy the text.
- **Zoom** — Zoom web portal → Recordings → Audio Transcript → download `.vtt`/`.txt`, or open the AI Companion summary and copy the transcript.
- **Google Meet, Read.ai, or other bots** — same pattern, look for "Transcript" or "Export."
- **No note-taker at all** — record with a phone voice memo, run it through any free transcription tool, or paste a rough manual recap. More raw dialogue (real quotes) makes better drafts than a tidy summary.

You can either paste the raw text into the chat, or point the skill at a local `.txt` / `.md` / `.docx` file you've already exported.

### 3. Run the skill

In Claude Code, type:

```
/call-to-content
```

or just describe what you want:

```
"Turn this call into LinkedIn posts"
"I have a client call I want to turn into content"
"call to content"
```

### 4. Set up once (first run only)

The skill walks you through this before drafting anything, and only ever asks once: upload a voice doc you already have, or answer a guided interview (about 50 questions, if you're short on time you can start with the most important ones), plus 3 LinkedIn posts you've actually written, that's the single most important input. Same pass also sets your standing defaults, whether to anonymize names by default, anyone always off-limits, how many drafts you usually want.

Skip voice setup and the skill falls back to a generic voice with `[VOICE NEEDS CUSTOMIZING]` flags on every draft. It works, but your real voice always outperforms the fallback.

### 5. Every run after that

Just: whose call is this and what's your role (the one thing that genuinely changes call to call), then a one-line confirm of your saved defaults ("same as usual, or anything different this time?"). No re-answering the same setup questions.

### 6. Review the mined angles

The skill mines the transcript for real moments (stories, contrarian takes, lessons, case studies, how-tos) and shows you the full list before writing anything. Confirm the recommended picks, or choose your own.

### 7. Review the brief, revise, ship

By default you get an article brief: a working angle, a why section with real quotes and context, a steps section with real quotes and context, and any extra material mined but not used. Not a finished post, raw material for an article. Tell the skill what to change, or say "ship it." Up to 5 revision rounds.

Want finished, ready-to-post LinkedIn drafts instead? Say so, "give me short posts instead," and you'll get those instead of the brief.

### 8. Ship it

On "ship it," the skill saves to **`outputs/`** inside the skill folder and reports the path and voice status.

Filename pattern: `article-brief-{slug}-{YYYY-MM-DD}.md` for the default brief, or `call-to-content-{slug}-{YYYY-MM-DD}.md` for short drafts. Re-runs append `-v2`, `-v3`, never overwrite.

---

## The hard rules

The skill enforces these. They are not optional.

1. **Never fabricates.** No invented quotes, numbers, names, or outcomes. If it's not in the transcript, it's not in the draft.
2. **Never leaks a real client or company name** unless you explicitly said it was fine in intake.
3. **Every quote and step traces to a specific transcript detail.** Content that could've been written without the call is a failed output.
4. **No em dashes, no bold, no stacked negatives, no LinkedIn "thought leader" clichés** (short-draft mode).
5. **You still ship it.** This is a brief or a set of drafts, not a finished, published piece. Read it before using it.

---

## What this skill is NOT

- It's not a live integration for most note-takers. No API keys, ever. Fireflies is the one exception, if it's already connected in your own Claude account, the skill can pull your latest transcript automatically. Everything else, you bring the transcript.
- It's not a content calendar or scheduler. It hands you a brief or drafts, you post.
- It's not an email or landing-page generator. LinkedIn content only.
- It doesn't track to-dos or action items from the call. Content only.
- It's not "publish and forget." The output is raw material or a draft. You still write and ship the real thing.

---

## Tips for the best results

- **Do your voice setup before your first real run**, even if it's imperfect.
- **Bring real dialogue, not a tidy summary.** A rough transcript with actual quotes beats a polished recap.
- **Don't skip the intake questions.** The clearer the answers, the sharper the angle recommendations.
- **Read every draft aloud** before posting. If you stumble, rewrite.

---

## Credits

Built as a Claude Code skill for free distribution, sharing the same call-to-content system used internally to turn real conversations into real LinkedIn posts.

If it helps you ship content that actually sounds like you, share what you learned. Pass it on.

---

## License

Use it. Share it. Modify it. Don't sell it as your own.
