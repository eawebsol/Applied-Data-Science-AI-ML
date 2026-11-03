# Day 0: Professional Development Environment Setup & Configuration Guide

**Programme:** Educentriks — 23-Day Applied Data Science, AI/ML & Generative AI  
**Brand tagline:** From Learning to Real-World Application  
**Python baseline:** Python 3.13.x (64-bit), subject to the course compatibility validation described in this guide  
**IDE and workflow:** Visual Studio Code (VS Code) + Python and Jupyter extensions + isolated virtual environment (`.venv`)  
**Primary approach:** Local-first development, with Google Colab as an approved alternative  
**Objective:** Establish a consistent, reproducible development environment for the practical work covered throughout the programme.

---

## Before You Begin: Important Course Standards

This guide uses the previously agreed course baseline of **Python 3.13.x (64-bit)**. The submitted draft used Python 3.12.x; this revision aligns the instructions with the earlier course decision.

Before distributing the final package requirements to a full batch, the course maintainer must validate the complete package stack on a clean Python 3.13 installation. If a required library has a blocking compatibility issue, the course baseline should be reconsidered deliberately and changed consistently across this guide, the requirements file, notebooks and smoke test. Do not mix Python 3.12 and 3.13 instructions.

The package list in this guide is a **dependency checklist, not a final lockfile**. Exact package versions must be pinned only after compatibility testing. Do not interpret version ranges or unpinned package names as a reproducible, tested environment.

---

## 1. Why a Standard, Local-First Environment?

A consistent environment helps every learner run the same notebooks, reproduce demonstrations and troubleshoot problems using a known configuration.

### 1.1 Why standardize the Python version?

The programme uses Python 3.13.x as its planned baseline because a shared interpreter version makes classroom support, notebook execution and dependency management more consistent.

Python releases do not use the same formal “LTS” designation commonly associated with some operating systems or enterprise distributions. Python versions have defined release and maintenance lifecycles. The appropriate version for a project depends on the support status of the interpreter, the compatibility of required libraries and the deployment environment.

For this programme, the final decision must be supported by a clean installation test of the complete stack, including:

- NumPy, pandas and SciPy
- Matplotlib and Seaborn
- scikit-learn and statsmodels
- PyTorch and torchvision
- Transformers and Sentence Transformers
- FAISS, where supported on the student's operating system
- Jupyter and ipykernel
- Streamlit

### 1.2 Why local-first development?

Local development gives students experience with common professional workflows:

- Working with project folders and source files
- Creating and activating isolated Python environments
- Installing and managing dependencies
- Running Jupyter notebooks through a local IDE
- Debugging code and interpreting errors
- Running a local application, such as Streamlit
- Using Git and GitHub to manage learning materials and code

**Local-first does not mean local-only.** Google Colab is an approved alternative when a student's computer has installation restrictions, insufficient resources or a package compatibility problem. Colab may also provide access to an optional accelerator, subject to availability and usage limits.

### 1.3 Standard tools

| Tool | Purpose |
|---|---|
| Python 3.13.x, 64-bit | Course programming language |
| Visual Studio Code | Main development environment |
| Python extension for VS Code | Interpreter selection, execution and debugging |
| Jupyter extension for VS Code | Notebook editing and execution |
| `venv` | Isolated project environment |
| Jupyter / ipykernel | Notebook runtime and kernel |
| Git and GitHub | Version control and course repository access |
| Google Colab | Alternative cloud notebook environment |

---

## 2. Standard Project Folder Structure

Create a dedicated working folder for the programme. This folder is the student's local workspace; it is separate from the centrally maintained Educentriks GitHub course repository.

### 2.1 Create the project directory

Open PowerShell or Command Prompt on Windows, or Terminal on macOS/Linux:

```bash
mkdir ds-aiml-workspace
cd ds-aiml-workspace
```

### 2.2 Recommended structure

