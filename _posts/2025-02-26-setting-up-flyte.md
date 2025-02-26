---
layout: post
title: Setting Up Flyte (A Step-by-Step Guide)
categories: [Flyte, Workflow Orchestration]
tags: [Flyte, Python, Ubuntu]
author: Dae-young Kim
comment: true
---
Flyte is a powerful workflow automation platform designed for machine learning and data engineering tasks. This guide will walk you through the setup process, including configuring a virtual environment, installing dependencies, setting up Docker, and running Flyte in a sandbox environment.

## 1. Setting Up a Virtual Environment
Before installing Flyte, it's recommended to use a virtual environment to manage dependencies and ensure an isolated setup.

### Check Python Version and Install Virtual Environment
Run the following commands to ensure you have Python 3 installed and set up a virtual environment:
```bash
python3 --version
sudo apt update
sudo apt install python3-venv
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install poetry
```

### Install Required Packages
If you are starting a new project, you can initialize a Poetry environment with:
```bash
poetry init
```

If you are adopting Flyte in an existing project, ensure that your dependencies are properly managed within Poetry. Run:
```bash
poetry install
```

This will install all dependencies defined in your project's pyproject.toml file. If you haven’t defined Flyte dependencies yet, you may need to add them manually:
```bash
poetry add flytekit flytectl
```

Poetry will manage package versions and dependencies, making it easier to integrate Flyte into your existing workflow.

## 2. Installing Docker
Flyte requires Docker to run in a sandbox environment. Follow these steps to install Docker on your system.

### Install Docker Dependencies
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
```

### Add Docker’s Official GPG Key
```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### Add Docker Repository to Apt Sources
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker Engine and CLI
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Docker Installation
Check if Docker is running correctly by listing the Docker socket:
```bash
ls -l /var/run/docker.sock
```

### Add User to Docker Group
```bash
newgrp docker
sudo usermod -aG docker $(whoami)
```
Reboot your system to apply these changes:
```bash
sudo reboot
```

## 3. Installing `flytectl` (Flyte CLI)
Flyte’s command-line tool, `flytectl`, allows you to manage projects, workflows, and tasks.
Install `jq` and `flytectl`
```bash
sudo apt install jq
curl -sL https://ctl.flyte.org/install | sudo bash -s -- -b /usr/local/bin
```

## 4. Configuring Flyte Sandbox
The Flyte Sandbox provides an easy way to run Flyte locally for development and testing.
### Create Flyte Configuration File
Create the file `~/.flyte/config-sandbox.yaml` and add the following content:
```yaml
flyte:
  admin:
    endpoint: localhost:30080
    authType: Pkce
    insecure: true
```
### Start Flyte Sandbox
```bash
export FLYTECTL_CONFIG=~/.flyte/config-sandbox.yaml
sudo flytectl demo start
```
After running this command, you should see output indicating that Flyte is successfully running. The Flyte UI will be available at: http://localhost:30080/console
Additional services like Minio (for storage) will also be available: http://localhost:30080/minio

## 5. Example Flyte Project Directory Structure
When setting up a Flyte project, your directory structure may look something like this:
```bash
flyte_project/
├── pyproject.toml
├── poetry.lock
├── dataset
└── workflow_codes/
    ├── imageSpec.yaml
    ├── project_definition.yaml
    └── codes/
        ├── __init__.py
        ├── workflow.py
        ├── tasks.py
        └── utils.py
```
### Explanation of Files and Directories
- `pyproject.toml` – Configuration file for Poetry dependencies.
- `poetry.lock` – Auto-generated file that locks dependency versions.
- `dataset` - dataset directory. We will copy this when running example workflow.
- `workflow_codes/` – Main directory containing Flyte workflows.
  - `imageSpec.yaml` – Defines the Docker image specification for Flyte workflows.
  - `project_definition.yaml` – Defines the Flyte project metadata.
  - `codes/` – Contains Python files defining Flyte workflows, tasks, and utilities.

## 6. Creating a New Flyte Project
Once Flyte is running, you can create a new project to organize your workflows.

### Define Project Configuration
Ensure you have a project definition file (e.g., `workflow_codes/project_definition.yaml`) and populate it with necessary metadata.

### Create Project in Flyte
```bash
flytectl create project --file ./workflow_codes/project_definition.yaml
```

### `project_definition.yaml` example
```yaml
id: "flyteproject"
name: "flyteproject"
description: "The pipeline that orchestrate data processing and training process of my project."
```

### Example workflow
Once your project is set up, you can define and execute workflows. Here’s an example of a simple Flyte workflow:

```python
# workflow.py
import os
from pathlib import Path
from flytekit import task, workflow

# Define the dataset path based on the copied directory inside the container
DATASET_DIR = Path("/dataset")

@task
def list_files_in_dataset() -> list:
    """Lists all files inside the dataset directory."""
    if not DATASET_DIR.exists():
        raise FileNotFoundError(f"Dataset directory {DATASET_DIR} not found!")

    return [str(file) for file in DATASET_DIR.iterdir()]

@task
def say_hello(name: str, dataset_files: list) -> str:
    """Prints a greeting along with dataset files."""
    dataset_info = f"Dataset contains {len(dataset_files)} files: {', '.join(dataset_files)}" if dataset_files else "Dataset is empty."
    return f"Hello, {name}! {dataset_info}"

@workflow
def greeting_workflow(name: str) -> str:
    """Workflow that lists dataset files and prints a greeting."""
    dataset_files = list_files_in_dataset()
    return say_hello(name=name, dataset_files=dataset_files)
```

## 7. Running workflows in Flyte Sandbox Cluster
To execute the workflow on the Flyte sandbox cluster, use the pyflyte run command. This ensures the workflow is executed in a Flyte-managed environment.

### Execute the workflow in Flyte Sandbox

```bash
pyflyte run --remote --image ./workflow_codes/imageSpec.yaml -p flyteproject -d development ./workflow_codes/codes/workflow.py greeting_workflow
```

### Explanation of Command Arguments
- `--remote` → Runs the workflow in the Flyte sandbox cluster instead of locally.
- `--image` ./workflow_codes/imageSpec.yaml → Specifies the Docker image to use for execution.
- `-p flyteproject` → Specifies the Flyte project name.
- `-d development` → Specifies the domain (development/staging/production).
- `./workflow_codes/workflow.py greeting_workflow` → Specifies the script and workflow function.

### `imageSpec.yaml` example
```yaml
python_version: 3.12.3
registry: localhost:30000
packages:
  - beautifulsoup4
  - pandas
  - tqdm
  - chardet
  - ujson
  - lxml
  - jupyter
  - tokenizers
  - loguru
  - pytz
  - spacy
  - plotly
  - datasets
  - csvkit
  - lz4
  - dask[dataframe]
  - distributed
  - cloudpickle
  - flytekit
  - https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-3.8.0/en_core_web_sm-3.8.0-py3-none-any.whl
copy:
  - dataset
env:
  Debug: "True"
```

**Explanation**
- `python_version`: Specifies the Python version.
- `registry`: Uses a local Docker registry.
- `packages`: List of dependencies for Flyte workflows.
- `copy`: Directories to copy into the container.
- `env`: Environment variables.