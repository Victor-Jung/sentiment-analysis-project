

##### Jung Victor*

---

# Sentiment Analysis Project

## Context

With the rise of social networks and deep learning techniques sentiment analysis became a must have for a lot of compagny wanted to know the public opinion. FIrst we will preprocess the dataset, then we will implement two models to evaluate if a tweet is positive or negative, one model will be very simple and act as a baseline and the second model will be more complex. We will then benchmark the baseline against the complex model.



## Our Dataset

We've got 1 600 000 tweets extracted using twitter API labelized as follow :

- 0 : negative
- 4 : positive

For each tweet we've got :

- the id 
- the data
- the username
- the text

This dataset has been created by Go, A., Bhayani, R. and Huang, L,  for Twitter sentiment classification using distant supervision. *CS224N Project Report, Stanford, 1(2009), p.12*.

## Our Approach

### Preprocessing

We first cleaned the dataset be replacing english contraction by the full words, for exemple "he's" become "he is". We also removed english stopwords, tweeter username and short word (less than 2 caracters). After that we used the Lancaster Stemmer and convert everything in lower case.

Then we use the pretrained GloVe 100 Model Embedding with max length of 20 and padding with zeros.

### Baseline Model

Below our baseline model summary, we're using a simple layer of 128 Simple RNN units followed by a 64 units ReLu Dense layer and a 2 classes Softmax classifier.![model_summary](./img/baseline_model_summary.png)

### Our Model

Here we've got 2 layers of LSTM instead of Simple RNN and we added Dropout to avoid ouverfitting on the data.

 ![model_summary](./img/model_summary.png)

### Performances

![loss](/home/victor/Documents/M1/NLP/SentimentAnalysisProject/img/loss.png)

Our LSTM Model is performing better than the baseline model, even if the baseline train loss is close to the LSTM train loss the baseline validation loss isn't following the baseline training loss.

It means our baseline model is overfitting it is maybe due to the lack of Dropout layers.

## Suggested Improvements

We could train more the LSTM model until find the overfit limit to push performances to the maximum, we also could focus more on the preprocessing by converting more abreviations like asap = as soon as possible.