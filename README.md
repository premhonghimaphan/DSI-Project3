## Project 3: Web APIs & Classification (Reddit)
## Problem Statement
Its been a long time since people can actually travel freely. This serves as a perfect opportunity for travel companies to build new products that provide a niche in the market. Especially after the world opens again, travel industry would probably sky rocket and everyone would offer the nicest deals they can.

One of the niche identified by this travel agency is the opportunity to create product/service for solotraveler and people who would like to go on road trips, focusing on United States. In order to exploit this particular niche, the manager has asked a market research firm to conduct preliminary analysis on solo traveling and road trips.

In order to find out what people talk about in regards to travel, we will look to analyze posts on Reddit. Reddit is a great platform for discussion, especially in the United States. More than just random posts on Reddit, they also have subreddits that people can go to in order to find content or start a discussion that people in the same group like talking about.

Based on my findings of what people talk about on Reddit, the company would then like to build their product/services with features that people often discuss about on Reddit and offer lucrative packages.

## Why Reddit for information about USA?
According to Statista, regional distribution of desktop traffic to Reddit.com as of December 2020, by country, shows that USA has traffic of around 50%.
https://www.statista.com/statistics/325144/reddit-global-active-user-distribution/

## Subreddit - Solotravel
A place for all of those interested in solo travel to share their experience and stories!
https://www.reddit.com/r/solotravel

## Subreddit - Road trip
Whether you enjoy traveling by motorcycle, car, or recreational vehicle this is your destination for everything related to road trips!
https://www.reddit.com/r/roadtrip

## Data Dictionary

|Feature|Type|Description|
|---|---|---|
|subreddit|object|Name of subreddit the posts belong to|
|selftext|object|Content of the post by users|
|title|object|Title of the post by users|
|alltext|object|Combination of selftext and title|
|clean_text|object|Cleaned text of alltext column|
|classifier|int|1=Solotravel, 0=Roadtrip|

## Best Model as per Grid Search (also better performance than using default parameters)
### Naive Bayes Multinomial with TF-IDF Vectorizer
- Train Score: 0.909
- Test Score: 0.9055
      - max_df = 0.9
      - min_df = 3
      - max_features = 2000
      - ngram_range = (1,2)
      - alpha = 2

### Interpreting the best model
- Very low overfit. Therefore, a good model to use
- max_df: ignore terms that appear in more than 90% of the documents.
- min_df: ignore terms that appear in less than 5 documents.
- max_features = only words that occur most frequently in top 2000 is required
- ngram_range: a pair of words help predict unseen data better
- alpha: A little bit of smoothing.

## Constructing Confusion Matrix from predictions made
- True Positive: Predict solotravel, it is solotravel
- False Positive: Predict solotravel, but it is roadtrip
- False Negative: Predict not solotravel (predict roadtrip), but it is solotravel
- True Negative: Predict not solotravel (predict roadtrip), it is roadtrip

### Interpretation of the Confusion Matrix
- Our chosen model shows a high accuracy score of correct predictions.
- Model incorrectly predicts around 9.5% of posts.
- Out of all the positive classes, our model predicted a very good sensitivity score.
- There are about 14 words which are incorrectly predicted to be Roadtrip, but actually it comes from posts in Solotravel.
- There are 29 words which are incorrectly predicted to be Solotravel, but actually it comes from posts in Roadtrip.
- We probably want to find some combination of sensitivity and specificity.

Focusing only on sensitivity means we minimize false negatives. This means there will be few posts we incorrectly predict to be solotravel, but more posts we incorrectly predict to be roadtrip.

Focusing only on specificity means we minimize false positives. This means there will be few posts we incorrectly predict to be roadtrip, but more posts we incorrectly predict to be solotravel.

   As we are only gathering features that relate to the same topic and not have any health implications or other serious implication, we can focus on improving our accuracy score instead.

- Removing some words that overlap in both classification would certainly help improve accuracy.
- An update of new posts might need to be gathered on a daily basis for a certain period of time to ensure lasting results.

## Conclusion and Recommendation
1. For people who like solo traveling, things such as information about ‘Visa’, ‘Flight’, and ‘Hostel’ would prove to be very helpful.
2. For road trips, a lot of words that relate to U.S. appear from this analysis as we can see many state names coming up. For example, Savannah, California and Grand Canyon. The company can look into partnering with hotels or motels from those places, and provide places to stop at for scenery or food as well.
3. Both posts has similar words that come up often such as ‘Plan’ and ‘Time’. The company can look into providing details about those when making travel itinerary.
4. Since this model is biased towards United States, it will not be applicable to audience from elsewhere or who go to other countries. To offer full service, the company can look at their customer base and conduct analysis like this but using discussion platforms that more localized such as Pantip for Thailand.
5. Since there is a high count of active global users of Reddit in the United States, our chance of bias towards providing information is slightly lower. However, taking information from one source is also not enough. Analysing other travel forums that are popular in the United States would also be necessary to provide more information. For example, Trip Advisor and Lonely Planet Forum.
6. This model is likely to only be limited to a certain period of time as traveling and destinations depend highly on weather conditions and time of the year. The same set of information cannot be used for summer months and winter months.