```text
ds-aiml-workspace/
│
├── .venv/                         # Local virtual environment; never commit
│
├── data/
│   ├── raw/                       # Original downloaded datasets
│   └── processed/                 # Cleaned or transformed data
│
├── notebooks/                     # Working copies of course notebooks
│   ├── day01_foundations.ipynb
│   ├── day04_linear_regression.ipynb
│   ├── day05_logistic_regression.ipynb
│   ├── day13_ann_pytorch.ipynb
│   └── day21_lean_rag.ipynb
│
├── src/                            # Reusable Python source code
│   ├── __init__.py
│   └── app.py                      # Example Streamlit application
│
├── models/                         # Locally saved model artifacts
│
├── outputs/                        # Charts, predictions and exported results
├── reports/                        # Analysis reports and project documentation
│
├── requirements.txt                # Maintainer-approved package versions
├── smoke_test.py                   # Environment diagnostic script
└── .gitignore                      # Excludes local and generated files
```

The example notebook names are illustrative. Students should use the actual filenames supplied in each day's course folder.

### 2.3 Folder usage guidelines

- `data/raw/`: Keep original downloaded datasets unchanged.
- `data/processed/`: Store cleaned or transformed copies.
- `notebooks/`: Keep working copies of the course notebooks and personal experiments.
- `src/`: Store reusable Python modules and application code.
- `models/`: Store model artifacts generated during exercises. Large artifacts should not be committed to GitHub.
- `outputs/`: Store generated charts, predictions and exports.
- `reports/`: Store written findings and project documentation.
- `.venv/`: Contains the local Python environment. It must not be uploaded to GitHub.

### 2.4 Git and data safety

Do not commit the following to GitHub:

- `.venv/` or any other virtual environment
- API keys, passwords, access tokens or `.env` files
- Confidential or personally identifiable information
- Large datasets unless the dataset licence and repository policy explicitly permit it
- Large model weights or generated artifacts

The Educentriks student repository provides learning materials. Students should use their own local workspace for experiments and generated files.

---

## 3. Python Installation

Choose the pathway that matches your computer.

- **Path A:** Python is not installed.
- **Path B:** Another Python version is already installed.

You do not need to uninstall an existing Python installation. Multiple Python versions can coexist when the correct interpreter is selected for each project.

### 3.1 Path A — Python is not installed

#### Windows 10/11

1. Visit the official Python website: <https://www.python.org/downloads/>.
2. Open the Python 3.13 release downloads and select the appropriate **Windows installer (64-bit)**.
3. Run the installer.
4. If the installer offers an **Add Python to PATH** option, enable it if you want the `python` command available in a new terminal. The Python launcher (`py`) is also useful for selecting a specific version.
5. Complete the installation.
6. If the installer offers to disable the Windows path-length limit, you may enable it.
7. Close the installer and open a **new** PowerShell window.

Verify:

```powershell
py -3.13 --version
```

Expected output should begin with:

```text
Python 3.13.
```

If the Python launcher is unavailable, try:

```powershell
python --version
```

Make sure the result is Python 3.13.x before creating the environment.

#### macOS

1. Visit <https://www.python.org/downloads/>.
2. Download the official Python 3.13 installer suitable for your Mac.
3. Run the `.pkg` installer and follow the instructions.
4. Open a new Terminal window.
5. Verify the installation:

```bash
python3.13 --version
```

The official installer may include an `Install Certificates.command` utility in its Python folder. If certificate verification problems occur, follow the instructions supplied with that installer.

#### Linux

Linux distributions differ in their package repositories and supported Python versions. Do not assume that one installation command works on every distribution.

For Ubuntu, first check whether Python 3.13 is available from the configured repositories:

```bash
sudo apt update
apt-cache policy python3.13
```

If a suitable package is available, install the interpreter and virtual-environment support using the distribution's package manager. For example:

```bash
sudo apt install python3.13 python3.13-venv
```

If it is not available, use a trusted installation method appropriate to the specific distribution, following its official documentation. Do not add a third-party repository such as Deadsnakes to every Debian-based system indiscriminately; repository instructions are distribution- and release-specific.

Verify:

```bash
python3.13 --version
```

### 3.2 Path B — another Python version is already installed

You do not need to uninstall Python 3.10, 3.12, 3.13 or an Anaconda distribution simply because another version is present.

Install Python 3.13.x alongside the existing version, if it is not already installed.

**Windows PowerShell:**

```powershell
py --list
py -3.13 --version
```

