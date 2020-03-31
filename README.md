# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: NLP Binary Classification

### Problem Statement

I am moderator for r/Biology and r/ Microbiology, someone hacked my subreddits and combined them into one. I need to build a model ASAP that will help me differeniate between the subreddit posts. Once complete, I can begin to organize the mess that the hacker created! Luckily, I have some back up data from both subreddits that I can use to train my models with. Since this is a NLP binary classification problem, I will try out Logistic and Naive Bayes models with accuracy as my metric.

---


## Executive Summary

I started out with two separate data frames one for each subreddit. I concatenated them then preceded to binarize the subreddit column according to their respective subreddit. r/Biology was mapped as 1 and r/ Microbiology was mapped as 0.Data cleaning was minimal because Count Vectorizer essentially does it for you. Exploratory data analysis was kicked off by utilizing Count Vectorizer on the combined DataFrame. I sorted out the top ten words and utilized this to base my stop word customization off of. Then did some masking to put the binary subreddits into their own data frames. I then sorted out the top words using Count Vectorizer as well and further customized my stop words. I gathered that since microbiology is a sub field of biology they would share a lot over cross over terminology. This proved accurate, they shared common terms but many of which were due the fact Reddit is a forum based community. They get a lot of people asking for help and/ or advice in these fields, which would explain the rest of the cross over words. They ended up sharing 70% of the same top ten words which was surprising to me. Another key finding was that cell and cells were under biology's top ten instead of micro. Which I intuitively thought would go to microbiology.
 
 
Next up was selecting my X and Y variables. I chose the "selftext" column as my X because it allows for more data to be utilized, there are more words in self text than title. I picked my "binary_class" columns as my Y because it is binarized according to subreddit. I chose four models Tfidif Vectorizer & Logistic Regression, CountVectorizer & Logistic Regression, Multinomial Naive Bayes & CountVectorizer and finally the Gaussian Naive Bayes & Tfidf Vectorizer Model. I did a grid search over several iterations of parameters and ultimately input the parameters from "best_params" into my models. I compared my scores to the baseline model of .514 that would always default to predicting biology, they all performed at least .25 better than it. None of my models were over or under fit. The Highest performing model was Tfidf Vectorizer & Logistic Regression so I chose this one. After model selection I evaluated my model by graphing a confusion matrix and manually calculated the accuracy score of .80. My last evaluation was to graph  and interpret the ROC Curve. My AUROC was better than the baseline and the ROC curve was closer to one than the baseline, so it safe to say this is a decent model. I then tested out my model a couple times and it predicted accurately!!!


## Datasets

- [subreddit_microbiology](./data/subreddit_microbiology.csv)
- [subreddit_biology](./data/subreddit_biology.csv)

### Data Dictionary

|Feature|Type|Description|
|---|---|---|
|**title**|*object*|post title|
|**selftext**|*object*|post text|
|**subreddit**|*object*|subreddit thread|
|**created_utc**|*int*|time|
|**author**|*object*|author|
|**num_comments**|*int*|number of comments|
|**score**|*int*|score|
|**is_self**|*bool*|is this the original post or a repost|
|**timestamp**|*object*|time|
|**binary_class**|*int*|binarized subreddits bio = 1 & micro = 0|

## Conclusions

The selected TfidfVectorizer & Logistic Regression model has an accuracy rate of .80. This is good enough to help solve my problem of subreddit differeniation. I do not need a super accurate model and since I am in a time crunch this should suffice. I just need something good enough to get the job done. I can optimize my model more in my spare time.


## Recommendations

Now that I have a model ready to be put into action, the next step would be to build a function that would  automate the following. Scrape the posts from the combined subreddits, pass them into my predictive model, then separate them into two data frames based on their respective classes. I would give then the data to reddit so that they could put the posts back where they belong

My model can be improved by the implementing the following. I would not have dropped several the columns before filtering for removed or deleted rows. I ended up deleting posts that could have upped my score because they may have had applicable data in them. I could have also tried to pull out some of the common stop words to see how that would have affected my model.I would also use regex, stemming and lemmatizing to see which one worked better also do some feature engineering. Lastly I could try out more models to see if I could get a better score.

## References 

[r/ Biology post utilized in my predictive model](https://www.reddit.com/r/science/comments/ev41ym/study_suggests_parkinsons_present_from_birth_and/)


[r/ Microbiology post utilized in my predictive model](https://www.reddit.com/r/microbiology/comments/ew8n4g/i_would_like_to_know_what_the_swimming_organisms/)