# Day 0: Professional Local Environment Setup & Configuration Guide

**Programme:** 23-Day Applied Data Science, AI/ML & Generative AI  
**Runtime Baseline:** Python 3.12.x (Local Workstation Baseline)  
**IDE & Workflow:** Visual Studio Code (VS Code) + Jupyter Extension + Isolated Virtual Environment (`.venv`)  
**Objective:** Establish an authentic, enterprise-grade data science development environment on each student's physical machine.

---

## 1. Why Python 3.12.x and 100% Local?

1. **Production Parity:** Enterprise ML platforms (AWS SageMaker, Azure ML, GCP Vertex AI, Databricks, Docker bases) target stable LTS releases (3.11/3.12). 
2. **Binary Compatibility:** Pre-compiled C/C++ binary wheels for foundational libraries (`torch`, `faiss-cpu`, `tokenizers`, `scipy`) are fully stable for 3.12, avoiding missing compiler errors on student machines.
3. **Engineering Rigour:** Real-world data teams use local IDEs, project folder structures, terminal commands, virtual environments, Git workflows, and local servers (`localhost:8501` for Streamlit), rather than disposable browser runtimes.

---

## 2. Standard Enterprise Project Structure

Before installing libraries, every student must create a dedicated project directory. Open terminal (macOS/Linux) or PowerShell (Windows) and create:

```bash
# Create and navigate to the project directory
mkdir ds-aiml-workspace
cd ds-aiml-workspace
```

The resulting folder structure across the 23-day programme will look like this:

```text
ds-aiml-workspace/
├── .venv/                      # Isolated Python 3.12 virtual environment (do not commit to git)
├── data/
│   ├── raw/                    # Static datasets (Housing, Telco Churn, Segmentation)
│   └── processed/              # Cleaned datasets and feature matrices
├── notebooks/                  # Day 01 to Day 21 Jupyter notebooks
│   ├── day04_linear_regression.ipynb
│   ├── day05_logistic_regression.ipynb
│   ├── day13_ann_pytorch.ipynb
│   └── day21_lean_rag.ipynb
├── src/
│   ├── __init__.py
│   └── app.py                  # Day 22 Streamlit application
├── models/                     # Saved artifacts (.joblib, .pkl, .pt)
├── requirements.txt            # Pinned package specifications
├── smoke_test.py               # Pre-flight environment diagnostic script
└── .gitignore
```

---

## 3. Installation Pathways

Choose **Path A** if Python is not yet installed. Choose **Path B** if Python (such as 3.13.x or 3.10.x) is already on the computer.

---

### Path A: Student Has Never Installed Python

#### Step A1: Download and Install Python 3.12

