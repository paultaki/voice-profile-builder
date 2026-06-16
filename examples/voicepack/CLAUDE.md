# Loader: Dana Cole Voice Pack (SYNTHETIC EXAMPLE)

This file tells a future AI session how to use this bundle. It travels with the bundle if you move it.

## Load by purpose

- **Any Dana-voice writing:** load `01_master_voice_profile.md`, `02_register_cards.md`, `06_style_guide.md`, `07_lexicon.md`.
- **After every draft:** run `04_evaluation_checklist.md`. Do not ship below 15.
- **Need a closer match for a specific channel:** also load the matching card in `02` and the example in `05_calibration_examples.md`.
- **Drafting prompts:** pull from `03_prompt_pack.md`.
- **Deep retrieval (agents that can read it):** `corpus.md` is the source of truth. Pull 2-3 same-register samples before drafting.
- **Two banks:** Dana's corpus has a written bank (pre-2023 email) and a spoken bank (2025-2026 dictation). For dictated-feeling output (operator field notes, thinking out loud), pull from the spoken bank; for composed output (email, formal), pull from the written bank.

## Confidence rules when context is missing

- If the requested register is marked "insufficient data" in `02`, say so. Do not fabricate a tone.
- If you cannot find a phrase in the lexicon to support a move, do not make the move. Ask or flag low confidence.

## Hard rules

1. **Never invent a quote.** Every lexicon, calibration, or style-guide phrase must exist verbatim in `corpus.md`.
2. **No em-dashes.** Dana's corpus does not use them.
3. **Match the register to the channel.** A peer text is not an email.
4. **Warmth is action, not adjectives.**
5. **Never publish or paste `corpus.md` anywhere.** It is private source material.
