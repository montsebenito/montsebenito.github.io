---
layout: splash
permalink: /earncrypto/
title: "New Feature Case Study (I)"

header:
  image: /assets/images/Coinbase_7.jpg
  teaser: #assets/images/unsplash-gallery-image-1-th.jpg

sidebar:
  - title: "Project Overview"
    image: #http://placehold.it/350x250
    image_alt: #"logo"
    text: "This case study is the first of a series, whose goal is reverse-engineering the steps that led the product data team to implement the feature. 
<ul>
  <li>Why did they want to test that feature in the first place?</li> 
  <li>What was the data-driven hypothesis behind?</li>
  <li>Which metric(s) did they choose for the test?</li> <li>How was the test designed?</li> 
</ul>"
    
---



### [EARN CRYPTO WHILE LEARNING ABOUT CRYPTO](https://www.coinbase.com/earn) with coinbase.
<p>This new feature offers the opportunity to discover how specific cryptocurrencies work - via 2-minute courses offered in both their web and app platforms- while getting a bit of each crypto to taste the thrill. </p>

<p>Because of Coinbase’s ambitious vision & mission of disrupting the financial system as we know it, the company's North Star is probably highly focused on growth, with a higher weight on increasing new users. 
</p>
 
<blockquote> “Our mission is to increase economic freedom in the world. We started in 2012 with the radical idea that anyone, anywhere, should be able to easily and securely send and receive Bitcoin.Today, we offer a trusted and easy-to-use platform for accessing the broader cryptoeconomy.” </blockquote>

<h3> WHY DID THEY WANT TO TEST THAT FEATURE IN THE FIRST PLACE? WHAT WAS THE DATA DRIVEN HYPOTHESIS THAT LEAD THE PRODUCT TEAM TO THINK THIS FEATURE WAS A GOOD IDEA TO TEST? WHICH DATA WOULD SUPPORT THE HYPOTHESIS? </h3>

<p>Two groups of new users were compared: those who bought cryptos over X weeks after signing up in Coinbase (label churn 0) vs those who did not (label churn 1).  Using demographics and behavior user data, along with a decision tree classifier model, the data team identified a segment of “super-low power” users who only bought > 30$ and just spent >15 active minutes browsing the app after sign up, but keep trading small amount of cryptos over the X weeks without “churning”. In addition, these customers were also more prone to send out more app-referral invitations than the ones that eventually churned. </p>

<p>So the hypothesis to test is: if Coinbase offers the chance to taste the thrill of trading/buying cryptos by earning up around 30$-valued coins just by taking a few 2-minute courses offered in both their web and app platforms, users will love the experience, the product and will purchase more coins. 
Expected results (before the test) are:</p>
<ol start=1>
<li> **Overall activation rate will go up**. Defined as ratio between users who buy cryptocurrencies) divided for all users that signed up (i.e. downloaded the app & provided identification proof) even though they didn’t buy yet. 
We’re not taking into account if users have provided bank account info or not (as users who ‘earn’ the coins will eventually provide this if they want to cash the free coins) nor other activation actions such as selling coins for the same reason.
  We’ll use activation rate as our **main metric**</li>

<li> This is a change that **removes friction** and potentially will break some users’ barriers to buy coins/use Coinbase. These mini-courses force users to spend some time using the App: **increasing familiarity** with it, learning a bit on some blockchain uses. It is widely known that people tend to invest in assets they understand vs unknown.</li> 

<li> **#referrals/new user will increase**. Coinbase makes this easy by having a parallel referral program of 10$ for referee and referral, and this extra $30 will support the referral further.</li>

<li> It is unlikely that power users bother to take advantage of this promotion for such a small amount, especially if we compare it with their potential gains (or losses) in a few minutes. It is also unlikely existing customers are interested in it.</li>

<li> Even though it's extremely difficult to forecast cryptocurrencies' value due to their highly volatile behavior, it’s supposed that the long term value of a crypto is related to the amount of people who trust it.  If Coinbase itself somehow promotes these specific coins it is likely their value will go up as well as this specific segment user satisfaction. **Increasing engagement defined as total $ invested in coins/user.**</li>

<li>Said all the above, one major concern: May this feature **cannibalize** avg amount spent for these “super low power” traders? Why pay with your own money if you have some coins to play with? We have to keep in mind that Coinbase business model is centered around the fees it charges for trading cryptocurrencies.</li>


  <h3> WHICH METRIC(S) DID THEY CHOOSE FOR THE TEST?</h3>

##### Driver Metrics:

1. **Overall activation rate** will go up. Defined as ratio between users who buy cryptocurrencies) divided for all users that signed up (i.e. downloaded the app & provided identification proof) even though they didn’t buy yet. We’re not taking into account if users have provided bank account info or not (as users who ‘earn’ the coins will eventually provide this if they want to cash the free coins) nor other activation actions such as selling coins for the same reason.

2. **#referrals/new_user** will increase.

##### Guardrail metric:

3. Coinbase probably expects these promoting expenses (a.k.a the new feature) to be covered for this low power user segment. We’ll use a **short term proxy for LTV** as a guardrail metric. LTV, measured as total amount of $ in fees paid by buying/selling during the first year + estimated $fees if selling coins in their wallet at the end of the period) - CAC (let’s keep it simple at 30$). Data team built a model to predict LTV and was able to assign a predicted $ value to different identified segments, so we can have an estimate of LTV per segment. We aim to keep this metric flat.

So, we will fail to reject the null hypothesis if our sample won’t provide enough evidence that activation rate and #requests/users are the same for control and test groups and we accept the alternative hypothesis that is certainly a significant effect in these metrics between the control and the treatment group.


  <h3>HOW WAS THE TEST DESIGNED?</h3>

##### Target Population: 

This new feature targets all (inactive) users, so it will be test across all users. If this was a promotion requiring taking action within X time after sign-up, 
very common in the brokerage industry, then the experiment will be targeting new users only (with less noisy data)

##### Practical Significance for each metric (minimum difference btw test and control): 
Let’s say PM estimates this new feature will make sense if activation rate is up 1% and we expect #referrals/new users 5% up.

##### Sample Size:  

Calculated with power=80%, adjusted significance level=5%/3 (with **Bonferroni correction**) and minimum difference between test and control as specified above.

##### Independence: 

- When expected lift in referrals is relatively 'low': Users will be randomly split between test and control, as I assume there is independence between one user taking the course/earning 30$ and another's action. In the extreme case all Coinbase’ 43 million users earning 30$ we may expect the so called Coinbase effect, but I think the increase of value won’t have an impact of how many people takes the courses as the value in $ will be the same, 30$ (less coin portion)

- If 'high' lift in referrals is expected: Users will be **test by market**. Users in certain location will see the new feature and others don't. Being the control group an equivalent market () to the 'treatment' one. 


##### How long will the test run?:  

2 weeks to capturing **weekly patterns** or more to reach required sample size for test and control

#### TEST RESULTS INTERPRETATION:

##### Sanity Check:

- **Randomization**. Are test and control user distribution comparable?

- Even though this is only one time used (i.e.we cannot compare new vs existing users behaviour) we can check **novelty effects** as the percentage of courses taken/coins earned. The lesser volume, the higher the novelty effects.

##### Results:

This feature/ad was implemented so we can safely assume the main metric won significantly, and they didn’t notice any effect on the guardrail metric.

#### POST LAUNCH MONITORING:

Predict via a time series where the metric would have been without the change and then compare the prediction to the actual number, the assumption being that whatever delta you see is given by the change.
