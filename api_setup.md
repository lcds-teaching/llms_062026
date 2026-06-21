# OpenAI API Setup for Lab Three

This file supports `Labs/Lab_Three.ipynb`. Lab Three uses **OpenAI only** and now requires real API calls.

The notebook does not use substitute responses. If the API key, model name, request, network connection, or response parsing fails, the notebook will raise an error. Fix the error before continuing.

Do not paste real API keys into notebooks, Python files, slides, screenshots, GitHub, Slack, Teams, or shared documents.

## What You Need

For Lab Three:

- Python
- Jupyter
- one OpenAI API account
- one OpenAI API key
- one current OpenAI model name available to your account
- permission to send non-sensitive synthetic teaching prompts to OpenAI

Use toy examples only. Do not send personal data, health data, interview transcripts, service-user records, or confidential institutional material during the class.

## The Two Variables

Lab Three needs two environment variables:

| Variable | Meaning | Secret? |
|---|---|---|
| `OPENAI_API_KEY` | your OpenAI API key | yes |
| `OPENAI_MODEL` | the OpenAI model name to call | no |

Do not mix these up. The key is secret. The model name is not secret.

## Get an OpenAI API Key

1. Go to the OpenAI API dashboard: https://platform.openai.com/
2. Sign in or create an account.
3. Create an API key.
4. Copy it once and store it securely.
5. Set it as `OPENAI_API_KEY` using one of the methods below.

Recommended:

- create a separate course/testing key, not your main production key;
- save the key in a password manager;
- set a spending limit, usage alert, or quota if available;
- revoke the course key after the course or if it is exposed.

## Choose a Model Name

Use a model name from your OpenAI dashboard or the current OpenAI model docs:

https://platform.openai.com/docs/models

Store the model name in:

```bash
OPENAI_MODEL
```

Good habits:

- use the exact model identifier shown by OpenAI;
- prefer a low-cost, fast model for this lab;
- check that your account has access to the model;
- record the model name in your methods notes and logs;
- recheck model names before teaching, because model lists change.

Avoid:

- putting the model name into `OPENAI_API_KEY`;
- using a generic variable like `MODEL`;
- hard-coding model names inside notebook answers;
- assuming last year's model name still works.

## Temporary Setup

Use this if you only need the variables for the current terminal session. They disappear when the terminal closes.

### macOS/Linux

```bash
export OPENAI_API_KEY="paste_key_here"
export OPENAI_MODEL="paste_current_model_name_here"
```

Then launch VS Code or Jupyter from that same terminal:

```bash
code .
```

or:

```bash
jupyter lab
```

### Windows PowerShell

```powershell
$env:OPENAI_API_KEY = "paste_key_here"
$env:OPENAI_MODEL = "paste_current_model_name_here"
```

Then launch VS Code or Jupyter from that same PowerShell window.

## Persistent Setup

Use this if you want the variables to survive after closing the terminal.

### macOS/Linux

Add lines like these to your shell profile, usually `~/.zshrc` on recent macOS or `~/.bashrc` on many Linux systems:

```bash
export OPENAI_API_KEY="paste_key_here"
export OPENAI_MODEL="paste_current_model_name_here"
```

Then restart the terminal or run:

```bash
source ~/.zshrc
```

If using `~/.bashrc`, run:

```bash
source ~/.bashrc
```

### Windows PowerShell

```powershell
setx OPENAI_API_KEY "paste_key_here"
setx OPENAI_MODEL "paste_current_model_name_here"
```

After `setx`, open a new terminal and restart VS Code or Jupyter.

## Conda Setup Option

If you use conda and want these variables to appear whenever a specific conda environment is activated:

```bash
conda activate lcds-python
conda env config vars set OPENAI_API_KEY="paste_key_here"
conda env config vars set OPENAI_MODEL="paste_current_model_name_here"
conda deactivate
conda activate lcds-python
```

Then restart VS Code or Jupyter and select the `lcds-python` kernel.

## Check Setup

Run this in the same terminal that will launch VS Code or Jupyter:

```bash
python -c "import os; print(os.getenv('OPENAI_API_KEY') is not None); print(os.getenv('OPENAI_MODEL'))"
```

Expected output:

```text
True
your_model_name
```

In a notebook, run:

```python
import os

print("OpenAI key:", os.getenv("OPENAI_API_KEY") is not None)
print("OpenAI model:", os.getenv("OPENAI_MODEL"))
```

## If the Notebook Still Says `False`

If the terminal check works but the notebook says the key or model is missing, the notebook kernel did not inherit the terminal environment.

This usually happens when:

- VS Code or Jupyter was already open before you ran `export`;
- VS Code was opened from the desktop launcher instead of from the terminal;
- the notebook kernel was started before the variables existed;
- the variables were set in one terminal, but Jupyter was launched from another terminal.

Fix:

1. Fully close VS Code or Jupyter.
2. Open a terminal.
3. Set or confirm `OPENAI_API_KEY` and `OPENAI_MODEL`.
4. Launch VS Code or Jupyter from that same terminal.
5. Restart the notebook kernel.
6. Rerun the setup cells.

## Before Running Lab Three

Use this checklist:

- I am using synthetic teaching prompts, not sensitive data.
- I understand that OpenAI calls may cost money.
- I have set a low `max_output_tokens` value in lab calls.
- I have set `OPENAI_API_KEY` and `OPENAI_MODEL`.
- I have restarted the notebook kernel after setting environment variables.
- I know how to revoke the key if it leaks.

## Removing Keys

macOS/Linux, current session:

```bash
unset OPENAI_API_KEY
unset OPENAI_MODEL
```

Windows PowerShell, persistent user variables:

```powershell
[Environment]::SetEnvironmentVariable("OPENAI_API_KEY", $null, "User")
[Environment]::SetEnvironmentVariable("OPENAI_MODEL", $null, "User")
```

Also revoke exposed keys in the OpenAI dashboard.

## Expected Lab Three Errors

Lab Three is designed to fail loudly when setup is wrong.

Common causes:

- missing `OPENAI_API_KEY`;
- missing `OPENAI_MODEL`;
- model name is misspelled or unavailable to your account;
- account has no billing or quota;
- selected model does not support a parameter used in a later exercise;
- network connection fails;
- the API call times out before the full response is received;
- a structured-output prompt returns invalid JSON.

When this happens, read the traceback and fix the underlying setup, request, or prompt.

## If a Request Times Out

A timeout means the notebook sent the request but did not receive a complete response before the timeout limit. This can happen because of network instability, provider delay, or a batch cell making several calls.

Lab Three defines this setting near the top:

```python
OPENAI_TIMEOUT_SECONDS = 240
```

If a timeout happens:

1. Rerun the same cell once.
2. Check your internet connection.
3. Reduce `max_output_tokens` or run fewer batch examples.
4. Increase `OPENAI_TIMEOUT_SECONDS`, then rerun the setup cells.

The notebook still does not create substitute outputs. A timeout remains a real failure that must be fixed or rerun.
