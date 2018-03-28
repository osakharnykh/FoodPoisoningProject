

```python
import pandas as pd
import praw
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import time

# Import and Initialize Sentiment Analyzer
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer
analyzer = SentimentIntensityAnalyzer()

reddit = praw.Reddit(client_id='',
                     client_secret='',
                     user_agent='')

```


```python
subreddit = reddit.subreddit("all")
print(subreddit.display_name)
print(reddit.read_only)
```

    all
    True



```python
subreddits = []
subreddit_ids = []
submission_ids = []
created_dates = []
titles = []
scores = []
comments_numbers = []
urls = []
domains = []
keywords2 = []

keywords = ["Domino’s Pizza", "Burger King ", "Costco", "Popeyes",
           "Panda Express"]

for keyword in keywords:

    for i in subreddit.search(keyword, limit=None):
        #print(i.title)
        keywords2.append(keyword)
        subreddits.append(subreddit.display_name)
        subreddit_ids.append(i.subreddit_id)
        submission_ids.append(i.id)
        created_dates.append(i.created)
        titles.append(i.title)
        scores.append(i.score)
        comments_numbers.append(i.num_comments)
        urls.append(i.url)
        domains.append(i.domain)

```


```python
#title
```


```python
reddit_df = pd.DataFrame({"Keyword":keywords2, "Subreddit":subreddits, "Submission ID":subreddit_ids, "Submission ID":submission_ids,
                          "Created Date":created_dates, "Submission Title":titles, "Submission Score":scores, "Submission URL":urls, "Total Submission Comments":comments_numbers,
                         "Domain":domains})

reddit_df = reddit_df[["Keyword", "Submission ID", "Subreddit", "Created Date", "Submission Title", "Submission Score", "Submission URL", "Total Submission Comments", "Submission URL", "Domain"]]

reddit_df.sort_values('Total Submission Comments', ascending=False)

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>507</th>
      <td>Costco</td>
      <td>7pt4yj</td>
      <td>all</td>
      <td>1.515750e+09</td>
      <td>When Your Girls Insist The Costco Clerk Is Mau...</td>
      <td>124760</td>
      <td>https://i.imgur.com/VB4KRlR.gifv</td>
      <td>4818</td>
      <td>https://i.imgur.com/VB4KRlR.gifv</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Burger King</td>
      <td>5uhzr4</td>
      <td>all</td>
      <td>1.487309e+09</td>
      <td>Cook fired for "stealing" 50c worth of french ...</td>
      <td>48276</td>
      <td>http://www.bbc.com/news/world-us-canada-38996427</td>
      <td>4487</td>
      <td>http://www.bbc.com/news/world-us-canada-38996427</td>
      <td>bbc.com</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Burger King</td>
      <td>4jkvf5</td>
      <td>all</td>
      <td>1.463430e+09</td>
      <td>So I decided to try one of Burger King's new h...</td>
      <td>46767</td>
      <td>http://i.imgur.com/BLQSOta.jpg?1</td>
      <td>4363</td>
      <td>http://i.imgur.com/BLQSOta.jpg?1</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>510</th>
      <td>Costco</td>
      <td>83f9e2</td>
      <td>all</td>
      <td>1.520719e+09</td>
      <td>Costco says extra profit from tax cuts will be...</td>
      <td>63651</td>
      <td>https://www.seattletimes.com/business/retail/c...</td>
      <td>4224</td>
      <td>https://www.seattletimes.com/business/retail/c...</td>
      <td>seattletimes.com</td>
    </tr>
    <tr>
      <th>522</th>
      <td>Costco</td>
      <td>2kp34z</td>
      <td>all</td>
      <td>1.414634e+09</td>
      <td>Costco will again stay closed on Thanksgiving ...</td>
      <td>57262</td>
      <td>http://money.cnn.com/2014/10/28/news/companies...</td>
      <td>4168</td>
      <td>http://money.cnn.com/2014/10/28/news/companies...</td>
      <td>money.cnn.com</td>
    </tr>
    <tr>
      <th>504</th>
      <td>Costco</td>
      <td>1z9zs7</td>
      <td>all</td>
      <td>1.393724e+09</td>
      <td>TIL a full-time cashier at Costco makes about ...</td>
      <td>4155</td>
      <td>http://beta.fool.com/hukgon/2012/01/06/intervi...</td>
      <td>4162</td>
      <td>http://beta.fool.com/hukgon/2012/01/06/intervi...</td>
      <td>beta.fool.com</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Burger King</td>
      <td>41vy0n</td>
      <td>all</td>
      <td>1.453347e+09</td>
      <td>TIL: 60% of the Fat and 31% of the calories in...</td>
      <td>22327</td>
      <td>http://www.bk.com/menu-item/original-chicken-s...</td>
      <td>3644</td>
      <td>http://www.bk.com/menu-item/original-chicken-s...</td>
      <td>bk.com</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Burger King</td>
      <td>7snpc5</td>
      <td>all</td>
      <td>1.516836e+09</td>
      <td>Burger King Deviously Explains Net Neutrality ...</td>
      <td>66293</td>
      <td>http://www.adweek.com/creativity/burger-king-d...</td>
      <td>3644</td>
      <td>http://www.adweek.com/creativity/burger-king-d...</td>
      <td>adweek.com</td>
    </tr>
    <tr>
      <th>532</th>
      <td>Costco</td>
      <td>4gts5c</td>
      <td>all</td>
      <td>1.461876e+09</td>
      <td>Successfully smuggled a Costco cheesecake into...</td>
      <td>22400</td>
      <td>http://i.imgur.com/wrhHGQ5.jpg</td>
      <td>3377</td>
      <td>http://i.imgur.com/wrhHGQ5.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>518</th>
      <td>Costco</td>
      <td>6yrmwr</td>
      <td>all</td>
      <td>1.504863e+09</td>
      <td>TIL Costco purposefully designed their store w...</td>
      <td>55811</td>
      <td>http://www.npr.org/sections/money/2015/09/25/4...</td>
      <td>3342</td>
      <td>http://www.npr.org/sections/money/2015/09/25/4...</td>
      <td>npr.org</td>
    </tr>
    <tr>
      <th>524</th>
      <td>Costco</td>
      <td>7f0z0s</td>
      <td>all</td>
      <td>1.511486e+09</td>
      <td>'We're not lazy, we're old': 71-year-old worke...</td>
      <td>54028</td>
      <td>http://www.cbc.ca/beta/news/canada/montreal/co...</td>
      <td>3328</td>
      <td>http://www.cbc.ca/beta/news/canada/montreal/co...</td>
      <td>cbc.ca</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Burger King</td>
      <td>552o7l</td>
      <td>all</td>
      <td>1.475191e+09</td>
      <td>Two month long undercover drug operation, in w...</td>
      <td>24629</td>
      <td>http://www.fredericknewspost.com/news/crime_an...</td>
      <td>3284</td>
      <td>http://www.fredericknewspost.com/news/crime_an...</td>
      <td>fredericknewspost.com</td>
    </tr>
    <tr>
      <th>556</th>
      <td>Costco</td>
      <td>1a5fk6</td>
      <td>all</td>
      <td>1.363130e+09</td>
      <td>Costco Proves Republicans Wrong By Paying a Li...</td>
      <td>2297</td>
      <td>http://www.politicususa.com/costco-proves-repu...</td>
      <td>3131</td>
      <td>http://www.politicususa.com/costco-proves-repu...</td>
      <td>politicususa.com</td>
    </tr>
    <tr>
      <th>516</th>
      <td>Costco</td>
      <td>13viu7</td>
      <td>all</td>
      <td>1.354057e+09</td>
      <td>Good Guy CEO of Costco</td>
      <td>4180</td>
      <td>http://imgur.com/bNqSH</td>
      <td>2940</td>
      <td>http://imgur.com/bNqSH</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Burger King</td>
      <td>3igg9n</td>
      <td>all</td>
      <td>1.440619e+09</td>
      <td>Burger King wants to make a McWhopper with McD...</td>
      <td>10449</td>
      <td>https://www.youtube.com/watch?v=e01a4-ClcTs</td>
      <td>2811</td>
      <td>https://www.youtube.com/watch?v=e01a4-ClcTs</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>511</th>
      <td>Costco</td>
      <td>850g3t</td>
      <td>all</td>
      <td>1.521278e+09</td>
      <td>Police lay in wait at backdoor, arrest 3 Costc...</td>
      <td>32894</td>
      <td>https://www.youtube.com/watch?v=LWF4VtZVz24</td>
      <td>2549</td>
      <td>https://www.youtube.com/watch?v=LWF4VtZVz24</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>548</th>
      <td>Costco</td>
      <td>37jnp6</td>
      <td>all</td>
      <td>1.432810e+09</td>
      <td>TIL Costco hasn't changed the price of its $1....</td>
      <td>19115</td>
      <td>http://en.wikipedia.org/w/index.php?title=Cost...</td>
      <td>2507</td>
      <td>http://en.wikipedia.org/w/index.php?title=Cost...</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Burger King</td>
      <td>1jvul0</td>
      <td>all</td>
      <td>1.375914e+09</td>
      <td>I Work for Burger King at $7.40 an Hour: Here'...</td>
      <td>2203</td>
      <td>http://www.alternet.org/labor/i-work-burger-ki...</td>
      <td>2459</td>
      <td>http://www.alternet.org/labor/i-work-burger-ki...</td>
      <td>alternet.org</td>
    </tr>
    <tr>
      <th>550</th>
      <td>Costco</td>
      <td>v2tf5</td>
      <td>all</td>
      <td>1.339758e+09</td>
      <td>TIL Costco hasn't changed the price of a hot d...</td>
      <td>3162</td>
      <td>http://shop.costco.com/en/Membership/Welcome/A...</td>
      <td>2388</td>
      <td>http://shop.costco.com/en/Membership/Welcome/A...</td>
      <td>shop.costco.com</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
    </tr>
    <tr>
      <th>178</th>
      <td>Burger King</td>
      <td>1ldmxh</td>
      <td>all</td>
      <td>1.377863e+09</td>
      <td>Why I'm on strike today: I can't support mysel...</td>
      <td>1798</td>
      <td>http://www.theguardian.com/commentisfree/2013/...</td>
      <td>2183</td>
      <td>http://www.theguardian.com/commentisfree/2013/...</td>
      <td>theguardian.com</td>
    </tr>
    <tr>
      <th>555</th>
      <td>Costco</td>
      <td>hq1ld</td>
      <td>all</td>
      <td>1.307063e+09</td>
      <td>I'm buying a Costco membership</td>
      <td>2123</td>
      <td>http://i.imgur.com/Zf2nk.jpg</td>
      <td>2169</td>
      <td>http://i.imgur.com/Zf2nk.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>526</th>
      <td>Costco</td>
      <td>48t4ho</td>
      <td>all</td>
      <td>1.457057e+09</td>
      <td>Costco Raises Minimum Wage to at Least $13-to-...</td>
      <td>13103</td>
      <td>http://www.bloomberg.com/news/articles/2016-03...</td>
      <td>2154</td>
      <td>http://www.bloomberg.com/news/articles/2016-03...</td>
      <td>bloomberg.com</td>
    </tr>
    <tr>
      <th>596</th>
      <td>Costco</td>
      <td>y7a2v</td>
      <td>all</td>
      <td>1.344981e+09</td>
      <td>Costco:  A Leader in Corporate Social Respons...</td>
      <td>3464</td>
      <td>http://www.triplepundit.com/2012/08/costco-gen...</td>
      <td>2132</td>
      <td>http://www.triplepundit.com/2012/08/costco-gen...</td>
      <td>triplepundit.com</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Burger King</td>
      <td>28ee3w</td>
      <td>all</td>
      <td>1.403065e+09</td>
      <td>This Burger King has had its windows broken on...</td>
      <td>3712</td>
      <td>http://i.imgur.com/Nlnt8gV.jpg</td>
      <td>2031</td>
      <td>http://i.imgur.com/Nlnt8gV.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>541</th>
      <td>Costco</td>
      <td>396myh</td>
      <td>all</td>
      <td>1.433899e+09</td>
      <td>Just-released investigation into a Costco egg ...</td>
      <td>8208</td>
      <td>https://www.youtube.com/watch?v=ZeabWClSZfI</td>
      <td>1995</td>
      <td>https://www.youtube.com/watch?v=ZeabWClSZfI</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Burger King</td>
      <td>6d9jj0</td>
      <td>all</td>
      <td>1.495747e+09</td>
      <td>If "Real People" Commercials Were Real Life - ...</td>
      <td>21221</td>
      <td>https://youtu.be/-PgfLysQua0</td>
      <td>1960</td>
      <td>https://youtu.be/-PgfLysQua0</td>
      <td>youtu.be</td>
    </tr>
    <tr>
      <th>566</th>
      <td>Costco</td>
      <td>1r4xmn</td>
      <td>all</td>
      <td>1.385069e+09</td>
      <td>Costco Apologizes for Labeling Bibles as "Fict...</td>
      <td>2150</td>
      <td>http://business.time.com/2013/11/20/costco-apo...</td>
      <td>1902</td>
      <td>http://business.time.com/2013/11/20/costco-apo...</td>
      <td>business.time.com</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Burger King</td>
      <td>3uihqe</td>
      <td>all</td>
      <td>1.448690e+09</td>
      <td>Chicago Police Deleted Footage of Them Killing...</td>
      <td>12142</td>
      <td>http://www.nbcchicago.com/investigations/laqua...</td>
      <td>1899</td>
      <td>http://www.nbcchicago.com/investigations/laqua...</td>
      <td>nbcchicago.com</td>
    </tr>
    <tr>
      <th>519</th>
      <td>Costco</td>
      <td>2rzgro</td>
      <td>all</td>
      <td>1.420945e+09</td>
      <td>Walking in to Costco</td>
      <td>40779</td>
      <td>http://i.imgur.com/pFyoZn2.gif</td>
      <td>1861</td>
      <td>http://i.imgur.com/pFyoZn2.gif</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1637</th>
      <td>Panda Express</td>
      <td>5gbut8</td>
      <td>all</td>
      <td>1.480829e+09</td>
      <td>HIF on a lazy Saturday watching YouTube videos...</td>
      <td>59</td>
      <td>https://giphy.com/gifs/aziz-ansari-tom-haverfo...</td>
      <td>0</td>
      <td>https://giphy.com/gifs/aziz-ansari-tom-haverfo...</td>
      <td>giphy.com</td>
    </tr>
    <tr>
      <th>1395</th>
      <td>Popeyes</td>
      <td>4piinn</td>
      <td>all</td>
      <td>1.466738e+09</td>
      <td>Popeye Tso's Chicken (General Tso's Chicken Ma...</td>
      <td>57</td>
      <td>http://www.seriouseats.com/recipes/2011/10/pop...</td>
      <td>0</td>
      <td>http://www.seriouseats.com/recipes/2011/10/pop...</td>
      <td>seriouseats.com</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Domino’s Pizza</td>
      <td>372a3k</td>
      <td>all</td>
      <td>1.432472e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Domino’s Pizza</td>
      <td>7m7nup</td>
      <td>all</td>
      <td>1.514322e+09</td>
      <td>ОЗОН ПАТРУЛЬ- Пицца на заказ - Domino"s Pizza</td>
      <td>1</td>
      <td>https://www.youtube.com/attribution_link?a=oJQ...</td>
      <td>0</td>
      <td>https://www.youtube.com/attribution_link?a=oJQ...</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Domino’s Pizza</td>
      <td>572osz</td>
      <td>all</td>
      <td>1.476281e+09</td>
      <td>Dominos V.S Pizza Hut</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=_I9oYZy0cUY</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=_I9oYZy0cUY</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>1841</th>
      <td>Panda Express</td>
      <td>24kmb9</td>
      <td>all</td>
      <td>1.399093e+09</td>
      <td>Panda Express has decreed I will deliver one m...</td>
      <td>22</td>
      <td>http://i.imgur.com/sXA9Lt3.jpg</td>
      <td>0</td>
      <td>http://i.imgur.com/sXA9Lt3.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1842</th>
      <td>Panda Express</td>
      <td>66hm3a</td>
      <td>all</td>
      <td>1.492723e+09</td>
      <td>If only Panda Express had brand guidelines.</td>
      <td>21</td>
      <td>https://i.redd.it/tao4vu5skpsy.jpg</td>
      <td>0</td>
      <td>https://i.redd.it/tao4vu5skpsy.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Domino’s Pizza</td>
      <td>371w1s</td>
      <td>all</td>
      <td>1.432463e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>1844</th>
      <td>Panda Express</td>
      <td>7hgg12</td>
      <td>all</td>
      <td>1.512411e+09</td>
      <td>The local Panda Express has these training cho...</td>
      <td>27</td>
      <td>https://i.redd.it/i22m00jcrv101.jpg</td>
      <td>0</td>
      <td>https://i.redd.it/i22m00jcrv101.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1765</th>
      <td>Panda Express</td>
      <td>4b3xeo</td>
      <td>all</td>
      <td>1.458437e+09</td>
      <td>Panda Express-Style Orange Chicken</td>
      <td>29</td>
      <td>https://food52.com/blog/14700-homemade-takeout...</td>
      <td>0</td>
      <td>https://food52.com/blog/14700-homemade-takeout...</td>
      <td>food52.com</td>
    </tr>
    <tr>
      <th>1835</th>
      <td>Panda Express</td>
      <td>46yr0u</td>
      <td>all</td>
      <td>1.456138e+09</td>
      <td>Tom work at a Panda Express cookie factory</td>
      <td>20</td>
      <td>http://imgur.com/L6Dzihq</td>
      <td>0</td>
      <td>http://imgur.com/L6Dzihq</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>1847</th>
      <td>Panda Express</td>
      <td>3t1pzi</td>
      <td>all</td>
      <td>1.447726e+09</td>
      <td>Cashier at Panda Express gave me and my girlfr...</td>
      <td>22</td>
      <td>http://i.imgur.com/EcGU9Kc.jpg</td>
      <td>0</td>
      <td>http://i.imgur.com/EcGU9Kc.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Domino’s Pizza</td>
      <td>61ycu</td>
      <td>all</td>
      <td>1.196647e+09</td>
      <td>Domino's Pizza is having an order online on De...</td>
      <td>0</td>
      <td>http://www.dominos.com/home/conLogin.jsp</td>
      <td>0</td>
      <td>http://www.dominos.com/home/conLogin.jsp</td>
      <td>dominos.com</td>
    </tr>
    <tr>
      <th>1646</th>
      <td>Panda Express</td>
      <td>5l4sqm</td>
      <td>all</td>
      <td>1.483150e+09</td>
      <td>Panda Express is #RCTID</td>
      <td>54</td>
      <td>https://i.reddituploads.com/b6e5e8b684be490b83...</td>
      <td>0</td>
      <td>https://i.reddituploads.com/b6e5e8b684be490b83...</td>
      <td>i.reddituploads.com</td>
    </tr>
    <tr>
      <th>1802</th>
      <td>Panda Express</td>
      <td>252cpm</td>
      <td>all</td>
      <td>1.399605e+09</td>
      <td>Poker Chip perfectly covers the Panda Express ...</td>
      <td>26</td>
      <td>http://imgur.com/tYXwEUs</td>
      <td>0</td>
      <td>http://imgur.com/tYXwEUs</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>1854</th>
      <td>Panda Express</td>
      <td>632c1s</td>
      <td>all</td>
      <td>1.491197e+09</td>
      <td>TRIGGLYPUFF 2.0 SEXUAL HARRASSMENT PANDA EXPRESS</td>
      <td>37</td>
      <td>https://m.liveleak.com/view?i=aa7_1490982861</td>
      <td>0</td>
      <td>https://m.liveleak.com/view?i=aa7_1490982861</td>
      <td>m.liveleak.com</td>
    </tr>
    <tr>
      <th>1767</th>
      <td>Panda Express</td>
      <td>3mleix</td>
      <td>all</td>
      <td>1.443402e+09</td>
      <td>Panda Express sweet fire chicken</td>
      <td>28</td>
      <td>http://damndelicious.net/2014/08/02/panda-expr...</td>
      <td>0</td>
      <td>http://damndelicious.net/2014/08/02/panda-expr...</td>
      <td>damndelicious.net</td>
    </tr>
    <tr>
      <th>1669</th>
      <td>Panda Express</td>
      <td>183rcz</td>
      <td>all</td>
      <td>1.360317e+09</td>
      <td>My fortune from panda express today.</td>
      <td>42</td>
      <td>http://imgur.com/rqH0EgA</td>
      <td>0</td>
      <td>http://imgur.com/rqH0EgA</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>1858</th>
      <td>Panda Express</td>
      <td>7zxchs</td>
      <td>all</td>
      <td>1.519516e+09</td>
      <td>Inside the kitchen of Panda Express</td>
      <td>21</td>
      <td>https://i.redd.it/93sfusv0m6i01.jpg</td>
      <td>0</td>
      <td>https://i.redd.it/93sfusv0m6i01.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1859</th>
      <td>Panda Express</td>
      <td>2x09mb</td>
      <td>all</td>
      <td>1.424827e+09</td>
      <td>Panda Express knows what's up</td>
      <td>22</td>
      <td>http://i.imgur.com/69M9gXw.jpg</td>
      <td>0</td>
      <td>http://i.imgur.com/69M9gXw.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1639</th>
      <td>Panda Express</td>
      <td>3u006h</td>
      <td>all</td>
      <td>1.448346e+09</td>
      <td>Panda Express has been celebrating all year ro...</td>
      <td>57</td>
      <td>http://imgur.com/nO9rZKz</td>
      <td>0</td>
      <td>http://imgur.com/nO9rZKz</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>1748</th>
      <td>Panda Express</td>
      <td>4v5ib8</td>
      <td>all</td>
      <td>1.469807e+09</td>
      <td>Make a movie called "The Panda Express" which ...</td>
      <td>21</td>
      <td>https://www.reddit.com/r/CrazyIdeas/comments/4...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/CrazyIdeas/comments/4...</td>
      <td>self.CrazyIdeas</td>
    </tr>
    <tr>
      <th>1675</th>
      <td>Panda Express</td>
      <td>1xzgrn</td>
      <td>all</td>
      <td>1.392507e+09</td>
      <td>MRW the employee at Panda Express, purely out ...</td>
      <td>48</td>
      <td>http://i.imgur.com/Rfr2TQP.gif</td>
      <td>0</td>
      <td>http://i.imgur.com/Rfr2TQP.gif</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1863</th>
      <td>Panda Express</td>
      <td>392tvs</td>
      <td>all</td>
      <td>1.433827e+09</td>
      <td>How Panda Express Grew From Family Business to...</td>
      <td>23</td>
      <td>http://www.nbcnews.com/news/asian-america/pand...</td>
      <td>0</td>
      <td>http://www.nbcnews.com/news/asian-america/pand...</td>
      <td>nbcnews.com</td>
    </tr>
    <tr>
      <th>1864</th>
      <td>Panda Express</td>
      <td>80z0mh</td>
      <td>all</td>
      <td>1.519876e+09</td>
      <td>The nose fell off of the sign at the Panda Exp...</td>
      <td>15</td>
      <td>https://i.redd.it/pg04yo1wd0j01.jpg</td>
      <td>0</td>
      <td>https://i.redd.it/pg04yo1wd0j01.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Domino’s Pizza</td>
      <td>3eszqt</td>
      <td>all</td>
      <td>1.438053e+09</td>
      <td>That dominos mlb pizza promotion went well... /s</td>
      <td>0</td>
      <td>http://imgur.com/G6jj6s0</td>
      <td>0</td>
      <td>http://imgur.com/G6jj6s0</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>1866</th>
      <td>Panda Express</td>
      <td>2accdc</td>
      <td>all</td>
      <td>1.405038e+09</td>
      <td>In response to the former fat man who analyzed...</td>
      <td>20</td>
      <td>http://i.imgur.com/OaAiIPN.jpg</td>
      <td>0</td>
      <td>http://i.imgur.com/OaAiIPN.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1638</th>
      <td>Panda Express</td>
      <td>2cuvc4</td>
      <td>all</td>
      <td>1.407416e+09</td>
      <td>So, my friends and I were discussing restauran...</td>
      <td>66</td>
      <td>http://i.imgur.com/hZFMMFP.png</td>
      <td>0</td>
      <td>http://i.imgur.com/hZFMMFP.png</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Domino’s Pizza</td>
      <td>4ixd3x</td>
      <td>all</td>
      <td>1.463032e+09</td>
      <td>Free Domino's Pizza with Piece of the Pie Rewa...</td>
      <td>1</td>
      <td>https://gleam.io/1pKgO-Y068C4?l=http%3A%2F%2Fw...</td>
      <td>0</td>
      <td>https://gleam.io/1pKgO-Y068C4?l=http%3A%2F%2Fw...</td>
      <td>gleam.io</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>Panda Express</td>
      <td>1waee9</td>
      <td>all</td>
      <td>1.390869e+09</td>
      <td>Panda Express Free Firecracker Chicken Breast ...</td>
      <td>27</td>
      <td>http://pandaexpress.com/coupon/full/FCCB-Free-...</td>
      <td>0</td>
      <td>http://pandaexpress.com/coupon/full/FCCB-Free-...</td>
      <td>pandaexpress.com</td>
    </tr>
  </tbody>
</table>
<p>1901 rows × 10 columns</p>
</div>




```python
reddit_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1901 entries, 0 to 1900
    Data columns (total 10 columns):
    Keyword                      1901 non-null object
    Submission ID                1901 non-null object
    Subreddit                    1901 non-null object
    Created Date                 1901 non-null float64
    Submission Title             1901 non-null object
    Submission Score             1901 non-null int64
    Submission URL               1901 non-null object
    Total Submission Comments    1901 non-null int64
    Submission URL               1901 non-null object
    Domain                       1901 non-null object
    dtypes: float64(1), int64(2), object(7)
    memory usage: 148.6+ KB



