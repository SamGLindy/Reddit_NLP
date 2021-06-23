# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

## Problem Statement

As an operative for Dogecoin, I'm trying to build a model that can tell the difference between Bitcoin and Ethereum investors.
To do so, I'll be scraping data from the Bitcoin and Ethereum subreddits on Reddit.  With this model, I'll be able to identify
users from each crypto community so Dogecoin can send them targeted ads that will inflame tensions between the two groups.
Our hope is that in the midst of all this chaos, users will flock to Dogecoin and help it's value increase.  However, our budget
to serve these ads is modest, so it's important that the ads only go to the correct users.  To optimize our budget, the models we
test will ultimately be evaluated on their precision scores, with consideration for their AUC ROC scores as well.  These scores
will highlight if the right users are being targeted or not, which is our end goal.  As we all know, when you're trying to create
chaos, it's important to maximize your results when you only have limited resources at your disposal.

### Data Used

bitcoin_url = "https://api.pushshift.io/reddit/search/submission?subreddit=Bitcoin"

ethereum_url = "https://api.pushshift.io/reddit/search/submission?subreddit=ethereum"

---

## Data Dictionary

| column                    | data type | description                                                  |
|---------------------------|-----------|--------------------------------------------------------------|
| title                     | object    | Title of subreddit post                                      |
| selftext                  | object    | Content of subreddit post                                    |
| subreddit                 | object    | The subreddit the post was scraped from                      |
| created_utc               | float64   | The time and date the post was created                       |
| author                    | object    | The username of the post's author                            |
| title_and_selftext        | object    | A concatenated column of title and selftext                  |
| is_bitcoin                | float64   | Numeric value assigned to show if a post was from BTC or ETH |
| selftext_tokens           | object    | Tokenized selftext                                           |
| title_and_selftext_tokens | object    | Tokenized title and selftext                                 |
| selftext_lem              | object    | Lemmatized selftext                                          |
| title_and_selftext_lem    | object    | Lemmatized title and selftext                                |
| title_word_count          | float64   | Title word count                                             |
| title_length              | float64   | Title character length                                       |
| selftext_word_count       | float64   | Post word count                                              |
| selftext_length           | float64   | Post post character length                                   |
| preds                     | float64   | Model predictions                                            |

---

## Summary

Phase 1, Web Scraping: In order to acquire the data for this project, we'll build a web scraping function that will pull at least 10k posts between the Bitcoin
and Ethereum subreddits.

Phase 2, Preprocessing and EDA: The data will then be cleaned and manipulated through tokenization and lemmatizing to reduce noise. Then, the distribution
of the data will be analyzed for any relevant patterns. Next, the most common words, bigrams, and trigrams will be extracted to see if any notable differences
between the two threads can be unearthed.

Phase 3, Modeling: Three models will be deployed, Count Vectorization/Naive Bayes, tf-idf/Naive Bayes, and Count Vectorization/Random Forest to determine
which can produce the best precision score.  Then the three models's ROC curves will be compared for an additional level of analysis.

---

## Conclusions and Takeaways

EDA: The most common words, bigrams, and trigrams in both of these subreddits' posts show that a large number of users are looking for advice
as they navigate their cryptocurrency investing journey.  Stripping a few of the obvious words out of the analysis shows more specific discussions
around the unique mechanisms of the currency, especially in the ETH thread. Adding a more robust custom stop word list, as well as sentiment analysis,
are definitely two analysis tools I wish I had employed. Otherwise, nothing too surprising came out of my EDA.

Modeling: After running CV and Naive Bayes, tf-idf and Naive Bayes, and CV and Random Forest models, it's still a bit unclear which model I would
ultimately recommend.  Using the precision scores from the confusion matrices, the RF model would be the choice. When comparing the models with ROC
curves however, the CV/NB model would be the choice.  If I had more time with this project, I would circle back to my EDA and add the additional steps
and features I've mentioned and run the models again to see if a clear standout emerged.  Additionally, I would try to do a deeper investigation into
the incorrectly classified posts to see if any patterns emerged that could improve the model further
