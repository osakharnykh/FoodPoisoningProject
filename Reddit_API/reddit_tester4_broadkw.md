

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

keywords = ["Chipotle Mexican Grill", "McDonald's", "Subway Restaurant", "Taco Bell",
           "Wendy's"]

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
      <th>1092</th>
      <td>Taco Bell</td>
      <td>21il1d</td>
      <td>all</td>
      <td>1.395967e+09</td>
      <td>I am Brian Niccol, President of Taco Bell. Tod...</td>
      <td>1773</td>
      <td>https://www.reddit.com/r/IAmA/comments/21il1d/...</td>
      <td>8275</td>
      <td>https://www.reddit.com/r/IAmA/comments/21il1d/...</td>
      <td>self.IAmA</td>
    </tr>
    <tr>
      <th>1390</th>
      <td>Taco Bell</td>
      <td>5ea6y0</td>
      <td>all</td>
      <td>1.479842e+09</td>
      <td>Hey Reddit, I Am A Taco Bell employee who work...</td>
      <td>14383</td>
      <td>https://www.reddit.com/r/IAmA/comments/5ea6y0/...</td>
      <td>5476</td>
      <td>https://www.reddit.com/r/IAmA/comments/5ea6y0/...</td>
      <td>self.IAmA</td>
    </tr>
    <tr>
      <th>1101</th>
      <td>Taco Bell</td>
      <td>7xvcbl</td>
      <td>all</td>
      <td>1.518774e+09</td>
      <td>170 upvotes and I’ll buy these $170 custom Nik...</td>
      <td>16083</td>
      <td>https://i.redd.it/6c8sf7ilahg01.jpg</td>
      <td>4195</td>
      <td>https://i.redd.it/6c8sf7ilahg01.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1132</th>
      <td>Taco Bell</td>
      <td>33ldqt</td>
      <td>all</td>
      <td>1.429826e+09</td>
      <td>McDonald's sales continue to plummet worldwide...</td>
      <td>11964</td>
      <td>http://www.sfgate.com/business/article/McDonal...</td>
      <td>4045</td>
      <td>http://www.sfgate.com/business/article/McDonal...</td>
      <td>sfgate.com</td>
    </tr>
    <tr>
      <th>1171</th>
      <td>Taco Bell</td>
      <td>1s2sso</td>
      <td>all</td>
      <td>1.386194e+09</td>
      <td>CEO Of Yumi Brands (KFC, Taco Bell, Pizza Hut)...</td>
      <td>3047</td>
      <td>http://iacknowledge.net/major-ceo-makes-100-mi...</td>
      <td>3923</td>
      <td>http://iacknowledge.net/major-ceo-makes-100-mi...</td>
      <td>iacknowledge.net</td>
    </tr>
    <tr>
      <th>1133</th>
      <td>Taco Bell</td>
      <td>21i1qs</td>
      <td>all</td>
      <td>1.395954e+09</td>
      <td>Taco Bell's New Breakfast Menu</td>
      <td>1710</td>
      <td>http://imgur.com/a/4xzQR</td>
      <td>3758</td>
      <td>http://imgur.com/a/4xzQR</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>626</th>
      <td>Subway Restaurant</td>
      <td>1uvfsu</td>
      <td>all</td>
      <td>1.389377e+09</td>
      <td>IAmA Subway Restaurant Employee for just over ...</td>
      <td>1105</td>
      <td>https://www.reddit.com/r/IAmA/comments/1uvfsu/...</td>
      <td>3671</td>
      <td>https://www.reddit.com/r/IAmA/comments/1uvfsu/...</td>
      <td>self.IAmA</td>
    </tr>
    <tr>
      <th>1550</th>
      <td>Wendy's</td>
      <td>7dl6m1</td>
      <td>all</td>
      <td>1.510957e+09</td>
      <td>Perverted Wendy Williams willingly performs se...</td>
      <td>26749</td>
      <td>https://www.youtube.com/watch?v=Ml79j4zNVcE</td>
      <td>3423</td>
      <td>https://www.youtube.com/watch?v=Ml79j4zNVcE</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>1106</th>
      <td>Taco Bell</td>
      <td>3luli7</td>
      <td>all</td>
      <td>1.442896e+09</td>
      <td>Taco Bell</td>
      <td>28183</td>
      <td>http://i.imgur.com/B9Qb7km.jpg</td>
      <td>3316</td>
      <td>http://i.imgur.com/B9Qb7km.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1107</th>
      <td>Taco Bell</td>
      <td>tj3y3</td>
      <td>all</td>
      <td>1.336817e+09</td>
      <td>I just won 3 free tacos at taco bell. Reddit, ...</td>
      <td>967</td>
      <td>https://www.reddit.com/r/AskReddit/comments/tj...</td>
      <td>3159</td>
      <td>https://www.reddit.com/r/AskReddit/comments/tj...</td>
      <td>self.AskReddit</td>
    </tr>
    <tr>
      <th>1163</th>
      <td>Taco Bell</td>
      <td>23qaoo</td>
      <td>all</td>
      <td>1.398244e+09</td>
      <td>So this kid at my school took three dates to T...</td>
      <td>2254</td>
      <td>http://imgur.com/UMXpyZX</td>
      <td>2870</td>
      <td>http://imgur.com/UMXpyZX</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>1112</th>
      <td>Taco Bell</td>
      <td>7r50z0</td>
      <td>all</td>
      <td>1.516258e+09</td>
      <td>The 24 hour Taco Bell that got me and my frien...</td>
      <td>93613</td>
      <td>https://i.redd.it/hf5pybs7ipa01.jpg</td>
      <td>2754</td>
      <td>https://i.redd.it/hf5pybs7ipa01.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1286</th>
      <td>Taco Bell</td>
      <td>14ls68</td>
      <td>all</td>
      <td>1.355179e+09</td>
      <td>While McDonald’s enjoyed profits of 130 percen...</td>
      <td>1617</td>
      <td>http://www.cagle.com/2012/12/some-better-targe...</td>
      <td>2243</td>
      <td>http://www.cagle.com/2012/12/some-better-targe...</td>
      <td>cagle.com</td>
    </tr>
    <tr>
      <th>1190</th>
      <td>Taco Bell</td>
      <td>fau0i</td>
      <td>all</td>
      <td>1.296264e+09</td>
      <td>Taco Bell: "Thank You for Suing Us"</td>
      <td>2103</td>
      <td>http://i.huffpost.com/gen/242169/TACO-BELL-MEA...</td>
      <td>2227</td>
      <td>http://i.huffpost.com/gen/242169/TACO-BELL-MEA...</td>
      <td>i.huffpost.com</td>
    </tr>
    <tr>
      <th>1498</th>
      <td>Taco Bell</td>
      <td>jliog</td>
      <td>all</td>
      <td>1.313612e+09</td>
      <td>I am a Brit who will be visiting a Taco Bell f...</td>
      <td>449</td>
      <td>https://www.reddit.com/r/AskReddit/comments/jl...</td>
      <td>2152</td>
      <td>https://www.reddit.com/r/AskReddit/comments/jl...</td>
      <td>self.AskReddit</td>
    </tr>
    <tr>
      <th>1151</th>
      <td>Taco Bell</td>
      <td>3m7piz</td>
      <td>all</td>
      <td>1.443140e+09</td>
      <td>Taco Bell fires employee shown with hand down ...</td>
      <td>13589</td>
      <td>http://www.wibw.com/home/headlines/Taco-Bell-f...</td>
      <td>2064</td>
      <td>http://www.wibw.com/home/headlines/Taco-Bell-f...</td>
      <td>wibw.com</td>
    </tr>
    <tr>
      <th>1137</th>
      <td>Taco Bell</td>
      <td>3ra7gk</td>
      <td>all</td>
      <td>1.446538e+09</td>
      <td>Taco Bell Fires the Marketing Manager who punc...</td>
      <td>8853</td>
      <td>http://www.adweek.com/news/technology/taco-bel...</td>
      <td>2058</td>
      <td>http://www.adweek.com/news/technology/taco-bel...</td>
      <td>adweek.com</td>
    </tr>
    <tr>
      <th>1136</th>
      <td>Taco Bell</td>
      <td>39rd9i</td>
      <td>all</td>
      <td>1.434271e+09</td>
      <td>This is what you get when you order "no lettuc...</td>
      <td>19386</td>
      <td>http://imgur.com/8U4AuPt</td>
      <td>2012</td>
      <td>http://imgur.com/8U4AuPt</td>
      <td>imgur.com</td>
    </tr>
    <tr>
      <th>161</th>
      <td>McDonald's</td>
      <td>3h8ao7</td>
      <td>all</td>
      <td>1.439783e+09</td>
      <td>McDonalds worker in the 80s.</td>
      <td>10592</td>
      <td>http://m.imgur.com/QcH5CVD</td>
      <td>1960</td>
      <td>http://m.imgur.com/QcH5CVD</td>
      <td>m.imgur.com</td>
    </tr>
    <tr>
      <th>1109</th>
      <td>Taco Bell</td>
      <td>7bkvlo</td>
      <td>all</td>
      <td>1.510171e+09</td>
      <td>Girl cries racism for not getting french fries...</td>
      <td>11622</td>
      <td>https://streamable.com/21ht9</td>
      <td>1941</td>
      <td>https://streamable.com/21ht9</td>
      <td>streamable.com</td>
    </tr>
    <tr>
      <th>1093</th>
      <td>Taco Bell</td>
      <td>71l4xs</td>
      <td>all</td>
      <td>1.506047e+09</td>
      <td>Taco Bell vs Chipotle</td>
      <td>62390</td>
      <td>https://i.redd.it/uf12a09a4anz.jpg</td>
      <td>1901</td>
      <td>https://i.redd.it/uf12a09a4anz.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1150</th>
      <td>Taco Bell</td>
      <td>5laojl</td>
      <td>all</td>
      <td>1.483235e+09</td>
      <td>For the fourth year in a row my friends and I ...</td>
      <td>23317</td>
      <td>http://i.imgur.com/NX6Clbm.jpg</td>
      <td>1853</td>
      <td>http://i.imgur.com/NX6Clbm.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1105</th>
      <td>Taco Bell</td>
      <td>7bksov</td>
      <td>all</td>
      <td>1.510170e+09</td>
      <td>Creedence Clearwater Revival at a Taco Bell in...</td>
      <td>39644</td>
      <td>https://i.redd.it/rp1i9rk5oqwz.jpg</td>
      <td>1740</td>
      <td>https://i.redd.it/rp1i9rk5oqwz.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1154</th>
      <td>Taco Bell</td>
      <td>37c2og</td>
      <td>all</td>
      <td>1.432682e+09</td>
      <td>Taco Bell and Pizza Hut join companies doing a...</td>
      <td>7239</td>
      <td>http://www.theguardian.com/us-news/2015/may/26...</td>
      <td>1740</td>
      <td>http://www.theguardian.com/us-news/2015/may/26...</td>
      <td>theguardian.com</td>
    </tr>
    <tr>
      <th>1087</th>
      <td>Taco Bell</td>
      <td>66m7vj</td>
      <td>all</td>
      <td>1.492767e+09</td>
      <td>TIL that Taco Bell failed to pay the men who p...</td>
      <td>51972</td>
      <td>https://en.wikipedia.org/wiki/Taco_Bell_chihuahua</td>
      <td>1702</td>
      <td>https://en.wikipedia.org/wiki/Taco_Bell_chihuahua</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>1152</th>
      <td>Taco Bell</td>
      <td>769alp</td>
      <td>all</td>
      <td>1.507974e+09</td>
      <td>This couple is on their first date at Taco Bel...</td>
      <td>23356</td>
      <td>https://i.redd.it/2b6iqiir9prz.jpg</td>
      <td>1696</td>
      <td>https://i.redd.it/2b6iqiir9prz.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>1124</th>
      <td>Taco Bell</td>
      <td>14cpc3</td>
      <td>all</td>
      <td>1.354781e+09</td>
      <td>TIL that Doritos tacos have pulled Taco Bell o...</td>
      <td>2465</td>
      <td>http://www.huffingtonpost.com/2012/04/20/dorit...</td>
      <td>1695</td>
      <td>http://www.huffingtonpost.com/2012/04/20/dorit...</td>
      <td>huffingtonpost.com</td>
    </tr>
    <tr>
      <th>1118</th>
      <td>Taco Bell</td>
      <td>7a4ela</td>
      <td>all</td>
      <td>1.509580e+09</td>
      <td>I got my taco bell xbox one x. It came with fo...</td>
      <td>22927</td>
      <td>https://i.redd.it/k8b6ivv1xdvz.jpg</td>
      <td>1643</td>
      <td>https://i.redd.it/k8b6ivv1xdvz.jpg</td>
      <td>i.redd.it</td>
    </tr>
    <tr>
      <th>167</th>
      <td>McDonald's</td>
      <td>8719rh</td>
      <td>all</td>
      <td>1.522020e+09</td>
      <td>[AMA Request] Someone Who has won the McDonald...</td>
      <td>6867</td>
      <td>https://www.reddit.com/r/IAmA/comments/8719rh/...</td>
      <td>1641</td>
      <td>https://www.reddit.com/r/IAmA/comments/8719rh/...</td>
      <td>self.IAmA</td>
    </tr>
    <tr>
      <th>1129</th>
      <td>Taco Bell</td>
      <td>2rqn6b</td>
      <td>all</td>
      <td>1.420751e+09</td>
      <td>The day Taco Bell betrayed me .</td>
      <td>16451</td>
      <td>http://imgur.com/BgLJa7I</td>
      <td>1609</td>
      <td>http://imgur.com/BgLJa7I</td>
      <td>imgur.com</td>
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
      <th>137</th>
      <td>Chipotle Mexican Grill</td>
      <td>7gdx7w</td>
      <td>all</td>
      <td>1.511997e+09</td>
      <td>Chipotle Mexican Grill begins search for new CEO</td>
      <td>1</td>
      <td>https://www.cnbc.com/2017/11/29/chipotle-mexic...</td>
      <td>0</td>
      <td>https://www.cnbc.com/2017/11/29/chipotle-mexic...</td>
      <td>cnbc.com</td>
    </tr>
    <tr>
      <th>138</th>
      <td>Chipotle Mexican Grill</td>
      <td>7gluow</td>
      <td>all</td>
      <td>1.512072e+09</td>
      <td>@Reuters: WATCH: Embattled Chipotle Mexican Gr...</td>
      <td>1</td>
      <td>https://twitter.com/Reuters/status/93620266533...</td>
      <td>0</td>
      <td>https://twitter.com/Reuters/status/93620266533...</td>
      <td>twitter.com</td>
    </tr>
    <tr>
      <th>139</th>
      <td>Chipotle Mexican Grill</td>
      <td>408dio</td>
      <td>all</td>
      <td>1.452406e+09</td>
      <td>Chipotle Mexican Grill gets wrapped in more co...</td>
      <td>1</td>
      <td>http://sputniknews.com/news/20160110/103288651...</td>
      <td>0</td>
      <td>http://sputniknews.com/news/20160110/103288651...</td>
      <td>sputniknews.com</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Chipotle Mexican Grill</td>
      <td>78r0p</td>
      <td>all</td>
      <td>1.224738e+09</td>
      <td>CMG Chipotle Mexican Grill Earnings Preview (4...</td>
      <td>1</td>
      <td>http://www.stockmarketfunding.com/SMF-Blogs/Co...</td>
      <td>0</td>
      <td>http://www.stockmarketfunding.com/SMF-Blogs/Co...</td>
      <td>stockmarketfunding.com</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Chipotle Mexican Grill</td>
      <td>4nip6j</td>
      <td>all</td>
      <td>1.465625e+09</td>
      <td>This restaurant just unseated Chipotle as the ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/4ni...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/autotldr/comments/4ni...</td>
      <td>self.autotldr</td>
    </tr>
    <tr>
      <th>142</th>
      <td>Chipotle Mexican Grill</td>
      <td>7gd4s1</td>
      <td>all</td>
      <td>1.511990e+09</td>
      <td>[Top Stories] - Chipotle Mexican Grill begins ...</td>
      <td>1</td>
      <td>https://www.cnbc.com/2017/11/29/chipotle-mexic...</td>
      <td>0</td>
      <td>https://www.cnbc.com/2017/11/29/chipotle-mexic...</td>
      <td>cnbc.com</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Chipotle Mexican Grill</td>
      <td>23mk39</td>
      <td>all</td>
      <td>1.398146e+09</td>
      <td>Chipotle Mexican Grill, Inc. Shows How to Do G...</td>
      <td>0</td>
      <td>http://www.fool.com/investing/general/2014/04/...</td>
      <td>0</td>
      <td>http://www.fool.com/investing/general/2014/04/...</td>
      <td>fool.com</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Chipotle Mexican Grill</td>
      <td>86f4dk</td>
      <td>all</td>
      <td>1.521782e+09</td>
      <td>Chipotle Mexican Grill, Inc. To Announce First...</td>
      <td>1</td>
      <td>https://www.prnewswire.com/news-releases/chipo...</td>
      <td>0</td>
      <td>https://www.prnewswire.com/news-releases/chipo...</td>
      <td>prnewswire.com</td>
    </tr>
    <tr>
      <th>146</th>
      <td>Chipotle Mexican Grill</td>
      <td>67nfci</td>
      <td>all</td>
      <td>1.493234e+09</td>
      <td>[Tech] - WATCH: Possible data breach at Chipot...</td>
      <td>1</td>
      <td>http://abcnews.go.com/Technology/video/data-br...</td>
      <td>0</td>
      <td>http://abcnews.go.com/Technology/video/data-br...</td>
      <td>abcnews.go.com</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Chipotle Mexican Grill</td>
      <td>40rao9</td>
      <td>all</td>
      <td>1.452706e+09</td>
      <td>Brower Piven Encourages Investors Who Have Los...</td>
      <td>1</td>
      <td>http://www.financialbuzz.com/brower-piven-enco...</td>
      <td>0</td>
      <td>http://www.financialbuzz.com/brower-piven-enco...</td>
      <td>financialbuzz.com</td>
    </tr>
    <tr>
      <th>127</th>
      <td>Chipotle Mexican Grill</td>
      <td>5hexs6</td>
      <td>all</td>
      <td>1.481332e+09</td>
      <td>[Business] - Chipotle Mexican Grill Must Take ...</td>
      <td>1</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>0</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>philly.com</td>
    </tr>
    <tr>
      <th>126</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wvu6</td>
      <td>all</td>
      <td>1.433718e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/38w...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/autotldr/comments/38w...</td>
      <td>self.autotldr</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Chipotle Mexican Grill</td>
      <td>7xprmt</td>
      <td>all</td>
      <td>1.518723e+09</td>
      <td>Morning Technical Insight on These Restaurants...</td>
      <td>1</td>
      <td>https://www.prnewswire.com/news-releases/morni...</td>
      <td>0</td>
      <td>https://www.prnewswire.com/news-releases/morni...</td>
      <td>prnewswire.com</td>
    </tr>
    <tr>
      <th>109</th>
      <td>Chipotle Mexican Grill</td>
      <td>5nl8u2</td>
      <td>all</td>
      <td>1.484276e+09</td>
      <td>Illegal Pete’s v. Chipotle Mexican Grill</td>
      <td>1</td>
      <td>http://qqquestion.com/illegal-petes-v-chipotle...</td>
      <td>0</td>
      <td>http://qqquestion.com/illegal-petes-v-chipotle...</td>
      <td>qqquestion.com</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Chipotle Mexican Grill</td>
      <td>6ah1q9</td>
      <td>all</td>
      <td>1.494495e+09</td>
      <td>[Business] - Chipotle Mexican Grill: Cramer's ...</td>
      <td>1</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>0</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>philly.com</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Chipotle Mexican Grill</td>
      <td>7ha75q</td>
      <td>all</td>
      <td>1.512344e+09</td>
      <td>[Local] - Chipotle Mexican Grill to open in Pa...</td>
      <td>1</td>
      <td>https://www.newsday.com/lifestyle/restaurants/...</td>
      <td>0</td>
      <td>https://www.newsday.com/lifestyle/restaurants/...</td>
      <td>newsday.com</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Chipotle Mexican Grill</td>
      <td>7gd963</td>
      <td>all</td>
      <td>1.511991e+09</td>
      <td>[Top Stories] - Chipotle Mexican Grill begins ...</td>
      <td>1</td>
      <td>https://www.cnbc.com/2017/11/29/chipotle-mexic...</td>
      <td>0</td>
      <td>https://www.cnbc.com/2017/11/29/chipotle-mexic...</td>
      <td>cnbc.com</td>
    </tr>
    <tr>
      <th>995</th>
      <td>Subway Restaurant</td>
      <td>3or9wb</td>
      <td>all</td>
      <td>1.444878e+09</td>
      <td>Naked Woman Destroys Alaskan Subway Restaurant...</td>
      <td>3</td>
      <td>http://www.ktuu.com/news/news/naked-woman-dest...</td>
      <td>0</td>
      <td>http://www.ktuu.com/news/news/naked-woman-dest...</td>
      <td>ktuu.com</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Chipotle Mexican Grill</td>
      <td>1kaz1y</td>
      <td>all</td>
      <td>1.376457e+09</td>
      <td>Chipotle Mexican Grill is reviewing a change t...</td>
      <td>0</td>
      <td>http://bigstory.ap.org/article/chipotle-consid...</td>
      <td>0</td>
      <td>http://bigstory.ap.org/article/chipotle-consid...</td>
      <td>bigstory.ap.org</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Chipotle Mexican Grill</td>
      <td>3692ay</td>
      <td>all</td>
      <td>1.431888e+09</td>
      <td>Job openings at Chipotle Mexican Grill in Cupe...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/SanJose/comments/3692...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/SanJose/comments/3692...</td>
      <td>self.SanJose</td>
    </tr>
    <tr>
      <th>994</th>
      <td>Subway Restaurant</td>
      <td>35szpr</td>
      <td>all</td>
      <td>1.431528e+09</td>
      <td>'Intruder spray': Subway restaurant armed with...</td>
      <td>3</td>
      <td>http://rt.com/usa/257913-intruder-spray-dna-ul...</td>
      <td>0</td>
      <td>http://rt.com/usa/257913-intruder-spray-dna-ul...</td>
      <td>rt.com</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Chipotle Mexican Grill</td>
      <td>2upfty</td>
      <td>all</td>
      <td>1.423043e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG) Stock Plunges...</td>
      <td>1</td>
      <td>http://www.ibtimes.com/chipotle-mexican-grill-...</td>
      <td>0</td>
      <td>http://www.ibtimes.com/chipotle-mexican-grill-...</td>
      <td>ibtimes.com</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Chipotle Mexican Grill</td>
      <td>2upbsj</td>
      <td>all</td>
      <td>1.423041e+09</td>
      <td>After-Hours News: Walt Disney Co (DIS), Macy's...</td>
      <td>1</td>
      <td>http://www.ibtimes.com/after-hours-news-walt-d...</td>
      <td>0</td>
      <td>http://www.ibtimes.com/after-hours-news-walt-d...</td>
      <td>ibtimes.com</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Chipotle Mexican Grill</td>
      <td>5whai4</td>
      <td>all</td>
      <td>1.488238e+09</td>
      <td>Leave It To Chipotle Mexican Grill To Shame A ...</td>
      <td>1</td>
      <td>https://www.forbes.com/forbes/welcome/?toURL=h...</td>
      <td>0</td>
      <td>https://www.forbes.com/forbes/welcome/?toURL=h...</td>
      <td>forbes.com</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Chipotle Mexican Grill</td>
      <td>32zup8</td>
      <td>all</td>
      <td>1.429356e+09</td>
      <td>Chipotle Mexican Grill Pico De Gallo</td>
      <td>1</td>
      <td>http://myfrugaladventures.com/2014/07/easy-cop...</td>
      <td>0</td>
      <td>http://myfrugaladventures.com/2014/07/easy-cop...</td>
      <td>myfrugaladventures.com</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Chipotle Mexican Grill</td>
      <td>42948c</td>
      <td>all</td>
      <td>1.453548e+09</td>
      <td>SHAREHOLDER ALERT: Pomerantz Law Firm Reminds ...</td>
      <td>1</td>
      <td>http://www.financialbuzz.com/shareholder-alert...</td>
      <td>0</td>
      <td>http://www.financialbuzz.com/shareholder-alert...</td>
      <td>financialbuzz.com</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Chipotle Mexican Grill</td>
      <td>7xis35</td>
      <td>all</td>
      <td>1.518651e+09</td>
      <td>Chipotle Mexican Grill, Inc. (CMG) jumped 15% ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/FIRSTOINVEST/comments...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/FIRSTOINVEST/comments...</td>
      <td>self.FIRSTOINVEST</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Chipotle Mexican Grill</td>
      <td>3zrjuv</td>
      <td>all</td>
      <td>1.452140e+09</td>
      <td>SHAREHOLDER ALERT: Pomerantz Law Firm Investig...</td>
      <td>1</td>
      <td>http://finance.yahoo.com/news/shareholder-aler...</td>
      <td>0</td>
      <td>http://finance.yahoo.com/news/shareholder-aler...</td>
      <td>finance.yahoo.com</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Chipotle Mexican Grill</td>
      <td>1uubso</td>
      <td>all</td>
      <td>1.389342e+09</td>
      <td>[#410|+273|24] Founder of popular Mexican gril...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/thatHappened/comments/...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/thatHappened/comments/...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>1086</th>
      <td>Subway Restaurant</td>
      <td>m4t04</td>
      <td>all</td>
      <td>1.320791e+09</td>
      <td>Cops: Man runs naked through Subway restaurant...</td>
      <td>1</td>
      <td>http://www.cbsnews.com/8301-504083_162-5731995...</td>
      <td>0</td>
      <td>http://www.cbsnews.com/8301-504083_162-5731995...</td>
      <td>cbsnews.com</td>
    </tr>
  </tbody>
</table>
<p>1800 rows × 10 columns</p>
</div>




```python
reddit_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1800 entries, 0 to 1799
    Data columns (total 10 columns):
    Keyword                      1800 non-null object
    Submission ID                1800 non-null object
    Subreddit                    1800 non-null object
    Created Date                 1800 non-null float64
    Submission Title             1800 non-null object
    Submission Score             1800 non-null int64
    Submission URL               1800 non-null object
    Total Submission Comments    1800 non-null int64
    Submission URL               1800 non-null object
    Domain                       1800 non-null object
    dtypes: float64(1), int64(2), object(7)
    memory usage: 140.7+ KB



```python
reddit_df['Keyword'].value_counts()
```




    Subway Restaurant         471
    Taco Bell                 462
    McDonald's                456
    Wendy's                   251
    Chipotle Mexican Grill    160
    Name: Keyword, dtype: int64




```python
reddit_df["Total Submission Comments"].sum()
```




    231701




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
      <td>I'm reading this on my way to Chipotle. I gues...</td>
      <td>38wus9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>[deleted]</td>
      <td>38wus9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>38wus9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>So if I get a part time job making burritos th...</td>
      <td>38wus9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>This is GREAT. I am often one of the oldest cu...</td>
      <td>38wus9</td>
    </tr>
  </tbody>
</table>
</div>




```python
comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 42395 entries, 0 to 42394
    Data columns (total 2 columns):
    Submission Comments    42395 non-null object
    Submission ID          42395 non-null object
    dtypes: object(2)
    memory usage: 662.5+ KB



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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>[deleted]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 42720 entries, 0 to 42719
    Data columns (total 11 columns):
    Keyword                      42720 non-null object
    Submission ID                42720 non-null object
    Subreddit                    42720 non-null object
    Created Date                 42720 non-null float64
    Submission Title             42720 non-null object
    Submission Score             42720 non-null int64
    Submission URL               42720 non-null object
    Total Submission Comments    42720 non-null int64
    Submission URL               42720 non-null object
    Domain                       42720 non-null object
    Submission Comments          42399 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 3.9+ MB



```python
reddit_comments_df['Keyword'].value_counts()
```




    Taco Bell                 33783
    McDonald's                 4082
    Subway Restaurant          3763
    Wendy's                     626
    Chipotle Mexican Grill      466
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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>[deleted]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Now all the need is some queso!</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I think I'll go to Chipotles for dinner tonigh...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>WOW!\n\nGood food AND good treatment of employees</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Well, I guess I need to start going to Chipotl...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I do wonder if this will tempt certain investm...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>An employee that wants to be at work, and enjo...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>What's the catch?</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>could be the start of a new wave of corporate ...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will eat more burritos because of this!</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will stop coming if my burrito price increases.</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Working at chipotle as a non-salaried job is n...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Chipotle is run by anti gmo nuts. Maybe they s...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is great and all but I'm not looking forw...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Will this make the guacamole cheaper? I don't ...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Why would they not test this in Denver?</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chicago you need to help make this successful</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>As someone moving to Chicago in a few months, ...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chipotle, craft beer, and Chicago are 3 of my ...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Yay! And ten years from now we will have craft...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>60,000 bottles really isnt that much beer</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Holy shit I am so excited. I absolutely love C...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Three of my favorite things. Beer, Chicago, an...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>All right, now I can drink in a Chipotle!!!\n\...</td>
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
      <th>42690</th>
      <td>Wendy's</td>
      <td>1rs9al</td>
      <td>all</td>
      <td>1.385864e+09</td>
      <td>Grill Skills - 1980s Wendy's Training Guide</td>
      <td>0</td>
      <td>http://youtube.com/watch?v=7B5nO4LQ3do&amp;desktop...</td>
      <td>0</td>
      <td>http://youtube.com/watch?v=7B5nO4LQ3do&amp;desktop...</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42691</th>
      <td>Wendy's</td>
      <td>5whsmy</td>
      <td>all</td>
      <td>1.488243e+09</td>
      <td>Former U.S. Attorney Wendy Olson joins Stoel R...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/IdahoPolitics/comment...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/IdahoPolitics/comment...</td>
      <td>self.IdahoPolitics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42692</th>
      <td>Wendy's</td>
      <td>1vpj72</td>
      <td>all</td>
      <td>1.390286e+09</td>
      <td>Wendys Gril Skills - Rap from the 80s to teach...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=WTXsAOpSf9k&amp;no...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=WTXsAOpSf9k&amp;no...</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42693</th>
      <td>Wendy's</td>
      <td>3xe60r</td>
      <td>all</td>
      <td>1.450503e+09</td>
      <td>1980s Wendy's hip hop training video</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=4KIdTPS6LH4</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=4KIdTPS6LH4</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42694</th>
      <td>Wendy's</td>
      <td>1pj3hp</td>
      <td>all</td>
      <td>1.383157e+09</td>
      <td>State Sen. Wendy Davis, the Democratic candida...</td>
      <td>1</td>
      <td>http://www.keyetv.com/news/features/top-storie...</td>
      <td>0</td>
      <td>http://www.keyetv.com/news/features/top-storie...</td>
      <td>keyetv.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42695</th>
      <td>Wendy's</td>
      <td>7jc6xo</td>
      <td>all</td>
      <td>1.513128e+09</td>
      <td>Wendy Chan 47kg class S. 132.5kg (jr WR) B. 73...</td>
      <td>1</td>
      <td>https://instagram.com/p/BckXX1cjO56/</td>
      <td>0</td>
      <td>https://instagram.com/p/BckXX1cjO56/</td>
      <td>instagram.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42696</th>
      <td>Wendy's</td>
      <td>6u5d14</td>
      <td>all</td>
      <td>1.502948e+09</td>
      <td>TIL that Kathryn Beaumont was 13-15 years old ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/todayilearned/comment...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/todayilearned/comment...</td>
      <td>reddit.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42697</th>
      <td>Wendy's</td>
      <td>5jm2hw</td>
      <td>all</td>
      <td>1.482380e+09</td>
      <td>[Lifestyle] - Wendy's franchise owner bikes ac...</td>
      <td>1</td>
      <td>http://www.chicagotribune.com/lifestyles/sc-ed...</td>
      <td>0</td>
      <td>http://www.chicagotribune.com/lifestyles/sc-ed...</td>
      <td>chicagotribune.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42698</th>
      <td>Wendy's</td>
      <td>38tdk6</td>
      <td>all</td>
      <td>1.433641e+09</td>
      <td>Need help identifying this Wendy Lawton doll f...</td>
      <td>1</td>
      <td>http://imgur.com/uDTYNdv</td>
      <td>0</td>
      <td>http://imgur.com/uDTYNdv</td>
      <td>imgur.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42699</th>
      <td>Wendy's</td>
      <td>57azyk</td>
      <td>all</td>
      <td>1.476403e+09</td>
      <td>Woman Says She Found Marijuana in Daughter&amp;#03...</td>
      <td>0</td>
      <td>http://insider.foxnews.com/2016/10/13/woman-sa...</td>
      <td>0</td>
      <td>http://insider.foxnews.com/2016/10/13/woman-sa...</td>
      <td>insider.foxnews.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42700</th>
      <td>Wendy's</td>
      <td>808tds</td>
      <td>all</td>
      <td>1.519633e+09</td>
      <td>Oldschool fellowkids from the 90s. Thanks Wendys</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42701</th>
      <td>Wendy's</td>
      <td>cbber</td>
      <td>all</td>
      <td>1.275662e+09</td>
      <td>Epic 90's lesbian scene -- Wendy Whoppers and ...</td>
      <td>1</td>
      <td>http://www.xvideos.com/video191784/lisa_lipps_...</td>
      <td>0</td>
      <td>http://www.xvideos.com/video191784/lisa_lipps_...</td>
      <td>xvideos.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42702</th>
      <td>Wendy's</td>
      <td>2lngi4</td>
      <td>all</td>
      <td>1.415453e+09</td>
      <td>Democrats Ann Kirkpatrick and Kyrsten Sinema h...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>0</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>azcentral.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42703</th>
      <td>Wendy's</td>
      <td>2d8cyu</td>
      <td>all</td>
      <td>1.407792e+09</td>
      <td>FP's Situation Report: Maliki becomes the new ...</td>
      <td>1</td>
      <td>http://www.foreignpolicy.com/articles/2014/08/...</td>
      <td>0</td>
      <td>http://www.foreignpolicy.com/articles/2014/08/...</td>
      <td>foreignpolicy.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42704</th>
      <td>Wendy's</td>
      <td>1kl0ot</td>
      <td>all</td>
      <td>1.376820e+09</td>
      <td>Amazingly hilarious 1980s Wendy's musical trai...</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=S6Kt1rgYzjs</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=S6Kt1rgYzjs</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42705</th>
      <td>Wendy's</td>
      <td>9gbm1</td>
      <td>all</td>
      <td>1.251864e+09</td>
      <td>Damn those patties look FRESSSSH! A Wendy's tr...</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=4KIdTPS6LH4</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=4KIdTPS6LH4</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42706</th>
      <td>Wendy's</td>
      <td>52pegq</td>
      <td>all</td>
      <td>1.473867e+09</td>
      <td>Clip request: S8E12- Stupid spoiled whore vide...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/southpark/comments/52...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/southpark/comments/52...</td>
      <td>self.southpark</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42707</th>
      <td>Wendy's</td>
      <td>d7xf9</td>
      <td>all</td>
      <td>1.283324e+09</td>
      <td>1980s Wendy's Employee Training Video Uses New...</td>
      <td>1</td>
      <td>http://aht.seriouseats.com/archives/2010/08/vi...</td>
      <td>0</td>
      <td>http://aht.seriouseats.com/archives/2010/08/vi...</td>
      <td>aht.seriouseats.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42708</th>
      <td>Wendy's</td>
      <td>181mjd</td>
      <td>all</td>
      <td>1.360238e+09</td>
      <td>Wendy's training video from the 80s...</td>
      <td>1</td>
      <td>http://www.youtube.com/watch?v=X3m7CyKptM0</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=X3m7CyKptM0</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42709</th>
      <td>Wendy's</td>
      <td>2tti3u</td>
      <td>all</td>
      <td>1.422372e+09</td>
      <td>[#2 Score:1612 Comments:70] - TIL Ulysses Lee ...</td>
      <td>1</td>
      <td>http://reddit.com/r/todayilearned/comments/2ts...</td>
      <td>0</td>
      <td>http://reddit.com/r/todayilearned/comments/2ts...</td>
      <td>reddit.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42710</th>
      <td>Wendy's</td>
      <td>7o4vk</td>
      <td>all</td>
      <td>1.231400e+09</td>
      <td>Wendy's training video from the 1980s.</td>
      <td>0</td>
      <td>http://au.youtube.com/watch?v=4KIdTPS6LH4</td>
      <td>0</td>
      <td>http://au.youtube.com/watch?v=4KIdTPS6LH4</td>
      <td>au.youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42711</th>
      <td>Wendy's</td>
      <td>1mffc3</td>
      <td>all</td>
      <td>1.379274e+09</td>
      <td>Wendy's Delights: Born Pretty Store Sweet Colo...</td>
      <td>1</td>
      <td>http://wendysdelights.blogspot.co.uk/2013/09/b...</td>
      <td>0</td>
      <td>http://wendysdelights.blogspot.co.uk/2013/09/b...</td>
      <td>wendysdelights.blogspot.co.uk</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42712</th>
      <td>Wendy's</td>
      <td>24s64p</td>
      <td>all</td>
      <td>1.399333e+09</td>
      <td>"Chili Can Be Served with Cheese" - 90s Wendy'...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=eOvHZDGK-kY</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=eOvHZDGK-kY</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42713</th>
      <td>Wendy's</td>
      <td>d5xn8</td>
      <td>all</td>
      <td>1.282898e+09</td>
      <td>Video: 1980s Wendy's Employee Training Video U...</td>
      <td>0</td>
      <td>http://aht.seriouseats.com/archives/2010/08/vi...</td>
      <td>0</td>
      <td>http://aht.seriouseats.com/archives/2010/08/vi...</td>
      <td>aht.seriouseats.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42714</th>
      <td>Wendy's</td>
      <td>1e3bcb</td>
      <td>all</td>
      <td>1.368248e+09</td>
      <td>Wendy's training rap video from the 80s.</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=6ZzLG2yr7Rs</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=6ZzLG2yr7Rs</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42715</th>
      <td>Wendy's</td>
      <td>2w2627</td>
      <td>all</td>
      <td>1.424105e+09</td>
      <td>Wendy's commercial from the 80s: Soviet Fashio...</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=5CaMUfxVJVQ</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=5CaMUfxVJVQ</td>
      <td>youtube.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42716</th>
      <td>Wendy's</td>
      <td>2tti0d</td>
      <td>all</td>
      <td>1.422372e+09</td>
      <td>[#18|+3995|846] TIL Ulysses Lee Bridgeman, a m...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>reddit.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42717</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>^(Hi, I'm a bot for linking direct images of a...</td>
    </tr>
    <tr>
      <th>42718</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>Troi wasn't as morally compromised :)</td>
    </tr>
    <tr>
      <th>42719</th>
      <td>Wendy's</td>
      <td>2e9nxq</td>
      <td>all</td>
      <td>1.408735e+09</td>
      <td>80s Wendy's Training Video - Part Deux, Cold D...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>youtube.com</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
    </tr>
  </tbody>
</table>
<p>42720 rows × 11 columns</p>
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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Now all the need is some queso!</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I think I'll go to Chipotles for dinner tonigh...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>WOW!\n\nGood food AND good treatment of employees</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Well, I guess I need to start going to Chipotl...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I do wonder if this will tempt certain investm...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>An employee that wants to be at work, and enjo...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>What's the catch?</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>could be the start of a new wave of corporate ...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will eat more burritos because of this!</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will stop coming if my burrito price increases.</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Working at chipotle as a non-salaried job is n...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Chipotle is run by anti gmo nuts. Maybe they s...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is great and all but I'm not looking forw...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Will this make the guacamole cheaper? I don't ...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Why would they not test this in Denver?</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chicago you need to help make this successful</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>As someone moving to Chicago in a few months, ...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chipotle, craft beer, and Chicago are 3 of my ...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Yay! And ten years from now we will have craft...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>60,000 bottles really isnt that much beer</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Holy shit I am so excited. I absolutely love C...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Three of my favorite things. Beer, Chicago, an...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>All right, now I can drink in a Chipotle!!!\n\...</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Anyone know specifically which Chipotles will ...</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Sweet, I work in downtown Chicago and go to ch...</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>You know what they need to do is sell said bee...</td>
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
      <th>42586</th>
      <td>Wendy's</td>
      <td>tfgw6</td>
      <td>all</td>
      <td>1.336632e+09</td>
      <td>Wendy's 80s training video (Excessive amounts ...</td>
      <td>1</td>
      <td>http://www.youtube.com/watch?feature=player_em...</td>
      <td>2</td>
      <td>http://www.youtube.com/watch?feature=player_em...</td>
      <td>youtube.com</td>
      <td>Wendy's made better music and videos in the 80...</td>
    </tr>
    <tr>
      <th>42591</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>She claims to be an atheist, yet can't get thr...</td>
    </tr>
    <tr>
      <th>42592</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>she is a "fox news atheist" thats the only way...</td>
    </tr>
    <tr>
      <th>42593</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>[Who cares.](http://www.youtube.com/watch?v=1_...</td>
    </tr>
    <tr>
      <th>42597</th>
      <td>Wendy's</td>
      <td>4bt5sy</td>
      <td>all</td>
      <td>1.458877e+09</td>
      <td>[USA] [H] AC cards: 100 Walker, 152 Wendy, 180...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>self.amiiboSwap</td>
      <td>I'll take Agent S!</td>
    </tr>
    <tr>
      <th>42598</th>
      <td>Wendy's</td>
      <td>4bt5sy</td>
      <td>all</td>
      <td>1.458877e+09</td>
      <td>[USA] [H] AC cards: 100 Walker, 152 Wendy, 180...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>self.amiiboSwap</td>
      <td>Post is closed. All cards are accounted for. T...</td>
    </tr>
    <tr>
      <th>42606</th>
      <td>Wendy's</td>
      <td>r63de</td>
      <td>all</td>
      <td>1.332324e+09</td>
      <td>/r/news [removed] Wendy's overtakes Burger Kin...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>2</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>--- \n\n[Wendy&amp;#39;s overtakes Burger King as ...</td>
    </tr>
    <tr>
      <th>42607</th>
      <td>Wendy's</td>
      <td>r63de</td>
      <td>all</td>
      <td>1.332324e+09</td>
      <td>/r/news [removed] Wendy's overtakes Burger Kin...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>2</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>March 21, 2012 4:19 a.m. :\nThis post has re-a...</td>
    </tr>
    <tr>
      <th>42608</th>
      <td>Wendy's</td>
      <td>1qatlz</td>
      <td>all</td>
      <td>1.384107e+09</td>
      <td>So apparently the Wendy's girl did some some p...</td>
      <td>3</td>
      <td>http://www.reddit.com/r/gaming/comments/1qale8...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/gaming/comments/1qale8...</td>
      <td>reddit.com</td>
      <td>&gt;S&amp;P cosplay\n\nSpice and… Polf?</td>
    </tr>
    <tr>
      <th>42609</th>
      <td>Wendy's</td>
      <td>84rz2p</td>
      <td>all</td>
      <td>1.521194e+09</td>
      <td>J.S. Bach - Two Part Invention #1 (played in t...</td>
      <td>2</td>
      <td>https://www.youtube.com/watch?v=-9xqh_wUVHU</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=-9xqh_wUVHU</td>
      <td>youtube.com</td>
      <td>It looks like Wendy Carlos has gotten her musi...</td>
    </tr>
    <tr>
      <th>42611</th>
      <td>Wendy's</td>
      <td>44e877</td>
      <td>all</td>
      <td>1.454754e+09</td>
      <td>[TOMT][CARTOON TV SERIES] Late 90s-early 00's ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>self.tipofmytongue</td>
      <td>maybe the anime [The Adventures of Peter Pan](...</td>
    </tr>
    <tr>
      <th>42618</th>
      <td>Wendy's</td>
      <td>7sv4df</td>
      <td>all</td>
      <td>1.516903e+09</td>
      <td>Tiffany Wendy (aka Samantha Alexandra, Sam Ale...</td>
      <td>1</td>
      <td>https://www.nicsgalleries.com/g/46/67/02/9d372...</td>
      <td>1</td>
      <td>https://www.nicsgalleries.com/g/46/67/02/9d372...</td>
      <td>nicsgalleries.com</td>
      <td>**[Tiffany Wendy](https://www.nicsgalleries.co...</td>
    </tr>
    <tr>
      <th>42621</th>
      <td>Wendy's</td>
      <td>4z9s2r</td>
      <td>all</td>
      <td>1.472028e+09</td>
      <td>[TOMT][Video] I would like some help identifyi...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>self.tipofmytongue</td>
      <td>The video is actually from the early 90s. The ...</td>
    </tr>
    <tr>
      <th>42622</th>
      <td>Wendy's</td>
      <td>2cydz7</td>
      <td>all</td>
      <td>1.407504e+09</td>
      <td>Wendy's 80s training video (from /u/GiselleMon...</td>
      <td>1</td>
      <td>http://youtu.be/3xSyVjkSib4#r=/r/WoahTube/</td>
      <td>1</td>
      <td>http://youtu.be/3xSyVjkSib4#r=/r/WoahTube/</td>
      <td>youtu.be</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
    </tr>
    <tr>
      <th>42626</th>
      <td>Wendy's</td>
      <td>1tgjn0</td>
      <td>all</td>
      <td>1.387749e+09</td>
      <td>A little more than two months into her campaig...</td>
      <td>2</td>
      <td>http://www.huffingtonpost.com/2013/12/21/wendy...</td>
      <td>1</td>
      <td>http://www.huffingtonpost.com/2013/12/21/wendy...</td>
      <td>huffingtonpost.com</td>
      <td>[Original Submission at /r/politics](/r/politi...</td>
    </tr>
    <tr>
      <th>42628</th>
      <td>Wendy's</td>
      <td>51omu8</td>
      <td>all</td>
      <td>1.473324e+09</td>
      <td>Wendy's in Hanover, Pennsylvania, a 1990s-era ...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>flickr.com</td>
      <td>[Link To Original Submission](http://reddit.co...</td>
    </tr>
    <tr>
      <th>42630</th>
      <td>Wendy's</td>
      <td>2h7h11</td>
      <td>all</td>
      <td>1.411483e+09</td>
      <td>Dinesh D'Souza pleaded guilty in May to charge...</td>
      <td>1</td>
      <td>http://abcnews.go.com/US/wireStory/conservativ...</td>
      <td>1</td>
      <td>http://abcnews.go.com/US/wireStory/conservativ...</td>
      <td>abcnews.go.com</td>
      <td>[Original Submission at /r/progressive](/r/pro...</td>
    </tr>
    <tr>
      <th>42632</th>
      <td>Wendy's</td>
      <td>r4f59</td>
      <td>all</td>
      <td>1.332237e+09</td>
      <td>Wendy's overtakes Burger King as No. 2 U.S. bu...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>Pink slime burgers anyone? This was not intere...</td>
    </tr>
    <tr>
      <th>42634</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>&gt; Anyone else notice she whispered something i...</td>
    </tr>
    <tr>
      <th>42635</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>GFY</td>
    </tr>
    <tr>
      <th>42637</th>
      <td>Wendy's</td>
      <td>2ln7bd</td>
      <td>all</td>
      <td>1.415446e+09</td>
      <td>Democrats Ann Kirkpatrick and Kyrsten Sinema h...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>azcentral.com</td>
      <td>[Original Submission at /r/uspolitics](/r/uspo...</td>
    </tr>
    <tr>
      <th>42650</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>I don't think we need a key for Oryx Castle.</td>
    </tr>
    <tr>
      <th>42651</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>Key looks horrible (the pure black/white combi...</td>
    </tr>
    <tr>
      <th>42652</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>They key looks like a baby Oryx sitting on a c...</td>
    </tr>
    <tr>
      <th>42653</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>That's a big ass portal xD</td>
    </tr>
    <tr>
      <th>42669</th>
      <td>Wendy's</td>
      <td>r4reg</td>
      <td>all</td>
      <td>1.332254e+09</td>
      <td>/r/business [removed] Wendy's overtakes Burger...</td>
      <td>0</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>--- \n\n[Wendy&amp;#39;s overtakes Burger King as ...</td>
    </tr>
    <tr>
      <th>42689</th>
      <td>Wendy's</td>
      <td>51omuz</td>
      <td>all</td>
      <td>1.473324e+09</td>
      <td>[Retail] Wendy's in Hanover, Pennsylvania, a 1...</td>
      <td>0</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>flickr.com</td>
      <td>[RetailFans](https://www.reddit.com/r/RetailFa...</td>
    </tr>
    <tr>
      <th>42717</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>^(Hi, I'm a bot for linking direct images of a...</td>
    </tr>
    <tr>
      <th>42718</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>Troi wasn't as morally compromised :)</td>
    </tr>
    <tr>
      <th>42719</th>
      <td>Wendy's</td>
      <td>2e9nxq</td>
      <td>all</td>
      <td>1.408735e+09</td>
      <td>80s Wendy's Training Video - Part Deux, Cold D...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>youtube.com</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
    </tr>
  </tbody>
</table>
<p>41556 rows × 11 columns</p>
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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Now all the need is some queso!</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I think I'll go to Chipotles for dinner tonigh...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>WOW!\n\nGood food AND good treatment of employees</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Well, I guess I need to start going to Chipotl...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I do wonder if this will tempt certain investm...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>An employee that wants to be at work, and enjo...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>What's the catch?</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>could be the start of a new wave of corporate ...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will eat more burritos because of this!</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will stop coming if my burrito price increases.</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Working at chipotle as a non-salaried job is n...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Chipotle is run by anti gmo nuts. Maybe they s...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is great and all but I'm not looking forw...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Will this make the guacamole cheaper? I don't ...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Why would they not test this in Denver?</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chicago you need to help make this successful</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>As someone moving to Chicago in a few months, ...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chipotle, craft beer, and Chicago are 3 of my ...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Yay! And ten years from now we will have craft...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>60,000 bottles really isnt that much beer</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Holy shit I am so excited. I absolutely love C...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Three of my favorite things. Beer, Chicago, an...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>All right, now I can drink in a Chipotle!!!\n\...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Anyone know specifically which Chipotles will ...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Sweet, I work in downtown Chicago and go to ch...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>You know what they need to do is sell said bee...</td>
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
      <th>41526</th>
      <td>Wendy's</td>
      <td>tfgw6</td>
      <td>all</td>
      <td>1.336632e+09</td>
      <td>Wendy's 80s training video (Excessive amounts ...</td>
      <td>1</td>
      <td>http://www.youtube.com/watch?feature=player_em...</td>
      <td>2</td>
      <td>http://www.youtube.com/watch?feature=player_em...</td>
      <td>youtube.com</td>
      <td>Wendy's made better music and videos in the 80...</td>
    </tr>
    <tr>
      <th>41527</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>She claims to be an atheist, yet can't get thr...</td>
    </tr>
    <tr>
      <th>41528</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>she is a "fox news atheist" thats the only way...</td>
    </tr>
    <tr>
      <th>41529</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>[Who cares.](http://www.youtube.com/watch?v=1_...</td>
    </tr>
    <tr>
      <th>41530</th>
      <td>Wendy's</td>
      <td>4bt5sy</td>
      <td>all</td>
      <td>1.458877e+09</td>
      <td>[USA] [H] AC cards: 100 Walker, 152 Wendy, 180...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>self.amiiboSwap</td>
      <td>I'll take Agent S!</td>
    </tr>
    <tr>
      <th>41531</th>
      <td>Wendy's</td>
      <td>4bt5sy</td>
      <td>all</td>
      <td>1.458877e+09</td>
      <td>[USA] [H] AC cards: 100 Walker, 152 Wendy, 180...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>self.amiiboSwap</td>
      <td>Post is closed. All cards are accounted for. T...</td>
    </tr>
    <tr>
      <th>41532</th>
      <td>Wendy's</td>
      <td>r63de</td>
      <td>all</td>
      <td>1.332324e+09</td>
      <td>/r/news [removed] Wendy's overtakes Burger Kin...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>2</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>--- \n\n[Wendy&amp;#39;s overtakes Burger King as ...</td>
    </tr>
    <tr>
      <th>41533</th>
      <td>Wendy's</td>
      <td>r63de</td>
      <td>all</td>
      <td>1.332324e+09</td>
      <td>/r/news [removed] Wendy's overtakes Burger Kin...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>2</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>March 21, 2012 4:19 a.m. :\nThis post has re-a...</td>
    </tr>
    <tr>
      <th>41534</th>
      <td>Wendy's</td>
      <td>1qatlz</td>
      <td>all</td>
      <td>1.384107e+09</td>
      <td>So apparently the Wendy's girl did some some p...</td>
      <td>3</td>
      <td>http://www.reddit.com/r/gaming/comments/1qale8...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/gaming/comments/1qale8...</td>
      <td>reddit.com</td>
      <td>&gt;S&amp;P cosplay\n\nSpice and… Polf?</td>
    </tr>
    <tr>
      <th>41535</th>
      <td>Wendy's</td>
      <td>84rz2p</td>
      <td>all</td>
      <td>1.521194e+09</td>
      <td>J.S. Bach - Two Part Invention #1 (played in t...</td>
      <td>2</td>
      <td>https://www.youtube.com/watch?v=-9xqh_wUVHU</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=-9xqh_wUVHU</td>
      <td>youtube.com</td>
      <td>It looks like Wendy Carlos has gotten her musi...</td>
    </tr>
    <tr>
      <th>41536</th>
      <td>Wendy's</td>
      <td>44e877</td>
      <td>all</td>
      <td>1.454754e+09</td>
      <td>[TOMT][CARTOON TV SERIES] Late 90s-early 00's ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>self.tipofmytongue</td>
      <td>maybe the anime [The Adventures of Peter Pan](...</td>
    </tr>
    <tr>
      <th>41537</th>
      <td>Wendy's</td>
      <td>7sv4df</td>
      <td>all</td>
      <td>1.516903e+09</td>
      <td>Tiffany Wendy (aka Samantha Alexandra, Sam Ale...</td>
      <td>1</td>
      <td>https://www.nicsgalleries.com/g/46/67/02/9d372...</td>
      <td>1</td>
      <td>https://www.nicsgalleries.com/g/46/67/02/9d372...</td>
      <td>nicsgalleries.com</td>
      <td>**[Tiffany Wendy](https://www.nicsgalleries.co...</td>
    </tr>
    <tr>
      <th>41538</th>
      <td>Wendy's</td>
      <td>4z9s2r</td>
      <td>all</td>
      <td>1.472028e+09</td>
      <td>[TOMT][Video] I would like some help identifyi...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>self.tipofmytongue</td>
      <td>The video is actually from the early 90s. The ...</td>
    </tr>
    <tr>
      <th>41539</th>
      <td>Wendy's</td>
      <td>2cydz7</td>
      <td>all</td>
      <td>1.407504e+09</td>
      <td>Wendy's 80s training video (from /u/GiselleMon...</td>
      <td>1</td>
      <td>http://youtu.be/3xSyVjkSib4#r=/r/WoahTube/</td>
      <td>1</td>
      <td>http://youtu.be/3xSyVjkSib4#r=/r/WoahTube/</td>
      <td>youtu.be</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
    </tr>
    <tr>
      <th>41540</th>
      <td>Wendy's</td>
      <td>1tgjn0</td>
      <td>all</td>
      <td>1.387749e+09</td>
      <td>A little more than two months into her campaig...</td>
      <td>2</td>
      <td>http://www.huffingtonpost.com/2013/12/21/wendy...</td>
      <td>1</td>
      <td>http://www.huffingtonpost.com/2013/12/21/wendy...</td>
      <td>huffingtonpost.com</td>
      <td>[Original Submission at /r/politics](/r/politi...</td>
    </tr>
    <tr>
      <th>41541</th>
      <td>Wendy's</td>
      <td>51omu8</td>
      <td>all</td>
      <td>1.473324e+09</td>
      <td>Wendy's in Hanover, Pennsylvania, a 1990s-era ...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>flickr.com</td>
      <td>[Link To Original Submission](http://reddit.co...</td>
    </tr>
    <tr>
      <th>41542</th>
      <td>Wendy's</td>
      <td>2h7h11</td>
      <td>all</td>
      <td>1.411483e+09</td>
      <td>Dinesh D'Souza pleaded guilty in May to charge...</td>
      <td>1</td>
      <td>http://abcnews.go.com/US/wireStory/conservativ...</td>
      <td>1</td>
      <td>http://abcnews.go.com/US/wireStory/conservativ...</td>
      <td>abcnews.go.com</td>
      <td>[Original Submission at /r/progressive](/r/pro...</td>
    </tr>
    <tr>
      <th>41543</th>
      <td>Wendy's</td>
      <td>r4f59</td>
      <td>all</td>
      <td>1.332237e+09</td>
      <td>Wendy's overtakes Burger King as No. 2 U.S. bu...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>Pink slime burgers anyone? This was not intere...</td>
    </tr>
    <tr>
      <th>41544</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>&gt; Anyone else notice she whispered something i...</td>
    </tr>
    <tr>
      <th>41545</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>GFY</td>
    </tr>
    <tr>
      <th>41546</th>
      <td>Wendy's</td>
      <td>2ln7bd</td>
      <td>all</td>
      <td>1.415446e+09</td>
      <td>Democrats Ann Kirkpatrick and Kyrsten Sinema h...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>azcentral.com</td>
      <td>[Original Submission at /r/uspolitics](/r/uspo...</td>
    </tr>
    <tr>
      <th>41547</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>I don't think we need a key for Oryx Castle.</td>
    </tr>
    <tr>
      <th>41548</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>Key looks horrible (the pure black/white combi...</td>
    </tr>
    <tr>
      <th>41549</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>They key looks like a baby Oryx sitting on a c...</td>
    </tr>
    <tr>
      <th>41550</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>That's a big ass portal xD</td>
    </tr>
    <tr>
      <th>41551</th>
      <td>Wendy's</td>
      <td>r4reg</td>
      <td>all</td>
      <td>1.332254e+09</td>
      <td>/r/business [removed] Wendy's overtakes Burger...</td>
      <td>0</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>--- \n\n[Wendy&amp;#39;s overtakes Burger King as ...</td>
    </tr>
    <tr>
      <th>41552</th>
      <td>Wendy's</td>
      <td>51omuz</td>
      <td>all</td>
      <td>1.473324e+09</td>
      <td>[Retail] Wendy's in Hanover, Pennsylvania, a 1...</td>
      <td>0</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>flickr.com</td>
      <td>[RetailFans](https://www.reddit.com/r/RetailFa...</td>
    </tr>
    <tr>
      <th>41553</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>^(Hi, I'm a bot for linking direct images of a...</td>
    </tr>
    <tr>
      <th>41554</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>Troi wasn't as morally compromised :)</td>
    </tr>
    <tr>
      <th>41555</th>
      <td>Wendy's</td>
      <td>2e9nxq</td>
      <td>all</td>
      <td>1.408735e+09</td>
      <td>80s Wendy's Training Video - Part Deux, Cold D...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>youtube.com</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
    </tr>
  </tbody>
</table>
<p>41556 rows × 11 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 41556 entries, 0 to 41555
    Data columns (total 11 columns):
    Keyword                      41556 non-null object
    Submission ID                41556 non-null object
    Subreddit                    41556 non-null object
    Created Date                 41556 non-null float64
    Submission Title             41556 non-null object
    Submission Score             41556 non-null int64
    Submission URL               41556 non-null object
    Total Submission Comments    41556 non-null int64
    Submission URL               41556 non-null object
    Domain                       41556 non-null object
    Submission Comments          41556 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 3.5+ MB



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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>0.4767</td>
      <td>0.045</td>
      <td>0.031</td>
      <td>0.924</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
      <td>0.9829</td>
      <td>0.362</td>
      <td>0.033</td>
      <td>0.605</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Now all the need is some queso!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I think I'll go to Chipotles for dinner tonigh...</td>
      <td>0.4588</td>
      <td>0.200</td>
      <td>0.000</td>
      <td>0.800</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>WOW!\n\nGood food AND good treatment of employees</td>
      <td>0.8916</td>
      <td>0.680</td>
      <td>0.000</td>
      <td>0.320</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Well, I guess I need to start going to Chipotl...</td>
      <td>-0.5508</td>
      <td>0.118</td>
      <td>0.262</td>
      <td>0.620</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I do wonder if this will tempt certain investm...</td>
      <td>0.9017</td>
      <td>0.236</td>
      <td>0.036</td>
      <td>0.728</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>An employee that wants to be at work, and enjo...</td>
      <td>0.9022</td>
      <td>0.268</td>
      <td>0.000</td>
      <td>0.732</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>What's the catch?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>could be the start of a new wave of corporate ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will eat more burritos because of this!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I will stop coming if my burrito price increases.</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.239</td>
      <td>0.761</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Working at chipotle as a non-salaried job is n...</td>
      <td>-0.7910</td>
      <td>0.102</td>
      <td>0.155</td>
      <td>0.743</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Chipotle is run by anti gmo nuts. Maybe they s...</td>
      <td>-0.5574</td>
      <td>0.000</td>
      <td>0.213</td>
      <td>0.787</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is great and all but I'm not looking forw...</td>
      <td>0.6858</td>
      <td>0.335</td>
      <td>0.136</td>
      <td>0.529</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Will this make the guacamole cheaper? I don't ...</td>
      <td>-0.0844</td>
      <td>0.115</td>
      <td>0.132</td>
      <td>0.753</td>
      <td>2015-06-07 22:51:17</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Why would they not test this in Denver?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chicago you need to help make this successful</td>
      <td>0.7579</td>
      <td>0.520</td>
      <td>0.000</td>
      <td>0.480</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>As someone moving to Chicago in a few months, ...</td>
      <td>0.7430</td>
      <td>0.364</td>
      <td>0.000</td>
      <td>0.636</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Chipotle, craft beer, and Chicago are 3 of my ...</td>
      <td>0.6705</td>
      <td>0.256</td>
      <td>0.000</td>
      <td>0.744</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Yay! And ten years from now we will have craft...</td>
      <td>0.6103</td>
      <td>0.235</td>
      <td>0.000</td>
      <td>0.765</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>60,000 bottles really isnt that much beer</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Holy shit I am so excited. I absolutely love C...</td>
      <td>0.8432</td>
      <td>0.348</td>
      <td>0.070</td>
      <td>0.581</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Three of my favorite things. Beer, Chicago, an...</td>
      <td>0.4588</td>
      <td>0.273</td>
      <td>0.000</td>
      <td>0.727</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>All right, now I can drink in a Chipotle!!!\n\...</td>
      <td>0.2905</td>
      <td>0.127</td>
      <td>0.000</td>
      <td>0.873</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Anyone know specifically which Chipotles will ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>Sweet, I work in downtown Chicago and go to ch...</td>
      <td>0.4588</td>
      <td>0.214</td>
      <td>0.000</td>
      <td>0.786</td>
      <td>2012-11-05 03:14:58</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>all</td>
      <td>1.352085e+09</td>
      <td>Chipotle Mexican Grill to Test Craft Beer in C...</td>
      <td>575</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>74</td>
      <td>http://www.thedailymeal.com/chipotle-testing-c...</td>
      <td>thedailymeal.com</td>
      <td>You know what they need to do is sell said bee...</td>
      <td>-0.6194</td>
      <td>0.000</td>
      <td>0.112</td>
      <td>0.888</td>
      <td>2012-11-05 03:14:58</td>
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
      <th>41526</th>
      <td>Wendy's</td>
      <td>tfgw6</td>
      <td>all</td>
      <td>1.336632e+09</td>
      <td>Wendy's 80s training video (Excessive amounts ...</td>
      <td>1</td>
      <td>http://www.youtube.com/watch?feature=player_em...</td>
      <td>2</td>
      <td>http://www.youtube.com/watch?feature=player_em...</td>
      <td>youtube.com</td>
      <td>Wendy's made better music and videos in the 80...</td>
      <td>0.4404</td>
      <td>0.162</td>
      <td>0.000</td>
      <td>0.838</td>
      <td>2012-05-10 06:39:56</td>
    </tr>
    <tr>
      <th>41527</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>She claims to be an atheist, yet can't get thr...</td>
      <td>-0.3612</td>
      <td>0.040</td>
      <td>0.074</td>
      <td>0.886</td>
      <td>2013-06-27 23:27:52</td>
    </tr>
    <tr>
      <th>41528</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>she is a "fox news atheist" thats the only way...</td>
      <td>0.0387</td>
      <td>0.102</td>
      <td>0.066</td>
      <td>0.832</td>
      <td>2013-06-27 23:27:52</td>
    </tr>
    <tr>
      <th>41529</th>
      <td>Wendy's</td>
      <td>1h6lil</td>
      <td>all</td>
      <td>1.372376e+09</td>
      <td>Get ready to rage » S.E. Cupp (conservative at...</td>
      <td>0</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>8</td>
      <td>http://www.rawstory.com/rs/2013/06/26/s-e-cupp...</td>
      <td>rawstory.com</td>
      <td>[Who cares.](http://www.youtube.com/watch?v=1_...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2013-06-27 23:27:52</td>
    </tr>
    <tr>
      <th>41530</th>
      <td>Wendy's</td>
      <td>4bt5sy</td>
      <td>all</td>
      <td>1.458877e+09</td>
      <td>[USA] [H] AC cards: 100 Walker, 152 Wendy, 180...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>self.amiiboSwap</td>
      <td>I'll take Agent S!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-03-25 03:38:00</td>
    </tr>
    <tr>
      <th>41531</th>
      <td>Wendy's</td>
      <td>4bt5sy</td>
      <td>all</td>
      <td>1.458877e+09</td>
      <td>[USA] [H] AC cards: 100 Walker, 152 Wendy, 180...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/amiiboSwap/comments/4...</td>
      <td>self.amiiboSwap</td>
      <td>Post is closed. All cards are accounted for. T...</td>
      <td>0.4926</td>
      <td>0.285</td>
      <td>0.000</td>
      <td>0.715</td>
      <td>2016-03-25 03:38:00</td>
    </tr>
    <tr>
      <th>41532</th>
      <td>Wendy's</td>
      <td>r63de</td>
      <td>all</td>
      <td>1.332324e+09</td>
      <td>/r/news [removed] Wendy's overtakes Burger Kin...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>2</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>--- \n\n[Wendy&amp;#39;s overtakes Burger King as ...</td>
      <td>-0.4479</td>
      <td>0.032</td>
      <td>0.078</td>
      <td>0.890</td>
      <td>2012-03-21 10:04:46</td>
    </tr>
    <tr>
      <th>41533</th>
      <td>Wendy's</td>
      <td>r63de</td>
      <td>all</td>
      <td>1.332324e+09</td>
      <td>/r/news [removed] Wendy's overtakes Burger Kin...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>2</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>March 21, 2012 4:19 a.m. :\nThis post has re-a...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2012-03-21 10:04:46</td>
    </tr>
    <tr>
      <th>41534</th>
      <td>Wendy's</td>
      <td>1qatlz</td>
      <td>all</td>
      <td>1.384107e+09</td>
      <td>So apparently the Wendy's girl did some some p...</td>
      <td>3</td>
      <td>http://www.reddit.com/r/gaming/comments/1qale8...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/gaming/comments/1qale8...</td>
      <td>reddit.com</td>
      <td>&gt;S&amp;P cosplay\n\nSpice and… Polf?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2013-11-10 18:14:58</td>
    </tr>
    <tr>
      <th>41535</th>
      <td>Wendy's</td>
      <td>84rz2p</td>
      <td>all</td>
      <td>1.521194e+09</td>
      <td>J.S. Bach - Two Part Invention #1 (played in t...</td>
      <td>2</td>
      <td>https://www.youtube.com/watch?v=-9xqh_wUVHU</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=-9xqh_wUVHU</td>
      <td>youtube.com</td>
      <td>It looks like Wendy Carlos has gotten her musi...</td>
      <td>0.9118</td>
      <td>0.142</td>
      <td>0.000</td>
      <td>0.858</td>
      <td>2018-03-16 09:53:37</td>
    </tr>
    <tr>
      <th>41536</th>
      <td>Wendy's</td>
      <td>44e877</td>
      <td>all</td>
      <td>1.454754e+09</td>
      <td>[TOMT][CARTOON TV SERIES] Late 90s-early 00's ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>self.tipofmytongue</td>
      <td>maybe the anime [The Adventures of Peter Pan](...</td>
      <td>0.4137</td>
      <td>0.283</td>
      <td>0.000</td>
      <td>0.717</td>
      <td>2016-02-06 10:25:16</td>
    </tr>
    <tr>
      <th>41537</th>
      <td>Wendy's</td>
      <td>7sv4df</td>
      <td>all</td>
      <td>1.516903e+09</td>
      <td>Tiffany Wendy (aka Samantha Alexandra, Sam Ale...</td>
      <td>1</td>
      <td>https://www.nicsgalleries.com/g/46/67/02/9d372...</td>
      <td>1</td>
      <td>https://www.nicsgalleries.com/g/46/67/02/9d372...</td>
      <td>nicsgalleries.com</td>
      <td>**[Tiffany Wendy](https://www.nicsgalleries.co...</td>
      <td>0.9360</td>
      <td>0.186</td>
      <td>0.000</td>
      <td>0.814</td>
      <td>2018-01-25 18:04:45</td>
    </tr>
    <tr>
      <th>41538</th>
      <td>Wendy's</td>
      <td>4z9s2r</td>
      <td>all</td>
      <td>1.472028e+09</td>
      <td>[TOMT][Video] I would like some help identifyi...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/tipofmytongue/comment...</td>
      <td>self.tipofmytongue</td>
      <td>The video is actually from the early 90s. The ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-08-24 08:38:13</td>
    </tr>
    <tr>
      <th>41539</th>
      <td>Wendy's</td>
      <td>2cydz7</td>
      <td>all</td>
      <td>1.407504e+09</td>
      <td>Wendy's 80s training video (from /u/GiselleMon...</td>
      <td>1</td>
      <td>http://youtu.be/3xSyVjkSib4#r=/r/WoahTube/</td>
      <td>1</td>
      <td>http://youtu.be/3xSyVjkSib4#r=/r/WoahTube/</td>
      <td>youtu.be</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
      <td>0.2023</td>
      <td>0.122</td>
      <td>0.000</td>
      <td>0.878</td>
      <td>2014-08-08 13:13:35</td>
    </tr>
    <tr>
      <th>41540</th>
      <td>Wendy's</td>
      <td>1tgjn0</td>
      <td>all</td>
      <td>1.387749e+09</td>
      <td>A little more than two months into her campaig...</td>
      <td>2</td>
      <td>http://www.huffingtonpost.com/2013/12/21/wendy...</td>
      <td>1</td>
      <td>http://www.huffingtonpost.com/2013/12/21/wendy...</td>
      <td>huffingtonpost.com</td>
      <td>[Original Submission at /r/politics](/r/politi...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2013-12-22 21:43:05</td>
    </tr>
    <tr>
      <th>41541</th>
      <td>Wendy's</td>
      <td>51omu8</td>
      <td>all</td>
      <td>1.473324e+09</td>
      <td>Wendy's in Hanover, Pennsylvania, a 1990s-era ...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>flickr.com</td>
      <td>[Link To Original Submission](http://reddit.co...</td>
      <td>0.3182</td>
      <td>0.113</td>
      <td>0.000</td>
      <td>0.887</td>
      <td>2016-09-08 08:47:28</td>
    </tr>
    <tr>
      <th>41542</th>
      <td>Wendy's</td>
      <td>2h7h11</td>
      <td>all</td>
      <td>1.411483e+09</td>
      <td>Dinesh D'Souza pleaded guilty in May to charge...</td>
      <td>1</td>
      <td>http://abcnews.go.com/US/wireStory/conservativ...</td>
      <td>1</td>
      <td>http://abcnews.go.com/US/wireStory/conservativ...</td>
      <td>abcnews.go.com</td>
      <td>[Original Submission at /r/progressive](/r/pro...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2014-09-23 14:38:50</td>
    </tr>
    <tr>
      <th>41543</th>
      <td>Wendy's</td>
      <td>r4f59</td>
      <td>all</td>
      <td>1.332237e+09</td>
      <td>Wendy's overtakes Burger King as No. 2 U.S. bu...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>Pink slime burgers anyone? This was not intere...</td>
      <td>-0.3089</td>
      <td>0.000</td>
      <td>0.101</td>
      <td>0.899</td>
      <td>2012-03-20 09:51:39</td>
    </tr>
    <tr>
      <th>41544</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>&gt; Anyone else notice she whispered something i...</td>
      <td>0.4222</td>
      <td>0.081</td>
      <td>0.000</td>
      <td>0.919</td>
      <td>2017-05-09 01:03:03</td>
    </tr>
    <tr>
      <th>41545</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>GFY</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017-05-09 01:03:03</td>
    </tr>
    <tr>
      <th>41546</th>
      <td>Wendy's</td>
      <td>2ln7bd</td>
      <td>all</td>
      <td>1.415446e+09</td>
      <td>Democrats Ann Kirkpatrick and Kyrsten Sinema h...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>1</td>
      <td>http://www.azcentral.com/story/news/arizona/po...</td>
      <td>azcentral.com</td>
      <td>[Original Submission at /r/uspolitics](/r/uspo...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2014-11-08 11:29:22</td>
    </tr>
    <tr>
      <th>41547</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>I don't think we need a key for Oryx Castle.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2014-05-09 12:29:29</td>
    </tr>
    <tr>
      <th>41548</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>Key looks horrible (the pure black/white combi...</td>
      <td>0.3818</td>
      <td>0.193</td>
      <td>0.111</td>
      <td>0.696</td>
      <td>2014-05-09 12:29:29</td>
    </tr>
    <tr>
      <th>41549</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>They key looks like a baby Oryx sitting on a c...</td>
      <td>0.3612</td>
      <td>0.217</td>
      <td>0.000</td>
      <td>0.783</td>
      <td>2014-05-09 12:29:29</td>
    </tr>
    <tr>
      <th>41550</th>
      <td>Wendy's</td>
      <td>253rgm</td>
      <td>all</td>
      <td>1.399639e+09</td>
      <td>I was inspired by the Oryx portal created by /...</td>
      <td>0</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>5</td>
      <td>http://imgur.com/a/sKKdy</td>
      <td>imgur.com</td>
      <td>That's a big ass portal xD</td>
      <td>0.0772</td>
      <td>0.369</td>
      <td>0.340</td>
      <td>0.291</td>
      <td>2014-05-09 12:29:29</td>
    </tr>
    <tr>
      <th>41551</th>
      <td>Wendy's</td>
      <td>r4reg</td>
      <td>all</td>
      <td>1.332254e+09</td>
      <td>/r/business [removed] Wendy's overtakes Burger...</td>
      <td>0</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>1</td>
      <td>http://money.cnn.com/2012/03/19/news/companies...</td>
      <td>money.cnn.com</td>
      <td>--- \n\n[Wendy&amp;#39;s overtakes Burger King as ...</td>
      <td>-0.5204</td>
      <td>0.034</td>
      <td>0.090</td>
      <td>0.876</td>
      <td>2012-03-20 14:27:21</td>
    </tr>
    <tr>
      <th>41552</th>
      <td>Wendy's</td>
      <td>51omuz</td>
      <td>all</td>
      <td>1.473324e+09</td>
      <td>[Retail] Wendy's in Hanover, Pennsylvania, a 1...</td>
      <td>0</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>1</td>
      <td>https://www.flickr.com/photos/schuminweb/29239...</td>
      <td>flickr.com</td>
      <td>[RetailFans](https://www.reddit.com/r/RetailFa...</td>
      <td>0.3182</td>
      <td>0.108</td>
      <td>0.000</td>
      <td>0.892</td>
      <td>2016-09-08 08:47:36</td>
    </tr>
    <tr>
      <th>41553</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>^(Hi, I'm a bot for linking direct images of a...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2018-02-27 05:06:34</td>
    </tr>
    <tr>
      <th>41554</th>
      <td>Wendy's</td>
      <td>80giap</td>
      <td>all</td>
      <td>1.519708e+09</td>
      <td>Wendy Rhoades = Deanna Troi? S01E09</td>
      <td>0</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>2</td>
      <td>https://imgur.com/a/YlVzj</td>
      <td>imgur.com</td>
      <td>Troi wasn't as morally compromised :)</td>
      <td>0.4588</td>
      <td>0.375</td>
      <td>0.000</td>
      <td>0.625</td>
      <td>2018-02-27 05:06:34</td>
    </tr>
    <tr>
      <th>41555</th>
      <td>Wendy's</td>
      <td>2e9nxq</td>
      <td>all</td>
      <td>1.408735e+09</td>
      <td>80s Wendy's Training Video - Part Deux, Cold D...</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=PJ-JBFXh2IU#r=...</td>
      <td>youtube.com</td>
      <td>From the top /r/WoahTube posts for this week. ...</td>
      <td>0.2023</td>
      <td>0.122</td>
      <td>0.000</td>
      <td>0.878</td>
      <td>2014-08-22 19:13:33</td>
    </tr>
  </tbody>
</table>
<p>41556 rows × 16 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 41556 entries, 0 to 41555
    Data columns (total 16 columns):
    Keyword                      41556 non-null object
    Submission ID                41556 non-null object
    Subreddit                    41556 non-null object
    Created Date                 41556 non-null float64
    Submission Title             41556 non-null object
    Submission Score             41556 non-null int64
    Submission URL               41556 non-null object
    Total Submission Comments    41556 non-null int64
    Submission URL               41556 non-null object
    Domain                       41556 non-null object
    Submission Comments          41556 non-null object
    Compound Score               41556 non-null float64
    Positive Score               41556 non-null float64
    Negative Score               41556 non-null float64
    Neutral Score                41556 non-null float64
    Date                         41556 non-null datetime64[ns]
    dtypes: datetime64[ns](1), float64(5), int64(2), object(8)
    memory usage: 5.1+ MB



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
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>I'm reading this on my way to Chipotle. I gues...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>0.4767</td>
      <td>0.045</td>
      <td>0.031</td>
      <td>0.924</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>So if I get a part time job making burritos th...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>This is GREAT. I am often one of the oldest cu...</td>
      <td>0.9829</td>
      <td>0.362</td>
      <td>0.033</td>
      <td>0.605</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>38wus9</td>
      <td>all</td>
      <td>1.433717e+09</td>
      <td>"Chipotle Mexican Grill Inc. will expand benef...</td>
      <td>1350</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>105</td>
      <td>http://nrn.com/hr-training/chipotle-expand-ben...</td>
      <td>nrn.com</td>
      <td>Now all the need is some queso!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.to_csv("top5_kws.csv",
                     encoding="utf-8", index=False)
```


```python
reddit_comments_df['Date'].value_counts()
```




    2017    7217
    2012    5878
    2014    5640
    2015    5523
    2013    5485
    2016    4521
    2018    3393
    2011    3090
    2010     736
    2009      69
    2008       4
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
      <th rowspan="5" valign="top">Chipotle Mexican Grill</th>
      <th>10g2tj</th>
      <th>1.348605e+09</th>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10xzgu</th>
      <th>1.349398e+09</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>12mgrv</th>
      <th>1.352085e+09</th>
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
      <th>19vdl1</th>
      <th>1.362722e+09</th>
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
      <th>1akwu1</th>
      <th>1.363705e+09</th>
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
      <th rowspan="30" valign="top">Chipotle Mexican Grill</th>
      <th>10g2tj</th>
      <th>1.348605e+09</th>
      <td>0.119775</td>
    </tr>
    <tr>
      <th>10xzgu</th>
      <th>1.349398e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>12mgrv</th>
      <th>1.352085e+09</th>
      <td>0.253828</td>
    </tr>
    <tr>
      <th>19vdl1</th>
      <th>1.362722e+09</th>
      <td>0.113458</td>
    </tr>
    <tr>
      <th>1akwu1</th>
      <th>1.363705e+09</th>
      <td>0.354600</td>
    </tr>
    <tr>
      <th>1am70w</th>
      <th>1.363754e+09</th>
      <td>-0.779500</td>
    </tr>
    <tr>
      <th>1cq65r</th>
      <th>1.366464e+09</th>
      <td>0.394433</td>
    </tr>
    <tr>
      <th>1dr7fi</th>
      <th>1.367822e+09</th>
      <td>0.329100</td>
    </tr>
    <tr>
      <th>1eh6kf</th>
      <th>1.368769e+09</th>
      <td>0.260370</td>
    </tr>
    <tr>
      <th>1fozju</th>
      <th>1.370426e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1ie563</th>
      <th>1.373978e+09</th>
      <td>0.515275</td>
    </tr>
    <tr>
      <th>1kayy5</th>
      <th>1.376457e+09</th>
      <td>0.359633</td>
    </tr>
    <tr>
      <th>1ldhug</th>
      <th>1.377858e+09</th>
      <td>0.051100</td>
    </tr>
    <tr>
      <th>1ot86p</th>
      <th>1.382262e+09</th>
      <td>-0.421500</td>
    </tr>
    <tr>
      <th>1q5r3i</th>
      <th>1.383918e+09</th>
      <td>0.397550</td>
    </tr>
    <tr>
      <th>1qgxqd</th>
      <th>1.384308e+09</th>
      <td>0.159100</td>
    </tr>
    <tr>
      <th>1tal65</th>
      <th>1.387533e+09</th>
      <td>0.637800</td>
    </tr>
    <tr>
      <th>2352wd</th>
      <th>1.397637e+09</th>
      <td>0.318200</td>
    </tr>
    <tr>
      <th>2354qb</th>
      <th>1.397638e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>23l51l</th>
      <th>1.398114e+09</th>
      <td>0.082050</td>
    </tr>
    <tr>
      <th>24ofcd</th>
      <th>1.399214e+09</th>
      <td>0.226300</td>
    </tr>
    <tr>
      <th>2apego</th>
      <th>1.405403e+09</th>
      <td>0.361200</td>
    </tr>
    <tr>
      <th>2bpbkz</th>
      <th>1.406334e+09</th>
      <td>0.233125</td>
    </tr>
    <tr>
      <th>2i623r</th>
      <th>1.412347e+09</th>
      <td>0.239231</td>
    </tr>
    <tr>
      <th>2k17sa</th>
      <th>1.414042e+09</th>
      <td>0.401900</td>
    </tr>
    <tr>
      <th>2nub9b</th>
      <th>1.417382e+09</th>
      <td>-0.039275</td>
    </tr>
    <tr>
      <th>2rqyqx</th>
      <th>1.420759e+09</th>
      <td>0.236680</td>
    </tr>
    <tr>
      <th>2tfu3j</th>
      <th>1.422074e+09</th>
      <td>0.167564</td>
    </tr>
    <tr>
      <th>340rav</th>
      <th>1.430164e+09</th>
      <td>0.380400</td>
    </tr>
    <tr>
      <th>37lrok</th>
      <th>1.432856e+09</th>
      <td>-0.002400</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="30" valign="top">Wendy's</th>
      <th>7eaibv</th>
      <th>1.511228e+09</th>
      <td>0.113000</td>
    </tr>
    <tr>
      <th>7i4sat</th>
      <th>1.512660e+09</th>
      <td>0.421600</td>
    </tr>
    <tr>
      <th>7lwjpx</th>
      <th>1.514168e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>7obvpb</th>
      <th>1.515195e+09</th>
      <td>0.079700</td>
    </tr>
    <tr>
      <th>7s43fb</th>
      <th>1.516633e+09</th>
      <td>0.196033</td>
    </tr>
    <tr>
      <th>7sv4df</th>
      <th>1.516903e+09</th>
      <td>0.936000</td>
    </tr>
    <tr>
      <th>7tafbe</th>
      <th>1.517057e+09</th>
      <td>0.187833</td>
    </tr>
    <tr>
      <th>7vi4ma</th>
      <th>1.517895e+09</th>
      <td>-0.133967</td>
    </tr>
    <tr>
      <th>7wwwz8</th>
      <th>1.518424e+09</th>
      <td>0.267100</td>
    </tr>
    <tr>
      <th>80e8h4</th>
      <th>1.519691e+09</th>
      <td>0.294400</td>
    </tr>
    <tr>
      <th>80giap</th>
      <th>1.519708e+09</th>
      <td>0.229400</td>
    </tr>
    <tr>
      <th>80m6i8</th>
      <th>1.519765e+09</th>
      <td>0.226300</td>
    </tr>
    <tr>
      <th>81g48m</th>
      <th>1.520042e+09</th>
      <td>0.789600</td>
    </tr>
    <tr>
      <th>81kjsg</th>
      <th>1.520066e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>82idw0</th>
      <th>1.520398e+09</th>
      <td>0.580725</td>
    </tr>
    <tr>
      <th>83w71i</th>
      <th>1.520900e+09</th>
      <td>0.090636</td>
    </tr>
    <tr>
      <th>84rz2p</th>
      <th>1.521194e+09</th>
      <td>0.911800</td>
    </tr>
    <tr>
      <th>86v843</th>
      <th>1.521947e+09</th>
      <td>-0.177775</td>
    </tr>
    <tr>
      <th>ee9tj</th>
      <th>1.291202e+09</th>
      <td>0.321700</td>
    </tr>
    <tr>
      <th>hk0sz</th>
      <th>1.306380e+09</th>
      <td>-0.238350</td>
    </tr>
    <tr>
      <th>il9ij</th>
      <th>1.310287e+09</th>
      <td>-0.135800</td>
    </tr>
    <tr>
      <th>lr1k9</th>
      <th>1.319759e+09</th>
      <td>0.563500</td>
    </tr>
    <tr>
      <th>r4f59</th>
      <th>1.332237e+09</th>
      <td>-0.308900</td>
    </tr>
    <tr>
      <th>r4reg</th>
      <th>1.332254e+09</th>
      <td>-0.520400</td>
    </tr>
    <tr>
      <th>r5zdk</th>
      <th>1.332320e+09</th>
      <td>-0.546750</td>
    </tr>
    <tr>
      <th>r63de</th>
      <th>1.332324e+09</th>
      <td>-0.223950</td>
    </tr>
    <tr>
      <th>r9i5m</th>
      <th>1.332504e+09</th>
      <td>-0.037350</td>
    </tr>
    <tr>
      <th>tfgw6</th>
      <th>1.336632e+09</th>
      <td>0.140000</td>
    </tr>
    <tr>
      <th>wklw6</th>
      <th>1.342342e+09</th>
      <td>0.093633</td>
    </tr>
    <tr>
      <th>yoisy</th>
      <th>1.345727e+09</th>
      <td>0.824400</td>
    </tr>
  </tbody>
</table>
<p>1476 rows × 1 columns</p>
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
      <td>Chipotle Mexican Grill</td>
      <td>10g2tj</td>
      <td>1.348605e+09</td>
      <td>0.119775</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>10xzgu</td>
      <td>1.349398e+09</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>12mgrv</td>
      <td>1.352085e+09</td>
      <td>0.253828</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>19vdl1</td>
      <td>1.362722e+09</td>
      <td>0.113458</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>1akwu1</td>
      <td>1.363705e+09</td>
      <td>0.354600</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
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

plt.savefig("Restaurant_Sentiments_top5all.png", dpi=350)

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
      <th>36</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>wonder what % of people on this sub just make ...</td>
      <td>0.3612</td>
      <td>0.127</td>
      <td>0.000</td>
      <td>0.873</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Did we not learn from United?  2 to 3 days of ...</td>
      <td>-0.3252</td>
      <td>0.000</td>
      <td>0.143</td>
      <td>0.857</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>They announced the attack during their earning...</td>
      <td>-0.6597</td>
      <td>0.000</td>
      <td>0.265</td>
      <td>0.735</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Bold strategy Cotton.</td>
      <td>0.3818</td>
      <td>0.565</td>
      <td>0.000</td>
      <td>0.435</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>my own fucking chipotle and I go there twice a...</td>
      <td>-0.7893</td>
      <td>0.000</td>
      <td>0.291</td>
      <td>0.709</td>
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
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>wonder what % of people on this sub just make ...</td>
      <td>0.3612</td>
      <td>0.127</td>
      <td>0.000</td>
      <td>0.873</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Did we not learn from United?  2 to 3 days of ...</td>
      <td>-0.3252</td>
      <td>0.000</td>
      <td>0.143</td>
      <td>0.857</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>They announced the attack during their earning...</td>
      <td>-0.6597</td>
      <td>0.000</td>
      <td>0.265</td>
      <td>0.735</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Bold strategy Cotton.</td>
      <td>0.3818</td>
      <td>0.565</td>
      <td>0.000</td>
      <td>0.435</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>my own fucking chipotle and I go there twice a...</td>
      <td>-0.7893</td>
      <td>0.000</td>
      <td>0.291</td>
      <td>0.709</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Inverse WSB I'm going long CMG w/ P.O. of 520.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Hey, if I hypothetically just ate a chipotle, ...</td>
      <td>0.4939</td>
      <td>0.151</td>
      <td>0.000</td>
      <td>0.849</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>I wonder who at Chipotle approved the use of "...</td>
      <td>0.4215</td>
      <td>0.091</td>
      <td>0.000</td>
      <td>0.909</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Those people claiming this is already priced i...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>priced in</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Doesn't that mean that they are more secure fr...</td>
      <td>-0.6083</td>
      <td>0.158</td>
      <td>0.176</td>
      <td>0.666</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Good luck with that shit.</td>
      <td>0.3182</td>
      <td>0.513</td>
      <td>0.313</td>
      <td>0.174</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>I just ate there yesterday...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Faggot</td>
      <td>-0.6597</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>I used to alternate locations b/c even the emp...</td>
      <td>0.6712</td>
      <td>0.155</td>
      <td>0.000</td>
      <td>0.845</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>All about those technicals baby. Opportunity t...</td>
      <td>0.4215</td>
      <td>0.286</td>
      <td>0.000</td>
      <td>0.714</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>My co worker had 3 cards skimmed at the same s...</td>
      <td>0.4902</td>
      <td>0.117</td>
      <td>0.000</td>
      <td>0.883</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>This isn't going to do anything to the stock...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle Mexican Grill</td>
      <td>6dtzc2</td>
      <td>all</td>
      <td>1.496010e+09</td>
      <td>Almost ALL Chipotle Mexican Grill were infecte...</td>
      <td>345</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>55</td>
      <td>https://www.theverge.com/2017/5/26/15701776/ch...</td>
      <td>theverge.com</td>
      <td>Anyone that knows how CMG trades know that thi...</td>
      <td>0.4404</td>
      <td>0.121</td>
      <td>0.000</td>
      <td>0.879</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>Ingredients:\n\n2.5 oz package of dried ancho ...</td>
      <td>0.3182</td>
      <td>0.016</td>
      <td>0.000</td>
      <td>0.984</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>One of the things I love about meal prepping i...</td>
      <td>0.7901</td>
      <td>0.179</td>
      <td>0.000</td>
      <td>0.821</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>*has immediate craving for burritos*</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>Love the video! Definitely subscribing, lots o...</td>
      <td>0.8772</td>
      <td>0.502</td>
      <td>0.000</td>
      <td>0.498</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>Thanks for posting. What kind of stovetop pan ...</td>
      <td>0.4926</td>
      <td>0.186</td>
      <td>0.000</td>
      <td>0.814</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>My ancho chiles are soaking right now\n\ngonna...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>all</td>
      <td>1.488062e+09</td>
      <td>Chipotle Mexican Grill - Chicken Burritos (rec...</td>
      <td>217</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>26</td>
      <td>https://www.youtube.com/watch?v=1OoZwOofEHE</td>
      <td>youtube.com</td>
      <td>Those knife skill though,</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle Mexican Grill</td>
      <td>5pziaj</td>
      <td>all</td>
      <td>1.485328e+09</td>
      <td>Chipotle Mexican Grill -- Chipotle-Honey Vinai...</td>
      <td>77</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>self.MimicRecipes</td>
      <td>Looks correct to me\nSource: work there.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle Mexican Grill</td>
      <td>5pziaj</td>
      <td>all</td>
      <td>1.485328e+09</td>
      <td>Chipotle Mexican Grill -- Chipotle-Honey Vinai...</td>
      <td>77</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>self.MimicRecipes</td>
      <td>Thanks for posting this. This sweet nectar of ...</td>
      <td>0.8126</td>
      <td>0.393</td>
      <td>0.000</td>
      <td>0.607</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle Mexican Grill</td>
      <td>5pziaj</td>
      <td>all</td>
      <td>1.485328e+09</td>
      <td>Chipotle Mexican Grill -- Chipotle-Honey Vinai...</td>
      <td>77</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>self.MimicRecipes</td>
      <td>I made a double batch of this today using your...</td>
      <td>0.7003</td>
      <td>0.326</td>
      <td>0.000</td>
      <td>0.674</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle Mexican Grill</td>
      <td>5pziaj</td>
      <td>all</td>
      <td>1.485328e+09</td>
      <td>Chipotle Mexican Grill -- Chipotle-Honey Vinai...</td>
      <td>77</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/MimicRecipes/comments...</td>
      <td>self.MimicRecipes</td>
      <td>You forgot 1/3 cup of norovirus.</td>
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
      <th>7187</th>
      <td>Wendy's</td>
      <td>7i4sat</td>
      <td>all</td>
      <td>1.512660e+09</td>
      <td>Wendy's is now serving freshly cooked U N D E ...</td>
      <td>65</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>8</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>i.redd.it</td>
      <td>[Wendy is the next ~~Roger Ebert~~ Stuckmann](...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7188</th>
      <td>Wendy's</td>
      <td>7i4sat</td>
      <td>all</td>
      <td>1.512660e+09</td>
      <td>Wendy's is now serving freshly cooked U N D E ...</td>
      <td>65</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>8</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>i.redd.it</td>
      <td>lol they were also talking about twin peaks th...</td>
      <td>0.6705</td>
      <td>0.224</td>
      <td>0.000</td>
      <td>0.776</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7189</th>
      <td>Wendy's</td>
      <td>7i4sat</td>
      <td>all</td>
      <td>1.512660e+09</td>
      <td>Wendy's is now serving freshly cooked U N D E ...</td>
      <td>65</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>8</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>i.redd.it</td>
      <td>Great food and intellectual discussion.</td>
      <td>0.8126</td>
      <td>0.712</td>
      <td>0.000</td>
      <td>0.288</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7190</th>
      <td>Wendy's</td>
      <td>7i4sat</td>
      <td>all</td>
      <td>1.512660e+09</td>
      <td>Wendy's is now serving freshly cooked U N D E ...</td>
      <td>65</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>8</td>
      <td>https://i.redd.it/kco76gvkbg201.png</td>
      <td>i.redd.it</td>
      <td>Wendy’s out here saying what everyone was feel...</td>
      <td>0.6249</td>
      <td>0.282</td>
      <td>0.000</td>
      <td>0.718</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7191</th>
      <td>Wendy's</td>
      <td>7eaibv</td>
      <td>all</td>
      <td>1.511228e+09</td>
      <td>Wendy's S'awesome sauce is literally chik-fil-...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rants/comments/7eaibv...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/Rants/comments/7eaibv...</td>
      <td>self.Rants</td>
      <td>and mcdonalds special sauce is thousand island...</td>
      <td>0.4019</td>
      <td>0.278</td>
      <td>0.000</td>
      <td>0.722</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7192</th>
      <td>Wendy's</td>
      <td>7eaibv</td>
      <td>all</td>
      <td>1.511228e+09</td>
      <td>Wendy's S'awesome sauce is literally chik-fil-...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rants/comments/7eaibv...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/Rants/comments/7eaibv...</td>
      <td>self.Rants</td>
      <td>Why are you mad? Now people don't have to go t...</td>
      <td>-0.1759</td>
      <td>0.120</td>
      <td>0.150</td>
      <td>0.730</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7193</th>
      <td>Wendy's</td>
      <td>5oq24d</td>
      <td>all</td>
      <td>1.484783e+09</td>
      <td>Fedcoin: The U.S. Will Issue E-Currency That Y...</td>
      <td>16</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>7</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>news.bitcoin.com</td>
      <td>The US Dollar is already a digital currency.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7194</th>
      <td>Wendy's</td>
      <td>5oq24d</td>
      <td>all</td>
      <td>1.484783e+09</td>
      <td>Fedcoin: The U.S. Will Issue E-Currency That Y...</td>
      <td>16</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>7</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>news.bitcoin.com</td>
      <td>If they can track it - NO I WON'T.</td>
      <td>-0.4466</td>
      <td>0.000</td>
      <td>0.328</td>
      <td>0.672</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7195</th>
      <td>Wendy's</td>
      <td>5oq24d</td>
      <td>all</td>
      <td>1.484783e+09</td>
      <td>Fedcoin: The U.S. Will Issue E-Currency That Y...</td>
      <td>16</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>7</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>news.bitcoin.com</td>
      <td>no, I won't.</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.688</td>
      <td>0.312</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7196</th>
      <td>Wendy's</td>
      <td>5oq24d</td>
      <td>all</td>
      <td>1.484783e+09</td>
      <td>Fedcoin: The U.S. Will Issue E-Currency That Y...</td>
      <td>16</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>7</td>
      <td>https://news.bitcoin.com/fedcoin-u-s-issue-e-c...</td>
      <td>news.bitcoin.com</td>
      <td>It's still controlled by the US government thr...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7197</th>
      <td>Wendy's</td>
      <td>77n4ou</td>
      <td>all</td>
      <td>1.508545e+09</td>
      <td>Be creative in bringing N. Korea to talks: Wen...</td>
      <td>4</td>
      <td>http://the-japan-news.com/news/article/0004014178</td>
      <td>4</td>
      <td>http://the-japan-news.com/news/article/0004014178</td>
      <td>the-japan-news.com</td>
      <td>Wendy Sherman is one the people largely respon...</td>
      <td>-0.9100</td>
      <td>0.048</td>
      <td>0.308</td>
      <td>0.644</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7198</th>
      <td>Wendy's</td>
      <td>5xdqi4</td>
      <td>all</td>
      <td>1.488611e+09</td>
      <td>Question about the shredded American cheese th...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>self.wendys</td>
      <td>No it comes in a separate bag .</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.306</td>
      <td>0.694</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7199</th>
      <td>Wendy's</td>
      <td>5xdqi4</td>
      <td>all</td>
      <td>1.488611e+09</td>
      <td>Question about the shredded American cheese th...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>self.wendys</td>
      <td>In my store it comes pre-shredded.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7200</th>
      <td>Wendy's</td>
      <td>5xdqi4</td>
      <td>all</td>
      <td>1.488611e+09</td>
      <td>Question about the shredded American cheese th...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>self.wendys</td>
      <td>Only ever had type of shredded cheddar.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7201</th>
      <td>Wendy's</td>
      <td>5xdqi4</td>
      <td>all</td>
      <td>1.488611e+09</td>
      <td>Question about the shredded American cheese th...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>self.wendys</td>
      <td>I guess I might email Wendy's and see if they ...</td>
      <td>0.6705</td>
      <td>0.164</td>
      <td>0.000</td>
      <td>0.836</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7202</th>
      <td>Wendy's</td>
      <td>5xdqi4</td>
      <td>all</td>
      <td>1.488611e+09</td>
      <td>Question about the shredded American cheese th...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/wendys/comments/5xdqi...</td>
      <td>self.wendys</td>
      <td>Just wanted to be clear that I'm talking about...</td>
      <td>0.7964</td>
      <td>0.105</td>
      <td>0.000</td>
      <td>0.895</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7203</th>
      <td>Wendy's</td>
      <td>6fyj33</td>
      <td>all</td>
      <td>1.496922e+09</td>
      <td>Interesting observation about the Wendy v Cart...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/southpark/comments/6f...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/southpark/comments/6f...</td>
      <td>self.southpark</td>
      <td>The scene from Cripple Fight where Jimmy and T...</td>
      <td>-0.7717</td>
      <td>0.000</td>
      <td>0.312</td>
      <td>0.688</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7204</th>
      <td>Wendy's</td>
      <td>6fyj33</td>
      <td>all</td>
      <td>1.496922e+09</td>
      <td>Interesting observation about the Wendy v Cart...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/southpark/comments/6f...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/southpark/comments/6f...</td>
      <td>self.southpark</td>
      <td>In case you didn't know, you can google any ep...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.066</td>
      <td>0.934</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7205</th>
      <td>Wendy's</td>
      <td>6fyj33</td>
      <td>all</td>
      <td>1.496922e+09</td>
      <td>Interesting observation about the Wendy v Cart...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/southpark/comments/6f...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/southpark/comments/6f...</td>
      <td>self.southpark</td>
      <td>I always thought cartmans attack in coon and f...</td>
      <td>0.0000</td>
      <td>0.180</td>
      <td>0.180</td>
      <td>0.640</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7206</th>
      <td>Wendy's</td>
      <td>7lwjpx</td>
      <td>all</td>
      <td>1.514168e+09</td>
      <td>U.S. Commerce Official Still Holds Stake in Co...</td>
      <td>21</td>
      <td>https://www.propublica.org/article/u-s-commerc...</td>
      <td>1</td>
      <td>https://www.propublica.org/article/u-s-commerc...</td>
      <td>propublica.org</td>
      <td>\n\nSnapshots:\n\n1. *This Post* - [archive.or...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7207</th>
      <td>Wendy's</td>
      <td>6v5k0i</td>
      <td>all</td>
      <td>1.503374e+09</td>
      <td>This Wendy's coupon from the 80s. I'm gonna se...</td>
      <td>2</td>
      <td>http://imgur.com/a/URxCR</td>
      <td>6</td>
      <td>http://imgur.com/a/URxCR</td>
      <td>imgur.com</td>
      <td>I would guess if you talk to a manger they wil...</td>
      <td>-0.4466</td>
      <td>0.000</td>
      <td>0.155</td>
      <td>0.845</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7208</th>
      <td>Wendy's</td>
      <td>711dck</td>
      <td>all</td>
      <td>1.505835e+09</td>
      <td>"We think in two-year, four-year, six-year tim...</td>
      <td>6</td>
      <td>https://www.newyorker.com/magazine/2017/09/18/...</td>
      <td>1</td>
      <td>https://www.newyorker.com/magazine/2017/09/18/...</td>
      <td>newyorker.com</td>
      <td>I think this 'Long Term Vision' is all about m...</td>
      <td>0.4653</td>
      <td>0.079</td>
      <td>0.000</td>
      <td>0.921</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7209</th>
      <td>Wendy's</td>
      <td>62g6ng</td>
      <td>all</td>
      <td>1.490931e+09</td>
      <td>A short film I wrote, directed, &amp; produced abo...</td>
      <td>3</td>
      <td>https://vimeo.com/196966954</td>
      <td>2</td>
      <td>https://vimeo.com/196966954</td>
      <td>vimeo.com</td>
      <td>I loved this!</td>
      <td>0.6360</td>
      <td>0.807</td>
      <td>0.000</td>
      <td>0.193</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7210</th>
      <td>Wendy's</td>
      <td>7cwezm</td>
      <td>all</td>
      <td>1.510703e+09</td>
      <td>Senate Dems want Commerce Dept.'s top watchdog...</td>
      <td>13</td>
      <td>http://archive.is/aG3QY</td>
      <td>1</td>
      <td>http://archive.is/aG3QY</td>
      <td>archive.is</td>
      <td>More government waste and useless actions</td>
      <td>-0.7076</td>
      <td>0.000</td>
      <td>0.595</td>
      <td>0.405</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7211</th>
      <td>Wendy's</td>
      <td>6jtrlm</td>
      <td>all</td>
      <td>1.498609e+09</td>
      <td>"Wendy s**ts her pants" to the tune of "Safety...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/howardstern/comments/...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/howardstern/comments/...</td>
      <td>self.howardstern</td>
      <td>I wish there was a huge archive of just song p...</td>
      <td>0.6124</td>
      <td>0.185</td>
      <td>0.000</td>
      <td>0.815</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7212</th>
      <td>Wendy's</td>
      <td>6jtrlm</td>
      <td>all</td>
      <td>1.498609e+09</td>
      <td>"Wendy s**ts her pants" to the tune of "Safety...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/howardstern/comments/...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/howardstern/comments/...</td>
      <td>self.howardstern</td>
      <td>I need to hear this too!!! Cmon guys! Please f...</td>
      <td>-0.4153</td>
      <td>0.150</td>
      <td>0.265</td>
      <td>0.586</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7213</th>
      <td>Wendy's</td>
      <td>5lbrst</td>
      <td>all</td>
      <td>1.483248e+09</td>
      <td>A Wendy's training video from the 1980s</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=X3m7CyKptM0</td>
      <td>3</td>
      <td>https://www.youtube.com/watch?v=X3m7CyKptM0</td>
      <td>youtube.com</td>
      <td>Okay, first, why do we only throw the spoon aw...</td>
      <td>0.3720</td>
      <td>0.074</td>
      <td>0.000</td>
      <td>0.926</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7214</th>
      <td>Wendy's</td>
      <td>5lbrst</td>
      <td>all</td>
      <td>1.483248e+09</td>
      <td>A Wendy's training video from the 1980s</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=X3m7CyKptM0</td>
      <td>3</td>
      <td>https://www.youtube.com/watch?v=X3m7CyKptM0</td>
      <td>youtube.com</td>
      <td>The [Wendy's Grill Skills](https://youtu.be/Mb...</td>
      <td>-0.2500</td>
      <td>0.090</td>
      <td>0.127</td>
      <td>0.784</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7215</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>&gt; Anyone else notice she whispered something i...</td>
      <td>0.4222</td>
      <td>0.081</td>
      <td>0.000</td>
      <td>0.919</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7216</th>
      <td>Wendy's</td>
      <td>69zdvr</td>
      <td>all</td>
      <td>1.494292e+09</td>
      <td>[Spoilers S2E12] When Axe and Wendy hugged...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Billions/comments/69z...</td>
      <td>self.Billions</td>
      <td>GFY</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
<p>7217 rows × 16 columns</p>
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
      <th rowspan="5" valign="top">Chipotle Mexican Grill</th>
      <th>5pziaj</th>
      <th>1.485328e+09</th>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5q6ndz</th>
      <th>1.485415e+09</th>
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
      <th>5q6p8b</th>
      <th>1.485415e+09</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5qoctp</th>
      <th>1.485650e+09</th>
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
      <th>5w4a3q</th>
      <th>1.488062e+09</th>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
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
      <th rowspan="16" valign="top">Chipotle Mexican Grill</th>
      <th>5pziaj</th>
      <th>1.485328e+09</th>
      <td>0.378225</td>
    </tr>
    <tr>
      <th>5q6ndz</th>
      <th>1.485415e+09</th>
      <td>0.435233</td>
    </tr>
    <tr>
      <th>5q6p8b</th>
      <th>1.485415e+09</th>
      <td>-0.210750</td>
    </tr>
    <tr>
      <th>5qoctp</th>
      <th>1.485650e+09</th>
      <td>-0.202450</td>
    </tr>
    <tr>
      <th>5w4a3q</th>
      <th>1.488062e+09</th>
      <td>0.354014</td>
    </tr>
    <tr>
      <th>5w5yr3</th>
      <th>1.488082e+09</th>
      <td>0.046589</td>
    </tr>
    <tr>
      <th>68qpx7</th>
      <th>1.493724e+09</th>
      <td>-0.051600</td>
    </tr>
    <tr>
      <th>6bkhfk</th>
      <th>1.495000e+09</th>
      <td>0.180367</td>
    </tr>
    <tr>
      <th>6c3hf1</th>
      <th>1.495228e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>6dtzc2</th>
      <th>1.496010e+09</th>
      <td>0.050405</td>
    </tr>
    <tr>
      <th>6dw5ve</th>
      <th>1.496034e+09</th>
      <td>0.077200</td>
    </tr>
    <tr>
      <th>6ihoz8</th>
      <th>1.498028e+09</th>
      <td>0.757900</td>
    </tr>
    <tr>
      <th>7ah77t</th>
      <th>1.509713e+09</th>
      <td>0.430880</td>
    </tr>
    <tr>
      <th>7gpcc5</th>
      <th>1.512103e+09</th>
      <td>0.401900</td>
    </tr>
    <tr>
      <th>7izv1v</th>
      <th>1.512996e+09</th>
      <td>0.351867</td>
    </tr>
    <tr>
      <th>7k541j</th>
      <th>1.513428e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th rowspan="14" valign="top">McDonald's</th>
      <th>5o604h</th>
      <th>1.484539e+09</th>
      <td>0.306967</td>
    </tr>
    <tr>
      <th>5os472</th>
      <th>1.484802e+09</th>
      <td>0.076773</td>
    </tr>
    <tr>
      <th>5prcc8</th>
      <th>1.485231e+09</th>
      <td>0.066463</td>
    </tr>
    <tr>
      <th>5ptuei</th>
      <th>1.485257e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5s3gm3</th>
      <th>1.486274e+09</th>
      <td>-0.035930</td>
    </tr>
    <tr>
      <th>5s7wbi</th>
      <th>1.486337e+09</th>
      <td>-0.027247</td>
    </tr>
    <tr>
      <th>5sqqts</th>
      <th>1.486559e+09</th>
      <td>0.038467</td>
    </tr>
    <tr>
      <th>5svjh9</th>
      <th>1.486617e+09</th>
      <td>0.052767</td>
    </tr>
    <tr>
      <th>5sx2tz</th>
      <th>1.486633e+09</th>
      <td>-0.071560</td>
    </tr>
    <tr>
      <th>5sxkyx</th>
      <th>1.486639e+09</th>
      <td>0.214125</td>
    </tr>
    <tr>
      <th>5ujkuv</th>
      <th>1.487326e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5vhcsm</th>
      <th>1.487777e+09</th>
      <td>-0.044242</td>
    </tr>
    <tr>
      <th>5vqjhm</th>
      <th>1.487888e+09</th>
      <td>0.168500</td>
    </tr>
    <tr>
      <th>5vwrbd</th>
      <th>1.487960e+09</th>
      <td>0.133400</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="6" valign="top">Taco Bell</th>
      <th>7gn174</th>
      <th>1.512084e+09</th>
      <td>-0.024187</td>
    </tr>
    <tr>
      <th>7jnx3l</th>
      <th>1.513241e+09</th>
      <td>0.107107</td>
    </tr>
    <tr>
      <th>7jrdnx</th>
      <th>1.513285e+09</th>
      <td>0.216794</td>
    </tr>
    <tr>
      <th>7laty1</th>
      <th>1.513905e+09</th>
      <td>-0.024890</td>
    </tr>
    <tr>
      <th>7lnane</th>
      <th>1.514041e+09</th>
      <td>-0.053705</td>
    </tr>
    <tr>
      <th>7lwp2b</th>
      <th>1.514169e+09</th>
      <td>-0.062365</td>
    </tr>
    <tr>
      <th rowspan="24" valign="top">Wendy's</th>
      <th>5lbrst</th>
      <th>1.483248e+09</th>
      <td>0.061000</td>
    </tr>
    <tr>
      <th>5oq24d</th>
      <th>1.484783e+09</th>
      <td>-0.185650</td>
    </tr>
    <tr>
      <th>5tjfam</th>
      <th>1.486900e+09</th>
      <td>-0.124647</td>
    </tr>
    <tr>
      <th>5tkqgn</th>
      <th>1.486924e+09</th>
      <td>0.356433</td>
    </tr>
    <tr>
      <th>5xdqi4</th>
      <th>1.488611e+09</th>
      <td>0.234180</td>
    </tr>
    <tr>
      <th>62g6ng</th>
      <th>1.490931e+09</th>
      <td>0.636000</td>
    </tr>
    <tr>
      <th>64hm6b</th>
      <th>1.491828e+09</th>
      <td>-0.125383</td>
    </tr>
    <tr>
      <th>69zdvr</th>
      <th>1.494292e+09</th>
      <td>0.211100</td>
    </tr>
    <tr>
      <th>6fyj33</th>
      <th>1.496922e+09</th>
      <td>-0.355900</td>
    </tr>
    <tr>
      <th>6jtrlm</th>
      <th>1.498609e+09</th>
      <td>0.098550</td>
    </tr>
    <tr>
      <th>6qv1hr</th>
      <th>1.501607e+09</th>
      <td>0.213457</td>
    </tr>
    <tr>
      <th>6s0ke4</th>
      <th>1.502078e+09</th>
      <td>0.294240</td>
    </tr>
    <tr>
      <th>6u2m6k</th>
      <th>1.502925e+09</th>
      <td>0.323029</td>
    </tr>
    <tr>
      <th>6v5k0i</th>
      <th>1.503374e+09</th>
      <td>-0.446600</td>
    </tr>
    <tr>
      <th>6ylx3w</th>
      <th>1.504801e+09</th>
      <td>0.084427</td>
    </tr>
    <tr>
      <th>70q2yx</th>
      <th>1.505709e+09</th>
      <td>-0.245767</td>
    </tr>
    <tr>
      <th>711dck</th>
      <th>1.505835e+09</th>
      <td>0.465300</td>
    </tr>
    <tr>
      <th>77n4ou</th>
      <th>1.508545e+09</th>
      <td>-0.910000</td>
    </tr>
    <tr>
      <th>7b7k9f</th>
      <th>1.510026e+09</th>
      <td>0.213208</td>
    </tr>
    <tr>
      <th>7cwezm</th>
      <th>1.510703e+09</th>
      <td>-0.707600</td>
    </tr>
    <tr>
      <th>7dl6m1</th>
      <th>1.510957e+09</th>
      <td>-0.219688</td>
    </tr>
    <tr>
      <th>7eaibv</th>
      <th>1.511228e+09</th>
      <td>0.113000</td>
    </tr>
    <tr>
      <th>7i4sat</th>
      <th>1.512660e+09</th>
      <td>0.421600</td>
    </tr>
    <tr>
      <th>7lwjpx</th>
      <th>1.514168e+09</th>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>290 rows × 1 columns</p>
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
      <td>Chipotle Mexican Grill</td>
      <td>5pziaj</td>
      <td>1.485328e+09</td>
      <td>0.378225</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Mexican Grill</td>
      <td>5q6ndz</td>
      <td>1.485415e+09</td>
      <td>0.435233</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Mexican Grill</td>
      <td>5q6p8b</td>
      <td>1.485415e+09</td>
      <td>-0.210750</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Mexican Grill</td>
      <td>5qoctp</td>
      <td>1.485650e+09</td>
      <td>-0.202450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Mexican Grill</td>
      <td>5w4a3q</td>
      <td>1.488062e+09</td>
      <td>0.354014</td>
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

plt.savefig("Restaurant_Sentiments_2017.png", dpi=350)

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

