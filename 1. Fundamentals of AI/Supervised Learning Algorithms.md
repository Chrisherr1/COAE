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

At each node, the tree picks the feature that splits the data best.

It scores the options with Gini `impurity, entropy, or information gain`.

`Gini Impurity` gives up the probability of misclassifying a randomly chosen element from a set.
> A lower Gini means the set is more pure.

```
Gini(S) = 1 - Σ (pi)^2
```
S = Dataset, pi = number of elements in the set

Gini Impurity would be calculated for 2 classes would be 

Assuming...

Class A = 30 elements
Class B = 20 elements

```
Gini(S) = 1 - (pi)^

pi = pA + pB = (elements(A)/ Total Number of elements) + (elements(B)/ Total Number of elements)

Therefore, 1 - 0.52 = 0.48

This would be the Gini Impurity for the dataset.
```

---

### Entropy 

It measures the disorder/uncertainty in a set.

> Lower is better.

```
Entropy(S) = - Σ pi * log2(pi)
```

S = dataset, pi = proportional to elements belonging to a class (i) in the set.

Assuming..

- Proportion of class `A`: `pA = 0.6`
- Proportion of class `B`: `pB = 0.4`

```
Entropy(S) = - (0.6 * log2(0.6) + 0.4 * log2(0.4))

= 0.970954
```

> You probably just use a calculator, but note you need to be wary that most calculators don't convert the log2 correctly. 

---
### Information Gain

It measures the reduction in entropy achieve by splitting a set based on a particular feature.

The feature with the highest information again is chosen for the split.

```
Information Gain(S, A) = Entropy(S) - Σ ((|Sv| / |S|) * Entropy(Sv))
```

 `S` = dataset, 
 `A` = feature being used for splitting, 
 `Sv` = subset of `S` for which feature `A` has value `v`.

Assuming 50 instances in 2 classes A and B.

Suppose we consider a feature F that can take values 1 and 2.

AND

The distribution looks like...

- For `F = 1`: 30 instances, 20 class `A`, 10 class `B`
- For `F = 2`: 20 instances, 10 class `A`, 10 class `B`

Step 1 : Calculate entropy of the entire dataset S.
	```
	Entropy(S) = - (30/50 * log2(30/50) + 20/50 * log2(20/50)) 
	= - (0.6 * log2(0.6) + 0.4 * log2(0.4)) 
	= - (0.6 * (-0.73697) + 0.4 * (-1.32193)) 
	= 0.970954
	```
Step 2 : Calculate the entropy for each subset Sv.

- For `F = 1`:
    - Proportion of class `A`: `pA = 20/30 = 0.6667`
    - Proportion of class `B`: `pB = 10/30 = 0.3333`
    - Entropy(S1) = `- (0.6667 * log2(0.6667) + 0.3333 * log2(0.3333)) = 0.9183`
- For `F = 2`:
    - Proportion of class `A`: `pA = 10/20 = 0.5`
    - Proportion of class `B`: `pB = 10/20 = 0.5`
    - Entropy(S2) = `- (0.5 * log2(0.5) + 0.5 * log2(0.5)) = 1.0`

Step 3 : Calculate the weighted Average entropy of subsets.
```
Weighted Entropy = (|S1| / |S|) * Entropy(S1) + (|S2| / |S|) * Entropy(S2) 
= (30/50) * 0.9183 + (20/50) * 1.0 
= 0.55098 + 0.4 
= 0.95098
```

Step 4:  Calculate the information gain

```
Information Gain(S, F) = Entropy(S) - Weighted Entropy 
= 0.970954 - 0.95098 
= 0.019974
```

---
### Building the Tree

The tree starts with the root node and selectes the feature that best splits the data based on either Gini impurity , entropy, or information gain.

The features becomes the internal node and branches are created for each possible value or range of values of that feature.

The data is then divided into subsets based on the branches. 

The process continues recurisvely for each subset until a stopping citerion is met.

