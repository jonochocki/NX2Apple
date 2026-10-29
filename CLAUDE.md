# Notes for Claude

- Read [engine/AGENTS.md](engine/AGENTS.md) first: the engine's guide, from seedds/nxnative at the pin. `engine/` is made by `python3 tools/engine.py sync` (the SessionStart hook in `.claude/settings.json` runs it). Until the committed copy goes (step 2 of #214), [AGENTS.md](AGENTS.md) at the root is the same file.
- For an issue or a pull request, follow [CONTRIBUTING.md](CONTRIBUTING.md), section "For AI agents and other tools", and the templates in `.github/`.
- The engine is seedds/nxnative at `.upstream-ref` plus the patch queue in `patches/`. Work on it in `engine/`: commit there, then `python3 tools/engine.py export` turns the commits into patches with their header (see [patches/README.md](patches/README.md)). `dm/`, `scripts/`, `docs/`, `ref/` and `AGENTS.md` at the root are the same tree, still committed until step 2 of #214: never edit them directly, `tools/engine.py check --tree` fails otherwise.
