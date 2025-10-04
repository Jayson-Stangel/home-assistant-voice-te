# Home Assistant Voice: Preview Edition

This is the ESPHome source code of the [Home Assistant Voice: Preview Edition](https://www.home-assistant.io/voice-pe/).

See [the documentation](https://voice-pe.home-assistant.io/) for set up and troubleshooting.

If you need to re-install the firmware, [use this installer](https://esphome.github.io/home-assistant-voice-pe/).

## Fork Information

This repository is a fork of the upstream project:

- Upstream: https://github.com/esphome/home-assistant-voice-pe
- This fork: https://github.com/Jayson-Stangel/home-assistant-voice-te

Purpose: maintain local tweaks (e.g., custom micro_wake_word models) and experiments while tracking upstream closely. Please open core issues upstream unless specific to this fork.

### Keeping the fork in sync

```
git fetch upstream
git checkout dev
git rebase upstream/dev
git push origin dev --force-with-lease
```

CI in this fork mirrors upstream and builds from `dev`.
