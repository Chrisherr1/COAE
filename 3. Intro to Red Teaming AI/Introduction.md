
Red teaming is made up of:

* `Red Team Assessments`: Can be traditional penetration testing with Social engineering.

* `Vulnerability Assessments`: More automated but focuses on finding known vulnerabilities within an org and documenting them.

> `Nessus` or `OpenVAS` are common scanners for Vulnerability Assessments.

## Red Teaming ML-based Systems

ML-based systems are uniquely vulnerable due it it's reliance on large data sets, statistical inference, and complex model architectures.

> Red team assessments  is preferred for security testing for ML-based systems.

ML-based systems are comprised of various components interacting with each other, these interaction points are points of weakness.

And should be documented.

# ML OWASP TOP 10

| ML01 | `Input Manipulation Attack`: Attackers modify input data to cause incorrect or malicious model outputs.                                                                               |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
![[Pasted image 20261115104932.png]]

> [!note] Notes:
> Many real world manipulation attack vectors involve applying small perturbations to benign input data, resulting in unexpected behavior from the ML model.
> 
> https://arxiv.org/pdf/1707.08945 , https://arxiv.org/pdf/2307.08278


| ML02 | `Data Poisoning Attack`: Attackers inject malicious or misleading data into training data, compromising model performance or creating backdoors. |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------ |

> [!note] Notes:
> * The quality of any ML model is highly dependent on the quality of the training data. 
>* These attacks can cause incorrect predictions, misclassify certain inputs, or behave unpredicably in specific scenarios.
> * Unverified or publicly sourced data could make the ML vulnerable to this.
> * https://arxiv.org/pdf/2408.13221

| ML03 | `Model Inversion Attack`: Attackers train a separate model to reconstruct inputs from model outputs, potentially revealing sensitive information. |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
> [!note] Notes:
> * The attacker's model inverts the target's functionality. Often called 'Model inversion attack'.
> * More challenging to execute if the target model provides less output information. 
> * If the model only gives the target class instead of every output probability.
> * https://arxiv.org/pdf/2311.13647

| ML04 | `Membership Inference Attack`: Attackers analyze model behavior to determine whether data was included in the model's training data set, potentially revealing sensitive information. |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
![[Pasted image 20261115105146.png]]
> [!note] Notes:
> * If the model is trained on sensitive data such as medical information, this can pose privacy issues.
> * More concerning with Public or Shared models accessible over the cloud.
> * Attack tries to see if it can remember data points from the training process.

| ML05 | `Model Theft`: Attackers train a separate model from interactions with the original model, thereby stealing intellectual property. |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------- |
![[Pasted image 20261115105213.png]]
> [!note] Notes:
> * Attackers try to guess it's decision making process by gathering data about its decision-making behavior to duplicate it.
> * https://arxiv.org/pdf/2305.13584

| ML06 | `AI Supply Chain Attacks`: Attackers exploit vulnerabilities in any part of the ML supply chain. |
| ---- | ------------------------------------------------------------------------------------------------ |
> [!note] Notes:
> * This can be vulnerabilities in third-party data sources, libraries, or pre-trained models, to compromise the model's integrity, security, or performance.
> * Risk has increased in ML systems due to the reliance on open-source tools, public data sets, and pre-trained models from external sources.

| ML07 | `Transfer Learning Attack`: Attackers manipulate the baseline model that is subsequently fine-tuned by a third-party. This can lead to biased or backdoored models. |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
> [!note] Notes:
>* Open-source pre-trained models are used all the time as baselines for many ML model deployments due to the cost of training models from scratch.
>* New models are built on these.
>* Security issues arise such as backdoors or biases may arise even after fine tuning.


| ML08 | `Model Skewing`: Attackers skew the model's behavior for malicious purposes, for instance, by manipulating the training data set. |
| ---- | --------------------------------------------------------------------------------------------------------------------------------- |
> [!note] Notes:
> * They can achieve this by injecting biased, misleading, or incorrect data into the training data set to influence the model's output toward maliciously biased outcomes.
> * Trying to label something as harmless even when it isn't.


| ML09 | `Output Integrity Attack`: Attackers manipulate a model's output before processing, making it look like the model produced a different output. |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
> [!note] Notes:
> * It doesn't effect the model directly, it intercepts the model's output before the respective target entity processes it.
> * It manipulates the output to make it appear as through the model has produced a different result.
> * Eg: If we can alter the output to prevent something from being labeled as bad, then we can bypass restrictions.



| ML10 | `Model Poisoning`: Attackers manipulate the model's weights, compromising model performance or creating backdoors.                             |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
> [!note] Notes:
> * Model Poisoning is more about attacks targeting the model's parameters, rather than the training data(Data Poisioning).
> * This can be rather challenging, it requires getting the model to deviate from it's intended behavior.
> * This vulnerability can lead to incorrect predications, misclassifications of certain inputs or unpredicatable behavior.