* **Windows:**
  1. Visit the official Python release page: [python.org/downloads](https://www.python.org/downloads/)
  2. Download the latest **Python 3.12.x Windows installer (64-bit)**.
  3. Run the installer.
  4. **CRITICAL CHECKBOX:** At the bottom of the first setup screen, check the box:  
     `[X] Add python.exe to PATH`
  5. Select **Install Now**.
  6. On the final screen, click **Disable path length limit** (if prompted), then click **Close**.

* **macOS:**
  1. Download the latest **Python 3.12.x macOS 64-bit universal2 installer** from [python.org/downloads](https://www.python.org/downloads/).
  2. Run the `.pkg` installer and follow the default prompts.
  3. Once finished, open **Finder** $\to$ **Applications** $\to$ **Python 3.12** and double-click `Install Certificates.command` (this fixes local SSL verification issues when downloading datasets/models).

* **Linux (Ubuntu/Debian):**
  ```bash
  sudo apt update
  sudo apt install software-properties-common -y
  sudo add-apt-repository ppa:deadsnakes/ppa -y
  sudo apt update
  sudo apt install python3.12 python3.12-venv python3.12-dev -y
  ```

#### Step A2: Verify the Installation

Open a fresh terminal or PowerShell window and run:

```bash
python --version
# Expected output: Python 3.12.x
```

*(On macOS/Linux, if `python` points to an older system binary, use `python3.12 --version`)*

---

### Path B: Machine Already Has Python (Configuring 3.12.x in Parallel)

If the computer already has Python 3.13.x, 3.10.x, or an Anaconda distribution, you do not need to uninstall it. Install Python 3.12 side-by-side and create the environment targeting 3.12 explicitly.

#### Step B1: Install Python 3.12 Alongside Existing Versions

* **Windows (Using the Official Python Launcher):**
  1. Download and run the **Python 3.12.x 64-bit installer** from [python.org](https://www.python.org/downloads/).
  2. Uncheck `"Add python.exe to PATH"` to avoid overriding your primary default Python command, but keep the **py launcher** enabled.
  3. Complete installation.

* **macOS (Using Homebrew or Installer):**
  * Using Homebrew:
    ```bash
    brew install python@3.12
    ```
  * Or install the official `.pkg` from [python.org](https://www.python.org/downloads/) (installed to `/Library/Frameworks/Python.framework/Versions/3.12/`).

* **Linux (Ubuntu):**
  ```bash
  sudo add-apt-repository ppa:deadsnakes/ppa -y
  sudo apt update
  sudo apt install python3.12 python3.12-venv python3.12-dev -y
  ```

#### Step B2: Verify the Python 3.12 Command

Check that Python 3.12 is selectable:

* **Windows (PowerShell):**
  ```powershell
  py -3.12 --version
  # Output: Python 3.12.x
  ```
* **macOS / Linux:**
  ```bash
  python3.12 --version
  # Output: Python 3.12.x
  ```

---

## 4. Virtual Environment Creation & Activation

Navigate into `ds-aiml-workspace` and create an isolated virtual environment named `.venv`.

### Scenario 1: For Path A (Single Default Python 3.12)

```bash
# Windows / macOS / Linux:
python -m venv .venv
```

### Scenario 2: For Path B (Targeting 3.12 Explicitly)

* **Windows (PowerShell):**
  ```powershell
  py -3.12 -m venv .venv
  ```
* **macOS / Linux:**
  ```bash
  python3.12 -m venv .venv
  ```

---

### Activating the Environment

Run this every time you open a new terminal window:

* **Windows (PowerShell):**
  ```powershell
  .venv\Scripts\Activate.ps1
  ```
  *(If PowerShell displays an `Execution_Policies` script restriction error, run: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`, then re-run the activate command).*

* **Windows (Command Prompt `cmd`):**
  ```cmd
  .venv\Scripts\activate.bat
  ```

* **macOS / Linux (bash/zsh):**
  ```bash
  source .venv/bin/activate
  ```

**Success check:** Your command prompt will display `(.venv)` at the beginning of the line. Check version inside the environment:

```bash
python --version
# MUST output: Python 3.12.x
```

---

## 5. Visual Studio Code Configuration

1. **Install VS Code:** Download from [code.visualstudio.com](https://code.visualstudio.com/).
2. **Install Required Extensions:**
   * Open VS Code, press `Ctrl+Shift+X` (or `Cmd+Shift+X` on macOS).
   * Search and install:
     * **Python** (by Microsoft)
     * **Jupyter** (by Microsoft)
3. **Open Project Folder:**
   * Click **File** $\to$ **Open Folder...** $\to$ Select `ds-aiml-workspace`.
4. **Select Kernel / Interpreter:**
   * Press `Ctrl+Shift+P` (or `Cmd+Shift+P`), type: `Python: Select Interpreter`.
   * Choose: `Python 3.12.x ('.venv': venv) ./.venv/bin/python` (or `.\.venv\Scripts\python.exe`).

---

## 6. Pinned Dependencies Installation (`requirements.txt`)

Save the following content into a file named `requirements.txt` inside `ds-aiml-workspace`:

```text
# --- Numerical & Core Data Handling (Days 1–11) ---
numpy>=1.26.0,<2.0.0
pandas>=2.1.0,<2.3.0
scipy>=1.11.0,<1.14.0
statsmodels>=0.14.0

# --- Visualisation ---
matplotlib>=3.8.0,<3.10.0
seaborn>=0.13.0

# --- Traditional Machine Learning ---
scikit-learn>=1.4.0,<1.6.0
joblib>=1.3.0

# --- Deep Learning (CPU Baseline / Pre-compiled for 3.12) ---
torch>=2.2.0,<2.4.0
torchvision>=0.17.0,<0.19.0

# --- NLP, Pretrained Models & Embeddings (Days 18–21) ---
nltk>=3.8.0
transformers>=4.38.0,<4.43.0
sentence-transformers>=2.5.0,<3.0.0
huggingface-hub>=0.21.0

# --- Local Vector Search (Day 21 Lean RAG) ---
faiss-cpu>=1.8.0

# --- Web UI & Local Model Serving (Day 22) ---
streamlit>=1.32.0,<1.38.0

# --- Interactive Notebook Runtime ---
jupyter>=1.0.0
ipykernel>=6.29.0
```

With your `(.venv)` activated in the terminal, run:

```bash
# Upgrade installation toolchain
python -m pip install --upgrade pip setuptools wheel

# Install pinned dependencies
pip install -r requirements.txt
```

---

## 7. Pre-Flight Verification Script (`smoke_test.py`)

Create `smoke_test.py` in the workspace root and run it to verify all modules:

```python
"""
Day 0 Diagnostic Smoke Test
Checks all functional modules across the 23-day syllabus on Python 3.12.
"""
import sys

def run_checks():
    print("=" * 65)
    print("RUNNING DAY 0 ENVIRONMENT SMOKE TEST (LOCAL PYTHON 3.12)")
    print("=" * 65)
    
    # Check Python version
    v = sys.version_info
    print(f"Active Interpreter: Python {v.major}.{v.minor}.{v.micro}")
    if v.major != 3 or v.minor != 12:
        print("[WARNING] Active Python is NOT 3.12.x! Issues may arise with C-extensions.")
    else:
        print("[PASS] Python version is strictly 3.12.x")

    # Check Core DS / ML
    try:
        import numpy as np
        import pandas as pd
        from sklearn.linear_model import LogisticRegression
        from sklearn.metrics import f1_score
        
        X = np.array([[10, 20], [20, 30], [30, 40], [40, 50]])
        y = np.array([0, 0, 1, 1])
        model = LogisticRegression().fit(X, y)
        preds = model.predict(X)
        _ = f1_score(y, preds)
        print("[PASS] Modules 1 & 2: NumPy, Pandas, Scikit-Learn")
    except Exception as e:
        print(f"[FAIL] Modules 1 & 2 (Scikit-Learn/Data): {e}")

    # Check PyTorch Local CPU Execution
    try:
        import torch
        import torch.nn as nn
        
        net = nn.Sequential(nn.Linear(2, 4), nn.ReLU(), nn.Linear(4, 1))
        x = torch.randn(2, 2)
        out = net(x)
        assert out.shape == (2, 1)
        cuda_status = "CUDA GPU Available" if torch.cuda.is_available() else "Local CPU Mode"
        print(f"[PASS] Module 3: PyTorch ({torch.__version__} - {cuda_status})")
    except Exception as e:
        print(f"[FAIL] Module 3 (PyTorch): {e}")

    # Check NLP, Sentence Transformers & FAISS
    try:
        from sentence_transformers import SentenceTransformer
        import faiss
        
        # Load lightweight embeddings model
        embedder = SentenceTransformer("all-MiniLM-L6-v2")
        vectors = embedder.encode(["Customer churn inquiry", "Technical product question"])
        
        # Build 384-dimensional FAISS index
        dim = vectors.shape[1]
        index = faiss.IndexFlatL2(dim)
        index.add(vectors.astype("float32"))
        assert index.ntotal == 2
        print("[PASS] Module 4: Sentence Transformers & FAISS (Lean RAG Ready)")
    except Exception as e:
        print(f"[FAIL] Module 4 (NLP / Embeddings / Vector Search): {e}")

    # Check Streamlit (Day 22 Deployment)
    try:
        import streamlit as st
        import joblib
        print(f"[PASS] Module 5: Streamlit (v{st.__version__}) & Joblib Artifact Serializer")
    except Exception as e:
        print(f"[FAIL] Module 5 (Streamlit/Deployment): {e}")

    print("=" * 65)
    print("VERIFICATION COMPLETE. WORKSTATION READY FOR DAY 1.")
    print("=" * 65)

if __name__ == "__main__":
    run_checks()
```

Run the script from your terminal:

```bash
python smoke_test.py
```

If every module reports `[PASS]`, the student machine is completely configured for the course.

---

## 8. Emergency Classroom Fallback Rules

* **If a student's personal laptop encounters an operating system lock:**  
  Switch that specific student to **Google Colab** using the Day 0 Colab setup as a temporary measure.
* **Streamlit Testing (Day 22):**  
  Run directly in the local terminal:
  ```bash
  streamlit run src/app.py
  ```
  It will automatically serve on `http://localhost:8501` without requiring complex networking, proxies, or reverse tunnels.