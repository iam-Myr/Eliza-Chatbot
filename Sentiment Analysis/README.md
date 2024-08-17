# Sentiment Analysis

**Author:** Myriam Kapon - aid24008  
**Date:** 22/04/24

## Approach

This project focuses on developing straightforward code to implement various sentiment analysis options. The approach includes different preprocessing techniques, the flexibility to choose vector models and parameters for fine-tuning, and the option to select different classifiers. The goal is to allow users to experiment with different combinations easily, enabling them to identify the optimal choice and analyze and interpret the results effectively.

## Data Exploration

Before starting the analysis, the dataset was examined to ensure that the classes are balanced:

- **Number of positive reviews:** 1000
- **Number of negative reviews:** 1000
- **Total words:** 1,583,820
- **Number of words in positive reviews:** 832,564
- **Number of words in negative reviews:** 751,256

**Most popular words:**
- **In positive reviews:** `(',', 42,448)`, `('the', 41,471)`, `('.', 33,714)`
- **In negative reviews:** `(',', 35,269)`, `('the', 35,058)`, `('.', 32,162)`

The dataset is balanced, with positive reviews containing slightly more words. Given the frequency of common words, some word preprocessing was necessary.

## Preprocessing

The preprocessing pipeline was designed for flexibility, allowing easy enabling or disabling of different steps:

- **Tokenization (default):** Splits the review into individual tokens.
- **Lowercasing:** Converts all characters to lowercase to ensure consistency.
- **Removal of punctuation:** Removes common punctuation marks like commas and periods.
- **Removal of non-alphabetic characters:** Ensures only alphabetic characters remain.
- **Lemmatization:** Reduces words to their base or root form.
- **Stemming:** Reduces words to their root forms by removing prefixes and suffixes.
- **Removal of stopwords:** Eliminates common words like "and", "the", and "a".
- **Removal of short words:** Filters out single-character words.

More aggressive preprocessing was applied to models trained from scratch, while less aggressive preprocessing was used for pretrained models, which already possess an understanding of normal words and their variations.


## Word Vectors

The Word2Vec model from the Gensim library was used to convert words into vectors. Both custom-trained and pretrained models were examined.

### Custom Trained Model

- **Vector size:** 256 (chosen to encapsulate a large dimensionality).
- **Strategies experimented:**
  1. **Not-word:** Combines words prefixed with "not" into a single token (e.g., "not-good").
  2. **Default Vector for Unknown:** Assigned a default vector of zeroes to unknown words.
  3. **Labels as Words:** Appended "positive" and "negative" labels after each sentence for context.

**Antonymy Problem:**
- The model struggled with recognizing opposites like "good" and "bad" as distinct, leading to issues in sentiment analysis.

### Pretrained Model

- **Trained on:** Twitter data (similar to conversational style in movie reviews).
- **Best Performance:** Achieved with a pretrained model on the Google News Dataset, resulting in an accuracy of 83%.

## Classification

The following classifiers were tested:
1. Linear Discriminant Analysis (LDA)
2. Logistic Regression
3. Decision Tree
4. Random Forest
5. K-Nearest Neighbors (kNN)
6. Naive Bayes
7. Support Vector Machines (SVM)

### Results

**Final Setup:**
- **Preprocessing:** Lowercase, Remove Punctuation, Lemmatize, Remove Short Words.
- **Model:** Sample Pretrained Word2Vec Model.

| Classifier            | Accuracy | Precision | Recall  | F1      | Roc-Auc  | Sensitivity | Specificity |
|-----------------------|----------|-----------|---------|---------|----------|-------------|-------------|
| Decision Tree         | 0.655504 | 0.651172  | 0.668087| 0.658327| 0.655552 | 0.668087    | 0.643017    |
| LDA                   | 0.837992 | 0.834672  | 0.842984| 0.838797| 0.837988 | 0.842984    | 0.832992    |
| Logistic Regression   | 0.678000 | 0.682243  | 0.667011| 0.674333| 0.678000 | 0.667011    | 0.688988    |
| Naive Bayes           | 0.685002 | 0.692934  | 0.665012| 0.678525| 0.684993 | 0.665012    | 0.704974    |
| Random Forest         | 0.713499 | 0.720779  | 0.698000| 0.709009| 0.713484 | 0.698000    | 0.728968    |
| SVM                   | 0.668499 | 0.663818  | 0.688053| 0.674433| 0.668552 | 0.688053    | 0.649050    |
| kNN                   | 0.654517 | 0.656102  | 0.652014| 0.653895| 0.654526 | 0.652014    | 0.657037    |

Based on average scores across three folds, LDA emerged as the top-performing classifier in terms of accuracy and F1 score, achieving an accuracy and F1 score of 0.84.

## Thoughts

Preprocessing was crucial for achieving high accuracy, but using a pretrained model was the most significant factor. Despite various attempts, it was challenging to prevent "good" and "bad" from being considered similar due to the inherent limitations of word embeddings. Further experimentation with different preprocessing techniques, model training strategies, vector sizes, and classifier parameters could yield even better results.


