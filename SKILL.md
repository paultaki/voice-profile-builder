---
name: voice-profile-builder
description: Use when someone wants to build a personal voice profile, voice pack, or writing-style system from their own real writing so an AI can draft in their voice. Use when the goal is AI output that sounds like a specific person and passes AI detection, when starting from a corpus of sent emails, past writing, or voice transcripts and dictation, or when previous voice prompts produced generic AI prose.
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

One file: a corpus of the user's own words. Two kinds of source count as clean. Written material is cleanest from before January 2023 (a safe buffer past the late-2022 ChatGPT launch). Spoken or transcribed material (dictation, voice memos, podcast/YouTube/interview transcripts) counts as clean at any date, because speech cannot be AI-edited in the moment; see [docs/SPOKEN-SOURCES.md](docs/SPOKEN-SOURCES.md). Minimum useful size 20,000 words. Sweet spot 80,000+ words across multiple kinds of source. If they don't have one, walk them through assembling it before proceeding (see Assembling a corpus). If the user has an AI email connector (such as Claude's Gmail connector), prefer it for written material: it can search, pull, and assemble the corpus, and you can run the contamination scan in the same pass.

## Assembling a corpus

Manual path (always works):

1. Search Gmail "Sent" on the user's own address, filtered to before 2023.
2. Keep threads where the user's own writing is clearly theirs, not forwarded or AI-assisted.
3. Strip the other person's words. Keep only the user's.
4. Paste everything into one plain-text or Markdown file. Do not clean it up. Typos, run-ons, and rough phrasing are the signal, not noise.

Faster path (if an AI email connector is available): have the connector search and pull directly, then run the contamination scan inline. AI that retrieves the corpus is fine; the contamination you are avoiding is AI that drafted the words.

Either way, drive coverage by writing type, not recency. Deliberately pull every register: work email, personal email, email to family, emails where the user pushes back, emails where they are excited or celebrating. Width beats polish. A corpus that is 90% one type only writes that type well.

Spoken path (often the cleanest source, and the fastest way to volume): pull the user's own speech: dictation they already do (Wispr Flow, OS dictation), transcribed voice memos, or transcripts of their podcasts, talks, and interviews. Strip other speakers, keep only their words. Transcripts are clean at any date, no pre-2023 cutoff. Do not smooth them: fix only obvious transcription garble, never the disfluency. See [docs/SPOKEN-SOURCES.md](docs/SPOKEN-SOURCES.md).

## Workflow

### Stage 1: intake and contamination scan

1. Read the corpus. Report total words (the person's own words, excluding date stamps, source annotations, or headers), approximate date range, the written-vs-spoken split, and rough coverage by writing type.
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
4. For spoken or transcribed sections, the contamination scan rarely fires, since raw speech is not AI-edited. The risk there is the opposite: do not smooth the disfluency. Treat run-ons, fillers, and false starts as signal; fix only clear transcription errors.

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

1. `corpus.md`: the cleaned source corpus, sorted into register sections. Header includes source description, cutoff date, total word count, exclusion notes. If the corpus mixes pre-2023 written material and modern spoken/transcribed material, keep them as two labeled banks (written, spoken) rather than blending; calibration and lexicon entries note which bank they came from. See [docs/SPOKEN-SOURCES.md](docs/SPOKEN-SOURCES.md).
2. `01_master_voice_profile.md`: identity layer: core identity (3-5 sentences from Stage 3), non-negotiables (5-10 rules), sentence architecture, diction (reached-for and banned words), emotional range with verbatim anchors, register selection rule, a paste-ready portable AI instruction block.
3. `02_register_cards.md`: one card per populated register: when to use, default structure, typical openers and closers (verbatim), voice rules, what to avoid.
4. `03_prompt_pack.md`: copy-paste prompts: drafting per register, rewriting to remove AI polish, red-team a draft, customer-service escalation, strategy memo, personal memory, public social post.
5. `04_evaluation_checklist.md`: the gate: fast-pass scan list (auto-reject triggers), a 0-2 scorecard across 10 dimensions (register match, opener, specificity, rhythm, punctuation, diction, emotional accuracy, close, fact discipline, read-aloud), interpretation bands (18-20 ship, 15-17 one pass, 11-14 rewrite, 10 or below start over).
6. `05_calibration_examples.md`: one verbatim example per register, pulled from the corpus, with a one-line note on what to copy.
7. `06_style_guide.md`: operational distillation: five non-negotiables, structural rules per register, sentence-level rules, a register table (audience, greeting, tone, closer, sign-off), what the user never does, things they do that read AI-suspicious but are real.
8. `07_lexicon.md`: verbatim phrase bank: greetings, closers, self-correction, frustration escalation, warmth, casual filler, signature typos, punctuation lexicon, sentence kickers, reference phrases. All verbatim. No paraphrasing.
9. `CLAUDE.md`: loader instructions for future sessions: which files to load by purpose, confidence rules when context is missing, the hard rule never to invent quotes, the hard rule no em-dashes if the corpus did not use them. When the corpus has two banks, tell future sessions to pull from the spoken bank for spoken-cadence registers (casual, thinking-out-loud, narrating work) and the written bank for composed registers (email, formal).

### Stage 5: verify

Generate one 150-200 word test draft in each populated register; keep these inline in your message to the user, they are not bundle files. Score each against the evaluation checklist. Surface any category below 1. Iterate the relevant files. Show the final bundle and the test drafts to the user. Tell them to read the test drafts aloud before shipping anything public.

### Stage 6: source-fidelity audit

This operationalizes the "never invent a quote" rule. Under pressure the drafting model will smooth a quote or reach for a plausible line that is not actually in the corpus. Catch it mechanically.

Audit only material claimed to be the person's own words. Skip the deliberately-absent items: banned-word and "what they never do" lists (their absence from the corpus is the point) and bracketed instruction templates like `Hey [Name],`. Grepping those produces expected misses, not failures. For every remaining verbatim quote in `07_lexicon.md` and `05_calibration_examples.md` (and any quoted phrase in `02_register_cards.md` and `06_style_guide.md`):

1. Take a distinctive 5-10 word substring and grep it against `corpus.md`.
2. Classify the result:
   - **Verbatim, or a trivial transcription fix** (a homophone, a doubled word): keep.
   - **Smoothed** (disfluency removed, grammar normalized, run-on broken, rephrased): the source is in the corpus but it was tidied. Restore the raw text exactly.
   - **Not found** (no match after trying several substrings): drop it. A quote can be a real thing the person once said and still fail this test. If it is not in the vetted corpus, it has not been screened, and it does not ship. Authentic is not the same as in-corpus.
3. Fix or drop every failure, then re-run until clean.

Report the counts: quotes checked, smoothed (restored), not-found (dropped).

## Hard rules

1. Never invent a quote. Every phrase in the lexicon, calibration examples, or style guide must exist verbatim in the corpus. Grep before writing, and run the Stage 6 audit to catch anything smoothed or invented.
2. Never paraphrase the user's voice into the rules. The rules describe patterns the corpus exhibits, not patterns the model assumes are good.
3. Surface contamination, do not delete it. The user approves every cut.
4. No em-dashes in any output file unless the corpus consistently uses them. This covers your own scaffolding prose, headers, and scorecard lines, not just the quoted voice samples. Sweep every bundle file and replace any em-dash with a comma, colon, period, or parentheses before finishing.
5. If a register has fewer than 5 samples, mark it "insufficient data, draft with caution" and tell future sessions not to use it confidently.
6. Output goes to the user-named directory, default `~/VoicePack/`. Never write into a vault, project, or work directory by default.
7. Never publish the corpus. It is the user's private writing. The bundle is shareable, the corpus is not.
8. Never smooth transcribed speech. Disfluency, run-ons, false starts, repetition, and fragments are the voice and the thing that beats AI detectors. On a transcript, fix only obvious transcription garble (a wrong homophone, a doubled word). Do not normalize grammar, break up run-ons, or delete filler.

## Common mistakes

| Mistake | Fix |
|---|---|
| Using recent *written* material as the corpus | Recent writing may be AI-contaminated. Prefer pre-2023 writing. But recent *spoken* material (dictation, transcripts) is clean at any date. See `docs/SPOKEN-SOURCES.md`. |
| Averaging all registers into one voice | Keep registers separate. The best draft is the user in the right situation, not a blended mean. |
| Inventing plausible-sounding phrases | Every lexicon entry must be grep-verifiable in the corpus. The Stage 6 audit enforces this. |
| Smoothing transcribed speech | The disfluency is the fingerprint. Fix only true transcription errors; never normalize grammar or delete filler. |
| Auto-cutting flagged passages | Flag, then let the user decide. Some flagged moves are genuinely theirs. |
| Drafting confidently in a thin register | Honor the "insufficient data" flag. Tell the user, do not fake it. |

## Done definition

- Bundle exists in the target directory with all 9 files
- Test drafts in every populated register generated and scored 15 or higher on `04_evaluation_checklist.md` (18-20 ships as-is, 15-17 after one light pass)
- Stage 6 source-fidelity audit run: every lexicon and calibration quote traces to the corpus, smoothed quotes restored, untraceable quotes dropped
- User has confirmed at least one test draft reads like them
- If the corpus is too thin for any register to reach 5 samples, the run still completes: deliver the bundle with every register flagged "insufficient data" and tell the user to add volume (a week of dictation is the fastest path) before relying on it
