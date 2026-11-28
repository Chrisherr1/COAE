
**Membership interference**, is when a machine learning model reveals specific details from the data that they were trained on.
> Core Vulnerability.

> OWASP ML Security TOP 10 - 
> *ML04:2023 - Membership inference
> ML03:2023 - Model inversion
> ML05:2023 - Model Theft

> If a model leaks membership, it likely leaks other information too.
> 
> Differential privacy is the recommended countermeasure, which is why we focus on DP-SGD and PATE in subsequent sections.

## What is membership Interference Attack (MIA)?

> Was a specific data point used to train a given model?

The attacker provides a sample and receives a binary answer based on how the model responds to the sample.(Boolean based)
> This can basically tell us yes or no, if something is within the data.


## MIA is a family of privacy attacks

> MIA attacks attempt to extract data in different ways.

> `MIA` success also serves as a privacy audit metric: if a model leaks membership, it likely leaks other information too.

1. A related threat comes from `attribute inference attacks`, where we deduce sensitive attributes not directly predicted by the model.
	* If a model predicts income and was trained on income data, querying it might reveal education levels or employment status of trainning members.

2. The most direct form of leakage occurs in `training data extraction attacks`, where we recover verbatim training examples from models.
	* LLMs that memorized specific sequences are vulnerable to this type ot approach.

## Why does MIA work?

