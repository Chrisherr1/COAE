
We will use Naive Bayes for Spam detection.

Recap: 
`P(A|B) = (P(B|A) * P(A)) / P(B)`
- `P(A|B)` is the probability of event `A` occurring, given that `B` is true.
- `P(B|A)` is the probability of event `B` occurring, given that `A` is true.
- `P(A)` is the prior probability of event `A`.
- `P(B)` is the prior probability of event `B`.

A = Likelihood of Spam
B = Likelihood of it having certain features (words, phrases, etc).


1. What is the probability that an email is spam given features?
	1. P(Spam|Features)
2.  What is the probably of it having certain features given that we know the email is spam?
	1. P(Features|Spam)
3. What is the probability that any email is spam regardless of it's features.
	1. P(Spam)
4. What is the probability of seeing the features regardless if it is spam or not?
	1. P(Features)

```
P(Spam|Features) = (P(Features|Spam) * P(Spam)) / P(Features)
```

> Naive Bayes makes the "naive" assumption that the presence of a particular feature in an email is independent of the presence of any other feature, given the class label

`P(Features|Spam) = P(feature1|Spam) * P(feature2|Spam) * ... * P(featureN|Spam)`

Same for non-spam emails:
`
P(Features|Not Spam) = P(feature1|Not Spam) * P(feature2|Not Spam) * ... * P(featureN|Not Spam)`

> Using these probabilities we can calculate the posterior probability of an email being spam or not spam given its features.

The class with the higher `postier probability` is chosen as the predicted class.

---
---
# Example Calculation

Email with features `F1` and `F2`. Is it spam?

Given:

- `P(Spam) = 0.3` : Prior probability that any email is spam.
- `P(Not Spam) = 0.7` : Prior probability that any email is not spam.
- `P(F1|Spam) = 0.4`
- `P(F2|Spam) = 0.5`
- `P(F1|Not Spam) = 0.2`
- `P(F2|Not Spam) = 0.3`

1. Naive Bayes assumption, so multiply the feature probabilities:
```
P(F1, F2|Spam) = P(F1|Spam) * P(F2|Spam) = 0.4 * 0.5 = 0.2
P(F1, F2|Not Spam) = P(F1|Not Spam) * P(F2|Not Spam) = 0.2 * 0.3 = 0.06
```

2. Bayes' Theorem:
```
P(Spam|F1, F2) = (P(F1, F2|Spam) * P(Spam)) / P(F1, F2)
```

3. Get `P(F1, F2)` with the law of total probability:
```
P(F1, F2) = P(F1, F2|Spam) * P(Spam) + P(F1, F2|Not Spam) * P(Not Spam)
          = (0.2 * 0.3) + (0.06 * 0.7)
          = 0.06 + 0.042
          = 0.102
```

4. Spam:
```
P(Spam|F1, F2) = (0.2 * 0.3) / 0.102
               = 0.06 / 0.102
               ≈ 0.588
```

5. Not spam:
```
P(Not Spam|F1, F2) = (0.06 * 0.7) / 0.102
                   = 0.042 / 0.102
                   ≈ 0.412
```

> `P(Spam|F1, F2) > P(Not Spam|F1, F2)` so the email is classified as spam.

> Shortcut: `P(F1, F2)` is the same denominator for both classes. If you only need the predicted class and not the actual probability, compare the numerators (`0.06` vs `0.042`) and skip steps 3-5.

----
---
---
## SMS Spam Collection dataset 

- **Size:** 5,574 text messages
- **Labels:** each message is tagged either `ham` or `spam`
    - **ham:** legitimate messages the recipient actually wants, such as texts from known contacts, subscriptions, or newsletters
    - **spam:** unsolicited messages that offer no benefit and can be risky or deceptive
