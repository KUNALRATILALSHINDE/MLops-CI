# 🔁 Continuous Integration in MLOps – Automating the ML Workflow

Welcome to my exploration of **Continuous Integration (CI)** in the world of **Machine Learning Operations (MLOps)**! This project is focused on automating and testing the machine learning pipeline to make model building faster, safer, and more scalable. 🚀

CI is the foundation for bringing DevOps practices into ML, and in this project, I explored how to integrate ML workflows with automated testing, version control, and pipeline execution.

---

## 🤖 What is Continuous Integration in MLOps?

In software development, **CI** refers to the practice of automatically integrating and testing code changes. In ML, CI goes beyond code — it includes:

- Code updates (`model.py`, `train.py`, etc.)
- Data versioning
- Model artifacts
- Experiment tracking
- Pipeline consistency

✅ The goal? **Every update to your ML system is tested, versioned, and reproducible.**

---

## 🛠️ Tools Used

- **GitHub Actions** – For CI pipelines
- **DVC** – Data & model versioning
- **MLflow** – Experiment tracking
- **pytest** – Automated testing
- **DAGsHub** – To visualize the flow
- **Docker** *(optional)* – For containerization
- **VS Code + Git** – My dev environment

---

## 🧪 What the CI Pipeline Does

Whenever I push new code or data:

1. 🔍 **Lint & test code** (with `flake8` and `pytest`)
2. ⚙️ **Run DVC pipeline** (reproduces stages if dependencies change)
3. 📊 **Log experiments with MLflow**
4. ☁️ **Push data/models to remote storage**
5. 📤 **Track experiment on DAGsHub/MLflow UI**
6. ✅ **Check for successful runs before merging**

---

## 📦 GitHub Actions Workflow Example

```yaml
name: CI for ML Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.9

      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install dvc[gs] mlflow pytest

      - name: Run tests
        run: pytest tests/

      - name: Reproduce pipeline
        run: dvc repro

      - name: Push to remote
        run: dvc push
