# Voice Template — Your LinkedIn Voice

This is where your voice lives. The skill reads it every run and writes drafts that sound like you, not like a generic AI.

You fill this in ONE of two ways (both covered in Step 1 of the skill, don't fill this in cold if you'd rather be walked through it):

- **Paste an existing voice/style doc** you already have, and the skill will map it into the sections below for you.
- **Do the guided interview** (`voice-interview-questions.md`, ~50 questions) and the skill assembles your answers into this file.

Either way, **Section 9 (three real LinkedIn posts) is mandatory.** It's the single most important input in this file — more important than every question above it combined.

---

## Status

```
filled_in: false   # the skill flips this to true once setup is complete
voice_owner: [YOUR NAME]
default_anonymize: true          # always use "a client of mine" instead of real names/companies
default_draft_count: 3           # how many drafts per run, unless you say otherwise
```

---

## 1. Voice calibration

Describe your voice in one sentence, using a metaphor or comparison.

**Examples:**
- "A senior consultant giving it to you straight over coffee."
- "A friend texting you what actually happened on the call."
- "The person in the room who says the thing everyone's thinking."

**Your version:**

> _____________________________________________________

---

## 2. Core identity

Who are you when you're writing as you?

- What you do, who you do it for
- The career background that matters
- The "why" behind your work
- What makes you the right person to say this

**Your version:**

> _____________________________________________________

---

## 3. What you believe (that your audience doesn't yet)

The 2-3 strong opinions that show up in your posts.

**Your version:**

- _____________________________________________________
- _____________________________________________________
- _____________________________________________________

---

## 4. Banned words and phrases

Words that make you cringe in copy, beyond the universal defaults already enforced by `craft-rules.md` (leverage, synergy, unlock, empower, revolutionary, game-changing, best-in-class, dive in, etc.)

**Your additions:**

- _____________________________________________________
- _____________________________________________________

---

## 5. Words and phrases you DO use

Your verbal tics. Real things you actually say.

**Your version:**

- _____________________________________________________
- _____________________________________________________
- _____________________________________________________

---

## 6. Hook style

What kind of opening line sounds like you? A blunt claim, a question, a scene, a number?

**Your version:**

> _____________________________________________________

---

## 7. Closer / PS style

How do you end a post? A question, a one-line takeaway, a soft nudge?

**Your version:**

> _____________________________________________________

---

## 8. How you refer to clients and team in stories

When a client, colleague, or specific person shows up in a post, what's your convention? Real first name with role ("a client of mine, a SaaS founder"), fully anonymized ("a client I work with"), or something else?

**Your version:**

> _____________________________________________________

---

## 9. Three real LinkedIn posts (MANDATORY — the most important section)

Paste 3 posts you've actually written and posted. Anything you're proud of, or that did well, works.

The skill absorbs sentence rhythm, word choice, and structure directly from these. Everything above this section is a starting point. This section is the ground truth.

### Post 1

```
[PASTE HERE]
```

### Post 2

```
[PASTE HERE]
```

### Post 3

```
[PASTE HERE]
```

---

## 10. Off-limits topics

Anything you'd never post about.

**Your version:**

- _____________________________________________________

---

## 11. Call defaults (asked once, remembered after)

These used to get asked fresh on every single run. Now they're set once here, during setup, and every future run just confirms them in one line instead of asking from scratch.

**Anonymize real names and companies by default?** (recommended: yes, unless you're comfortable with names appearing in public drafts)

> default_anonymize: _____________________________________________________ (yes / no)

**Always off-limits, regardless of what's said on a call:**

- _____________________________________________________
- _____________________________________________________

**Default number of drafts per run:**

> default_draft_count: _____________________________________________________ (usual default: 3)

---

## How the skill uses this file

1. Checks `filled_in: true` at the top.
2. If **true** → uses your voice, with the 3 posts in Section 9 as the primary style match.
3. If **false** → falls back to `voice-reference.md` (the bundled fallback voice) and adds `[VOICE NEEDS CUSTOMIZING]` notes to every draft, and proactively offers to run voice setup before drafting anything.

Your version beats the fallback every time, even filled in imperfectly.

---

*Last filled in: [DATE]*
