# Introduction

We will construct 3 AI modules here
1. A `Spam Classifier` to determine whether an SMS message is `spam` or not.
2. A `Network Anomaly Detection Model` designed to identify abnormal or potentially malicious network traffic.
3. A `Malware Classifier` using `byteplots`, which are visual representations of binary data.

> You can copy and paste code snippets into Jupyter notebook to execute them in sequence, either in the playground Vm or your environment.

> You can train your own models, you just need 4GB of Ram and 4CPU cores.

---
---
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

---
---
---
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
---
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

---
---
---
# Datasets 

Data sets are Collections of data points used for analysis and model training, come in various forms and formats, each with its own properties and considerations.

`Data preprocessing` is a crucial step in the machine-learning pipeline that involves transforming raw data into a suitable format for algorithms to process effectively.

- `Tabular Data`: Data organized into tables with rows and columns, common in spreadsheets or databases.
- `Image Data`: Sets of images represented numerically as pixel arrays.
- `Text Data`: Unstructured data composed of sentences, paragraphs, or full documents.
- `Time Series Data`: Sequential data points collected over time, emphasizing temporal patterns.

The quality of the dataset is important for model accuracy, generalization, efficiency, and reliability.

### The Dataset

https://cdn.services-k8s.prod.aws.htb.systems/content/modules/292/demo_dataset.zip
> This is the demo_dataset.csv, it contains network log entries with info and threat level.

> Analyzing this will help us simulate network scenarios that are useful for developing and evaluating instruction detection systems.

Problems we will see:
- The dataset contains a mix of numerical and categorical data.
- Missing values and invalid entries appear in some columns, requiring data cleaning.
- Certain numeric columns may contain non-numeric strings, which must be converted or removed.
- The `threat_level` column includes unknown values (e.g., `?`, `-1`) that must be standardized or addressed during preprocessing.

### Loading the Dataset:

Load into `pandas DataFrame` to begin working with the dataset.

Utilizing a DataFrame simplifies subsequent tasks like inspection, cleaning, encoding, and data transformation.

```
import pandas as pd 

# Load the dataset 
data = pd.read_csv("./demo_dataset.csv")
```
>In this code, `pd.read_csv("./demo_dataset.csv")` loads the downloaded CSV file into a DataFrame named `data`.

### Exploring the Dataset

After loading the dataset, we employ various operations to understand its structure, identify anomalies, and determine the nature of cleaning or transformations needed.

1. Examining the first few rows, to see issues  such as unexpected column names, incorrect data types, or irregular patterns.

```
# Display the first few rows of the dataset 
print(data.head())
```

2. See what data types and completeness of each column.
```
# Get a summary of column data types and non-null counts
print(data.info())
```

> Info() reveals the dataset's shape, column names, data types, and how many entries are present for each column, enabling early detection of unexpected data.

### Checking for Missing Values 

3. The next step is to identify how many missing values each column contains.
```
print(data.isnull().sum())
```
> Command returns the count of null values for each column, helping to prioritize which needs attention. You can remove, or alter the data if you need to.

----
---
---

# Data Preprocessing

`Data preprocessing` transforms raw data into a suitable format for machine learning algorithms.

Key techniques include:
- `Data Cleaning`: Handling missing values, removing duplicates, and smoothing noisy data.
- `Data Transformation`: Normalizing, encoding, scaling, and reducing data.
- `Data Integration`: Merging and aggregating data from multiple sources.
- `Data Formatting`: Converting data types and reshaping data structures.

Doing this will help address inconsistencies.

### Checking for Invalid IP Addresses


4. To identify invalid `source_ip` values, you can use a regular expression to validate the IP addresses:
```
import re

def is_valid_ip(ip):
	pattern = re.compile(r'^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$') 
	return bool(pattern.match(ip))

# Check for invalid IP addresses
invalid_ips = data[~data['source_ip'].astype(str).apply(is_valid_ip)] print(invalid_ips)
```
5. To identify invalid `destination_port` values, you can check if the port numbers are within the valid range (0-65535):
```
def is_valid_port(port): 
	try: 
		port = int(port) 
		return 0 <= port <= 65535 
	except ValueError: 
		return False

# Check for invalid port numbers invalid_ports = data[~data['destination_port'].apply(is_valid_port)] 
print(invalid_ports)
```

6. To identify invalid `protocol` values, you can check against a list of known protocols:
```
valid_protocols = ['TCP', 'TLS', 'SSH', 'POP3', 'DNS', 'HTTPS', 'SMTP', 'FTP', 'UDP', 'HTTP'] 

# Check for invalid protocol values invalid_protocols = data[~data['protocol'].isin(valid_protocols)] 
print(invalid_protocols)
```

### Checking for Invalid Bytes Transferred

7. To identify invalid `bytes_transferred` values, you can check if the values are numeric and non-negative:
```
def is_valid_bytes(bytes):
    try:
        bytes = int(bytes)
        return bytes >= 0
    except ValueError:
        return False

# Check for invalid bytes transferred
invalid_bytes = data[~data['bytes_transferred'].apply(is_valid_bytes)]
print(invalid_bytes)
```

