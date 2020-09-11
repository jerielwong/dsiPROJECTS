# Project 3 - Investing and Trading Subreddits



## Problem Statement

Investing and Trading the word have been loosely used in the financial world. Many people have been posting in Investing, as they feel it is a more broadly used term Today i am trying to find out what do the world feel investing and trading should be. And explore what the textbook answer is.

To get the textbook answer, i use the source from Investopedia to analyse. Based on the key takeaways,

Investing can be summarised as long term approach to markets, purpose of retirement. Investors ride out shrot term losses.

Trading is summarised as short term strategies that maximize returns daily , monthly quarterly. Traders profit from fluctuating markets.


## Solution 

To solve this, i aim to build a classification model to correctly identify which subreddit a post belongs to, and at the same time able to determine any findings on the interpretation of Investing and Evaluation 

This report will help us do the following things:

I will be comparing two different models: **Logistic Regression and Naive Bayes Model**. Since in this context, **correctly identifying one subreddit is not more important than the other,** I will be using **accuracy score as the main metric to evaluate my models**



---

## Content


- [Data Import and Cleaning]
- [Exploratory Data Analysis]
- [Modeling]
- [Conclusion]
- [Recommendations]
- [Limitations]


## Datasets

For this project, we have collected the following data from Reddit:
- [Investing](investing.csv)
- [Trading](trading.csv)



## Data Dictionary

### Variables
|Column Name|Data Type|Description|
|---|---|---|
|**subreddit**|*object*|Investing or Trading|
|**posts**|*object*|The title and self-text combined|

---

# Conclusion 

- Through our model, we managed to study the predicative words of what the Investing and Trading subreddit is about
- By using the world most active discussion board, we managed to get a 'global' interpretation of what everyone feels Investing and Trading actually is.

From the findings of the Naive Bayes + CVEC model ,global interpretation for Investing suggests that people are looking to do long term investments or funds, holding/buying companies, and most importantly looking at value of the company. 

Whilst for the global interpration for Trading, it suggests people are looking to day trade, discussing about brokers, probably to find the lowest commission platforms, and mostly asking questions , as there is a high word count of Thank. 

### Recommendation(s):

__Redefining Description__
#1 : Moderators can re-define  the description of each subreddit, so that posters have a sense of which subreddit to enter, this would __improve user experience and readers/authors know the differences of the two subreddits.__

__Subreddit Merger__ 
#2 : Although I might not have included the common predictive words for both subreddits, it also suggests another point of view, if there is so much similarity, could the two subreddit be combined as 1 subreddit ? 
Investing subreddit has 1.20 million members, Trading has 0.03 million members

__Auto Subreddit Classifier__
#3 With this model, it is able to identify 77% of the posts accurately, reddit could deploy this model to 'force' authors to select the proper subreddit, i.e. after the author types his/her post, if the models predicts it belongs to Investing, authors have no other options but to post to Investing


### Limitation(s):

#1 : __Common Predictive Words__


Predictive words that are present in predicting it is a Trading or Investing subreddit, could have been further included in the stopwords. This would allow better features being selected, which could lead to a better prediction model. 



#2 : __Sample Size__

The train dataset studied on 868 posts , whilst the test dataset only has 217. The test sample size might be too small, and some of these posts could be mostly __hyperlink sharing, which does not tell much about the post.__

#3 : __Coefficients 20__ 

As the coefficients captured are only the top 20, some posts could not be understood as the posts might be only having the coefficients of rank 40 or rank 50 onwards. 

```python

```
