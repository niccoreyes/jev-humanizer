# Jev Humanizer: English-first fork

This fork makes the existing English audit the primary workflow. Jev checks paragraphs for writing patterns; a writing agent reviews the findings and edits only confirmed problems. The local linter catches mechanical issues. Jev does not generate the rewrite or establish who wrote the text.

## Run from this checkout

```bash
cd /Users/niccoreyes/Github/jev-humanizer
python3 -m unittest discover -s tests
python3 -m jev_humanizer.audit draft.md --lang en --sections --json audit.json
```

The audit reads `TYPESAFE_API_KEY` from the environment, then `~/.codex/.env` or `~/.config/typesafe.env` when those files are owner-only. No key belongs in this repository. `--no-jev` runs the local linter without sending text to TypeSafe.

The agent workflow is in [`skill/ENGLISH.md`](skill/ENGLISH.md). The Russian workflow remains in [`skill/SKILL.md`](skill/SKILL.md). English patterns are based on the vendored [blader/humanizer](https://github.com/blader/humanizer); vendor files remain untouched.

## Evidence limits

The upstream English mode has unit tests, but this fork has no measured English writing-quality or latency benchmark yet. Review facts, citations, and uncertainty after every rewrite. Jev's style findings are advisory.
