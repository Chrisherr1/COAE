# Supervised Learning Algorithms

`Supervised learning` algorithms form the cornerstone of many Machine Learning (ML) applications, enabling systems to learn from labeled data and make accurate predictions.

Each data point is associated with a known outcome or label in supervised learning.

Think of it as having a set of examples with the correct answers already provided.

> The algorithm aims to learn a mapping function to predict the label for new, unseen data.
---
 
## Supervised learning problems can be broadly categorized into two main types:

`Classification`: In classification problems, the goal is to predict a categorical label.
> For example, classifying emails as spam or not or identifying images of cats, dogs, or birds.

`Regression`: In regression problems, the goal is to predict a continuous value.
> For example, one could predict the price of a house based on its size, location, and other features or forecast the stock market.

---
---
---
# Linear Regression 

Fundamental to `supervised learning`, it is used to predict a continuous target variable by establishing a linear relationship between the target and one or more predictor variables.

> The goal is to find the best fitting line that minimizes the sum of the squared differences between the predicted values and actual values.

---

## What is Regression?

Regression analysis is a type of supervised learning where the goal is to predict a continuous target variable.

hink of it as estimating a number instead of classifying something into categories.

eg:
Predicting the price of a house based on its size, location, and age.

Forecasting the daily temperature based on historical weather data.

Estimating the number of website visitors based on marketing spend and time of year.


> In all these cases, the output we're trying to predict is a continuous value. This is what distinguishes regression from classification, where the output is a categorical label (e.g., "spam" or "not spam").

---

## Simple Linear Regression

`y = mx + c`

`y` is the predicted target variable
`x` is the predictor variable
`m` is the slope of the line (representing the relationship between x and y)
`c` is the y-intercept (the value of y when x is 0)

> The algorithm aims to find the optimal values for `m` and `c` that minimize the error between the predicted `y values` and the actual `y values` in the training data.

This is often done using OLS(Ordinary Least Squares), which aims to minimize the sum of squared errors.

##  Multiple Linear Regression 

> When multiple predictor variables are involved.

y = b0 + b1x1 + b2x2 + ... + bnxn

`y` is the predicted target variable
`x1, x2, ..., xn` are the predictor variables
`b0` is the y-intercept
`b1, b2, ..., bn` are the coefficients representing the relationship between each predictor variable and the target variable.

---

# Ordinary Least of Squares

Common for estimating the optimal values for the coefficients in a linear regression.

> It claims to minimize the sum of the square differences between the actual values and the values predicted by the model.

## OLS Process

1. `Calculate Residuals:` For each data point, the `residual` is the difference between the actual `y` value and the `y` value predicted by the model.
2. `Square the Residuals:` Each residual is squared to ensure that all values are positive and to give more weight to larger errors.
3. `Sum the Squared Residuals:` All the squared residuals are summed to get a single value representing the model's overall error. This sum is called the `Residual Sum of Squares` (RSS).
4. `Minimize the Sum of Squared Residuals:` The algorithm adjusts the coefficients to find the values that result in the smallest possible RSS.

> Think of finding the line that minimizes the total area of squares formed between the data points and line...

## General Assumptions of Linear Regression

Linearity, Independence, Homoscedasticity, Normality

> If these assumptions are violated, the model's predictions may be inaccurate or misleading.
---
---
---
# Logistic Regression

It is a supervised learning algorithms primarily used for classification, not regression.

It predicts a categorical target variable with two possible outcomes(binary classification). This outcomes are typically represented as binary values (0 or 1)(true or false).

The algorithm models the probability of the target variable belonging to a particular class using a logistic function, which maps the input features to a value between 0 and 1.

> For example, logistic regression can predict whether an email is spam or not or whether a customer will click on an ad.

## What is Classification?

Classification is a type of supervised learning that aims to assign data points to specific categories or classes.

Unlike regression, which predicts a continuous value, classification predicts a discrete label.

Eg: 
- Identifying fraudulent transactions (fraudulent or not fraudulent)
- Classifying images of animals (cat, dog, bird, etc.)
- Diagnosing diseases based on patient symptoms (disease present or not present)

> In all these cases, the output we're trying to predict is a category or class label.

# How Logistic Regression Works

Unlike `linear regression`, which outputs a continuous value, `logistic regression` outputs a probability score between 0 and 1.

>This score represents the likelihood of the input belonging to the positive class (typically denoted as '1').

Uses `Sigmoid function` which maps any input value to a value within 0 to 1 range.

This allows the model to capture complex relationships between the features and probability of the outcome.

> The score represents the likelyhood of the input belonging to the positive class.

## The Sigmoid Function

`P(x) = 1 / (1 + e^-z)`

It's a function that takes a input (-infinity to infinity) and maps it to an output value between 0 and 1.

