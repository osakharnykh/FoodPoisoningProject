

```python
import pandas as pd
import praw
import numpy as np
#import matplotlib.pyplot as plt
import matplotlib.dates as md
import matplotlib.pylab as plt
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

keywords = ["Chipotle food poisoning", "Chipotle food allergy", "Chipotle e. coli", 
            "Chipotle salmonella", "Chipotle Norovirus", "Chipotle foodborne illness",
            "McDonald's food poisoning", "McDonald's food allergy", "McDonald's e. coli", 
            "McDonald's salmonella", "McDonald's Norovirus", "McDonald's foodborne illness",
            "Taco Bell food poisoning", "Taco Bell food allergy", "Taco Bell e. coli", 
            "Taco Bell salmonella", "Taco Bell Norovirus", "Taco Bell foodborne illness",
            "Wendy's food poisoning", "Wendy's food allergy", "Wendy's e. coli", 
            "Wendy's salmonella", "Wendy's Norovirus", "Wendy's foodborne illness",
            "Domino’s Pizza food poisoning", "Domino’s Pizza food allergy", "Domino’s Pizza e. coli", 
            "Domino’s Pizza salmonella", "Domino’s Pizza Norovirus", "Domino’s Pizza foodborne illness",
            "Burger King food poisoning", "Burger King food allergy", "Burger King e. coli", 
            "Burger King salmonella", "Burger King Norovirus", "Burger King foodborne illness",
            "Costco food poisoning", "Costco food allergy", "Costco e. coli", 
            "Costco salmonella", "Costco Norovirus", "Costco foodborne illness",
            "Popeyes food poisoning", "Popeyes food allergy", "Popeyes e. coli", 
            "Popeyes salmonella", "Popeyes Norovirus", "Popeyes foodborne illness",
            "Panda Express food poisoning", "Panda Express food allergy", "Panda Express e. coli", 
            "Panda Express salmonella", "Panda Express Norovirus", "Panda Express foodborne illness"
            "'Subway sandwich' food poisoning", "'Subway sandwich' food allergy", "'Subway sandwich' e. coli", 
            "'Subway sandwich' salmonella", "'Subway sandwich' Norovirus", "'Subway sandwich' foodborne illness"
           "KFC food poisoning", "KFC food allergy", "KFC e. coli", 
            "KFC salmonella", "KFC Norovirus", "KFC foodborne illness",
           "Jimmy John's food poisoning", "Jimmy John's food allergy", "Jimmy John's e. coli", 
            "Jimmy John's salmonella", "Jimmy John's Norovirus", "Jimmy John's foodborne illness"]

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
      <th>361</th>
      <td>Chipotle Norovirus</td>
      <td>4a05qr</td>
      <td>all</td>
      <td>1.457751e+09</td>
      <td>ELI5: Since Norovirus is not a food-borne illn...</td>
      <td>3624</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>1062</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Chipotle e. coli</td>
      <td>3r7wvw</td>
      <td>all</td>
      <td>1.446507e+09</td>
      <td>Chipotle Tumbles After E. Coli Outbreak Is Lin...</td>
      <td>2615</td>
      <td>http://www.bloomberg.com/news/articles/2015-11...</td>
      <td>532</td>
      <td>http://www.bloomberg.com/news/articles/2015-11...</td>
      <td>bloomberg.com</td>
    </tr>
    <tr>
      <th>360</th>
      <td>Chipotle Norovirus</td>
      <td>6ojkiw</td>
      <td>all</td>
      <td>1.500616e+09</td>
      <td>Chipotle's stock is tanking on reports of rats...</td>
      <td>499</td>
      <td>http://www.cnbc.com/2017/07/20/rodents-reporte...</td>
      <td>314</td>
      <td>http://www.cnbc.com/2017/07/20/rodents-reporte...</td>
      <td>cnbc.com</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6113</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Chipotle e. coli</td>
      <td>3vxewb</td>
      <td>all</td>
      <td>1.449611e+09</td>
      <td>Chipotle shares take fresh hit after Boston Co...</td>
      <td>750</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>194</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
    </tr>
    <tr>
      <th>536</th>
      <td>Chipotle foodborne illness</td>
      <td>40zzl4</td>
      <td>all</td>
      <td>1.452839e+09</td>
      <td>Chipotle's supply chain called into question a...</td>
      <td>699</td>
      <td>https://www.healthline.com/health-news/chipotl...</td>
      <td>191</td>
      <td>https://www.healthline.com/health-news/chipotl...</td>
      <td>healthline.com</td>
    </tr>
    <tr>
      <th>362</th>
      <td>Chipotle Norovirus</td>
      <td>4acy2o</td>
      <td>all</td>
      <td>1.457989e+09</td>
      <td>Chipotle Suspends Exec Bonuses After Outbreaks...</td>
      <td>1065</td>
      <td>https://www.reddit.com/r/investing/comments/4a...</td>
      <td>171</td>
      <td>https://www.reddit.com/r/investing/comments/4a...</td>
      <td>self.investing</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Chipotle e. coli</td>
      <td>4acy2o</td>
      <td>all</td>
      <td>1.457989e+09</td>
      <td>Chipotle Suspends Exec Bonuses After Outbreaks...</td>
      <td>1066</td>
      <td>https://www.reddit.com/r/investing/comments/4a...</td>
      <td>171</td>
      <td>https://www.reddit.com/r/investing/comments/4a...</td>
      <td>self.investing</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Chipotle e. coli</td>
      <td>3vuk04</td>
      <td>all</td>
      <td>1.449556e+09</td>
      <td>Extremely bearish; Chipotle E. Coli disables e...</td>
      <td>533</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>166</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Chipotle e. coli</td>
      <td>43pftt</td>
      <td>all</td>
      <td>1.454376e+09</td>
      <td>CDC declares Chipotle-linked E. coli outbreak ...</td>
      <td>846</td>
      <td>http://www.cnbc.com/2016/02/01/cdc-declares-ch...</td>
      <td>164</td>
      <td>http://www.cnbc.com/2016/02/01/cdc-declares-ch...</td>
      <td>cnbc.com</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Chipotle e. coli</td>
      <td>3qzjqg</td>
      <td>all</td>
      <td>1.446342e+09</td>
      <td>22 sick from E. coli; Chipotles closed in Ore....</td>
      <td>411</td>
      <td>http://www.kgw.com/story/news/local/2015/10/31...</td>
      <td>152</td>
      <td>http://www.kgw.com/story/news/local/2015/10/31...</td>
      <td>kgw.com</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Chipotle e. coli</td>
      <td>3r8edx</td>
      <td>all</td>
      <td>1.446514e+09</td>
      <td>MFW I read the door of Chipotle last night aft...</td>
      <td>46</td>
      <td>http://giant.gfycat.com/UnrealisticWellwornInd...</td>
      <td>113</td>
      <td>http://giant.gfycat.com/UnrealisticWellwornInd...</td>
      <td>giant.gfycat.com</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Chipotle e. coli</td>
      <td>43pitn</td>
      <td>all</td>
      <td>1.454377e+09</td>
      <td>CDC declares Chipotle-linked E. coli outbreak ...</td>
      <td>498</td>
      <td>https://www.reddit.com/r/investing/comments/43...</td>
      <td>111</td>
      <td>https://www.reddit.com/r/investing/comments/43...</td>
      <td>self.investing</td>
    </tr>
    <tr>
      <th>365</th>
      <td>Chipotle Norovirus</td>
      <td>49l1sn</td>
      <td>all</td>
      <td>1.457506e+09</td>
      <td>Chipotle restaurant in Massachusetts shut down...</td>
      <td>286</td>
      <td>http://www.whdh.com/story/31418890/chipotle-re...</td>
      <td>105</td>
      <td>http://www.whdh.com/story/31418890/chipotle-re...</td>
      <td>whdh.com</td>
    </tr>
    <tr>
      <th>366</th>
      <td>Chipotle Norovirus</td>
      <td>49l7ql</td>
      <td>all</td>
      <td>1.457509e+09</td>
      <td>Chipotle restaurant in Billerica shut down aft...</td>
      <td>150</td>
      <td>http://www.whdh.com/story/31418890/chipotle-re...</td>
      <td>101</td>
      <td>http://www.whdh.com/story/31418890/chipotle-re...</td>
      <td>whdh.com</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Chipotle e. coli</td>
      <td>3zsozj</td>
      <td>all</td>
      <td>1.452154e+09</td>
      <td>Chipotle is a victim of corporate sabotage... ...</td>
      <td>553</td>
      <td>http://www.naturalnews.com/052405_Chipotle_eco...</td>
      <td>91</td>
      <td>http://www.naturalnews.com/052405_Chipotle_eco...</td>
      <td>naturalnews.com</td>
    </tr>
    <tr>
      <th>590</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>513</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>591</th>
      <td>Costco e. coli</td>
      <td>1oacvi</td>
      <td>all</td>
      <td>1.381612e+09</td>
      <td>Costco recalls beef over E. coli concerns in W...</td>
      <td>223</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>73</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>cbc.ca</td>
    </tr>
    <tr>
      <th>364</th>
      <td>Chipotle Norovirus</td>
      <td>6pgsou</td>
      <td>all</td>
      <td>1.501025e+09</td>
      <td>Second Norovirus Case Tied To Virginia Chipotl...</td>
      <td>256</td>
      <td>http://dcist.com/2017/07/second_norovirus_case...</td>
      <td>72</td>
      <td>http://dcist.com/2017/07/second_norovirus_case...</td>
      <td>dcist.com</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Chipotle e. coli</td>
      <td>414q3q</td>
      <td>all</td>
      <td>1.452916e+09</td>
      <td>Chipotle should offer free guac as a way to pa...</td>
      <td>832</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>70</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Chipotle e. coli</td>
      <td>52o6ei</td>
      <td>all</td>
      <td>1.473846e+09</td>
      <td>Chipotle Customer Who Got E. Coli Asks for Fre...</td>
      <td>490</td>
      <td>http://time.com/4490672/chipotle-ecoli-free-bu...</td>
      <td>69</td>
      <td>http://time.com/4490672/chipotle-ecoli-free-bu...</td>
      <td>time.com</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Chipotle e. coli</td>
      <td>3z9ncd</td>
      <td>all</td>
      <td>1.451853e+09</td>
      <td>ANALYSIS: Chipotle is a victim of corporate sa...</td>
      <td>366</td>
      <td>http://investmentwatchblog.com/analysis-chipot...</td>
      <td>63</td>
      <td>http://investmentwatchblog.com/analysis-chipot...</td>
      <td>investmentwatchblog.com</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Chipotle e. coli</td>
      <td>3qzw81</td>
      <td>all</td>
      <td>1.446347e+09</td>
      <td>All Chipotle restaurants in Oregon and Washing...</td>
      <td>212</td>
      <td>http://q13fox.com/2015/10/31/all-chipotle-rest...</td>
      <td>62</td>
      <td>http://q13fox.com/2015/10/31/all-chipotle-rest...</td>
      <td>q13fox.com</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Chipotle e. coli</td>
      <td>3xx84v</td>
      <td>all</td>
      <td>1.450872e+09</td>
      <td>ANALYSIS: Chipotle is a victim of corporate sa...</td>
      <td>136</td>
      <td>http://www.naturalnews.com/052405_Chipotle_eco...</td>
      <td>59</td>
      <td>http://www.naturalnews.com/052405_Chipotle_eco...</td>
      <td>naturalnews.com</td>
    </tr>
    <tr>
      <th>371</th>
      <td>Chipotle Norovirus</td>
      <td>6o9dza</td>
      <td>all</td>
      <td>1.500509e+09</td>
      <td>Chipotle had another outbreak of norovirus, wh...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/6o...</td>
      <td>57</td>
      <td>https://www.reddit.com/r/AskReddit/comments/6o...</td>
      <td>self.AskReddit</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Chipotle e. coli</td>
      <td>3rfmip</td>
      <td>all</td>
      <td>1.446629e+09</td>
      <td>Twelve confirmed cases of E Coli from Chipotle...</td>
      <td>69</td>
      <td>http://www.wweek.com/2015/11/03/there-are-now-...</td>
      <td>57</td>
      <td>http://www.wweek.com/2015/11/03/there-are-now-...</td>
      <td>wweek.com</td>
    </tr>
    <tr>
      <th>363</th>
      <td>Chipotle Norovirus</td>
      <td>6op39k</td>
      <td>all</td>
      <td>1.500684e+09</td>
      <td>UPDATE: 60 sickened by Chipotle norovirus in S...</td>
      <td>171</td>
      <td>http://www.insidenova.com/news/business/sicken...</td>
      <td>56</td>
      <td>http://www.insidenova.com/news/business/sicken...</td>
      <td>insidenova.com</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Chipotle e. coli</td>
      <td>3rflv7</td>
      <td>all</td>
      <td>1.446629e+09</td>
      <td>Seattle Chipotle locations part of E. coli out...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/Seattle/comments/3rfl...</td>
      <td>50</td>
      <td>https://www.reddit.com/r/Seattle/comments/3rfl...</td>
      <td>self.Seattle</td>
    </tr>
    <tr>
      <th>368</th>
      <td>Chipotle Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>197</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
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
      <th>273</th>
      <td>Chipotle e. coli</td>
      <td>3xuyqp</td>
      <td>all</td>
      <td>1.450836e+09</td>
      <td>Chipotle's E. Coli Problem Scares Me</td>
      <td>1</td>
      <td>http://gizmodo.com/chipotles-e-coli-problem-sc...</td>
      <td>0</td>
      <td>http://gizmodo.com/chipotles-e-coli-problem-sc...</td>
      <td>gizmodo.com</td>
    </tr>
    <tr>
      <th>297</th>
      <td>Chipotle e. coli</td>
      <td>3xzx74</td>
      <td>all</td>
      <td>1.450928e+09</td>
      <td>[Gamer] Chipotle Cooks Up New, Stricter Food S...</td>
      <td>1</td>
      <td>http://www.entrepreneur.com/article/254351</td>
      <td>0</td>
      <td>http://www.entrepreneur.com/article/254351</td>
      <td>entrepreneur.com</td>
    </tr>
    <tr>
      <th>299</th>
      <td>Chipotle e. coli</td>
      <td>5gts0x</td>
      <td>all</td>
      <td>1.481070e+09</td>
      <td>[Business] - Chipotle's E. coli woes might not...</td>
      <td>1</td>
      <td>http://money.cnn.com/2016/12/06/investing/chip...</td>
      <td>0</td>
      <td>http://money.cnn.com/2016/12/06/investing/chip...</td>
      <td>money.cnn.com</td>
    </tr>
    <tr>
      <th>329</th>
      <td>Chipotle e. coli</td>
      <td>3r12ub</td>
      <td>all</td>
      <td>1.446367e+09</td>
      <td>E. coli sickens at least 22 people who ate at ...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/autotldr/comments/3r1...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/autotldr/comments/3r1...</td>
      <td>self.autotldr</td>
    </tr>
    <tr>
      <th>315</th>
      <td>Chipotle e. coli</td>
      <td>4rdrxw</td>
      <td>all</td>
      <td>1.467768e+09</td>
      <td>The Chipotle marketing executive leading the c...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/NoFilterNews/comments...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/NoFilterNews/comments...</td>
      <td>self.NoFilterNews</td>
    </tr>
    <tr>
      <th>328</th>
      <td>Chipotle e. coli</td>
      <td>3rgh4o</td>
      <td>all</td>
      <td>1.446644e+09</td>
      <td>[#3] Chipotle now linked to 35 confirmed E. co...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/worldnews/comments/3rg...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/worldnews/comments/3rg...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>326</th>
      <td>Chipotle e. coli</td>
      <td>3sa9v6</td>
      <td>all</td>
      <td>1.447200e+09</td>
      <td>No source found for E. coli; Washington and Or...</td>
      <td>1</td>
      <td>http://registerguard.com/rg/news/local/3369837...</td>
      <td>0</td>
      <td>http://registerguard.com/rg/news/local/3369837...</td>
      <td>registerguard.com</td>
    </tr>
    <tr>
      <th>325</th>
      <td>Chipotle e. coli</td>
      <td>3r7wyv</td>
      <td>all</td>
      <td>1.446507e+09</td>
      <td>[#901|+73|13] Chipotle shares down 7% in thin ...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/Economics/comments/3r7...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/Economics/comments/3r7...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>324</th>
      <td>Chipotle e. coli</td>
      <td>3rn8be</td>
      <td>all</td>
      <td>1.446770e+09</td>
      <td>CDC Investigating As E. Coli Outbreak Linked T...</td>
      <td>1</td>
      <td>http://www.npr.org/sections/thesalt/2015/11/05...</td>
      <td>0</td>
      <td>http://www.npr.org/sections/thesalt/2015/11/05...</td>
      <td>npr.org</td>
    </tr>
    <tr>
      <th>323</th>
      <td>Chipotle e. coli</td>
      <td>6mysk3</td>
      <td>all</td>
      <td>1.499942e+09</td>
      <td>[Business] - We Tried Chipotle's New Queso Dip...</td>
      <td>1</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>0</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>philly.com</td>
    </tr>
    <tr>
      <th>322</th>
      <td>Chipotle e. coli</td>
      <td>5gtwt5</td>
      <td>all</td>
      <td>1.481072e+09</td>
      <td>[Business] - Chipotle's E. coli woes might not...</td>
      <td>1</td>
      <td>http://money.cnn.com/2016/12/06/investing/chip...</td>
      <td>0</td>
      <td>http://money.cnn.com/2016/12/06/investing/chip...</td>
      <td>money.cnn.com</td>
    </tr>
    <tr>
      <th>321</th>
      <td>Chipotle e. coli</td>
      <td>43mduw</td>
      <td>all</td>
      <td>1.454323e+09</td>
      <td>CDC expected to declare end to Chipotle's E.co...</td>
      <td>1</td>
      <td>http://feeds.reuters.com/~r/Reuters/domesticNe...</td>
      <td>0</td>
      <td>http://feeds.reuters.com/~r/Reuters/domesticNe...</td>
      <td>feeds.reuters.com</td>
    </tr>
    <tr>
      <th>320</th>
      <td>Chipotle e. coli</td>
      <td>3r41pj</td>
      <td>all</td>
      <td>1.446434e+09</td>
      <td>Chipotle shuts Seattle, Portland stores after ...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/01/us-c...</td>
      <td>0</td>
      <td>http://www.reuters.com/article/2015/11/01/us-c...</td>
      <td>reuters.com</td>
    </tr>
    <tr>
      <th>319</th>
      <td>Chipotle e. coli</td>
      <td>6lnuah</td>
      <td>all</td>
      <td>1.499395e+09</td>
      <td>[Business] - This Millennial Visited Chipotle ...</td>
      <td>1</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>0</td>
      <td>http://www.philly.com/philly/business/thestree...</td>
      <td>philly.com</td>
    </tr>
    <tr>
      <th>317</th>
      <td>Chipotle e. coli</td>
      <td>3r7x0a</td>
      <td>all</td>
      <td>1.446507e+09</td>
      <td>[#900|+73|13] Chipotle shares down 7% in thin ...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Economics/comments/3r...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Economics/comments/3r...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>316</th>
      <td>Chipotle e. coli</td>
      <td>3xz5ol</td>
      <td>all</td>
      <td>1.450916e+09</td>
      <td>[Tech] FDA and CDC probe second wave of Chipot...</td>
      <td>1</td>
      <td>http://arstechnica.com/science/2015/12/fda-and...</td>
      <td>0</td>
      <td>http://arstechnica.com/science/2015/12/fda-and...</td>
      <td>arstechnica.com</td>
    </tr>
    <tr>
      <th>314</th>
      <td>Chipotle e. coli</td>
      <td>440v7f</td>
      <td>all</td>
      <td>1.454550e+09</td>
      <td>The Cost of Chipotle's E. Coli Outbreak, Measu...</td>
      <td>1</td>
      <td>http://gizmodo.com/the-cost-of-chipotles-e-col...</td>
      <td>0</td>
      <td>http://gizmodo.com/the-cost-of-chipotles-e-col...</td>
      <td>gizmodo.com</td>
    </tr>
    <tr>
      <th>301</th>
      <td>Chipotle e. coli</td>
      <td>3ubk44</td>
      <td>all</td>
      <td>1.448551e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3ub...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/autotldr/comments/3ub...</td>
      <td>self.autotldr</td>
    </tr>
    <tr>
      <th>313</th>
      <td>Chipotle e. coli</td>
      <td>43pqum</td>
      <td>all</td>
      <td>1.454379e+09</td>
      <td>CDC says Chipotle-linked outbreak of E. coli a...</td>
      <td>1</td>
      <td>http://hosted.ap.org/dynamic/stories/U/US_CHIP...</td>
      <td>0</td>
      <td>http://hosted.ap.org/dynamic/stories/U/US_CHIP...</td>
      <td>hosted.ap.org</td>
    </tr>
    <tr>
      <th>312</th>
      <td>Chipotle e. coli</td>
      <td>3zb5ks</td>
      <td>all</td>
      <td>1.451879e+09</td>
      <td>ANALYSIS: Chipotle is a victim of corporate sa...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/conspiracy/comments/3...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/conspiracy/comments/3...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>311</th>
      <td>Chipotle e. coli</td>
      <td>43vndj</td>
      <td>all</td>
      <td>1.454468e+09</td>
      <td>CDC investigation of Chipotle further supports...</td>
      <td>1</td>
      <td>https://reddit.com/r/conspiracy/comments/43vn8...</td>
      <td>0</td>
      <td>https://reddit.com/r/conspiracy/comments/43vn8...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>310</th>
      <td>Chipotle e. coli</td>
      <td>3r42jp</td>
      <td>all</td>
      <td>1.446434e+09</td>
      <td>Chipotle shuts Seattle, Portland stores after ...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/01/us-c...</td>
      <td>0</td>
      <td>http://www.reuters.com/article/2015/11/01/us-c...</td>
      <td>reuters.com</td>
    </tr>
    <tr>
      <th>309</th>
      <td>Chipotle e. coli</td>
      <td>3wb2z7</td>
      <td>all</td>
      <td>1.449825e+09</td>
      <td>After E. coli and norovirus outbreaks, Chipotl...</td>
      <td>1</td>
      <td>http://boingboing.net/2015/12/10/after-e-coli-...</td>
      <td>0</td>
      <td>http://boingboing.net/2015/12/10/after-e-coli-...</td>
      <td>boingboing.net</td>
    </tr>
    <tr>
      <th>308</th>
      <td>Chipotle e. coli</td>
      <td>5n7reg</td>
      <td>all</td>
      <td>1.484112e+09</td>
      <td>Chipotle Sales Jump, But That's Compared To La...</td>
      <td>1</td>
      <td>http://www.forbes.com/forbes/welcome/?toURL=ht...</td>
      <td>0</td>
      <td>http://www.forbes.com/forbes/welcome/?toURL=ht...</td>
      <td>forbes.com</td>
    </tr>
    <tr>
      <th>307</th>
      <td>Chipotle e. coli</td>
      <td>3s7w3e</td>
      <td>all</td>
      <td>1.447151e+09</td>
      <td>Washington state finds no E.coli in first Chip...</td>
      <td>1</td>
      <td>http://feeds.reuters.com/~r/Reuters/domesticNe...</td>
      <td>0</td>
      <td>http://feeds.reuters.com/~r/Reuters/domesticNe...</td>
      <td>feeds.reuters.com</td>
    </tr>
    <tr>
      <th>306</th>
      <td>Chipotle e. coli</td>
      <td>5gp8eo</td>
      <td>all</td>
      <td>1.481008e+09</td>
      <td>Some Perspective on Delos's Corporate Dysfunct...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/westworld/comments/5g...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/westworld/comments/5g...</td>
      <td>self.westworld</td>
    </tr>
    <tr>
      <th>305</th>
      <td>Chipotle e. coli</td>
      <td>42h9jv</td>
      <td>all</td>
      <td>1.453692e+09</td>
      <td>You can't spell Chipotle without E Coli</td>
      <td>1</td>
      <td>https://www.reddit.com/r/RIPshowerthoughts/com...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/RIPshowerthoughts/com...</td>
      <td>self.RIPshowerthoughts</td>
    </tr>
    <tr>
      <th>303</th>
      <td>Chipotle e. coli</td>
      <td>3tm98w</td>
      <td>all</td>
      <td>1.448085e+09</td>
      <td>Chipotle shares hit by E. coli scare</td>
      <td>1</td>
      <td>http://www.bbc.co.uk/news/business-34886105#sa...</td>
      <td>0</td>
      <td>http://www.bbc.co.uk/news/business-34886105#sa...</td>
      <td>bbc.co.uk</td>
    </tr>
    <tr>
      <th>302</th>
      <td>Chipotle e. coli</td>
      <td>3y1kzm</td>
      <td>all</td>
      <td>1.450958e+09</td>
      <td>"There is no E. coli in Chipotle. ” - Steve Ells</td>
      <td>0</td>
      <td>https://www.reddit.com/r/funny/comments/3y1kzm...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/funny/comments/3y1kzm...</td>
      <td>self.funny</td>
    </tr>
    <tr>
      <th>653</th>
      <td>KFC salmonella</td>
      <td>106nxu</td>
      <td>all</td>
      <td>1.348162e+09</td>
      <td>KFC appeals the verdict which awarded a Sydney...</td>
      <td>1</td>
      <td>http://news.smh.com.au/breaking-news-national/...</td>
      <td>0</td>
      <td>http://news.smh.com.au/breaking-news-national/...</td>
      <td>news.smh.com.au</td>
    </tr>
  </tbody>
</table>
<p>654 rows × 10 columns</p>
</div>




```python
reddit_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 654 entries, 0 to 653
    Data columns (total 10 columns):
    Keyword                      654 non-null object
    Submission ID                654 non-null object
    Subreddit                    654 non-null object
    Created Date                 654 non-null float64
    Submission Title             654 non-null object
    Submission Score             654 non-null int64
    Submission URL               654 non-null object
    Total Submission Comments    654 non-null int64
    Submission URL               654 non-null object
    Domain                       654 non-null object
    dtypes: float64(1), int64(2), object(7)
    memory usage: 51.2+ KB



