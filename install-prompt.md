# One-paste install

If you would rather not clone the repo, paste the block below into a fresh Claude Code session. It downloads the skill, confirms it is available, then asks for your corpus path and output directory and runs it end to end.

> Before you paste: you need a corpus. One file, plain text or Markdown, at least 20,000 words of your own writing, ideally pre-January 2023. See the README section "Before you start: build a corpus."

````text
Run this to install the skill, then use it:

mkdir -p ~/.claude/skills/voice-profile-builder && curl -fsSL https://raw.githubusercontent.com/paultaki/voice-profile-builder/main/SKILL.md -o ~/.claude/skills/voice-profile-builder/SKILL.md

After it downloads, confirm the voice-profile-builder skill is available, then ask me for (a) the path to my writing corpus and (b) the directory where the bundle should be written, and run the skill end to end.
````

After the first run, the skill stays on your machine. To use it again later, from any directory:

```text
Use the voice-profile-builder skill on the corpus at <path>, write the bundle to <directory>.
```

## A few things worth knowing

The contamination scan is conservative. It flags, it does not cut. You stay in the loop. If it flags a phrase you actually say, keep it. The point is your real voice, not a sanitized one.

If your corpus is light on a register, the bundle will say so. Do not fight it. The "insufficient data" flag exists so you do not ask an AI to draft a memoir chapter from a corpus that is 80% customer-service complaints.

The `CLAUDE.md` the skill writes is the most important file in the bundle. It tells every future session which files to load and in what order. If you move the bundle to another machine, the `CLAUDE.md` goes with it.

The first step is to prove it. Build the bundle, generate a test draft, read it aloud. If it sounds like you, ship it. If it does not, the corpus is the lever, not the rules.