If Python 3.13 is listed, use it explicitly when creating the environment:

```powershell
py -3.13 -m venv .venv
```

**macOS/Linux:**

```bash
python3.13 --version
python3.13 -m venv .venv
```

Do not rely on whichever interpreter happens to be returned by `python` or `python3` when multiple versions are installed. Explicitly select Python 3.13 for this project.

---

## 4. Virtual Environment Creation and Activation

A virtual environment isolates this programme's packages from other Python projects on the computer. This reduces package conflicts and makes the course setup easier to reproduce.

The standard environment directory for this programme is:

```text
.venv
```

### 4.1 Create the environment

Run these commands from inside `ds-aiml-workspace`.

**Windows PowerShell:**

```powershell
py -3.13 -m venv .venv
```

**macOS/Linux:**

```bash
python3.13 -m venv .venv
```

### 4.2 Activate the environment

Activate the environment whenever you open a new terminal to work on the project.

**Windows PowerShell:**

```powershell
.venv\Scripts\Activate.ps1
```

If PowerShell blocks the activation script because of the execution policy, you can allow locally created scripts for your current user:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Review the prompt and confirm only if you are comfortable changing this user-level setting. Then activate the environment again.

**Windows Command Prompt:**

```cmd
.venv\Scripts\activate.bat
```

**macOS/Linux (bash or zsh):**

```bash
source .venv/bin/activate
```

### 4.3 Verify the active environment

The terminal prompt should show `(.venv)`.

Run:

```bash
python --version
python -c "import sys; print(sys.executable)"
```

Confirm that:

- The Python version is 3.13.x.
- The executable path points inside the project's `.venv` directory.

To leave the environment:

```bash
deactivate
```

---

## 5. Visual Studio Code and Jupyter Configuration

### 5.1 Install VS Code

Download and install Visual Studio Code from:

<https://code.visualstudio.com/>

### 5.2 Install the required extensions

1. Open VS Code.
2. Open the Extensions panel (`Ctrl+Shift+X` on Windows/Linux or `Cmd+Shift+X` on macOS).
3. Install the following extensions published by Microsoft:
   - **Python**
   - **Jupyter**

Use the official Microsoft extensions and avoid similarly named third-party extensions unless specifically instructed.

### 5.3 Open the project folder

1. Select **File → Open Folder**.
2. Open `ds-aiml-workspace`.
3. Open the integrated terminal in VS Code.
4. Activate `.venv` using the command for your operating system.

### 5.4 Select the Python interpreter

1. Open the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`).
2. Select **Python: Select Interpreter**.
3. Choose the interpreter inside the project's `.venv` folder.

Typical paths:

- Windows: `.venv\Scripts\python.exe`
- macOS/Linux: `.venv/bin/python`

If the environment does not appear, close and reopen the project folder, activate the environment in the terminal, or use the interpreter selection option to enter its path.

### 5.5 Install and register the Jupyter kernel

With `.venv` activated, install the notebook kernel package:

```bash
python -m pip install ipykernel
```

Register a recognizable kernel name:

```bash
python -m ipykernel install --user \
    --name educentriks-ds \
    --display-name "Educentriks - Data Science"
```

On Windows PowerShell, the command can also be entered on one line:

```powershell
python -m ipykernel install --user --name educentriks-ds --display-name "Educentriks - Data Science"
```

### 5.6 Select the notebook kernel

1. Open a course `.ipynb` notebook in VS Code.
2. Select the kernel shown near the top-right of the notebook.
3. Choose **Educentriks - Data Science**.
4. Run a test cell:

```python
import sys

