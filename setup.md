# Pre-Arrival Setup Guide

[Back to course page](../)

Please complete this setup before the first day of class. The required tools are **Git**, **Anaconda Python**, and **VS Code**.

Lab Four compares and tunes locally hosted language models. It now requires Ollama and locally downloaded model weights. The notebook checks for Ollama and pulls the required models by default.

## Before You Start

- Have admin access on your laptop.
- Keep at least 8--10 GB free disk space for the required course tools.
- If you want to try Lab Four with a real local model, keep an extra 2--5 GB free for small model downloads.
- Use a stable internet connection.
- If you get stuck, do not worry. Bring your laptop and we will help.

## 1. Install Git

Git is the version control tool we will use to download and manage course materials.

### Windows

1. Download Git from [git-scm.com/download/win](https://git-scm.com/download/win).
2. Run the installer and keep the default options.
3. Open `Git Bash` or PowerShell.

Check installation:

```bash
git --version
```

### macOS

1. Open the Terminal app.
2. Run this command:

```bash
xcode-select --install
```

This installs Apple command line tools, including Git.

Check installation:

```bash
git --version
```

### Linux

Use the command for your distribution:

```bash
# Ubuntu / Debian
sudo apt update
sudo apt install -y git

# Fedora
sudo dnf install -y git

# Arch
sudo pacman -S --needed git
```

Check installation:

```bash
git --version
```

### Optional Git Configuration

Recommended: run once.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## 2. Install Anaconda Python

Anaconda gives you Python plus common data science tools in one installer. Download it from [anaconda.com/download](https://www.anaconda.com/download).

### Windows

1. Download the 64-bit graphical installer for Windows.
2. Run the installer with `Just Me` selected.
3. Keep default options. You can leave **Add Anaconda to my PATH** unchecked.
4. Open `Anaconda Prompt` after install.

### macOS

1. Choose the correct installer: `Apple Silicon` for M1/M2/M3/M4, or `Intel`.
2. Run the package installer.
3. Open Terminal after install.

### Linux

1. Download the Linux installer script from Anaconda.
2. From terminal, run:

```bash
bash ~/Downloads/Anaconda3-*-Linux-*.sh
```

3. Accept defaults and answer `yes` when asked to run `conda init`.
4. Close and reopen terminal.

### Check Anaconda Installation

Use `Anaconda Prompt` on Windows, or Terminal on macOS/Linux.

```bash
conda --version
python --version
jupyter --version
```

### Create a Course Environment

Recommended:

```bash
conda create -n lcds-python python=3.12 -y
conda activate lcds-python
python -c "print('Python works')"
```

### Install Course Python Packages

After activating the course environment, install the packages used by the notebooks:

```bash
python -m pip install -r requirements.txt
```

Check that the main packages import correctly:

```bash
python -c "import pandas, sklearn, jupyter; print('Course packages work')"
```

### Open and Run the Notebooks

After installing the packages:

1. Open VS Code.
2. Choose `File` then `Open Folder`.
3. Open this course folder.
4. Open `Labs/Lab_One.ipynb`.
5. Click `Select Kernel` in the top-right of the notebook.
6. Choose the `lcds-python` environment.
7. Run the first code cell with the play button or `Shift+Enter`.

Run notebook cells from top to bottom. If you skip earlier cells, later cells may fail because variables have not been created yet.

If Python imports fail inside the notebook but worked in the terminal, check that the notebook kernel is `lcds-python`. This is the most common setup problem.

### If You Are New to Notebooks

Read [`BEGINNER_GUIDE.md`](./BEGINNER_GUIDE.md) before starting Lab One. It explains cells, kernels, common errors, and how to use the solution notebooks.

When you are done testing:

```bash
conda deactivate
```

## 3. Install VS Code

VS Code is the editor we recommend for writing and running code.

### Windows, macOS, and Linux

1. Download VS Code from [code.visualstudio.com](https://code.visualstudio.com/).
2. Install it normally for your operating system.
3. Open VS Code, then install these extensions:
   - `Python` by Microsoft
   - `Jupyter` by Microsoft

### Check VS Code Installation

In terminal or PowerShell, run:

```bash
code --version
```

If macOS says `code: command not found`:

1. Open VS Code.
2. Press `Cmd+Shift+P`.
3. Run: `Shell Command: Install 'code' command in PATH`.
4. Restart terminal and run `code --version` again.

## 4. Required for Lab Four: Prepare a Local LLM Runtime

Lab Four now focuses on comparing small local models, tuning parameters, and evaluating outputs. The required runtime for the notebook is **Ollama**, because it is simple to install and exposes a local API that Python can call.

This section is no longer optional for running Lab Four. The notebook can pull missing model weights itself. It can also attempt an automatic Ollama install on Linux, but macOS and Windows users should still install Ollama with the normal app installer before class.

### Install Ollama

Download Ollama from [ollama.com/download](https://ollama.com/download).

On Linux, the official install command is currently:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

On macOS and Windows, use the installer from the download page unless the instructor tells you otherwise. GUI installers are more reliable than trying to install the desktop app from inside Jupyter.

After installation, close and reopen your terminal. Then check:

```bash
ollama --version
```

If this says `command not found` or `not recognized`, Ollama is either not installed or the terminal cannot find it yet.

If `ollama --version` works in a terminal but Lab Four still says Ollama is unavailable, restart VS Code/Jupyter and rerun the notebook setup preamble. If it still fails, open this repository from the same terminal where the command works:

```bash
code .
```

Then select the same Python/Jupyter environment for the notebook.

### Models Used in Lab Four

Lab Four uses these Ollama model tags and pulls missing models by default from inside the notebook:

```bash
ollama pull smollm2:360m
ollama pull qwen3:0.6b
ollama pull llama3.2:1b
```

Approximate download sizes used in the lab notebook:

- `smollm2:360m`: about 0.7 GB;
- `qwen3:0.6b`: about 0.5 GB;
- `llama3.2:1b`: about 1.3 GB.

The notebook can pull these for you. It also smoke-tests each pulled model before the comparison section and skips a candidate if its local runner crashes. The commands above are useful if you want to prepare them before class.

### Run One Terminal Test

After the model downloads, run:

```bash
ollama run smollm2:360m
```

Paste a tiny synthetic prompt, for example:

```text
Classify this public comment as access_barrier, housing_stress, health_need, or other.
Comment: The evening bus was cancelled and I missed my diabetes clinic appointment.
Return only the label.
```

Do not paste confidential, patient, client, or service-user data into a local model during setup.

### Check the Local Server

Ollama usually serves a local API at:

```text
http://localhost:11434/api
```

Lab Four pulls missing model weights by default using:

```python
AUTO_PULL_MISSING_MODELS = True
```

On Linux, Lab Four can also attempt the Ollama runtime install from inside the notebook using:

```python
INSTALL_OLLAMA_IF_MISSING = True
```

Run the lab only after:

- Ollama is installed or you are ready for the notebook to attempt a Linux install;
- the notebook can see the `ollama` command after installation;
- you are using synthetic or approved de-identified text;
- you understand that prompts and outputs may still appear in local logs or caches.

### LM Studio Alternative

If you prefer a graphical application, you can use [LM Studio](https://lmstudio.ai/) instead. It can download local models and start a local server. The Lab Four notebook is written around Ollama for simplicity, but the lecture explains how LM Studio fits into the same local-runtime idea.

### Local Model Troubleshooting

- **`ollama` command not found:** on Linux, rerun the setup cells and check the automatic install output; on macOS or Windows, reinstall/open Ollama and restart VS Code/Jupyter.
- **Model not found:** run `ollama pull smollm2:360m` and check the model tag spelling.
- **Connection refused:** Ollama is not running, or the local server is not available.
- **Laptop becomes slow:** stop the model, use a smaller model, and avoid long prompts.
- **Not enough disk space:** remove unused local models or free enough space before running Lab Four.

## 5. Final Full-System Check

Run the commands below in terminal, or Anaconda Prompt on Windows:

```bash
git --version
conda --version
python --version
jupyter --version
code --version
```

You should see version numbers for all five commands and no errors.

For Lab Four, also run:

```bash
ollama --version
ollama list
```

`ollama list` should show any models you have downloaded, such as `smollm2:360m`. If the list is empty, the Lab Four setup cell should pull the required models when you run it.

### Optional Quick Coding Test

```bash
conda activate lcds-python
python -c "print('Setup complete')"
```

## Troubleshooting

- **Command not found:** close and reopen terminal, then retry.
- **Still failing on Windows:** run commands in `Anaconda Prompt` instead of PowerShell.
- **Still failing on macOS:** restart Terminal after installation.
- **Linux permissions issue:** confirm you used `sudo` for package install commands.
- **Notebook cannot find a package:** select the `lcds-python` kernel and rerun the cell.
- **Notebook output looks inconsistent:** restart the kernel, then run cells from the top.
- **A data download fails:** skip the optional download cell and continue with the built-in examples, unless the instructor says otherwise.

> If anything does not work, bring your laptop to the course anyway. We will run a setup support session before teaching starts.
