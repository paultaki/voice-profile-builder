# Why a pre-AI corpus

## The contamination problem

ChatGPT shipped in late November 2022. Within months, a large share of the writing people produce stopped being purely theirs. You ask a model to "tighten this email." You accept its phrasing on a LinkedIn post. You let autocomplete finish a sentence. Each of those is a small edit toward the statistical center of how language models write: balanced, hedged, smooth, and faintly generic.

If you then build a voice profile from that writing, you are not capturing your voice. You are capturing your voice already bent halfway toward the model. The profile teaches the AI to sound like a slightly-more-you version of itself. That is why so many "write in my voice" setups still feel off. The source was contaminated before the analysis began.

## The fix: time-slice the source

Use writing from before the contamination started. A January 2023 cutoff is a safe buffer past the late-2022 launch. Writing from that era has a property nothing produced afterward can guarantee: it is unambiguously, entirely yours. Your run-ons. Your trailing dots. The word you overuse. The closer you always reach for. The way you get blunt when you are annoyed.

That rawness is the asset. A clean corpus does not need to be laundered, and an AI trained on it does not need to be humanized after the fact.

## How this differs from the common advice

Most guides and tools say: gather three to five of your **best** or **most recent** pieces, have AI analyze the style, save it as instructions. Two problems:

1. **Best is not characteristic.** Your polished, edited work is the least *you* it ever gets. Your voice lives in the rough draft, the quick reply, the unguarded text.
2. **Recent is contaminated.** See above.

A second family of tools attacks the problem from the other end: they take AI output and run it through a "humanizer" until a detector passes. That treats the symptom. The text still originated from the model's center of gravity; the humanizer just adds noise on top. Fixing the input is cleaner than laundering the output.

## What still matters besides the cutoff

The cutoff is necessary, not sufficient. The corpus also needs:

- **Width.** Multiple registers. Email, customer service, family notes, strategy, texts. A profile built from 80% customer-service complaints will only write customer-service complaints well.
- **Volume.** 20,000 words is a floor. 80,000+ is the sweet spot. Patterns need repetition to be trustworthy.
- **Rawness.** Do not clean it up before feeding it in. The typos and the run-ons are the fingerprint.

## If you do not have pre-2023 writing

You can still build a useful profile from later writing, but be deliberate:

- Prefer writing you know you did not run through an AI (handwritten-then-typed notes, quick texts, private journals).
- Run the contamination scan aggressively and cut hard.
- Accept that the profile will be a little closer to the model's center than a pre-AI one would be.

The cutoff is the ideal. The principle underneath it is the real rule: **the cleaner the source, the truer the voice.**