```python
reddit_df['Keyword'].value_counts()
```




    Costco            477
    Burger King       467
    Popeyes           462
    Panda Express     458
    Domino’s Pizza     37
    Name: Keyword, dtype: int64




```python
reddit_df["Total Submission Comments"].sum()
```




    350770




```python
comments = []
submission_id2 = []

for submission_id in reddit_df["Submission ID"]:
    
    submission = reddit.submission(id=submission_id)
    try:
        for comment in submission.comments:
            #print(submission_id)
            comments.append(comment.body)
            submission_id2.append(submission_id)
    except(AttributeError):
        continue
    
```


```python
comments_df = pd.DataFrame({"Submission ID":submission_id2,"Submission Comments":comments})
comments_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Submission Comments</th>
      <th>Submission ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
      <td>3712y2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Huh. Now I know why the Noid went away. It was...</td>
      <td>3712y2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>wait...wait... don't tell me</td>
      <td>3712y2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
      <td>3712y2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>One of my childhood favorite memories involved...</td>
      <td>3712y2</td>
    </tr>
  </tbody>
</table>
</div>




```python
comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 63408 entries, 0 to 63407
    Data columns (total 2 columns):
    Submission Comments    63408 non-null object
    Submission ID          63408 non-null object
    dtypes: object(2)
    memory usage: 990.8+ KB



