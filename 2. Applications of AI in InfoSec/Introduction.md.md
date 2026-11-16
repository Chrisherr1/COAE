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

## Important: Jupyter is stateful

Meaning that any code that you execute within the cells will effect future results.

Any variables you make will still exist, so be careful when naming stuff.

Eg: 
1. `x = 1`
2. then later you call `print(x)` // this will be 1
3. if you change the first cell to x = 2
4. Then re-run it before running the `print(x)`cell, the value of `x` in the envronment becomes 2, so the output will be different when you run the print cell.


> You can add new cells. (+) 

JupyterLab integrates with libraries like `pandas, matplotlib, seaborn` for data exploration and visualization.
```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Create a sample DataFrame
data = pd.DataFrame({
    "column1": np.random.rand(50),  # 50 random values for column1
    "column2": np.random.rand(50) * 10  # 50 random values (multiplied by 10) for column2
})

# Display the first few rows
print(data.head())

# Create a scatter plot
plt.scatter(data["column1"], data["column2"])
plt.xlabel("Column 1")
plt.ylabel("Column 2")
plt.title("Scatter Plot")
plt.show()
```
> This is the example they showed to visualize a dataset with pandas.

## Restarting the kernel 

JupyterLab uses a kernel to run code. 

Sometimes a reset is necessary if its too cluttered with variables, functions, and imports. 

Open Kernel menu in the top toolbar, then restart the kernel and clear all outputs and also remove all previously generated outputs from the notebook.

> You'll have to re-run any cells that you ran(AKA code).

---

# Python Libraries for AI

Python has 2 libraries for AI.

`Scikit-learn` and `PyTorch`

---
## Scikit-learn

It is a great library built on `NumPy`,`SciPy`, and `Matplotlib`.

For supervised learning, it has these algorithms.

- `Linear Regression`
- `Logistic Regression`
- `Support Vector Machines (SVMs)`
- `Decision Trees`
- `Naive Bayes`
- `Ensemble Methods`

For un-supervised learning, it has these algorithms.

- `Clustering (K-Means, DBSCAN)`
- `Dimensionality Reduction (PCA, t-SNE)`

It provides great tools for preprocessing data. This helps transform raw data into a suitable format that improve the accuracy of the model.

It also provides feature scaling.

- `StandardScaler` : Standardizes features by removing the mean and scaling to unit variance.
- `MinMaxScaler` : Scales features to a given range, typically between 0 and 1.
- `RobustScaler` : Scales features using statistics that are robust to outliers.
```
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

Categorical data needs to be converted to a numerical?

- `OneHotEncoder` : Creates binary (0 or 1) columns for each category.
- `LabelEncoder` : Assigns a unique integer to each category.

```
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder()
X_encoded = encoder.fit_transform(X)
```

Missing values?

- `SimpleImputer` : Replaces missing values with a specified strategy (e.g., mean, median, most frequent).
- `KNNImputer` : Imputes missing values using the k-Nearest Neighbors algorithm.

```
from sklearn.impute import SimpleImputer 
imputer = SimpleImputer(strategy='mean') 
X_imputed = imputer.fit_transform(X)
```

Splitting data? (train_test_split)
```
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
```

Cross Validating the data?(cross_val_score)
```
from sklearn.model_selection import cross_val_score

scores = cross_val_score(model, X, y, cv=5)
```

Metrics Provided:
- `accuracy_score` : For classification tasks.
- `mean_squared_error` : For regression tasks.
- `precision_score`, `recall_score`, `f1_score` : For classification tasks with imbalanced classes.

```
from sklearn.metrics import accuracy_score 
accuracy = accuracy_score(y_test, y_pred
```

## Model Training and Predication

1. Create an instance of the desired model with appropriate hyperparameters.
```
from sklearn.linear_model import LogisticRegression 
model = LogisticRegression(C=1.0)
```
2. train the model using `fit()` method with the training data.
```
model.fit(X_train, y_train)
```
3. Make predications on new data using the predict() method.
```
y_pred = model.predict(X_test)
```

---
# PyTorch

Open-source machine learning library developed by Facebook's AI research lab.

Provides framework for deploying various types of machine learning models, including deep learning models.

PyTorch is a tool for building neural networks. It's flexible and easy to debug, runs faster on GPUs, handles the math for training automatically, and has a big community with lots of extra tools.

## Dynamic Computational Graphs and tensors

PyTorch is known for this, it allows for more flexible and dynamic model building.

> Makes it easier to implement complex and non-linear models.

`Tensors` are multi-dimensional arrays that hold the data being processed.

> `PyTorch` tensors are similar to NumPy arrays but can run on GPUs for faster computation.

```
import torch

# Creating a tensor
x = torch.tensor([1.0, 2.0, 3.0])

# Tensors can be moved to GPU if available
if torch.cuda.is_available():
    x = x.to('cuda')
```

## Building models with PyTorch

 The `torch.nn` module contains various layers and modules for constructing neural networks.

The `Sequential` API allows building models layer by layer, adding each layer sequentially.

The `Module` class provides more flexibility for building complex models with non-linear topologies, shared layers, and multiple inputs/outputs.

```
import torch.nn as nn 

model = nn.Sequential( 
nn.Linear(784, 128), 
nn.ReLU(), 
nn.Linear(128, 10), 
nn.Softmax(dim=1) 
)
```

Model class version: 
```
import torch.nn as nn 
class CustomModel(nn.Module): 
	def __init__(self):super(CustomModel,self).__init__() 
		self.layer1 = nn.Linear(784, 128) 
		self.relu = nn.ReLU() 
		self.layer2 = nn.Linear(128, 10) 
		self.softmax = nn.Softmax(dim=1) 
	
	def forward(self, x): 
	x = self.layer1(x) 
	x = self.relu(x) 
	x = self.layer2(x) 
	x = self.softmax(x) 
	return x 
	model = CustomModel()
```

## Training and Evaluation.

`Optimizers` are algorithms that adjust the model's parameters during training to minimize the loss function.

Options: 
- `Adam`
- `SGD` (Stochastic Gradient Descent)
- `RMSprop`

`Loss Functions` measure the difference between the model's predictions and the actual target values.

Options:
- `CrossEntropyLoss` : For multi-class classification.
- `BCEWithLogitsLoss` : For binary classification.
- `MSELoss` : For regression.

`Metrics` evaluate the model's performance during training and testing.

Options: 
- `Accuracy`
- `Precision`
- `Recall`

The training loop updates the model's parameters based on the training data.

```
import torch

epochs = 10
num_batches = 100

for epoch in range(epochs):
    for batch in range(num_batches):
        # Get batch of data
        x_batch, y_batch = get_batch(batch)
        
        # Forward pass
        y_pred = model(x_batch)
        
        # Calculate loss
        loss = loss_fn(y_pred, y_batch)
        
        # Backward pass and optimization
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
        
        # Optional: print loss or other metrics
        if batch % 10 == 0:
            print(f'Epoch [{epoch+1}/{epochs}], Batch [{batch+1}/{num_batches}], Loss: {loss.item():.4f}')
```

`PyTorch` provides the `torch.utils.data.Dataset` and `DataLoader` classes for handling data loading and preprocessing.

`PyTorch` allows models to be saved and loaded for inference or further training.

```
# Save model
torch.save(model.state_dict(), 'model.pth')

# Load model
model = CustomModel()
model.load_state_dict(torch.load('model.pth'))
model.eval()  # Set the model to evaluation mode
```