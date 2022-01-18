---
layout: splash
permalink: /improvemarketplace/
#excerpt: If you had to improve the Olist marketplace, what would you do? (HINT: Data)"
classes: wide

header:
  image: /assets/images/market1.jpg
  teaser: #assets/images/unsplash-gallery-image-1-th.jpg

sidebar:
  - title: "Project Overview"
    image: #http://placehold.it/350x250
    image_alt: #"logo"
    text: "Segmented sellers based on sale/no_sale as well as on avg LTV (rmse ~BRL289) to find what characteristics makes a top seller, following CRISP-DM process model."
  - title: "Data Understanding:" 
    text: "Explored and Wranged data from 9 datasets with +100k observations (one of the datasets have +1M observations!) and max 15 variables. Wordclouds of good/bad/neutral scored reviews"
    
---




# How to improve a Marketplace?

#### _If you had to improve the Olist marketplace, what would you do? (HINT: Data)_
 
[Olist](https://olist.com/pt-br/), a Brazilian e-commerce marketplace integrator, has raised more than [$126 million](https://techcrunch.com/2021/04/15/goldman-sachs-leads-23m-in-funding-for-brazilian-e-commerce-startup-olist/) since its 2015 inception. Founded with the mission of “empowering trade”, it connects +100k merchants (as of December, 2021) from all over Brazil to different marketplaces with a single contract and a drop-shipping model to send products directly from stores to clients using logistics partners.

The anonymised datasets used in this case study were generously provided by Olist. Consist of a sample of their real data, with information on +100k orders from 2016 to 2018 as well as +8k Marketing Qualified Leads (MQLs) from potential sellers that requested contact between Jun 2017 and Jun 2018. You can find (and play with!) these datasets [here](https://www.kaggle.com/olistbr/brazilian-ecommerce) and [here](https://www.kaggle.com/olistbr/marketing-funnel-olist/home).

<img src="https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_pics/Jory0O3.png?raw=true"
width="450"><img src="https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_pics/HRhd2Y0.png?raw=true"
width="450">

--- Olist public data schema. Source: [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce) & [Kaggle](https://www.kaggle.com/olistbr/marketing-funnel-olist/home)

### Marketplaces performance metrics

What does to 'improve' mean, anyway? 

**Growth** is usually the main goal for any team of most successful companies (once product/market fit is achieved). There are two main components to drive growth 1) the ability to acquire new customers (it is pretty much impossible to grow if the user base is not increasing), and 2) the ability to retain current users (it is really hard to grow while losing past users and, certainly, not sustainable in the long run). 

Unlike 'typical' 2-sided marketplaces, Olist facilitates the interaction between sellers and buyers by providing the sellers an intermediary unique platform to +10 marketplaces (including Amazon, Mercado Livre,...etc). Based on this business model, Olist’ real customers are the merchants and its (indirect) supply, the [+3 million](https://olist.com/pt-br/solucoes-para-comercio/vender-em-marketplaces/) end purchasers. 

So, a good metric regarding ‘acquiring new users’ could be: new sellers per month who sell at least 1 product within the first X days (with X being defined by determining a discriminant period on seller LTV). Regarding engagement (retaining current merchants) seller LTV and good reviews (to incentivize network effects) are the key actions Olist want to perform. Average Customer Lifetime Value captures the projected value of a customer for a fixed time horizon, usually enables marketplaces to efficiently allocate budget across different marketing channels and creates better segments. **DISCLAIMER:** Unfortunately, the provided data doesn't allow to calculate as we're missing important info to determine Customer Adquisition Cost. To resolve this, I will calculate average monthly GMV per seller (Gross Merchandise Value) as a target sustitute in the model BUT I'll use both terms indistinctly along this project.

### Would improving Olist supply or demand significantly increase the transactions volume (& avg GMV)? 

It is often really hard to understand whether a marketplace should focus on improving supply or demand, as they’re so strictly related. A priori, Olist is not supply constrained as they provide sellers access to millions of online purchasers. Said that, supply health does depend on the business casuistry per se, for example company stage (pre-post PMF) Let's perform a descriptive and explanatory analysis to answer the following business questions, that may show the health of some proxies for supply and demand:

**- How is the seller acquisition journey? How long is it?**

**- What is the average time it takes to a new merchant (a.k.a seller) to sell for the first time after being acquired?**

**- How are the overall sales? Are there any product category doing particularly well … or particularly badly?** 

**- What are the characteristics of the top sellers?**

and finally

**- What channels are bringing in more top selling sellers?**


### Project Approach

I will analyze the sellers acquisition journey and will segment them based on average monthly LTV to understand what characteristics make a top seller, following the [CRISP-DM](https://www.datascience-pm.com/crisp-dm-2/) apprach.
- **Business Understanding**
- **Data Understanding**: Descriptive statistics and Visualizations.
- **Data Preparation**: Feature Engineering relevant features that may be correlated with the chosen outcome variable. Handling missing values and outliers, encoded categorical variables
- **Data Modeling**: Optimized Random Forest Regressor and Classifier using GridCV.
- **Results Evaluation**: Extracted actionable insights & Next Steps recommendations


<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/MainTimelines.png?raw=true'
height="350">

--- Timelines extracted from the provided raw data
(Just felt like we needed a colorful Gantt chart right here)

### How is the seller acquisition journey?

The journey starts when a potential seller sign-up at a landing page. Organic search lead sign-up volume, followed by paid search, social and an unknown origin from Jul, 2017 to May, 2018.

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/monthlyVolumebychannel.png?raw=true'
height="350">


After sign-up, they get contacted by one of the Olist 32 Sales development Representative (SDR) to confirm some information and schedule a consultancy with a Sales Representative (SR) (of a total of 22). The SR may close the deal (lead becomes a seller) or lose the deal.

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/monthlyCRbychannel.png?raw=true'
height="250">


Unknown origin maintains a consistent high conversion rate from Jan, 2018.

**How long is the seller acquisition journey?** Median length of one month for all origins (except other publicities)

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/SellerAcquisitionlength.png?raw=true'
height="350">

### What is the average time it takes to a new merchant (a.k.a seller) to sell for the first time after being acquired?

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/DayswithOlist.png?raw=true'
height="350">

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/DaystoSale.png?raw=true'
height="350">


### How are the overall sales doing? Are there any product category/business segment doing particularly well … or particularly badly?

Regarding overall sales Nov,2017 - Aug, 2018, monthly number of transactions as well as monthly volume sold in BRL show a steady increase overtime. During this period, both measures converge.

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/monthlysales.png?raw=true'
height="250">


Here we can see same line plot for the Top 5 product categories of overall sales (in units and BRL).
<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/Top5cat_vol&rev.png?raw=true'
height="250">

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/itemspertransaction.png?raw=true'
height="250">

Overall sales: Basket size

The following tables show some aggregates for top and bottom 5 product categories and business segment (acquired between Dec,2017-Aug,2018): 

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/top5_prodcat_table.png.jpg?raw=true'
height="150">

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/bot5_prodcat_table.png?raw=true'
height="150">

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/top5_busseg_table.png?raw=true'
height="150">

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/bot5_busseg_table.png?raw=true'
height="150">


### What are the characteristics of the top sellers?

The choosen model, a Random Forest Regressor with Root Mean Square error of 289 BRL, used the following variables (per importance):

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/Top10featuresBRL.png?raw=true'
height="350">

A deep-dive within partial dependant plots (looking at the impact of each of the variables individually) confirmed these results. 

### What channels are bringing in more top selling sellers?

<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/bigonlinevstotal_origin.png?raw=true'
height="350">
<img src='https://github.com/montsebenito/How_to_Improve_a_Marketplace/blob/main/Olist_saved/sellingvstotal_origin.png?raw=true'
height="350">

### Insights summary and next steps

**Summary**

- 'Big Online' lead type are the **top sellers** in terms of revenue. We need the marketing team to get more of those sellers to Olist. Marketing team should also target and attract top performing business segments like 'Health&Beauty" and 'Watches' (among others) to Olist. It is difficult to determine what are best channels to do so (considering the pretty equilibrated barplot above) as it will mainly depend on cost of acquisition in each of the origins. From a product standpoint, I would recommend to personalize two different versions of Olist platform for each group: Big_online sellers and the rest of them.

- Looks like days with Olist is also a high correlated variable with the average monthly amount sold (in BRL). The longer a seller is selling with Olist, the larger is their monthly revenue, overall when they are Olist users >200 days. One assumption on why that's happenning may be products become more popular over time because their exposure in all main Brazillian marketplaces, and this is a really good indicator that Olist is very useful promoting seller's products. The product group should here focus on how to reduce this period and **make the sellers profitable sooner**.

**Next Steps**: 

- Analyze data related to purchasers' searches and use of filters (if available) to determine if there is any issue with the quality, quantity or price offered by the sellers, plus further recommendations.

- Increase Basket size. Olist recommends the sellers to bundle their products if possible, as sellers pay a fee for each one pf the products. To help them do this as efficient as possible (so helping the sellers increasing their profit per transaction) I'll propose to build a **recommender system** to help them understand what products are more probable to be sold together.

___________________________________________________________________________________________________
**And you? How do you improve a marketplace?** Stay tuned for updates & next steps! You can dive deeper in this project checking this [repo](https://github.com/montsebenito/How_to_Improve_a_Marketplace) 