print(sys.version)
print(sys.executable)
```

Confirm that the interpreter is Python 3.13.x and that the executable path points to the project's `.venv`.

---

## 6. Dependency Installation and Package Management

The course uses a shared package set. Installing the same tested versions helps reduce differences between student machines.

### 6.1 Package groups used in the programme

| Programme area | Packages |
|---|---|
| Numerical computing and data handling | `numpy`, `pandas`, `scipy`, `statsmodels` |
| Visualisation | `matplotlib`, `seaborn` |
| Traditional machine learning | `scikit-learn`, `joblib` |
| Deep learning | `torch`, `torchvision` |
| NLP foundations | `nltk` |
| Transformers and pretrained models | `transformers`, `huggingface-hub` |
| Text embeddings | `sentence-transformers` |
| Local vector search for Lean RAG | `faiss-cpu`, where supported |
| Deployment | `streamlit` |
| Notebook runtime | `jupyter`, `ipykernel` |
| Excel file reading, where required | `openpyxl` |

### 6.2 Important: exact versions will be supplied after validation

The package names above describe the required course stack. They are not a tested lockfile.

The Educentriks maintainer should:

1. Create a clean Python 3.13.x virtual environment.
2. Install the selected package versions.
3. Verify compatibility between related packages, especially PyTorch/torchvision and Transformers/Sentence Transformers.
4. Test FAISS on the supported operating systems.
5. Run the course notebooks and smoke tests.
6. Record the exact working versions in the repository's `requirements.txt`.

A file with version ranges such as `numpy>=...` is not an exact lockfile. For a reproducible classroom installation, use exact tested pins (`package==version`) in the final requirements file.

### 6.3 Install the approved requirements file

Once the course maintainer has published the validated `requirements.txt`, activate `.venv` and run:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Use `python -m pip` so package installation is tied to the active interpreter.

### 6.4 Verify package consistency

After installation:

```bash
python -m pip check
```

This checks for broken declared package dependencies. A successful result does not replace running the course smoke test and notebooks.

### 6.5 PyTorch CPU and GPU guidance

The course does not require a dedicated NVIDIA GPU.

- The standard classroom path should support CPU execution for introductory PyTorch exercises.
- GPU installation is optional and depends on the student's hardware, operating system, NVIDIA driver and compatible PyTorch build.
- Do not install arbitrary CUDA or torchvision versions.
- Follow the official PyTorch installation selector for a hardware-specific GPU setup: <https://pytorch.org/get-started/locally/>.
- Google Colab may be used for selected exercises that benefit from GPU acceleration, subject to availability and usage limits.

The final course requirements file should state whether PyTorch is installed through the standard CPU-compatible route or through a separately documented hardware-specific route.

---

## 7. Environment Verification and Smoke Testing

A smoke test checks whether the main components can be imported and whether a few basic operations execute. It is a useful pre-flight check, but it cannot guarantee that every future notebook or model download will work.

### 7.1 Create `smoke_test.py`

Save the following file in the root of `ds-aiml-workspace`, alongside `requirements.txt`.

```python
"""
Educentriks Day 0 — Environment Smoke Test

Purpose:
    Perform quick local checks of the core course environment.

Run:
    python smoke_test.py

This test does not download pretrained models or datasets.
"""

import sys
import importlib
from pathlib import Path


EXPECTED_PYTHON = (3, 13)

# Core modules that should be available after the approved setup.
MODULES_TO_CHECK = {
    "numpy": "NumPy",
    "pandas": "pandas",
    "scipy": "SciPy",
    "matplotlib": "Matplotlib",
    "seaborn": "Seaborn",
    "sklearn": "scikit-learn",
    "statsmodels": "statsmodels",
    "torch": "PyTorch",
    "torchvision": "torchvision",
    "transformers": "Hugging Face Transformers",
    "sentence_transformers": "Sentence Transformers",
    "nltk": "NLTK",
    "streamlit": "Streamlit",
    "jupyter": "Jupyter",
    "ipykernel": "ipykernel",
    "joblib": "joblib",
}

results = []


def record_result(name, passed, details=""):
    """Store and print the result of an individual check."""
    status = "PASS" if passed else "FAIL"
    print(f"[{status}] {name}")
    if details:
        print(f"       {details}")
    results.append((name, passed))


def check_python_version():
    """Check that the active interpreter uses the course Python baseline."""
    version = sys.version_info
    actual = f"{version.major}.{version.minor}.{version.micro}"

    passed = (version.major, version.minor) == EXPECTED_PYTHON
    record_result(
        "Python version",
        passed,
        f"Detected Python {actual}; expected {EXPECTED_PYTHON[0]}.{EXPECTED_PYTHON[1]}.x",
    )