```python
reddit_df["Keyword"].value_counts()
```




    Chipotle e. coli                  320
    Chipotle Norovirus                176
    Costco e. coli                     54
    Chipotle food poisoning            32
    Chipotle foodborne illness         24
    Taco Bell food poisoning            8
    Chipotle salmonella                 8
    Taco Bell salmonella                8
    KFC e. coli                         3
    Burger King e. coli                 3
    Burger King food poisoning          3
    KFC salmonella                      3
    Burger King salmonella              3
    Taco Bell e. coli                   2
    Costco food poisoning               2
    Burger King food allergy            1
    Popeyes food poisoning              1
    'Subway sandwich' food allergy      1
    Costco salmonella                   1
    Panda Express food poisoning        1
    Name: Keyword, dtype: int64




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
      <td>[removed]</td>
      <td>4135sq</td>
    </tr>
    <tr>
      <th>1</th>
      <td>I mentioned this in a similar thread, but requ...</td>
      <td>4135sq</td>
    </tr>
    <tr>
      <th>2</th>
      <td>How about not punishing/ firing employees for ...</td>
      <td>4135sq</td>
    </tr>
    <tr>
      <th>3</th>
      <td>I think their flailing hurt them as bad as the...</td>
      <td>4135sq</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A Chipotle just opened up a few months ago rig...</td>
      <td>4135sq</td>
    </tr>
  </tbody>
</table>
</div>




