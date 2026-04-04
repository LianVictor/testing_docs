---
title: Setting up the SDK
layout: default
nav_order: 1
---
# Setting up the SDK

## Pre-reqs for Vectorblox SDK:

 - Ubuntu 20.04, 22.04, 24.04 LTS (If using WSL, please run from the home directory or have permissions set for the directory)

 - git lfs

 - Updated drivers on host system (Due to certain python package dependencies)

## Getting started:
 1. Install git lfs via:

    ```
    sudo apt-get update
    sudo apt install git-lfs && git-lfs install   
    ```

 2. Clone the VectorBlox SDK library via the following command the directory you want to work in:

    ```
    git clone https://github.com/Microchip-Vectorblox/VectorBlox-SDK.git
    ```

    *Note*: If running this command in WSL, it is recommended  to run this on a WSL directory

 3. Navigate to the `VectorBlox-SDK` directory and run the following command:

    ```
    bash install_dependencies.sh
    ```

 3. Set up the VectorBlox Virtual environment via:

    ```
    source setup_vars.sh
    ```

## Once the virtual environment is setup, proceed to the next step to run a tutorial


[Running a Tutorial]
----
[Running a Tutorial]: tutorial_run