```python
# Merge two dataframes using an outer join
reddit_comments_df = pd.merge(reddit_df, comments_df, on="Submission ID", how="outer")

reddit_comments_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 63696 entries, 0 to 63695
    Data columns (total 11 columns):
    Keyword                      63696 non-null object
    Submission ID                63696 non-null object
    Subreddit                    63696 non-null object
    Created Date                 63696 non-null float64
    Submission Title             63696 non-null object
    Submission Score             63696 non-null int64
    Submission URL               63696 non-null object
    Total Submission Comments    63696 non-null int64
    Submission URL               63696 non-null object
    Domain                       63696 non-null object
    Submission Comments          63644 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 5.8+ MB



```python
reddit_comments_df['Keyword'].value_counts()
```




    Burger King       25471
    Costco            24004
    Popeyes            9608
    Panda Express      4374
    Domino’s Pizza      239
    Name: Keyword, dtype: int64




```python
reddit_comments_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.replace("[removed]", pd.np.nan, inplace=True)
reddit_comments_df.replace("[deleted]", pd.np.nan, inplace=True)
```


```python
reddit_comments_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Yeah, I heard this story on "Wait, wait don't ...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>That guy was clearly crazy and should have bee...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I had the NES game shown in the thumbnail.  It...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I never understood why this would cause them t...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>***STAY NOIDED***</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>It comes from the Greek 'para' meaning beside,...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Now they have to keep an eye on Kile Stuffedcr...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>So I see you listened to Wait, Wait, Don't Tel...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair, they did repeatedly warn their emp...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>We used to have one of these "noids" at the of...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I was also listening to "Wait Wait Don't Tell ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>TIL. I was actually working at Domino's back t...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Avoid the Noid!</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>According to the Wikipedia article:\n\n&gt; Polic...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I used to have an avoid the noid video game on...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'm curious, because I distinctly remember tho...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait Don't Tell Me today.</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Some one listened to wait wait don't tell me t...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait this morning</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'VE SEEN FOOTAGE</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Dominoes sucked so bad back then, and I fuckin...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair if it was me I would be anoid too.</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>How many times a month does this get posted?</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>No matter how many times this is posted, I sti...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>aww poor guy</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>63666</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I could easily google this, but I figure I'd j...</td>
    </tr>
    <tr>
      <th>63667</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>A few questions please:\n\n(1) What is the rec...</td>
    </tr>
    <tr>
      <th>63668</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>This comment has been overwritten by an open s...</td>
    </tr>
    <tr>
      <th>63669</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>What are the best items on the menu?</td>
    </tr>
    <tr>
      <th>63670</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Lol exposed!!</td>
    </tr>
    <tr>
      <th>63671</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Took me a while to figure out s/o meant shout ...</td>
    </tr>
    <tr>
      <th>63672</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Hi this is the Edmonton Police. Please call 1(...</td>
    </tr>
    <tr>
      <th>63673</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Reminds me of this one time at McDonald's when...</td>
    </tr>
    <tr>
      <th>63674</th>
      <td>Panda Express</td>
      <td>6ejv8u</td>
      <td>all</td>
      <td>1.496313e+09</td>
      <td>The Panda Express is high energy!!!</td>
      <td>37</td>
      <td>https://i.redd.it/b4fmr1l54y0z.png</td>
      <td>0</td>
      <td>https://i.redd.it/b4fmr1l54y0z.png</td>
      <td>i.redd.it</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>63675</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>They must've meant that about their food.</td>
    </tr>
    <tr>
      <th>63676</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>Yes fuck that good advice</td>
    </tr>
    <tr>
      <th>63677</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>I expect mediocre Chinese food</td>
    </tr>
    <tr>
      <th>63678</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I think the older ones had a more fair judgeme...</td>
    </tr>
    <tr>
      <th>63679</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I felt like the American born Chinese reaction...</td>
    </tr>
    <tr>
      <th>63680</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>We have a Panda Express on my campus which is ...</td>
    </tr>
    <tr>
      <th>63681</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>At least in the case of the young people in th...</td>
    </tr>
    <tr>
      <th>63682</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>it closed so fast i didn't even know they exis...</td>
    </tr>
    <tr>
      <th>63683</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>I ate it back in February, and it was terrible...</td>
    </tr>
    <tr>
      <th>63684</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>Where is this?</td>
    </tr>
    <tr>
      <th>63685</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>They did take forever when all I order was spr...</td>
    </tr>
    <tr>
      <th>63686</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>How to look like you're using chopsticks</td>
    </tr>
    <tr>
      <th>63687</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>Once again, American "cleverness" completely d...</td>
    </tr>
    <tr>
      <th>63688</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>ironic, because panda express is the shitty one</td>
    </tr>
    <tr>
      <th>63689</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>There's a place called Panda Chinese Japanese ...</td>
    </tr>
    <tr>
      <th>63690</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>I know we've mentioned this new spot a couple ...</td>
    </tr>
    <tr>
      <th>63691</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>Having never been to the old Lake Ave Panda lo...</td>
    </tr>
    <tr>
      <th>63692</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>went last night- the music is too loud and the...</td>
    </tr>
    <tr>
      <th>63693</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>I don't think Yum Bunz is much like Panda Expr...</td>
    </tr>
    <tr>
      <th>63694</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>The real question is, would it matter? Is ther...</td>
    </tr>
    <tr>
      <th>63695</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>thanks for posting, glad JZ's writing stuff again</td>
    </tr>
  </tbody>
</table>
<p>63696 rows × 11 columns</p>
</div>




```python
reddit_comments_df = reddit_comments_df.dropna()
```


```python
reddit_comments_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Yeah, I heard this story on "Wait, wait don't ...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>That guy was clearly crazy and should have bee...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I had the NES game shown in the thumbnail.  It...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I never understood why this would cause them t...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>***STAY NOIDED***</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>It comes from the Greek 'para' meaning beside,...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Now they have to keep an eye on Kile Stuffedcr...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>So I see you listened to Wait, Wait, Don't Tel...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair, they did repeatedly warn their emp...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>We used to have one of these "noids" at the of...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I was also listening to "Wait Wait Don't Tell ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>TIL. I was actually working at Domino's back t...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Avoid the Noid!</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>According to the Wikipedia article:\n\n&gt; Polic...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I used to have an avoid the noid video game on...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'm curious, because I distinctly remember tho...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait Don't Tell Me today.</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Some one listened to wait wait don't tell me t...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait this morning</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'VE SEEN FOOTAGE</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Dominoes sucked so bad back then, and I fuckin...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair if it was me I would be anoid too.</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>How many times a month does this get posted?</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>No matter how many times this is posted, I sti...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>aww poor guy</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>63665</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I love Panda Express!\nAre there any dishes on...</td>
    </tr>
    <tr>
      <th>63666</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I could easily google this, but I figure I'd j...</td>
    </tr>
    <tr>
      <th>63667</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>A few questions please:\n\n(1) What is the rec...</td>
    </tr>
    <tr>
      <th>63668</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>This comment has been overwritten by an open s...</td>
    </tr>
    <tr>
      <th>63669</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>What are the best items on the menu?</td>
    </tr>
    <tr>
      <th>63670</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Lol exposed!!</td>
    </tr>
    <tr>
      <th>63671</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Took me a while to figure out s/o meant shout ...</td>
    </tr>
    <tr>
      <th>63672</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Hi this is the Edmonton Police. Please call 1(...</td>
    </tr>
    <tr>
      <th>63673</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Reminds me of this one time at McDonald's when...</td>
    </tr>
    <tr>
      <th>63675</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>They must've meant that about their food.</td>
    </tr>
    <tr>
      <th>63676</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>Yes fuck that good advice</td>
    </tr>
    <tr>
      <th>63677</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>I expect mediocre Chinese food</td>
    </tr>
    <tr>
      <th>63678</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I think the older ones had a more fair judgeme...</td>
    </tr>
    <tr>
      <th>63679</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I felt like the American born Chinese reaction...</td>
    </tr>
    <tr>
      <th>63680</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>We have a Panda Express on my campus which is ...</td>
    </tr>
    <tr>
      <th>63681</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>At least in the case of the young people in th...</td>
    </tr>
    <tr>
      <th>63682</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>it closed so fast i didn't even know they exis...</td>
    </tr>
    <tr>
      <th>63683</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>I ate it back in February, and it was terrible...</td>
    </tr>
    <tr>
      <th>63684</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>Where is this?</td>
    </tr>
    <tr>
      <th>63685</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>They did take forever when all I order was spr...</td>
    </tr>
    <tr>
      <th>63686</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>How to look like you're using chopsticks</td>
    </tr>
    <tr>
      <th>63687</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>Once again, American "cleverness" completely d...</td>
    </tr>
    <tr>
      <th>63688</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>ironic, because panda express is the shitty one</td>
    </tr>
    <tr>
      <th>63689</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>There's a place called Panda Chinese Japanese ...</td>
    </tr>
    <tr>
      <th>63690</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>I know we've mentioned this new spot a couple ...</td>
    </tr>
    <tr>
      <th>63691</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>Having never been to the old Lake Ave Panda lo...</td>
    </tr>
    <tr>
      <th>63692</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>went last night- the music is too loud and the...</td>
    </tr>
    <tr>
      <th>63693</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>I don't think Yum Bunz is much like Panda Expr...</td>
    </tr>
    <tr>
      <th>63694</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>The real question is, would it matter? Is ther...</td>
    </tr>
    <tr>
      <th>63695</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>thanks for posting, glad JZ's writing stuff again</td>
    </tr>
  </tbody>
</table>
<p>62223 rows × 11 columns</p>
</div>




```python
reddit_comments_df = reddit_comments_df.reset_index()
del reddit_comments_df['index']
```


```python
reddit_comments_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Yeah, I heard this story on "Wait, wait don't ...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>That guy was clearly crazy and should have bee...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I had the NES game shown in the thumbnail.  It...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I never understood why this would cause them t...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>***STAY NOIDED***</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>It comes from the Greek 'para' meaning beside,...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Now they have to keep an eye on Kile Stuffedcr...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>So I see you listened to Wait, Wait, Don't Tel...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair, they did repeatedly warn their emp...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>We used to have one of these "noids" at the of...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I was also listening to "Wait Wait Don't Tell ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>TIL. I was actually working at Domino's back t...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Avoid the Noid!</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>According to the Wikipedia article:\n\n&gt; Polic...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I used to have an avoid the noid video game on...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'm curious, because I distinctly remember tho...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait Don't Tell Me today.</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Some one listened to wait wait don't tell me t...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait this morning</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'VE SEEN FOOTAGE</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Dominoes sucked so bad back then, and I fuckin...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair if it was me I would be anoid too.</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>How many times a month does this get posted?</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>No matter how many times this is posted, I sti...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>aww poor guy</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>62193</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I love Panda Express!\nAre there any dishes on...</td>
    </tr>
    <tr>
      <th>62194</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I could easily google this, but I figure I'd j...</td>
    </tr>
    <tr>
      <th>62195</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>A few questions please:\n\n(1) What is the rec...</td>
    </tr>
    <tr>
      <th>62196</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>This comment has been overwritten by an open s...</td>
    </tr>
    <tr>
      <th>62197</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>What are the best items on the menu?</td>
    </tr>
    <tr>
      <th>62198</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Lol exposed!!</td>
    </tr>
    <tr>
      <th>62199</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Took me a while to figure out s/o meant shout ...</td>
    </tr>
    <tr>
      <th>62200</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Hi this is the Edmonton Police. Please call 1(...</td>
    </tr>
    <tr>
      <th>62201</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Reminds me of this one time at McDonald's when...</td>
    </tr>
    <tr>
      <th>62202</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>They must've meant that about their food.</td>
    </tr>
    <tr>
      <th>62203</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>Yes fuck that good advice</td>
    </tr>
    <tr>
      <th>62204</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>I expect mediocre Chinese food</td>
    </tr>
    <tr>
      <th>62205</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I think the older ones had a more fair judgeme...</td>
    </tr>
    <tr>
      <th>62206</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I felt like the American born Chinese reaction...</td>
    </tr>
    <tr>
      <th>62207</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>We have a Panda Express on my campus which is ...</td>
    </tr>
    <tr>
      <th>62208</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>At least in the case of the young people in th...</td>
    </tr>
    <tr>
      <th>62209</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>it closed so fast i didn't even know they exis...</td>
    </tr>
    <tr>
      <th>62210</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>I ate it back in February, and it was terrible...</td>
    </tr>
    <tr>
      <th>62211</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>Where is this?</td>
    </tr>
    <tr>
      <th>62212</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>They did take forever when all I order was spr...</td>
    </tr>
    <tr>
      <th>62213</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>How to look like you're using chopsticks</td>
    </tr>
    <tr>
      <th>62214</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>Once again, American "cleverness" completely d...</td>
    </tr>
    <tr>
      <th>62215</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>ironic, because panda express is the shitty one</td>
    </tr>
    <tr>
      <th>62216</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>There's a place called Panda Chinese Japanese ...</td>
    </tr>
    <tr>
      <th>62217</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>I know we've mentioned this new spot a couple ...</td>
    </tr>
    <tr>
      <th>62218</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>Having never been to the old Lake Ave Panda lo...</td>
    </tr>
    <tr>
      <th>62219</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>went last night- the music is too loud and the...</td>
    </tr>
    <tr>
      <th>62220</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>I don't think Yum Bunz is much like Panda Expr...</td>
    </tr>
    <tr>
      <th>62221</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>The real question is, would it matter? Is ther...</td>
    </tr>
    <tr>
      <th>62222</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>thanks for posting, glad JZ's writing stuff again</td>
    </tr>
  </tbody>
</table>
<p>62223 rows × 11 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 62223 entries, 0 to 62222
    Data columns (total 11 columns):
    Keyword                      62223 non-null object
    Submission ID                62223 non-null object
    Subreddit                    62223 non-null object
    Created Date                 62223 non-null float64
    Submission Title             62223 non-null object
    Submission Score             62223 non-null int64
    Submission URL               62223 non-null object
    Total Submission Comments    62223 non-null int64
    Submission URL               62223 non-null object
    Domain                       62223 non-null object
    Submission Comments          62223 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 5.2+ MB



```python
compound_list = []
positive_list = []
negative_list = []
neutral_list = []

for comment in reddit_comments_df["Submission Comments"]:
    
    sentiment_analysis = analyzer.polarity_scores(str(comment))

    #print(sentiment_analysis)
    compound_list.append(sentiment_analysis["compound"])
    positive_list.append(sentiment_analysis["pos"])
    negative_list.append(sentiment_analysis["neg"])
    neutral_list.append(sentiment_analysis["neu"])

    #add the sentiment analysis columns into the dataframe
reddit_comments_df["Compound Score"] = compound_list
reddit_comments_df["Positive Score"] = positive_list
reddit_comments_df["Negative Score"] = negative_list
reddit_comments_df["Neutral Score"] = neutral_list
```


```python
reddit_comments_df['Date'] = pd.to_datetime(reddit_comments_df['Created Date'],unit='s')
reddit_comments_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
      <th>Compound Score</th>
      <th>Positive Score</th>
      <th>Negative Score</th>
      <th>Neutral Score</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.063</td>
      <td>0.937</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
      <td>-0.3818</td>
      <td>0.000</td>
      <td>0.184</td>
      <td>0.816</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
      <td>0.8701</td>
      <td>0.126</td>
      <td>0.024</td>
      <td>0.850</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
      <td>0.4588</td>
      <td>0.034</td>
      <td>0.000</td>
      <td>0.966</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Yeah, I heard this story on "Wait, wait don't ...</td>
      <td>0.2960</td>
      <td>0.180</td>
      <td>0.000</td>
      <td>0.820</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>That guy was clearly crazy and should have bee...</td>
      <td>-0.2732</td>
      <td>0.186</td>
      <td>0.331</td>
      <td>0.483</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I had the NES game shown in the thumbnail.  It...</td>
      <td>-0.5423</td>
      <td>0.050</td>
      <td>0.106</td>
      <td>0.844</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I never understood why this would cause them t...</td>
      <td>0.4215</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>***STAY NOIDED***</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>It comes from the Greek 'para' meaning beside,...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Now they have to keep an eye on Kile Stuffedcr...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>So I see you listened to Wait, Wait, Don't Tel...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair, they did repeatedly warn their emp...</td>
      <td>-0.4897</td>
      <td>0.123</td>
      <td>0.345</td>
      <td>0.533</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>We used to have one of these "noids" at the of...</td>
      <td>-0.4973</td>
      <td>0.000</td>
      <td>0.062</td>
      <td>0.938</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I was also listening to "Wait Wait Don't Tell ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>TIL. I was actually working at Domino's back t...</td>
      <td>0.0698</td>
      <td>0.047</td>
      <td>0.069</td>
      <td>0.884</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Avoid the Noid!</td>
      <td>-0.3595</td>
      <td>0.000</td>
      <td>0.555</td>
      <td>0.445</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>According to the Wikipedia article:\n\n&gt; Polic...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I used to have an avoid the noid video game on...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.167</td>
      <td>0.833</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'm curious, because I distinctly remember tho...</td>
      <td>0.1655</td>
      <td>0.062</td>
      <td>0.000</td>
      <td>0.938</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait Don't Tell Me today.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Some one listened to wait wait don't tell me t...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I too listened to Wait Wait this morning</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>I'VE SEEN FOOTAGE</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Dominoes sucked so bad back then, and I fuckin...</td>
      <td>-0.9183</td>
      <td>0.000</td>
      <td>0.600</td>
      <td>0.400</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>To be fair if it was me I would be anoid too.</td>
      <td>0.3182</td>
      <td>0.187</td>
      <td>0.000</td>
      <td>0.813</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>How many times a month does this get posted?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>No matter how many times this is posted, I sti...</td>
      <td>-0.7579</td>
      <td>0.043</td>
      <td>0.296</td>
      <td>0.661</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>aww poor guy</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.608</td>
      <td>0.392</td>
      <td>2015-05-24 05:46:15</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>62193</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I love Panda Express!\nAre there any dishes on...</td>
      <td>-0.6964</td>
      <td>0.147</td>
      <td>0.193</td>
      <td>0.660</td>
      <td>2015-09-30 11:42:06</td>
    </tr>
    <tr>
      <th>62194</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>I could easily google this, but I figure I'd j...</td>
      <td>0.7476</td>
      <td>0.241</td>
      <td>0.000</td>
      <td>0.759</td>
      <td>2015-09-30 11:42:06</td>
    </tr>
    <tr>
      <th>62195</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>A few questions please:\n\n(1) What is the rec...</td>
      <td>-0.7993</td>
      <td>0.045</td>
      <td>0.098</td>
      <td>0.857</td>
      <td>2015-09-30 11:42:06</td>
    </tr>
    <tr>
      <th>62196</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>This comment has been overwritten by an open s...</td>
      <td>0.9335</td>
      <td>0.191</td>
      <td>0.031</td>
      <td>0.778</td>
      <td>2015-09-30 11:42:06</td>
    </tr>
    <tr>
      <th>62197</th>
      <td>Panda Express</td>
      <td>3mx87v</td>
      <td>all</td>
      <td>1.443613e+09</td>
      <td>I work as a server/cashier (and whatever else ...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/casualiama/comments/3...</td>
      <td>self.casualiama</td>
      <td>What are the best items on the menu?</td>
      <td>0.6369</td>
      <td>0.375</td>
      <td>0.000</td>
      <td>0.625</td>
      <td>2015-09-30 11:42:06</td>
    </tr>
    <tr>
      <th>62198</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Lol exposed!!</td>
      <td>0.4738</td>
      <td>0.722</td>
      <td>0.278</td>
      <td>0.000</td>
      <td>2017-09-23 05:47:05</td>
    </tr>
    <tr>
      <th>62199</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Took me a while to figure out s/o meant shout ...</td>
      <td>-0.1511</td>
      <td>0.000</td>
      <td>0.109</td>
      <td>0.891</td>
      <td>2017-09-23 05:47:05</td>
    </tr>
    <tr>
      <th>62200</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Hi this is the Edmonton Police. Please call 1(...</td>
      <td>0.3182</td>
      <td>0.126</td>
      <td>0.000</td>
      <td>0.874</td>
      <td>2017-09-23 05:47:05</td>
    </tr>
    <tr>
      <th>62201</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Reminds me of this one time at McDonald's when...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017-09-23 05:47:05</td>
    </tr>
    <tr>
      <th>62202</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>They must've meant that about their food.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2013-01-08 15:04:07</td>
    </tr>
    <tr>
      <th>62203</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>Yes fuck that good advice</td>
      <td>0.2732</td>
      <td>0.505</td>
      <td>0.315</td>
      <td>0.180</td>
      <td>2013-01-08 15:04:07</td>
    </tr>
    <tr>
      <th>62204</th>
      <td>Panda Express</td>
      <td>1667hh</td>
      <td>all</td>
      <td>1.357657e+09</td>
      <td>Well fuck you too panda express</td>
      <td>16</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>3</td>
      <td>http://i.imgur.com/itqbq.jpg</td>
      <td>i.imgur.com</td>
      <td>I expect mediocre Chinese food</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2013-01-08 15:04:07</td>
    </tr>
    <tr>
      <th>62205</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I think the older ones had a more fair judgeme...</td>
      <td>-0.6888</td>
      <td>0.024</td>
      <td>0.078</td>
      <td>0.897</td>
      <td>2015-02-03 03:54:22</td>
    </tr>
    <tr>
      <th>62206</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>I felt like the American born Chinese reaction...</td>
      <td>0.4404</td>
      <td>0.110</td>
      <td>0.051</td>
      <td>0.838</td>
      <td>2015-02-03 03:54:22</td>
    </tr>
    <tr>
      <th>62207</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>We have a Panda Express on my campus which is ...</td>
      <td>-0.0408</td>
      <td>0.074</td>
      <td>0.080</td>
      <td>0.846</td>
      <td>2015-02-03 03:54:22</td>
    </tr>
    <tr>
      <th>62208</th>
      <td>Panda Express</td>
      <td>2uju8b</td>
      <td>all</td>
      <td>1.422936e+09</td>
      <td>Chinese People Try Panda Express For The First...</td>
      <td>13</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>4</td>
      <td>http://www.youtube.com/watch?v=Fo59LlkTDe4</td>
      <td>youtube.com</td>
      <td>At least in the case of the young people in th...</td>
      <td>0.1531</td>
      <td>0.043</td>
      <td>0.032</td>
      <td>0.925</td>
      <td>2015-02-03 03:54:22</td>
    </tr>
    <tr>
      <th>62209</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>it closed so fast i didn't even know they exis...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-09-13 06:44:09</td>
    </tr>
    <tr>
      <th>62210</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>I ate it back in February, and it was terrible...</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.220</td>
      <td>0.780</td>
      <td>2015-09-13 06:44:09</td>
    </tr>
    <tr>
      <th>62211</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>Where is this?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-09-13 06:44:09</td>
    </tr>
    <tr>
      <th>62212</th>
      <td>Panda Express</td>
      <td>3kpuig</td>
      <td>all</td>
      <td>1.442127e+09</td>
      <td>Panda Express - Closed</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>11</td>
      <td>https://www.reddit.com/r/Oshawa/comments/3kpui...</td>
      <td>self.Oshawa</td>
      <td>They did take forever when all I order was spr...</td>
      <td>0.3400</td>
      <td>0.160</td>
      <td>0.090</td>
      <td>0.750</td>
      <td>2015-09-13 06:44:09</td>
    </tr>
    <tr>
      <th>62213</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>How to look like you're using chopsticks</td>
      <td>0.3612</td>
      <td>0.294</td>
      <td>0.000</td>
      <td>0.706</td>
      <td>2017-07-29 02:32:25</td>
    </tr>
    <tr>
      <th>62214</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>Once again, American "cleverness" completely d...</td>
      <td>-0.0076</td>
      <td>0.211</td>
      <td>0.213</td>
      <td>0.576</td>
      <td>2017-07-29 02:32:25</td>
    </tr>
    <tr>
      <th>62215</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>ironic, because panda express is the shitty one</td>
      <td>-0.6249</td>
      <td>0.000</td>
      <td>0.459</td>
      <td>0.541</td>
      <td>2016-05-22 06:45:46</td>
    </tr>
    <tr>
      <th>62216</th>
      <td>Panda Express</td>
      <td>4kfvvu</td>
      <td>all</td>
      <td>1.463900e+09</td>
      <td>Crappy Panda Express</td>
      <td>14</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>3</td>
      <td>https://imgur.com/a/6RQAL</td>
      <td>imgur.com</td>
      <td>There's a place called Panda Chinese Japanese ...</td>
      <td>-0.1779</td>
      <td>0.095</td>
      <td>0.118</td>
      <td>0.787</td>
      <td>2016-05-22 06:45:46</td>
    </tr>
    <tr>
      <th>62217</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>I know we've mentioned this new spot a couple ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2018-02-07 00:25:52</td>
    </tr>
    <tr>
      <th>62218</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>Having never been to the old Lake Ave Panda lo...</td>
      <td>0.5916</td>
      <td>0.117</td>
      <td>0.068</td>
      <td>0.816</td>
      <td>2018-02-07 00:25:52</td>
    </tr>
    <tr>
      <th>62219</th>
      <td>Panda Express</td>
      <td>7vogom</td>
      <td>all</td>
      <td>1.517963e+09</td>
      <td>Pasadena’s New Panda Express Is the Healthiest...</td>
      <td>11</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>7</td>
      <td>https://la.eater.com/2018/2/1/16956330/panda-e...</td>
      <td>la.eater.com</td>
      <td>went last night- the music is too loud and the...</td>
      <td>0.4939</td>
      <td>0.140</td>
      <td>0.057</td>
      <td>0.803</td>
      <td>2018-02-07 00:25:52</td>
    </tr>
    <tr>
      <th>62220</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>I don't think Yum Bunz is much like Panda Expr...</td>
      <td>0.1779</td>
      <td>0.103</td>
      <td>0.074</td>
      <td>0.823</td>
      <td>2013-08-12 23:16:37</td>
    </tr>
    <tr>
      <th>62221</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>The real question is, would it matter? Is ther...</td>
      <td>0.1179</td>
      <td>0.071</td>
      <td>0.000</td>
      <td>0.929</td>
      <td>2013-08-12 23:16:37</td>
    </tr>
    <tr>
      <th>62222</th>
      <td>Panda Express</td>
      <td>1k7l4o</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>Is Yum Bunz the Panda Express of dim sum?</td>
      <td>8</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>11</td>
      <td>http://clatl.com/atlanta/first-look-yum-bunz/C...</td>
      <td>clatl.com</td>
      <td>thanks for posting, glad JZ's writing stuff again</td>
      <td>0.7096</td>
      <td>0.496</td>
      <td>0.000</td>
      <td>0.504</td>
      <td>2013-08-12 23:16:37</td>
    </tr>
  </tbody>
</table>
<p>62223 rows × 16 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 62223 entries, 0 to 62222
    Data columns (total 16 columns):
    Keyword                      62223 non-null object
    Submission ID                62223 non-null object
    Subreddit                    62223 non-null object
    Created Date                 62223 non-null float64
    Submission Title             62223 non-null object
    Submission Score             62223 non-null int64
    Submission URL               62223 non-null object
    Total Submission Comments    62223 non-null int64
    Submission URL               62223 non-null object
    Domain                       62223 non-null object
    Submission Comments          62223 non-null object
    Compound Score               62223 non-null float64
    Positive Score               62223 non-null float64
    Negative Score               62223 non-null float64
    Neutral Score                62223 non-null float64
    Date                         62223 non-null datetime64[ns]
    dtypes: datetime64[ns](1), float64(5), int64(2), object(8)
    memory usage: 7.6+ MB



```python
reddit_comments_df['Date'][0].year
```




    2015




```python
reddit_comments_df['Date'] = reddit_comments_df['Date'].map(lambda x: x.year)
```


```python
reddit_comments_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
      <th>Compound Score</th>
      <th>Positive Score</th>
      <th>Negative Score</th>
      <th>Neutral Score</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>&gt;After forcing them to make him a pizza and ma...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.063</td>
      <td>0.937</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>Huh. Now I know why the Noid went away. It was...</td>
      <td>-0.3818</td>
      <td>0.000</td>
      <td>0.184</td>
      <td>0.816</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>wait...wait... don't tell me</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>True Story:\n\nThey had a heavily-advertised p...</td>
      <td>0.8701</td>
      <td>0.126</td>
      <td>0.024</td>
      <td>0.850</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>3712y2</td>
      <td>all</td>
      <td>1.432446e+09</td>
      <td>TIL in the 1980s, Dominos Pizza had a campaign...</td>
      <td>3556</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>239</td>
      <td>http://en.wikipedia.org/wiki/Noid</td>
      <td>en.wikipedia.org</td>
      <td>One of my childhood favorite memories involved...</td>
      <td>0.4588</td>
      <td>0.034</td>
      <td>0.000</td>
      <td>0.966</td>
      <td>2015</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.to_csv("bottom5_kws.csv",
                     encoding="utf-8", index=False)
```


```python
reddit_comments_df['Date'].value_counts()
```




    2017    11557
    2015    10926
    2014     8863
    2013     8403
    2016     8176
    2012     5363
    2018     4016
    2011     3597
    2010      653
    2008      355
    2009      235
    2007       79
    Name: Date, dtype: int64




```python
g_years_df = reddit_comments_df.groupby(['Keyword','Submission ID','Created Date'])
```


```python
g_years_df.count().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>Subreddit</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
      <th>Compound Score</th>
      <th>Positive Score</th>
      <th>Negative Score</th>
      <th>Neutral Score</th>
      <th>Date</th>
    </tr>
    <tr>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Created Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Burger King</th>
      <th>10bcum</th>
      <th>1.348379e+09</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>10mfie</th>
      <th>1.348876e+09</th>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
      <td>160</td>
    </tr>
    <tr>
      <th>121spq</th>
      <th>1.351168e+09</th>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
    </tr>
    <tr>
      <th>12lwuq</th>
      <th>1.352057e+09</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
    <tr>
      <th>143r41</th>
      <th>1.354402e+09</th>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
    </tr>
  </tbody>
</table>
</div>




```python
g_years_df = pd.DataFrame(g_years_df["Compound Score"].mean())
g_years_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>Compound Score</th>
    </tr>
    <tr>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Created Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="30" valign="top">Burger King</th>
      <th>10bcum</th>
      <th>1.348379e+09</th>
      <td>-0.143856</td>
    </tr>
    <tr>
      <th>10mfie</th>
      <th>1.348876e+09</th>
      <td>0.263052</td>
    </tr>
    <tr>
      <th>121spq</th>
      <th>1.351168e+09</th>
      <td>-0.129609</td>
    </tr>
    <tr>
      <th>12lwuq</th>
      <th>1.352057e+09</th>
      <td>0.105582</td>
    </tr>
    <tr>
      <th>143r41</th>
      <th>1.354402e+09</th>
      <td>0.057273</td>
    </tr>
    <tr>
      <th>14fuei</th>
      <th>1.354909e+09</th>
      <td>-0.001987</td>
    </tr>
    <tr>
      <th>14vpfd</th>
      <th>1.355574e+09</th>
      <td>0.340044</td>
    </tr>
    <tr>
      <th>152nfr</th>
      <th>1.355897e+09</th>
      <td>0.046311</td>
    </tr>
    <tr>
      <th>15tpwc</th>
      <th>1.357164e+09</th>
      <td>0.003297</td>
    </tr>
    <tr>
      <th>16xjp1</th>
      <th>1.358724e+09</th>
      <td>0.077026</td>
    </tr>
    <tr>
      <th>17pjuz</th>
      <th>1.359775e+09</th>
      <td>0.157785</td>
    </tr>
    <tr>
      <th>184ggn</th>
      <th>1.360343e+09</th>
      <td>0.180000</td>
    </tr>
    <tr>
      <th>18rehy</th>
      <th>1.361238e+09</th>
      <td>0.018666</td>
    </tr>
    <tr>
      <th>18res3</th>
      <th>1.361238e+09</th>
      <td>0.030890</td>
    </tr>
    <tr>
      <th>18x4yg</th>
      <th>1.361434e+09</th>
      <td>-0.066188</td>
    </tr>
    <tr>
      <th>18yoen</th>
      <th>1.361496e+09</th>
      <td>-0.075214</td>
    </tr>
    <tr>
      <th>1908zk</th>
      <th>1.361541e+09</th>
      <td>0.065722</td>
    </tr>
    <tr>
      <th>1930a3</th>
      <th>1.361665e+09</th>
      <td>0.227609</td>
    </tr>
    <tr>
      <th>1985mw</th>
      <th>1.361868e+09</th>
      <td>0.080326</td>
    </tr>
    <tr>
      <th>1989l0</th>
      <th>1.361871e+09</th>
      <td>0.019950</td>
    </tr>
    <tr>
      <th>19990k</th>
      <th>1.361912e+09</th>
      <td>0.123986</td>
    </tr>
    <tr>
      <th>19c8i7</th>
      <th>1.362017e+09</th>
      <td>0.073671</td>
    </tr>
    <tr>
      <th>1a5lrc</th>
      <th>1.363136e+09</th>
      <td>0.108870</td>
    </tr>
    <tr>
      <th>1agvmw</th>
      <th>1.363566e+09</th>
      <td>0.052431</td>
    </tr>
    <tr>
      <th>1bheuk</th>
      <th>1.364895e+09</th>
      <td>0.022152</td>
    </tr>
    <tr>
      <th>1dc3b4</th>
      <th>1.367270e+09</th>
      <td>0.070013</td>
    </tr>
    <tr>
      <th>1dy6mn</th>
      <th>1.368069e+09</th>
      <td>0.368338</td>
    </tr>
    <tr>
      <th>1erxbn</th>
      <th>1.369186e+09</th>
      <td>0.044728</td>
    </tr>
    <tr>
      <th>1esktk</th>
      <th>1.369203e+09</th>
      <td>0.036423</td>
    </tr>
    <tr>
      <th>1etume</th>
      <th>1.369253e+09</th>
      <td>-0.204805</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="30" valign="top">Popeyes</th>
      <th>85t9yw</th>
      <th>1.521586e+09</th>
      <td>-0.078589</td>
    </tr>
    <tr>
      <th>85y3n7</th>
      <th>1.521622e+09</th>
      <td>0.265375</td>
    </tr>
    <tr>
      <th>86q35p</th>
      <th>1.521886e+09</th>
      <td>0.189229</td>
    </tr>
    <tr>
      <th>8fk8b</th>
      <th>1.240779e+09</th>
      <td>0.033445</td>
    </tr>
    <tr>
      <th>b8wll</th>
      <th>1.267684e+09</th>
      <td>0.102536</td>
    </tr>
    <tr>
      <th>ccr3o</th>
      <th>1.276038e+09</th>
      <td>0.053465</td>
    </tr>
    <tr>
      <th>d3gge</th>
      <th>1.282343e+09</th>
      <td>0.030517</td>
    </tr>
    <tr>
      <th>dxxh2</th>
      <th>1.288331e+09</th>
      <td>0.058761</td>
    </tr>
    <tr>
      <th>hn5on</th>
      <th>1.306748e+09</th>
      <td>0.072240</td>
    </tr>
    <tr>
      <th>m8q0w</th>
      <th>1.321053e+09</th>
      <td>0.148854</td>
    </tr>
    <tr>
      <th>ocm6e</th>
      <th>1.326334e+09</th>
      <td>0.004275</td>
    </tr>
    <tr>
      <th>oe7m5</th>
      <th>1.326422e+09</th>
      <td>0.166437</td>
    </tr>
    <tr>
      <th>pas5m</th>
      <th>1.328405e+09</th>
      <td>-0.160825</td>
    </tr>
    <tr>
      <th>pm7ky</th>
      <th>1.329097e+09</th>
      <td>0.118608</td>
    </tr>
    <tr>
      <th>pmmyt</th>
      <th>1.329118e+09</th>
      <td>0.114650</td>
    </tr>
    <tr>
      <th>pnqyj</th>
      <th>1.329186e+09</th>
      <td>0.125605</td>
    </tr>
    <tr>
      <th>pv7jb</th>
      <th>1.329602e+09</th>
      <td>0.096973</td>
    </tr>
    <tr>
      <th>q5oni</th>
      <th>1.330224e+09</th>
      <td>0.297820</td>
    </tr>
    <tr>
      <th>qqj7g</th>
      <th>1.331435e+09</th>
      <td>-0.020950</td>
    </tr>
    <tr>
      <th>qum2x</th>
      <th>1.331681e+09</th>
      <td>0.163142</td>
    </tr>
    <tr>
      <th>rgq1j</th>
      <th>1.332923e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>sy9ef</th>
      <th>1.335744e+09</th>
      <td>0.280166</td>
    </tr>
    <tr>
      <th>t7huj</th>
      <th>1.336197e+09</th>
      <td>0.183867</td>
    </tr>
    <tr>
      <th>tp09v</th>
      <th>1.337152e+09</th>
      <td>0.278613</td>
    </tr>
    <tr>
      <th>vrnds</th>
      <th>1.340955e+09</th>
      <td>-0.291575</td>
    </tr>
    <tr>
      <th>vx5of</th>
      <th>1.341260e+09</th>
      <td>-0.261275</td>
    </tr>
    <tr>
      <th>x4vd9</th>
      <th>1.343259e+09</th>
      <td>0.127595</td>
    </tr>
    <tr>
      <th>xo61o</th>
      <th>1.344119e+09</th>
      <td>-0.017283</td>
    </tr>
    <tr>
      <th>y111u</th>
      <th>1.344678e+09</th>
      <td>0.089111</td>
    </tr>
    <tr>
      <th>yp0h3</th>
      <th>1.345758e+09</th>
      <td>0.091835</td>
    </tr>
  </tbody>
</table>
<p>1848 rows × 1 columns</p>
</div>




```python
g_years_df = g_years_df.reset_index()
g_years_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Created Date</th>
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burger King</td>
      <td>10bcum</td>
      <td>1.348379e+09</td>
      <td>-0.143856</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burger King</td>
      <td>10mfie</td>
      <td>1.348876e+09</td>
      <td>0.263052</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Burger King</td>
      <td>121spq</td>
      <td>1.351168e+09</td>
      <td>-0.129609</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Burger King</td>
      <td>12lwuq</td>
      <td>1.352057e+09</td>
      <td>0.105582</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Burger King</td>
      <td>143r41</td>
      <td>1.354402e+09</td>
      <td>0.057273</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set()
sns.lmplot(x='Created Date', y='Compound Score', hue="Keyword", data=g_years_df, fit_reg=False, palette="Paired")

#plt.title("Restaurant Comment Sentiments on Reddit 2017")

plt.ylabel("Sentiment Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y') for tm in xticks],
                  rotation=25)

#xfmt = md.DateFormatter('%Y-%m-%d %H:%M:%S')
#ax.xaxis.set_major_formatter(xfmt)

plt.savefig("Restaurant_Sentiments_bottom5_all.png", dpi=350)

plt.show()
```


![png](output_34_0.png)



```python
year_2017_df = reddit_comments_df.loc[reddit_comments_df["Date"] == 2017,:]
year_2017_df.head()

#year_2017_df = combined_kw.loc[reddit_comments_df["Date"] == 2017,:]
#year_2018_df = combined_kw.loc[reddit_comments_df["Date"] == 2018,:]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
      <th>Compound Score</th>
      <th>Positive Score</th>
      <th>Negative Score</th>
      <th>Neutral Score</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>149</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>These commercials drove a man insane!</td>
      <td>-0.4574</td>
      <td>0.000</td>
      <td>0.428</td>
      <td>0.572</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>150</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>I knew a guy called Noid. Punk rocker. His rea...</td>
      <td>-0.2421</td>
      <td>0.000</td>
      <td>0.035</td>
      <td>0.965</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>The NES game, Avoid the Noid, was really good....</td>
      <td>0.6738</td>
      <td>0.193</td>
      <td>0.063</td>
      <td>0.744</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>This isn't really obscure. It was part of the ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>Excellent collection.  Thanks for sharing!</td>
      <td>0.8655</td>
      <td>0.829</td>
      <td>0.000</td>
      <td>0.171</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
</div>




```python
year_2017_df = year_2017_df.reset_index()
del year_2017_df['index']
year_2017_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Subreddit</th>
      <th>Created Date</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
      <th>Compound Score</th>
      <th>Positive Score</th>
      <th>Negative Score</th>
      <th>Neutral Score</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>These commercials drove a man insane!</td>
      <td>-0.4574</td>
      <td>0.000</td>
      <td>0.428</td>
      <td>0.572</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>I knew a guy called Noid. Punk rocker. His rea...</td>
      <td>-0.2421</td>
      <td>0.000</td>
      <td>0.035</td>
      <td>0.965</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>The NES game, Avoid the Noid, was really good....</td>
      <td>0.6738</td>
      <td>0.193</td>
      <td>0.063</td>
      <td>0.744</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>This isn't really obscure. It was part of the ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>Excellent collection.  Thanks for sharing!</td>
      <td>0.8655</td>
      <td>0.829</td>
      <td>0.000</td>
      <td>0.171</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>I have a giant stuffed Noid :)</td>
      <td>0.4588</td>
      <td>0.429</td>
      <td>0.000</td>
      <td>0.571</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>Will Vinton's studio did these ads, IIRC.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>Amazing. I was the Noid for Halloween one year.</td>
      <td>0.5859</td>
      <td>0.352</td>
      <td>0.000</td>
      <td>0.648</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>There are people who benefit from an explanati...</td>
      <td>0.4588</td>
      <td>0.214</td>
      <td>0.000</td>
      <td>0.786</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>Yo! Noid!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>&gt; (1980)s Domino's Pizza's Avoid The Noid comm...</td>
      <td>-0.8860</td>
      <td>0.000</td>
      <td>0.257</td>
      <td>0.743</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>I remember when the Noid first came out, you c...</td>
      <td>0.4939</td>
      <td>0.138</td>
      <td>0.000</td>
      <td>0.862</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>Not to sound rude, but the Noid is somewhat ic...</td>
      <td>-0.2500</td>
      <td>0.000</td>
      <td>0.182</td>
      <td>0.818</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>/r/80sfastfood</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>He's back on the domino's pinball game.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Domino’s Pizza</td>
      <td>739tdv</td>
      <td>all</td>
      <td>1.506739e+09</td>
      <td>(1980)s Domino's Pizza's Avoid The Noid commer...</td>
      <td>179</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>52</td>
      <td>https://www.youtube.com/watch?v=QP6nkbJf7Xw&amp;li...</td>
      <td>youtube.com</td>
      <td>The Noid was made by Will Vinton, the man who ...</td>
      <td>0.2500</td>
      <td>0.125</td>
      <td>0.000</td>
      <td>0.875</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>Reminds me of  McDonald's on Australia Day two...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>When I sold pizza and we'd get a lot of people...</td>
      <td>0.4588</td>
      <td>0.083</td>
      <td>0.056</td>
      <td>0.860</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>That is how April Fools for a company is done....</td>
      <td>0.2263</td>
      <td>0.210</td>
      <td>0.156</td>
      <td>0.634</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>People mock marketers for treating people like...</td>
      <td>-0.4215</td>
      <td>0.130</td>
      <td>0.180</td>
      <td>0.691</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>What a sinister prank.</td>
      <td>-0.5994</td>
      <td>0.000</td>
      <td>0.661</td>
      <td>0.339</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>This reminds me of the Diamond Shreddies campa...</td>
      <td>0.8689</td>
      <td>0.403</td>
      <td>0.066</td>
      <td>0.531</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>That's just like Diamond Shreddies.  Actually ...</td>
      <td>0.7184</td>
      <td>0.500</td>
      <td>0.000</td>
      <td>0.500</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>Diamond Shreddies were pretty good too, basica...</td>
      <td>0.8176</td>
      <td>0.548</td>
      <td>0.000</td>
      <td>0.452</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>Back in the early 1980's when A&amp;W was a thing ...</td>
      <td>-0.8519</td>
      <td>0.000</td>
      <td>0.165</td>
      <td>0.835</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>Only lefties can read this comment.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>McDonald's just tried something like this in A...</td>
      <td>0.3612</td>
      <td>0.094</td>
      <td>0.000</td>
      <td>0.906</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>I immediately started reading this with cautio...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>These people vote.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Burger King</td>
      <td>61xoze</td>
      <td>all</td>
      <td>1.490710e+09</td>
      <td>TIL for April Fools Day in 1998, Burger King t...</td>
      <td>42307</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>2184</td>
      <td>http://content.time.com/time/specials/packages...</td>
      <td>content.time.com</td>
      <td>Rotating it 180 degrees would not make it left...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11527</th>
      <td>Panda Express</td>
      <td>5qbx3k</td>
      <td>all</td>
      <td>1.485485e+09</td>
      <td>Panda Express Drive Thru Clip</td>
      <td>16</td>
      <td>https://www.youtube.com/watch?v=-a1NMFmJqqs</td>
      <td>3</td>
      <td>https://www.youtube.com/watch?v=-a1NMFmJqqs</td>
      <td>youtube.com</td>
      <td>The Dad accent killed me lol. Good job Jean.</td>
      <td>0.0516</td>
      <td>0.352</td>
      <td>0.278</td>
      <td>0.370</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11528</th>
      <td>Panda Express</td>
      <td>7acbo2</td>
      <td>all</td>
      <td>1.509666e+09</td>
      <td>Spirits, what should I order at Panda Express?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskOuija/comments/7ac...</td>
      <td>16</td>
      <td>https://www.reddit.com/r/AskOuija/comments/7ac...</td>
      <td>self.AskOuija</td>
      <td>P</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11529</th>
      <td>Panda Express</td>
      <td>5r8n9g</td>
      <td>all</td>
      <td>1.485904e+09</td>
      <td>[GIVING]FREE Panda Express firecracker Chicken</td>
      <td>26</td>
      <td>https://www.reddit.com/r/FREE/comments/5r8n9g/...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/FREE/comments/5r8n9g/...</td>
      <td>self.FREE</td>
      <td>This is a multi-use code so anyone who sees th...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11530</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>At Subway I usually get turkey with lots of ve...</td>
      <td>0.4588</td>
      <td>0.120</td>
      <td>0.000</td>
      <td>0.880</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11531</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>Getting drunk then demanding both Panda and Su...</td>
      <td>-0.5106</td>
      <td>0.000</td>
      <td>0.417</td>
      <td>0.583</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11532</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>Chicken teriyaki, orange chicken on fried or w...</td>
      <td>-0.5106</td>
      <td>0.000</td>
      <td>0.102</td>
      <td>0.898</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11533</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>The past several times I've went to Subway I'v...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11534</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>Subway - 6 inch Italian BMT on the Italian che...</td>
      <td>0.7279</td>
      <td>0.102</td>
      <td>0.000</td>
      <td>0.898</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11535</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>sweet onion chicken teriyaki on italian herbs ...</td>
      <td>0.7184</td>
      <td>0.222</td>
      <td>0.000</td>
      <td>0.778</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11536</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>Subway: Spicy Italian on Italian herbs and che...</td>
      <td>0.3612</td>
      <td>0.077</td>
      <td>0.000</td>
      <td>0.923</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11537</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>Panda Express: mixed veggies, orange chicken, ...</td>
      <td>0.6996</td>
      <td>0.149</td>
      <td>0.000</td>
      <td>0.851</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11538</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>I'm very plain at Subway. Foot-long Meatball S...</td>
      <td>0.4939</td>
      <td>0.080</td>
      <td>0.000</td>
      <td>0.920</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11539</th>
      <td>Panda Express</td>
      <td>5qiwiz</td>
      <td>all</td>
      <td>1.485572e+09</td>
      <td>What are your favorite Subway and Panda Expres...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/CasualConversation/co...</td>
      <td>self.CasualConversation</td>
      <td>Well first off I would choose not to go to Sub...</td>
      <td>0.3818</td>
      <td>0.045</td>
      <td>0.000</td>
      <td>0.955</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11540</th>
      <td>Panda Express</td>
      <td>6mi7k2</td>
      <td>all</td>
      <td>1.499757e+09</td>
      <td>How does Panda Express know where I am?</td>
      <td>15</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>self.cybersecurity</td>
      <td>On your phone, browsers have access to your lo...</td>
      <td>0.1280</td>
      <td>0.071</td>
      <td>0.046</td>
      <td>0.883</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11541</th>
      <td>Panda Express</td>
      <td>6mi7k2</td>
      <td>all</td>
      <td>1.499757e+09</td>
      <td>How does Panda Express know where I am?</td>
      <td>15</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>self.cybersecurity</td>
      <td>Your internet connection is not the only thing...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11542</th>
      <td>Panda Express</td>
      <td>6mi7k2</td>
      <td>all</td>
      <td>1.499757e+09</td>
      <td>How does Panda Express know where I am?</td>
      <td>15</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>self.cybersecurity</td>
      <td>No one can hide from The Panda</td>
      <td>-0.4404</td>
      <td>0.000</td>
      <td>0.438</td>
      <td>0.562</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11543</th>
      <td>Panda Express</td>
      <td>6mi7k2</td>
      <td>all</td>
      <td>1.499757e+09</td>
      <td>How does Panda Express know where I am?</td>
      <td>15</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>self.cybersecurity</td>
      <td>Logged into any Google services on phone and l...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11544</th>
      <td>Panda Express</td>
      <td>6mi7k2</td>
      <td>all</td>
      <td>1.499757e+09</td>
      <td>How does Panda Express know where I am?</td>
      <td>15</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/cybersecurity/comment...</td>
      <td>self.cybersecurity</td>
      <td>The Panda is one, the Panda is All!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11545</th>
      <td>Panda Express</td>
      <td>7dujhr</td>
      <td>all</td>
      <td>1.511057e+09</td>
      <td>Panda Express Orange Chicken Tacos</td>
      <td>14</td>
      <td>https://i.redd.it/lh9dvseqwryz.jpg</td>
      <td>3</td>
      <td>https://i.redd.it/lh9dvseqwryz.jpg</td>
      <td>i.redd.it</td>
      <td>Meh, I'd try it.</td>
      <td>-0.0772</td>
      <td>0.000</td>
      <td>0.302</td>
      <td>0.698</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11546</th>
      <td>Panda Express</td>
      <td>7dujhr</td>
      <td>all</td>
      <td>1.511057e+09</td>
      <td>Panda Express Orange Chicken Tacos</td>
      <td>14</td>
      <td>https://i.redd.it/lh9dvseqwryz.jpg</td>
      <td>3</td>
      <td>https://i.redd.it/lh9dvseqwryz.jpg</td>
      <td>i.redd.it</td>
      <td>Not a bad idea but I see those taco shells sha...</td>
      <td>-0.3071</td>
      <td>0.000</td>
      <td>0.111</td>
      <td>0.889</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11547</th>
      <td>Panda Express</td>
      <td>7dujhr</td>
      <td>all</td>
      <td>1.511057e+09</td>
      <td>Panda Express Orange Chicken Tacos</td>
      <td>14</td>
      <td>https://i.redd.it/lh9dvseqwryz.jpg</td>
      <td>3</td>
      <td>https://i.redd.it/lh9dvseqwryz.jpg</td>
      <td>i.redd.it</td>
      <td>Taco shells e_e</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11548</th>
      <td>Panda Express</td>
      <td>6w7ijs</td>
      <td>all</td>
      <td>1.503804e+09</td>
      <td>If you go to Panda Express and order from a bi...</td>
      <td>13</td>
      <td>https://www.reddit.com/r/lifehacks/comments/6w...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/lifehacks/comments/6w...</td>
      <td>self.lifehacks</td>
      <td>This is anecdotal. I've had to wait for food b...</td>
      <td>-0.4023</td>
      <td>0.000</td>
      <td>0.162</td>
      <td>0.838</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11549</th>
      <td>Panda Express</td>
      <td>6w7ijs</td>
      <td>all</td>
      <td>1.503804e+09</td>
      <td>If you go to Panda Express and order from a bi...</td>
      <td>13</td>
      <td>https://www.reddit.com/r/lifehacks/comments/6w...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/lifehacks/comments/6w...</td>
      <td>self.lifehacks</td>
      <td>The Panda Express by our house actually gives ...</td>
      <td>0.5562</td>
      <td>0.135</td>
      <td>0.000</td>
      <td>0.865</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11550</th>
      <td>Panda Express</td>
      <td>6w7ijs</td>
      <td>all</td>
      <td>1.503804e+09</td>
      <td>If you go to Panda Express and order from a bi...</td>
      <td>13</td>
      <td>https://www.reddit.com/r/lifehacks/comments/6w...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/lifehacks/comments/6w...</td>
      <td>self.lifehacks</td>
      <td>LPT: Go to Panda Express and have the cashier ...</td>
      <td>0.5106</td>
      <td>0.155</td>
      <td>0.070</td>
      <td>0.775</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11551</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Lol exposed!!</td>
      <td>0.4738</td>
      <td>0.722</td>
      <td>0.278</td>
      <td>0.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11552</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Took me a while to figure out s/o meant shout ...</td>
      <td>-0.1511</td>
      <td>0.000</td>
      <td>0.109</td>
      <td>0.891</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11553</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Hi this is the Edmonton Police. Please call 1(...</td>
      <td>0.3182</td>
      <td>0.126</td>
      <td>0.000</td>
      <td>0.874</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11554</th>
      <td>Panda Express</td>
      <td>71u8oi</td>
      <td>all</td>
      <td>1.506146e+09</td>
      <td>Hijacking Panda Express Soda Dispenser</td>
      <td>14</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/uAlberta/comments/71u...</td>
      <td>self.uAlberta</td>
      <td>Reminds me of this one time at McDonald's when...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11555</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>How to look like you're using chopsticks</td>
      <td>0.3612</td>
      <td>0.294</td>
      <td>0.000</td>
      <td>0.706</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11556</th>
      <td>Panda Express</td>
      <td>6q5rky</td>
      <td>all</td>
      <td>1.501296e+09</td>
      <td>My fork from Panda Express was also chopsticks</td>
      <td>21</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/918ddgz9ndcz.jpg</td>
      <td>i.redd.it</td>
      <td>Once again, American "cleverness" completely d...</td>
      <td>-0.0076</td>
      <td>0.211</td>
      <td>0.213</td>
      <td>0.576</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
<p>11557 rows × 16 columns</p>
</div>




```python
g_year_2017_df = year_2017_df.groupby(['Keyword','Submission ID','Created Date'])
```


```python
g_year_2017_df.count().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>Subreddit</th>
      <th>Submission Title</th>
      <th>Submission Score</th>
      <th>Submission URL</th>
      <th>Total Submission Comments</th>
      <th>Submission URL</th>
      <th>Domain</th>
      <th>Submission Comments</th>
      <th>Compound Score</th>
      <th>Positive Score</th>
      <th>Negative Score</th>
      <th>Neutral Score</th>
      <th>Date</th>
    </tr>
    <tr>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Created Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Burger King</th>
      <th>5m8nsx</th>
      <th>1.483675e+09</th>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5mllq7</th>
      <th>1.483839e+09</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5nns1h</th>
      <th>1.484302e+09</th>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
      <td>21</td>
    </tr>
    <tr>
      <th>5nst9e</th>
      <th>1.484366e+09</th>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5px5ik</th>
      <th>1.485305e+09</th>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
      <td>130</td>
    </tr>
  </tbody>
</table>
</div>




```python
g_year_2017_df = pd.DataFrame(g_year_2017_df["Compound Score"].mean())
g_year_2017_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>Compound Score</th>
    </tr>
    <tr>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Created Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="30" valign="top">Burger King</th>
      <th>5m8nsx</th>
      <th>1.483675e+09</th>
      <td>-0.080333</td>
    </tr>
    <tr>
      <th>5mllq7</th>
      <th>1.483839e+09</th>
      <td>0.146800</td>
    </tr>
    <tr>
      <th>5nns1h</th>
      <th>1.484302e+09</th>
      <td>0.144386</td>
    </tr>
    <tr>
      <th>5nst9e</th>
      <th>1.484366e+09</th>
      <td>-0.335700</td>
    </tr>
    <tr>
      <th>5px5ik</th>
      <th>1.485305e+09</th>
      <td>-0.097292</td>
    </tr>
    <tr>
      <th>5rclkr</th>
      <th>1.485942e+09</th>
      <td>0.157140</td>
    </tr>
    <tr>
      <th>5u0djp</th>
      <th>1.487110e+09</th>
      <td>0.445800</td>
    </tr>
    <tr>
      <th>5u7gue</th>
      <th>1.487196e+09</th>
      <td>-0.168575</td>
    </tr>
    <tr>
      <th>5uhzr4</th>
      <th>1.487309e+09</th>
      <td>-0.084249</td>
    </tr>
    <tr>
      <th>5uj7co</th>
      <th>1.487322e+09</th>
      <td>-0.121273</td>
    </tr>
    <tr>
      <th>5ulnxb</th>
      <th>1.487360e+09</th>
      <td>-0.100896</td>
    </tr>
    <tr>
      <th>5uyzpw</th>
      <th>1.487550e+09</th>
      <td>0.189489</td>
    </tr>
    <tr>
      <th>5vbxcp</th>
      <th>1.487718e+09</th>
      <td>-0.026565</td>
    </tr>
    <tr>
      <th>5vc9l5</th>
      <th>1.487722e+09</th>
      <td>0.169550</td>
    </tr>
    <tr>
      <th>5vcm06</th>
      <th>1.487725e+09</th>
      <td>-0.051864</td>
    </tr>
    <tr>
      <th>5vv4xw</th>
      <th>1.487935e+09</th>
      <td>-0.116524</td>
    </tr>
    <tr>
      <th>5wmt0d</th>
      <th>1.488298e+09</th>
      <td>0.149891</td>
    </tr>
    <tr>
      <th>5wvtvi</th>
      <th>1.488404e+09</th>
      <td>-0.034831</td>
    </tr>
    <tr>
      <th>5wwont</th>
      <th>1.488412e+09</th>
      <td>-0.020590</td>
    </tr>
    <tr>
      <th>5wwotk</th>
      <th>1.488412e+09</th>
      <td>-0.017737</td>
    </tr>
    <tr>
      <th>5wwoxe</th>
      <th>1.488412e+09</th>
      <td>0.034704</td>
    </tr>
    <tr>
      <th>5x9yu3</th>
      <th>1.488571e+09</th>
      <td>-0.159608</td>
    </tr>
    <tr>
      <th>5xyqh7</th>
      <th>1.488895e+09</th>
      <td>-0.045537</td>
    </tr>
    <tr>
      <th>5yyol4</th>
      <th>1.489354e+09</th>
      <td>-0.014511</td>
    </tr>
    <tr>
      <th>60u6ee</th>
      <th>1.490213e+09</th>
      <td>-0.265302</td>
    </tr>
    <tr>
      <th>60w2o1</th>
      <th>1.490233e+09</th>
      <td>-0.032100</td>
    </tr>
    <tr>
      <th>617wtv</th>
      <th>1.490376e+09</th>
      <td>0.084020</td>
    </tr>
    <tr>
      <th>618gll</th>
      <th>1.490385e+09</th>
      <td>0.000214</td>
    </tr>
    <tr>
      <th>61m1gv</th>
      <th>1.490570e+09</th>
      <td>-0.090669</td>
    </tr>
    <tr>
      <th>61xoze</th>
      <th>1.490710e+09</th>
      <td>-0.055210</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="30" valign="top">Popeyes</th>
      <th>772lap</th>
      <th>1.508312e+09</th>
      <td>0.011087</td>
    </tr>
    <tr>
      <th>779pex</th>
      <th>1.508390e+09</th>
      <td>0.093369</td>
    </tr>
    <tr>
      <th>77ag0j</th>
      <th>1.508397e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>77e6tz</th>
      <th>1.508447e+09</th>
      <td>0.162544</td>
    </tr>
    <tr>
      <th>77f98d</th>
      <th>1.508457e+09</th>
      <td>0.046820</td>
    </tr>
    <tr>
      <th>78libk</th>
      <th>1.508936e+09</th>
      <td>-0.059818</td>
    </tr>
    <tr>
      <th>78wn0u</th>
      <th>1.509063e+09</th>
      <td>0.190253</td>
    </tr>
    <tr>
      <th>792968</th>
      <th>1.509127e+09</th>
      <td>0.023783</td>
    </tr>
    <tr>
      <th>79x37s</th>
      <th>1.509498e+09</th>
      <td>-0.339940</td>
    </tr>
    <tr>
      <th>7aj95r</th>
      <th>1.509743e+09</th>
      <td>0.275720</td>
    </tr>
    <tr>
      <th>7amu1o</th>
      <th>1.509777e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>7apqlt</th>
      <th>1.509817e+09</th>
      <td>0.022200</td>
    </tr>
    <tr>
      <th>7byf3v</th>
      <th>1.510311e+09</th>
      <td>-0.013616</td>
    </tr>
    <tr>
      <th>7dso4o</th>
      <th>1.511038e+09</th>
      <td>-0.536200</td>
    </tr>
    <tr>
      <th>7dt5be</th>
      <th>1.511043e+09</th>
      <td>-0.172287</td>
    </tr>
    <tr>
      <th>7eqxdw</th>
      <th>1.511386e+09</th>
      <td>0.414133</td>
    </tr>
    <tr>
      <th>7gez8s</th>
      <th>1.512005e+09</th>
      <td>-0.165943</td>
    </tr>
    <tr>
      <th>7gz35n</th>
      <th>1.512200e+09</th>
      <td>0.387691</td>
    </tr>
    <tr>
      <th>7h508a</th>
      <th>1.512275e+09</th>
      <td>-0.038709</td>
    </tr>
    <tr>
      <th>7hb2kx</th>
      <th>1.512352e+09</th>
      <td>0.257940</td>
    </tr>
    <tr>
      <th>7hx72x</th>
      <th>1.512585e+09</th>
      <td>-0.438900</td>
    </tr>
    <tr>
      <th>7ifesy</th>
      <th>1.512773e+09</th>
      <td>-0.223880</td>
    </tr>
    <tr>
      <th>7ig7iu</th>
      <th>1.512781e+09</th>
      <td>-0.127062</td>
    </tr>
    <tr>
      <th>7igdp9</th>
      <th>1.512782e+09</th>
      <td>0.057480</td>
    </tr>
    <tr>
      <th>7ik8ax</th>
      <th>1.512818e+09</th>
      <td>0.292164</td>
    </tr>
    <tr>
      <th>7jk3fe</th>
      <th>1.513209e+09</th>
      <td>-0.014356</td>
    </tr>
    <tr>
      <th>7ju6ij</th>
      <th>1.513310e+09</th>
      <td>0.427327</td>
    </tr>
    <tr>
      <th>7kz03y</th>
      <th>1.513773e+09</th>
      <td>0.209200</td>
    </tr>
    <tr>
      <th>7mz481</th>
      <th>1.514632e+09</th>
      <td>0.297491</td>
    </tr>
    <tr>
      <th>7n0jff</th>
      <th>1.514651e+09</th>
      <td>-0.142489</td>
    </tr>
  </tbody>
</table>
<p>449 rows × 1 columns</p>
</div>




```python
g_year_2017_df = g_year_2017_df.reset_index()
g_year_2017_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Keyword</th>
      <th>Submission ID</th>
      <th>Created Date</th>
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burger King</td>
      <td>5m8nsx</td>
      <td>1.483675e+09</td>
      <td>-0.080333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burger King</td>
      <td>5mllq7</td>
      <td>1.483839e+09</td>
      <td>0.146800</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Burger King</td>
      <td>5nns1h</td>
      <td>1.484302e+09</td>
      <td>0.144386</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Burger King</td>
      <td>5nst9e</td>
      <td>1.484366e+09</td>
      <td>-0.335700</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Burger King</td>
      <td>5px5ik</td>
      <td>1.485305e+09</td>
      <td>-0.097292</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', hue="Keyword", data=g_year_2017_df, fit_reg=False, palette="Paired")

#plt.title("Restaurant Comment Sentiments on Reddit 2017")

plt.ylabel("Sentiment Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y-%m-%d') for tm in xticks],
                  rotation=25)

#xfmt = md.DateFormatter('%Y-%m-%d %H:%M:%S')
#ax.xaxis.set_major_formatter(xfmt)

plt.savefig("Restaurant_Sentiments_bottom5_2017.png", dpi=350)

plt.show()
```


![png](output_41_0.png)



```python
#reddit_comments_df['Created Date'] = reddit_comments_df['Created Date'].dt.strftime('%m/%d/%Y')

#reddit_comments_df.head()
```


```python
reddit_comments_df['Keyword'].value_counts()
```




    Taco Bell                 32248
    McDonald's                 3971
    Subway Restaurant          3606
    Wendy's                     478
    Chipotle Mexican Grill      379
    Name: Keyword, dtype: int64




```python
keyword_data = {}

for keyword in reddit_comments_df['Keyword']:
   
   keyword_data[keyword] = reddit_comments_df[reddit_comments_df['Keyword']== keyword]
```


```python
for kw in keyword_data.keys():
   
   dataframe = keyword_data[kw]
   
   sns.set()
   sns.lmplot(x='Created Date', y='Compound Score', data=dataframe, hue="Keyword", fit_reg=False)

   plt.title("Brand Comments on Reddit")

   plt.ylabel("Tweet Polarity")
   plt.xlabel("Date")

   plt.grid(True)
    #plt.xlim([100, 0])
   plt.ylim([-1, 1])

    #plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)
#ax=plt.gca()
#xfmt = md.DateFormatter('%Y-%m-%d %H:%M:%S')
#ax.xaxis.set_major_formatter(xfmt)
       
   plt.show()
    
   
```


![png](output_45_0.png)



![png](output_45_1.png)



![png](output_45_2.png)



![png](output_45_3.png)



![png](output_45_4.png)