### Checking for Invalid Threat Levels

8. To identify invalid `threat_level` values, you can check if the values are within a valid range (e.g. 0-2):
```
def is_valid_threat_level(threat_level):
    try:
        threat_level = int(threat_level)
        return 0 <= threat_level <= 2
    except ValueError:
        return False

# Check for invalid threat levels
invalid_threat_levels = data[~data['threat_level'].apply(is_valid_threat_level)]
print(invalid_threat_levels)
```

---
# Handling Invalid Entries

There are a few different ways we can approach this bad data.

## Dropping Invalid Entries

The most straightforward approach is to discard the invalid entries entirely.

> This ensures the remaining dataset is clean and free of potentially misleading information.

```
# the ignore errors covers the fact that there might be some overlap between indexes that match other invalid criteria
data = data.drop(invalid_ips.index, errors='ignore')
data = data.drop(invalid_ports.index, errors='ignore')
data = data.drop(invalid_protocols.index, errors='ignore')
data = data.drop(invalid_bytes.index, errors='ignore')
data = data.drop(invalid_threat_levels.index, errors='ignore')

print(data.describe(include='all'))
```

Preferred when data accuracy is paramount, and losing some data points does not significantly compromise the overall analysis.

> Not always feasible though, especially if the dataset is small or the invalid entries are a substantial portion of the data.

> After dropping the bad data from our dataset, we are only left with 77 clean entries.

It is sometimes possible to clean or transform invalid entries into valid and usable data instead of discarding them, which retains as much information as possible.

## Imputing Missing Values

`Imputing` is the process of replacing missing or invalid values in a dataset with estimated values.

> Crucial for maintaining the integrity and usability of the data, especially in ML tasks where missing values lead to biased or inaccurate results.

9. First, convert all invalid or corrupted entries, such as `MISSING_IP`, `INVALID_IP`, `STRING_PORT`, `UNUSED_PORT`, `NON_NUMERIC`, or `?`, into `NaN`.

> This standardizes the representation of missing values, so the downstream imputation steps are uniform.

```
import pandas as pd
import numpy as np
import re
from ipaddress import ip_address

df = pd.read_csv('demo_dataset.csv')

invalid_ips = ['INVALID_IP', 'MISSING_IP']
invalid_ports = ['STRING_PORT', 'UNUSED_PORT']
invalid_bytes = ['NON_NUMERIC', 'NEGATIVE']
invalid_threat = ['?']

df.replace(invalid_ips + invalid_ports + invalid_bytes + invalid_threat, np.nan, inplace=True)

df['destination_port'] = pd.to_numeric(df['destination_port'], errors='coerce')
df['bytes_transferred'] = pd.to_numeric(df['bytes_transferred'], errors='coerce')
df['threat_level'] = pd.to_numeric(df['threat_level'], errors='coerce')

def is_valid_ip(ip):
    pattern = re.compile(r'^((25[0-5]|2[0-4][0-9]|[01]?\d?\d)\.){3}(25[0-5]|2[0-4]\d|[01]?\d?\d)$')
    if pd.isna(ip) or not pattern.match(str(ip)):
        return np.nan
    return ip

df['source_ip'] = df['source_ip'].apply(is_valid_ip)
```

> After this step, `NaN` represents all missing or invalid data points.

10. For basic numeric columns like `bytes_transferred`, use simple methods such as the median or mean. For categorical columns like `protocol`, use the most frequent value.

```
from sklearn.impute import SimpleImputer

numeric_cols = ['destination_port', 'bytes_transferred', 'threat_level']
categorical_cols = ['protocol']

num_imputer = SimpleImputer(strategy='median')
df[numeric_cols] = num_imputer.fit_transform(df[numeric_cols])

cat_imputer = SimpleImputer(strategy='most_frequent')
df[categorical_cols] = cat_imputer.fit_transform(df[categorical_cols])
```

> These ensure all columns have valid, non-missing values, but they do not consider complex relationships among features.

11. For more sophisticated scenarios, use advanced techniques like `KNNImputer` or `IterativeImputer`.

> These consider relationships among features to produce contextually meaningful imputations.

```
from sklearn.impute import KNNImputer

knn_imputer = KNNImputer(n_neighbors=5)
df[numeric_cols] = knn_imputer.fit_transform(df[numeric_cols])
```

12. After cleaning and imputations, apply domain knowledge.

- For `source_ip` values that remain missing, assign a default such as `0.0.0.0`.
- Validate `protocol` values against known valid protocols.
- For ports, ensure values fall within the valid range `0-65535`.
- For protocols that imply certain ports, consider mode-based assignments or domain-specific mappings.

```
valid_protocols = ['TCP', 'TLS', 'SSH', 'POP3', 'DNS', 'HTTPS', 'SMTP', 'FTP', 'UDP', 'HTTP']
df.loc[~df['protocol'].isin(valid_protocols), 'protocol'] = df['protocol'].mode()[0]

df['source_ip'] = df['source_ip'].fillna('0.0.0.0')
df['destination_port'] = df['destination_port'].clip(lower=0, upper=65535)
```

