# API Setup for Lab Three: OpenAI or Gemini

This file supports `Labs/Lab_Three.ipynb`. Lab Three now works with either **OpenAI** or **Google Gemini**.

You only need one provider. The notebook does not use substitute responses. If the API key, model name, request, network connection, quota, or response parsing fails, the notebook raises an error. Fix the error before continuing.

Do not paste real API keys into notebooks, Python files, slides, screenshots, GitHub, Slack, Teams, or shared documents.

## What You Need

For Lab Three:

- Python
- Jupyter
- one OpenAI or Gemini API account
- one API key for the provider you choose
- one current model name available to that account
- permission to send non-sensitive synthetic teaching prompts to the chosen provider

Use toy examples only. Do not send personal data, health data, interview transcripts, service-user records, or confidential institutional material during the class.

## Choose a Provider

The notebook uses this optional variable:

| Variable | Meaning | Required? |
|---|---|---|
| `LAB_THREE_PROVIDER` | `openai` or `gemini` | recommended |

If `LAB_THREE_PROVIDER` is not set, the notebook auto-detects:

1. OpenAI, if `OPENAI_API_KEY` and `OPENAI_MODEL` are set.
2. Gemini, if `GEMINI_API_KEY` and `GEMINI_MODEL` are set.

If both providers are configured and you want Gemini, set:

```bash
LAB_THREE_PROVIDER=gemini
```

## Provider Variables

### OpenAI

| Variable | Meaning | Secret? |
|---|---|---|
| `OPENAI_API_KEY` | your OpenAI API key | yes |
| `OPENAI_MODEL` | the OpenAI model name to call | no |

OpenAI setup links:

- Dashboard: https://platform.openai.com/
- Model docs: https://platform.openai.com/docs/models
- API docs: https://platform.openai.com/docs/api-reference/responses

### Gemini

| Variable | Meaning | Secret? |
|---|---|---|
| `GEMINI_API_KEY` | your Gemini API key | yes |
| `GEMINI_MODEL` | the Gemini model name to call | no |

Gemini setup links:

- Get a key in Google AI Studio: https://aistudio.google.com/app/apikey
- Model docs: https://ai.google.dev/gemini-api/docs/models
- Text generation docs: https://ai.google.dev/gemini-api/docs/text-generation

The Lab Three notebook calls Gemini through the Interactions API endpoint:

```text
https://generativelanguage.googleapis.com/v1beta/interactions
```

## Choose a Model Name

Use a current model name from your provider dashboard or documentation.

For Gemini, a typical classroom choice is a Flash model such as:

```bash
GEMINI_MODEL="gemini-2.5-flash"
```

For OpenAI, choose a low-cost, fast model available to your account and store it as:

```bash
OPENAI_MODEL="paste_current_model_name_here"
```

Good habits:

- use the exact model identifier shown by the provider;
- prefer a low-cost, fast model for this lab;
- check that your account has access to the model;
- record the provider and model name in your methods notes and logs;
- recheck model names before teaching, because model lists change.

Avoid:

- putting the model name into the API key variable;
- using a generic variable like `MODEL`;
- hard-coding model names inside notebook answers;
- assuming last year's model name still works.

## Temporary Setup

Use this if you only need the variables for the current terminal session. They disappear when the terminal closes.

### macOS/Linux: OpenAI

```bash
export LAB_THREE_PROVIDER="openai"
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

### macOS/Linux: Gemini

```bash
export LAB_THREE_PROVIDER="gemini"
export GEMINI_API_KEY="paste_key_here"
export GEMINI_MODEL="gemini-2.5-flash"
```

Then launch VS Code or Jupyter from that same terminal:

```bash
code .
```

or:

```bash
jupyter lab
```

### Windows PowerShell: OpenAI

```powershell
$env:LAB_THREE_PROVIDER = "openai"
$env:OPENAI_API_KEY = "paste_key_here"
$env:OPENAI_MODEL = "paste_current_model_name_here"
```

Then launch VS Code or Jupyter from that same PowerShell window.

### Windows PowerShell: Gemini

```powershell
$env:LAB_THREE_PROVIDER = "gemini"
$env:GEMINI_API_KEY = "paste_key_here"
$env:GEMINI_MODEL = "gemini-2.5-flash"
```

Then launch VS Code or Jupyter from that same PowerShell window.

## Persistent Setup

Use this if you want the variables to survive after closing the terminal.

### macOS/Linux: OpenAI

Add lines like these to your shell profile, usually `~/.zshrc` on recent macOS or `~/.bashrc` on many Linux systems:

```bash
export LAB_THREE_PROVIDER="openai"
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

### macOS/Linux: Gemini

```bash
export LAB_THREE_PROVIDER="gemini"
export GEMINI_API_KEY="paste_key_here"
export GEMINI_MODEL="gemini-2.5-flash"
```

Then restart the terminal or source your shell profile.

### Windows PowerShell: OpenAI

```powershell
setx LAB_THREE_PROVIDER "openai"
setx OPENAI_API_KEY "paste_key_here"
setx OPENAI_MODEL "paste_current_model_name_here"
```

After `setx`, open a new terminal and restart VS Code or Jupyter.

### Windows PowerShell: Gemini

