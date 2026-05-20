---
name: voice-profile-builder
description: Use when someone wants to build a personal voice profile, voice pack, or writing-style system from their own real writing so an AI can draft in their voice. Use when the goal is AI output that sounds like a specific person and passes AI detection, when starting from a corpus of sent emails or past writing, or when previous voice prompts produced generic AI prose.
---

# Voice Profile Builder

## Overview

Builds a register-aware voice profile from a person's own writing corpus, ideally writing produced before late November 2022 when ChatGPT shipped. The output is a multi-file bundle that future AI sessions load to write in that person's voice without producing generic AI prose.

Core principle: a clean source beats a clever prompt. Most voice tools humanize the output. This one fixes the input by using a corpus that was never contaminated by AI in the first place.

## When to use

- The person wants AI to draft emails, posts, essays, or messages that sound like them
- Generic "write in my voice" prompts keep producing AI slop
- They have, or can assemble, a body of their own pre-AI writing
- They want output that survives AI-detection tools

When NOT to use: third-person writing about the person, technical documentation, or any case where a generic professional voice is fine.

## Inputs

One file: a corpus of the user's own writing, ideally pre-AI (before January 2023 as a safe buffer). Minimum useful size 20,000 words. Sweet spot 80,000+ words across multiple kinds of writing. If they don't have one, walk them through assembling it before proceeding (see Assembling a corpus). If the user has an AI email connector (such as Claude's Gmail connector), prefer it: it can search, pull, and assemble the corpus, and you can run the contamination scan in the same pass.

## Assembling a corpus

Manual path (always works):

1. Search Gmail "Sent" on the user's own address, filtered to before 2023.
2. Keep threads where the user's own writing is clearly theirs, not forwarded or AI-assisted.
3. Strip the other person's words. Keep only the user's.
4. Paste everything into one plain-text or Markdown file. Do not clean it up. Typos, run-ons, and rough phrasing are the signal, not noise.

Faster path (if an AI email connector is available): have the connector search and pull directly, then run the contamination scan inline. AI that retrieves the corpus is fine; the contamination you are avoiding is AI that drafted the words.

Either way, drive coverage by writing type, not recency. Deliberately pull every register: work email, personal email, email to family, emails where the user pushes back, emails where they are excited or celebrating. Width beats polish. A corpus that is 90% one type only writes that type well.

## Workflow

### Stage 1: intake and contamination scan

1. Read the corpus. Report total words, approximate date range, and rough coverage by writing type.
2. Scan for AI contamination. Flag every match for user review, never auto-delete:
   - Bracket placeholders like `[Name]`, `[Your name]`, `[CEO's name]`, `[Company]`
   - Em-dashes
   - "excited to share", "thrilled to announce", "honored to"
   - "leverage" as a verb, "utilize", "synergy", "bandwidth" in the metaphor sense, "circle back", "unpack"
   - "in today's fast-paced", "let's dive in", "here's the thing", "at its core", "in essence", "fundamentally"
   - "however", "moreover", "furthermore", "additionally", "consequently" as paragraph openers
   - "best regards", "warmly", "cheers", "all my best"
   - Repeated three-of-a-kind parallel clauses
3. Show flagged passages to the user. They decide: keep (it is really how they write) or cut (contamination). Never decide for them.

### Stage 2: register sort

Group surviving samples into registers. Default eight, adjust to what the corpus actually contains:

1. Transactional email
2. Customer service / escalation
3. Warm professional / community
4. Family / memory archive
5. Strategy / business / coaching
6. Quick text / peer
7. Leadership / public / social
8. Memoir / narrative

If a register has fewer than 5 samples, mark it "insufficient data" and instruct the future model not to draft in that register without more evidence.

### Stage 3: extract patterns

For each populated register, extract verbatim:

- Greetings and closers, with frequency counts
- Sentence architecture defaults: average sentence length, fragment frequency, paragraph length
- Reached-for phrases and idioms
- Landing lines and short fragments used as kickers
- Frustration escalation pattern, if present
- AI-suspicious-but-real moves: trailing dots, double `??` or `!!`, run-on commas, signature typos, random caps for emphasis

Cross-register identity layer:

- How does the user own mistakes? Verbatim phrases.
- How do they express warmth? Vulnerability? Verbatim phrases.
- What punctuation patterns are consistent?
- What words never appear in the corpus? Absence is signal. If "leverage" never appears in 80k words, it is banned.

### Stage 4: write the bundle

Produce these files in the target directory. Use the user's first name where indicated.

1. `corpus.md`: the cleaned source corpus, sorted into register sections. Header includes source description, cutoff date, total word count, exclusion notes.
2. `01_master_voice_profile.md`: identity layer: core identity (3-5 sentences from Stage 3), non-negotiables (5-10 rules), sentence architecture, diction (reached-for and banned words), emotional range with verbatim anchors, register selection rule, a paste-ready portable AI instruction block.
3. `02_register_cards.md`: one card per populated register: when to use, default structure, typical openers and closers (verbatim), voice rules, what to avoid.
4. `03_prompt_pack.md`: copy-paste prompts: drafting per register, rewriting to remove AI polish, red-team a draft, customer-service escalation, strategy memo, personal memory, public social post.
5. `04_evaluation_checklist.md`: the gate: fast-pass scan list (auto-reject triggers), a 0-2 scorecard across 10 dimensions (register match, opener, specificity, rhythm, punctuation, diction, emotional accuracy, close, fact discipline, read-aloud), interpretation bands (18-20 ship, 15-17 one pass, 11-14 rewrite, 10 or below start over).
6. `05_calibration_examples.md`: one verbatim example per register, pulled from the corpus, with a one-line note on what to copy.
7. `06_style_guide.md`: operational distillation: five non-negotiables, structural rules per register, sentence-level rules, a register table (audience, greeting, tone, closer, sign-off), what the user never does, things they do that read AI-suspicious but are real.
8. `07_lexicon.md`: verbatim phrase bank: greetings, closers, self-correction, frustration escalation, warmth, casual filler, signature typos, punctuation lexicon, sentence kickers, reference phrases. All verbatim. No paraphrasing.
9. `CLAUDE.md`: loader instructions for future sessions: which files to load by purpose, confidence rules when context is missing, the hard rule never to invent quotes, the hard rule no em-dashes if the corpus did not use them.

### Stage 5: verify

Generate one 150-200 word test draft in each populated register. Score each against the evaluation checklist. Surface any category below 1. Iterate the relevant files. Show the final bundle and the test drafts to the user. Tell them to read the test drafts aloud before shipping anything public.

## Hard rules

1. Never invent a quote. Every phrase in the lexicon, calibration examples, or style guide must exist verbatim in the corpus. Grep before writing.
2. Never paraphrase the user's voice into the rules. The rules describe patterns the corpus exhibits, not patterns the model assumes are good.
3. Surface contamination, do not delete it. The user approves every cut.
4. No em-dashes in any output file unless the corpus consistently uses them.
5. If a register has fewer than 5 samples, mark it "insufficient data, draft with caution" and tell future sessions not to use it confidently.
6. Output goes to the user-named directory, default `~/VoicePack/`. Never write into a vault, project, or work directory by default.
7. Never publish the corpus. It is the user's private writing. The bundle is shareable, the corpus is not.

## Common mistakes

| Mistake | Fix |
|---|---|
| Using recent writing as the corpus | Recent writing is already AI-contaminated. Use pre-2023 source where possible. |
| Averaging all registers into one voice | Keep registers separate. The best draft is the user in the right situation, not a blended mean. |
| Inventing plausible-sounding phrases | Every lexicon entry must be grep-verifiable in the corpus. |
| Auto-cutting flagged passages | Flag, then let the user decide. Some flagged moves are genuinely theirs. |
| Drafting confidently in a thin register | Honor the "insufficient data" flag. Tell the user, do not fake it. |

## Done definition

- Bundle exists in the target directory with all 9 files
- Test drafts in every populated register generated and scored 15 or higher on `04_evaluation_checklist.md` (18-20 ships as-is, 15-17 after one light pass)
- User has confirmed at least one test draft reads like them
