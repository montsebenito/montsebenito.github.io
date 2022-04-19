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

This project analyses the so called 'Elon Effect': the viability of predicting Bitcoin price fluctuations from the content of daily Elon Musk tweets. You can also deep-dive into this project’ [Github repo](https://github.com/montsebenito/Elon_Effect)

The data used in this case study is publicly available in Twitter (collected via tweepy) and yahoo finance platform (data-reader pandas library). Training data is compressed between January-2019 and January-2022 and test data from January-2022 to February-2022. A daily timeframe has been used in order to isolate the effect of the Tweet on the crypto price. 

Lot has been said ([here](https://www.wsj.com/video/series/wsj-explains/elon-musks-power-over-crypto-explained/D1C22EF9-4279-409E-8AE3-DE3C995E6845), [here](https://www.bloomberg.com/news/videos/2021-07-22/elon-musk-s-influence-on-crypto-video), and [here](https://www.coindesk.com/layer2/culture-week/2021/12/14/the-elon-effect-how-musks-tweets-move-crypto-markets/),also [here](https://www.vox.com/recode/2021/5/18/22441831/elon-musk-bitcoin-dogecoin-crypto-prices-tesla)) about the influence of Elon Musk' tweets over the cryptocurrency investors and ecosystem.

<img src="https://https://github.com/montsebenito/montsebenito.github.io/blob/master/assets/images/oh-hi-elon-tweet.jpg?raw=true"
width="450">

Regarding Bitcoin, the specific crypto this study focus on, it is a strange financial instrument that is both a currency and an investment. You can use bitcoins to buy and sell things online, even though its most popular use is buying and holding (hodl) in the hope of turnng a profit. Its highly volatile price, relative lack of regulation compared to the stock market and newly-lowered barrier to entry makes it an exciting and relatively easy investment for speculation, especially for techie and young people.[1]
 
#### Data Preprocessing & Modelling: 

Performed natural language processing (NLP) considering Twitter-specific syntax (such as hashtags, emoticons, and mentions) based on the text and other attributes as year, month, day as well as number of retweets, comments and likes. Word-level language features are also used. Bag of Words are useful vector space representations of words used in a Twitter context. By leveraging the huge amount of data available via the Twitter API, this approach consists on encoding the subtext context of Tweets into the word embeddings without extensive manual labeling to harnessing for prediction. 
Much of the research regarding the relationship between Twitter NLP and the stock market (comparable to this project' scope) has dealt with sentiment classification, which is other kind of analysis.



#### Results and next steps
This results in a gradient boosting regressor model that predicts a value within a 10% range of the real price. My conclusion is that this study serves as a proof-of-concept identifying a clear link between the attributes and the target. 
In order to significantly improve bitcoin price predictions to convert this project to a viable trading strategy, the following next steps are recommended: 
- increasing bag of words or adding new sources (i.e Google Analytics searches for keywords)
- including tweets sentiment analysis as a new feature







#### Inspiration:
- [1] Mehta, Neel; Agashe, Adi; Detroja, Parth. Buble or Revolution 
- [2] Michael Jermaann [Predicting Stock Movement through Executive Tweets](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/reports/2743946.pdf)

 