```powershell
setx LAB_THREE_PROVIDER "gemini"
setx GEMINI_API_KEY "paste_key_here"
setx GEMINI_MODEL "gemini-2.5-flash"
```

After `setx`, open a new terminal and restart VS Code or Jupyter.

## Conda Setup Option

If you use conda and want these variables to appear whenever a specific conda environment is activated:

### OpenAI

```bash
conda activate lcds-python
conda env config vars set LAB_THREE_PROVIDER="openai"
conda env config vars set OPENAI_API_KEY="paste_key_here"
conda env config vars set OPENAI_MODEL="paste_current_model_name_here"
conda deactivate
conda activate lcds-python
```

### Gemini

```bash
conda activate lcds-python
conda env config vars set LAB_THREE_PROVIDER="gemini"
conda env config vars set GEMINI_API_KEY="paste_key_here"
conda env config vars set GEMINI_MODEL="gemini-2.5-flash"
conda deactivate
conda activate lcds-python
```

Then restart VS Code or Jupyter and select the `lcds-python` kernel.

## Check Setup

Run this in the same terminal that will launch VS Code or Jupyter.

### OpenAI

```bash
python -c "import os; print(os.getenv('LAB_THREE_PROVIDER')); print(os.getenv('OPENAI_API_KEY') is not None); print(os.getenv('OPENAI_MODEL'))"
```

Expected output:

```text
openai
True
your_openai_model_name
```

### Gemini

```bash
python -c "import os; print(os.getenv('LAB_THREE_PROVIDER')); print(os.getenv('GEMINI_API_KEY') is not None); print(os.getenv('GEMINI_MODEL'))"
```

Expected output:

```text
gemini
True
your_gemini_model_name
```

In a notebook, run:

```python
import os

print("Provider:", os.getenv("LAB_THREE_PROVIDER"))
print("OpenAI key:", os.getenv("OPENAI_API_KEY") is not None)
print("OpenAI model:", os.getenv("OPENAI_MODEL"))
print("Gemini key:", os.getenv("GEMINI_API_KEY") is not None)
print("Gemini model:", os.getenv("GEMINI_MODEL"))
```

## If the Notebook Still Says a Variable Is Missing

If the terminal check works but the notebook says the key or model is missing, the notebook kernel did not inherit the terminal environment.

This usually happens when:

- VS Code or Jupyter was already open before you ran `export`, `$env:...`, or `setx`;
- VS Code was opened from the desktop launcher instead of from the terminal;
- the notebook kernel was started before the variables existed;
- the variables were set in one terminal, but Jupyter was launched from another terminal;
- `LAB_THREE_PROVIDER` says `openai` but only Gemini variables are set, or the reverse.

Fix:

1. Fully close VS Code or Jupyter.
2. Open a terminal.
3. Set or confirm your provider variables.
4. Launch VS Code or Jupyter from that same terminal.
5. Restart the notebook kernel.
6. Rerun the setup cells.

## Before Running Lab Three

Use this checklist:

- I am using synthetic teaching prompts, not sensitive data.
- I understand that remote API calls may cost money or consume quota.
- I have set a low `max_output_tokens` value in lab calls.
- I have set either OpenAI variables or Gemini variables.
- I have restarted the notebook kernel after setting environment variables.
- I know how to revoke the key if it leaks.
- I know which provider and model I am using and will record both in my notes.

## Removing Keys

macOS/Linux, current session:

```bash
unset LAB_THREE_PROVIDER
unset OPENAI_API_KEY
unset OPENAI_MODEL
unset GEMINI_API_KEY
unset GEMINI_MODEL
```

Windows PowerShell, persistent user variables:

```powershell
[Environment]::SetEnvironmentVariable("LAB_THREE_PROVIDER", $null, "User")
[Environment]::SetEnvironmentVariable("OPENAI_API_KEY", $null, "User")
[Environment]::SetEnvironmentVariable("OPENAI_MODEL", $null, "User")
[Environment]::SetEnvironmentVariable("GEMINI_API_KEY", $null, "User")
[Environment]::SetEnvironmentVariable("GEMINI_MODEL", $null, "User")
```

Also revoke exposed keys in the provider dashboard.

## Expected Lab Three Errors

Lab Three is designed to fail loudly when setup is wrong.

Common causes:

- `LAB_THREE_PROVIDER` is misspelled;
- missing provider API key;
- missing provider model variable;
- model name is misspelled or unavailable to your account;
- account has no billing, credit, or quota;
- selected model does not support a parameter used in a later exercise;
- network connection fails;
- the API call times out before the full response is received;
- a structured-output prompt returns invalid JSON.

When this happens, read the traceback and fix the underlying setup, request, or prompt.

## If a Request Times Out

A timeout means the notebook sent the request but did not receive a complete response before the timeout limit. This can happen because of network instability, provider delay, or a batch cell making several calls.

Lab Three defines this setting near the top:

```python
API_TIMEOUT_SECONDS = 240
```

If a timeout happens:

1. Rerun the same cell once.
2. Check your internet connection.
3. Reduce `max_output_tokens` or run fewer batch examples.
4. Increase `API_TIMEOUT_SECONDS`, then rerun the setup cells.
