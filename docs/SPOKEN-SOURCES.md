# Spoken sources and the recency refinement

The pre-2023 rule (see [WHY-PRE-AI-CORPUS.md](WHY-PRE-AI-CORPUS.md)) exists because AI *editing* bends your writing toward the model's statistical center. The cutoff is a proxy for "before you started letting a model touch your words."

But the real rule is about the contamination *vector*, not the calendar. And there is one kind of source the vector cannot reach: **speech.**

## Why speech is clean at any date

You cannot AI-smooth your own talking in the moment. When you dictate, narrate, or get recorded, the words leave your mouth before any model can balance their clauses or hedge their claims. A transcript from last week is as uncontaminated as an email from 2019. The disfluency, the run-ons, the false starts, the word you reach for three times in a paragraph: all yours, all intact.

So the refined rule:

- **Written material:** prefer pre-2023. Anything you typed after late 2022 may have been AI-touched.
- **Spoken or transcribed material:** any era is fair game. Date does not matter. Rawness does.

This matters because most people do not have an 80,000-word pre-2023 email archive lying around, but almost anyone can generate spoken volume fast. Talk through your work for a week with dictation on and you have tens of thousands of words of pure, recent, uncontaminated voice.

## Spoken sources, ranked by value

1. **Dictation you already do all day.** Wispr Flow, macOS/iOS dictation, any speech-to-text you use while working. The highest-volume, most natural source.
2. **Voice memos transcribed.** Phone voice notes run through Whisper or any transcription tool.
3. **Your own podcast, YouTube, webinar, or talk transcripts.** Long-form, on-topic, you doing the talking.
4. **Recorded interviews, sales calls, or meetings where you talk a lot.** Strip the other speakers, keep your turns.

Strip the other people's words, the same way you strip a reply quote out of an email thread. Keep only the person's own speech.

## The one discipline that matters: do not smooth it

This is where spoken corpora get ruined. An AI extracting from a transcript will instinctively *tidy*: drop the "um," fix the run-on, normalize the grammar, turn three fragments into one clean sentence. That tidying is the exact thing that pushes the voice back toward the model's center. The unevenness is not noise. It is the signal that beats detectors.

When a sample is a transcript:

- **Fix only obvious transcription garble.** A wrong homophone ("their/there"), a doubled word the speaker did not say, a mangled product name.
- **Never** normalize grammar, break up run-ons, delete filler, or "clean up" the cadence.
- A real slip the speaker actually made (a stutter, a self-correction mid-sentence, a trailing-off) **stays.** It is the fingerprint.

Rule of thumb: if you are unsure whether a change is a garble-fix or a smoothing, it is a smoothing. Leave it alone.

## Two banks, not one

When a corpus mixes pre-2023 written material and modern spoken material, keep them as two labeled banks rather than blending them:

- **Written bank (pre-AI).** The canonical source for composed registers: email, formal notes, anything with a greeting and a closer.
- **Spoken bank (any era).** The canonical source for raw cadence: casual or peer, thinking-out-loud strategy, narrating your own work, and any register that should sound dictated rather than drafted.

Label each calibration example and lexicon entry with the bank it came from when both exist. When the consumer drafts, it pulls from the bank that matches the register: spoken for spoken-feeling output, written for composed output. A hot take or a build note should sound like the person talking. A client email should sound like the person writing.

## Net

The pre-2023 cutoff is the rule for *written* sources. Speech is exempt because it cannot be laundered in the moment. If someone has thin pre-AI writing, do not treat the profile as second-rate. Point them at a week of dictation instead. It is often the cleaner, higher-volume source.
