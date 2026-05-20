# Example bundle (synthetic)

Everything in this folder is **fictional**. The persona is "Dana Cole," an invented owner of a small landscaping business. No real person's writing is included anywhere in this repo.

The point is to show you the *shape* of what the builder produces, so you can evaluate the method without anyone handing over private correspondence.

- [`sample-corpus.md`](sample-corpus.md): a tiny synthetic corpus (a real one would be 20,000+ words). Shows the raw, multi-register input the builder expects. In a real run this becomes `corpus.md` inside the bundle, the cleaned and register-sorted source. It is the ninth file, kept one level up here so the example reads cleanly.
- [`voicepack/`](voicepack/): the eight generated files: [`01_master_voice_profile.md`](voicepack/01_master_voice_profile.md), [`02_register_cards.md`](voicepack/02_register_cards.md), [`03_prompt_pack.md`](voicepack/03_prompt_pack.md), [`04_evaluation_checklist.md`](voicepack/04_evaluation_checklist.md), [`05_calibration_examples.md`](voicepack/05_calibration_examples.md), [`06_style_guide.md`](voicepack/06_style_guide.md), [`07_lexicon.md`](voicepack/07_lexicon.md), and [`CLAUDE.md`](voicepack/CLAUDE.md).

When you run the skill on your own corpus, you get this same set plus your own `corpus.md`, populated from your writing, written to the directory you name.
