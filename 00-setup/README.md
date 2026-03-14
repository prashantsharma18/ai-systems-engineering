# Environment Setup — WSL Prerequisites

Reference guide for setting up the Python development environment for this repo from scratch.
Written for **WSL2 (Ubuntu 20.04+) on Windows 10/11**.

---

## 1. Windows & WSL Prerequisites

Before running any commands below, ensure:

- **Windows 10 (21H2+) or Windows 11** with WSL2 enabled
- **Ubuntu 20.04 or later** installed from the Microsoft Store
- **VSCode** with the [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) extension (`ms-vscode-remote.remote-wsl`)
- **Git configured in WSL:**

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

> All subsequent steps run inside a WSL terminal, not Windows PowerShell or CMD.

---

## 2. `uv` — Python Version & Package Manager

**Why:** `uv` replaces `pip` + `venv` + `pyenv` with a single, fast tool. It manages Python versions and virtual environments. Used throughout this curriculum.

**Install:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc          # or restart the terminal
uv --version              # should show 0.x.x
```

**If `uv` is not found after install**, add it to PATH manually:
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

---

## 3. Python 3.11

**Why:** Python 3.11 is the target version for this curriculum. It has the best compatibility with PyTorch, HuggingFace, scikit-learn, and all curriculum dependencies. Do **not** use Ubuntu's system Python (3.8) — it is too old and leaks into the environment.

**Install via uv:**
```bash
uv python install 3.11
uv python list            # verify cpython-3.11.x appears
```

---

## 4. Project Virtual Environment

**Why:** Isolates all packages from the system Python. Every curriculum topic runs inside this venv.

**Create and activate:**
```bash
cd ~/projects/ai-systems-engineering
uv venv .venv --python 3.11
source .venv/bin/activate
python --version          # must show 3.11.x
```

**To activate in future sessions:**
```bash
source ~/projects/ai-systems-engineering/.venv/bin/activate
```

> `.venv/` is in `.gitignore`. If you clone the repo fresh, re-run steps 4–6 to recreate it.

---

## 5. Learning Dependencies

**Why each package is needed:**

| Package | Topics | Why |
|---------|--------|-----|
| `jupyter`, `jupyterlab` | 1–16 | Interactive notebooks — the primary learning environment |
| `ipykernel` | 1–16 | Registers the venv as a Jupyter kernel so notebooks use Python 3.11 |
| `numpy` | 15, capstone | Numerical arrays — the foundation all ML sits on |
| `pandas` | 16, capstone | Tabular data loading, cleaning, and feature engineering |
| `matplotlib` | 15–16 | Data visualization for EDA |
| `pytest` | 6 | Testing framework — writing and running tests |
| `pytest-cov` | 6 | Coverage reports alongside pytest |
| `mypy` | 5 | Static type checking — catching type errors before runtime |
| `pyyaml` | 8, 11 | Loading and writing YAML config files |
| `python-dotenv` | 8 | Loading `.env` files — never hardcode API keys |
| `joblib` | 11, 13 | ML-optimized serialization and parallelism |
| `httpx` | 10 | Async HTTP client for inference API calls |
| `line-profiler` | 14 | Line-by-line profiling to find hot loops |
| `memory-profiler` | 14 | Line-by-line memory usage — find the allocation that doubles your RAM |
| `python-json-logger` | 7 | Structured JSON log output (CloudWatch / Datadog ready) |
| `rich` | all | Pretty tracebacks and terminal output |

**Install all at once:**
```bash
uv pip install \
  jupyter jupyterlab ipykernel \
  numpy pandas matplotlib \
  pytest pytest-cov \
  mypy \
  pyyaml python-dotenv \
  joblib \
  httpx \
  line-profiler memory-profiler \
  python-json-logger \
  rich
```

---

## 6. Jupyter Kernel Registration

**Why:** Registers the `.venv` as a named kernel. VSCode and JupyterLab will then use Python 3.11 from the venv — not system Python — when opening notebooks.

```bash
python -m ipykernel install --user \
  --name ai-systems \
  --display-name "AI Systems (Python 3.11)"

jupyter kernelspec list   # "ai-systems" should appear in the list
```

---

## 7. VSCode Configuration

**Why:** Tells VSCode which interpreter to use, auto-activates the venv in the integrated terminal, and sets Ruff as the Python formatter.

The file `.vscode/settings.json` is already committed to this repo:

```json
{
  "python.defaultInterpreterPath": "${workspaceFolder}/.venv/bin/python",
  "python.terminal.activateEnvironment": true,
  "editor.formatOnSave": true,
  "[python]": {
    "editor.defaultFormatter": "charliermarsh.ruff"
  }
}
```

**Required VSCode extensions** — install via the Extensions panel (`Ctrl+Shift+X`) or the command below:

```bash
code --install-extension ms-python.python
code --install-extension ms-toolsai.jupyter
code --install-extension ms-python.vscode-pylance
code --install-extension charliermarsh.ruff
code --install-extension ms-vscode-remote.remote-wsl
```

> Always open VSCode from WSL with `code .`, not by launching it from Windows. This ensures the Remote-WSL extension activates and all paths resolve correctly.

---

## 8. Smoke Test

Run these after completing all steps above to confirm everything is working:

```bash
source ~/projects/ai-systems-engineering/.venv/bin/activate

python --version
# Expected: Python 3.11.x

python -c "import numpy, pandas, pytest; print('All good')"
# Expected: All good

jupyter kernelspec list
# Expected: ai-systems listed at ~/.local/share/jupyter/kernels/ai-systems
```

---

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| `uv: command not found` | `export PATH="$HOME/.local/bin:$PATH"` then `source ~/.bashrc` |
| `python --version` shows 3.8 | Venv not activated — run `source .venv/bin/activate` |
| Notebook shows wrong kernel | Select "AI Systems (Python 3.11)" in the kernel picker (top right in VSCode) |
| `ModuleNotFoundError` in notebook | Confirm the notebook is using the `ai-systems` kernel, not `python3` |
| VSCode can't find interpreter | Close VSCode, reopen from WSL with `code .` |
