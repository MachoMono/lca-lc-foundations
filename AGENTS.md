# Agent guide

This is a personal fork of LangChain Academy's "Introduction to LangChain" course
(`langchain-ai/lca-lc-foundations`). The owner works through the notebooks on several
computers and keeps them in sync through this fork.

## Getting a fresh checkout working

Run `./setup` from the repo root. It is safe to re-run and does the following:

1. Builds `.venv` with `uv sync` if `uv` is installed, otherwise with `python -m venv`
   and `pip install -r requirements.txt`.
2. Copies `example.env` to `.env` if `.env` is missing.
3. Runs `env_utils.py`, which checks the Python version, packages and API keys.

Requirements and things `./setup` cannot do for you:

- Python must be >=3.12,<3.14. A system Python of 3.14 will not work; use `python3.13`,
  `python3.12` or `uv`.
- `.env` is gitignored and holds real API keys, so it never arrives with a clone. If
  `./setup` had to create it, the keys are placeholders: stop and ask the owner to fill
  them in (or copy `.env` from their other computer). Never commit `.env` or print its
  values.
- `OPENAI_API_KEY` and `TAVILY_API_KEY` are required. The Anthropic, Google and
  LangSmith keys are optional.
- Module 2, lesson 1 runs an MCP server with `uvx`, so `uv` is needed for that lesson.
- `notebooks/module-3/agent-chat-ui` is a separate Node app, needed only for the bonus
  lesson.

## Daily sync

- `./start` pulls the latest work, and runs `./setup` if `.venv` or `.env` is missing.
- `./done` commits everything and pushes. An optional message can follow:
  `./done "finished module 1"`.

Run these as `./start` and `./done`; `done` alone is a shell reserved word. On Windows
use Git Bash.

## Running things

- Notebooks: open them in VS Code and pick the `.venv` kernel, or run
  `.venv/bin/jupyter lab`.
- LangGraph Studio: `cd notebooks/module-1` (or `module-3`), then
  `../../.venv/bin/langgraph dev`.
- With `uv`, the equivalents are `uv run jupyter lab` and `uv run langgraph dev`.

## Git layout

- `origin` is the owner's fork, `MachoMono/lca-lc-foundations`. Push here.
- `upstream` is the course repo. A new clone does not have it; add it with
  `git remote add upstream https://github.com/langchain-ai/lca-lc-foundations.git`
  and pull course updates with `git pull upstream main`.
- `.langgraph_api/` folders are local caches and are gitignored. Do not re-add them.
- When adding a dependency, add it to both `pyproject.toml` and `requirements.txt`.