```python
comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1714 entries, 0 to 1713
    Data columns (total 2 columns):
    Submission Comments    1714 non-null object
    Submission ID          1714 non-null object
    dtypes: object(2)
    memory usage: 26.9+ KB



```python
# Merge two dataframes using an outer join
reddit_comments_df = pd.merge(reddit_df, comments_df, on="Submission ID", how="outer")

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
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>[removed]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Personal anecdote. Every time I had been to Ch...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>This has got to be hell for employees.  There ...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I have been following this since the beginning...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I've watched people at chipotle pour new meat,...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>They don't open till 11am. You can coordinate ...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I bet they order Chinese for that company-wide...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I used to work at chipotle. Our store had fail...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I don't eat there anymore not because of food ...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I like how their come back plan was more marke...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Chi chi's went bankrupt after a Hepatitis A ou...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I stopped eating there long before this.\n\n1....</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I ate at a Seattle store 2 hours before they c...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I went to Chipotle the other day and the guy c...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I already stopped eating there because they we...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>The 30% hit could also be because they charge ...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I hope Baja Fresh comes back.</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Which is why I've been going there more often....</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I have converted to eating at Qdoba now.</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I still go every week, and its been night and ...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>They still have my business. I just love the w...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>What happened to Chipotle is the same thing th...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I make up 3% of chipotles annual sales. They b...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Pancheros is so much better</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I knew Pancheros was better !</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>What good will closing the stores do if the ta...</td>
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
      <th>2206</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Idk I think I’m still gonna go</td>
    </tr>
    <tr>
      <th>2207</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>[deleted]</td>
    </tr>
    <tr>
      <th>2208</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>The one on East Ridge has rats so I'm not surp...</td>
    </tr>
    <tr>
      <th>2209</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Love me some Golden Ponds.</td>
    </tr>
    <tr>
      <th>2210</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>This isn't going to be good for business.\n/se...</td>
    </tr>
    <tr>
      <th>2211</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>[I'm surprised they didn't run out of chicken....</td>
    </tr>
    <tr>
      <th>2212</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Take the $11 loss</td>
    </tr>
    <tr>
      <th>2213</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>If you are concerned, call the [Monroe County ...</td>
    </tr>
    <tr>
      <th>2214</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Lol. If I went to the hospital/a doctor and ha...</td>
    </tr>
    <tr>
      <th>2215</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>I got broads in Atlanta...</td>
    </tr>
    <tr>
      <th>2216</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>Don't fuck around with food poisoning, if it d...</td>
    </tr>
    <tr>
      <th>2217</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>You're lucky, all Panda ever gives me is a box...</td>
    </tr>
    <tr>
      <th>2218</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>Not the panda you're talking about, but still,...</td>
    </tr>
    <tr>
      <th>2219</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>I got food poisoning from a place called \n\nW...</td>
    </tr>
    <tr>
      <th>2220</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>i don't even care i will never stop eating pan...</td>
    </tr>
    <tr>
      <th>2221</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>"Panda express isnt *that* bad" said my friend...</td>
    </tr>
    <tr>
      <th>2222</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>why am I not surprised</td>
    </tr>
    <tr>
      <th>2223</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>I've had this happen to friends before, but go...</td>
    </tr>
    <tr>
      <th>2224</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>Sux</td>
    </tr>
    <tr>
      <th>2225</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>sue them</td>
    </tr>
    <tr>
      <th>2226</th>
      <td>'Subway sandwich' food allergy</td>
      <td>1xfn5g</td>
      <td>all</td>
      <td>1.391985e+09</td>
      <td>Subway Takes Chemical Out of Sandwich Bread Af...</td>
      <td>17</td>
      <td>http://grist.org/list/subway-removes-yoga-mat-...</td>
      <td>0</td>
      <td>http://grist.org/list/subway-removes-yoga-mat-...</td>
      <td>grist.org</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2227</th>
      <td>KFC e. coli</td>
      <td>1eq6hg</td>
      <td>all</td>
      <td>1.369120e+09</td>
      <td>KFC gave me E. Coli.</td>
      <td>8</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>&gt; but the local news shared their information ...</td>
    </tr>
    <tr>
      <th>2228</th>
      <td>KFC e. coli</td>
      <td>16fk6p</td>
      <td>all</td>
      <td>1.358014e+09</td>
      <td>An outbreak of E. coli-related illnesses that ...</td>
      <td>2</td>
      <td>http://www.grainews.ca/news/e-coli-probes-focu...</td>
      <td>0</td>
      <td>http://www.grainews.ca/news/e-coli-probes-focu...</td>
      <td>grainews.ca</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2229</th>
      <td>KFC salmonella</td>
      <td>suuhx</td>
      <td>all</td>
      <td>1.335531e+09</td>
      <td>KFC ordered to pay $8 million to salmonella po...</td>
      <td>19</td>
      <td>http://www.smh.com.au/nsw/kfc-ordered-to-pay-8...</td>
      <td>9</td>
      <td>http://www.smh.com.au/nsw/kfc-ordered-to-pay-8...</td>
      <td>smh.com.au</td>
      <td>Still awaiting reports from Austlii/LexusNexus...</td>
    </tr>
    <tr>
      <th>2230</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>[deleted]</td>
    </tr>
    <tr>
      <th>2231</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>She wouldn't have a chance in hell if this was...</td>
    </tr>
    <tr>
      <th>2232</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>[deleted]</td>
    </tr>
    <tr>
      <th>2233</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>I don't completelpely trust alternet.</td>
    </tr>
    <tr>
      <th>2234</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>Something is afoul with this story.</td>
    </tr>
    <tr>
      <th>2235</th>
      <td>KFC salmonella</td>
      <td>106nxu</td>
      <td>all</td>
      <td>1.348162e+09</td>
      <td>KFC appeals the verdict which awarded a Sydney...</td>
      <td>1</td>
      <td>http://news.smh.com.au/breaking-news-national/...</td>
      <td>0</td>
      <td>http://news.smh.com.au/breaking-news-national/...</td>
      <td>news.smh.com.au</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>2236 rows × 11 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2236 entries, 0 to 2235
    Data columns (total 11 columns):
    Keyword                      2236 non-null object
    Submission ID                2236 non-null object
    Subreddit                    2236 non-null object
    Created Date                 2236 non-null float64
    Submission Title             2236 non-null object
    Submission Score             2236 non-null int64
    Submission URL               2236 non-null object
    Total Submission Comments    2236 non-null int64
    Submission URL               2236 non-null object
    Domain                       2236 non-null object
    Submission Comments          1834 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 209.6+ KB



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
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>[removed]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.replace("[removed]", pd.np.nan, inplace=True)
reddit_comments_df.replace("[deleted]", pd.np.nan, inplace=True)
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df = reddit_comments_df.dropna()
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Personal anecdote. Every time I had been to Ch...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df = reddit_comments_df.reset_index()
del reddit_comments_df['index']
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Personal anecdote. Every time I had been to Ch...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1774 entries, 0 to 1773
    Data columns (total 11 columns):
    Keyword                      1774 non-null object
    Submission ID                1774 non-null object
    Subreddit                    1774 non-null object
    Created Date                 1774 non-null float64
    Submission Title             1774 non-null object
    Submission Score             1774 non-null int64
    Submission URL               1774 non-null object
    Total Submission Comments    1774 non-null int64
    Submission URL               1774 non-null object
    Domain                       1774 non-null object
    Submission Comments          1774 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 152.5+ KB



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
#reddit_comments_df['Created Date'] = reddit_comments_df['Created Date'].dt.strftime('%m/%d/%Y')

#reddit_comments_df.head()
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
      <td>-0.9087</td>
      <td>0.000</td>
      <td>0.241</td>
      <td>0.759</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
      <td>-0.9490</td>
      <td>0.042</td>
      <td>0.384</td>
      <td>0.575</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
      <td>0.1124</td>
      <td>0.108</td>
      <td>0.086</td>
      <td>0.805</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
      <td>-0.2023</td>
      <td>0.000</td>
      <td>0.043</td>
      <td>0.957</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Personal anecdote. Every time I had been to Ch...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.061</td>
      <td>0.939</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df['Keyword'].value_counts()
```




    Chipotle e. coli                1021
    Chipotle Norovirus               310
    Chipotle food poisoning          140
    Costco e. coli                    72
    Chipotle foodborne illness        62
    Taco Bell food poisoning          40
    Burger King e. coli               38
    Chipotle salmonella               30
    Panda Express food poisoning      11
    Popeyes food poisoning             9
    Costco salmonella                  7
    Burger King food poisoning         6
    Costco food poisoning              6
    Burger King salmonella             6
    Taco Bell e. coli                  6
    Taco Bell salmonella               5
    KFC salmonella                     4
    KFC e. coli                        1
    Name: Keyword, dtype: int64




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
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
      <td>-0.9087</td>
      <td>0.000</td>
      <td>0.241</td>
      <td>0.759</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
      <td>-0.9490</td>
      <td>0.042</td>
      <td>0.384</td>
      <td>0.575</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
      <td>0.1124</td>
      <td>0.108</td>
      <td>0.086</td>
      <td>0.805</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
      <td>-0.2023</td>
      <td>0.000</td>
      <td>0.043</td>
      <td>0.957</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Personal anecdote. Every time I had been to Ch...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.061</td>
      <td>0.939</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>This has got to be hell for employees.  There ...</td>
      <td>0.1896</td>
      <td>0.129</td>
      <td>0.086</td>
      <td>0.786</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I have been following this since the beginning...</td>
      <td>0.6349</td>
      <td>0.082</td>
      <td>0.000</td>
      <td>0.918</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I've watched people at chipotle pour new meat,...</td>
      <td>-0.2528</td>
      <td>0.040</td>
      <td>0.068</td>
      <td>0.892</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>They don't open till 11am. You can coordinate ...</td>
      <td>-0.5244</td>
      <td>0.143</td>
      <td>0.180</td>
      <td>0.677</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I bet they order Chinese for that company-wide...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I used to work at chipotle. Our store had fail...</td>
      <td>-0.6822</td>
      <td>0.043</td>
      <td>0.148</td>
      <td>0.809</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I don't eat there anymore not because of food ...</td>
      <td>-0.3182</td>
      <td>0.133</td>
      <td>0.154</td>
      <td>0.713</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I like how their come back plan was more marke...</td>
      <td>0.3612</td>
      <td>0.128</td>
      <td>0.000</td>
      <td>0.872</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Chi chi's went bankrupt after a Hepatitis A ou...</td>
      <td>-0.5574</td>
      <td>0.000</td>
      <td>0.375</td>
      <td>0.625</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I stopped eating there long before this.\n\n1....</td>
      <td>-0.7557</td>
      <td>0.073</td>
      <td>0.141</td>
      <td>0.786</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I ate at a Seattle store 2 hours before they c...</td>
      <td>-0.1447</td>
      <td>0.056</td>
      <td>0.087</td>
      <td>0.857</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I went to Chipotle the other day and the guy c...</td>
      <td>-0.5574</td>
      <td>0.000</td>
      <td>0.223</td>
      <td>0.777</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I already stopped eating there because they we...</td>
      <td>-0.6840</td>
      <td>0.043</td>
      <td>0.163</td>
      <td>0.794</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>The 30% hit could also be because they charge ...</td>
      <td>-0.7337</td>
      <td>0.035</td>
      <td>0.113</td>
      <td>0.852</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I hope Baja Fresh comes back.</td>
      <td>0.6369</td>
      <td>0.634</td>
      <td>0.000</td>
      <td>0.366</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Which is why I've been going there more often....</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I have converted to eating at Qdoba now.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I still go every week, and its been night and ...</td>
      <td>0.2263</td>
      <td>0.079</td>
      <td>0.000</td>
      <td>0.921</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>They still have my business. I just love the w...</td>
      <td>0.6369</td>
      <td>0.276</td>
      <td>0.000</td>
      <td>0.724</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>What happened to Chipotle is the same thing th...</td>
      <td>0.9639</td>
      <td>0.138</td>
      <td>0.033</td>
      <td>0.828</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I make up 3% of chipotles annual sales. They b...</td>
      <td>0.7026</td>
      <td>0.309</td>
      <td>0.000</td>
      <td>0.691</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Pancheros is so much better</td>
      <td>0.4902</td>
      <td>0.443</td>
      <td>0.000</td>
      <td>0.557</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I knew Pancheros was better !</td>
      <td>0.4926</td>
      <td>0.516</td>
      <td>0.000</td>
      <td>0.484</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>What good will closing the stores do if the ta...</td>
      <td>0.0276</td>
      <td>0.113</td>
      <td>0.109</td>
      <td>0.778</td>
      <td>2016-01-15 21:50:42</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I love Chipotle ever since that news broke. Th...</td>
      <td>0.3400</td>
      <td>0.150</td>
      <td>0.100</td>
      <td>0.750</td>
      <td>2016-01-15 21:50:42</td>
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
      <th>1744</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>Almost all chicken you get in America has Salm...</td>
      <td>0.2732</td>
      <td>0.095</td>
      <td>0.000</td>
      <td>0.905</td>
      <td>2013-10-14 09:13:19</td>
    </tr>
    <tr>
      <th>1745</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>GET THIS:\n\nNob Hill (Raley's) is being told ...</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.149</td>
      <td>0.851</td>
      <td>2013-10-14 09:13:19</td>
    </tr>
    <tr>
      <th>1746</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>As long as the hot dogs are fine, I'm ok.</td>
      <td>0.4588</td>
      <td>0.333</td>
      <td>0.000</td>
      <td>0.667</td>
      <td>2013-10-14 09:13:19</td>
    </tr>
    <tr>
      <th>1747</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>Well, salmonella is "always natural, always fr...</td>
      <td>0.5574</td>
      <td>0.434</td>
      <td>0.000</td>
      <td>0.566</td>
      <td>2013-10-14 09:13:19</td>
    </tr>
    <tr>
      <th>1748</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>ah poop</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2013-10-14 09:13:19</td>
    </tr>
    <tr>
      <th>1749</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>It's very hard to prove the source of your ill...</td>
      <td>-0.5256</td>
      <td>0.000</td>
      <td>0.149</td>
      <td>0.851</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1750</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Idk I think I’m still gonna go</td>
      <td>-0.1027</td>
      <td>0.000</td>
      <td>0.219</td>
      <td>0.781</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1751</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>The one on East Ridge has rats so I'm not surp...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1752</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Love me some Golden Ponds.</td>
      <td>0.6369</td>
      <td>0.512</td>
      <td>0.000</td>
      <td>0.488</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1753</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>This isn't going to be good for business.\n/se...</td>
      <td>0.4404</td>
      <td>0.266</td>
      <td>0.000</td>
      <td>0.734</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1754</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>[I'm surprised they didn't run out of chicken....</td>
      <td>0.2263</td>
      <td>0.213</td>
      <td>0.000</td>
      <td>0.787</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1755</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Take the $11 loss</td>
      <td>-0.3182</td>
      <td>0.000</td>
      <td>0.434</td>
      <td>0.566</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1756</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>If you are concerned, call the [Monroe County ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1757</th>
      <td>Popeyes food poisoning</td>
      <td>7n9hmg</td>
      <td>all</td>
      <td>1.514768e+09</td>
      <td>Food poisoning from Popeyes's In Henrietta</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/Rochester/comments/7n...</td>
      <td>self.Rochester</td>
      <td>Lol. If I went to the hospital/a doctor and ha...</td>
      <td>0.4215</td>
      <td>0.085</td>
      <td>0.000</td>
      <td>0.915</td>
      <td>2018-01-01 00:51:07</td>
    </tr>
    <tr>
      <th>1758</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>I got broads in Atlanta...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1759</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>Don't fuck around with food poisoning, if it d...</td>
      <td>-0.4104</td>
      <td>0.114</td>
      <td>0.138</td>
      <td>0.748</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1760</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>You're lucky, all Panda ever gives me is a box...</td>
      <td>0.4215</td>
      <td>0.141</td>
      <td>0.000</td>
      <td>0.859</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1761</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>Not the panda you're talking about, but still,...</td>
      <td>-0.4215</td>
      <td>0.000</td>
      <td>0.167</td>
      <td>0.833</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1762</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>I got food poisoning from a place called \n\nW...</td>
      <td>-0.2263</td>
      <td>0.174</td>
      <td>0.228</td>
      <td>0.599</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1763</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>i don't even care i will never stop eating pan...</td>
      <td>-0.1877</td>
      <td>0.164</td>
      <td>0.228</td>
      <td>0.608</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1764</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>"Panda express isnt *that* bad" said my friend...</td>
      <td>0.8338</td>
      <td>0.447</td>
      <td>0.117</td>
      <td>0.436</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1765</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>why am I not surprised</td>
      <td>-0.1695</td>
      <td>0.000</td>
      <td>0.357</td>
      <td>0.643</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1766</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>I've had this happen to friends before, but go...</td>
      <td>0.7876</td>
      <td>0.403</td>
      <td>0.136</td>
      <td>0.461</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1767</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>Sux</td>
      <td>-0.3612</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1768</th>
      <td>Panda Express food poisoning</td>
      <td>4dzut5</td>
      <td>all</td>
      <td>1.460202e+09</td>
      <td>Panda express gave me food poisoning</td>
      <td>27</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/teenagers/comments/4d...</td>
      <td>self.teenagers</td>
      <td>sue them</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-04-09 11:36:26</td>
    </tr>
    <tr>
      <th>1769</th>
      <td>KFC e. coli</td>
      <td>1eq6hg</td>
      <td>all</td>
      <td>1.369120e+09</td>
      <td>KFC gave me E. Coli.</td>
      <td>8</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>&gt; but the local news shared their information ...</td>
      <td>0.9599</td>
      <td>0.161</td>
      <td>0.105</td>
      <td>0.734</td>
      <td>2013-05-21 07:14:48</td>
    </tr>
    <tr>
      <th>1770</th>
      <td>KFC salmonella</td>
      <td>suuhx</td>
      <td>all</td>
      <td>1.335531e+09</td>
      <td>KFC ordered to pay $8 million to salmonella po...</td>
      <td>19</td>
      <td>http://www.smh.com.au/nsw/kfc-ordered-to-pay-8...</td>
      <td>9</td>
      <td>http://www.smh.com.au/nsw/kfc-ordered-to-pay-8...</td>
      <td>smh.com.au</td>
      <td>Still awaiting reports from Austlii/LexusNexus...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2012-04-27 12:56:22</td>
    </tr>
    <tr>
      <th>1771</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>She wouldn't have a chance in hell if this was...</td>
      <td>-0.7461</td>
      <td>0.000</td>
      <td>0.413</td>
      <td>0.587</td>
      <td>2012-04-29 01:40:47</td>
    </tr>
    <tr>
      <th>1772</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>I don't completelpely trust alternet.</td>
      <td>-0.4023</td>
      <td>0.000</td>
      <td>0.474</td>
      <td>0.526</td>
      <td>2012-04-29 01:40:47</td>
    </tr>
    <tr>
      <th>1773</th>
      <td>KFC salmonella</td>
      <td>swzyk</td>
      <td>all</td>
      <td>1.335664e+09</td>
      <td>KFC Ordered to Pay $8.3 Million to Australian ...</td>
      <td>80</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>22</td>
      <td>http://www.alternet.org/food/155180/kfc_ordere...</td>
      <td>alternet.org</td>
      <td>Something is afoul with this story.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2012-04-29 01:40:47</td>
    </tr>
  </tbody>
</table>
<p>1774 rows × 16 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1774 entries, 0 to 1773
    Data columns (total 16 columns):
    Keyword                      1774 non-null object
    Submission ID                1774 non-null object
    Subreddit                    1774 non-null object
    Created Date                 1774 non-null float64
    Submission Title             1774 non-null object
    Submission Score             1774 non-null int64
    Submission URL               1774 non-null object
    Total Submission Comments    1774 non-null int64
    Submission URL               1774 non-null object
    Domain                       1774 non-null object
    Submission Comments          1774 non-null object
    Compound Score               1774 non-null float64
    Positive Score               1774 non-null float64
    Negative Score               1774 non-null float64
    Neutral Score                1774 non-null float64
    Date                         1774 non-null datetime64[ns]
    dtypes: datetime64[ns](1), float64(5), int64(2), object(8)
    memory usage: 221.8+ KB



```python
reddit_comments_df['Date'][0].year
```




    2016




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
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I mentioned this in a similar thread, but requ...</td>
      <td>-0.9087</td>
      <td>0.000</td>
      <td>0.241</td>
      <td>0.759</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>How about not punishing/ firing employees for ...</td>
      <td>-0.9490</td>
      <td>0.042</td>
      <td>0.384</td>
      <td>0.575</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>I think their flailing hurt them as bad as the...</td>
      <td>0.1124</td>
      <td>0.108</td>
      <td>0.086</td>
      <td>0.805</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>A Chipotle just opened up a few months ago rig...</td>
      <td>-0.2023</td>
      <td>0.000</td>
      <td>0.043</td>
      <td>0.957</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2154</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
      <td>Personal anecdote. Every time I had been to Ch...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.061</td>
      <td>0.939</td>
      <td>2016</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.to_csv("combined_kws.csv",
                     encoding="utf-8", index=False)
```


```python
#grouped_df5 = reddit_comments_df.groupby('Keyword')['Compound Score'].mean()
```


```python
year_2015_df = reddit_comments_df.loc[reddit_comments_df["Date"] == 2015,:]
year_2015_df.head()
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
      <th>70</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>I keep kosher, so I'm ignorant, but isn't it s...</td>
      <td>0.7992</td>
      <td>0.307</td>
      <td>0.066</td>
      <td>0.627</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Expert here. Try substituting Taco Del Mar a c...</td>
      <td>0.3612</td>
      <td>0.082</td>
      <td>0.000</td>
      <td>0.918</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Why would you *want* food poisoning?</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>0.432</td>
      <td>0.568</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You must be really rich or very stupid</td>
      <td>0.0516</td>
      <td>0.287</td>
      <td>0.272</td>
      <td>0.442</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>And hows that going?</td>
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
year_2015_df = year_2015_df.reset_index()
del year_2015_df['index']
year_2015_df
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
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>I keep kosher, so I'm ignorant, but isn't it s...</td>
      <td>0.7992</td>
      <td>0.307</td>
      <td>0.066</td>
      <td>0.627</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Expert here. Try substituting Taco Del Mar a c...</td>
      <td>0.3612</td>
      <td>0.082</td>
      <td>0.000</td>
      <td>0.918</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Why would you *want* food poisoning?</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>0.432</td>
      <td>0.568</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You must be really rich or very stupid</td>
      <td>0.0516</td>
      <td>0.287</td>
      <td>0.272</td>
      <td>0.442</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle food poisoning</td>
      <td>3xvhi7</td>
      <td>all</td>
      <td>1.450844e+09</td>
      <td>I go to Chipotle at least twice a week hoping ...</td>
      <td>121</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>And hows that going?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle food poisoning</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>123</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>124</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle food poisoning</td>
      <td>3peld0</td>
      <td>all</td>
      <td>1.445318e+09</td>
      <td>Wife and I got food poisoning from Chipotle on...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/FortCollins/comments/...</td>
      <td>27</td>
      <td>https://www.reddit.com/r/FortCollins/comments/...</td>
      <td>self.FortCollins</td>
      <td>How long after eating it did you start experie...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
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
      <th>744</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>You should have kept it but you can't change t...</td>
      <td>-0.9834</td>
      <td>0.000</td>
      <td>0.209</td>
      <td>0.791</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>745</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>*I am a bot whose sole purpose is to improve t...</td>
      <td>0.8738</td>
      <td>0.116</td>
      <td>0.050</td>
      <td>0.834</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>746</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Do you have any of the sandwiches left (refrig...</td>
      <td>0.8412</td>
      <td>0.118</td>
      <td>0.045</td>
      <td>0.836</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>747</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Not a lawyer, but I am a microbiologist in the...</td>
      <td>0.6939</td>
      <td>0.086</td>
      <td>0.069</td>
      <td>0.846</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>748</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Call your local county board of health. This i...</td>
      <td>0.1280</td>
      <td>0.078</td>
      <td>0.067</td>
      <td>0.855</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>749</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>How were these sandwiches stored before the ga...</td>
      <td>0.4696</td>
      <td>0.117</td>
      <td>0.000</td>
      <td>0.883</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>750</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>This reminds me a lot of a pot luck gone bad i...</td>
      <td>-0.1513</td>
      <td>0.061</td>
      <td>0.059</td>
      <td>0.880</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>751</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>20</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Call DEC or the board of health in your hometo...</td>
      <td>-0.1531</td>
      <td>0.000</td>
      <td>0.049</td>
      <td>0.951</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>752</th>
      <td>Costco e. coli</td>
      <td>3u5oif</td>
      <td>all</td>
      <td>1.448444e+09</td>
      <td>CDC says at least 19 E. coli infections linked...</td>
      <td>112</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>9</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>reuters.com</td>
      <td>My bet is on the celery being contaminated.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>753</th>
      <td>Costco e. coli</td>
      <td>3u5oif</td>
      <td>all</td>
      <td>1.448444e+09</td>
      <td>CDC says at least 19 E. coli infections linked...</td>
      <td>112</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>9</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>reuters.com</td>
      <td>When I first heard about it I though it was th...</td>
      <td>0.6369</td>
      <td>0.231</td>
      <td>0.000</td>
      <td>0.769</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>754</th>
      <td>Costco e. coli</td>
      <td>3u5oif</td>
      <td>all</td>
      <td>1.448444e+09</td>
      <td>CDC says at least 19 E. coli infections linked...</td>
      <td>112</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>9</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>reuters.com</td>
      <td>19 out of 350,000,000. It's the end of the wor...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>755</th>
      <td>Costco e. coli</td>
      <td>3u5oif</td>
      <td>all</td>
      <td>1.448444e+09</td>
      <td>CDC says at least 19 E. coli infections linked...</td>
      <td>112</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>9</td>
      <td>http://www.reuters.com/article/2015/11/24/us-c...</td>
      <td>reuters.com</td>
      <td>~~i had something of theirs recently, for the ...</td>
      <td>-0.3612</td>
      <td>0.027</td>
      <td>0.054</td>
      <td>0.919</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>756</th>
      <td>Costco e. coli</td>
      <td>3uexbx</td>
      <td>all</td>
      <td>1.448617e+09</td>
      <td>Taylor Farms Celery Recalled After Link To Cos...</td>
      <td>53</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>8</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>sacramento.cbslocal.com</td>
      <td>How terrible must it feel to know you got E. C...</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.193</td>
      <td>0.807</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>757</th>
      <td>Costco e. coli</td>
      <td>3uexbx</td>
      <td>all</td>
      <td>1.448617e+09</td>
      <td>Taylor Farms Celery Recalled After Link To Cos...</td>
      <td>53</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>8</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>sacramento.cbslocal.com</td>
      <td>hellofafuckingday for this.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>758</th>
      <td>Costco e. coli</td>
      <td>3uexbx</td>
      <td>all</td>
      <td>1.448617e+09</td>
      <td>Taylor Farms Celery Recalled After Link To Cos...</td>
      <td>53</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>8</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>sacramento.cbslocal.com</td>
      <td>Crapping in the fields.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>759</th>
      <td>Costco e. coli</td>
      <td>3uexbx</td>
      <td>all</td>
      <td>1.448617e+09</td>
      <td>Taylor Farms Celery Recalled After Link To Cos...</td>
      <td>53</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>8</td>
      <td>http://sacramento.cbslocal.com/2015/11/26/tayl...</td>
      <td>sacramento.cbslocal.com</td>
      <td>Good glob, I hate celery so much. This just pe...</td>
      <td>-0.8555</td>
      <td>0.115</td>
      <td>0.448</td>
      <td>0.437</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>760</th>
      <td>Costco e. coli</td>
      <td>3u3sdg</td>
      <td>all</td>
      <td>1.448417e+09</td>
      <td>E. coli infections linked to Costco chicken salad</td>
      <td>35</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>9</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>cnn.com</td>
      <td>Well, TIL you can buy E. coli in bulk. Costco ...</td>
      <td>0.2732</td>
      <td>0.139</td>
      <td>0.000</td>
      <td>0.861</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>761</th>
      <td>Costco e. coli</td>
      <td>3u3sdg</td>
      <td>all</td>
      <td>1.448417e+09</td>
      <td>E. coli infections linked to Costco chicken salad</td>
      <td>35</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>9</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>cnn.com</td>
      <td>Soon on the front page will be a post about ho...</td>
      <td>0.6249</td>
      <td>0.255</td>
      <td>0.000</td>
      <td>0.745</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>762</th>
      <td>Costco e. coli</td>
      <td>3u3sdg</td>
      <td>all</td>
      <td>1.448417e+09</td>
      <td>E. coli infections linked to Costco chicken salad</td>
      <td>35</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>9</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>cnn.com</td>
      <td>Not surprised.  What they do is sell those Chi...</td>
      <td>0.5859</td>
      <td>0.076</td>
      <td>0.000</td>
      <td>0.924</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>763</th>
      <td>Costco e. coli</td>
      <td>3u3sdg</td>
      <td>all</td>
      <td>1.448417e+09</td>
      <td>E. coli infections linked to Costco chicken salad</td>
      <td>35</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>9</td>
      <td>http://www.cnn.com/2015/11/24/health/e-coli-co...</td>
      <td>cnn.com</td>
      <td>I eat their chicken Caesar salad for lunch lik...</td>
      <td>0.7579</td>
      <td>0.292</td>
      <td>0.091</td>
      <td>0.617</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>764</th>
      <td>Costco e. coli</td>
      <td>3u8je8</td>
      <td>all</td>
      <td>1.448500e+09</td>
      <td>Multi-state E. coli outbreak linked to Costco'...</td>
      <td>29</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>8</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>consumeraffairs.com</td>
      <td>I will say that this is no joke. I now know my...</td>
      <td>0.9418</td>
      <td>0.212</td>
      <td>0.056</td>
      <td>0.733</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>765</th>
      <td>Costco e. coli</td>
      <td>3u8je8</td>
      <td>all</td>
      <td>1.448500e+09</td>
      <td>Multi-state E. coli outbreak linked to Costco'...</td>
      <td>29</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>8</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>consumeraffairs.com</td>
      <td>Their food taste like crap anyways. You ever h...</td>
      <td>-0.0258</td>
      <td>0.155</td>
      <td>0.161</td>
      <td>0.683</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>766</th>
      <td>Costco e. coli</td>
      <td>3u4pvo</td>
      <td>all</td>
      <td>1.448429e+09</td>
      <td>More E-Coli News: This Time, Costco (COST)</td>
      <td>6</td>
      <td>https://www.reddit.com/r/investing/comments/3u...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/investing/comments/3u...</td>
      <td>self.investing</td>
      <td>Damn, I just bought and ate some costco rotiss...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.252</td>
      <td>0.748</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>767</th>
      <td>Costco e. coli</td>
      <td>3v8ax5</td>
      <td>all</td>
      <td>1.449140e+09</td>
      <td>FDA Expands Recall of Food Items for E.Coli to...</td>
      <td>28</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>3</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>cnbc.com</td>
      <td>It's celery and things that contain celery. Do...</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.147</td>
      <td>0.853</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>768</th>
      <td>Costco e. coli</td>
      <td>3v8ax5</td>
      <td>all</td>
      <td>1.449140e+09</td>
      <td>FDA Expands Recall of Food Items for E.Coli to...</td>
      <td>28</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>3</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>cnbc.com</td>
      <td>So, wait. 7-11 is considered a Major Grocery S...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>769</th>
      <td>Costco e. coli</td>
      <td>3u4pjf</td>
      <td>all</td>
      <td>1.448429e+09</td>
      <td>Missouri Costco stores may have sold E. Coli-t...</td>
      <td>18</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>2</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>kctv5.com</td>
      <td>I'll still eat it.  That shit is delicious.</td>
      <td>0.0258</td>
      <td>0.278</td>
      <td>0.271</td>
      <td>0.451</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>770</th>
      <td>Costco e. coli</td>
      <td>3u4pjf</td>
      <td>all</td>
      <td>1.448429e+09</td>
      <td>Missouri Costco stores may have sold E. Coli-t...</td>
      <td>18</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>2</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>kctv5.com</td>
      <td>Boop Boop tainted cluck, whoaaaooo</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>771</th>
      <td>Costco e. coli</td>
      <td>3uv57m</td>
      <td>all</td>
      <td>1.448928e+09</td>
      <td>[US - AZ] I believe I was infected by the E. C...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Start by contacting Costco and asking them wha...</td>
      <td>0.4927</td>
      <td>0.071</td>
      <td>0.000</td>
      <td>0.929</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>772</th>
      <td>Costco e. coli</td>
      <td>3uv57m</td>
      <td>all</td>
      <td>1.448928e+09</td>
      <td>[US - AZ] I believe I was infected by the E. C...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>To the best of my knowledge Costco's food cour...</td>
      <td>0.6369</td>
      <td>0.144</td>
      <td>0.000</td>
      <td>0.856</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>773</th>
      <td>Costco e. coli</td>
      <td>3uv57m</td>
      <td>all</td>
      <td>1.448928e+09</td>
      <td>[US - AZ] I believe I was infected by the E. C...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>I got food poisoning from Costco a few years b...</td>
      <td>-0.9185</td>
      <td>0.042</td>
      <td>0.063</td>
      <td>0.895</td>
      <td>2015</td>
    </tr>
  </tbody>
</table>
<p>774 rows × 16 columns</p>
</div>




```python
year_2015_df = year_2015_df.groupby(['Keyword','Submission ID','Created Date'])
```


```python
year_2015_df.count().head()
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
      <th>Burger King salmonella</th>
      <th>3wqd6v</th>
      <th>1.450090e+09</th>
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
      <th rowspan="4" valign="top">Chipotle Norovirus</th>
      <th>3vyt7n</th>
      <th>1.449631e+09</th>
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
      <th>3vzn5g</th>
      <th>1.449642e+09</th>
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
      <th>3w00k9</th>
      <th>1.449647e+09</th>
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
    <tr>
      <th>3w0vnt</th>
      <th>1.449660e+09</th>
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
  </tbody>
</table>
</div>




```python
year_2015_df = pd.DataFrame(year_2015_df["Compound Score"].mean())
year_2015_df
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
      <th>Burger King salmonella</th>
      <th>3wqd6v</th>
      <th>1.450090e+09</th>
      <td>-0.207367</td>
    </tr>
    <tr>
      <th rowspan="7" valign="top">Chipotle Norovirus</th>
      <th>3vyt7n</th>
      <th>1.449631e+09</th>
      <td>0.419900</td>
    </tr>
    <tr>
      <th>3vzn5g</th>
      <th>1.449642e+09</th>
      <td>-0.702750</td>
    </tr>
    <tr>
      <th>3w00k9</th>
      <th>1.449647e+09</th>
      <td>-0.291514</td>
    </tr>
    <tr>
      <th>3w0vnt</th>
      <th>1.449660e+09</th>
      <td>-0.913600</td>
    </tr>
    <tr>
      <th>3w97ya</th>
      <th>1.449800e+09</th>
      <td>-0.985800</td>
    </tr>
    <tr>
      <th>3wk9b4</th>
      <th>1.449984e+09</th>
      <td>-0.169975</td>
    </tr>
    <tr>
      <th>3wy61m</th>
      <th>1.450222e+09</th>
      <td>-0.230189</td>
    </tr>
    <tr>
      <th rowspan="27" valign="top">Chipotle e. coli</th>
      <th>3qz0mu</th>
      <th>1.446333e+09</th>
      <td>-0.190830</td>
    </tr>
    <tr>
      <th>3qz2qk</th>
      <th>1.446334e+09</th>
      <td>0.040069</td>
    </tr>
    <tr>
      <th>3qzjqg</th>
      <th>1.446342e+09</th>
      <td>0.014560</td>
    </tr>
    <tr>
      <th>3qzk26</th>
      <th>1.446342e+09</th>
      <td>-0.273114</td>
    </tr>
    <tr>
      <th>3qzk5h</th>
      <th>1.446342e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3qzk5i</th>
      <th>1.446342e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3qzo9r</th>
      <th>1.446344e+09</th>
      <td>-0.032950</td>
    </tr>
    <tr>
      <th>3qzw81</th>
      <th>1.446347e+09</th>
      <td>-0.126171</td>
    </tr>
    <tr>
      <th>3r0up6</th>
      <th>1.446362e+09</th>
      <td>-0.094300</td>
    </tr>
    <tr>
      <th>3r12ny</th>
      <th>1.446366e+09</th>
      <td>-0.193700</td>
    </tr>
    <tr>
      <th>3r1loy</th>
      <th>1.446377e+09</th>
      <td>0.036429</td>
    </tr>
    <tr>
      <th>3r23nk</th>
      <th>1.446390e+09</th>
      <td>-0.920000</td>
    </tr>
    <tr>
      <th>3r4elr</th>
      <th>1.446439e+09</th>
      <td>-0.072033</td>
    </tr>
    <tr>
      <th>3r5o9y</th>
      <th>1.446458e+09</th>
      <td>-0.024167</td>
    </tr>
    <tr>
      <th>3r5pll</th>
      <th>1.446459e+09</th>
      <td>0.273200</td>
    </tr>
    <tr>
      <th>3r6dh8</th>
      <th>1.446471e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3r6dqt</th>
      <th>1.446471e+09</th>
      <td>0.636900</td>
    </tr>
    <tr>
      <th>3r7izn</th>
      <th>1.446500e+09</th>
      <td>-0.272200</td>
    </tr>
    <tr>
      <th>3r7wvw</th>
      <th>1.446507e+09</th>
      <td>-0.037773</td>
    </tr>
    <tr>
      <th>3r8edx</th>
      <th>1.446514e+09</th>
      <td>0.062708</td>
    </tr>
    <tr>
      <th>3r8evk</th>
      <th>1.446514e+09</th>
      <td>-0.735100</td>
    </tr>
    <tr>
      <th>3r9cyl</th>
      <th>1.446526e+09</th>
      <td>0.318200</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>3y4ugx</th>
      <th>1.451032e+09</th>
      <td>-0.680800</td>
    </tr>
    <tr>
      <th>3y728k</th>
      <th>1.451092e+09</th>
      <td>-0.425687</td>
    </tr>
    <tr>
      <th>3yngoe</th>
      <th>1.451423e+09</th>
      <td>-0.589100</td>
    </tr>
    <tr>
      <th>3yv9s3</th>
      <th>1.451562e+09</th>
      <td>0.832933</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">Chipotle food poisoning</th>
      <th>304vlw</th>
      <th>1.427237e+09</th>
      <td>0.476650</td>
    </tr>
    <tr>
      <th>3peld0</th>
      <th>1.445318e+09</th>
      <td>0.225900</td>
    </tr>
    <tr>
      <th>3rf75z</th>
      <th>1.446623e+09</th>
      <td>-0.565050</td>
    </tr>
    <tr>
      <th>3tn4ko</th>
      <th>1.448099e+09</th>
      <td>0.381800</td>
    </tr>
    <tr>
      <th>3vhh7u</th>
      <th>1.449305e+09</th>
      <td>0.119500</td>
    </tr>
    <tr>
      <th>3w6drp</th>
      <th>1.449751e+09</th>
      <td>0.170500</td>
    </tr>
    <tr>
      <th>3xvhi7</th>
      <th>1.450844e+09</th>
      <td>0.125220</td>
    </tr>
    <tr>
      <th>3yty74</th>
      <th>1.451539e+09</th>
      <td>-0.165100</td>
    </tr>
    <tr>
      <th rowspan="7" valign="top">Chipotle salmonella</th>
      <th>3khsjo</th>
      <th>1.441969e+09</th>
      <td>-0.585900</td>
    </tr>
    <tr>
      <th>3khtjo</th>
      <th>1.441969e+09</th>
      <td>-0.045167</td>
    </tr>
    <tr>
      <th>3kji7g</th>
      <th>1.442008e+09</th>
      <td>-0.192500</td>
    </tr>
    <tr>
      <th>3kmigm</th>
      <th>1.442056e+09</th>
      <td>0.329850</td>
    </tr>
    <tr>
      <th>3l8vwn</th>
      <th>1.442482e+09</th>
      <td>0.089067</td>
    </tr>
    <tr>
      <th>3laxcl</th>
      <th>1.442527e+09</th>
      <td>-0.046429</td>
    </tr>
    <tr>
      <th>3lb0n3</th>
      <th>1.442529e+09</th>
      <td>-0.030667</td>
    </tr>
    <tr>
      <th rowspan="9" valign="top">Costco e. coli</th>
      <th>3u3sdg</th>
      <th>1.448417e+09</th>
      <td>0.560475</td>
    </tr>
    <tr>
      <th>3u4pjf</th>
      <th>1.448429e+09</th>
      <td>0.012900</td>
    </tr>
    <tr>
      <th>3u4pvo</th>
      <th>1.448429e+09</th>
      <td>-0.401900</td>
    </tr>
    <tr>
      <th>3u5oif</th>
      <th>1.448444e+09</th>
      <td>0.068925</td>
    </tr>
    <tr>
      <th>3u8je8</th>
      <th>1.448500e+09</th>
      <td>0.458000</td>
    </tr>
    <tr>
      <th>3uajeq</th>
      <th>1.448531e+09</th>
      <td>0.136167</td>
    </tr>
    <tr>
      <th>3uexbx</th>
      <th>1.448617e+09</th>
      <td>-0.333050</td>
    </tr>
    <tr>
      <th>3uv57m</th>
      <th>1.448928e+09</th>
      <td>0.070367</td>
    </tr>
    <tr>
      <th>3v8ax5</th>
      <th>1.449140e+09</th>
      <td>-0.238350</td>
    </tr>
    <tr>
      <th>Costco food poisoning</th>
      <th>3l8p74</th>
      <th>1.442478e+09</th>
      <td>0.304717</td>
    </tr>
    <tr>
      <th>Taco Bell e. coli</th>
      <th>3vx31d</th>
      <th>1.449604e+09</th>
      <td>-0.334833</td>
    </tr>
  </tbody>
</table>
<p>135 rows × 1 columns</p>
</div>




```python
year_2015_df = year_2015_df.reset_index()
year_2015_df.head()
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
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>1.450090e+09</td>
      <td>-0.207367</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle Norovirus</td>
      <td>3vyt7n</td>
      <td>1.449631e+09</td>
      <td>0.419900</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle Norovirus</td>
      <td>3vzn5g</td>
      <td>1.449642e+09</td>
      <td>-0.702750</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Norovirus</td>
      <td>3w00k9</td>
      <td>1.449647e+09</td>
      <td>-0.291514</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle Norovirus</td>
      <td>3w0vnt</td>
      <td>1.449660e+09</td>
      <td>-0.913600</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', hue="Keyword", data=year_2015_df, fit_reg=False, palette="Paired")

#plt.title("Restaurant Comment Sentiments on Reddit 2015")

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

plt.savefig("Combinedkw_Sentiments_2015.png", dpi=350)

plt.show()
```


![png](output_36_0.png)



```python
reddit_comments_df.to_csv("combined_kws.csv",
                     encoding="utf-8", index=False)
```


```python
grouped_df = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "Chipotle e. coli",:]
grouped_df = grouped_df.reset_index()
del grouped_df['index']
grouped_df
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle e. coli</td>
      <td>3tn4ko</td>
      <td>all</td>
      <td>1.448099e+09</td>
      <td>More than 40 people have fallen ill with E. co...</td>
      <td>15</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>reuters.com</td>
      <td>"Food With Integrity" -- and E. Coli</td>
      <td>0.3818</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle e. coli</td>
      <td>3tn4ko</td>
      <td>all</td>
      <td>1.448099e+09</td>
      <td>More than 40 people have fallen ill with E. co...</td>
      <td>15</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>reuters.com</td>
      <td>"Food With Integrity" -- and E. Coli</td>
      <td>0.3818</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>That can't be good for business.</td>
      <td>-0.3412</td>
      <td>0.000</td>
      <td>0.325</td>
      <td>0.675</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>E-coli, is shit/feces/poop bacteria. It means ...</td>
      <td>-0.7889</td>
      <td>0.081</td>
      <td>0.140</td>
      <td>0.780</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>That can't be good for business.</td>
      <td>-0.3412</td>
      <td>0.000</td>
      <td>0.325</td>
      <td>0.675</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>E-coli, is shit/feces/poop bacteria. It means ...</td>
      <td>-0.7889</td>
      <td>0.081</td>
      <td>0.140</td>
      <td>0.780</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>So far...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Wait there were free chipotle burritos?</td>
      <td>0.5106</td>
      <td>0.398</td>
      <td>0.000</td>
      <td>0.602</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Except your bowels have billions of E. Coli.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>*Day 4: Stomach is cramping, diarrhea is preva...</td>
      <td>-0.5943</td>
      <td>0.000</td>
      <td>0.188</td>
      <td>0.812</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Chipotle worker her, was given 6 Family and Fr...</td>
      <td>0.8316</td>
      <td>0.286</td>
      <td>0.000</td>
      <td>0.714</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Currently eating free burrito. E. coli, you da...</td>
      <td>0.5106</td>
      <td>0.268</td>
      <td>0.000</td>
      <td>0.732</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Well, considering that E. coli is a model orga...</td>
      <td>0.8478</td>
      <td>0.277</td>
      <td>0.000</td>
      <td>0.723</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You have had E-coli. You have E-coli in your g...</td>
      <td>0.0382</td>
      <td>0.054</td>
      <td>0.000</td>
      <td>0.946</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You got your free burrito already!?</td>
      <td>0.5562</td>
      <td>0.418</td>
      <td>0.000</td>
      <td>0.582</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>E. Coli lives in the intestines....everyone's ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Yesterday I got a free steak bowl at Chipotle ...</td>
      <td>0.4659</td>
      <td>0.115</td>
      <td>0.000</td>
      <td>0.885</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Good guy E. coli</td>
      <td>0.4404</td>
      <td>0.492</td>
      <td>0.000</td>
      <td>0.508</td>
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
    </tr>
    <tr>
      <th>991</th>
      <td>Chipotle e. coli</td>
      <td>3v1cri</td>
      <td>all</td>
      <td>1.449027e+09</td>
      <td>Chipotle lovers in the northwest, have you ret...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/AskReddit/comments/3v...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/3v...</td>
      <td>self.AskReddit</td>
      <td>Considering buying stock?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>992</th>
      <td>Chipotle e. coli</td>
      <td>3y4ugx</td>
      <td>all</td>
      <td>1.451032e+09</td>
      <td>ANALYSIS: Chipotle is a victim of corporate sa...</td>
      <td>1</td>
      <td>http://www.naturalnews.com/052405_Chipotle_eco...</td>
      <td>2</td>
      <td>http://www.naturalnews.com/052405_Chipotle_eco...</td>
      <td>naturalnews.com</td>
      <td>This has been posted and debunked in conspirac...</td>
      <td>-0.6808</td>
      <td>0.000</td>
      <td>0.259</td>
      <td>0.741</td>
    </tr>
    <tr>
      <th>993</th>
      <td>Chipotle e. coli</td>
      <td>3u1m3b</td>
      <td>all</td>
      <td>1.448373e+09</td>
      <td>Chipotle E. coli outbreak reaches six states, ...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/20/us-c...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/20/us-c...</td>
      <td>reuters.com</td>
      <td>[Source](https://www.reddit.com/r/Chipotle/com...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>994</th>
      <td>Chipotle e. coli</td>
      <td>3tlznx</td>
      <td>all</td>
      <td>1.448081e+09</td>
      <td>CDC update on Chipotle and E. coli adds 2 more...</td>
      <td>1</td>
      <td>http://www.cdc.gov/ecoli/2015/o26-11-15/index....</td>
      <td>1</td>
      <td>http://www.cdc.gov/ecoli/2015/o26-11-15/index....</td>
      <td>cdc.gov</td>
      <td>[original submission](/r/Seattle/comments/3tly...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>995</th>
      <td>Chipotle e. coli</td>
      <td>3qzk5i</td>
      <td>all</td>
      <td>1.446342e+09</td>
      <td>22 sick from E. coli; Chipotles closed in Ore....</td>
      <td>1</td>
      <td>http://www.kgw.com/story/news/local/2015/10/31...</td>
      <td>1</td>
      <td>http://www.kgw.com/story/news/local/2015/10/31...</td>
      <td>kgw.com</td>
      <td>[original submission](/r/Seattle/comments/3qzj...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>996</th>
      <td>Chipotle e. coli</td>
      <td>3rz8fv</td>
      <td>all</td>
      <td>1.446991e+09</td>
      <td>Chipotle Shuts Restaurants in Northwest After ...</td>
      <td>1</td>
      <td>http://www.nytimes.com/2015/11/03/business/chi...</td>
      <td>1</td>
      <td>http://www.nytimes.com/2015/11/03/business/chi...</td>
      <td>nytimes.com</td>
      <td>[Source](https://www.reddit.com/r/Chipotle/com...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>997</th>
      <td>Chipotle e. coli</td>
      <td>3vzkdi</td>
      <td>all</td>
      <td>1.449641e+09</td>
      <td>ELI5: Why is the E. Coli outbreak isolated in ...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>Don't know which outbreak you mean, because it...</td>
      <td>-0.0772</td>
      <td>0.040</td>
      <td>0.044</td>
      <td>0.916</td>
    </tr>
    <tr>
      <th>998</th>
      <td>Chipotle e. coli</td>
      <td>3vzkdi</td>
      <td>all</td>
      <td>1.449641e+09</td>
      <td>ELI5: Why is the E. Coli outbreak isolated in ...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>IIRC, Chipotle wasn't the only one affected as...</td>
      <td>0.3291</td>
      <td>0.067</td>
      <td>0.061</td>
      <td>0.872</td>
    </tr>
    <tr>
      <th>999</th>
      <td>Chipotle e. coli</td>
      <td>42gp7b</td>
      <td>all</td>
      <td>1.453685e+09</td>
      <td>[/r/Showerthoughts] You can't spell Chipotle w...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>reddit.com</td>
      <td>Stats of this post when RedditFox issued the i...</td>
      <td>0.6369</td>
      <td>0.057</td>
      <td>0.000</td>
      <td>0.943</td>
    </tr>
    <tr>
      <th>1000</th>
      <td>Chipotle e. coli</td>
      <td>44yxq5</td>
      <td>all</td>
      <td>1.455081e+09</td>
      <td>What if some mastermind carefully planned and ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Taco bell did it</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1001</th>
      <td>Chipotle e. coli</td>
      <td>3rfm7d</td>
      <td>all</td>
      <td>1.446629e+09</td>
      <td>Seattle Chipotle locations part of E. coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/SeattleUnmoderated/co...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/SeattleUnmoderated/co...</td>
      <td>self.SeattleUnmoderated</td>
      <td>[original submission](/r/Seattle/comments/3rfl...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1002</th>
      <td>Chipotle e. coli</td>
      <td>3saxgt</td>
      <td>all</td>
      <td>1.447209e+09</td>
      <td>Seattle Chipotle restaurant to reopen after E....</td>
      <td>1</td>
      <td>http://www.kirotv.com/news/news/seattle-chipot...</td>
      <td>1</td>
      <td>http://www.kirotv.com/news/news/seattle-chipot...</td>
      <td>kirotv.com</td>
      <td>[original submission](/r/Seattle/comments/3sax...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1003</th>
      <td>Chipotle e. coli</td>
      <td>5gnaj3</td>
      <td>all</td>
      <td>1.480989e+09</td>
      <td>Survey for MKTG class: This is Chipotle's firs...</td>
      <td>1</td>
      <td>https://docs.google.com/forms/d/e/1FAIpQLSfVCU...</td>
      <td>1</td>
      <td>https://docs.google.com/forms/d/e/1FAIpQLSfVCU...</td>
      <td>docs.google.com</td>
      <td>You didn't have a don't know column for the pr...</td>
      <td>0.2732</td>
      <td>0.062</td>
      <td>0.000</td>
      <td>0.938</td>
    </tr>
    <tr>
      <th>1004</th>
      <td>Chipotle e. coli</td>
      <td>3r6dh8</td>
      <td>all</td>
      <td>1.446471e+09</td>
      <td>Officials anticipate more E. coli cases in Was...</td>
      <td>1</td>
      <td>http://www.seattletimes.com/seattle-news/offic...</td>
      <td>1</td>
      <td>http://www.seattletimes.com/seattle-news/offic...</td>
      <td>seattletimes.com</td>
      <td>[Google cached version](http://webcache.google...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1005</th>
      <td>Chipotle e. coli</td>
      <td>3wgcmv</td>
      <td>all</td>
      <td>1.449911e+09</td>
      <td>DAE want to eat at Chipotle more since their r...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/DoesAnybodyElse/comme...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/DoesAnybodyElse/comme...</td>
      <td>self.DoesAnybodyElse</td>
      <td>If I get sick from chipotle I'm gonna go back ...</td>
      <td>-0.8213</td>
      <td>0.000</td>
      <td>0.178</td>
      <td>0.822</td>
    </tr>
    <tr>
      <th>1006</th>
      <td>Chipotle e. coli</td>
      <td>3wgcmv</td>
      <td>all</td>
      <td>1.449911e+09</td>
      <td>DAE want to eat at Chipotle more since their r...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/DoesAnybodyElse/comme...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/DoesAnybodyElse/comme...</td>
      <td>self.DoesAnybodyElse</td>
      <td>Related: DAE miss green onions at Taco Bell?</td>
      <td>-0.1531</td>
      <td>0.000</td>
      <td>0.186</td>
      <td>0.814</td>
    </tr>
    <tr>
      <th>1007</th>
      <td>Chipotle e. coli</td>
      <td>3qzk5h</td>
      <td>all</td>
      <td>1.446342e+09</td>
      <td>Chipotles closed in Ore.and Wash. amid E. coli...</td>
      <td>1</td>
      <td>http://www.king5.com/story/news/local/2015/10/...</td>
      <td>1</td>
      <td>http://www.king5.com/story/news/local/2015/10/...</td>
      <td>king5.com</td>
      <td>[original submission](/r/Seattle/comments/3qzk...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1008</th>
      <td>Chipotle e. coli</td>
      <td>3s3tfy</td>
      <td>all</td>
      <td>1.447081e+09</td>
      <td>PSA: *ALL* WA Chipotles are closed, not just t...</td>
      <td>1</td>
      <td>http://chipotle.com/update</td>
      <td>1</td>
      <td>http://chipotle.com/update</td>
      <td>chipotle.com</td>
      <td>[original submission](/r/Seattle/comments/3s3t...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1009</th>
      <td>Chipotle e. coli</td>
      <td>4rdwcr</td>
      <td>all</td>
      <td>1.467769e+09</td>
      <td>[/r/news] The Chipotle marketing executive lea...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/news/comments/4rdofe</td>
      <td>1</td>
      <td>https://www.reddit.com/r/news/comments/4rdofe</td>
      <td>reddit.com</td>
      <td>Stats of this post when RedditFox issued the i...</td>
      <td>0.6369</td>
      <td>0.060</td>
      <td>0.000</td>
      <td>0.940</td>
    </tr>
    <tr>
      <th>1010</th>
      <td>Chipotle e. coli</td>
      <td>3xzk1r</td>
      <td>all</td>
      <td>1.450923e+09</td>
      <td>ANALYSIS: Chipotle is a victim of corporate sa...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/conspiracy/comments/3...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/conspiracy/comments/3...</td>
      <td>reddit.com</td>
      <td>https://www.reddit.com/r/conspiratard/comments...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1011</th>
      <td>Chipotle e. coli</td>
      <td>3w0vnt</td>
      <td>all</td>
      <td>1.449660e+09</td>
      <td>Chipotle: New illnesses look like norovirus no...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3w0...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3w0...</td>
      <td>self.autotldr</td>
      <td>Summary generated by [cruyff8's autosummarizer...</td>
      <td>-0.9136</td>
      <td>0.029</td>
      <td>0.132</td>
      <td>0.839</td>
    </tr>
    <tr>
      <th>1012</th>
      <td>Chipotle e. coli</td>
      <td>3w0vnt</td>
      <td>all</td>
      <td>1.449660e+09</td>
      <td>Chipotle: New illnesses look like norovirus no...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3w0...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3w0...</td>
      <td>self.autotldr</td>
      <td>Summary generated by [cruyff8's autosummarizer...</td>
      <td>-0.9136</td>
      <td>0.029</td>
      <td>0.132</td>
      <td>0.839</td>
    </tr>
    <tr>
      <th>1013</th>
      <td>Chipotle e. coli</td>
      <td>3w0uds</td>
      <td>all</td>
      <td>1.449659e+09</td>
      <td>Chipotle shares take fresh hit after Boston Co...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3w0...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/3w0...</td>
      <td>self.autotldr</td>
      <td>Summary generated by [cruyff8's autosummarizer...</td>
      <td>-0.9654</td>
      <td>0.014</td>
      <td>0.148</td>
      <td>0.838</td>
    </tr>
    <tr>
      <th>1014</th>
      <td>Chipotle e. coli</td>
      <td>3w47oz</td>
      <td>all</td>
      <td>1.449720e+09</td>
      <td>Anyone heard of the Chipotle E Coli outbreak c...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/UIUC/comments/3w47oz/...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/UIUC/comments/3w47oz/...</td>
      <td>self.UIUC</td>
      <td>I thought getting rid of GMOs would magically ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1015</th>
      <td>Chipotle e. coli</td>
      <td>4gk8ja</td>
      <td>all</td>
      <td>1.461724e+09</td>
      <td>Chipotle Consumer Survey Post E.Coli outbreak....</td>
      <td>0</td>
      <td>https://docs.google.com/forms/d/1PeQVuCidKCmmj...</td>
      <td>3</td>
      <td>https://docs.google.com/forms/d/1PeQVuCidKCmmj...</td>
      <td>docs.google.com</td>
      <td>You posting this in a subreddit where the majo...</td>
      <td>-0.7184</td>
      <td>0.000</td>
      <td>0.250</td>
      <td>0.750</td>
    </tr>
    <tr>
      <th>1016</th>
      <td>Chipotle e. coli</td>
      <td>4gk8ja</td>
      <td>all</td>
      <td>1.461724e+09</td>
      <td>Chipotle Consumer Survey Post E.Coli outbreak....</td>
      <td>0</td>
      <td>https://docs.google.com/forms/d/1PeQVuCidKCmmj...</td>
      <td>3</td>
      <td>https://docs.google.com/forms/d/1PeQVuCidKCmmj...</td>
      <td>docs.google.com</td>
      <td>Ok.... looking at the questions, a lot of thes...</td>
      <td>0.7402</td>
      <td>0.185</td>
      <td>0.039</td>
      <td>0.776</td>
    </tr>
    <tr>
      <th>1017</th>
      <td>Chipotle e. coli</td>
      <td>4gk8ja</td>
      <td>all</td>
      <td>1.461724e+09</td>
      <td>Chipotle Consumer Survey Post E.Coli outbreak....</td>
      <td>0</td>
      <td>https://docs.google.com/forms/d/1PeQVuCidKCmmj...</td>
      <td>3</td>
      <td>https://docs.google.com/forms/d/1PeQVuCidKCmmj...</td>
      <td>docs.google.com</td>
      <td>Stand outside a patch and ask customers. You m...</td>
      <td>0.6096</td>
      <td>0.266</td>
      <td>0.098</td>
      <td>0.636</td>
    </tr>
    <tr>
      <th>1018</th>
      <td>Chipotle e. coli</td>
      <td>3r8evk</td>
      <td>all</td>
      <td>1.446514e+09</td>
      <td>How could you tell if it's E. Coli or a normal...</td>
      <td>0</td>
      <td>http://abcnews.go.com/Health/chipotle-closes-4...</td>
      <td>1</td>
      <td>http://abcnews.go.com/Health/chipotle-closes-4...</td>
      <td>abcnews.go.com</td>
      <td>Holy shit imagine all of the people losing the...</td>
      <td>-0.7351</td>
      <td>0.000</td>
      <td>0.383</td>
      <td>0.617</td>
    </tr>
    <tr>
      <th>1019</th>
      <td>Chipotle e. coli</td>
      <td>3rr6ib</td>
      <td>all</td>
      <td>1.446841e+09</td>
      <td>Chipotle's E. coli outbreak threatens sales, e...</td>
      <td>0</td>
      <td>http://www.reuters.com/article/2015/11/05/us-c...</td>
      <td>2</td>
      <td>http://www.reuters.com/article/2015/11/05/us-c...</td>
      <td>reuters.com</td>
      <td>Chipotle isn't fucking Mexican food.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1020</th>
      <td>Chipotle e. coli</td>
      <td>40nqrs</td>
      <td>all</td>
      <td>1.452653e+09</td>
      <td>E. coli? The Chipotle cult scoffs: 'We're tota...</td>
      <td>0</td>
      <td>https://www.washingtonpost.com/lifestyle/style...</td>
      <td>1</td>
      <td>https://www.washingtonpost.com/lifestyle/style...</td>
      <td>washingtonpost.com</td>
      <td>South Park nailed it with Chipotl-Away, gettin...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
  </tbody>
</table>
<p>1021 rows × 15 columns</p>
</div>




```python
grouped_df = grouped_df.groupby(['Created Date','Submission ID'])
```


```python
grouped_df.count().head()
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
      <th>Keyword</th>
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
    </tr>
    <tr>
      <th>Created Date</th>
      <th>Submission ID</th>
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
      <th>1.446333e+09</th>
      <th>3qz0mu</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1.446334e+09</th>
      <th>3qz2qk</th>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">1.446342e+09</th>
      <th>3qzjqg</th>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
      <td>42</td>
    </tr>
    <tr>
      <th>3qzk26</th>
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
    <tr>
      <th>3qzk5h</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_df = pd.DataFrame(grouped_df["Compound Score"].mean())
grouped_df
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
      <th>Compound Score</th>
    </tr>
    <tr>
      <th>Created Date</th>
      <th>Submission ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1.446333e+09</th>
      <th>3qz0mu</th>
      <td>-0.190830</td>
    </tr>
    <tr>
      <th>1.446334e+09</th>
      <th>3qz2qk</th>
      <td>0.040069</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">1.446342e+09</th>
      <th>3qzjqg</th>
      <td>0.014560</td>
    </tr>
    <tr>
      <th>3qzk26</th>
      <td>-0.273114</td>
    </tr>
    <tr>
      <th>3qzk5h</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3qzk5i</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.446344e+09</th>
      <th>3qzo9r</th>
      <td>-0.032950</td>
    </tr>
    <tr>
      <th>1.446347e+09</th>
      <th>3qzw81</th>
      <td>-0.126171</td>
    </tr>
    <tr>
      <th>1.446362e+09</th>
      <th>3r0up6</th>
      <td>-0.094300</td>
    </tr>
    <tr>
      <th>1.446366e+09</th>
      <th>3r12ny</th>
      <td>-0.193700</td>
    </tr>
    <tr>
      <th>1.446377e+09</th>
      <th>3r1loy</th>
      <td>0.036429</td>
    </tr>
    <tr>
      <th>1.446390e+09</th>
      <th>3r23nk</th>
      <td>-0.920000</td>
    </tr>
    <tr>
      <th>1.446439e+09</th>
      <th>3r4elr</th>
      <td>-0.072033</td>
    </tr>
    <tr>
      <th>1.446458e+09</th>
      <th>3r5o9y</th>
      <td>-0.024167</td>
    </tr>
    <tr>
      <th>1.446459e+09</th>
      <th>3r5pll</th>
      <td>0.273200</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.446471e+09</th>
      <th>3r6dh8</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3r6dqt</th>
      <td>0.636900</td>
    </tr>
    <tr>
      <th>1.446500e+09</th>
      <th>3r7izn</th>
      <td>-0.272200</td>
    </tr>
    <tr>
      <th>1.446507e+09</th>
      <th>3r7wvw</th>
      <td>-0.037773</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.446514e+09</th>
      <th>3r8edx</th>
      <td>0.062708</td>
    </tr>
    <tr>
      <th>3r8evk</th>
      <td>-0.735100</td>
    </tr>
    <tr>
      <th>1.446526e+09</th>
      <th>3r9cyl</th>
      <td>0.318200</td>
    </tr>
    <tr>
      <th>1.446597e+09</th>
      <th>3rda2k</th>
      <td>0.037350</td>
    </tr>
    <tr>
      <th>1.446614e+09</th>
      <th>3relvy</th>
      <td>0.510600</td>
    </tr>
    <tr>
      <th>1.446617e+09</th>
      <th>3reso5</th>
      <td>0.557400</td>
    </tr>
    <tr>
      <th>1.446623e+09</th>
      <th>3rf75z</th>
      <td>-0.565050</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">1.446629e+09</th>
      <th>3rflv7</th>
      <td>0.095309</td>
    </tr>
    <tr>
      <th>3rfm7d</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3rfmip</th>
      <td>0.012847</td>
    </tr>
    <tr>
      <th>1.446686e+09</th>
      <th>3rijdf</th>
      <td>0.180600</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.453911e+09</th>
      <th>42wiq7</th>
      <td>0.417300</td>
    </tr>
    <tr>
      <th>1.453950e+09</th>
      <th>42yzw1</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.454376e+09</th>
      <th>43pftt</th>
      <td>0.030534</td>
    </tr>
    <tr>
      <th>1.454377e+09</th>
      <th>43pitn</th>
      <td>0.017253</td>
    </tr>
    <tr>
      <th>1.454383e+09</th>
      <th>43q370</th>
      <td>0.075383</td>
    </tr>
    <tr>
      <th>1.454468e+09</th>
      <th>43vn8p</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.454548e+09</th>
      <th>440r6e</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.454551e+09</th>
      <th>44102q</th>
      <td>-0.215550</td>
    </tr>
    <tr>
      <th>1.455081e+09</th>
      <th>44yxq5</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.455245e+09</th>
      <th>45ab40</th>
      <td>0.169313</td>
    </tr>
    <tr>
      <th>1.455352e+09</th>
      <th>45hskf</th>
      <td>0.310250</td>
    </tr>
    <tr>
      <th>1.456209e+09</th>
      <th>473ejo</th>
      <td>0.152800</td>
    </tr>
    <tr>
      <th>1.457989e+09</th>
      <th>4acy2o</th>
      <td>0.014524</td>
    </tr>
    <tr>
      <th>1.461724e+09</th>
      <th>4gk8ja</th>
      <td>0.210467</td>
    </tr>
    <tr>
      <th>1.462693e+09</th>
      <th>4icb9k</th>
      <td>0.139264</td>
    </tr>
    <tr>
      <th>1.463620e+09</th>
      <th>4jxp87</th>
      <td>0.486900</td>
    </tr>
    <tr>
      <th>1.464127e+09</th>
      <th>4ktvcm</th>
      <td>0.455875</td>
    </tr>
    <tr>
      <th>1.467769e+09</th>
      <th>4rdwcr</th>
      <td>0.636900</td>
    </tr>
    <tr>
      <th>1.467972e+09</th>
      <th>4rs9qp</th>
      <td>-0.139350</td>
    </tr>
    <tr>
      <th>1.468368e+09</th>
      <th>4shppv</th>
      <td>0.431900</td>
    </tr>
    <tr>
      <th>1.473134e+09</th>
      <th>51b6zz</th>
      <td>0.039733</td>
    </tr>
    <tr>
      <th>1.473222e+09</th>
      <th>51h8kk</th>
      <td>-0.377400</td>
    </tr>
    <tr>
      <th>1.473846e+09</th>
      <th>52o6ei</th>
      <td>0.100785</td>
    </tr>
    <tr>
      <th>1.473884e+09</th>
      <th>52q4qt</th>
      <td>-0.061417</td>
    </tr>
    <tr>
      <th>1.473896e+09</th>
      <th>52r2l6</th>
      <td>0.717550</td>
    </tr>
    <tr>
      <th>1.474078e+09</th>
      <th>5337o3</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.480988e+09</th>
      <th>5gn7f6</th>
      <td>-0.781000</td>
    </tr>
    <tr>
      <th>1.480989e+09</th>
      <th>5gnaj3</th>
      <td>0.273200</td>
    </tr>
    <tr>
      <th>1.509504e+09</th>
      <th>79xu6n</th>
      <td>-0.186100</td>
    </tr>
    <tr>
      <th>1.515229e+09</th>
      <th>7ofumn</th>
      <td>-0.211833</td>
    </tr>
  </tbody>
</table>
<p>144 rows × 1 columns</p>
</div>




```python
grouped_df = grouped_df.reset_index()
grouped_df.head()
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
      <th>Created Date</th>
      <th>Submission ID</th>
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.446333e+09</td>
      <td>3qz0mu</td>
      <td>-0.190830</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.446334e+09</td>
      <td>3qz2qk</td>
      <td>0.040069</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.446342e+09</td>
      <td>3qzjqg</td>
      <td>0.014560</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.446342e+09</td>
      <td>3qzk26</td>
      <td>-0.273114</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.446342e+09</td>
      <td>3qzk5h</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df, fit_reg=False, palette="Paired")

#plt.title("Chipotle e. coli Comment Sentiments on Reddit")

plt.ylabel("Sentiment Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y') for tm in xticks],
                  rotation=45)

#xfmt = md.DateFormatter('%Y-%m-%d %H:%M:%S')
#ax.xaxis.set_major_formatter(xfmt)

plt.savefig("Chipotle_ecoli_Sentiments.png", dpi=350)

plt.show()
```


![png](output_43_0.png)



```python
grouped_df3 = reddit_comments_df.groupby(['Created Date','Submission ID', 'Keyword'])
```


```python
grouped_df3.count().head()
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
    </tr>
    <tr>
      <th>Created Date</th>
      <th>Submission ID</th>
      <th>Keyword</th>
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
      <th>1.213810e+09</th>
      <th>6nvct</th>
      <th>Burger King food poisoning</th>
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
      <th>1.263184e+09</th>
      <th>anww0</th>
      <th>Burger King e. coli</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1.263190e+09</th>
      <th>anxt4</th>
      <th>Burger King e. coli</th>
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
      <th>1.307031e+09</th>
      <th>hpry7</th>
      <th>Costco e. coli</th>
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
      <th>1.328227e+09</th>
      <th>p7sdy</th>
      <th>Taco Bell salmonella</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_df3 = pd.DataFrame(grouped_df3["Compound Score"].mean())
grouped_df3
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
      <th>Created Date</th>
      <th>Submission ID</th>
      <th>Keyword</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1.213810e+09</th>
      <th>6nvct</th>
      <th>Burger King food poisoning</th>
      <td>0.170600</td>
    </tr>
    <tr>
      <th>1.263184e+09</th>
      <th>anww0</th>
      <th>Burger King e. coli</th>
      <td>0.006510</td>
    </tr>
    <tr>
      <th>1.263190e+09</th>
      <th>anxt4</th>
      <th>Burger King e. coli</th>
      <td>-0.085055</td>
    </tr>
    <tr>
      <th>1.307031e+09</th>
      <th>hpry7</th>
      <th>Costco e. coli</th>
      <td>0.182210</td>
    </tr>
    <tr>
      <th>1.328227e+09</th>
      <th>p7sdy</th>
      <th>Taco Bell salmonella</th>
      <td>-0.421500</td>
    </tr>
    <tr>
      <th>1.328254e+09</th>
      <th>p8ff0</th>
      <th>Taco Bell salmonella</th>
      <td>0.075433</td>
    </tr>
    <tr>
      <th>1.328838e+09</th>
      <th>pi0xm</th>
      <th>Taco Bell salmonella</th>
      <td>-0.891400</td>
    </tr>
    <tr>
      <th>1.335531e+09</th>
      <th>suuhx</th>
      <th>KFC salmonella</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.335664e+09</th>
      <th>swzyk</th>
      <th>KFC salmonella</th>
      <td>-0.382800</td>
    </tr>
    <tr>
      <th>1.348012e+09</th>
      <th>1030g9</th>
      <th>Costco e. coli</th>
      <td>0.314500</td>
    </tr>
    <tr>
      <th>1.348797e+09</th>
      <th>10knau</th>
      <th>Costco e. coli</th>
      <td>-0.155225</td>
    </tr>
    <tr>
      <th>1.352498e+09</th>
      <th>12wukq</th>
      <th>Taco Bell food poisoning</th>
      <td>-0.196429</td>
    </tr>
    <tr>
      <th>1.357597e+09</th>
      <th>164c2v</th>
      <th>Taco Bell food poisoning</th>
      <td>0.050575</td>
    </tr>
    <tr>
      <th>1.369120e+09</th>
      <th>1eq6hg</th>
      <th>KFC e. coli</th>
      <td>0.959900</td>
    </tr>
    <tr>
      <th>1.381612e+09</th>
      <th>1oacvi</th>
      <th>Costco e. coli</th>
      <td>0.010329</td>
    </tr>
    <tr>
      <th>1.381627e+09</th>
      <th>1oarxe</th>
      <th>Costco e. coli</th>
      <td>0.335250</td>
    </tr>
    <tr>
      <th>1.381742e+09</th>
      <th>1oe6xm</th>
      <th>Costco salmonella</th>
      <td>0.076857</td>
    </tr>
    <tr>
      <th>1.381964e+09</th>
      <th>1okphe</th>
      <th>Costco e. coli</th>
      <td>0.104733</td>
    </tr>
    <tr>
      <th>1.386249e+09</th>
      <th>1s51we</th>
      <th>Taco Bell food poisoning</th>
      <td>-0.458800</td>
    </tr>
    <tr>
      <th>1.390949e+09</th>
      <th>1wdeqs</th>
      <th>Chipotle food poisoning</th>
      <td>-0.254614</td>
    </tr>
    <tr>
      <th>1.405829e+09</th>
      <th>2b5ldt</th>
      <th>Burger King food poisoning</th>
      <td>-0.146475</td>
    </tr>
    <tr>
      <th>1.427237e+09</th>
      <th>304vlw</th>
      <th>Chipotle food poisoning</th>
      <td>0.476650</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.441969e+09</th>
      <th>3khsjo</th>
      <th>Chipotle salmonella</th>
      <td>-0.585900</td>
    </tr>
    <tr>
      <th>3khtjo</th>
      <th>Chipotle salmonella</th>
      <td>-0.045167</td>
    </tr>
    <tr>
      <th>1.442008e+09</th>
      <th>3kji7g</th>
      <th>Chipotle salmonella</th>
      <td>-0.192500</td>
    </tr>
    <tr>
      <th>1.442056e+09</th>
      <th>3kmigm</th>
      <th>Chipotle salmonella</th>
      <td>0.329850</td>
    </tr>
    <tr>
      <th>1.442478e+09</th>
      <th>3l8p74</th>
      <th>Costco food poisoning</th>
      <td>0.304717</td>
    </tr>
    <tr>
      <th>1.442482e+09</th>
      <th>3l8vwn</th>
      <th>Chipotle salmonella</th>
      <td>0.089067</td>
    </tr>
    <tr>
      <th>1.442527e+09</th>
      <th>3laxcl</th>
      <th>Chipotle salmonella</th>
      <td>-0.046429</td>
    </tr>
    <tr>
      <th>1.442529e+09</th>
      <th>3lb0n3</th>
      <th>Chipotle salmonella</th>
      <td>-0.030667</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.473846e+09</th>
      <th>52o6ei</th>
      <th>Chipotle e. coli</th>
      <td>0.100785</td>
    </tr>
    <tr>
      <th>1.473884e+09</th>
      <th>52q4qt</th>
      <th>Chipotle e. coli</th>
      <td>-0.061417</td>
    </tr>
    <tr>
      <th>1.473896e+09</th>
      <th>52r2l6</th>
      <th>Chipotle e. coli</th>
      <td>0.717550</td>
    </tr>
    <tr>
      <th>1.474078e+09</th>
      <th>5337o3</th>
      <th>Chipotle e. coli</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.480988e+09</th>
      <th>5gn7f6</th>
      <th>Chipotle e. coli</th>
      <td>-0.781000</td>
    </tr>
    <tr>
      <th>1.480989e+09</th>
      <th>5gnaj3</th>
      <th>Chipotle e. coli</th>
      <td>0.273200</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">1.500426e+09</th>
      <th>6o21s6</th>
      <th>Chipotle foodborne illness</th>
      <td>-0.130814</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">6o2355</th>
      <th>Chipotle Norovirus</th>
      <td>-0.072946</td>
    </tr>
    <tr>
      <th>Chipotle foodborne illness</th>
      <td>-0.072946</td>
    </tr>
    <tr>
      <th>1.500436e+09</th>
      <th>6o396e</th>
      <th>Chipotle food poisoning</th>
      <td>-0.143650</td>
    </tr>
    <tr>
      <th>1.500466e+09</th>
      <th>6o625l</th>
      <th>Chipotle Norovirus</th>
      <td>-0.599400</td>
    </tr>
    <tr>
      <th>1.500509e+09</th>
      <th>6o9dza</th>
      <th>Chipotle Norovirus</th>
      <td>0.031327</td>
    </tr>
    <tr>
      <th>1.500614e+09</th>
      <th>6ojbfy</th>
      <th>Chipotle Norovirus</th>
      <td>-0.201400</td>
    </tr>
    <tr>
      <th>1.500616e+09</th>
      <th>6ojkiw</th>
      <th>Chipotle Norovirus</th>
      <td>0.006655</td>
    </tr>
    <tr>
      <th>1.500684e+09</th>
      <th>6op39k</th>
      <th>Chipotle Norovirus</th>
      <td>-0.285619</td>
    </tr>
    <tr>
      <th>1.500696e+09</th>
      <th>6oqgo0</th>
      <th>Chipotle Norovirus</th>
      <td>0.340000</td>
    </tr>
    <tr>
      <th>1.501025e+09</th>
      <th>6pgsou</th>
      <th>Chipotle Norovirus</th>
      <td>0.087200</td>
    </tr>
    <tr>
      <th>1.501049e+09</th>
      <th>6pjneb</th>
      <th>Chipotle Norovirus</th>
      <td>0.659700</td>
    </tr>
    <tr>
      <th>1.501067e+09</th>
      <th>6plbvf</th>
      <th>Chipotle Norovirus</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.501673e+09</th>
      <th>6r1g6t</th>
      <th>Chipotle Norovirus</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.501816e+09</th>
      <th>6rembl</th>
      <th>Chipotle Norovirus</th>
      <td>-0.446840</td>
    </tr>
    <tr>
      <th>1.502654e+09</th>
      <th>6tepxi</th>
      <th>Costco e. coli</th>
      <td>-0.199967</td>
    </tr>
    <tr>
      <th>1.504507e+09</th>
      <th>6xwbia</th>
      <th>Chipotle food poisoning</th>
      <td>-0.152927</td>
    </tr>
    <tr>
      <th>1.508234e+09</th>
      <th>76vfad</th>
      <th>Taco Bell food poisoning</th>
      <td>0.133340</td>
    </tr>
    <tr>
      <th>1.509504e+09</th>
      <th>79xu6n</th>
      <th>Chipotle e. coli</th>
      <td>-0.186100</td>
    </tr>
    <tr>
      <th>1.513823e+09</th>
      <th>7l3bej</th>
      <th>Chipotle foodborne illness</th>
      <td>-0.544700</td>
    </tr>
    <tr>
      <th>1.514001e+09</th>
      <th>7ljt9w</th>
      <th>Chipotle food poisoning</th>
      <td>-0.245150</td>
    </tr>
    <tr>
      <th>1.514768e+09</th>
      <th>7n9hmg</th>
      <th>Popeyes food poisoning</th>
      <td>0.086511</td>
    </tr>
    <tr>
      <th>1.515229e+09</th>
      <th>7ofumn</th>
      <th>Chipotle e. coli</th>
      <td>-0.211833</td>
    </tr>
    <tr>
      <th>1.518328e+09</th>
      <th>7wohs5</th>
      <th>Burger King e. coli</th>
      <td>0.177424</td>
    </tr>
  </tbody>
</table>
<p>251 rows × 1 columns</p>
</div>




```python
grouped_df3 = grouped_df3.reset_index()
grouped_df3.head()
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
      <th>Created Date</th>
      <th>Submission ID</th>
      <th>Keyword</th>
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.213810e+09</td>
      <td>6nvct</td>
      <td>Burger King food poisoning</td>
      <td>0.170600</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.263184e+09</td>
      <td>anww0</td>
      <td>Burger King e. coli</td>
      <td>0.006510</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.263190e+09</td>
      <td>anxt4</td>
      <td>Burger King e. coli</td>
      <td>-0.085055</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.307031e+09</td>
      <td>hpry7</td>
      <td>Costco e. coli</td>
      <td>0.182210</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.328227e+09</td>
      <td>p7sdy</td>
      <td>Taco Bell salmonella</td>
      <td>-0.421500</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set(font_scale=1)
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df3, hue="Keyword", fit_reg=False, palette="Paired")

#plt.title("Combined Comment Sentiments on Reddit")

plt.ylabel("Sentiment Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y') for tm in xticks],
                  rotation=45)

#xfmt = md.DateFormatter('%Y-%m-%d %H:%M:%S')
#ax.xaxis.set_major_formatter(xfmt)

plt.savefig("Combinedkw_Sentiments.png", dpi=350)

plt.show()
```


![png](output_48_0.png)



```python
reddit_comments_df['Keyword'].value_counts()
```




    Chipotle e. coli                1021
    Chipotle Norovirus               310
    Chipotle food poisoning          140
    Costco e. coli                    72
    Chipotle foodborne illness        62
    Taco Bell food poisoning          40
    Burger King e. coli               38
    Chipotle salmonella               30
    Panda Express food poisoning      11
    Popeyes food poisoning             9
    Costco salmonella                  7
    Burger King food poisoning         6
    Costco food poisoning              6
    Burger King salmonella             6
    Taco Bell e. coli                  6
    Taco Bell salmonella               5
    KFC salmonella                     4
    KFC e. coli                        1
    Name: Keyword, dtype: int64




```python
grouped_df4 = reddit_comments_df.groupby('Keyword')['Compound Score'].mean()
```


```python
grouped_df4 = pd.DataFrame(grouped_df4)
grouped_df4 = grouped_df4.reset_index()
grouped_df4
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
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burger King e. coli</td>
      <td>0.056466</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burger King food poisoning</td>
      <td>-0.040783</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Burger King salmonella</td>
      <td>-0.207367</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle Norovirus</td>
      <td>-0.052390</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle e. coli</td>
      <td>0.007160</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle food poisoning</td>
      <td>-0.017724</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle foodborne illness</td>
      <td>-0.147444</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle salmonella</td>
      <td>-0.047377</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Costco e. coli</td>
      <td>0.099962</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Costco food poisoning</td>
      <td>0.304717</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Costco salmonella</td>
      <td>0.076857</td>
    </tr>
    <tr>
      <th>11</th>
      <td>KFC e. coli</td>
      <td>0.959900</td>
    </tr>
    <tr>
      <th>12</th>
      <td>KFC salmonella</td>
      <td>-0.287100</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Panda Express food poisoning</td>
      <td>0.024209</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Popeyes food poisoning</td>
      <td>0.086511</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Taco Bell e. coli</td>
      <td>-0.334833</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Taco Bell food poisoning</td>
      <td>-0.035730</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Taco Bell salmonella</td>
      <td>-0.217320</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set()
ax = sns.barplot(x='Keyword', y='Compound Score', data=grouped_df4, ci=None)

ttl = ax.title
ttl.set_position([0.5, 1.05])

plt.title("Overall Sentiments for Combined Keywords on Reddit (%s) %s" % (time.strftime("%x"), ""))
plt.ylabel("Sentiment Polarity")
plt.xlabel("Keywords")

plt.ylim(-0.15, 0.15)

for item in ax.get_xticklabels():
    item.set_rotation(45)

#get labels for bars
for p in ax.patches:
    height = p.get_height()
    ax.text(p.get_x()+p.get_width()/2.,
            1.05*height,
                '{:1.2f}'.format(height),
            ha="center") 

plt.savefig("Combined_Sentiment_Overall.png", dpi=350)
plt.show()
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    ~/anaconda3/lib/python3.6/site-packages/IPython/core/formatters.py in __call__(self, obj)
        330                 pass
        331             else:
    --> 332                 return printer(obj)
        333             # Finally look for special method names
        334             method = get_real_method(obj, self.print_method)


    ~/anaconda3/lib/python3.6/site-packages/IPython/core/pylabtools.py in <lambda>(fig)
        235 
        236     if 'png' in formats:
    --> 237         png_formatter.for_type(Figure, lambda fig: print_figure(fig, 'png', **kwargs))
        238     if 'retina' in formats or 'png2x' in formats:
        239         png_formatter.for_type(Figure, lambda fig: retina_figure(fig, **kwargs))


    ~/anaconda3/lib/python3.6/site-packages/IPython/core/pylabtools.py in print_figure(fig, fmt, bbox_inches, **kwargs)
        119 
        120     bytes_io = BytesIO()
    --> 121     fig.canvas.print_figure(bytes_io, **kw)
        122     data = bytes_io.getvalue()
        123     if fmt == 'svg':


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/backend_bases.py in print_figure(self, filename, dpi, facecolor, edgecolor, orientation, format, **kwargs)
       2206                     orientation=orientation,
       2207                     dryrun=True,
    -> 2208                     **kwargs)
       2209                 renderer = self.figure._cachedRenderer
       2210                 bbox_inches = self.figure.get_tightbbox(renderer)


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/backends/backend_agg.py in print_png(self, filename_or_obj, *args, **kwargs)
        505 
        506     def print_png(self, filename_or_obj, *args, **kwargs):
    --> 507         FigureCanvasAgg.draw(self)
        508         renderer = self.get_renderer()
        509         original_dpi = renderer.dpi


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/backends/backend_agg.py in draw(self)
        428             if toolbar:
        429                 toolbar.set_cursor(cursors.WAIT)
    --> 430             self.figure.draw(self.renderer)
        431         finally:
        432             if toolbar:


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/artist.py in draw_wrapper(artist, renderer, *args, **kwargs)
         53                 renderer.start_filter()
         54 
    ---> 55             return draw(artist, renderer, *args, **kwargs)
         56         finally:
         57             if artist.get_agg_filter() is not None:


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/figure.py in draw(self, renderer)
       1293 
       1294             mimage._draw_list_compositing_images(
    -> 1295                 renderer, self, artists, self.suppressComposite)
       1296 
       1297             renderer.close_group('figure')


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/image.py in _draw_list_compositing_images(renderer, parent, artists, suppress_composite)
        136     if not_composite or not has_images:
        137         for a in artists:
    --> 138             a.draw(renderer)
        139     else:
        140         # Composite any adjacent images together


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/artist.py in draw_wrapper(artist, renderer, *args, **kwargs)
         53                 renderer.start_filter()
         54 
    ---> 55             return draw(artist, renderer, *args, **kwargs)
         56         finally:
         57             if artist.get_agg_filter() is not None:


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/axes/_base.py in draw(self, renderer, inframe)
       2397             renderer.stop_rasterizing()
       2398 
    -> 2399         mimage._draw_list_compositing_images(renderer, self, artists)
       2400 
       2401         renderer.close_group('axes')


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/image.py in _draw_list_compositing_images(renderer, parent, artists, suppress_composite)
        136     if not_composite or not has_images:
        137         for a in artists:
    --> 138             a.draw(renderer)
        139     else:
        140         # Composite any adjacent images together


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/artist.py in draw_wrapper(artist, renderer, *args, **kwargs)
         53                 renderer.start_filter()
         54 
    ---> 55             return draw(artist, renderer, *args, **kwargs)
         56         finally:
         57             if artist.get_agg_filter() is not None:


    ~/anaconda3/lib/python3.6/site-packages/matplotlib/text.py in draw(self, renderer)
        761             posy = float(textobj.convert_yunits(textobj._y))
        762             if not np.isfinite(posx) or not np.isfinite(posy):
    --> 763                 raise ValueError("posx and posy should be finite values")
        764             posx, posy = trans.transform_point((posx, posy))
        765             canvasw, canvash = renderer.get_canvas_width_height()


    ValueError: posx and posy should be finite values



    <matplotlib.figure.Figure at 0x10f13e2b0>



```python
sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=reddit_comments_df, hue='Keyword', fit_reg=False)

plt.title("Food Sickness Comments on Reddit")

plt.ylabel("Tweet Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

    
ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y') for tm in xticks],
                  rotation=45)

#xfmt = md.DateFormatter('%Y-%m-%d %H:%M:%S')
#ax.xaxis.set_major_formatter(xfmt)

#plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)

plt.show()
```


![png](output_53_0.png)



```python
keyword_data = {}

for keyword in reddit_comments_df['Keyword']:
   
   keyword_data[keyword] = reddit_comments_df[reddit_comments_df['Keyword']== keyword]
```


```python
for kw in keyword_data.keys():
   
    dataframe = keyword_data[kw]
   
    sns.set()
    sns.lmplot(x='Created Date', y='Compound Score', data=dataframe, hue='Keyword', fit_reg=False)

    plt.title("Food Sickness Comments on Reddit")

    plt.ylabel("Tweet Polarity")
    plt.xlabel("Date")

    plt.grid(True)
    #plt.xlim([100, 0])
    plt.ylim([-1, 1])

    ax = plt.gca()
    xticks = ax.get_xticks()
    ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y-%m-%d') for tm in xticks],
                  rotation=45)
    
    #plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)

    plt.show()
    

```


![png](output_55_0.png)



![png](output_55_1.png)



![png](output_55_2.png)



![png](output_55_3.png)



![png](output_55_4.png)



![png](output_55_5.png)



![png](output_55_6.png)



![png](output_55_7.png)



![png](output_55_8.png)



![png](output_55_9.png)



![png](output_55_10.png)



![png](output_55_11.png)



![png](output_55_12.png)



![png](output_55_13.png)



![png](output_55_14.png)



![png](output_55_15.png)



![png](output_55_16.png)



![png](output_55_17.png)



```python
#combine chipotle keywords
chipotle_kws1 = keyword_data['Chipotle e. coli']
chipotle_kws2 = keyword_data['Chipotle Norovirus']
chipotle_kws3 = keyword_data['Chipotle food poisoning']
chipotle_kws4 = keyword_data['Chipotle foodborne illness']
chipotle_kws5 = keyword_data['Chipotle salmonella']

chipotle_kws1 = chipotle_kws1.append(chipotle_kws2)
chipotle_kws1 = chipotle_kws1.append(chipotle_kws3)
chipotle_kws1 = chipotle_kws1.append(chipotle_kws4)
chipotle_kws1 = chipotle_kws1.append(chipotle_kws5)

chipotle_kws1 = chipotle_kws1.reset_index()
del chipotle_kws1['index']
chipotle_kws1
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>chipotle-away sales will be through the roof</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>As I understand it no contamination has been f...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.095</td>
      <td>0.905</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>According to the article, this is a produce su...</td>
      <td>-0.6948</td>
      <td>0.033</td>
      <td>0.130</td>
      <td>0.837</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I drove past a chipotle last night and the lin...</td>
      <td>0.8880</td>
      <td>0.189</td>
      <td>0.000</td>
      <td>0.811</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will not eat there again.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Chipotle e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>127</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>13</td>
      <td>http://www.reuters.com/article/us-chipotle-mex...</td>
      <td>reuters.com</td>
      <td>I will never eat there.\n\nI will eat at McDon...</td>
      <td>0.8198</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chipotle e. coli</td>
      <td>3tn4ko</td>
      <td>all</td>
      <td>1.448099e+09</td>
      <td>More than 40 people have fallen ill with E. co...</td>
      <td>15</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>reuters.com</td>
      <td>"Food With Integrity" -- and E. Coli</td>
      <td>0.3818</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chipotle e. coli</td>
      <td>3tn4ko</td>
      <td>all</td>
      <td>1.448099e+09</td>
      <td>More than 40 people have fallen ill with E. co...</td>
      <td>15</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>1</td>
      <td>http://www.reuters.com/article/2015/11/21/us-c...</td>
      <td>reuters.com</td>
      <td>"Food With Integrity" -- and E. Coli</td>
      <td>0.3818</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>That can't be good for business.</td>
      <td>-0.3412</td>
      <td>0.000</td>
      <td>0.325</td>
      <td>0.675</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>E-coli, is shit/feces/poop bacteria. It means ...</td>
      <td>-0.7889</td>
      <td>0.081</td>
      <td>0.140</td>
      <td>0.780</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>That can't be good for business.</td>
      <td>-0.3412</td>
      <td>0.000</td>
      <td>0.325</td>
      <td>0.675</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chipotle e. coli</td>
      <td>3rf75z</td>
      <td>all</td>
      <td>1.446623e+09</td>
      <td>Chipotle Mexican Grill Inc (CMG.N) is now link...</td>
      <td>10</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>5</td>
      <td>http://www.reuters.com/article/2015/11/03/us-c...</td>
      <td>reuters.com</td>
      <td>E-coli, is shit/feces/poop bacteria. It means ...</td>
      <td>-0.7889</td>
      <td>0.081</td>
      <td>0.140</td>
      <td>0.780</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>So far...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Wait there were free chipotle burritos?</td>
      <td>0.5106</td>
      <td>0.398</td>
      <td>0.000</td>
      <td>0.602</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Except your bowels have billions of E. Coli.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>*Day 4: Stomach is cramping, diarrhea is preva...</td>
      <td>-0.5943</td>
      <td>0.000</td>
      <td>0.188</td>
      <td>0.812</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Chipotle worker her, was given 6 Family and Fr...</td>
      <td>0.8316</td>
      <td>0.286</td>
      <td>0.000</td>
      <td>0.714</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Currently eating free burrito. E. coli, you da...</td>
      <td>0.5106</td>
      <td>0.268</td>
      <td>0.000</td>
      <td>0.732</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Well, considering that E. coli is a model orga...</td>
      <td>0.8478</td>
      <td>0.277</td>
      <td>0.000</td>
      <td>0.723</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You have had E-coli. You have E-coli in your g...</td>
      <td>0.0382</td>
      <td>0.054</td>
      <td>0.000</td>
      <td>0.946</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You got your free burrito already!?</td>
      <td>0.5562</td>
      <td>0.418</td>
      <td>0.000</td>
      <td>0.582</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>E. Coli lives in the intestines....everyone's ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Yesterday I got a free steak bowl at Chipotle ...</td>
      <td>0.4659</td>
      <td>0.115</td>
      <td>0.000</td>
      <td>0.885</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Chipotle e. coli</td>
      <td>45ab40</td>
      <td>all</td>
      <td>1.455245e+09</td>
      <td>Yesterday I got a free burrito from Chipotle t...</td>
      <td>6106</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>245</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Good guy E. coli</td>
      <td>0.4404</td>
      <td>0.492</td>
      <td>0.000</td>
      <td>0.508</td>
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
    </tr>
    <tr>
      <th>1533</th>
      <td>Chipotle salmonella</td>
      <td>3l8vwn</td>
      <td>all</td>
      <td>1.442482e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>84</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>3</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>I read "tornadoes" instead of "tomatoes". Soun...</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.241</td>
      <td>0.759</td>
    </tr>
    <tr>
      <th>1534</th>
      <td>Chipotle salmonella</td>
      <td>3l8vwn</td>
      <td>all</td>
      <td>1.442482e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>84</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>3</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>Good thing I don't like tomatoes.</td>
      <td>0.1999</td>
      <td>0.362</td>
      <td>0.263</td>
      <td>0.375</td>
    </tr>
    <tr>
      <th>1535</th>
      <td>Chipotle salmonella</td>
      <td>3l8vwn</td>
      <td>all</td>
      <td>1.442482e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>84</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>3</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>No worries though, it was natural GMO free sal...</td>
      <td>0.6096</td>
      <td>0.391</td>
      <td>0.218</td>
      <td>0.392</td>
    </tr>
    <tr>
      <th>1536</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>Where is that guy who was trying to meet chipo...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1537</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>Salmonella is organic and local, right?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1538</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>They are trying to trace back to the farm that...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1539</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>How does salmonella get on tomatoes?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1540</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>I know someone who got sick because of this an...</td>
      <td>-0.7269</td>
      <td>0.000</td>
      <td>0.177</td>
      <td>0.823</td>
    </tr>
    <tr>
      <th>1541</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>I've read that high ecolli levels are a concer...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1542</th>
      <td>Chipotle salmonella</td>
      <td>3laxcl</td>
      <td>all</td>
      <td>1.442527e+09</td>
      <td>Tomatoes identified as source of Salmonella ou...</td>
      <td>62</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>17</td>
      <td>http://www.fox9.com/news/20541000-story</td>
      <td>fox9.com</td>
      <td>Go to chipotle on the 22nd to support Como's t...</td>
      <td>0.4019</td>
      <td>0.162</td>
      <td>0.000</td>
      <td>0.838</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>Minnesota Salmonella outbreak linked to Chipot...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1544</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>&gt; Salmonella infections may cause diarrhea, st...</td>
      <td>-0.4215</td>
      <td>0.000</td>
      <td>0.167</td>
      <td>0.833</td>
    </tr>
    <tr>
      <th>1545</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>Is the Salmonella made of GMO's?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1546</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>Nice to see that whole non-GMO thing is workin...</td>
      <td>0.4215</td>
      <td>0.237</td>
      <td>0.000</td>
      <td>0.763</td>
    </tr>
    <tr>
      <th>1547</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>Didn't like it before. Definitely don't want i...</td>
      <td>0.3111</td>
      <td>0.272</td>
      <td>0.197</td>
      <td>0.532</td>
    </tr>
    <tr>
      <th>1548</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>Bland, tasteless, and apparently unsafe.  Wow,...</td>
      <td>-0.8226</td>
      <td>0.105</td>
      <td>0.274</td>
      <td>0.621</td>
    </tr>
    <tr>
      <th>1549</th>
      <td>Chipotle salmonella</td>
      <td>3kji7g</td>
      <td>all</td>
      <td>1.442008e+09</td>
      <td>Minnesota Salmonella outbreak linked to Chipotle</td>
      <td>67</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>17</td>
      <td>http://www.startribune.com/twin-cities-salmone...</td>
      <td>startribune.com</td>
      <td>What the hell is going on with Chipotle recent...</td>
      <td>-0.8360</td>
      <td>0.000</td>
      <td>0.214</td>
      <td>0.786</td>
    </tr>
    <tr>
      <th>1550</th>
      <td>Chipotle salmonella</td>
      <td>3khtjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>MDH: Salmonella cases linked to Chipotle</td>
      <td>31</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>11</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>Well, at least it's GMO-free salmonella, then.</td>
      <td>0.2732</td>
      <td>0.259</td>
      <td>0.000</td>
      <td>0.741</td>
    </tr>
    <tr>
      <th>1551</th>
      <td>Chipotle salmonella</td>
      <td>3khtjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>MDH: Salmonella cases linked to Chipotle</td>
      <td>31</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>11</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>I went to the US Bank Plaza location on Wednes...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.083</td>
      <td>0.917</td>
    </tr>
    <tr>
      <th>1552</th>
      <td>Chipotle salmonella</td>
      <td>3khtjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>MDH: Salmonella cases linked to Chipotle</td>
      <td>31</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>11</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>Anyone know what the 'suspected produce item' ...</td>
      <td>-0.2263</td>
      <td>0.000</td>
      <td>0.213</td>
      <td>0.787</td>
    </tr>
    <tr>
      <th>1553</th>
      <td>Chipotle salmonella</td>
      <td>3khtjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>MDH: Salmonella cases linked to Chipotle</td>
      <td>31</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>11</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>Worth the risk...</td>
      <td>0.2263</td>
      <td>0.487</td>
      <td>0.000</td>
      <td>0.513</td>
    </tr>
    <tr>
      <th>1554</th>
      <td>Chipotle salmonella</td>
      <td>3khtjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>MDH: Salmonella cases linked to Chipotle</td>
      <td>31</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>11</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>Guess I'm not going to eat there today then......</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1555</th>
      <td>Chipotle salmonella</td>
      <td>3khtjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>MDH: Salmonella cases linked to Chipotle</td>
      <td>31</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>11</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>I've got some really bad gut poisoning after e...</td>
      <td>-0.1423</td>
      <td>0.201</td>
      <td>0.211</td>
      <td>0.588</td>
    </tr>
    <tr>
      <th>1556</th>
      <td>Chipotle salmonella</td>
      <td>3khsjo</td>
      <td>all</td>
      <td>1.441969e+09</td>
      <td>Minnesota Dept of Health:Salmonella cases link...</td>
      <td>17</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>1</td>
      <td>http://www.kare11.com/story/news/health/2015/0...</td>
      <td>kare11.com</td>
      <td>No worries. It's GMO free salmonella it is all...</td>
      <td>-0.5859</td>
      <td>0.248</td>
      <td>0.453</td>
      <td>0.299</td>
    </tr>
    <tr>
      <th>1557</th>
      <td>Chipotle salmonella</td>
      <td>3lb0n3</td>
      <td>all</td>
      <td>1.442529e+09</td>
      <td>Rochester Chipotle Restaurant Linked to Statew...</td>
      <td>6</td>
      <td>http://www.kaaltv.com/article/stories/s3903070...</td>
      <td>6</td>
      <td>http://www.kaaltv.com/article/stories/s3903070...</td>
      <td>kaaltv.com</td>
      <td>Know people that got food poisoning about a we...</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>0.322</td>
      <td>0.678</td>
    </tr>
    <tr>
      <th>1558</th>
      <td>Chipotle salmonella</td>
      <td>3lb0n3</td>
      <td>all</td>
      <td>1.442529e+09</td>
      <td>Rochester Chipotle Restaurant Linked to Statew...</td>
      <td>6</td>
      <td>http://www.kaaltv.com/article/stories/s3903070...</td>
      <td>6</td>
      <td>http://www.kaaltv.com/article/stories/s3903070...</td>
      <td>kaaltv.com</td>
      <td>This one always does look pretty rundown on th...</td>
      <td>0.4939</td>
      <td>0.262</td>
      <td>0.000</td>
      <td>0.738</td>
    </tr>
    <tr>
      <th>1559</th>
      <td>Chipotle salmonella</td>
      <td>3lb0n3</td>
      <td>all</td>
      <td>1.442529e+09</td>
      <td>Rochester Chipotle Restaurant Linked to Statew...</td>
      <td>6</td>
      <td>http://www.kaaltv.com/article/stories/s3903070...</td>
      <td>6</td>
      <td>http://www.kaaltv.com/article/stories/s3903070...</td>
      <td>kaaltv.com</td>
      <td>I went there a few hours ago..</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1560</th>
      <td>Chipotle salmonella</td>
      <td>3kmigm</td>
      <td>all</td>
      <td>1.442056e+09</td>
      <td>Minnesota Salmonella Outbreak Linked to Chipotle</td>
      <td>8</td>
      <td>http://time.com/4032218/chipotle-minnesota-sal...</td>
      <td>2</td>
      <td>http://time.com/4032218/chipotle-minnesota-sal...</td>
      <td>time.com</td>
      <td>What ingredient was contaminated?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1561</th>
      <td>Chipotle salmonella</td>
      <td>3kmigm</td>
      <td>all</td>
      <td>1.442056e+09</td>
      <td>Minnesota Salmonella Outbreak Linked to Chipotle</td>
      <td>8</td>
      <td>http://time.com/4032218/chipotle-minnesota-sal...</td>
      <td>2</td>
      <td>http://time.com/4032218/chipotle-minnesota-sal...</td>
      <td>time.com</td>
      <td>They are GMO free. Pity they couldn't make it ...</td>
      <td>0.6597</td>
      <td>0.393</td>
      <td>0.131</td>
      <td>0.476</td>
    </tr>
    <tr>
      <th>1562</th>
      <td>Chipotle salmonella</td>
      <td>44spy9</td>
      <td>all</td>
      <td>1.454991e+09</td>
      <td>How is it possible that there was salmonella i...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/shittyaskscience/comm...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/shittyaskscience/comm...</td>
      <td>self.shittyaskscience</td>
      <td>Well they don't serve it ANYMORE</td>
      <td>0.2732</td>
      <td>0.296</td>
      <td>0.000</td>
      <td>0.704</td>
    </tr>
  </tbody>
</table>
<p>1563 rows × 15 columns</p>
</div>




```python
chipotle_kws1.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1563 entries, 0 to 1562
    Data columns (total 15 columns):
    Keyword                      1563 non-null object
    Submission ID                1563 non-null object
    Subreddit                    1563 non-null object
    Created Date                 1563 non-null float64
    Submission Title             1563 non-null object
    Submission Score             1563 non-null int64
    Submission URL               1563 non-null object
    Total Submission Comments    1563 non-null int64
    Submission URL               1563 non-null object
    Domain                       1563 non-null object
    Submission Comments          1563 non-null object
    Compound Score               1563 non-null float64
    Positive Score               1563 non-null float64
    Negative Score               1563 non-null float64
    Neutral Score                1563 non-null float64
    dtypes: float64(5), int64(2), object(8)
    memory usage: 183.2+ KB



```python

#chipotle_kws1['Created Date'] = pd.to_datetime(chipotle_kws1['Created Date']).dt.date
chipotle_kws1['Created Date'] = pd.to_datetime(chipotle_kws1['Created Date'],unit='s')
#chipotle_kws1['Created Date'] = pd.to_datetime(chipotle_kws1['Created Date']).dt.date
chipotle_kws1['Created Date'] = chipotle_kws1['Created Date'].apply(lambda x: float(x.strftime('%s')))

```


```python
#chipotle plot

sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=chipotle_kws1, hue='Keyword', fit_reg=False)

plt.title("Chipotle Food Sickness Comments on Reddit")

plt.ylabel("Tweet Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y-%m-%d') for tm in xticks],
                  rotation=45)
#plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)

plt.show()
```


![png](output_59_0.png)



```python
#combine costco keywords
costco_kws1 = keyword_data['Costco e. coli']
costco_kws2 = keyword_data['Costco salmonella']
costco_kws3 = keyword_data['Costco food poisoning']

costco_kws1 = costco_kws1.append(costco_kws2)
costco_kws1 = costco_kws1.append(costco_kws3)

costco_kws1 = costco_kws1.reset_index()
del costco_kws1['index']
costco_kws1
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Costco e. coli</td>
      <td>3uajeq</td>
      <td>all</td>
      <td>1.448531e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>8</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>5</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>healthlatestnews.com</td>
      <td>BS\n\nCostco kitchens are spotless\n\nand the ...</td>
      <td>0.7003</td>
      <td>0.367</td>
      <td>0.000</td>
      <td>0.633</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Costco e. coli</td>
      <td>3uajeq</td>
      <td>all</td>
      <td>1.448531e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>8</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>5</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>healthlatestnews.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>-0.7506</td>
      <td>0.028</td>
      <td>0.084</td>
      <td>0.888</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Costco e. coli</td>
      <td>3uajeq</td>
      <td>all</td>
      <td>1.448531e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>8</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>5</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>healthlatestnews.com</td>
      <td>Welcome to Costco, I Luv U..Welcome to Costco,...</td>
      <td>0.4588</td>
      <td>0.130</td>
      <td>0.000</td>
      <td>0.870</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Costco e. coli</td>
      <td>3uajeq</td>
      <td>all</td>
      <td>1.448531e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>8</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>5</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>healthlatestnews.com</td>
      <td>BS\n\nCostco kitchens are spotless\n\nand the ...</td>
      <td>0.7003</td>
      <td>0.367</td>
      <td>0.000</td>
      <td>0.633</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Costco e. coli</td>
      <td>3uajeq</td>
      <td>all</td>
      <td>1.448531e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>8</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>5</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>healthlatestnews.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>-0.7506</td>
      <td>0.028</td>
      <td>0.084</td>
      <td>0.888</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Costco e. coli</td>
      <td>3uajeq</td>
      <td>all</td>
      <td>1.448531e+09</td>
      <td>E. coli tied to Costco more dangerous than Chi...</td>
      <td>8</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>5</td>
      <td>http://healthlatestnews.com/2015/11/26/491/e-c...</td>
      <td>healthlatestnews.com</td>
      <td>Welcome to Costco, I Luv U..Welcome to Costco,...</td>
      <td>0.4588</td>
      <td>0.130</td>
      <td>0.000</td>
      <td>0.870</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>&gt;Craig Wilson, Costco’s food safety director, ...</td>
      <td>-0.1531</td>
      <td>0.032</td>
      <td>0.043</td>
      <td>0.924</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>You just can't beat Costco for meat and cheese...</td>
      <td>0.6369</td>
      <td>0.296</td>
      <td>0.000</td>
      <td>0.704</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Did you read this from the provided wikipedia ...</td>
      <td>0.6743</td>
      <td>0.101</td>
      <td>0.046</td>
      <td>0.853</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Nothing surprises me from Tyson since he bit t...</td>
      <td>0.2263</td>
      <td>0.147</td>
      <td>0.000</td>
      <td>0.853</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Things like this are why I will be a lifetime ...</td>
      <td>0.3612</td>
      <td>0.217</td>
      <td>0.000</td>
      <td>0.783</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Every single day I hear more about Costco, it ...</td>
      <td>0.3417</td>
      <td>0.082</td>
      <td>0.000</td>
      <td>0.918</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>This was all handled years ago and the reason ...</td>
      <td>0.4917</td>
      <td>0.104</td>
      <td>0.076</td>
      <td>0.820</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Good.  Tyson is the worst of the factory farme...</td>
      <td>-0.1531</td>
      <td>0.193</td>
      <td>0.182</td>
      <td>0.625</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Their latest Costco Connection magazine has so...</td>
      <td>0.1010</td>
      <td>0.029</td>
      <td>0.017</td>
      <td>0.954</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>I had someone accuse me of being a terrorist w...</td>
      <td>-0.5023</td>
      <td>0.000</td>
      <td>0.200</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>I had Tyson teriyaki chicken before...the gros...</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.307</td>
      <td>0.693</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>While it's a fact they won't sell to Costco, w...</td>
      <td>-0.4215</td>
      <td>0.000</td>
      <td>0.061</td>
      <td>0.939</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Anyone else want to spam this to every single ...</td>
      <td>-0.2960</td>
      <td>0.088</td>
      <td>0.169</td>
      <td>0.743</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Submitting their meat for extra testing can on...</td>
      <td>-0.8618</td>
      <td>0.000</td>
      <td>0.236</td>
      <td>0.764</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>http://www.nytimes.com/2009/10/08/health/08mea...</td>
      <td>0.5983</td>
      <td>0.308</td>
      <td>0.000</td>
      <td>0.692</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Just picked up some Organic Rancher's ground b...</td>
      <td>0.6808</td>
      <td>0.193</td>
      <td>0.063</td>
      <td>0.744</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Repost.  And the next sentence goes on to say ...</td>
      <td>0.5994</td>
      <td>0.349</td>
      <td>0.000</td>
      <td>0.651</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>I love you.</td>
      <td>0.6369</td>
      <td>0.808</td>
      <td>0.000</td>
      <td>0.192</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Sounds to me like Tyson follows strong Liberta...</td>
      <td>0.7717</td>
      <td>0.562</td>
      <td>0.000</td>
      <td>0.438</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>Yummy Tyson! Aren't they the ones who make tho...</td>
      <td>0.5707</td>
      <td>0.187</td>
      <td>0.000</td>
      <td>0.813</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Costco e. coli</td>
      <td>hpry7</td>
      <td>all</td>
      <td>1.307031e+09</td>
      <td>Tyson won't sell beef to Costco, because Costc...</td>
      <td>511</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>76</td>
      <td>http://en.wikipedia.org/wiki/Tyson_Foods</td>
      <td>en.wikipedia.org</td>
      <td>You're thinking of "bitch" in a way that's sep...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Costco e. coli</td>
      <td>1oacvi</td>
      <td>all</td>
      <td>1.381612e+09</td>
      <td>Costco recalls beef over E. coli concerns in W...</td>
      <td>219</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>73</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>cbc.ca</td>
      <td>Costco is always the first to pull, and will b...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Costco e. coli</td>
      <td>1oacvi</td>
      <td>all</td>
      <td>1.381612e+09</td>
      <td>Costco recalls beef over E. coli concerns in W...</td>
      <td>219</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>73</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>cbc.ca</td>
      <td>Cook it properly.\n\nWhat's the issue?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Costco e. coli</td>
      <td>1oacvi</td>
      <td>all</td>
      <td>1.381612e+09</td>
      <td>Costco recalls beef over E. coli concerns in W...</td>
      <td>219</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>73</td>
      <td>http://www.cbc.ca/news/canada/edmonton/costco-...</td>
      <td>cbc.ca</td>
      <td>Any more information on this anywhere? Quite a...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
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
    </tr>
    <tr>
      <th>55</th>
      <td>Costco e. coli</td>
      <td>1okphe</td>
      <td>all</td>
      <td>1.381964e+09</td>
      <td>Costco Recall Western Canada E.Coli</td>
      <td>26</td>
      <td>https://www.reddit.com/r/BabyBumps/comments/1o...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/BabyBumps/comments/1o...</td>
      <td>self.BabyBumps</td>
      <td>My bad. The regular ground beef recall was las...</td>
      <td>0.3400</td>
      <td>0.263</td>
      <td>0.156</td>
      <td>0.580</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Costco e. coli</td>
      <td>1okphe</td>
      <td>all</td>
      <td>1.381964e+09</td>
      <td>Costco Recall Western Canada E.Coli</td>
      <td>26</td>
      <td>https://www.reddit.com/r/BabyBumps/comments/1o...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/BabyBumps/comments/1o...</td>
      <td>self.BabyBumps</td>
      <td>I'll find the link. Its not just the organic s...</td>
      <td>-0.0258</td>
      <td>0.066</td>
      <td>0.068</td>
      <td>0.867</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Costco e. coli</td>
      <td>1okphe</td>
      <td>all</td>
      <td>1.381964e+09</td>
      <td>Costco Recall Western Canada E.Coli</td>
      <td>26</td>
      <td>https://www.reddit.com/r/BabyBumps/comments/1o...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/BabyBumps/comments/1o...</td>
      <td>self.BabyBumps</td>
      <td>Aaaaaand this is why I don't eat meat.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Costco e. coli</td>
      <td>3u4pvo</td>
      <td>all</td>
      <td>1.448429e+09</td>
      <td>More E-Coli News: This Time, Costco (COST)</td>
      <td>8</td>
      <td>https://www.reddit.com/r/investing/comments/3u...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/investing/comments/3u...</td>
      <td>self.investing</td>
      <td>Damn, I just bought and ate some costco rotiss...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.252</td>
      <td>0.748</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Costco e. coli</td>
      <td>3v8ax5</td>
      <td>all</td>
      <td>1.449140e+09</td>
      <td>FDA Expands Recall of Food Items for E.Coli to...</td>
      <td>26</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>3</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>cnbc.com</td>
      <td>It's celery and things that contain celery. Do...</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.147</td>
      <td>0.853</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Costco e. coli</td>
      <td>3v8ax5</td>
      <td>all</td>
      <td>1.449140e+09</td>
      <td>FDA Expands Recall of Food Items for E.Coli to...</td>
      <td>26</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>3</td>
      <td>http://www.cnbc.com/2015/12/02/fda-expands-rec...</td>
      <td>cnbc.com</td>
      <td>So, wait. 7-11 is considered a Major Grocery S...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Costco e. coli</td>
      <td>3u4pjf</td>
      <td>all</td>
      <td>1.448429e+09</td>
      <td>Missouri Costco stores may have sold E. Coli-t...</td>
      <td>20</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>2</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>kctv5.com</td>
      <td>I'll still eat it.  That shit is delicious.</td>
      <td>0.0258</td>
      <td>0.278</td>
      <td>0.271</td>
      <td>0.451</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Costco e. coli</td>
      <td>3u4pjf</td>
      <td>all</td>
      <td>1.448429e+09</td>
      <td>Missouri Costco stores may have sold E. Coli-t...</td>
      <td>20</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>2</td>
      <td>http://www.kctv5.com/story/30598084/costco-chi...</td>
      <td>kctv5.com</td>
      <td>Boop Boop tainted cluck, whoaaaooo</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Costco e. coli</td>
      <td>1030g9</td>
      <td>all</td>
      <td>1.348012e+09</td>
      <td>Costco has announced a national recall on Kirk...</td>
      <td>24</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>9</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>thetelegram.com</td>
      <td>You will surely get the Kirkland Signature E. ...</td>
      <td>0.4404</td>
      <td>0.266</td>
      <td>0.000</td>
      <td>0.734</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Costco e. coli</td>
      <td>1030g9</td>
      <td>all</td>
      <td>1.348012e+09</td>
      <td>Costco has announced a national recall on Kirk...</td>
      <td>24</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>9</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>thetelegram.com</td>
      <td>One plus to being a costco member. They actual...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>65</th>
      <td>Costco e. coli</td>
      <td>1030g9</td>
      <td>all</td>
      <td>1.348012e+09</td>
      <td>Costco has announced a national recall on Kirk...</td>
      <td>24</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>9</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>thetelegram.com</td>
      <td>Kinda. None of the beef Costco received tested...</td>
      <td>0.8176</td>
      <td>0.187</td>
      <td>0.000</td>
      <td>0.813</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Costco e. coli</td>
      <td>1030g9</td>
      <td>all</td>
      <td>1.348012e+09</td>
      <td>Costco has announced a national recall on Kirk...</td>
      <td>24</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>9</td>
      <td>http://www.thetelegram.com/News/Local/2012-09-...</td>
      <td>thetelegram.com</td>
      <td>Why does anyone still eat industrial beef?!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Costco e. coli</td>
      <td>3uv57m</td>
      <td>all</td>
      <td>1.448928e+09</td>
      <td>[US - AZ] I believe I was infected by the E. C...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Start by contacting Costco and asking them wha...</td>
      <td>0.4927</td>
      <td>0.071</td>
      <td>0.000</td>
      <td>0.929</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Costco e. coli</td>
      <td>3uv57m</td>
      <td>all</td>
      <td>1.448928e+09</td>
      <td>[US - AZ] I believe I was infected by the E. C...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>To the best of my knowledge Costco's food cour...</td>
      <td>0.6369</td>
      <td>0.144</td>
      <td>0.000</td>
      <td>0.856</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Costco e. coli</td>
      <td>3uv57m</td>
      <td>all</td>
      <td>1.448928e+09</td>
      <td>[US - AZ] I believe I was infected by the E. C...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>15</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>I got food poisoning from Costco a few years b...</td>
      <td>-0.9185</td>
      <td>0.042</td>
      <td>0.063</td>
      <td>0.895</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Costco e. coli</td>
      <td>1oarxe</td>
      <td>all</td>
      <td>1.381627e+09</td>
      <td>Costco, CFIA issue beef recall over E. coli ri...</td>
      <td>0</td>
      <td>http://www.theglobeandmail.com/news/national/c...</td>
      <td>2</td>
      <td>http://www.theglobeandmail.com/news/national/c...</td>
      <td>theglobeandmail.com</td>
      <td>1. Don't editorialize titles.\n2. And, what is...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Costco e. coli</td>
      <td>1oarxe</td>
      <td>all</td>
      <td>1.381627e+09</td>
      <td>Costco, CFIA issue beef recall over E. coli ri...</td>
      <td>0</td>
      <td>http://www.theglobeandmail.com/news/national/c...</td>
      <td>2</td>
      <td>http://www.theglobeandmail.com/news/national/c...</td>
      <td>theglobeandmail.com</td>
      <td>They process 5,000 pounds of organic beef per ...</td>
      <td>0.6705</td>
      <td>0.198</td>
      <td>0.057</td>
      <td>0.746</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>And another reason I don't buy FF anymore.  Be...</td>
      <td>-0.5909</td>
      <td>0.000</td>
      <td>0.066</td>
      <td>0.934</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>I've been reading about this recently and foun...</td>
      <td>0.3818</td>
      <td>0.104</td>
      <td>0.052</td>
      <td>0.844</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>Almost all chicken you get in America has Salm...</td>
      <td>0.2732</td>
      <td>0.095</td>
      <td>0.000</td>
      <td>0.905</td>
    </tr>
    <tr>
      <th>75</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>GET THIS:\n\nNob Hill (Raley's) is being told ...</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.149</td>
      <td>0.851</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>As long as the hot dogs are fine, I'm ok.</td>
      <td>0.4588</td>
      <td>0.333</td>
      <td>0.000</td>
      <td>0.667</td>
    </tr>
    <tr>
      <th>77</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>Well, salmonella is "always natural, always fr...</td>
      <td>0.5574</td>
      <td>0.434</td>
      <td>0.000</td>
      <td>0.566</td>
    </tr>
    <tr>
      <th>78</th>
      <td>Costco salmonella</td>
      <td>1oe6xm</td>
      <td>all</td>
      <td>1.381742e+09</td>
      <td>South San Francisco Costco recalls Foster Farm...</td>
      <td>59</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>13</td>
      <td>http://www.sfgate.com/default/article/South-Sa...</td>
      <td>sfgate.com</td>
      <td>ah poop</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>79</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Do you have any of the sandwiches left (refrig...</td>
      <td>0.8412</td>
      <td>0.118</td>
      <td>0.045</td>
      <td>0.836</td>
    </tr>
    <tr>
      <th>80</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Not a lawyer, but I am a microbiologist in the...</td>
      <td>0.6939</td>
      <td>0.086</td>
      <td>0.069</td>
      <td>0.846</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Call your local county board of health. This i...</td>
      <td>0.1280</td>
      <td>0.078</td>
      <td>0.067</td>
      <td>0.855</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>How were these sandwiches stored before the ga...</td>
      <td>0.4696</td>
      <td>0.117</td>
      <td>0.000</td>
      <td>0.883</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>This reminds me a lot of a pot luck gone bad i...</td>
      <td>-0.1513</td>
      <td>0.061</td>
      <td>0.059</td>
      <td>0.880</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Costco food poisoning</td>
      <td>3l8p74</td>
      <td>all</td>
      <td>1.442478e+09</td>
      <td>50+ family members got food poisoning and have...</td>
      <td>22</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Call DEC or the board of health in your hometo...</td>
      <td>-0.1531</td>
      <td>0.000</td>
      <td>0.049</td>
      <td>0.951</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 15 columns</p>
</div>




```python
#Costco plot

sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=costco_kws1, hue='Keyword', fit_reg=False)

plt.title("Costco Food Sickness Comments on Reddit")

plt.ylabel("Tweet Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y-%m-%d') for tm in xticks],
                  rotation=45)

#plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)

plt.show()
```


![png](output_61_0.png)



```python
#combine taco_bell keywords
taco_bell_kws1 = keyword_data['Taco Bell food poisoning']
taco_bell_kws2 = keyword_data['Taco Bell e. coli']
taco_bell_kws3 = keyword_data['Taco Bell salmonella']

taco_bell_kws1 = taco_bell_kws1.append(taco_bell_kws2)
taco_bell_kws1 = taco_bell_kws1.append(taco_bell_kws3)

taco_bell_kws1 = taco_bell_kws1.reset_index()
del taco_bell_kws1['index']
taco_bell_kws1
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Taco Bell food poisoning</td>
      <td>4nhaw5</td>
      <td>all</td>
      <td>1.465607e+09</td>
      <td>Former #1 Mexican restaurant Chipotle has fall...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>usatoday.com</td>
      <td>Wtf</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Taco Bell food poisoning</td>
      <td>4nhaw5</td>
      <td>all</td>
      <td>1.465607e+09</td>
      <td>Former #1 Mexican restaurant Chipotle has fall...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>usatoday.com</td>
      <td>Does nobody remember the [Jack in the Box E.Co...</td>
      <td>-0.4939</td>
      <td>0.000</td>
      <td>0.211</td>
      <td>0.789</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Taco Bell food poisoning</td>
      <td>4nhaw5</td>
      <td>all</td>
      <td>1.465607e+09</td>
      <td>Former #1 Mexican restaurant Chipotle has fall...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>usatoday.com</td>
      <td>I feel bad for anyone who thinks Chipotle is M...</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.280</td>
      <td>0.720</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Taco Bell food poisoning</td>
      <td>4nhaw5</td>
      <td>all</td>
      <td>1.465607e+09</td>
      <td>Former #1 Mexican restaurant Chipotle has fall...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>usatoday.com</td>
      <td>Wtf</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Taco Bell food poisoning</td>
      <td>4nhaw5</td>
      <td>all</td>
      <td>1.465607e+09</td>
      <td>Former #1 Mexican restaurant Chipotle has fall...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>usatoday.com</td>
      <td>Does nobody remember the [Jack in the Box E.Co...</td>
      <td>-0.4939</td>
      <td>0.000</td>
      <td>0.211</td>
      <td>0.789</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Taco Bell food poisoning</td>
      <td>4nhaw5</td>
      <td>all</td>
      <td>1.465607e+09</td>
      <td>Former #1 Mexican restaurant Chipotle has fall...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>4</td>
      <td>http://www.usatoday.com/story/money/2016/06/09...</td>
      <td>usatoday.com</td>
      <td>I feel bad for anyone who thinks Chipotle is M...</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.280</td>
      <td>0.720</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Taco Bell food poisoning</td>
      <td>76vfad</td>
      <td>all</td>
      <td>1.508234e+09</td>
      <td>When you get food poisoning from Taco Bell.</td>
      <td>164</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>10</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>i.imgur.com</td>
      <td>Too technical. I don't understand, can someone...</td>
      <td>0.2263</td>
      <td>0.213</td>
      <td>0.000</td>
      <td>0.787</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Taco Bell food poisoning</td>
      <td>76vfad</td>
      <td>all</td>
      <td>1.508234e+09</td>
      <td>When you get food poisoning from Taco Bell.</td>
      <td>164</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>10</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>i.imgur.com</td>
      <td>i did what</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Taco Bell food poisoning</td>
      <td>76vfad</td>
      <td>all</td>
      <td>1.508234e+09</td>
      <td>When you get food poisoning from Taco Bell.</td>
      <td>164</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>10</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>i.imgur.com</td>
      <td>The good elephant in airship dropped what things?</td>
      <td>0.4404</td>
      <td>0.293</td>
      <td>0.000</td>
      <td>0.707</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Taco Bell food poisoning</td>
      <td>76vfad</td>
      <td>all</td>
      <td>1.508234e+09</td>
      <td>When you get food poisoning from Taco Bell.</td>
      <td>164</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>10</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>i.imgur.com</td>
      <td>This...is what who fart?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Taco Bell food poisoning</td>
      <td>76vfad</td>
      <td>all</td>
      <td>1.508234e+09</td>
      <td>When you get food poisoning from Taco Bell.</td>
      <td>164</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>10</td>
      <td>https://i.imgur.com/az38FuB.png</td>
      <td>i.imgur.com</td>
      <td>What is this from</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>You're gonna be OK. I used to have a bad habit...</td>
      <td>-0.1830</td>
      <td>0.119</td>
      <td>0.141</td>
      <td>0.740</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>Mods ain't asleep pls we are drunks :)</td>
      <td>0.4172</td>
      <td>0.293</td>
      <td>0.120</td>
      <td>0.587</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>Once I ate some tacos from taco bell and was l...</td>
      <td>-0.6641</td>
      <td>0.136</td>
      <td>0.207</td>
      <td>0.657</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>I think the ingredients in Taco Bell aren't pa...</td>
      <td>0.8071</td>
      <td>0.256</td>
      <td>0.104</td>
      <td>0.640</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>I've woken up cuddling the 12 taco box in bed ...</td>
      <td>0.6369</td>
      <td>0.144</td>
      <td>0.000</td>
      <td>0.856</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>Taco Bell can't go bad because it was never go...</td>
      <td>0.1139</td>
      <td>0.175</td>
      <td>0.148</td>
      <td>0.677</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>Mmmm, Taco Bell...that sounds delightful.</td>
      <td>0.5859</td>
      <td>0.487</td>
      <td>0.000</td>
      <td>0.513</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>Lol!\n\n6 hours ain't shit to taco bell.\n\nAn...</td>
      <td>0.7309</td>
      <td>0.179</td>
      <td>0.047</td>
      <td>0.773</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>If it's still the same day left over fast food...</td>
      <td>0.6566</td>
      <td>0.109</td>
      <td>0.000</td>
      <td>0.891</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>Taco Bell is like half salt. No worries any ea...</td>
      <td>-0.6369</td>
      <td>0.095</td>
      <td>0.294</td>
      <td>0.611</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>*Tacobellius bacilius* is one of the most resi...</td>
      <td>0.7906</td>
      <td>0.182</td>
      <td>0.048</td>
      <td>0.769</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>This thread is cracking me up.  I can't even c...</td>
      <td>0.4389</td>
      <td>0.163</td>
      <td>0.070</td>
      <td>0.767</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>You're fine. 6 hours is not enough time for an...</td>
      <td>-0.3818</td>
      <td>0.105</td>
      <td>0.198</td>
      <td>0.698</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>6 hours is nothing</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Taco Bell food poisoning</td>
      <td>3z4lqk</td>
      <td>all</td>
      <td>1.451758e+09</td>
      <td>Fuck it, taco bell that's been sitting out for...</td>
      <td>24</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>34</td>
      <td>https://www.reddit.com/r/cripplingalcoholism/c...</td>
      <td>self.cripplingalcoholism</td>
      <td>I have on multiple occasions eaten the leftove...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>It would not surprise me one bit if people got...</td>
      <td>-0.6266</td>
      <td>0.000</td>
      <td>0.317</td>
      <td>0.683</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>Got food poisoning at the Taco Bell on college...</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>0.275</td>
      <td>0.725</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>Nope. Ate it around 11pm.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>What did you order?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>I feel like seeing the Taco Bell logo should j...</td>
      <td>-0.2023</td>
      <td>0.053</td>
      <td>0.071</td>
      <td>0.876</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>I got some food around midnight.  Not sick.</td>
      <td>-0.5106</td>
      <td>0.000</td>
      <td>0.355</td>
      <td>0.645</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Taco Bell food poisoning</td>
      <td>12wukq</td>
      <td>all</td>
      <td>1.352498e+09</td>
      <td>Food poisoning from airport taco bell?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/Fairbanks/comments/12...</td>
      <td>self.Fairbanks</td>
      <td>I didn't eat there last night, but I do eat th...</td>
      <td>0.5504</td>
      <td>0.192</td>
      <td>0.000</td>
      <td>0.808</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Taco Bell food poisoning</td>
      <td>4hnlwj</td>
      <td>all</td>
      <td>1.462316e+09</td>
      <td>On average - how many food poisoning reports d...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4h...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4h...</td>
      <td>self.AskReddit</td>
      <td>Probably very few.  Nowadays any sort of food ...</td>
      <td>-0.5324</td>
      <td>0.125</td>
      <td>0.145</td>
      <td>0.730</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Taco Bell food poisoning</td>
      <td>4hnlwj</td>
      <td>all</td>
      <td>1.462316e+09</td>
      <td>On average - how many food poisoning reports d...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4h...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4h...</td>
      <td>self.AskReddit</td>
      <td>about 6 per week. And someone eats them.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Taco Bell food poisoning</td>
      <td>1s51we</td>
      <td>all</td>
      <td>1.386249e+09</td>
      <td>ELI5: How and why your stomach/intestines reac...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>They overreact.  A lot of the time you get sic...</td>
      <td>-0.4588</td>
      <td>0.102</td>
      <td>0.159</td>
      <td>0.739</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Taco Bell food poisoning</td>
      <td>164c2v</td>
      <td>all</td>
      <td>1.357597e+09</td>
      <td>Taco Bell, how could you do me so wrong? This ...</td>
      <td>0</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>4</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>i.imgur.com</td>
      <td>And yet they keep going back....</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Taco Bell food poisoning</td>
      <td>164c2v</td>
      <td>all</td>
      <td>1.357597e+09</td>
      <td>Taco Bell, how could you do me so wrong? This ...</td>
      <td>0</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>4</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>i.imgur.com</td>
      <td>You went back after the first time?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Taco Bell food poisoning</td>
      <td>164c2v</td>
      <td>all</td>
      <td>1.357597e+09</td>
      <td>Taco Bell, how could you do me so wrong? This ...</td>
      <td>0</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>4</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>i.imgur.com</td>
      <td>Call the board of health and have them inspect...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Taco Bell food poisoning</td>
      <td>164c2v</td>
      <td>all</td>
      <td>1.357597e+09</td>
      <td>Taco Bell, how could you do me so wrong? This ...</td>
      <td>0</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>4</td>
      <td>http://i.imgur.com/Bmhb1.jpg</td>
      <td>i.imgur.com</td>
      <td>Post on /r/wtf maybe?  Taco Bell brand advocat...</td>
      <td>0.2023</td>
      <td>0.083</td>
      <td>0.000</td>
      <td>0.917</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Taco Bell e. coli</td>
      <td>3vx31d</td>
      <td>all</td>
      <td>1.449604e+09</td>
      <td>Chipotle vs Taco Bell's comps after E Coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
      <td>It's not good right now at all but if it gets ...</td>
      <td>-0.3824</td>
      <td>0.088</td>
      <td>0.122</td>
      <td>0.790</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Taco Bell e. coli</td>
      <td>3vx31d</td>
      <td>all</td>
      <td>1.449604e+09</td>
      <td>Chipotle vs Taco Bell's comps after E Coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
      <td>I am perplexed to see that people are still ea...</td>
      <td>-0.6221</td>
      <td>0.000</td>
      <td>0.152</td>
      <td>0.848</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Taco Bell e. coli</td>
      <td>3vx31d</td>
      <td>all</td>
      <td>1.449604e+09</td>
      <td>Chipotle vs Taco Bell's comps after E Coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
      <td>Make the same graph for jack in the box pre an...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Taco Bell e. coli</td>
      <td>3vx31d</td>
      <td>all</td>
      <td>1.449604e+09</td>
      <td>Chipotle vs Taco Bell's comps after E Coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
      <td>It's not good right now at all but if it gets ...</td>
      <td>-0.3824</td>
      <td>0.088</td>
      <td>0.122</td>
      <td>0.790</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Taco Bell e. coli</td>
      <td>3vx31d</td>
      <td>all</td>
      <td>1.449604e+09</td>
      <td>Chipotle vs Taco Bell's comps after E Coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
      <td>I am perplexed to see that people are still ea...</td>
      <td>-0.6221</td>
      <td>0.000</td>
      <td>0.152</td>
      <td>0.848</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Taco Bell e. coli</td>
      <td>3vx31d</td>
      <td>all</td>
      <td>1.449604e+09</td>
      <td>Chipotle vs Taco Bell's comps after E Coli out...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/investing/comments/3v...</td>
      <td>self.investing</td>
      <td>Make the same graph for jack in the box pre an...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Taco Bell salmonella</td>
      <td>p8ff0</td>
      <td>all</td>
      <td>1.328254e+09</td>
      <td>OKC Salmonella Outbreak Tied to Taco Bell</td>
      <td>9</td>
      <td>http://www.koco.com/health/30357955/detail.html</td>
      <td>5</td>
      <td>http://www.koco.com/health/30357955/detail.html</td>
      <td>koco.com</td>
      <td>And um... How long does the sickness take to  ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Taco Bell salmonella</td>
      <td>p8ff0</td>
      <td>all</td>
      <td>1.328254e+09</td>
      <td>OKC Salmonella Outbreak Tied to Taco Bell</td>
      <td>9</td>
      <td>http://www.koco.com/health/30357955/detail.html</td>
      <td>5</td>
      <td>http://www.koco.com/health/30357955/detail.html</td>
      <td>koco.com</td>
      <td>Which one?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Taco Bell salmonella</td>
      <td>p8ff0</td>
      <td>all</td>
      <td>1.328254e+09</td>
      <td>OKC Salmonella Outbreak Tied to Taco Bell</td>
      <td>9</td>
      <td>http://www.koco.com/health/30357955/detail.html</td>
      <td>5</td>
      <td>http://www.koco.com/health/30357955/detail.html</td>
      <td>koco.com</td>
      <td>is anybody surprised by this?</td>
      <td>0.2263</td>
      <td>0.322</td>
      <td>0.000</td>
      <td>0.678</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Taco Bell salmonella</td>
      <td>p7sdy</td>
      <td>all</td>
      <td>1.328227e+09</td>
      <td>Taco Bell Linked To Salmonella Probe after 68 ...</td>
      <td>11</td>
      <td>http://www.myfoxdc.com/dpp/news/taco-bell-link...</td>
      <td>1</td>
      <td>http://www.myfoxdc.com/dpp/news/taco-bell-link...</td>
      <td>myfoxdc.com</td>
      <td>How many fall ill after eating Taco Bell on a ...</td>
      <td>-0.4215</td>
      <td>0.000</td>
      <td>0.219</td>
      <td>0.781</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Taco Bell salmonella</td>
      <td>pi0xm</td>
      <td>all</td>
      <td>1.328838e+09</td>
      <td>Restaurant A: How Food Safety News Tied Taco B...</td>
      <td>3</td>
      <td>http://www.theatlantic.com/health/archive/2012...</td>
      <td>2</td>
      <td>http://www.theatlantic.com/health/archive/2012...</td>
      <td>theatlantic.com</td>
      <td>Ugh. I like the Atlantic, but this is sloppy r...</td>
      <td>-0.8914</td>
      <td>0.025</td>
      <td>0.176</td>
      <td>0.799</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Taco Bell plot

sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=taco_bell_kws1, hue='Keyword', fit_reg=False)

plt.title("Taco Bell Food Sickness Comments on Reddit")

plt.ylabel("Tweet Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y-%m-%d') for tm in xticks],
                  rotation=45)

#plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)

plt.show()
```


![png](output_63_0.png)



```python
#burger_king kws
burger_king_kws1 = keyword_data['Burger King e. coli']
burger_king_kws2 = keyword_data['Burger King food poisoning']
burger_king_kws3 = keyword_data['Burger King salmonella']

burger_king_kws1 = burger_king_kws1.append(burger_king_kws2)
burger_king_kws1 = burger_king_kws1.append(burger_king_kws3)

burger_king_kws1 = burger_king_kws1.reset_index()
del burger_king_kws1['index']
burger_king_kws1

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Foreshadowing</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Ygh.  That pattern reminds me why I mash my gr...</td>
      <td>0.4939</td>
      <td>0.138</td>
      <td>0.000</td>
      <td>0.862</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>I’m glad Burger King is showing the correct Gr...</td>
      <td>0.4588</td>
      <td>0.158</td>
      <td>0.000</td>
      <td>0.842</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Always make promises you can keep.</td>
      <td>0.3818</td>
      <td>0.342</td>
      <td>0.000</td>
      <td>0.658</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Less than appetizing</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>The buildup over the years has formed a Level ...</td>
      <td>-0.3818</td>
      <td>0.000</td>
      <td>0.206</td>
      <td>0.794</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>This is Memphis Group design aesthetic.\n\nLik...</td>
      <td>0.3612</td>
      <td>0.200</td>
      <td>0.000</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Could also be ketchup (which would still be re...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Funny you mention E-Coli, there was a little 6...</td>
      <td>0.3313</td>
      <td>0.104</td>
      <td>0.063</td>
      <td>0.834</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>It basically is anyways</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Just a heads up</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>At least it’s not foot lettuce.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Tastes like it too</td>
      <td>0.3612</td>
      <td>0.455</td>
      <td>0.000</td>
      <td>0.545</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>the shines from the lights are a lot more visi...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>E.coli usually comes from contaminated food so...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>I now know what E Coli looks like lol</td>
      <td>0.6486</td>
      <td>0.515</td>
      <td>0.000</td>
      <td>0.485</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Burger King e. coli</td>
      <td>7wohs5</td>
      <td>all</td>
      <td>1.518328e+09</td>
      <td>This table at Burger King looks like E Coli</td>
      <td>365</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>28</td>
      <td>https://i.redd.it/wk7dgog7igf01.jpg</td>
      <td>i.redd.it</td>
      <td>Probably tastes like E Coli too</td>
      <td>0.3612</td>
      <td>0.385</td>
      <td>0.000</td>
      <td>0.615</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Ammonia is hardly exotic to the body; it is a ...</td>
      <td>-0.6808</td>
      <td>0.000</td>
      <td>0.075</td>
      <td>0.925</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>yea, let's do this instead of fixing the probl...</td>
      <td>-0.8883</td>
      <td>0.000</td>
      <td>0.377</td>
      <td>0.623</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>does anyone know if this same sort of thing is...</td>
      <td>0.5994</td>
      <td>0.234</td>
      <td>0.000</td>
      <td>0.766</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Besides the if it's harmful or not debate: isn...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>&gt; You can get the same effect by opening a can...</td>
      <td>0.4404</td>
      <td>0.073</td>
      <td>0.000</td>
      <td>0.927</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>We went through this on another thread a coupl...</td>
      <td>-0.8741</td>
      <td>0.040</td>
      <td>0.198</td>
      <td>0.762</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>I don't eat fast food. Those who do get what t...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Original NYT article: [Safety of Beef Processi...</td>
      <td>0.3182</td>
      <td>0.204</td>
      <td>0.000</td>
      <td>0.796</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>burgers = window cleaner? wtf\n\nI love the im...</td>
      <td>0.2732</td>
      <td>0.353</td>
      <td>0.228</td>
      <td>0.419</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Mike Adams, "Health Ranger"...isn't that the s...</td>
      <td>0.6172</td>
      <td>0.092</td>
      <td>0.043</td>
      <td>0.865</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Burger King e. coli</td>
      <td>anxt4</td>
      <td>all</td>
      <td>1.263190e+09</td>
      <td>USDA okay with ammonia in burgers: Beef sold t...</td>
      <td>67</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>38</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>No wonder American "food" tastes so fucking ba...</td>
      <td>-0.7408</td>
      <td>0.000</td>
      <td>0.269</td>
      <td>0.731</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>So what if it's used in window cleaner? So is ...</td>
      <td>0.9332</td>
      <td>0.208</td>
      <td>0.034</td>
      <td>0.759</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Yet irradiation would completely prevent this ...</td>
      <td>-0.7433</td>
      <td>0.040</td>
      <td>0.219</td>
      <td>0.741</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>You can use ammonium carbonate a leavener in s...</td>
      <td>0.2433</td>
      <td>0.091</td>
      <td>0.091</td>
      <td>0.818</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>This seems suspect.  Fast food places like mcd...</td>
      <td>-0.5574</td>
      <td>0.039</td>
      <td>0.112</td>
      <td>0.849</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Crap. I've been going the other way and swallo...</td>
      <td>-0.3818</td>
      <td>0.000</td>
      <td>0.167</td>
      <td>0.833</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>nasty motherfuckers...that is all I am going t...</td>
      <td>-0.1027</td>
      <td>0.154</td>
      <td>0.173</td>
      <td>0.673</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>And I thought my hamburger smelled 'fishy.'  B...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>The reason ammonia, irradiation or high temper...</td>
      <td>0.0772</td>
      <td>0.104</td>
      <td>0.099</td>
      <td>0.797</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Some E. coli bacteria only thrive on ammonia, ...</td>
      <td>0.1027</td>
      <td>0.170</td>
      <td>0.125</td>
      <td>0.705</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Burger King e. coli</td>
      <td>anww0</td>
      <td>all</td>
      <td>1.263184e+09</td>
      <td>USDA okay with ammonia in burgers: \nBeef sold...</td>
      <td>46</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>26</td>
      <td>http://www.NaturalNews.com/027872_ammonia_beef...</td>
      <td>naturalnews.com</td>
      <td>Care?</td>
      <td>0.4939</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Burger King food poisoning</td>
      <td>2b5ldt</td>
      <td>all</td>
      <td>1.405829e+09</td>
      <td>MRW I get food poisoning from eating Burger King</td>
      <td>60</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>4</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>giant.gfycat.com</td>
      <td>Can't you sue for getting food poisoning from ...</td>
      <td>-0.5859</td>
      <td>0.000</td>
      <td>0.297</td>
      <td>0.703</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Burger King food poisoning</td>
      <td>2b5ldt</td>
      <td>all</td>
      <td>1.405829e+09</td>
      <td>MRW I get food poisoning from eating Burger King</td>
      <td>60</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>4</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>giant.gfycat.com</td>
      <td>Should have had chicken instead.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Burger King food poisoning</td>
      <td>2b5ldt</td>
      <td>all</td>
      <td>1.405829e+09</td>
      <td>MRW I get food poisoning from eating Burger King</td>
      <td>60</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>4</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>giant.gfycat.com</td>
      <td>Repost...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Burger King food poisoning</td>
      <td>2b5ldt</td>
      <td>all</td>
      <td>1.405829e+09</td>
      <td>MRW I get food poisoning from eating Burger King</td>
      <td>60</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>4</td>
      <td>http://giant.gfycat.com/PlumpLeftKatydid.gif</td>
      <td>giant.gfycat.com</td>
      <td>http://i.imgur.com/R4ig9ia.gif</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Burger King food poisoning</td>
      <td>6nvct</td>
      <td>all</td>
      <td>1.213810e+09</td>
      <td>Burger King's $180 burger - whoever eats this,...</td>
      <td>3</td>
      <td>http://www.telegraph.co.uk/news/2146001/Burger...</td>
      <td>2</td>
      <td>http://www.telegraph.co.uk/news/2146001/Burger...</td>
      <td>telegraph.co.uk</td>
      <td>Yer you can feel the bling with plastic trays ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Burger King food poisoning</td>
      <td>6nvct</td>
      <td>all</td>
      <td>1.213810e+09</td>
      <td>Burger King's $180 burger - whoever eats this,...</td>
      <td>3</td>
      <td>http://www.telegraph.co.uk/news/2146001/Burger...</td>
      <td>2</td>
      <td>http://www.telegraph.co.uk/news/2146001/Burger...</td>
      <td>telegraph.co.uk</td>
      <td>In-N-Out has nothing to worry about. Nobody ca...</td>
      <td>0.3412</td>
      <td>0.211</td>
      <td>0.000</td>
      <td>0.789</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Damn, those are some fast symptoms.</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.351</td>
      <td>0.649</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>See s-dubya's response.  This isn't a legal is...</td>
      <td>-0.7327</td>
      <td>0.057</td>
      <td>0.328</td>
      <td>0.615</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>Talk to BK corporate - see what they offer up....</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>See a doctor.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>You should have kept it but you can't change t...</td>
      <td>-0.9834</td>
      <td>0.000</td>
      <td>0.209</td>
      <td>0.791</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Burger King salmonella</td>
      <td>3wqd6v</td>
      <td>all</td>
      <td>1.450090e+09</td>
      <td>I was just served raw chicken at a Burger King...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>17</td>
      <td>https://www.reddit.com/r/legaladvice/comments/...</td>
      <td>self.legaladvice</td>
      <td>*I am a bot whose sole purpose is to improve t...</td>
      <td>0.8738</td>
      <td>0.116</td>
      <td>0.050</td>
      <td>0.834</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Burger King plot

sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=burger_king_kws1, hue='Keyword', fit_reg=False)

plt.title("Burger King Food Sickness Comments on Reddit")

plt.ylabel("Tweet Polarity")
plt.xlabel("Date")

plt.grid(True)
#plt.xlim([100, 0])
plt.ylim([-1, 1])

ax = plt.gca()
xticks = ax.get_xticks()
ax.set_xticklabels([pd.to_datetime(tm, unit='s').strftime('%Y-%m-%d') for tm in xticks],
                  rotation=45)

#plt.savefig("Sentiment_Analysis_Tweets.png", dpi=150)

plt.show()
```


![png](output_65_0.png)