13. Perform final verification steps to confirm that distributions are reasonable and categorical sets remain valid.

```
print(df.describe(include='all'))
```

> Adjust imputation strategies and transformations or remove problematic records if anomalies persist.

---
---
---
# Data Transformation

`Data transformations` improve the representation and distribution of features, making them more suitable for machine learning models.

---
## Encoding Categorical Features

`Encoding` converts categorical values into numeric form so algorithms can use them.

- `OneHotEncoder` : Binary column per category.
- `LabelEncoder` : Integer codes, but implies unintended order.
- `HashingEncoder` : For high-cardinality features, controls feature space size.

> Check the encoded features don't introduce artificial ordering.

### One-Hot Encoding

Turns one categorical feature into a binary column per category value, holding `1` or `0`.

Eg: `color` (red/green/blue) becomes 3 columns:

- `color_red`
- `color_green`
- `color_blue`

A row where `color` = red gets `1` in `color_red`, `0` in the other two.

> Stops the model reading categories as a numeric hierarchy.

> Downside: feature count explodes on high-cardinality columns.

14. Encode the `protocol` feature.
```
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(handle_unknown='ignore', sparse_output=False)
encoded = encoder.fit_transform(df[['protocol']])

encoded_df = pd.DataFrame(encoded, columns=encoder.get_feature_names_out(['protocol']))
df = pd.concat([df.drop('protocol', axis=1), encoded_df], axis=1)
```

---
## Handling Skewed Data

`Skewed` = most values clustered at one end, a few extremes stretching the distribution.

> Hurts models that are sensitive to outliers or assume normal-like distributions.

A `log` transform compresses large values more than small ones, evening it out.

15. Log transform with `log1p`.
```
import numpy as np

df["bytes_transferred"] = np.log1p(df["bytes_transferred"])  # Add 1 to avoid log(0)
```
> `log1p` adds 1 first, so it still works at or near zero.

> No info is lost, the outliers just stop dominating.

---
## Data Splitting

Split into 3 subsets so evaluation is reliable.

- `Training Set` : Fit the model. 60-80%.
- `Validation Set` : Tune hyperparameters, model selection. 10-20%.
- `Test Set` : Only after all tuning is done. 10-20%.

16. Split with `train_test_split`.
```
from sklearn.model_selection import train_test_split

X = df.drop("threat_level", axis=1)
y = df["threat_level"]

# 80% training, 20% testing
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1337)

# from that 80%: 60% training, 20% validation
X_train, X_val, y_train, y_val = train_test_split(X_train, y_train, test_size=0.25, random_state=1337)
```
> `test_size=0.25` is 25% of the 80% subset. `0.8 x 0.25 = 0.2`, so 60/20/20 overall.

- Train on `X_train`, `y_train`.
- Tune on `X_val`, `y_val`.
- Evaluate once on `X_test`, `y_test`.


# Metrics for Evaluating a Model
Metrics quantify the relationship between predictions and the known ground-truth labels.

> `accuracy`, `precision`, `recall` and `F1-score` were covered in Fundamentals of AI.

---
## Accuracy

Proportion of correct predictions out of all predictions made.

- Overall correctness.
- `(true positives + true negatives) / (all instances)`
- Misleading with class imbalance.

Eg: 1% of emails are spam. A model that calls every email legitimate gets `accuracy: 0.99` and catches zero spam.

> Accuracy hides total failure on the minority class.

## Precision

How often the predicted positives are actually positive.

- Quality of positive predictions.
- `true positives / (true positives + false positives)`
- High `precision` = fewer false alarms.

Eg: flags 100 emails as spam, 99 really are = high precision. Legit mail doesn't get lost.

> Says nothing about how much spam it missed.

## Recall

Ability to find all the positive instances.

- Completeness of positive detection.
- `true positives / (true positives + false negatives)`
- High `recall` = fewer missed cases.

Eg: flags nearly all spam, little slips through.

> High `recall` + low `precision` = spam folder full of legit mail.

## F1-Score

Harmonic mean of `precision` and `recall`.

- Balances the two.
- `2 * (precision * recall) / (precision + recall)`
- Useful for class imbalance.

> Use when both missing spam and losing legit mail are costly.

## Other Metrics

- `Specificity` : How well it identifies negatives.
- `AUC` : Area Under the ROC Curve, discriminative ability across thresholds.
- `Matthews Correlation Coefficient` : For highly imbalanced datasets.
- `Confusion Matrix` : Predictions vs true labels, full view of performance.

---
## Contextualizing the Metrics

Ask:

- Are the metrics consistent across different segments of the data?
- Does the dataset reflect real-world conditions, class imbalance included?
- Is the cost of a false positive vs a false negative accounted for?

> High `accuracy` is easy if negatives are overrepresented. Check that `precision` and `recall` both hold up.

Trade-offs:

- Threat detection: favor `recall`. Missing a threat costs more than a false alarm.
- Limited resources: favor `precision`. Chasing false alarms burns analyst time.