Starts negative then rapidly increases at 0 and plateaus at high values for positive ones.

> This allows it to represent the probability of an event occurring.

In logistic regression, the sigmoid function transforms the linear combination of input features into a probability score

---
## How its used in Spam detection

Assume we are making a spam filter using `Logistic regression`.

It would analyze `sender's email,presense of keywords, content,` and make a probability score.

It would be considered spam if it exceeded a predefined threshold (.8).

---
## What is Decision Boundary in Logistic Regression

It's the line separator that separates the data points into two classes.

It acts like a decision boundary, and it's made by the models learned parameters and the chosen threshold probability.

---
## What is a hyperplane in Logistic Regression

It's a subspace whose dimension is less than that of the ambient space.

- A hyperplane is simply a line in a 2-dimensional space (like a sheet of paper) that divides the space into two regions.
- A hyperplane is a flat plane in a 3-dimensional space (like your room) that divides the space into two halves.

In logistic regression, the hyperplane is defined by the model's learned parameters (coefficients) and the chosen threshold probability.

 It acts as the decision boundary, separating data points into classes based on their predicted probabilities.
 
---
## Threshold Probability

The threshold probability is often set at 0.5 but can be adjusted depending on the specific problem and the desired balance between true and false positives.

If P(x) is above the threshold, then its positive class.

If P(x) is above the threshold, then its negative class.

The probability threshold just tells us what is the needed probability for something to be classified as something (spam for example).

---
## Data Assumptions

* The target variable must be categorical with only two possible outcomes.

* It assumes a linear relationship between predictor variables and log-odds of the outcome.

* Ideally, there should be little to no `multicollinearity` among the predictor variables. `Multicollinearity` occurs when predictor variables are highly correlated, making it difficult to determine their individual effects on the outcome

- Logistic regression performs better with larger datasets, allowing for more reliable parameter estimation.


---
---
---
# Decision trees

Popular `Supervised learning` algorithm for classification and regression tasks.

It creates a model that predicts the value of a target variable by learning simple decision rules inferred from the data's details.

Imagine you're trying to decide whether to play tennis based on the weather. A decision tree would break down this decision into a series of simple questions: Is it sunny? Is it windy? Is it humid?

`Root Node` - Starting point of tree.
`Internal Nodes` - represents features of data and contains other nodes representing decisions.
`Leaf Nodes` - Ending Nodes, representing final outcome or prediction.

---
## Building a Decision Tree

It involves picking the best feature to split the data at each node.

`Gini impurity`, `entropy`, or `information gain` is used to quantify the homogeneity of the subsets resulting from the split.

The goal is to create splits that result in increasingly pure subsets, where the data points within each subset belong predominantly to the same class.

---



---
---
---

## Keywords

> [!note] Training data
> Think of training data as a set of example problems with their correct solutions

> [!note] Features
> They are the variables that the algorithm uses to learn and make predictions.
> > EG: When predicting a house price, feature might include: Size,Number of bedrooms,Location, Age of the house

> [!note] Labels
> They represent the "correct answers" that the model aims to predict.
> > EG: In predicting house price, the label would be the acutal price of the house.

> [!note] Model
> The model can be considered a function that takes the features as input and outputs a prediction for the label.

> [!note] Training
> Training is the process of feeding the training data to the algorithm and adjusting the model's parameters to minimize prediction errors.

> [!note] Prediction
> Once the model is trained, it can be used to predict new, unseen data.
>
> This involves providing the model with the features of the new data point, and the model will output a prediction for the label.

> [!note] Inference
> It involves using a trained model to derive insights, estimate parameters, and understand relationships between variables.
> > Inference often focuses on explaining and interpreting results.

> [!note] Evaluation
> It involves assessing the model's performance to determine its accuracy and generalization ability to new data.
> > Accuracy,Precision,recall,F1-score

> [!note] Generalization
> refers to the model's ability to accurately predict outcomes for new, unseen data not used during training.
> > A good model that generalizes well will work well in real-world scenarios.

> [!note] Overfitting
> Model learns training data TOO well, and memorizes generalizations of new data rather than underlying patterns.

> [!note] Underfitting
> Model too simle to capture the underlying patterns in the data.
> > This results in poor performance in the training data and new unseen data.

> [!note] Cross-Validation
> It involves splitting the data into multiple subsets (folds) and training the model on different combinations of these folds while validating it on the remaining fold.
> > Helps reduce overfitting and provides more reliable estimate of the model's performance.

> [!note] Regularization
> a technique used to prevent overfitting by adding a penalty term to the loss function
> > This penalty discourages the model from learning overly complex patterns that might not generalize well.

> [!note] L1 Regularization
> Adds a penalty equal to the absolute value of the magnitude of coefficients.

> [!note] L2 Regularization
> Adds a penalty equal to the square of the magnitude of coefficients.

---