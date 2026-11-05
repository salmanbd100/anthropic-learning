# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal sandbox of Jupyter notebooks for working through Anthropic API course material. It is not an application: there is no package, build, test suite or linter. Notebooks are numbered (`01_client.ipynb`, …) and each one stands alone.

## Environment

- Python 3.14 venv at `.venv/`, managed with plain `pip` (no `uv`, no `requirements.txt` yet). Installed packages: `anthropic`, `python-dotenv`, `jupyter`/`ipykernel`.
- The API key lives in `.env` as `ANTHROPIC_API_KEY`. It is git-ignored and blocked by a hook, so don't read it. If you get a 401, ask the user to check the key.

## Commands

```sh
source .venv/bin/activate && jupyter lab                     # interactive
.venv/bin/jupyter nbconvert --to notebook --execute <nb>.ipynb --stdout   # run headlessly to verify
.venv/bin/pip install <pkg>                                  # add a dependency
```

## Conventions

- Every notebook's first cell is the same setup: `load_dotenv()`, then `client = Anthropic()` and a `model` variable. Later cells use `client` and `model`, so don't hard-code model IDs.
- The course material uses `claude-sonnet-4-0` (retired). The notebooks use the current `claude-sonnet-5-5` with the latest `anthropic` SDK instead.
- Don't port the course's `temperature`/`top_p`/`top_k` arguments: the SDK no longer accepts them and `claude-sonnet-5-5` rejects non-default values. Steer with the prompt or `output_config={"effort": ...}` instead.