- **Why it exists:** most spam filtering datasets were built for email, so this one targets SMS specifically
- **Use case:** training and testing models that tell real messages apart from spam
- **Download:** [sms+spam+collection.zip](https://archive.ics.uci.edu/static/public/228/sms+spam+collection.zip)


# First: Grabbing the data
## Code For NoteBook:
---
```python

import requests
import zipfile
import io

# URL of the dataset
url = "https://archive.ics.uci.edu/static/public/228/sms+spam+collection.zip"
# Download the dataset

response = requests.get(url)
if response.status_code == 200:
    print("Download successful")
else:
    print("Failed to download the dataset")


```
* Requests library is used to send a HTTP GET request to the URL of the dataset.

```python
# Extract the dataset
with zipfile.ZipFile(io.BytesIO(response.content)) as z:
    z.extractall("sms_spam_collection")
    print("Extraction successful")
```
```python
import os

# List the extracted files
extracted_files = os.listdir("sms_spam_collection")
print("Extracted files:", extracted_files)
```
* The Dataset was received via .zip so we need to extract it via zipfile and io libraries.

* Response content contains Binary so we need to convert it to bytes-like object that can be processed by `zipfile.ZipFile`.

* The `extractall()` extracts all files from the archive into a specified directory. (sms_spam_collection)

* `os.listdir` lists all files and directories in a specified path, allowing us to confirm that `SMS SpamCollectionfile` is present.

```python
import pandas as pd

# Load the dataset
df = pd.read_csv(
    "sms_spam_collection/SMSSpamCollection",
    sep="\t",
    header=None,
    names=["label", "message"],
)

```
* We can now load it into pandas DataFrame for further analysis.
* The dataset is stored in a TSV file format, we specify it via `pd.read_csv`.
```python
# Display basic information about the dataset
print("-------------------- HEAD --------------------")
print(df.head())
print("-------------------- DESCRIBE --------------------")
print(df.describe())
print("-------------------- INFO --------------------")
print(df.info())
```
*  This helps us understand the dataset a little better.
```python
# Check for missing values
print("Missing values:\n", df.isnull().sum())
```
* Checks for missing values.
```python
# Check for duplicates
print("Duplicate entries:", df.duplicated().sum())

# Remove duplicates if any
df = df.drop_duplicates()

```
* Duplicated returns a boolean series tells us each row is a duplicate or not.
* Sum will just add up the number of duplicates, by addin gup everytime duplicated returns true.
* We then remove the duplicates using drop_duplicates.

--- 
# NEXT UP :  Preprocessing the text data.

Preprocessing standardizes the text, reduces noise, and extracts meaningful features, all of which improve the performance of the Bayes spam classifier.

> The steps outlined here rely on the `nltk` library for tasks such as tokenization, stop word removal, and stemming.

```python
import nltk

# Download the necessary NLTK data files
nltk.download("punkt")
nltk.download("punkt_tab")
nltk.download("stopwords")

print("=== BEFORE ANY PREPROCESSING ===") 
print(df.head(5))
```
* `pnkt` for tokenization, and `stopwords` for removing common words that do not contribute to meaning.
* Doing this will prevent interruptions later process steps.
```python
# Convert all message text to lowercase 
df["message"] = df["message"].str.lower()
print("\n=== AFTER LOWERCASING ===")
print(df["message"].head(5))
```
*  This ensures that the classifier treats words equally, regardless of their original casing. 
* "Free" and "free" would be considered the same making it more consistent.
```python
import re 
# Remove non-essential punctuation and numbers, keep useful symbols like $ and !
df["message"] = df["message"].apply(lambda x: re.sub(r"[^a-z\s$!]", "", x)) 
print("\n=== AFTER REMOVING PUNCTUATION & NUMBERS (except $ and !) ===") 
print(df["message"].head(5))
```
* `$,!` may contain important context in spam messages.
* This section removals all characters other than lowercase letters.
* (whitespace, dollar signs, or exclamation marks)

You will need to balance between cleaning the data nd preserving important symbols helps the model concentrate on features relavant to disingushing spam from ham messages.

## Next up : Tokenizing the Text

`Tokenization` divides the message text into individual words or tokens, a crucial step before further analysis. By converting unstructured text into a sequence of words, we prepare the data for operations like removing stop words and applying stemming.

> `Each token corresponds to a meaningful unit`, allowing downstream processes to operate on smaller, standardized elements rather than entire sentences.

```python
from nltk.tokenize import word_tokenize

# Split each message into individual tokens
df["message"] = df["message"].apply(word_tokenize)
print("\n=== AFTER TOKENIZATION ===")
print(df["message"].head(5))
```

> Once tokenized, the dataset contains message represented as lists of words, ready for additional preprocessing steps that further refine the text data.

## Next up: Removing Stop Words

`Stop words` are words that don't add any meaningful context.

Removing them helps reduce noise and focuses the model on words most likely to help distinguish spam from ham messages.

> By reducing the number of non-informative tokens, we help the model learn more efficiently.

```python
from nltk.corpus import stopwords 

# Define a set of English stop words and remove them from the tokens 
stop_words = set(stopwords.words("english")) 
df["message"] = df["message"].apply(lambda x: [word for word in x if word not in stop_words]) 
print("\n=== AFTER REMOVING STOP WORDS ===")
print(df["message"].head(5))
```

The token lists are shorter at this stage and contain fewer on-informative words, setting a cleaner stage for future text transformations.

## Next up : Stemming 

`Stemming` normalizes words by reducing them to their base form (e.g., `running` becomes `run`).

By doing this it helps the model understand underlying concepts without having to deal with word variations.
```python
from nltk.stem import PorterStemmer 
# Stem each token to reduce words to their base form 
stemmer = PorterStemmer() 
df["message"] = df["message"].apply(lambda x: [stemmer.stem(word) for word in x]) 
print("\n=== AFTER STEMMING ===") 
print(df["message"].head(5))
```
> After stemming, the token lists focus on root word forms, further simplifying the text and improving the model’s generalization ability.

## Joining Tokens Back into a Single String

Rejoining the tokens into a space-separated string restores a format compatible with these methods, allowing the dataset to move seamlessly into the feature extraction phase.

```python
# Rejoin tokens into a single string for feature extraction 

df["message"] = df["message"].apply(lambda x: " ".join(x)) 
print("\n=== AFTER JOINING TOKENS BACK INTO STRINGS ===")
print(df["message"].head(5))
```

> At this point the message are fully preprocessed. Cleaned, normalized, for vectorization and subsequent model training, ultimately improving the classifier's performance.

# Feature Extraction

Feature extraction transforms preprocessed SMS messages into numerical vectors suitable for machine learning algorithms.

> Since models `cannot directly process raw text data`, they rely on numeric representations such as counts or frequencies of words to identify pattern that differentiate SPAM from HAM here.

## Representing Text as Numerical Features

A common way to represent text numerically is through a `bag-of-words` model.

This technique constructs a vocabulary of unique terms from the dataset and represents each message as a vector of term counts.

Each element in the vector corresponds to a term in the vocabulary, and its value indicates how often that term appears in the message.

---
### Quick bits :

Using only `unigrams` (individual words) does not preserve the original word order; it treats each document as a collection of terms and their frequencies, independent of sequence.

To introduce a limited sense of order, we also include `bigrams`, which are pairs of consecutive words. By incorporating bigrams, we capture some local ordering information.

---

`CountVectorizer` does not preserve complete word order; it only captures localized patterns defined by the chosen `ngram_range`