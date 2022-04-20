---
layout: splash
permalink: /elonmusk/
#excerpt: What's the real influence of Elon Musk' tweets over the crypto ecosystem?
classes: wide

header:
  image: /assets/images/elonrollercoaster.jpg
  caption:  "Source: [Prof Scott Galloway](https://www.profgalloway.com/elon/)"
    
---


### What's the real influence of Elon Musk' tweets over the crypto ecosystem? 

This project expands the so called **'Elon Effect'** and analyses the viability of predicting Bitcoin price fluctuations from the content of daily Elon Musk tweets. You can dive deeper into this project by checking this [repo.](https://github.com/montsebenito/Elon_Effect)

Lot has been said ([here](https://www.wsj.com/video/series/wsj-explains/elon-musks-power-over-crypto-explained/D1C22EF9-4279-409E-8AE3-DE3C995E6845), [here](https://www.bloomberg.com/news/videos/2021-07-22/elon-musk-s-influence-on-crypto-video), and [here](https://www.coindesk.com/layer2/culture-week/2021/12/14/the-elon-effect-how-musks-tweets-move-crypto-markets/),also [here](https://www.vox.com/recode/2021/5/18/22441831/elon-musk-bitcoin-dogecoin-crypto-prices-tesla)) about the influence of Elon Musk' tweets over the cryptocurrency investors and ecosystem.

<img src="https://raw.githubusercontent.com/montsebenito/montsebenito.github.io/master/assets/images/oh-hi-elon-tweet.jpg"
width="450" title="https://www.profgalloway.com/elon/">

Regarding Bitcoin, the specific cryptocurrency this study focus on, it is a strange financial instrument that is both a currency and an investment. You can use bitcoins to buy and sell things online, even though its highly volatile price, relative lack of regulation compared to the stock market and newly-lowered barrier to entry makes it an exciting and relatively easy investment for speculation (buying and hodling).[1]

#### Data Collection:

The data used in this case study is publicly available in Twitter (collected via tweepy) and yahoo finance platforms (data-reader pandas library). Training data is compressed between January-2019 and January-2022 (7278 tweets and replies) and test data from January-2022 to February-2022 (238 tweets). A daily timeframe has been used in order to better isolate the effect of the Tweet on the crypto price. 

<img src="https://raw.githubusercontent.com/montsebenito/Elon_Effect/main/pics/BitcoinS&P500Price.jpg"
width="1200">

Comparing the value of Bitcoin and S&P500 from January2019 to February2022. Bitcoin is far more volatile than S&P500, but it's growth is far faster.

<img src="https://raw.githubusercontent.com/montsebenito/Elon_Effect/main/pics/DailyTweets.jpg"
width="1200">

Elon not only leads two revolutionary companies, but he also is a prolific daily Twitter user.
 
#### Data Preprocessing & Modelling: 

**Natural language processing (NLP)** considering Twitter-specific syntax (such as hashtags, emoticons, and mentions) has been performed. 
- **Input**: "Jenna went back to University"
- **Normalize**: "jenna went back to university"
- **Tokenize**: <"jenna","went","back","to","university">
- **Remove Stop Words**: <"jenna","went","university>
- **Stem/Lemmatize**: <"jenna","go","univers">

Word-level language features are used. Bag of Words are useful vector space representations of words used in a Twitter context. By leveraging the huge amount of data available via the Twitter API (Elon most used word in training data, tweet datetime, number of retweets, comments and likes), this approach consists on encoding the subtext context of Tweets into the word embeddings without extensive manual labeling to harnessing for prediction. This is the main difference with much of the current available research studying the relationship between Twitter NLP and the stock market, which finds evidence of this relationship via sentiment classification [2].

<img src="https://raw.githubusercontent.com/montsebenito/Elon_Effect/main/pics/MostTweetedWords.jpg"
width="1200">

Three different regression models (Random Forest, Ada Boost and Gradient Boosting) have been evaluated to determine which algorithm will provide the lowest mean absolute error and the most convenient predictions trends. Mean absolute error (MAE) is the best metric for to evaluate the model because it is very useful when the target follows a skewed distribution: outliers will not influence models attempting to optimize on this metric as much as if when the mean squared error. Gradient Boosting Regressor showed the second lowest MAE and its predictions follow a pattern very similar to real data, with the advantage of being offset. This model has been optimized using GridCV, achieving the following results:
- Metric: MAE	
- Unoptimized Model: 5693	
- Optimized Model:5469

<img src="https://raw.githubusercontent.com/montsebenito/Elon_Effect/main/pics/GBpredictions.jpg"
width="1200">

Interestingly, the model predictions trends and behaviour fit with real data with a preceeding offset that will allow a trader made buy/sell decisions in advance. 

#### Insights and next steps
The above resulst in a **gradient boosting regressor model that predicts Bitcoin price within a 12% mean absolute error range. My conclusion is that this study serves as a proof-of-concept identifying a clear link between the attributes and the target.**

In order to significantly improve bitcoin price predictions to convert this project to a viable trading strategy, the following next steps are recommended: 
- increasing bag of words or adding new sources (i.e Google Analytics searches for keywords).
- including tweets sentiment analysis as a new feature.
- time series decomposition and multi-output regression


### Inspiration:
- [1] Mehta, Neel; Agashe, Adi; Detroja, Parth. Buble or Revolution 
- [2] Michael Jermaann [Predicting Stock Movement through Executive Tweets](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/reports/2743946.pdf)

 
