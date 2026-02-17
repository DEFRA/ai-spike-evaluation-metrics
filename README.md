# AI Document Processing Spike

This repository contains an experimental spike investigating the reliability of various methods for evaluating llm responses.

## Prequisites

- [Python](https://docs.python.org/3/using/index.html) `>= 3.13.7` - We recommend using [uv](https://docs.astral.sh/uv/getting-started/installation/) to manage your Python environment.
- [pipx](https://pipxproject.github.io/pipx/installation/)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- [Amazon Bedrock Access](https://aws.amazon.com/bedrock/) - Ensure you have either IAM user credentials or a [Bedrock API Key](https://docs.aws.amazon.com/bedrock/latest/userguide/api-keys-use.html) with appropriate permissions.

## Setup

### Python Environment

Please install python `>= 3.13.7` and `pipx` in your environment. This project uses [uv](https://github.com/astral-sh/uv) to manage the environment and dependencies.

```python
# install uv via pipx
pipx install uv

# sync dependencies
uv sync

# create jupyter kernel
uv run task create-kernel
```

### VS Code Setup
If you are running the notebooks in VS Code, we recommend installing the following extensions:
- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) - For Python language support.
- [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) - For Jupyter notebook support.

Ensure that the Jupyter kernel created by `uv` is selected in your VS Code environment which should be named `ai-spike-evaluation-metrics`.

### Jupyter Server
If you prefer to run a Jupyter server directly, you can do so with the following command:

```bash
uv run --with jupyter jupyter lab
```

### Notebooks
The experiments are contained within Jupyter notebooks located in the top level directory.

Further documentation is provided within each notebook and in the [Experiment Writeup](experiment-writeup.md).