It stops if...

1. The Tree hits a max depth
2. The number of data points in a node falls below a threshold.
3. All data points in a node belong to the same class, so no point in splitting.

---
# The real method when turning table data into a tree.

1. Identify features that best separate the yes and no instances.
2. Calculate each feature's information gain and Gini impurity.
> By doing this, you can find which provides the most information for the split.

3. Find the one with highest information gain.
4.  You'll do this recursively until a stopping criterion is met. (as seen above).
5. Then once the tree is done you can use it to predict behavior.

---
## Data Assumptions

1.  They are more flexible than linear regressions. They can handle linear and non-linear relationships between features and the target variable.
2. The data doesn't need to be distributed, so it's nice.
3. Outliers are fine, the algorithm doesn't care much about them.

---
---
---
# Naive Bayes

> Used in spam filtering

This is a probabilistic algorithm used for classification tasks.

It's based on a concept, that the probably of something happening is based on prior knowledge or observations.

## Bayes Theorem

> Allows us to calculate the probability of something happening, given another event has occurred.

<3 the theorem!

```
P(A|B) = [P(B|A) * P(A)] / P(B)
```

- `P(A|B)`: The posterior probability of event `A` happening, given that event `B` has already happened.
- `P(B|A)`: The likelihood of event `B` happening given that event `A` has already happened.
- `P(A)`: The prior probability of event `A` happening.
- `P(B)`: The prior probability of event `B` happening.

---

Consider...

- The prevalence of the disease in the population is 1%, so `P(A) = 0.01`.
- The test is 95% accurate, meaning if someone has the disease, they will test positive 95% of the time, so `P(B|A) = 0.95`.
- The test has a false positive rate of 5%, meaning if someone does not have the disease, they will test positive 5% of the time.
- The probability of testing positive, `P(B)`, can be calculated using the law of total probability.


To calculate P(B):
```
P(B) = P(B|A) * P(A) + P(B|¬A) * P(¬A)
```
- `P(¬A)`: The probability of not having the disease, which is `1 - P(A) = 0.99`.
- `P(B|¬A)`: The probability of testing positive given that the person does not have the disease, which is the false positive rate, `0.05`.

```
P(B) = (0.95 * 0.01) + (0.05 * 0.99)
     = 0.0095 + 0.0495
     = 0.059
```
Finally we use bayes' theorem:
```
P(A|B) = [P(B|A) * P(A)] / P(B)
        = (0.95 * 0.01) / 0.059
        = 0.0095 / 0.059
        ≈ 0.161
```

> The prob of someone having a disease and testing positive is 16.1%!

## So how does Naive Bayes' work then?

It leverages Bayes' theorem to predict the probability of a data point belonging to a particular class given its features.

it assumes that the presence or absence of one feature doesn't effect the presence or absence of any other feature, given that we know the class label.

The Process:

1. Calculate the probability of each class, before considering it's features.
2. Calculate the likelyhood of observing each feature given each class.
3. Apply Bayes' Theorem.(Calculate the posterior probability).
4.  Finally, the algorithm assigns the data point to the class with the highest posterior probability.

Types of Naive bayes:

- `Gaussian Naive Bayes:`if predicting whether a customer will purchase a product based on their age and income, `Gaussian Naive Bayes` could be used, assuming age and income are normally distributed.

- `Multinomial Naive Bayes:` in spam filtering, the frequency of words like "free" or "money" might be the features, and `Multinomial Naive Bayes` would model the probability of these words appearing in spam and non-spam emails.

- `Bernoulli Naive Bayes:` This type is employed for binary features, where the feature is either present or absent. 
---
## Data Assumptions

1. The core assumption is that features are conditionally independent given the class.
2.  The choice of Naive Bayes classifier (Gaussian, Multinomial, Bernoulli) depends on the assumed distribution of the features.
3. You need enough data to estimate probabilities accurately.



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