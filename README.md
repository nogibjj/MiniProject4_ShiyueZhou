# MiniProject1_ShiyueZhou
[![CI-Python Application Test with Github Actions](https://github.com/nogibjj/MiniProject4_ShiyueZhou/actions/workflows/ci.yml/badge.svg)](https://github.com/nogibjj/MiniProject4_ShiyueZhou/actions/workflows/ci.yml)

Based on the requirement of miniproject in week4, the following help to work through the Github Actions Matrix Build and the other structures.  

# Github Actions Matrix Build<br>
Existed in the **Jobs (`jobs`)** of `.github/workflows/ci.yml`  

```yaml
matrix:
  python-version: [3.7, 3.8, 3.9, 3.11]
  os: [ubuntu-latest, windows-latest]
```
- **Python versions:** Your workflow will run on Python versions 3.7, 3.8, 3.9, and 3.11.  
 | Python Version | Operating System  |  
 | -------------- | ----------------- |  
 | 3.7            | Ubuntu-latest      |  
 | 3.7            | Windows-latest     |  
 | 3.8            | Ubuntu-latest      |  
 | 3.8            | Windows-latest     |  
 | 3.9            | Ubuntu-latest      |  
 | 3.9            | Windows-latest     |  
 | 3.11           | Ubuntu-latest      |  
 | 3.11           | Windows-latest     |  
- **Operating systems:** The workflow will run on two operating systems: ubuntu-latest (Linux) and windows-latest (Windows).  
 - This means that your code will be tested across 8 different combinations (4 Python versions × 2 OS).  

```yaml
runs-on: ${{ matrix.os }}
```
 - This dynamically sets the OS for each job based on the current matrix value. For each combination, matrix.os will be either ubuntu-latest or windows-latest.  

```yaml
- name: Set up Python
  uses: actions/setup-python@v4
  with:
    python-version: ${{ matrix.python-version }}
```
 -  This step dynamically sets the Python version for each job, depending on the current matrix value (3.7, 3.8, 3.9, or 3.11).

# Github Actions<br>
 The `.github/workflows` directory contains workflows that automate various tasks using GitHub Actions.  

1. **`name: CI Pipeline`**  
   This gives the workflow a name, which will appear in the GitHub Actions tab of your repository.  

2. **Triggers (`on`)**:  
   - **`push`**: The workflow is triggered when code is pushed to the `main` branch.  
   - **`pull_request`**: The workflow is triggered when a pull request is opened or updated for the `main` branch.  

3. **Jobs (`jobs`)**:  
   - **`build`**:  
     - **`runs-on`**: This specifies the environment (runner) where the job will run. GitHub provides hosted runners, and in this case, it uses the latest version of Ubuntu (`ubuntu-latest`).  
     - **`steps`**: Each job contains a series of steps. Steps are the individual tasks performed in sequence, such as checking out code, installing dependencies, linting, and running tests.



# requirements.txt<br>
 -->related to packages and version in this project: allows you to specify the exact packages (and versions) to be installed, ensuring consistency across different environments  

# Makefile<br>
 -->For machine reading and executing by running `make all`.  
 -->This sequentially runs `make install`, `make format`, `make lint`, and `make test`.   
- **install**:: Installs the required packages listed in `requirements.txt`.  
- **format**:: Formats the code to ensure it follows proper code style (using black).  
- **lint**: Runs pylint to analyze the code for potential errors, coding standard violations, and best practices. 
- **test**: Uses pytest to run the test files, ensuring the code works as expected.  
- **all**: Runs all the above tasks sequentially (install, format, lint, test).  
 
  
# Dev Container<br>
 The `.devcontainer` folder contains two key components:
- **`devcontainer.json`**: The main configuration file that defines the development container’s setup. It specifies the tools, settings, and VSCode extensions for the environment.
- **`Dockerfile`**: Defines a custom Docker image used to create the container. It specifies the base image and any additional dependencies or system configurations required for the development environment.