def check_virtual_environment():
    """Check whether the current interpreter is running inside a venv."""
    in_venv = sys.prefix != sys.base_prefix
    executable = Path(sys.executable)

    record_result(
        "Virtual environment",
        in_venv,
        f"Interpreter: {executable}",
    )


def check_imports():
    """Attempt to import each required course module."""
    for module_name, display_name in MODULES_TO_CHECK.items():
        try:
            module = importlib.import_module(module_name)
            version = getattr(module, "__version__", "version not exposed")
            record_result(display_name, True, f"Version: {version}")
        except Exception as error:
            record_result(display_name, False, str(error))


def check_basic_ml():
    """Run a small scikit-learn classification example."""
    try:
        import numpy as np
        from sklearn.linear_model import LogisticRegression
        from sklearn.metrics import f1_score

        features = np.array([
            [10, 20],
            [20, 30],
            [30, 40],
            [40, 50],
        ])
        target = np.array([0, 0, 1, 1])

        model = LogisticRegression()
        model.fit(features, target)

        predictions = model.predict(features)
        score = f1_score(target, predictions)

        record_result(
            "Basic scikit-learn model",
            True,
            f"Model trained; F1 on tiny demonstration data: {score:.2f}",
        )
    except Exception as error:
        record_result("Basic scikit-learn model", False, str(error))


def check_pytorch_cpu():
    """Run a small PyTorch forward pass on the CPU."""
    try:
        import torch
        import torch.nn as nn

        model = nn.Sequential(
            nn.Linear(2, 4),
            nn.ReLU(),
            nn.Linear(4, 1),
        )

        sample = torch.randn(2, 2)
        output = model(sample)

        passed = tuple(output.shape) == (2, 1)
        device_message = (
            "CUDA available"
            if torch.cuda.is_available()
            else "CPU execution; no CUDA GPU detected"
        )

        record_result(
            "PyTorch CPU forward pass",
            passed,
            f"Output shape: {tuple(output.shape)}; {device_message}",
        )
    except Exception as error:
        record_result("PyTorch CPU forward pass", False, str(error))


def check_streamlit_import():
    """Check that Streamlit can be imported."""
    try:
        import streamlit
        record_result(
            "Streamlit import",
            True,
            f"Version: {streamlit.__version__}",
        )
    except Exception as error:
        record_result("Streamlit import", False, str(error))


def main():
    print("=" * 68)
    print("EDUCENTRIKS — DAY 0 ENVIRONMENT SMOKE TEST")
    print("=" * 68)
    print(f"Python executable: {sys.executable}")
    print(f"Python version: {sys.version.split()[0]}")
    print()

    check_python_version()
    check_virtual_environment()
    check_imports()
    check_basic_ml()
    check_pytorch_cpu()
    check_streamlit_import()

    print()
    print("=" * 68)
    print("RESULT SUMMARY")
    print("=" * 68)

    passed_count = sum(1 for _, passed in results if passed)
    failed_count = len(results) - passed_count

    print(f"Passed: {passed_count}")
    print(f"Failed: {failed_count}")

    if failed_count == 0:
        print("\nEnvironment checks passed.")
        print("Proceed to the course notebook verification.")
    else:
        print("\nEnvironment is NOT fully verified.")
        print("Review the failed checks before proceeding.")

    print("=" * 68)

    # A non-zero exit code makes failures visible to scripts and CI tools.
    return 0 if failed_count == 0 else 1


if __name__ == "__main__":
    raise SystemExit(main())
