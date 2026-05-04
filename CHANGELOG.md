# Changelog

All notable changes to Argus are documented here.

## Unreleased

## [0.5.6](https://github.com/JuroOravec/argus/compare/argus-ai-v0.5.2...argus-ai-v0.5.6) - 2026-03-22

### Fixed

- fix LLM base URL format
- *(npm)* download binaries from argus-ai-v* release tags
- *(ci)* strip binaries, add rust cache, harden packaging
- *(ci)* trigger release binary build on argus-ai-v* tags

### Other

- bump version to 0.5.6, add musl Linux build targets
- bump version to 0.5.5
- comments
- bump version to 0.5.4 (fork manual release)
- *(release-plz)* optional registry publish via ARGUS_PUBLISH_TO_REGISTRIES
- *(release-plz)* run release-pr only; skip crates.io and npm publish
- release v0.5.3

### Fixed

- **LLM `base_url` vs API version path (OpenAI-compatible, Anthropic, Gemini)**  
  
   Argus used to always append `/v1/...` or `/v1beta/...` after whatever you put in `[llm] base_url`. This breaks the **OpenAI-style** base URL, which already includes the version segment—e.g. `https://api.openai.com/v1` or gateways like `https://openrouter.ai/api/v1`. 
  
   In those cases Argus was calling `.../v1/v1/chat/completions` (or the Gemini equivalent), which often returns **404** with an HTML error page instead of JSON.

   The client now checks whether `base_url` already ends with `/v1` (OpenAI-compatible + Anthropic) or `/v1beta` (Gemini). If it does, that value is used as the API root; if not, Argus still appends the segment, preserving behavior from **0.5.2 and earlier**.

### Deprecated

- **`base_url` without a version suffix** (e.g. `https://api.openai.com`) still work but are **deprecated**. Instead use proper base URLs like `https://api.openai.com/v1` or `https://openrouter.ai/api/v1`. Support for host-only values may be removed in a future major release.

## [0.5.3](https://github.com/JuroOravec/argus/compare/argus-ai-v0.5.2...argus-ai-v0.5.3) - 2026-03-20

### Fixed

- *(npm)* download binaries from argus-ai-v* release tags
- *(ci)* strip binaries, add rust cache, harden packaging
- *(ci)* trigger release binary build on argus-ai-v* tags

## [0.5.2](https://github.com/Meru143/argus/compare/argus-ai-v0.5.1...argus-ai-v0.5.2) - 2026-02-26

### Other

