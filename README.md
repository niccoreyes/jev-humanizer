# Jev Humanizer

An English writing audit for AI agents. [Jev](https://docs.typesafe.ai/llms.txt) scores paragraphs for recognizable writing patterns; the agent checks the findings and edits only passages that need work. A local linter catches mechanical issues. Neither a style finding nor a detector score establishes who wrote a text.

This is [Nicco Reyes's fork](https://github.com/niccoreyes/jev-humanizer) of [snjrusmn/jev-humanizer](https://github.com/snjrusmn/jev-humanizer). The English pattern set builds on [blader/humanizer](https://github.com/blader/humanizer). The agent workflow is in [`skill/ENGLISH.md`](skill/ENGLISH.md).

## What it does

- Audits English prose paragraph by paragraph with Jev and local checks.
- Reports the pattern, location, and probability so an editor can verify each finding.
- Guides targeted revisions while preserving facts, numbers, names, citations, uncertainty, and the writer's voice.
- Supports a local-only linter pass with `--no-jev`.

Jev **does not write the replacement text**. An agent or person makes and reviews each edit. The audit sends text to TypeSafe when Jev is enabled.

## Quick start

```bash
cd ~/Github/jev-humanizer
python3 -m unittest discover -s tests
python3 -m jev_humanizer.audit draft.md --lang en --sections --json audit.json
```

The CLI requires Python 3 and uses the standard library. It reads `TYPESAFE_API_KEY` from the process environment, then from an owner-only `~/.codex/.env`, then from `~/.config/typesafe.env`. Keep the key out of this repository. To audit without an API call:

```bash
python3 -m jev_humanizer.audit draft.md --lang en --no-jev
```

For an agent, point it to [`skill/SKILL.md`](skill/SKILL.md), which routes English writing to [`skill/ENGLISH.md`](skill/ENGLISH.md). Set `JEVH` to the absolute path of your checkout if it is elsewhere.

## Evaluation status

The repository has tests for its audit and language handling. This fork has not yet established an independent English writing-quality or latency benchmark. Review every rewrite against the source, especially factual details and the strength of claims. Jev probabilities are advisory.

## Credits and license

Based on [snjrusmn/jev-humanizer](https://github.com/snjrusmn/jev-humanizer), with English patterns from [blader/humanizer](https://github.com/blader/humanizer). The code is [MIT licensed](LICENSE); see the vendored components' notices for their licenses and provenance.