```

### 7.2 Run the smoke test

With `.venv` activated:

```bash
python smoke_test.py
```

The script checks:

- Python version
- Virtual environment activation
- Required package imports
- A small scikit-learn model
- PyTorch CPU execution
- Streamlit import

A failure should be investigated rather than ignored. The smoke test does not download the Sentence Transformer model or test FAISS indexing; those checks belong in the advanced Day 21 readiness test.

### 7.3 Additional verification

Run:

```bash
python -m pip check
```

Then open a notebook in VS Code, select the **Educentriks - Data Science** kernel and run all cells in a small introductory notebook.

---

## 8. Troubleshooting and Google Colab Fallback

### 8.1 Common setup issues

| Issue | First action |
|---|---|
| `python` command not found | Open a new terminal; on Windows try `py -3.13 --version` |
| Wrong Python version | Recreate `.venv` using the explicit Python 3.13 command |
| Activation blocked in PowerShell | Review the user-level `RemoteSigned` execution policy instructions in Section 4 |
| VS Code cannot find `.venv` | Use **Python: Select Interpreter** and browse to the environment executable |
| Notebook uses the wrong Python | Select the `Educentriks - Data Science` kernel |
| Package installation fails | Confirm `.venv` is active; inspect the complete error and check platform compatibility |
| `pip check` reports conflicts | Do not randomly upgrade packages; share the output with the instructor |
| FAISS installation fails | Use the documented platform-specific alternative or the approved Colab route |
| PyTorch GPU is unavailable | Use CPU for supported exercises or use Colab where acceleration is available |

When asking for help, provide the operating system, Python version, active interpreter path, command executed and complete error message. Remove secrets and personal information before sharing logs.

### 8.2 Google Colab as an alternative

Use Google Colab if:

- Local installation is blocked by operating-system permissions.
- A required package cannot be installed successfully on the student's machine.
- The computer has insufficient resources for a selected deep learning exercise.
- The instructor directs the class to use a cloud runtime for a demonstration.

Basic procedure:

1. Visit <https://colab.research.google.com/>.
2. Sign in with a Google account.
3. Open the course notebook from the Educentriks repository or upload a notebook copy.
4. Select **Runtime → Change runtime type** if the instructor asks you to use a particular runtime.
5. Select a GPU only when required and available.
6. Run the notebook's setup cells as instructed.

Colab runtimes are temporary. Files installed or created in a runtime may not persist after it is disconnected or reset. Save required work to your own storage or download it before ending the session.

Do not place passwords, API keys or confidential datasets in notebook cells or shared notebooks.

### 8.3 Running the Streamlit application

For the Day 22 practical, activate `.venv`, navigate to the project root and run:

```bash
streamlit run src/app.py
```

Streamlit normally opens a local browser page at:

```text
http://localhost:8501
```

If the browser does not open automatically, copy the local address shown in the terminal into your browser. Do not expose the application publicly or configure network tunnels unless the instructor explicitly directs you to do so.

---

## 9. Day 0 Completion Checklist

Before starting Day 1, confirm each item:

- [ ] Python 3.13.x (64-bit) is installed.
- [ ] The `ds-aiml-workspace` folder has been created.
- [ ] The `.venv` virtual environment has been created.
- [ ] `.venv` activates successfully.
- [ ] The active interpreter points to `.venv`.
- [ ] VS Code is installed.
- [ ] Microsoft Python and Jupyter extensions are installed.
- [ ] The `Educentriks - Data Science` Jupyter kernel is registered and selectable.
- [ ] The maintainer-approved `requirements.txt` has been installed.
- [ ] `python -m pip check` completes without dependency conflicts.
- [ ] `smoke_test.py` completes without failed checks.
- [ ] A course notebook opens and executes using the correct kernel.
- [ ] The student can access the Educentriks course repository.

**Day 0 is complete when the environment is verified—not merely when Python has been installed.**

---

## 10. Instructor / Maintainer Validation Before Batch Distribution

This section is for the Educentriks course maintainer.

Before distributing the setup instructions and requirements file:

1. Test the complete setup on a clean Windows 10/11 machine using Python 3.13.x (64-bit).
2. Test the documented setup on at least one supported macOS or Linux environment, or clearly identify any platform-specific exceptions.
3. Install the selected package versions into a fresh `.venv`.
4. Confirm PyTorch and torchvision compatibility.
5. Test Sentence Transformers and Hugging Face dependencies together.
6. Test FAISS installation and indexing on each operating system the course claims to support.
7. Run the smoke test and all required introductory notebooks.
8. Record the exact working package versions in `requirements.txt`.
9. Keep CPU installation as the standard path; publish separate GPU instructions only after testing.
10. Update this guide, the requirements file and smoke test together if the Python baseline changes.

Do not describe the environment as fully validated until these checks have been completed.

---

**Educentriks**  
*From Learning to Real-World Application*
