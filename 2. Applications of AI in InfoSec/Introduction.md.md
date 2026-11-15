# Introduction

We will construct 3 AI modules here
1. A `Spam Classifier` to determine whether an SMS message is `spam` or not.
2. A `Network Anomaly Detection Model` designed to identify abnormal or potentially malicious network traffic.
3. A `Malware Classifier` using `byteplots`, which are visual representations of binary data.

> You can copy and paste code snippets into Jupyter notebook to execute them in sequence, either in the playground Vm or your environment.

> You can train your own models, you just need 4GB of Ram and 4CPU cores.

---
## Setup 

> `http://<VM-IP>:8888` on Pwnbox will give you access to Jupyter but its recommended to just set up your own environment.

### Miniconda / Anaconda

`Miniconda` is a minimal installer for `Anaconda` distribution of the Python programming language.

> Ananconda is just bigger and includes data science tools.

### Why Miniconda?

1. It preforms data science and ML tasks better due to optimized packages.
2. Conda package manager simplifies package install and management, ensuring compatibility and resolving dependencies.
3. It allows you to create Isolated environments for different projects. 

> This ensures every project has its own dependencies.

## Install Miniconda

>Just look it up. Different installs depending on the OS.

MacOS:
```
brew install --cask miniconda

conda --version

```

## Init 

The `init` command configures your shell to recognize and utilize `conda`.

* Allows you to use `conda activate` to switch between environments.
- Ensures that `conda` commands are available in your shell.

To start conda:
```
conda init
```
> it will modify your shell to include conda settings.

```
conda config --add channels defaults

conda config --add channels conda-forge

conda config --add channels nvidia # only needed if you are on a PC that has a nvidia gpu

conda config --add channels pytorch

conda config --set channel_priority strict
```

> Run these to finish the `init` process.

After installing miniconda, base environment is activated by default for every terminal.

Turn it off with:
```
conda config --set auto_activate_base false
```

---
## Managing Virtual Environments

VMs are useful for isolating projects without messing with other projects or system's global Python install.

```
1. Each project can have its own set of dependencies, even if they conflict with those of other projects.

2. Keeps your project directory clean and organized by containing all dependencies within the environment.

3. Ensures that your project can be easily reproduced on different systems with the same dependencies.

4. Prevents conflicts with your global Python installation and avoids breaking other projects.
```

Conda can make VMs.
```
conda create -n ai python=3.11
```
This will make a VM named `ai` with `Python 3.11`. which then can be used to contain Ai-related packages.

You can turn on the VM using:
```
conda activate ai
```

If your terminal has the the VM name prefixed (ai), then that means its on.

Any conda or pip packages will be installed in here.

Turn it off using:
```
conda deactivate
```

Fish Specific:
```
conda init fish
exec fish
conda activate ai
```
## Install things we need

```
conda install -y numpy scipy pandas scikit-learn matplotlib seaborn transformers datasets tokenizers accelerate evaluate optimum huggingface_hub nltk category_encoders
```

```
conda install -y pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia
```

```
pip install requests requests_toolbelt
```

OR 

MacOS:
```
pip install torch torchvision torchaudio transformers datasets tokenizers accelerate evaluate optimum huggingface_hub nltk category_encoders
```

```
pip install requests requests_toolbelt
```

To update conda packages:
```
conda update --all
```

> You will need to manage pip packages separately.

To update pip on MacOS:

```
pip install --upgrade torch torchvision torchaudio transformers datasets tokenizers accelerate evaluate optimum huggingface_hub nltk category_encoders requests requests_toolbelt
```

# JupyterLab

Popular for data scientists and machine learning practitioners.

Interactive development environment that provides web-based coding, data, and visualization interfaces.

It supports .md syntax and it allows us to run code in a iterative environment.

To install Jupyter:

Linux:
```
conda install -y jupyter jupyterlab notebook ipykernel
```
MacOS:
```
conda activate ai
pip install jupyter jupyterlab notebook ipykernel
```

To start JupterLab:
```
jupyter lab
```

> The primary component is the notebook, which allows combining code,text, and visualizations in a single document.

`Code cells`: Execute code.
`Markdown cells`: Create formatted text, equations, and images using markdown syntax.
`Raw cells`: Untyped raw text.