- Fix multiple bugs and performance issues across the workspace ([#60](https://github.com/Meru143/argus/pull/60))

## [0.5.1](https://github.com/Meru143/argus/compare/argus-ai-v0.5.0...argus-ai-v0.5.1) - 2026-02-26

### Added

- add event log for review history ([#58](https://github.com/Meru143/argus/pull/58))

## [0.5.0](https://github.com/Meru143/argus/compare/argus-ai-v0.4.1...argus-ai-v0.5.0) - 2026-02-25

### Other

- add quoted-path diff fixture regression coverage
- add codebase audit follow-up tasks

## [0.4.1](https://github.com/Meru143/argus/compare/argus-ai-v0.4.0...argus-ai-v0.4.1) - 2026-02-24

### Added

- add git hook install/uninstall commands ([#48](https://github.com/Meru143/argus/pull/48))
- *(review)* add --vouch and --skip flags ([#45](https://github.com/Meru143/argus/pull/45))
- *(review)* add --print-metadata flag for commit messages ([#42](https://github.com/Meru143/argus/pull/42))
- *(review)* add --commit flag to review already-committed changes ([#40](https://github.com/Meru143/argus/pull/40))
- *(review)* add --copy flag for AI-agent-friendly output ([#37](https://github.com/Meru143/argus/pull/37))

### Fixed

- hook improvements ([#50](https://github.com/Meru143/argus/pull/50))
- hook feedback improvements ([#49](https://github.com/Meru143/argus/pull/49))
- move vouch/skip checks before diff acquisition ([#47](https://github.com/Meru143/argus/pull/47))
- move vouch/skip checks earlier ([#46](https://github.com/Meru143/argus/pull/46))
- use singular comment when count is 1 ([#44](https://github.com/Meru143/argus/pull/44))
- address code review feedback ([#43](https://github.com/Meru143/argus/pull/43))
- *(review)* address code review feedback ([#41](https://github.com/Meru143/argus/pull/41))

## [0.4.0](https://github.com/Meru143/argus/compare/argus-ai-v0.3.2...argus-ai-v0.4.0) - 2026-02-17

### Added

- implement learning from feedback (argus feedback)

### Fixed

- *(review)* use local build for review and add rate limit backing off
- use GH_PAT for release-pr to trigger CI checks

### Other

- revert model to gemini-2.5-flash to fix rate limits
- add concurrency group to prevent rate limit collisions
- update gemini model ID to gemini-3-pro-preview
- upgrade argus review model to gemini-3-pro
- disable self-reflection to avoid Gemini 429 rate limits
- switch Argus review to gemini-2.5-flash
- switch Argus review to gemini-1.5-flash to avoid 429s

## [0.3.2](https://github.com/Meru143/argus/compare/argus-ai-v0.3.1...argus-ai-v0.3.2) - 2026-02-16

### Fixed

- remove invalid --diff argument from review workflow

### Other

- ignore and remove PLAN.md
- ignore private sprint logs
- add homebrew installation instructions

## [0.3.1](https://github.com/Meru143/argus/compare/argus-ai-v0.3.0...argus-ai-v0.3.1) - 2026-02-16

### Other

- update README with describe, custom rules, and ollama support

## [0.3.0](https://github.com/Meru143/argus/compare/argus-ai-v0.2.2...argus-ai-v0.3.0) - 2026-02-16

### Added

- implement learning from feedback (argus feedback)
- add PHP, Kotlin, Swift tree-sitter support (9→12 languages)
- implement incremental review (--incremental)
- add PR description generation (argus describe)
- self-reflection FP filtering, indicatif progress bars, 4 new languages ([#2](https://github.com/Meru143/argus/pull/2))

### Fixed

- configure gemini provider via .argus.toml instead of --provider flag

### Other

- add release-plz workflow for auto-publishing

## [0.2.2] — 2026-02-16

### Added
- **Welcome screen** — `argus` with no args now shows a branded welcome screen with quick start commands
- **Contextual error hints** — user-friendly hints for common errors (missing config, no API key, not in git repo)
- **Two-tier help** — `argus -h` for brief summary, `argus --help` for full details

## [0.2.0] — 2026-02-16

### Added
- **Summary generation** — reviews now produce a high-level summary paragraph (overall risk, key themes, areas of concern)
- **Suggested patches** — each review comment includes a concrete unified diff fix
- **SARIF output** — `--format sarif` for GitHub Code Scanning integration
- **Shell completions** — `argus completions bash|zsh|fish|powershell`
- **`argus doctor`** — environment diagnostics (API keys, config, providers)
- **`--color` flag** — explicit color control (`auto|always|never`), respects `NO_COLOR`
- **Cross-file analysis** — reviews analyze related files beyond the diff for better context
- **Custom review rules** — define project-specific rules in `.argus.toml`
- **Real-time progress** — streaming output during review so you're not staring at a blank terminal
- **`--show-filtered`** — debug noise reduction by seeing which comments were filtered and why

### Changed
- Bumped workspace version to 0.2.0
- Added CI workflow (test + clippy + fmt)
- Added Cargo.toml metadata (description, repository, keywords, categories)

## [0.1.1] — 2026-02-15

### Added
- **Gemini LLM provider** — use Gemini for reviews (free tier available)
- **Anthropic provider** — Claude support via Messages API
- **Multi-provider embeddings** — Voyage, Gemini, and OpenAI embedding support
- **Thinking model support** — handle thinking blocks in Anthropic responses
- **Dimension tracking** — multi-provider safety for embedding indices
- **npm package** — `npx argus-ai` / `npm install -g argus-ai`
- **Zero-cost setup** — Gemini for both LLM and embeddings with a free API key

### Fixed
- Fail early on missing API key with clear error message
- Redact API keys from error output
- Handle corrupted dimension metadata gracefully
- Validate model-provider compatibility on embedding init

## [0.1.0] — 2026-02-14

### Added
- **`argus review`** — AI-powered code review with context from all modules
- **`argus map`** — structural codebase overview (tree-sitter + PageRank)
- **`argus diff`** — risk scoring for code changes
- **`argus search`** — semantic + keyword hybrid code search
- **`argus history`** — hotspot detection, temporal coupling, bus factor analysis
- **`argus mcp`** — MCP server for IDE integration (Cursor, Windsurf, Claude Code)
- **`argus init`** — generate `.argus.toml` with sensible defaults
- **GitHub PR integration** — `--pr owner/repo#42`, `--post-comments`, `--fail-on`
- **GitHub Action** — automated review on pull requests
- **Release workflow** — cross-platform binaries (Linux, macOS, Windows)
- **Noise reduction** — pre-LLM file filtering, complexity scoring, deduplication
- **Anti-hallucination prompts** — strict rules to prevent fabricated line numbers
