# anthropic-learning

Jupyter notebooks for working through the Anthropic API course. Each notebook is
numbered and runs on its own.

## Notebooks

| Notebook | Covers |
| --- | --- |
| `01_client.ipynb` | Client setup, a single request, and a multi-turn chat loop with streamed responses |
| `02_structured_output.ipynb` | Structured JSON output with a Pydantic model (`messages.parse`) and a raw JSON schema (`output_config`) |
| `03_prompt_evals.ipynb` | Generating an eval dataset with structured output and running a prompt against each test case (grading still a placeholder) |

## Setup

Requires Python 3.14.

```sh
python3 -m venv .venv
.venv/bin/pip install anthropic python-dotenv jupyter ipykernel
```

Create a `.env` file in the repo root with your API key (it is git-ignored):

```
ANTHROPIC_API_KEY=sk-ant-...
```

## Running

```sh
source .venv/bin/activate && jupyter lab
```

To execute a notebook headlessly:

```sh
.venv/bin/jupyter nbconvert --to notebook --execute <notebook>.ipynb --stdout
```

Notebooks that read from `input()`, such as the chat loop in `01_client.ipynb`, only
work interactively.

## Differences from the course

- The notebooks use `claude-sonnet-5-5` instead of the retired `claude-sonnet-4-0`.
  Every notebook sets the model once in its first cell.
- The course's `temperature`, `top_p` and `top_k` arguments are left out. The current
  SDK doesn't accept them, so responses are steered through the prompt or
  `output_config={"effort": ...}` instead.
- The course gets JSON by prefilling the assistant turn and adding stop sequences.
  Current models reject assistant prefill, so `02_structured_output.ipynb` uses
  structured outputs instead.
