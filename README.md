# 1) Word Translation (Machine Translation)

## Goal: 

A program that translates English to French

## Approach: 

1) The word embeddings data for English and French words
2) Translations
3) LSH and document search
4) Looking up the tweets
5) Approximate K-NN


### Data: 
* English embeddings from Google code archive word2vec
[look for GoogleNews-vectors-negative300.bin.gz](https://code.google.com/archive/p/word2vec/)
    * You'll need to unzip the file first.
* and the French embeddings from
[cross_lingual_text_classification](https://github.com/vjstark/crosslingual_text_classification).


# 2) Multi-Class Classification and Rating Prediction of Yelp Dataset (Kaggle's Yelp Business Rating Prediction competition)

## Goal: Predict the star rating of a review using only the review text

## Approach: 

1) Split data into training and testing sets, using the review text as the only feature and the star rating as the response
2) Use CountVectorizer to create document-term matrices from X_train and X_test
3) Use multinomial Naive Bayes to predict the star rating for the reviews, calculate the accuracy by confusion matrix
4) Calculate the null accuracy (classification accuracy that could be achieved by always predicting the most frequent class)
5) Evaluating a classification model by "false positives" and "false negatives"
6) Calculate which 10 tokens are the most predictive of 5-star reviews, and which 10 tokens are the most predictive of 1-star reviews
7) Repeat the model building process using all reviews (instead of binary classification: 1-star and 5-star), 5-class classification 

## Results: 

### Binary Classification: 
- Accuracy: 92% (null accuracy 82%)
- False positive: Model is reacting to the words "good", "impressive", "nice"
- False negative: Model is reacting to the words "complain", "crowds", "rushing", "pricey", "scum"

### 5-Class Classification: 
- Accuracy: 47% 
- 47% accuracy is quite impressive, given that humans would also have a hard time precisely identifying the star rating for these reviews
- Precision: 54%
- Recall: 30%
- F1 score: 38%

## Interpretation: 

- Confusion matrix comments: Almost all 4-star and 5-star reviews are classified as 4 or 5 stars, but they are hard for the model to distinguish between, 1-star, 2-star, and 3-star reviews are most commonly classified as 4 stars, probably because it's the predominant class in the training data

- Classification report comments: Class 1 has low recall, meaning that the model has a hard time detecting the 1-star reviews, but high precision, meaning that when the model predicts a review is 1-star, it's usually correct, Class 5 has high recall and precision, probably because 5-star reviews have polarized language, and because the model has a lot of observations to learn from
