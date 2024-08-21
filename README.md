name: Python Security Analysis

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  security_analysis:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Run Bandit security analysis
      run: |
        pip install bandit
        bandit -r .

    # Se quiser usar o PyUp para análise de vulnerabilidades em pacotes
    - name: Install PyUp safety
      run: pip install safety

    - name: Run PyUp safety check
      run: safety check
