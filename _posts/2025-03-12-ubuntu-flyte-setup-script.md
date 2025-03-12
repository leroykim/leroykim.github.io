---
layout: post
title: Ubuntu Flyte Setup Script
categories: [Flyte, Workflow Orchestration]
tags: [Flyte, Python, Ubuntu]
author: Dae-young Kim
comment: true
---
```bash
#!/bin/bash
set -e

#------------------------------------------------------------------------------
# Script: env_setup_ubuntu.sh
#
# Description:
#   This script sets up a Python virtual environment, installs required Python
#   packages using Poetry, installs Docker with its dependencies, and installs
#   flytectl.
#
# How to Use:
#   1. Save this script to a file (e.g., env_setup_ubuntu.sh).
#   2. Make the script executable:
#          chmod +x env_setup_ubuntu.sh
#   3. Run the script:
#          ./env_setup_ubuntu.sh
#
# Note:
#   The script will prompt you to reboot your system at the end if Docker group
#   changes have been applied. Answer 'y' to reboot or 'n' to skip.
#
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# Function: setup_virtualenv
#
# Description:
#   Sets up the Python virtual environment by checking the Python version,
#   updating apt packages, installing python3-venv, creating a virtual
#   environment, activating it, upgrading pip, and installing Poetry.
#------------------------------------------------------------------------------
setup_virtualenv() {
    echo "Checking Python version..."
    python3 --version

    echo "Updating apt packages..."
    sudo apt update

    echo "Installing python3-venv..."
    sudo apt install -y python3-venv

    echo "Creating virtual environment..."
    python3 -m venv .venv

    echo "Activating virtual environment..."
    # shellcheck source=/dev/null
    source .venv/bin/activate

    echo "Upgrading pip and installing Poetry..."
    pip install --upgrade pip
    pip install poetry
}

#------------------------------------------------------------------------------
# Function: install_packages
#
# Description:
#   Installs Python packages using Poetry based on the project's configuration.
#------------------------------------------------------------------------------
install_packages() {
    echo "Installing project packages with Poetry..."
    poetry install
}

#------------------------------------------------------------------------------
# Function: install_docker
#
# Description:
#   Installs Docker and configures its repository. This includes installing
#   prerequisites, adding Docker's official GPG key and repository, installing
#   Docker and related tools, and adding the current user to the Docker group.
#------------------------------------------------------------------------------
install_docker() {
    echo "Updating apt packages for Docker installation..."
    sudo apt-get update

    echo "Installing prerequisites for Docker..."
    sudo apt-get install -y ca-certificates curl

    echo "Creating keyring directory for Docker..."
    sudo install -m 0755 -d /etc/apt/keyrings

    echo "Adding Docker's official GPG key..."
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
        -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    echo "Adding Docker repository to APT sources..."
    . /etc/os-release
    UBUNTU_CODENAME=${UBUNTU_CODENAME:-$VERSION_CODENAME}
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu ${UBUNTU_CODENAME} stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    echo "Updating apt packages..."
    sudo apt-get update

    echo "Installing Docker packages..."
    sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    echo "Listing Docker socket permissions..."
    ls -l /var/run/docker.sock

    echo "Adding current user to the Docker group..."
    sudo usermod -aG docker "$(whoami)"
    echo "NOTE: For the group changes to take effect, please log out and log in again or reboot your system."
}

#------------------------------------------------------------------------------
# Function: install_flytectl
#
# Description:
#   Installs flytectl along with its dependency jq.
#------------------------------------------------------------------------------
install_flytectl() {
    echo "Installing jq..."
    sudo apt install -y jq

    echo "Installing flytectl..."
    curl -sL https://ctl.flyte.org/install | sudo bash -s -- -b /usr/local/bin
}

#------------------------------------------------------------------------------
# Function: main
#
# Description:
#   Orchestrates the installation steps by sequentially setting up the virtual
#   environment, installing Python packages, Docker, and flytectl.
#------------------------------------------------------------------------------
main() {
    echo "=== Starting Virtual Environment Setup ==="
    setup_virtualenv

    echo "=== Installing Python Packages ==="
    install_packages

    echo "=== Installing Docker ==="
    install_docker

    echo "=== Installing flytectl ==="
    install_flytectl

    echo "All installations have been completed successfully."
    read -r -p "Reboot is recommended for Docker group changes to take effect. Reboot now? (y/N): " answer
    if [[ $answer =~ ^[Yy]$ ]]; then
        echo "Rebooting system..."
        sudo reboot
    else
        echo "Please remember to reboot your system later."
    fi
}

# Run the main function
main
```