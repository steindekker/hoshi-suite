# Hoshi suite

One place for Stein's Japanese-learning apps and the pieces they share. Each app keeps its own repo and upstream; this repo pins them as submodules.

| Path | What | Upstream to merge from |
|---|---|---|
| `hoshi-reader/` | Hoshi Reader Android: dictionary, card creation, books, Live | `HuangAntimony/Hoshi-Reader-Android` |
| `chimahon/` | chimahon (Komikku/Mihon based): manga/novel reader, OCR lookup | `Chimahon/chimahon` |
| `hoshi-card/` | Shared library: enrichment pack, pitch-marked sentences, the Hoshi note type, setup catalog client | none |
| `server/` | Builds and serves the first-run setup catalog: Rust pack builder, pack server, publish script, sentence-model build | none |

## Rules

- Priorities and app conventions live in each app's own `AGENTS.md`; read the one for the app you change.
- **Both apps must make the same Hoshi cards.** Card logic (enrichment fields, sentence pitch markup, note type, field mapping) belongs in `hoshi-card`, never copied into an app. Change it there, then bump the pin in both apps.
- Field names are plain: `{definition}`, `{definition-source}`, `{pitch-graph}`, `{frequency-rank}`, `{example-sentences}`, `{sentence-pitch}`. The pack format is defined by `server/` (builder) and read by `hoshi-card`; change both together.
- Inside the suite, both apps build against the shared `hoshi-card/` checkout (`../hoshi-card`); on their own they use their pinned `third_party/hoshi-card` submodule.
- Everything here is public: never commit hostnames, private IPs, personal paths, tokens, keys or credentials. Deployment values come from environment variables or local config files; docs use placeholders.
- Conventional Commits. Commit in the submodule first, then the suite's pin.

## Working in the suite

```bash
git clone --recurse-submodules https://github.com/steindekker/hoshi-suite.git
git submodule update --init --recursive   # after pulling
```
