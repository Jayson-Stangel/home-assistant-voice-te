# Repository Guidelines

## Project Structure & Module Organization
- Root YAML configs: `home-assistant-voice.yaml` (main), `home-assistant-voice.factory.yaml`, `home-assistant-voice.8mb.yaml`, `voice-kit.yaml`.
- Custom ESPHome component: `esphome/components/voice_kit/` (C++: `voice_kit.{h,cpp}`, Python codegen: `__init__.py`).
- Modules and includes: `modules/*.yaml` (e.g., `grove-i2c.yaml`, `grove-power.yaml`).
- Assets: `sounds/` and `static/`. CI workflows: `.github/workflows/`.

## Build, Test, and Development Commands
- Validate config: `esphome config home-assistant-voice.yaml` — schema and deps check.
- Compile firmware: `esphome compile home-assistant-voice.yaml`.
- Flash/run (USB/Web): `esphome run home-assistant-voice.yaml`.
- Docker alternative: `docker run --rm -v "$PWD":/config ghcr.io/esphome/esphome compile home-assistant-voice.yaml`.
- YAML lint: `yamllint --strict .` (uses `.yamllint`).
- Format C++: `clang-format -i esphome/components/voice_kit/*.{h,cpp}` (style in `.clang-format`).

## Coding Style & Naming Conventions
- YAML: 2-space indent, one blank line max between blocks; IDs and substitutions use `snake_case` (e.g., `voice_assistant_phase`).
- C++: follow `.clang-format`; member variables use trailing `_` (e.g., `firmware_bin_`), functions `lower_snake_case`, constants `UPPER_SNAKE_CASE`.
- Python (codegen): prefer Black-compatible style; keep minimal logic and validate via `esphome` build.
- File names: hyphenated for top-level YAML, `snake_case` for module YAML.

## Testing Guidelines
- No unit tests; use compile/flash cycle and device logs for verification.
- Before PRs: run `esphome config`, `esphome compile`, and `yamllint --strict .`.
- Add small, reviewable YAML modules under `modules/` when isolating changes.

## Commit & Pull Request Guidelines
- Commits: imperative mood, concise summary; reference PR/issue when applicable (e.g., “Enable IPv6 support (#394)”).
- PRs must include: purpose, summary of changes, test steps (commands + expected device behavior), and any UI/LED/audio changes.
- Keep PRs focused; update `README.md` or comments when behavior changes.

## Security & Configuration Tips
- Do not commit secrets (Wi‑Fi SSIDs/passwords). Prefer installer flows or `substitutions` with safe defaults.
- Avoid logging sensitive data; keep `logger:` levels appropriate.
- Verify firmware URLs and checksums when touching `voice_kit` DFU settings in `__init__.py`.

