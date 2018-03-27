

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

keywords = ["food allergy", "food poisoning", "foodborne illness", "e. coli", 
            "salmonella", "Norovirus"]

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
      <th>2</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
    </tr>
    <tr>
      <th>1594</th>
      <td>salmonella</td>
      <td>3enx5l</td>
      <td>all</td>
      <td>1.437952e+09</td>
      <td>Unprecedented Life Sentence Recommended for Pe...</td>
      <td>19582</td>
      <td>http://www.foodsafetymagazine.com/news/unprece...</td>
      <td>2058</td>
      <td>http://www.foodsafetymagazine.com/news/unprece...</td>
      <td>foodsafetymagazine.com</td>
    </tr>
    <tr>
      <th>1149</th>
      <td>e. coli</td>
      <td>1okza1</td>
      <td>all</td>
      <td>1.381971e+09</td>
      <td>Abdominal surgery + really bad e. coli = big h...</td>
      <td>2251</td>
      <td>http://i.imgur.com/5rMuBVp.jpg</td>
      <td>2026</td>
      <td>http://i.imgur.com/5rMuBVp.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1593</th>
      <td>salmonella</td>
      <td>3luw0z</td>
      <td>all</td>
      <td>1.442900e+09</td>
      <td>Peanut company CEO sentenced to 28 years in pr...</td>
      <td>26961</td>
      <td>http://bigstory.ap.org/article/823078b586f64cf...</td>
      <td>2017</td>
      <td>http://bigstory.ap.org/article/823078b586f64cf...</td>
      <td>bigstory.ap.org</td>
    </tr>
    <tr>
      <th>1592</th>
      <td>salmonella</td>
      <td>6rluwc</td>
      <td>all</td>
      <td>1.501895e+09</td>
      <td>TIL that due to EU regulations, EU eggs are ab...</td>
      <td>16391</td>
      <td>https://www.youtube.com/watch?v=Xbqv1SuQJ0s</td>
      <td>1990</td>
      <td>https://www.youtube.com/watch?v=Xbqv1SuQJ0s</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>1595</th>
      <td>salmonella</td>
      <td>479wz1</td>
      <td>all</td>
      <td>1.456305e+09</td>
      <td>TIL the UK virtually eliminated salmonella by ...</td>
      <td>22377</td>
      <td>http://www.nytimes.com/2010/08/25/business/25v...</td>
      <td>1930</td>
      <td>http://www.nytimes.com/2010/08/25/business/25v...</td>
      <td>nytimes.com</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>21w3ki</td>
      <td>all</td>
      <td>1.396351e+09</td>
      <td>ELI5: Why does it seem like so many more child...</td>
      <td>2292</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>1807</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
    </tr>
    <tr>
      <th>1599</th>
      <td>salmonella</td>
      <td>63e109</td>
      <td>all</td>
      <td>1.491341e+09</td>
      <td>TIL of the Rajneeshee bioterror attack, in 198...</td>
      <td>36985</td>
      <td>https://en.wikipedia.org/wiki/1984_Rajneeshee_...</td>
      <td>1584</td>
      <td>https://en.wikipedia.org/wiki/1984_Rajneeshee_...</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>41cnpt</td>
      <td>all</td>
      <td>1.453047e+09</td>
      <td>Why food allergy fakers need to stop -- From g...</td>
      <td>4359</td>
      <td>https://www.bostonglobe.com/magazine/2015/10/1...</td>
      <td>1529</td>
      <td>https://www.bostonglobe.com/magazine/2015/10/1...</td>
      <td>bostonglobe.com</td>
    </tr>
    <tr>
      <th>480</th>
      <td>food poisoning</td>
      <td>1mrtds</td>
      <td>all</td>
      <td>1.379707e+09</td>
      <td>3 years ago i got severe food poisoning after ...</td>
      <td>2166</td>
      <td>http://i.imgur.com/7k1VCr8.jpg</td>
      <td>1448</td>
      <td>http://i.imgur.com/7k1VCr8.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1601</th>
      <td>salmonella</td>
      <td>3tdbol</td>
      <td>all</td>
      <td>1.447923e+09</td>
      <td>TIL that in 1984 a cult spread salmonella on s...</td>
      <td>20750</td>
      <td>https://en.wikipedia.org/wiki/1984_Rajneeshee_...</td>
      <td>1169</td>
      <td>https://en.wikipedia.org/wiki/1984_Rajneeshee_...</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>1148</th>
      <td>e. coli</td>
      <td>7qiz1r</td>
      <td>all</td>
      <td>1.516042e+09</td>
      <td>Surfers more likely to harbour antibiotic resi...</td>
      <td>32326</td>
      <td>https://www.independent.co.uk/news/health/surf...</td>
      <td>1063</td>
      <td>https://www.independent.co.uk/news/health/surf...</td>
      <td>independent.co.uk</td>
    </tr>
    <tr>
      <th>2058</th>
      <td>Norovirus</td>
      <td>4a05qr</td>
      <td>all</td>
      <td>1.457751e+09</td>
      <td>ELI5: Since Norovirus is not a food-borne illn...</td>
      <td>3623</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>1062</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>49jixd</td>
      <td>all</td>
      <td>1.457487e+09</td>
      <td>I never realised how great having no food alle...</td>
      <td>12695</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>1019</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
    </tr>
    <tr>
      <th>1145</th>
      <td>e. coli</td>
      <td>3ejvhv</td>
      <td>all</td>
      <td>1.437854e+09</td>
      <td>City waits 7 hours before warning people about...</td>
      <td>9907</td>
      <td>http://www.kristv.com/story/29627802/city-told...</td>
      <td>1013</td>
      <td>http://www.kristv.com/story/29627802/city-told...</td>
      <td>kristv.com</td>
    </tr>
    <tr>
      <th>486</th>
      <td>food poisoning</td>
      <td>1f743v</td>
      <td>all</td>
      <td>1.369776e+09</td>
      <td>What food gave you the worst food poisoning? W...</td>
      <td>215</td>
      <td>https://www.reddit.com/r/AskReddit/comments/1f...</td>
      <td>1004</td>
      <td>https://www.reddit.com/r/AskReddit/comments/1f...</td>
      <td>self.AskReddit</td>
    </tr>
    <tr>
      <th>0</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
    </tr>
    <tr>
      <th>2055</th>
      <td>Norovirus</td>
      <td>15unuh</td>
      <td>all</td>
      <td>1.357195e+09</td>
      <td>Norovirus: the perfect pathogen spreading thro...</td>
      <td>1938</td>
      <td>http://phenomena.nationalgeographic.com/2013/0...</td>
      <td>918</td>
      <td>http://phenomena.nationalgeographic.com/2013/0...</td>
      <td>phenomena.nationalgeographic.com</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>c62o2</td>
      <td>all</td>
      <td>1.274334e+09</td>
      <td>Study finds that 84% of people who think they ...</td>
      <td>835</td>
      <td>http://www.aolhealth.com/condition-center/alle...</td>
      <td>915</td>
      <td>http://www.aolhealth.com/condition-center/alle...</td>
      <td>aolhealth.com</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>4b77wa</td>
      <td>all</td>
      <td>1.458503e+09</td>
      <td>Food Allergy transferred to patient following ...</td>
      <td>25912</td>
      <td>http://www.ncbi.nlm.nih.gov/pubmed/26990607</td>
      <td>884</td>
      <td>http://www.ncbi.nlm.nih.gov/pubmed/26990607</td>
      <td>ncbi.nlm.nih.gov</td>
    </tr>
    <tr>
      <th>485</th>
      <td>food poisoning</td>
      <td>4135sq</td>
      <td>all</td>
      <td>1.452895e+09</td>
      <td>Chipotle to close all restaurants for company-...</td>
      <td>2155</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>797</td>
      <td>http://www.foxnews.com/leisure/2016/01/15/chip...</td>
      <td>foxnews.com</td>
    </tr>
    <tr>
      <th>1171</th>
      <td>e. coli</td>
      <td>f48f3</td>
      <td>all</td>
      <td>1.295354e+09</td>
      <td>If it's real, it changes everything- Biotech c...</td>
      <td>1053</td>
      <td>http://www.theglobeandmail.com/news/opinions/o...</td>
      <td>782</td>
      <td>http://www.theglobeandmail.com/news/opinions/o...</td>
      <td>theglobeandmail.com</td>
    </tr>
    <tr>
      <th>1159</th>
      <td>e. coli</td>
      <td>170vil</td>
      <td>all</td>
      <td>1.358845e+09</td>
      <td>Louisiana senator asks if E. coli evolve into ...</td>
      <td>2117</td>
      <td>http://blogs.scientificamerican.com/the-curiou...</td>
      <td>777</td>
      <td>http://blogs.scientificamerican.com/the-curiou...</td>
      <td>blogs.scientificamerican.com</td>
    </tr>
    <tr>
      <th>1598</th>
      <td>salmonella</td>
      <td>5unxqy</td>
      <td>all</td>
      <td>1.487387e+09</td>
      <td>Collapse of Aztec society linked to catastroph...</td>
      <td>16935</td>
      <td>http://www.nature.com/news/collapse-of-aztec-s...</td>
      <td>773</td>
      <td>http://www.nature.com/news/collapse-of-aztec-s...</td>
      <td>nature.com</td>
    </tr>
    <tr>
      <th>2056</th>
      <td>Norovirus</td>
      <td>1omy0l</td>
      <td>all</td>
      <td>1.382037e+09</td>
      <td>Researchers have discovered that copper and co...</td>
      <td>2777</td>
      <td>http://www.sci-news.com/medicine/science-coppe...</td>
      <td>739</td>
      <td>http://www.sci-news.com/medicine/science-coppe...</td>
      <td>sci-news.com</td>
    </tr>
    <tr>
      <th>1147</th>
      <td>e. coli</td>
      <td>7uhxit</td>
      <td>all</td>
      <td>1.517511e+09</td>
      <td>TIL that Hitler's doctor, Theodor Morell, kept...</td>
      <td>7470</td>
      <td>https://en.wikipedia.org/wiki/Theodor_Morell</td>
      <td>725</td>
      <td>https://en.wikipedia.org/wiki/Theodor_Morell</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>1153</th>
      <td>e. coli</td>
      <td>2spgek</td>
      <td>all</td>
      <td>1.421499e+09</td>
      <td>TIL that Johnny Depp's daughter nearly died fr...</td>
      <td>17524</td>
      <td>https://en.wikipedia.org/wiki/Johnny_Depp#Fami...</td>
      <td>637</td>
      <td>https://en.wikipedia.org/wiki/Johnny_Depp#Fami...</td>
      <td>en.wikipedia.org</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>15ylkv</td>
      <td>all</td>
      <td>1.357352e+09</td>
      <td>There was a kid at camp who could eat only fru...</td>
      <td>1988</td>
      <td>http://i.imgur.com/CXiZc.jpg</td>
      <td>631</td>
      <td>http://i.imgur.com/CXiZc.jpg</td>
      <td>i.imgur.com</td>
    </tr>
    <tr>
      <th>1597</th>
      <td>salmonella</td>
      <td>5nmvzi</td>
      <td>all</td>
      <td>1.484293e+09</td>
      <td>Scientists just trained genetically modified s...</td>
      <td>14905</td>
      <td>http://www.digitaltrends.com/cool-tech/food-po...</td>
      <td>623</td>
      <td>http://www.digitaltrends.com/cool-tech/food-po...</td>
      <td>digitaltrends.com</td>
    </tr>
    <tr>
      <th>1152</th>
      <td>e. coli</td>
      <td>3noutg</td>
      <td>all</td>
      <td>1.444156e+09</td>
      <td>TIL that Johnny Depp's daughter nearly died fr...</td>
      <td>16375</td>
      <td>https://en.wikipedia.org/wiki/Johnny_Depp#Fami...</td>
      <td>580</td>
      <td>https://en.wikipedia.org/wiki/Johnny_Depp#Fami...</td>
      <td>en.wikipedia.org</td>
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
      <th>1123</th>
      <td>foodborne illness</td>
      <td>86e60p</td>
      <td>all</td>
      <td>1.521775e+09</td>
      <td>Chipotle wins dismissal of investor lawsuit ov...</td>
      <td>1</td>
      <td>https://www.reuters.com/article/us-chipotle-la...</td>
      <td>0</td>
      <td>https://www.reuters.com/article/us-chipotle-la...</td>
      <td>reuters.com</td>
    </tr>
    <tr>
      <th>1124</th>
      <td>foodborne illness</td>
      <td>lgx2f</td>
      <td>all</td>
      <td>1.319014e+09</td>
      <td>Twenty-five deaths in 12 states are now linked...</td>
      <td>1</td>
      <td>http://www.wsoctv.com/politics/29523265/detail...</td>
      <td>0</td>
      <td>http://www.wsoctv.com/politics/29523265/detail...</td>
      <td>wsoctv.com</td>
    </tr>
    <tr>
      <th>1125</th>
      <td>foodborne illness</td>
      <td>3cpucc</td>
      <td>all</td>
      <td>1.436503e+09</td>
      <td>[#16|+2926|524] TIL that after San Francisco's...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>0</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>1126</th>
      <td>foodborne illness</td>
      <td>7cqf63</td>
      <td>all</td>
      <td>1.510637e+09</td>
      <td>This Company Is Using Bitcoin's Tech To Preven...</td>
      <td>1</td>
      <td>https://www.youtube.com/watch?v=bux7rKTh98k</td>
      <td>0</td>
      <td>https://www.youtube.com/watch?v=bux7rKTh98k</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>1127</th>
      <td>foodborne illness</td>
      <td>5x7naf</td>
      <td>all</td>
      <td>1.488536e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>1</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>0</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
    </tr>
    <tr>
      <th>1128</th>
      <td>foodborne illness</td>
      <td>30069d</td>
      <td>all</td>
      <td>1.427142e+09</td>
      <td>Health Tip: Cancer Treatment Makes Foodborne I...</td>
      <td>1</td>
      <td>http://www.drugs.com/news/health-tip-cancer-ma...</td>
      <td>0</td>
      <td>http://www.drugs.com/news/health-tip-cancer-ma...</td>
      <td>drugs.com</td>
    </tr>
    <tr>
      <th>1129</th>
      <td>foodborne illness</td>
      <td>53swld</td>
      <td>all</td>
      <td>1.474490e+09</td>
      <td>Speedy bacteria detector could help prevent fo...</td>
      <td>1</td>
      <td>http://phys.org/news/2016-09-speedy-bacteria-d...</td>
      <td>0</td>
      <td>http://phys.org/news/2016-09-speedy-bacteria-d...</td>
      <td>phys.org</td>
    </tr>
    <tr>
      <th>1130</th>
      <td>foodborne illness</td>
      <td>86ehva</td>
      <td>all</td>
      <td>1.521777e+09</td>
      <td>[Health] - Chipotle wins dismissal of investor...</td>
      <td>1</td>
      <td>https://www.reuters.com/article/us-chipotle-la...</td>
      <td>0</td>
      <td>https://www.reuters.com/article/us-chipotle-la...</td>
      <td>reuters.com</td>
    </tr>
    <tr>
      <th>2249</th>
      <td>Norovirus</td>
      <td>4dswkr</td>
      <td>all</td>
      <td>1.460089e+09</td>
      <td>28 University of Minnesota students ill, norov...</td>
      <td>22</td>
      <td>http://www.fox9.com/news/118591735-story</td>
      <td>0</td>
      <td>http://www.fox9.com/news/118591735-story</td>
      <td>fox9.com</td>
    </tr>
    <tr>
      <th>1131</th>
      <td>foodborne illness</td>
      <td>1czscc</td>
      <td>all</td>
      <td>1.366811e+09</td>
      <td>Foodborne Illnesses</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=dM4S6i98HAQ&amp;fea...</td>
      <td>0</td>
      <td>http://www.youtube.com/watch?v=dM4S6i98HAQ&amp;fea...</td>
      <td>youtube.com</td>
    </tr>
    <tr>
      <th>1132</th>
      <td>foodborne illness</td>
      <td>793g5q</td>
      <td>all</td>
      <td>1.509142e+09</td>
      <td>@NPR: Poultry industry critics warn that highe...</td>
      <td>1</td>
      <td>https://twitter.com/NPR/status/923912923918999553</td>
      <td>0</td>
      <td>https://twitter.com/NPR/status/923912923918999553</td>
      <td>twitter.com</td>
    </tr>
    <tr>
      <th>1118</th>
      <td>foodborne illness</td>
      <td>2guy3l</td>
      <td>all</td>
      <td>1.411162e+09</td>
      <td>FDA releases updated proposals to improve food...</td>
      <td>1</td>
      <td>http://www.fda.gov/NewsEvents/Newsroom/PressAn...</td>
      <td>0</td>
      <td>http://www.fda.gov/NewsEvents/Newsroom/PressAn...</td>
      <td>fda.gov</td>
    </tr>
    <tr>
      <th>1116</th>
      <td>foodborne illness</td>
      <td>7a8eio</td>
      <td>all</td>
      <td>1.509616e+09</td>
      <td>This company is using bitcoin’s tech to preven...</td>
      <td>1</td>
      <td>https://news.vice.com/story/this-company-is-us...</td>
      <td>0</td>
      <td>https://news.vice.com/story/this-company-is-us...</td>
      <td>news.vice.com</td>
    </tr>
    <tr>
      <th>1115</th>
      <td>foodborne illness</td>
      <td>endow</td>
      <td>all</td>
      <td>1.292619e+09</td>
      <td>Swine Flu Kills 10 in Britain; Foodborne Illne...</td>
      <td>1</td>
      <td>http://www.diogenec.com/blog/bid/33320/Swine-F...</td>
      <td>0</td>
      <td>http://www.diogenec.com/blog/bid/33320/Swine-F...</td>
      <td>diogenec.com</td>
    </tr>
    <tr>
      <th>2290</th>
      <td>Norovirus</td>
      <td>1hrouf</td>
      <td>all</td>
      <td>1.373175e+09</td>
      <td>Health officials confirm norovirus at 'Tough M...</td>
      <td>17</td>
      <td>http://www.michiganradio.org/post/health-offic...</td>
      <td>0</td>
      <td>http://www.michiganradio.org/post/health-offic...</td>
      <td>michiganradio.org</td>
    </tr>
    <tr>
      <th>1103</th>
      <td>foodborne illness</td>
      <td>5zkgy7</td>
      <td>all</td>
      <td>1.489625e+09</td>
      <td>(洋葱) Report: Saying ‘Smells Okay’ Precedes 85%...</td>
      <td>1</td>
      <td>http://www.theonion.com/article/report-saying-...</td>
      <td>0</td>
      <td>http://www.theonion.com/article/report-saying-...</td>
      <td>theonion.com</td>
    </tr>
    <tr>
      <th>1104</th>
      <td>foodborne illness</td>
      <td>413sph</td>
      <td>all</td>
      <td>1.452904e+09</td>
      <td>Chipotle's supply chain called into question a...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/news/comments/40zzl4/...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/news/comments/40zzl4/...</td>
      <td>reddit.com</td>
    </tr>
    <tr>
      <th>2302</th>
      <td>Norovirus</td>
      <td>3bmcrd</td>
      <td>all</td>
      <td>1.435692e+09</td>
      <td>1,000 runners get norovirus after French mud run</td>
      <td>16</td>
      <td>http://www.upi.com/Odd_News/2015/06/29/1000-pe...</td>
      <td>0</td>
      <td>http://www.upi.com/Odd_News/2015/06/29/1000-pe...</td>
      <td>upi.com</td>
    </tr>
    <tr>
      <th>1105</th>
      <td>foodborne illness</td>
      <td>86ek6s</td>
      <td>all</td>
      <td>1.521778e+09</td>
      <td>@Reuters: Chipotle wins dismissal of investor ...</td>
      <td>1</td>
      <td>https://twitter.com/Reuters/status/97691148199...</td>
      <td>0</td>
      <td>https://twitter.com/Reuters/status/97691148199...</td>
      <td>twitter.com</td>
    </tr>
    <tr>
      <th>1106</th>
      <td>foodborne illness</td>
      <td>hunzr</td>
      <td>all</td>
      <td>1.307575e+09</td>
      <td>Mixed Results On Foodborne Illness Cast Shadow...</td>
      <td>1</td>
      <td>http://www.npr.org/blogs/health/2011/06/08/137...</td>
      <td>0</td>
      <td>http://www.npr.org/blogs/health/2011/06/08/137...</td>
      <td>npr.org</td>
    </tr>
    <tr>
      <th>2292</th>
      <td>Norovirus</td>
      <td>4gpl50</td>
      <td>all</td>
      <td>1.461807e+09</td>
      <td>New study estimates that norovirus costs the w...</td>
      <td>17</td>
      <td>http://blogs.plos.org/collections/whats-norovi...</td>
      <td>0</td>
      <td>http://blogs.plos.org/collections/whats-norovi...</td>
      <td>blogs.plos.org</td>
    </tr>
    <tr>
      <th>1107</th>
      <td>foodborne illness</td>
      <td>42cd2t</td>
      <td>all</td>
      <td>1.453607e+09</td>
      <td>-By Dr. Mercola Factory farming methods may be...</td>
      <td>1</td>
      <td>http://naturalpresswire.com/conventional-groun...</td>
      <td>0</td>
      <td>http://naturalpresswire.com/conventional-groun...</td>
      <td>naturalpresswire.com</td>
    </tr>
    <tr>
      <th>1113</th>
      <td>foodborne illness</td>
      <td>6fdbf</td>
      <td>all</td>
      <td>1.207911e+09</td>
      <td>Foodborne Illnesses Remain Constant in U.S.</td>
      <td>1</td>
      <td>http://www.washingtonpost.com/wp-dyn/content/a...</td>
      <td>0</td>
      <td>http://www.washingtonpost.com/wp-dyn/content/a...</td>
      <td>washingtonpost.com</td>
    </tr>
    <tr>
      <th>1108</th>
      <td>foodborne illness</td>
      <td>429anz</td>
      <td>all</td>
      <td>1.453551e+09</td>
      <td>Chipotle Tried To Cover Up Foodborne Illness O...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/autotldr/comments/429...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/autotldr/comments/429...</td>
      <td>self.autotldr</td>
    </tr>
    <tr>
      <th>1109</th>
      <td>foodborne illness</td>
      <td>2h85hv</td>
      <td>all</td>
      <td>1.411507e+09</td>
      <td>FDA food safety challenge to spur new technolo...</td>
      <td>1</td>
      <td>http://www.fda.gov/NewsEvents/Newsroom/PressAn...</td>
      <td>0</td>
      <td>http://www.fda.gov/NewsEvents/Newsroom/PressAn...</td>
      <td>fda.gov</td>
    </tr>
    <tr>
      <th>1110</th>
      <td>foodborne illness</td>
      <td>6o1mer</td>
      <td>all</td>
      <td>1.500422e+09</td>
      <td>[Business] - A Chipotle restaurant is closed a...</td>
      <td>1</td>
      <td>https://www.washingtonpost.com/news/wonk/wp/20...</td>
      <td>0</td>
      <td>https://www.washingtonpost.com/news/wonk/wp/20...</td>
      <td>washingtonpost.com</td>
    </tr>
    <tr>
      <th>1111</th>
      <td>foodborne illness</td>
      <td>86e45z</td>
      <td>all</td>
      <td>1.521774e+09</td>
      <td>OANN: Chipotle wins dismissal of investor laws...</td>
      <td>1</td>
      <td>http://www.oann.com/chipotle-wins-dismissal-of...</td>
      <td>0</td>
      <td>http://www.oann.com/chipotle-wins-dismissal-of...</td>
      <td>oann.com</td>
    </tr>
    <tr>
      <th>1112</th>
      <td>foodborne illness</td>
      <td>86e5t9</td>
      <td>all</td>
      <td>1.521775e+09</td>
      <td>[Business] - Chipotle wins dismissal of invest...</td>
      <td>1</td>
      <td>https://www.reuters.com/article/us-chipotle-la...</td>
      <td>0</td>
      <td>https://www.reuters.com/article/us-chipotle-la...</td>
      <td>reuters.com</td>
    </tr>
    <tr>
      <th>2279</th>
      <td>Norovirus</td>
      <td>1h26vs</td>
      <td>all</td>
      <td>1.372221e+09</td>
      <td>Yellowstone, Grand Teton park visitors warned ...</td>
      <td>20</td>
      <td>http://www.cnn.com/2013/06/19/travel/wyoming-p...</td>
      <td>0</td>
      <td>http://www.cnn.com/2013/06/19/travel/wyoming-p...</td>
      <td>cnn.com</td>
    </tr>
    <tr>
      <th>1013</th>
      <td>foodborne illness</td>
      <td>1o0dn7</td>
      <td>all</td>
      <td>1.381293e+09</td>
      <td>There’s a Major Foodborne Illness Outbreak (US...</td>
      <td>6</td>
      <td>http://www.wired.com/wiredscience/2013/10/shut...</td>
      <td>0</td>
      <td>http://www.wired.com/wiredscience/2013/10/shut...</td>
      <td>wired.com</td>
    </tr>
  </tbody>
</table>
<p>2514 rows × 10 columns</p>
</div>




```python
reddit_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2514 entries, 0 to 2513
    Data columns (total 10 columns):
    Keyword                      2514 non-null object
    Submission ID                2514 non-null object
    Subreddit                    2514 non-null object
    Created Date                 2514 non-null float64
    Submission Title             2514 non-null object
    Submission Score             2514 non-null int64
    Submission URL               2514 non-null object
    Total Submission Comments    2514 non-null int64
    Submission URL               2514 non-null object
    Domain                       2514 non-null object
    dtypes: float64(1), int64(2), object(7)
    memory usage: 196.5+ KB



```python
reddit_df["Total Submission Comments"].sum()
```




    111053




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
      <td>I am deathly allergic to peanuts and all nuts ...</td>
      <td>e6dlg</td>
    </tr>
    <tr>
      <th>1</th>
      <td>As a parent of a child with a peanut allergy I...</td>
      <td>e6dlg</td>
    </tr>
    <tr>
      <th>2</th>
      <td>I'm allergic to bees, so if you guys could get...</td>
      <td>e6dlg</td>
    </tr>
    <tr>
      <th>3</th>
      <td>I'm allergic to many different types of food a...</td>
      <td>e6dlg</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alright. I am confident that this will get bur...</td>
      <td>e6dlg</td>
    </tr>
  </tbody>
</table>
</div>




```python
comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 26345 entries, 0 to 26344
    Data columns (total 2 columns):
    Submission Comments    26345 non-null object
    Submission ID          26345 non-null object
    dtypes: object(2)
    memory usage: 411.7+ KB



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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 26926 entries, 0 to 26925
    Data columns (total 11 columns):
    Keyword                      26926 non-null object
    Submission ID                26926 non-null object
    Subreddit                    26926 non-null object
    Created Date                 26926 non-null float64
    Submission Title             26926 non-null object
    Submission Score             26926 non-null int64
    Submission URL               26926 non-null object
    Total Submission Comments    26926 non-null int64
    Submission URL               26926 non-null object
    Domain                       26926 non-null object
    Submission Comments          26707 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 2.5+ MB



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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>First they came for the peanuts, and I was sil...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>THIS IS AMERICA!! How dare someone promote per...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>The real question is:  How many people in this...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I knew a girl in middle school. She couldn't b...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm quietly munching on peanuts as I read this...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>my kid's class banned both nut and egg product...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I've had a "life-threatening peanut allergy" s...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>So precisely what is the argument against bann...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I think these comments perfectly sum up the ar...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Our oldest son is highly allergic to the uncoo...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm deathly allergic to wheat dust, but I have...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>No kidding.  I had no idea people were even su...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Unfortunately we've already determined as a po...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>peanuts and peanut butter are kind of a staple...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>My little brother is deadly allergic to peanut...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am inclined to agree with the responsibility...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm highly allergic to peanuts, but it's ridic...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Peanut allergies kill more people than terrori...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I know this is going to turn into a lot of per...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>4-6 percent of kids dictate how things go for ...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>How about a ´allergic people´-free zone!?\n</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>If your or your child is so allergic that mere...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>For the record: I live in Germany and have NEV...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bullshit so TVs in businesses ...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>here is what i want to know...where are all th...</td>
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
      <th>26896</th>
      <td>Norovirus</td>
      <td>2sh27m</td>
      <td>all</td>
      <td>1.421318e+09</td>
      <td>New evidence in mice suggests antibiotics may ...</td>
      <td>3</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>1</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>sciguru.org</td>
      <td>So the virus uses bacteria in order to remain ...</td>
    </tr>
    <tr>
      <th>26897</th>
      <td>Norovirus</td>
      <td>4h0h2g</td>
      <td>all</td>
      <td>1.461980e+09</td>
      <td>Norovirus outbreak aboard cruise ship docked i...</td>
      <td>6</td>
      <td>http://pilotonline.com/news/local/health/norov...</td>
      <td>0</td>
      <td>http://pilotonline.com/news/local/health/norov...</td>
      <td>pilotonline.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26898</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Soap! Wear gloves and clean all surfaces that ...</td>
    </tr>
    <tr>
      <th>26899</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Norovirus is simply a viral GI "bug". It's not...</td>
    </tr>
    <tr>
      <th>26900</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Use a 5-10% bleach solution to clean hard surf...</td>
    </tr>
    <tr>
      <th>26901</th>
      <td>Norovirus</td>
      <td>20c91p</td>
      <td>all</td>
      <td>1.394767e+09</td>
      <td>Four residents of state VA nursing home in Min...</td>
      <td>6</td>
      <td>http://www.startribune.com/local/south/2502089...</td>
      <td>0</td>
      <td>http://www.startribune.com/local/south/2502089...</td>
      <td>startribune.com</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26902</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Norovirus is extraordinarily easy to spread an...</td>
    </tr>
    <tr>
      <th>26903</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>You don't have to ingest food to contract noro...</td>
    </tr>
    <tr>
      <th>26904</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Yikes, no fun, though you don't necessarily ha...</td>
    </tr>
    <tr>
      <th>26905</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Contact the city's health department.</td>
    </tr>
    <tr>
      <th>26906</th>
      <td>Norovirus</td>
      <td>15w8xm</td>
      <td>all</td>
      <td>1.357261e+09</td>
      <td>Can people be immune/resistant to norovirus an...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>self.askscience</td>
      <td>With regards to your comment on "higher stomac...</td>
    </tr>
    <tr>
      <th>26907</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Gah, I hate when people think lying will help ...</td>
    </tr>
    <tr>
      <th>26908</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Also like to add, no crazy lovey dovey kissing...</td>
    </tr>
    <tr>
      <th>26909</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Now Monday, still nothing. I'm getting more co...</td>
    </tr>
    <tr>
      <th>26910</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>So I didn't catch it during the week. I hung o...</td>
    </tr>
    <tr>
      <th>26911</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>Down water, take vocal breaks, and just rest a...</td>
    </tr>
    <tr>
      <th>26912</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>I would say rest it as much as possible. If wo...</td>
    </tr>
    <tr>
      <th>26913</th>
      <td>Norovirus</td>
      <td>6wktp0</td>
      <td>all</td>
      <td>1.503969e+09</td>
      <td>Norovirus :(</td>
      <td>2</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>self.AskDocs</td>
      <td>It usually runs its course, its does generally...</td>
    </tr>
    <tr>
      <th>26914</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Small sips of water every 10 minutes. See if s...</td>
    </tr>
    <tr>
      <th>26915</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Go to the ER and get an IV.</td>
    </tr>
    <tr>
      <th>26916</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>If you have a primary care physician, you can ...</td>
    </tr>
    <tr>
      <th>26917</th>
      <td>Norovirus</td>
      <td>7w8d8d</td>
      <td>all</td>
      <td>1.518155e+09</td>
      <td>Norovirus at the Olympics</td>
      <td>2</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>self.Jokes</td>
      <td>That stuff is so ugly and spreads so fast. I w...</td>
    </tr>
    <tr>
      <th>26918</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>You could call your doctor to confirm, my unde...</td>
    </tr>
    <tr>
      <th>26919</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Agree with commenter above. And don't share to...</td>
    </tr>
    <tr>
      <th>26920</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>A couple Thanksgivings ago, my sister brought ...</td>
    </tr>
    <tr>
      <th>26921</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I had norovirus when my lo was about 11 months...</td>
    </tr>
    <tr>
      <th>26922</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I never updated here! Thanks so much for all y...</td>
    </tr>
    <tr>
      <th>26923</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Just wanted to give you a head's up! I went th...</td>
    </tr>
    <tr>
      <th>26924</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>I'd be willing to bet that your brother got si...</td>
    </tr>
    <tr>
      <th>26925</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Where are you located? I've seen in emetophobi...</td>
    </tr>
  </tbody>
</table>
<p>26926 rows × 11 columns</p>
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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>First they came for the peanuts, and I was sil...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>THIS IS AMERICA!! How dare someone promote per...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>The real question is:  How many people in this...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I knew a girl in middle school. She couldn't b...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm quietly munching on peanuts as I read this...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>my kid's class banned both nut and egg product...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I've had a "life-threatening peanut allergy" s...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>So precisely what is the argument against bann...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I think these comments perfectly sum up the ar...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Our oldest son is highly allergic to the uncoo...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm deathly allergic to wheat dust, but I have...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>No kidding.  I had no idea people were even su...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Unfortunately we've already determined as a po...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>peanuts and peanut butter are kind of a staple...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>My little brother is deadly allergic to peanut...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am inclined to agree with the responsibility...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm highly allergic to peanuts, but it's ridic...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Peanut allergies kill more people than terrori...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I know this is going to turn into a lot of per...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>4-6 percent of kids dictate how things go for ...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>How about a ´allergic people´-free zone!?\n</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>If your or your child is so allergic that mere...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>For the record: I live in Germany and have NEV...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bullshit so TVs in businesses ...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>here is what i want to know...where are all th...</td>
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
      <th>26891</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>Stay home. We always have noro out breaks in t...</td>
    </tr>
    <tr>
      <th>26892</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>No, you're still contagious, you should not go...</td>
    </tr>
    <tr>
      <th>26896</th>
      <td>Norovirus</td>
      <td>2sh27m</td>
      <td>all</td>
      <td>1.421318e+09</td>
      <td>New evidence in mice suggests antibiotics may ...</td>
      <td>3</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>1</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>sciguru.org</td>
      <td>So the virus uses bacteria in order to remain ...</td>
    </tr>
    <tr>
      <th>26898</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Soap! Wear gloves and clean all surfaces that ...</td>
    </tr>
    <tr>
      <th>26899</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Norovirus is simply a viral GI "bug". It's not...</td>
    </tr>
    <tr>
      <th>26900</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Use a 5-10% bleach solution to clean hard surf...</td>
    </tr>
    <tr>
      <th>26902</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Norovirus is extraordinarily easy to spread an...</td>
    </tr>
    <tr>
      <th>26903</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>You don't have to ingest food to contract noro...</td>
    </tr>
    <tr>
      <th>26904</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Yikes, no fun, though you don't necessarily ha...</td>
    </tr>
    <tr>
      <th>26905</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Contact the city's health department.</td>
    </tr>
    <tr>
      <th>26906</th>
      <td>Norovirus</td>
      <td>15w8xm</td>
      <td>all</td>
      <td>1.357261e+09</td>
      <td>Can people be immune/resistant to norovirus an...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>self.askscience</td>
      <td>With regards to your comment on "higher stomac...</td>
    </tr>
    <tr>
      <th>26907</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Gah, I hate when people think lying will help ...</td>
    </tr>
    <tr>
      <th>26908</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Also like to add, no crazy lovey dovey kissing...</td>
    </tr>
    <tr>
      <th>26909</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Now Monday, still nothing. I'm getting more co...</td>
    </tr>
    <tr>
      <th>26910</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>So I didn't catch it during the week. I hung o...</td>
    </tr>
    <tr>
      <th>26911</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>Down water, take vocal breaks, and just rest a...</td>
    </tr>
    <tr>
      <th>26912</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>I would say rest it as much as possible. If wo...</td>
    </tr>
    <tr>
      <th>26913</th>
      <td>Norovirus</td>
      <td>6wktp0</td>
      <td>all</td>
      <td>1.503969e+09</td>
      <td>Norovirus :(</td>
      <td>2</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>self.AskDocs</td>
      <td>It usually runs its course, its does generally...</td>
    </tr>
    <tr>
      <th>26914</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Small sips of water every 10 minutes. See if s...</td>
    </tr>
    <tr>
      <th>26915</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Go to the ER and get an IV.</td>
    </tr>
    <tr>
      <th>26916</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>If you have a primary care physician, you can ...</td>
    </tr>
    <tr>
      <th>26917</th>
      <td>Norovirus</td>
      <td>7w8d8d</td>
      <td>all</td>
      <td>1.518155e+09</td>
      <td>Norovirus at the Olympics</td>
      <td>2</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>self.Jokes</td>
      <td>That stuff is so ugly and spreads so fast. I w...</td>
    </tr>
    <tr>
      <th>26918</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>You could call your doctor to confirm, my unde...</td>
    </tr>
    <tr>
      <th>26919</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Agree with commenter above. And don't share to...</td>
    </tr>
    <tr>
      <th>26920</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>A couple Thanksgivings ago, my sister brought ...</td>
    </tr>
    <tr>
      <th>26921</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I had norovirus when my lo was about 11 months...</td>
    </tr>
    <tr>
      <th>26922</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I never updated here! Thanks so much for all y...</td>
    </tr>
    <tr>
      <th>26923</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Just wanted to give you a head's up! I went th...</td>
    </tr>
    <tr>
      <th>26924</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>I'd be willing to bet that your brother got si...</td>
    </tr>
    <tr>
      <th>26925</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Where are you located? I've seen in emetophobi...</td>
    </tr>
  </tbody>
</table>
<p>25858 rows × 11 columns</p>
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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>First they came for the peanuts, and I was sil...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>THIS IS AMERICA!! How dare someone promote per...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>The real question is:  How many people in this...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I knew a girl in middle school. She couldn't b...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm quietly munching on peanuts as I read this...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>my kid's class banned both nut and egg product...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I've had a "life-threatening peanut allergy" s...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>So precisely what is the argument against bann...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I think these comments perfectly sum up the ar...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Our oldest son is highly allergic to the uncoo...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm deathly allergic to wheat dust, but I have...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>No kidding.  I had no idea people were even su...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Unfortunately we've already determined as a po...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>peanuts and peanut butter are kind of a staple...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>My little brother is deadly allergic to peanut...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am inclined to agree with the responsibility...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm highly allergic to peanuts, but it's ridic...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Peanut allergies kill more people than terrori...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I know this is going to turn into a lot of per...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>4-6 percent of kids dictate how things go for ...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>How about a ´allergic people´-free zone!?\n</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>If your or your child is so allergic that mere...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>For the record: I live in Germany and have NEV...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bullshit so TVs in businesses ...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>here is what i want to know...where are all th...</td>
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
      <th>25828</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>Stay home. We always have noro out breaks in t...</td>
    </tr>
    <tr>
      <th>25829</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>No, you're still contagious, you should not go...</td>
    </tr>
    <tr>
      <th>25830</th>
      <td>Norovirus</td>
      <td>2sh27m</td>
      <td>all</td>
      <td>1.421318e+09</td>
      <td>New evidence in mice suggests antibiotics may ...</td>
      <td>3</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>1</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>sciguru.org</td>
      <td>So the virus uses bacteria in order to remain ...</td>
    </tr>
    <tr>
      <th>25831</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Soap! Wear gloves and clean all surfaces that ...</td>
    </tr>
    <tr>
      <th>25832</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Norovirus is simply a viral GI "bug". It's not...</td>
    </tr>
    <tr>
      <th>25833</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Use a 5-10% bleach solution to clean hard surf...</td>
    </tr>
    <tr>
      <th>25834</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Norovirus is extraordinarily easy to spread an...</td>
    </tr>
    <tr>
      <th>25835</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>You don't have to ingest food to contract noro...</td>
    </tr>
    <tr>
      <th>25836</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Yikes, no fun, though you don't necessarily ha...</td>
    </tr>
    <tr>
      <th>25837</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Contact the city's health department.</td>
    </tr>
    <tr>
      <th>25838</th>
      <td>Norovirus</td>
      <td>15w8xm</td>
      <td>all</td>
      <td>1.357261e+09</td>
      <td>Can people be immune/resistant to norovirus an...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>self.askscience</td>
      <td>With regards to your comment on "higher stomac...</td>
    </tr>
    <tr>
      <th>25839</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Gah, I hate when people think lying will help ...</td>
    </tr>
    <tr>
      <th>25840</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Also like to add, no crazy lovey dovey kissing...</td>
    </tr>
    <tr>
      <th>25841</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Now Monday, still nothing. I'm getting more co...</td>
    </tr>
    <tr>
      <th>25842</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>So I didn't catch it during the week. I hung o...</td>
    </tr>
    <tr>
      <th>25843</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>Down water, take vocal breaks, and just rest a...</td>
    </tr>
    <tr>
      <th>25844</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>I would say rest it as much as possible. If wo...</td>
    </tr>
    <tr>
      <th>25845</th>
      <td>Norovirus</td>
      <td>6wktp0</td>
      <td>all</td>
      <td>1.503969e+09</td>
      <td>Norovirus :(</td>
      <td>2</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>self.AskDocs</td>
      <td>It usually runs its course, its does generally...</td>
    </tr>
    <tr>
      <th>25846</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Small sips of water every 10 minutes. See if s...</td>
    </tr>
    <tr>
      <th>25847</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Go to the ER and get an IV.</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>If you have a primary care physician, you can ...</td>
    </tr>
    <tr>
      <th>25849</th>
      <td>Norovirus</td>
      <td>7w8d8d</td>
      <td>all</td>
      <td>1.518155e+09</td>
      <td>Norovirus at the Olympics</td>
      <td>2</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>self.Jokes</td>
      <td>That stuff is so ugly and spreads so fast. I w...</td>
    </tr>
    <tr>
      <th>25850</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>You could call your doctor to confirm, my unde...</td>
    </tr>
    <tr>
      <th>25851</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Agree with commenter above. And don't share to...</td>
    </tr>
    <tr>
      <th>25852</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>A couple Thanksgivings ago, my sister brought ...</td>
    </tr>
    <tr>
      <th>25853</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I had norovirus when my lo was about 11 months...</td>
    </tr>
    <tr>
      <th>25854</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I never updated here! Thanks so much for all y...</td>
    </tr>
    <tr>
      <th>25855</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Just wanted to give you a head's up! I went th...</td>
    </tr>
    <tr>
      <th>25856</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>I'd be willing to bet that your brother got si...</td>
    </tr>
    <tr>
      <th>25857</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Where are you located? I've seen in emetophobi...</td>
    </tr>
  </tbody>
</table>
<p>25858 rows × 11 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 25858 entries, 0 to 25857
    Data columns (total 11 columns):
    Keyword                      25858 non-null object
    Submission ID                25858 non-null object
    Subreddit                    25858 non-null object
    Created Date                 25858 non-null float64
    Submission Title             25858 non-null object
    Submission Score             25858 non-null int64
    Submission URL               25858 non-null object
    Total Submission Comments    25858 non-null int64
    Submission URL               25858 non-null object
    Domain                       25858 non-null object
    Submission Comments          25858 non-null object
    dtypes: float64(1), int64(2), object(8)
    memory usage: 2.2+ MB



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
reddit_comments_df['Keyword'].value_counts()
```




    food poisoning       7259
    e. coli              5991
    food allergy         5512
    salmonella           4042
    Norovirus            2546
    foodborne illness     508
    Name: Keyword, dtype: int64




```python
grouped_df = reddit_comments_df.groupby('Keyword')['Compound Score'].mean()
```


```python
grouped_df = pd.DataFrame(grouped_df)
grouped_df = grouped_df.reset_index()
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
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Norovirus</td>
      <td>-0.054806</td>
    </tr>
    <tr>
      <th>1</th>
      <td>e. coli</td>
      <td>0.056243</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>0.032503</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food poisoning</td>
      <td>-0.087096</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foodborne illness</td>
      <td>-0.077426</td>
    </tr>
    <tr>
      <th>5</th>
      <td>salmonella</td>
      <td>-0.016816</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set()
ax = sns.barplot(x='Keyword', y='Compound Score', data=grouped_df, ci=None)

ttl = ax.title
ttl.set_position([0.5, 1.05])

plt.title("Overall Sentiments for Foodborne Illness Keywords on Reddit (%s) %s" % (time.strftime("%x"), ""))
plt.ylabel("Sentiment Polarity")
plt.xlabel("Keywords")

plt.ylim(-0.15, 0.15)

for item in ax.get_xticklabels():
    item.set_rotation(15)

#get labels for bars
for p in ax.patches:
    height = p.get_height()
    ax.text(p.get_x()+p.get_width()/2.,
            1.05*height,
                '{:1.2f}'.format(height),
            ha="center") 

plt.savefig("Foodborne_Sentiment_Overall.png", dpi=350)
plt.show()
```


![png](output_24_0.png)



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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
      <td>-0.7717</td>
      <td>0.037</td>
      <td>0.151</td>
      <td>0.812</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
      <td>0.7391</td>
      <td>0.150</td>
      <td>0.000</td>
      <td>0.850</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.136</td>
      <td>0.864</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
      <td>-0.8625</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
      <td>-0.9365</td>
      <td>0.078</td>
      <td>0.109</td>
      <td>0.813</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>First they came for the peanuts, and I was sil...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>THIS IS AMERICA!! How dare someone promote per...</td>
      <td>0.5386</td>
      <td>0.303</td>
      <td>0.000</td>
      <td>0.697</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>The real question is:  How many people in this...</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.185</td>
      <td>0.815</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I knew a girl in middle school. She couldn't b...</td>
      <td>-0.0108</td>
      <td>0.074</td>
      <td>0.066</td>
      <td>0.859</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm quietly munching on peanuts as I read this...</td>
      <td>0.2975</td>
      <td>0.136</td>
      <td>0.000</td>
      <td>0.864</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>my kid's class banned both nut and egg product...</td>
      <td>-0.8357</td>
      <td>0.049</td>
      <td>0.228</td>
      <td>0.723</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I've had a "life-threatening peanut allergy" s...</td>
      <td>-0.5286</td>
      <td>0.084</td>
      <td>0.085</td>
      <td>0.831</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>So precisely what is the argument against bann...</td>
      <td>0.4660</td>
      <td>0.097</td>
      <td>0.044</td>
      <td>0.859</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I think these comments perfectly sum up the ar...</td>
      <td>0.4615</td>
      <td>0.062</td>
      <td>0.062</td>
      <td>0.876</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Our oldest son is highly allergic to the uncoo...</td>
      <td>0.5273</td>
      <td>0.089</td>
      <td>0.048</td>
      <td>0.863</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm deathly allergic to wheat dust, but I have...</td>
      <td>-0.1531</td>
      <td>0.000</td>
      <td>0.065</td>
      <td>0.935</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>No kidding.  I had no idea people were even su...</td>
      <td>-0.7717</td>
      <td>0.051</td>
      <td>0.331</td>
      <td>0.618</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Unfortunately we've already determined as a po...</td>
      <td>-0.9517</td>
      <td>0.053</td>
      <td>0.225</td>
      <td>0.722</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>peanuts and peanut butter are kind of a staple...</td>
      <td>-0.2732</td>
      <td>0.040</td>
      <td>0.081</td>
      <td>0.879</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>My little brother is deadly allergic to peanut...</td>
      <td>-0.9784</td>
      <td>0.029</td>
      <td>0.129</td>
      <td>0.842</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am inclined to agree with the responsibility...</td>
      <td>-0.0258</td>
      <td>0.054</td>
      <td>0.078</td>
      <td>0.868</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm highly allergic to peanuts, but it's ridic...</td>
      <td>-0.8764</td>
      <td>0.033</td>
      <td>0.184</td>
      <td>0.783</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Peanut allergies kill more people than terrori...</td>
      <td>-0.8948</td>
      <td>0.000</td>
      <td>0.574</td>
      <td>0.426</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I know this is going to turn into a lot of per...</td>
      <td>-0.4871</td>
      <td>0.078</td>
      <td>0.099</td>
      <td>0.823</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>4-6 percent of kids dictate how things go for ...</td>
      <td>-0.9765</td>
      <td>0.104</td>
      <td>0.253</td>
      <td>0.643</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>How about a ´allergic people´-free zone!?\n</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>If your or your child is so allergic that mere...</td>
      <td>-0.4882</td>
      <td>0.123</td>
      <td>0.172</td>
      <td>0.705</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>For the record: I live in Germany and have NEV...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.099</td>
      <td>0.901</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bullshit so TVs in businesses ...</td>
      <td>-0.7184</td>
      <td>0.000</td>
      <td>0.300</td>
      <td>0.700</td>
      <td>2010-11-15 22:14:37</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>here is what i want to know...where are all th...</td>
      <td>-0.6597</td>
      <td>0.051</td>
      <td>0.113</td>
      <td>0.835</td>
      <td>2010-11-15 22:14:37</td>
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
      <th>25828</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>Stay home. We always have noro out breaks in t...</td>
      <td>-0.7264</td>
      <td>0.000</td>
      <td>0.132</td>
      <td>0.868</td>
      <td>2016-01-07 13:12:25</td>
    </tr>
    <tr>
      <th>25829</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>No, you're still contagious, you should not go...</td>
      <td>-0.7717</td>
      <td>0.000</td>
      <td>0.372</td>
      <td>0.628</td>
      <td>2016-01-07 13:12:25</td>
    </tr>
    <tr>
      <th>25830</th>
      <td>Norovirus</td>
      <td>2sh27m</td>
      <td>all</td>
      <td>1.421318e+09</td>
      <td>New evidence in mice suggests antibiotics may ...</td>
      <td>3</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>1</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>sciguru.org</td>
      <td>So the virus uses bacteria in order to remain ...</td>
      <td>-0.8176</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
      <td>2015-01-15 10:37:16</td>
    </tr>
    <tr>
      <th>25831</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Soap! Wear gloves and clean all surfaces that ...</td>
      <td>0.5659</td>
      <td>0.182</td>
      <td>0.000</td>
      <td>0.818</td>
      <td>2016-12-20 01:21:13</td>
    </tr>
    <tr>
      <th>25832</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Norovirus is simply a viral GI "bug". It's not...</td>
      <td>0.6222</td>
      <td>0.178</td>
      <td>0.149</td>
      <td>0.674</td>
      <td>2016-12-20 01:21:13</td>
    </tr>
    <tr>
      <th>25833</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Use a 5-10% bleach solution to clean hard surf...</td>
      <td>0.5574</td>
      <td>0.214</td>
      <td>0.060</td>
      <td>0.726</td>
      <td>2016-12-20 01:21:13</td>
    </tr>
    <tr>
      <th>25834</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Norovirus is extraordinarily easy to spread an...</td>
      <td>0.8685</td>
      <td>0.116</td>
      <td>0.071</td>
      <td>0.813</td>
      <td>2016-01-19 15:44:57</td>
    </tr>
    <tr>
      <th>25835</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>You don't have to ingest food to contract noro...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-01-19 15:44:57</td>
    </tr>
    <tr>
      <th>25836</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Yikes, no fun, though you don't necessarily ha...</td>
      <td>0.8016</td>
      <td>0.288</td>
      <td>0.068</td>
      <td>0.644</td>
      <td>2016-01-19 15:44:57</td>
    </tr>
    <tr>
      <th>25837</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Contact the city's health department.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2016-01-19 15:44:57</td>
    </tr>
    <tr>
      <th>25838</th>
      <td>Norovirus</td>
      <td>15w8xm</td>
      <td>all</td>
      <td>1.357261e+09</td>
      <td>Can people be immune/resistant to norovirus an...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>self.askscience</td>
      <td>With regards to your comment on "higher stomac...</td>
      <td>0.4056</td>
      <td>0.053</td>
      <td>0.058</td>
      <td>0.889</td>
      <td>2013-01-04 01:04:05</td>
    </tr>
    <tr>
      <th>25839</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Gah, I hate when people think lying will help ...</td>
      <td>-0.7806</td>
      <td>0.143</td>
      <td>0.318</td>
      <td>0.539</td>
      <td>2017-01-29 10:50:23</td>
    </tr>
    <tr>
      <th>25840</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Also like to add, no crazy lovey dovey kissing...</td>
      <td>0.8268</td>
      <td>0.398</td>
      <td>0.149</td>
      <td>0.453</td>
      <td>2017-01-29 10:50:23</td>
    </tr>
    <tr>
      <th>25841</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Now Monday, still nothing. I'm getting more co...</td>
      <td>0.6361</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
      <td>2017-01-29 10:50:23</td>
    </tr>
    <tr>
      <th>25842</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>So I didn't catch it during the week. I hung o...</td>
      <td>0.1007</td>
      <td>0.070</td>
      <td>0.057</td>
      <td>0.873</td>
      <td>2017-01-29 10:50:23</td>
    </tr>
    <tr>
      <th>25843</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>Down water, take vocal breaks, and just rest a...</td>
      <td>0.9273</td>
      <td>0.179</td>
      <td>0.016</td>
      <td>0.805</td>
      <td>2017-01-03 12:01:55</td>
    </tr>
    <tr>
      <th>25844</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>I would say rest it as much as possible. If wo...</td>
      <td>0.9690</td>
      <td>0.158</td>
      <td>0.021</td>
      <td>0.821</td>
      <td>2017-01-03 12:01:55</td>
    </tr>
    <tr>
      <th>25845</th>
      <td>Norovirus</td>
      <td>6wktp0</td>
      <td>all</td>
      <td>1.503969e+09</td>
      <td>Norovirus :(</td>
      <td>2</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>self.AskDocs</td>
      <td>It usually runs its course, its does generally...</td>
      <td>0.7750</td>
      <td>0.140</td>
      <td>0.053</td>
      <td>0.807</td>
      <td>2017-08-29 01:14:45</td>
    </tr>
    <tr>
      <th>25846</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Small sips of water every 10 minutes. See if s...</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.091</td>
      <td>0.909</td>
      <td>2018-01-07 21:30:09</td>
    </tr>
    <tr>
      <th>25847</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Go to the ER and get an IV.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2018-01-07 21:30:09</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>If you have a primary care physician, you can ...</td>
      <td>0.7096</td>
      <td>0.211</td>
      <td>0.000</td>
      <td>0.789</td>
      <td>2018-01-07 21:30:09</td>
    </tr>
    <tr>
      <th>25849</th>
      <td>Norovirus</td>
      <td>7w8d8d</td>
      <td>all</td>
      <td>1.518155e+09</td>
      <td>Norovirus at the Olympics</td>
      <td>2</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>self.Jokes</td>
      <td>That stuff is so ugly and spreads so fast. I w...</td>
      <td>-0.4101</td>
      <td>0.087</td>
      <td>0.148</td>
      <td>0.765</td>
      <td>2018-02-09 05:36:41</td>
    </tr>
    <tr>
      <th>25850</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>You could call your doctor to confirm, my unde...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2018-02-03 06:08:20</td>
    </tr>
    <tr>
      <th>25851</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Agree with commenter above. And don't share to...</td>
      <td>0.1561</td>
      <td>0.162</td>
      <td>0.123</td>
      <td>0.715</td>
      <td>2018-02-03 06:08:20</td>
    </tr>
    <tr>
      <th>25852</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>A couple Thanksgivings ago, my sister brought ...</td>
      <td>-0.8555</td>
      <td>0.000</td>
      <td>0.120</td>
      <td>0.880</td>
      <td>2018-02-03 06:08:20</td>
    </tr>
    <tr>
      <th>25853</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I had norovirus when my lo was about 11 months...</td>
      <td>-0.1018</td>
      <td>0.000</td>
      <td>0.032</td>
      <td>0.968</td>
      <td>2018-02-03 06:08:20</td>
    </tr>
    <tr>
      <th>25854</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I never updated here! Thanks so much for all y...</td>
      <td>-0.4100</td>
      <td>0.119</td>
      <td>0.195</td>
      <td>0.686</td>
      <td>2018-02-03 06:08:20</td>
    </tr>
    <tr>
      <th>25855</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Just wanted to give you a head's up! I went th...</td>
      <td>0.7333</td>
      <td>0.136</td>
      <td>0.045</td>
      <td>0.819</td>
      <td>2018-01-17 13:14:18</td>
    </tr>
    <tr>
      <th>25856</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>I'd be willing to bet that your brother got si...</td>
      <td>-0.9699</td>
      <td>0.083</td>
      <td>0.154</td>
      <td>0.762</td>
      <td>2018-01-17 13:14:18</td>
    </tr>
    <tr>
      <th>25857</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Where are you located? I've seen in emetophobi...</td>
      <td>-0.8909</td>
      <td>0.065</td>
      <td>0.136</td>
      <td>0.799</td>
      <td>2018-01-17 13:14:18</td>
    </tr>
  </tbody>
</table>
<p>25858 rows × 16 columns</p>
</div>




```python
reddit_comments_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 25858 entries, 0 to 25857
    Data columns (total 16 columns):
    Keyword                      25858 non-null object
    Submission ID                25858 non-null object
    Subreddit                    25858 non-null object
    Created Date                 25858 non-null float64
    Submission Title             25858 non-null object
    Submission Score             25858 non-null int64
    Submission URL               25858 non-null object
    Total Submission Comments    25858 non-null int64
    Submission URL               25858 non-null object
    Domain                       25858 non-null object
    Submission Comments          25858 non-null object
    Compound Score               25858 non-null float64
    Positive Score               25858 non-null float64
    Negative Score               25858 non-null float64
    Neutral Score                25858 non-null float64
    Date                         25858 non-null datetime64[ns]
    dtypes: datetime64[ns](1), float64(5), int64(2), object(8)
    memory usage: 3.2+ MB



```python
reddit_comments_df['Date'][0].year
```




    2010




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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
      <td>-0.7717</td>
      <td>0.037</td>
      <td>0.151</td>
      <td>0.812</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
      <td>0.7391</td>
      <td>0.150</td>
      <td>0.000</td>
      <td>0.850</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.136</td>
      <td>0.864</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
      <td>-0.8625</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
      <td>-0.9365</td>
      <td>0.078</td>
      <td>0.109</td>
      <td>0.813</td>
      <td>2010</td>
    </tr>
  </tbody>
</table>
</div>




```python
reddit_comments_df.to_csv("foodborne_kws.csv",
                     encoding="utf-8", index=False)
```


```python
reddit_comments_df['Date'].value_counts()
```




    2017    5419
    2016    4794
    2015    3849
    2013    3468
    2014    2315
    2018    2283
    2012    1403
    2011     960
    2010     763
    2009     410
    2008     123
    2007      57
    2006      14
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
      <th rowspan="5" valign="top">Norovirus</th>
      <th>10mmvt</th>
      <th>1.348883e+09</th>
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
      <th>116vqn</th>
      <th>1.349811e+09</th>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
    </tr>
    <tr>
      <th>13zkix</th>
      <th>1.354213e+09</th>
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
      <th>1423g8</th>
      <th>1.354323e+09</th>
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
      <th>14b56c</th>
      <th>1.354716e+09</th>
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
      <th rowspan="30" valign="top">Norovirus</th>
      <th>10mmvt</th>
      <th>1.348883e+09</th>
      <td>0.285167</td>
    </tr>
    <tr>
      <th>116vqn</th>
      <th>1.349811e+09</th>
      <td>-0.051453</td>
    </tr>
    <tr>
      <th>13zkix</th>
      <th>1.354213e+09</th>
      <td>0.185400</td>
    </tr>
    <tr>
      <th>1423g8</th>
      <th>1.354323e+09</th>
      <td>0.325450</td>
    </tr>
    <tr>
      <th>14b56c</th>
      <th>1.354716e+09</th>
      <td>-0.246650</td>
    </tr>
    <tr>
      <th>14k3lt</th>
      <th>1.355108e+09</th>
      <td>0.724800</td>
    </tr>
    <tr>
      <th>14w69n</th>
      <th>1.355607e+09</th>
      <td>-0.115814</td>
    </tr>
    <tr>
      <th>14xz3d</th>
      <th>1.355701e+09</th>
      <td>0.163783</td>
    </tr>
    <tr>
      <th>15akfv</th>
      <th>1.356236e+09</th>
      <td>0.113333</td>
    </tr>
    <tr>
      <th>15ceaa</th>
      <th>1.356331e+09</th>
      <td>-0.223750</td>
    </tr>
    <tr>
      <th>15dusd</th>
      <th>1.356404e+09</th>
      <td>0.420900</td>
    </tr>
    <tr>
      <th>15gq4u</th>
      <th>1.356549e+09</th>
      <td>-0.379570</td>
    </tr>
    <tr>
      <th>15lqcm</th>
      <th>1.356775e+09</th>
      <td>-0.024555</td>
    </tr>
    <tr>
      <th>15unuh</th>
      <th>1.357195e+09</th>
      <td>-0.278521</td>
    </tr>
    <tr>
      <th>15v28m</th>
      <th>1.357208e+09</th>
      <td>-0.021950</td>
    </tr>
    <tr>
      <th>15vdfw</th>
      <th>1.357218e+09</th>
      <td>0.234260</td>
    </tr>
    <tr>
      <th>15vrv8</th>
      <th>1.357236e+09</th>
      <td>0.807000</td>
    </tr>
    <tr>
      <th>15vuj4</th>
      <th>1.357242e+09</th>
      <td>0.208950</td>
    </tr>
    <tr>
      <th>15w8xm</th>
      <th>1.357261e+09</th>
      <td>0.405600</td>
    </tr>
    <tr>
      <th>15wwsy</th>
      <th>1.357282e+09</th>
      <td>-0.088529</td>
    </tr>
    <tr>
      <th>15xnbj</th>
      <th>1.357305e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>15yvjw</th>
      <th>1.357360e+09</th>
      <td>-0.107771</td>
    </tr>
    <tr>
      <th>1625eg</th>
      <th>1.357507e+09</th>
      <td>0.937400</td>
    </tr>
    <tr>
      <th>164nzp</th>
      <th>1.357610e+09</th>
      <td>-0.164567</td>
    </tr>
    <tr>
      <th>16bfsn</th>
      <th>1.357861e+09</th>
      <td>-0.185918</td>
    </tr>
    <tr>
      <th>16egwy</th>
      <th>1.357969e+09</th>
      <td>-0.312600</td>
    </tr>
    <tr>
      <th>16exiv</th>
      <th>1.357984e+09</th>
      <td>-0.214387</td>
    </tr>
    <tr>
      <th>16w574</th>
      <th>1.358657e+09</th>
      <td>0.377500</td>
    </tr>
    <tr>
      <th>179eml</th>
      <th>1.359160e+09</th>
      <td>-0.081955</td>
    </tr>
    <tr>
      <th>179p4r</th>
      <th>1.359169e+09</th>
      <td>-0.648600</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="30" valign="top">salmonella</th>
      <th>dmpzt</th>
      <th>1.286246e+09</th>
      <td>-0.134664</td>
    </tr>
    <tr>
      <th>e418v</th>
      <th>1.289428e+09</th>
      <td>-0.206150</td>
    </tr>
    <tr>
      <th>eot1t</th>
      <th>1.292889e+09</th>
      <td>-0.119450</td>
    </tr>
    <tr>
      <th>feidq</th>
      <th>1.296773e+09</th>
      <td>-0.122338</td>
    </tr>
    <tr>
      <th>fjtel</th>
      <th>1.297501e+09</th>
      <td>0.012650</td>
    </tr>
    <tr>
      <th>g15tr</th>
      <th>1.299792e+09</th>
      <td>0.198079</td>
    </tr>
    <tr>
      <th>g26ba</th>
      <th>1.299905e+09</th>
      <td>-0.140725</td>
    </tr>
    <tr>
      <th>ja4de</th>
      <th>1.312600e+09</th>
      <td>-0.220820</td>
    </tr>
    <tr>
      <th>jbc34</th>
      <th>1.312721e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>jbr5q</th>
      <th>1.312777e+09</th>
      <td>-0.020311</td>
    </tr>
    <tr>
      <th>jfmy3</th>
      <th>1.313096e+09</th>
      <td>-0.263167</td>
    </tr>
    <tr>
      <th>jgouh</th>
      <th>1.313179e+09</th>
      <td>0.104917</td>
    </tr>
    <tr>
      <th>jjhn1</th>
      <th>1.313455e+09</th>
      <td>-0.142600</td>
    </tr>
    <tr>
      <th>kcj64</th>
      <th>1.315816e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>kg29m</th>
      <th>1.316082e+09</th>
      <td>0.007888</td>
    </tr>
    <tr>
      <th>nf7uc</th>
      <th>1.324077e+09</th>
      <td>-0.000506</td>
    </tr>
    <tr>
      <th>njgug</th>
      <th>1.324386e+09</th>
      <td>-0.023800</td>
    </tr>
    <tr>
      <th>omkos</th>
      <th>1.326969e+09</th>
      <td>-0.000314</td>
    </tr>
    <tr>
      <th>pbszj</th>
      <th>1.328477e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>q86km</th>
      <th>1.330386e+09</th>
      <td>-0.122671</td>
    </tr>
    <tr>
      <th>rt2yp</th>
      <th>1.333586e+09</th>
      <td>-0.006917</td>
    </tr>
    <tr>
      <th>smqgr</th>
      <th>1.335140e+09</th>
      <td>-0.050500</td>
    </tr>
    <tr>
      <th>so8cb</th>
      <th>1.335222e+09</th>
      <td>0.213720</td>
    </tr>
    <tr>
      <th>suuhx</th>
      <th>1.335531e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>swzyk</th>
      <th>1.335664e+09</th>
      <td>-0.382800</td>
    </tr>
    <tr>
      <th>t66m5</th>
      <th>1.336127e+09</th>
      <td>-0.012071</td>
    </tr>
    <tr>
      <th>t6mgy</th>
      <th>1.336153e+09</th>
      <td>0.285900</td>
    </tr>
    <tr>
      <th>w8mlo</th>
      <th>1.341815e+09</th>
      <td>-0.004412</td>
    </tr>
    <tr>
      <th>x19cj</th>
      <th>1.343105e+09</th>
      <td>0.125000</td>
    </tr>
    <tr>
      <th>x4neu</th>
      <th>1.343250e+09</th>
      <td>-0.098680</td>
    </tr>
  </tbody>
</table>
<p>2292 rows × 1 columns</p>
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
      <td>Norovirus</td>
      <td>10mmvt</td>
      <td>1.348883e+09</td>
      <td>0.285167</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Norovirus</td>
      <td>116vqn</td>
      <td>1.349811e+09</td>
      <td>-0.051453</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Norovirus</td>
      <td>13zkix</td>
      <td>1.354213e+09</td>
      <td>0.185400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Norovirus</td>
      <td>1423g8</td>
      <td>1.354323e+09</td>
      <td>0.325450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Norovirus</td>
      <td>14b56c</td>
      <td>1.354716e+09</td>
      <td>-0.246650</td>
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

plt.savefig("Foodbornekw_Sentiments_all.png", dpi=350)

plt.show()
```


![png](output_36_0.png)



```python
year_2017_df = reddit_comments_df.loc[reddit_comments_df["Date"] == 2017,:]
year_2017_df.head()
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
      <th>134</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I am a server in a restaurant and deal with gl...</td>
      <td>0.7783</td>
      <td>0.145</td>
      <td>0.000</td>
      <td>0.855</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>135</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Seriously people, we wont get pissed if you ju...</td>
      <td>0.2681</td>
      <td>0.126</td>
      <td>0.124</td>
      <td>0.750</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>136</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>As the proud owner of a nasty shrimp allergy, ...</td>
      <td>-0.9741</td>
      <td>0.094</td>
      <td>0.217</td>
      <td>0.689</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>137</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Unfortunately, there's a lot of truth in this....</td>
      <td>-0.9501</td>
      <td>0.069</td>
      <td>0.145</td>
      <td>0.785</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>138</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Yeah I always have to explain that I'm actuall...</td>
      <td>-0.2960</td>
      <td>0.133</td>
      <td>0.265</td>
      <td>0.602</td>
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
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I am a server in a restaurant and deal with gl...</td>
      <td>0.7783</td>
      <td>0.145</td>
      <td>0.000</td>
      <td>0.855</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Seriously people, we wont get pissed if you ju...</td>
      <td>0.2681</td>
      <td>0.126</td>
      <td>0.124</td>
      <td>0.750</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>As the proud owner of a nasty shrimp allergy, ...</td>
      <td>-0.9741</td>
      <td>0.094</td>
      <td>0.217</td>
      <td>0.689</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Unfortunately, there's a lot of truth in this....</td>
      <td>-0.9501</td>
      <td>0.069</td>
      <td>0.145</td>
      <td>0.785</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Yeah I always have to explain that I'm actuall...</td>
      <td>-0.2960</td>
      <td>0.133</td>
      <td>0.265</td>
      <td>0.602</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Chef here. I have a great deal of sympathy for...</td>
      <td>-0.2991</td>
      <td>0.126</td>
      <td>0.154</td>
      <td>0.720</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I have an aunt with a very serious strawberry ...</td>
      <td>-0.5481</td>
      <td>0.088</td>
      <td>0.109</td>
      <td>0.803</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I had a weird experience last week that I thin...</td>
      <td>0.6232</td>
      <td>0.078</td>
      <td>0.037</td>
      <td>0.885</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>It's a catch 22. My wife has a legit, diagnose...</td>
      <td>0.6801</td>
      <td>0.133</td>
      <td>0.060</td>
      <td>0.807</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I'm with the article. This makes me nervous. I...</td>
      <td>-0.1391</td>
      <td>0.072</td>
      <td>0.090</td>
      <td>0.838</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I once dated a girl who was greatly concerned ...</td>
      <td>-0.6361</td>
      <td>0.038</td>
      <td>0.090</td>
      <td>0.872</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I have IBS-A and attempt to avoid restaurants ...</td>
      <td>-0.7845</td>
      <td>0.032</td>
      <td>0.140</td>
      <td>0.828</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>&gt; As for Elliott, she wants the impostors to k...</td>
      <td>-0.5302</td>
      <td>0.077</td>
      <td>0.116</td>
      <td>0.807</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Those bastards who like to pretend they have d...</td>
      <td>-0.6794</td>
      <td>0.099</td>
      <td>0.145</td>
      <td>0.756</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>As a chef I take all allergies very seriously....</td>
      <td>-0.7774</td>
      <td>0.000</td>
      <td>0.106</td>
      <td>0.894</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>There are other, non allergic, medical reasons...</td>
      <td>-0.3815</td>
      <td>0.074</td>
      <td>0.089</td>
      <td>0.836</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I don't have a specific allergy, but I do have...</td>
      <td>0.7579</td>
      <td>0.182</td>
      <td>0.135</td>
      <td>0.683</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Between bogus "service animals" and "allergies...</td>
      <td>-0.3818</td>
      <td>0.000</td>
      <td>0.178</td>
      <td>0.822</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Had gone for Indian with my work mates. I have...</td>
      <td>-0.8748</td>
      <td>0.090</td>
      <td>0.154</td>
      <td>0.756</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Hell, I used to deal with this shenanigans whe...</td>
      <td>-0.9578</td>
      <td>0.000</td>
      <td>0.220</td>
      <td>0.780</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I once had a lady tell me she was allergic to ...</td>
      <td>-0.7945</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I went to Disney and said I had an allergy to ...</td>
      <td>-0.2533</td>
      <td>0.080</td>
      <td>0.106</td>
      <td>0.814</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Both of my sister have cialiacs disease which...</td>
      <td>-0.6908</td>
      <td>0.064</td>
      <td>0.109</td>
      <td>0.827</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I worked with a guy who got a big settlement w...</td>
      <td>-0.9327</td>
      <td>0.000</td>
      <td>0.177</td>
      <td>0.823</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Faking it can be a broad term.\n\nI'm going th...</td>
      <td>0.8689</td>
      <td>0.139</td>
      <td>0.060</td>
      <td>0.801</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>My son is allergic to like...everything.\n\nI ...</td>
      <td>0.8360</td>
      <td>0.313</td>
      <td>0.068</td>
      <td>0.619</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Yes. Ffs. Please. As someone who will spend 12...</td>
      <td>-0.8895</td>
      <td>0.090</td>
      <td>0.175</td>
      <td>0.735</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>I have a severe nut allergy and a dairy allerg...</td>
      <td>0.7000</td>
      <td>0.111</td>
      <td>0.059</td>
      <td>0.831</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>Egg allergy here... Whenever I go out to eat, ...</td>
      <td>0.8126</td>
      <td>0.149</td>
      <td>0.039</td>
      <td>0.812</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food allergy</td>
      <td>6dw1ph</td>
      <td>all</td>
      <td>1.496033e+09</td>
      <td>People with serious food allergies want impost...</td>
      <td>24490</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>4196</td>
      <td>http://www.cbc.ca/news/business/food-allergies...</td>
      <td>cbc.ca</td>
      <td>chef here. to all you people with allergies an...</td>
      <td>0.5853</td>
      <td>0.124</td>
      <td>0.095</td>
      <td>0.781</td>
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
      <th>5389</th>
      <td>Norovirus</td>
      <td>69az7n</td>
      <td>all</td>
      <td>1.493967e+09</td>
      <td>Norovirus prompts closure of 3 Sacramento Coun...</td>
      <td>4</td>
      <td>http://www.kcra.com/article/norovirus-prompts-...</td>
      <td>2</td>
      <td>http://www.kcra.com/article/norovirus-prompts-...</td>
      <td>kcra.com</td>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>-0.2023</td>
      <td>0.055</td>
      <td>0.069</td>
      <td>0.876</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5390</th>
      <td>Norovirus</td>
      <td>69az7n</td>
      <td>all</td>
      <td>1.493967e+09</td>
      <td>Norovirus prompts closure of 3 Sacramento Coun...</td>
      <td>4</td>
      <td>http://www.kcra.com/article/norovirus-prompts-...</td>
      <td>2</td>
      <td>http://www.kcra.com/article/norovirus-prompts-...</td>
      <td>kcra.com</td>
      <td>Unsurprising. Children are are like a disease ...</td>
      <td>0.6124</td>
      <td>0.333</td>
      <td>0.000</td>
      <td>0.667</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5391</th>
      <td>Norovirus</td>
      <td>7k7yvr</td>
      <td>all</td>
      <td>1.513471e+09</td>
      <td>Is this a crazy plan? (Norovirus mention)</td>
      <td>7</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Not weird or crazy at all! Also, I'm really pr...</td>
      <td>-0.6905</td>
      <td>0.104</td>
      <td>0.311</td>
      <td>0.585</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5392</th>
      <td>Norovirus</td>
      <td>7k7yvr</td>
      <td>all</td>
      <td>1.513471e+09</td>
      <td>Is this a crazy plan? (Norovirus mention)</td>
      <td>7</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>I would say that if you can afford it, then ma...</td>
      <td>0.3182</td>
      <td>0.054</td>
      <td>0.000</td>
      <td>0.946</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5393</th>
      <td>Norovirus</td>
      <td>7k7yvr</td>
      <td>all</td>
      <td>1.513471e+09</td>
      <td>Is this a crazy plan? (Norovirus mention)</td>
      <td>7</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>If you actually had diarrhea, regardless of wh...</td>
      <td>0.4019</td>
      <td>0.119</td>
      <td>0.000</td>
      <td>0.881</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5394</th>
      <td>Norovirus</td>
      <td>7k7yvr</td>
      <td>all</td>
      <td>1.513471e+09</td>
      <td>Is this a crazy plan? (Norovirus mention)</td>
      <td>7</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Just outta curiosity are you flying first clas...</td>
      <td>-0.8512</td>
      <td>0.019</td>
      <td>0.125</td>
      <td>0.855</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5395</th>
      <td>Norovirus</td>
      <td>5xhysj</td>
      <td>all</td>
      <td>1.488677e+09</td>
      <td>Norovirus: How do I keep it from coming back?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>self.AskDocs</td>
      <td>Now all of you have had it it will naturally b...</td>
      <td>0.8841</td>
      <td>0.117</td>
      <td>0.036</td>
      <td>0.847</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5396</th>
      <td>Norovirus</td>
      <td>5xhysj</td>
      <td>all</td>
      <td>1.488677e+09</td>
      <td>Norovirus: How do I keep it from coming back?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>self.AskDocs</td>
      <td>Just make sure no fresh victims enter your hou...</td>
      <td>0.7717</td>
      <td>0.334</td>
      <td>0.167</td>
      <td>0.499</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5397</th>
      <td>Norovirus</td>
      <td>5xhysj</td>
      <td>all</td>
      <td>1.488677e+09</td>
      <td>Norovirus: How do I keep it from coming back?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>self.AskDocs</td>
      <td>In the short term your fine. You just got over...</td>
      <td>0.6428</td>
      <td>0.104</td>
      <td>0.037</td>
      <td>0.859</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5398</th>
      <td>Norovirus</td>
      <td>5xhysj</td>
      <td>all</td>
      <td>1.488677e+09</td>
      <td>Norovirus: How do I keep it from coming back?</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>10</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5xhy...</td>
      <td>self.AskDocs</td>
      <td>I hope you're using bleach products to disinfe...</td>
      <td>0.2960</td>
      <td>0.077</td>
      <td>0.072</td>
      <td>0.851</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5399</th>
      <td>Norovirus</td>
      <td>6o0pu1</td>
      <td>all</td>
      <td>1.500413e+09</td>
      <td>How Long Avoiding Home of Norovirus Patient?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6o0p...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6o0p...</td>
      <td>self.AskDocs</td>
      <td>Norovirus is very contagious and actually is s...</td>
      <td>0.7537</td>
      <td>0.248</td>
      <td>0.073</td>
      <td>0.679</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5400</th>
      <td>Norovirus</td>
      <td>6o0pu1</td>
      <td>all</td>
      <td>1.500413e+09</td>
      <td>How Long Avoiding Home of Norovirus Patient?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6o0p...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6o0p...</td>
      <td>self.AskDocs</td>
      <td>It's impossible to predict. The patient can st...</td>
      <td>-0.5122</td>
      <td>0.095</td>
      <td>0.132</td>
      <td>0.773</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5401</th>
      <td>Norovirus</td>
      <td>7gekxx</td>
      <td>all</td>
      <td>1.512002e+09</td>
      <td>Norovirus and taking medication</td>
      <td>3</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>self.bipolar</td>
      <td>Is there any way you can go to urgent care and...</td>
      <td>0.4019</td>
      <td>0.235</td>
      <td>0.108</td>
      <td>0.657</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5402</th>
      <td>Norovirus</td>
      <td>7gekxx</td>
      <td>all</td>
      <td>1.512002e+09</td>
      <td>Norovirus and taking medication</td>
      <td>3</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>self.bipolar</td>
      <td>be careful with the lithium- dehydration can m...</td>
      <td>0.4767</td>
      <td>0.146</td>
      <td>0.000</td>
      <td>0.854</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5403</th>
      <td>Norovirus</td>
      <td>7gekxx</td>
      <td>all</td>
      <td>1.512002e+09</td>
      <td>Norovirus and taking medication</td>
      <td>3</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>self.bipolar</td>
      <td>Call your doctor.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5404</th>
      <td>Norovirus</td>
      <td>7gekxx</td>
      <td>all</td>
      <td>1.512002e+09</td>
      <td>Norovirus and taking medication</td>
      <td>3</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/bipolar/comments/7gek...</td>
      <td>self.bipolar</td>
      <td>Thanks everyone. Feeling a little better now, ...</td>
      <td>0.5717</td>
      <td>0.213</td>
      <td>0.084</td>
      <td>0.703</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5405</th>
      <td>Norovirus</td>
      <td>5lngnw</td>
      <td>all</td>
      <td>1.483418e+09</td>
      <td>Carleton Place hospital still fighting norovir...</td>
      <td>2</td>
      <td>http://www.cbc.ca/news/canada/ottawa/carleton-...</td>
      <td>3</td>
      <td>http://www.cbc.ca/news/canada/ottawa/carleton-...</td>
      <td>cbc.ca</td>
      <td>I've had the norovirus, shit fucking sucks.</td>
      <td>-0.7501</td>
      <td>0.000</td>
      <td>0.561</td>
      <td>0.439</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5406</th>
      <td>Norovirus</td>
      <td>5lngnw</td>
      <td>all</td>
      <td>1.483418e+09</td>
      <td>Carleton Place hospital still fighting norovir...</td>
      <td>2</td>
      <td>http://www.cbc.ca/news/canada/ottawa/carleton-...</td>
      <td>3</td>
      <td>http://www.cbc.ca/news/canada/ottawa/carleton-...</td>
      <td>cbc.ca</td>
      <td>Wife, myself and my 18month old got it last Th...</td>
      <td>0.1511</td>
      <td>0.138</td>
      <td>0.118</td>
      <td>0.743</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5407</th>
      <td>Norovirus</td>
      <td>5lngnw</td>
      <td>all</td>
      <td>1.483418e+09</td>
      <td>Carleton Place hospital still fighting norovir...</td>
      <td>2</td>
      <td>http://www.cbc.ca/news/canada/ottawa/carleton-...</td>
      <td>3</td>
      <td>http://www.cbc.ca/news/canada/ottawa/carleton-...</td>
      <td>cbc.ca</td>
      <td>My two kids and I are just recovering from it....</td>
      <td>-0.7003</td>
      <td>0.000</td>
      <td>0.345</td>
      <td>0.655</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5408</th>
      <td>Norovirus</td>
      <td>5m8n64</td>
      <td>all</td>
      <td>1.483675e+09</td>
      <td>Think I have norovirus :(</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Pretty sure that is what went through our hous...</td>
      <td>0.9097</td>
      <td>0.271</td>
      <td>0.063</td>
      <td>0.666</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5409</th>
      <td>Norovirus</td>
      <td>5m8n64</td>
      <td>all</td>
      <td>1.483675e+09</td>
      <td>Think I have norovirus :(</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I had this a couple months ago and my daughter...</td>
      <td>-0.7809</td>
      <td>0.090</td>
      <td>0.198</td>
      <td>0.712</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5410</th>
      <td>Norovirus</td>
      <td>5m8n64</td>
      <td>all</td>
      <td>1.483675e+09</td>
      <td>Think I have norovirus :(</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Oh no! I'm so sorry!</td>
      <td>-0.5231</td>
      <td>0.000</td>
      <td>0.593</td>
      <td>0.407</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5411</th>
      <td>Norovirus</td>
      <td>5m8n64</td>
      <td>all</td>
      <td>1.483675e+09</td>
      <td>Think I have norovirus :(</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>This is us right now. Baby had it first then m...</td>
      <td>-0.8531</td>
      <td>0.045</td>
      <td>0.161</td>
      <td>0.795</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5412</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Gah, I hate when people think lying will help ...</td>
      <td>-0.7806</td>
      <td>0.143</td>
      <td>0.318</td>
      <td>0.539</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5413</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Also like to add, no crazy lovey dovey kissing...</td>
      <td>0.8268</td>
      <td>0.398</td>
      <td>0.149</td>
      <td>0.453</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5414</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Now Monday, still nothing. I'm getting more co...</td>
      <td>0.6361</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5415</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>So I didn't catch it during the week. I hung o...</td>
      <td>0.1007</td>
      <td>0.070</td>
      <td>0.057</td>
      <td>0.873</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5416</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>Down water, take vocal breaks, and just rest a...</td>
      <td>0.9273</td>
      <td>0.179</td>
      <td>0.016</td>
      <td>0.805</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5417</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>I would say rest it as much as possible. If wo...</td>
      <td>0.9690</td>
      <td>0.158</td>
      <td>0.021</td>
      <td>0.821</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>5418</th>
      <td>Norovirus</td>
      <td>6wktp0</td>
      <td>all</td>
      <td>1.503969e+09</td>
      <td>Norovirus :(</td>
      <td>2</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>self.AskDocs</td>
      <td>It usually runs its course, its does generally...</td>
      <td>0.7750</td>
      <td>0.140</td>
      <td>0.053</td>
      <td>0.807</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
<p>5419 rows × 16 columns</p>
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
      <th rowspan="5" valign="top">Norovirus</th>
      <th>5laxjc</th>
      <th>1.483238e+09</th>
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
      <th>5lngnw</th>
      <th>1.483418e+09</th>
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
      <th>5lpsei</th>
      <th>1.483445e+09</th>
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
      <th>5m3vbl</th>
      <th>1.483615e+09</th>
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
    <tr>
      <th>5m8n64</th>
      <th>1.483675e+09</th>
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
      <th rowspan="30" valign="top">Norovirus</th>
      <th>5laxjc</th>
      <th>1.483238e+09</th>
      <td>0.098000</td>
    </tr>
    <tr>
      <th>5lngnw</th>
      <th>1.483418e+09</th>
      <td>-0.433100</td>
    </tr>
    <tr>
      <th>5lpsei</th>
      <th>1.483445e+09</th>
      <td>0.948150</td>
    </tr>
    <tr>
      <th>5m3vbl</th>
      <th>1.483615e+09</th>
      <td>-0.039500</td>
    </tr>
    <tr>
      <th>5m8n64</th>
      <th>1.483675e+09</th>
      <td>-0.311850</td>
    </tr>
    <tr>
      <th>5mk0lv</th>
      <th>1.483816e+09</th>
      <td>-0.309400</td>
    </tr>
    <tr>
      <th>5n1dt5</th>
      <th>1.484035e+09</th>
      <td>0.105600</td>
    </tr>
    <tr>
      <th>5n63hy</th>
      <th>1.484096e+09</th>
      <td>0.323520</td>
    </tr>
    <tr>
      <th>5olyeb</th>
      <th>1.484728e+09</th>
      <td>-0.389157</td>
    </tr>
    <tr>
      <th>5or1sc</th>
      <th>1.484793e+09</th>
      <td>-0.137488</td>
    </tr>
    <tr>
      <th>5otiqw</th>
      <th>1.484817e+09</th>
      <td>0.259440</td>
    </tr>
    <tr>
      <th>5p1gw0</th>
      <th>1.484911e+09</th>
      <td>-0.359800</td>
    </tr>
    <tr>
      <th>5p8uj3</th>
      <th>1.485002e+09</th>
      <td>-0.606833</td>
    </tr>
    <tr>
      <th>5pl6im</th>
      <th>1.485163e+09</th>
      <td>-0.075517</td>
    </tr>
    <tr>
      <th>5pvpwq</th>
      <th>1.485288e+09</th>
      <td>-0.087767</td>
    </tr>
    <tr>
      <th>5pwztf</th>
      <th>1.485303e+09</th>
      <td>-0.763200</td>
    </tr>
    <tr>
      <th>5pxdws</th>
      <th>1.485307e+09</th>
      <td>-0.317650</td>
    </tr>
    <tr>
      <th>5qaadm</th>
      <th>1.485468e+09</th>
      <td>-0.126000</td>
    </tr>
    <tr>
      <th>5qe8t2</th>
      <th>1.485508e+09</th>
      <td>0.261583</td>
    </tr>
    <tr>
      <th>5qrl5v</th>
      <th>1.485687e+09</th>
      <td>0.195750</td>
    </tr>
    <tr>
      <th>5rhg3l</th>
      <th>1.486005e+09</th>
      <td>-0.008263</td>
    </tr>
    <tr>
      <th>5rvufx</th>
      <th>1.486178e+09</th>
      <td>-0.460967</td>
    </tr>
    <tr>
      <th>5s92tz</th>
      <th>1.486349e+09</th>
      <td>0.151400</td>
    </tr>
    <tr>
      <th>5tnsn8</th>
      <th>1.486959e+09</th>
      <td>0.638100</td>
    </tr>
    <tr>
      <th>5ttxjz</th>
      <th>1.487033e+09</th>
      <td>-0.002820</td>
    </tr>
    <tr>
      <th>5v1r1q</th>
      <th>1.487583e+09</th>
      <td>-0.376380</td>
    </tr>
    <tr>
      <th>5v66ye</th>
      <th>1.487644e+09</th>
      <td>-0.414200</td>
    </tr>
    <tr>
      <th>5vz0ys</th>
      <th>1.487988e+09</th>
      <td>-0.134900</td>
    </tr>
    <tr>
      <th>5xhysj</th>
      <th>1.488677e+09</th>
      <td>0.648650</td>
    </tr>
    <tr>
      <th>5yge3k</th>
      <th>1.489109e+09</th>
      <td>-0.051800</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="30" valign="top">salmonella</th>
      <th>6xywj5</th>
      <th>1.504539e+09</th>
      <td>0.165814</td>
    </tr>
    <tr>
      <th>6xzktw</th>
      <th>1.504550e+09</th>
      <td>-0.024800</td>
    </tr>
    <tr>
      <th>6y9uhg</th>
      <th>1.504664e+09</th>
      <td>0.185971</td>
    </tr>
    <tr>
      <th>6z8bks</th>
      <th>1.505080e+09</th>
      <td>-0.899100</td>
    </tr>
    <tr>
      <th>6zprqk</th>
      <th>1.505278e+09</th>
      <td>0.203271</td>
    </tr>
    <tr>
      <th>6zs6g2</th>
      <th>1.505303e+09</th>
      <td>0.202300</td>
    </tr>
    <tr>
      <th>7001l6</th>
      <th>1.505392e+09</th>
      <td>-0.164733</td>
    </tr>
    <tr>
      <th>70dy1i</th>
      <th>1.505551e+09</th>
      <td>0.052870</td>
    </tr>
    <tr>
      <th>737i3w</th>
      <th>1.506717e+09</th>
      <td>0.211292</td>
    </tr>
    <tr>
      <th>73og5n</th>
      <th>1.506922e+09</th>
      <td>0.024390</td>
    </tr>
    <tr>
      <th>74m0vf</th>
      <th>1.507302e+09</th>
      <td>0.366443</td>
    </tr>
    <tr>
      <th>74p4gg</th>
      <th>1.507339e+09</th>
      <td>-0.542300</td>
    </tr>
    <tr>
      <th>75ntbn</th>
      <th>1.507741e+09</th>
      <td>-0.403100</td>
    </tr>
    <tr>
      <th>75oavy</th>
      <th>1.507748e+09</th>
      <td>0.576233</td>
    </tr>
    <tr>
      <th>77zs0f</th>
      <th>1.508702e+09</th>
      <td>0.132264</td>
    </tr>
    <tr>
      <th>7a48qi</th>
      <th>1.509578e+09</th>
      <td>0.146050</td>
    </tr>
    <tr>
      <th>7adb0h</th>
      <th>1.509675e+09</th>
      <td>0.286150</td>
    </tr>
    <tr>
      <th>7agf0h</th>
      <th>1.509703e+09</th>
      <td>-0.116992</td>
    </tr>
    <tr>
      <th>7c9h9d</th>
      <th>1.510448e+09</th>
      <td>-0.409817</td>
    </tr>
    <tr>
      <th>7cpuse</th>
      <th>1.510633e+09</th>
      <td>0.240033</td>
    </tr>
    <tr>
      <th>7e32wx</th>
      <th>1.511151e+09</th>
      <td>-0.140060</td>
    </tr>
    <tr>
      <th>7fyfsv</th>
      <th>1.511845e+09</th>
      <td>-0.136267</td>
    </tr>
    <tr>
      <th>7gzmex</th>
      <th>1.512206e+09</th>
      <td>-0.153875</td>
    </tr>
    <tr>
      <th>7gztkt</th>
      <th>1.512208e+09</th>
      <td>-0.229650</td>
    </tr>
    <tr>
      <th>7hc0rf</th>
      <th>1.512361e+09</th>
      <td>0.006450</td>
    </tr>
    <tr>
      <th>7ithv3</th>
      <th>1.512935e+09</th>
      <td>-0.067375</td>
    </tr>
    <tr>
      <th>7iwo44</th>
      <th>1.512968e+09</th>
      <td>-0.040350</td>
    </tr>
    <tr>
      <th>7j1xq6</th>
      <th>1.513025e+09</th>
      <td>-0.493900</td>
    </tr>
    <tr>
      <th>7j36gb</th>
      <th>1.513038e+09</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>7j44se</th>
      <th>1.513046e+09</th>
      <td>0.271467</td>
    </tr>
  </tbody>
</table>
<p>487 rows × 1 columns</p>
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
      <td>Norovirus</td>
      <td>5laxjc</td>
      <td>1.483238e+09</td>
      <td>0.09800</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Norovirus</td>
      <td>5lngnw</td>
      <td>1.483418e+09</td>
      <td>-0.43310</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>1.483445e+09</td>
      <td>0.94815</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Norovirus</td>
      <td>5m3vbl</td>
      <td>1.483615e+09</td>
      <td>-0.03950</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Norovirus</td>
      <td>5m8n64</td>
      <td>1.483675e+09</td>
      <td>-0.31185</td>
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

plt.savefig("Foodbornekw_Sentiments_2017.png", dpi=350)

plt.show()
```


![png](output_43_0.png)



```python
grouped_df2 = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "food poisoning",:]
grouped_df2 = grouped_df2.reset_index()
del grouped_df2['index']
grouped_df2
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
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>I hope you aren't allergic to arsenic., my lord.</td>
      <td>0.5842</td>
      <td>0.444</td>
      <td>0.000</td>
      <td>0.556</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>The cooks and the food tasters. They probably ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You'd get killed for ANYTHING in medieval time...</td>
      <td>-0.9217</td>
      <td>0.058</td>
      <td>0.339</td>
      <td>0.603</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>It seems extremely rare that someone would mak...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Science back then was surprisingly advanced co...</td>
      <td>0.6486</td>
      <td>0.240</td>
      <td>0.000</td>
      <td>0.760</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Who in Africa has ever heard of peanut allergy?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>There's some evidence that exposure in childho...</td>
      <td>0.4215</td>
      <td>0.113</td>
      <td>0.000</td>
      <td>0.887</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>I am not totally familiar with the science but...</td>
      <td>0.8819</td>
      <td>0.113</td>
      <td>0.065</td>
      <td>0.822</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>There was a thing back then where people thoug...</td>
      <td>-0.8201</td>
      <td>0.000</td>
      <td>0.201</td>
      <td>0.799</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Probably not too many people with serious alle...</td>
      <td>0.4033</td>
      <td>0.186</td>
      <td>0.166</td>
      <td>0.648</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>so I came in here to comment I originally read...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Dear King Joffrey :( RIP</td>
      <td>-0.0772</td>
      <td>0.306</td>
      <td>0.341</td>
      <td>0.353</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>People with serious food allergies didn't make...</td>
      <td>-0.0772</td>
      <td>0.000</td>
      <td>0.126</td>
      <td>0.874</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Enjoy this new delicacy called "peanuts" m'lord</td>
      <td>0.4939</td>
      <td>0.348</td>
      <td>0.000</td>
      <td>0.652</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>People didn't have food allergies until THE BO...</td>
      <td>-0.6633</td>
      <td>0.099</td>
      <td>0.251</td>
      <td>0.650</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>I hope you aren't allergic to arsenic., my lord.</td>
      <td>0.5842</td>
      <td>0.444</td>
      <td>0.000</td>
      <td>0.556</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>The cooks and the food tasters. They probably ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>You'd get killed for ANYTHING in medieval time...</td>
      <td>-0.9217</td>
      <td>0.058</td>
      <td>0.339</td>
      <td>0.603</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>It seems extremely rare that someone would mak...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Science back then was surprisingly advanced co...</td>
      <td>0.6486</td>
      <td>0.240</td>
      <td>0.000</td>
      <td>0.760</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Who in Africa has ever heard of peanut allergy?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>There's some evidence that exposure in childho...</td>
      <td>0.4215</td>
      <td>0.113</td>
      <td>0.000</td>
      <td>0.887</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>I am not totally familiar with the science but...</td>
      <td>0.8819</td>
      <td>0.113</td>
      <td>0.065</td>
      <td>0.822</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>There was a thing back then where people thoug...</td>
      <td>-0.8201</td>
      <td>0.000</td>
      <td>0.201</td>
      <td>0.799</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Probably not too many people with serious alle...</td>
      <td>0.4033</td>
      <td>0.186</td>
      <td>0.166</td>
      <td>0.648</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>so I came in here to comment I originally read...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Dear King Joffrey :( RIP</td>
      <td>-0.0772</td>
      <td>0.306</td>
      <td>0.341</td>
      <td>0.353</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>People with serious food allergies didn't make...</td>
      <td>-0.0772</td>
      <td>0.000</td>
      <td>0.126</td>
      <td>0.874</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Enjoy this new delicacy called "peanuts" m'lord</td>
      <td>0.4939</td>
      <td>0.348</td>
      <td>0.000</td>
      <td>0.652</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food poisoning</td>
      <td>5xan3p</td>
      <td>all</td>
      <td>1.488580e+09</td>
      <td>Tons of ancient and medieval cooks must have g...</td>
      <td>1261</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>75</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>People didn't have food allergies until THE BO...</td>
      <td>-0.6633</td>
      <td>0.099</td>
      <td>0.251</td>
      <td>0.650</td>
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
      <th>7229</th>
      <td>food poisoning</td>
      <td>6vpiw6</td>
      <td>all</td>
      <td>1.503593e+09</td>
      <td>SEA Games: 16 Malaysian athletes hit by food p...</td>
      <td>34</td>
      <td>http://www.channelnewsasia.com/news/sport/sea-...</td>
      <td>21</td>
      <td>http://www.channelnewsasia.com/news/sport/sea-...</td>
      <td>channelnewsasia.com</td>
      <td>Hotel 5 bintang pun kena keracunan ka?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7230</th>
      <td>food poisoning</td>
      <td>1k7kwu</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>TIL Michael Jordan's famous "The Flu Game" is ...</td>
      <td>42</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>9</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>m.espn.go.com</td>
      <td>He also might have been hungover as hell. Lots...</td>
      <td>-0.6808</td>
      <td>0.000</td>
      <td>0.235</td>
      <td>0.765</td>
    </tr>
    <tr>
      <th>7231</th>
      <td>food poisoning</td>
      <td>1k7kwu</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>TIL Michael Jordan's famous "The Flu Game" is ...</td>
      <td>42</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>9</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>m.espn.go.com</td>
      <td>Yeah I've heard that he was actually out all n...</td>
      <td>0.2960</td>
      <td>0.155</td>
      <td>0.000</td>
      <td>0.845</td>
    </tr>
    <tr>
      <th>7232</th>
      <td>food poisoning</td>
      <td>1k7kwu</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>TIL Michael Jordan's famous "The Flu Game" is ...</td>
      <td>42</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>9</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>m.espn.go.com</td>
      <td>"Who ordered pizza?!" - Tron</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7233</th>
      <td>food poisoning</td>
      <td>1k7kwu</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>TIL Michael Jordan's famous "The Flu Game" is ...</td>
      <td>42</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>9</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>m.espn.go.com</td>
      <td>[Desktop link for the lazy](http://espn.go.com...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7234</th>
      <td>food poisoning</td>
      <td>1k7kwu</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>TIL Michael Jordan's famous "The Flu Game" is ...</td>
      <td>42</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>9</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>m.espn.go.com</td>
      <td>As a Utah Jazz fan (at the time)...I remember ...</td>
      <td>-0.5009</td>
      <td>0.177</td>
      <td>0.201</td>
      <td>0.622</td>
    </tr>
    <tr>
      <th>7235</th>
      <td>food poisoning</td>
      <td>1k7kwu</td>
      <td>all</td>
      <td>1.376349e+09</td>
      <td>TIL Michael Jordan's famous "The Flu Game" is ...</td>
      <td>42</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>9</td>
      <td>http://m.espn.go.com/general/story?storyId=918...</td>
      <td>m.espn.go.com</td>
      <td>Where do you read intentional in that story?  ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7236</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>The fact that it doesn't take you below 15% co...</td>
      <td>-0.2263</td>
      <td>0.058</td>
      <td>0.076</td>
      <td>0.865</td>
    </tr>
    <tr>
      <th>7237</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>Thanks for testing this out, I am in the middl...</td>
      <td>0.2500</td>
      <td>0.150</td>
      <td>0.098</td>
      <td>0.751</td>
    </tr>
    <tr>
      <th>7238</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>That's one of the reasons hibernating is still...</td>
      <td>-0.2023</td>
      <td>0.130</td>
      <td>0.185</td>
      <td>0.685</td>
    </tr>
    <tr>
      <th>7239</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>Have you tested infections from bites!???  Tha...</td>
      <td>0.8029</td>
      <td>0.311</td>
      <td>0.000</td>
      <td>0.689</td>
    </tr>
    <tr>
      <th>7240</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>FUCK FUCK FUCK FUCK. I just died in my last pl...</td>
      <td>-0.9809</td>
      <td>0.053</td>
      <td>0.616</td>
      <td>0.331</td>
    </tr>
    <tr>
      <th>7241</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>So basically, you gotta decide between wasting...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.213</td>
      <td>0.787</td>
    </tr>
    <tr>
      <th>7242</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>At least this is one of the easier conditions ...</td>
      <td>-0.8957</td>
      <td>0.065</td>
      <td>0.192</td>
      <td>0.743</td>
    </tr>
    <tr>
      <th>7243</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>Not sure if I misread your comment, but did yo...</td>
      <td>-0.9650</td>
      <td>0.114</td>
      <td>0.292</td>
      <td>0.594</td>
    </tr>
    <tr>
      <th>7244</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>Does food poisoning honestly not drop below 15...</td>
      <td>-0.3790</td>
      <td>0.120</td>
      <td>0.184</td>
      <td>0.696</td>
    </tr>
    <tr>
      <th>7245</th>
      <td>food poisoning</td>
      <td>44nj7p</td>
      <td>all</td>
      <td>1.454908e+09</td>
      <td>Curing Food Poisoning without Antibiotics</td>
      <td>20</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>22</td>
      <td>https://imgur.com/a/8jjie</td>
      <td>imgur.com</td>
      <td>wow man this changes so much in my playstyle. ...</td>
      <td>0.7717</td>
      <td>0.401</td>
      <td>0.000</td>
      <td>0.599</td>
    </tr>
    <tr>
      <th>7246</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>Last night's dinner. Made my day at work today...</td>
      <td>-0.6808</td>
      <td>0.000</td>
      <td>0.295</td>
      <td>0.705</td>
    </tr>
    <tr>
      <th>7247</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>5 a.m. Denny's</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7248</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>Cheddar and bacon potato salad.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7249</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>King crab legs. I was puking my guts out for a...</td>
      <td>-0.4215</td>
      <td>0.000</td>
      <td>0.167</td>
      <td>0.833</td>
    </tr>
    <tr>
      <th>7250</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>Double cheese pizza with mushrooms in it, some...</td>
      <td>-0.6486</td>
      <td>0.000</td>
      <td>0.195</td>
      <td>0.805</td>
    </tr>
    <tr>
      <th>7251</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>a poorly cooked hamburger at home\n\n</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7252</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>The only time I had food poising was the only ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7253</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>What-A-Burger. Happened to my girlfriend and I...</td>
      <td>0.2382</td>
      <td>0.060</td>
      <td>0.061</td>
      <td>0.878</td>
    </tr>
    <tr>
      <th>7254</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>A cherry directly from a cherry tree. Looked f...</td>
      <td>-0.2500</td>
      <td>0.209</td>
      <td>0.209</td>
      <td>0.581</td>
    </tr>
    <tr>
      <th>7255</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>Not going to jinx myself...so im not gonna say...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7256</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>Mine was baked fish from long john silvers fas...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7257</th>
      <td>food poisoning</td>
      <td>4xvo7y</td>
      <td>all</td>
      <td>1.471322e+09</td>
      <td>What was the last food that gave you food pois...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>29</td>
      <td>https://www.reddit.com/r/AskReddit/comments/4x...</td>
      <td>self.AskReddit</td>
      <td>It an an apple pie. It was delicious, even the...</td>
      <td>0.5719</td>
      <td>0.252</td>
      <td>0.000</td>
      <td>0.748</td>
    </tr>
    <tr>
      <th>7258</th>
      <td>food poisoning</td>
      <td>2r3950</td>
      <td>all</td>
      <td>1.420222e+09</td>
      <td>HIFW I get food poisoning mere hours before a ...</td>
      <td>49</td>
      <td>http://24.media.tumblr.com/tumblr_m5pgxp1p141r...</td>
      <td>1</td>
      <td>http://24.media.tumblr.com/tumblr_m5pgxp1p141r...</td>
      <td>24.media.tumblr.com</td>
      <td>I'm so sorry.</td>
      <td>-0.1513</td>
      <td>0.000</td>
      <td>0.443</td>
      <td>0.557</td>
    </tr>
  </tbody>
</table>
<p>7259 rows × 15 columns</p>
</div>




```python
grouped_df2 = grouped_df2.groupby(['Created Date','Submission ID'])
```


```python
grouped_df2.count().head()
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
      <th>1.190836e+09</th>
      <th>2toho</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1.231573e+09</th>
      <th>7onmo</th>
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
      <th>1.246539e+09</th>
      <th>8xi9s</th>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1.272749e+09</th>
      <th>byq0y</th>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
      <td>28</td>
    </tr>
    <tr>
      <th>1.275696e+09</th>
      <th>cbgn8</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_df2 = pd.DataFrame(grouped_df2["Compound Score"].mean())
grouped_df2
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
      <th>1.190836e+09</th>
      <th>2toho</th>
      <td>-0.135145</td>
    </tr>
    <tr>
      <th>1.231573e+09</th>
      <th>7onmo</th>
      <td>-0.088925</td>
    </tr>
    <tr>
      <th>1.246539e+09</th>
      <th>8xi9s</th>
      <td>-0.251752</td>
    </tr>
    <tr>
      <th>1.272749e+09</th>
      <th>byq0y</th>
      <td>-0.174561</td>
    </tr>
    <tr>
      <th>1.275696e+09</th>
      <th>cbgn8</th>
      <td>-0.429963</td>
    </tr>
    <tr>
      <th>1.276178e+09</th>
      <th>cdfed</th>
      <td>-0.008141</td>
    </tr>
    <tr>
      <th>1.284139e+09</th>
      <th>dc0d8</th>
      <td>-0.275681</td>
    </tr>
    <tr>
      <th>1.284955e+09</th>
      <th>dg1pd</th>
      <td>0.157260</td>
    </tr>
    <tr>
      <th>1.314616e+09</th>
      <th>jxkof</th>
      <td>-0.105375</td>
    </tr>
    <tr>
      <th>1.316900e+09</th>
      <th>kq0lv</th>
      <td>-0.290038</td>
    </tr>
    <tr>
      <th>1.317255e+09</th>
      <th>ku79d</th>
      <td>0.026456</td>
    </tr>
    <tr>
      <th>1.319784e+09</th>
      <th>lri0l</th>
      <td>-0.002671</td>
    </tr>
    <tr>
      <th>1.320037e+09</th>
      <th>ludy5</th>
      <td>-0.295233</td>
    </tr>
    <tr>
      <th>1.320400e+09</th>
      <th>lzr2i</th>
      <td>-0.081600</td>
    </tr>
    <tr>
      <th>1.326618e+09</th>
      <th>ohf06</th>
      <td>-0.709600</td>
    </tr>
    <tr>
      <th>1.326759e+09</th>
      <th>oje4t</th>
      <td>0.075014</td>
    </tr>
    <tr>
      <th>1.331449e+09</th>
      <th>qqt0y</th>
      <td>-0.076043</td>
    </tr>
    <tr>
      <th>1.335410e+09</th>
      <th>ss7a9</th>
      <td>0.636800</td>
    </tr>
    <tr>
      <th>1.335664e+09</th>
      <th>swzyk</th>
      <td>-0.382800</td>
    </tr>
    <tr>
      <th>1.338105e+09</th>
      <th>u6m77</th>
      <td>-0.514300</td>
    </tr>
    <tr>
      <th>1.340649e+09</th>
      <th>vkeai</th>
      <td>0.209233</td>
    </tr>
    <tr>
      <th>1.340660e+09</th>
      <th>vkk8c</th>
      <td>-0.026825</td>
    </tr>
    <tr>
      <th>1.340679e+09</th>
      <th>vl22h</th>
      <td>-0.254410</td>
    </tr>
    <tr>
      <th>1.342490e+09</th>
      <th>wnkcg</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.343872e+09</th>
      <th>xikum</th>
      <td>-0.203698</td>
    </tr>
    <tr>
      <th>1.345069e+09</th>
      <th>y9g0c</th>
      <td>0.104000</td>
    </tr>
    <tr>
      <th>1.345989e+09</th>
      <th>yucrt</th>
      <td>-0.512400</td>
    </tr>
    <tr>
      <th>1.348020e+09</th>
      <th>1038kb</th>
      <td>-0.453296</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.349529e+09</th>
      <th>1114j5</th>
      <td>-0.213175</td>
    </tr>
    <tr>
      <th>1114qe</th>
      <td>0.336733</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.516029e+09</th>
      <th>7qi420</th>
      <td>-0.193600</td>
    </tr>
    <tr>
      <th>1.516630e+09</th>
      <th>7s3u8y</th>
      <td>-0.311450</td>
    </tr>
    <tr>
      <th>1.516711e+09</th>
      <th>7sbxox</th>
      <td>-0.513925</td>
    </tr>
    <tr>
      <th>1.517018e+09</th>
      <th>7t6c19</th>
      <td>0.503933</td>
    </tr>
    <tr>
      <th>1.517097e+09</th>
      <th>7tdh11</th>
      <td>0.064443</td>
    </tr>
    <tr>
      <th>1.517114e+09</th>
      <th>7tfe9g</th>
      <td>-0.253258</td>
    </tr>
    <tr>
      <th>1.517200e+09</th>
      <th>7tmumc</th>
      <td>0.525500</td>
    </tr>
    <tr>
      <th>1.517295e+09</th>
      <th>7twa5q</th>
      <td>-0.110250</td>
    </tr>
    <tr>
      <th>1.517318e+09</th>
      <th>7tyrip</th>
      <td>-0.320333</td>
    </tr>
    <tr>
      <th>1.517350e+09</th>
      <th>7u18o1</th>
      <td>-0.237810</td>
    </tr>
    <tr>
      <th>1.517459e+09</th>
      <th>7ucyt8</th>
      <td>0.057300</td>
    </tr>
    <tr>
      <th>1.517526e+09</th>
      <th>7ujbo5</th>
      <td>-0.273938</td>
    </tr>
    <tr>
      <th>1.518507e+09</th>
      <th>7x51kp</th>
      <td>-0.024127</td>
    </tr>
    <tr>
      <th>1.518892e+09</th>
      <th>7y5xal</th>
      <td>-0.296600</td>
    </tr>
    <tr>
      <th>1.518914e+09</th>
      <th>7y7l7s</th>
      <td>0.153787</td>
    </tr>
    <tr>
      <th>1.518967e+09</th>
      <th>7ycti6</th>
      <td>0.195678</td>
    </tr>
    <tr>
      <th>1.519112e+09</th>
      <th>7yrbah</th>
      <td>0.176825</td>
    </tr>
    <tr>
      <th>1.519359e+09</th>
      <th>7zhyfq</th>
      <td>0.117355</td>
    </tr>
    <tr>
      <th>1.519845e+09</th>
      <th>80v7wo</th>
      <td>-0.273427</td>
    </tr>
    <tr>
      <th>1.519953e+09</th>
      <th>816tsq</th>
      <td>-0.016200</td>
    </tr>
    <tr>
      <th>1.520111e+09</th>
      <th>81q0z6</th>
      <td>0.136611</td>
    </tr>
    <tr>
      <th>1.520540e+09</th>
      <th>82x20x</th>
      <td>-0.385607</td>
    </tr>
    <tr>
      <th>1.520921e+09</th>
      <th>83z1bd</th>
      <td>-0.215257</td>
    </tr>
    <tr>
      <th>1.521464e+09</th>
      <th>85h0c5</th>
      <td>-0.541000</td>
    </tr>
    <tr>
      <th>1.521773e+09</th>
      <th>86dyhv</th>
      <td>-0.349533</td>
    </tr>
    <tr>
      <th>1.521836e+09</th>
      <th>86k5km</th>
      <td>-0.007019</td>
    </tr>
    <tr>
      <th>1.521858e+09</th>
      <th>86mvxs</th>
      <td>-0.235808</td>
    </tr>
    <tr>
      <th>1.521920e+09</th>
      <th>86shnv</th>
      <td>0.005567</td>
    </tr>
    <tr>
      <th>1.521963e+09</th>
      <th>86wxi9</th>
      <td>-0.147515</td>
    </tr>
    <tr>
      <th>1.522074e+09</th>
      <th>876y6i</th>
      <td>-0.887333</td>
    </tr>
  </tbody>
</table>
<p>449 rows × 1 columns</p>
</div>




```python
grouped_df2.info()
```

    <class 'pandas.core.frame.DataFrame'>
    MultiIndex: 449 entries, (1190836050.0, 2toho) to (1522073644.0, 876y6i)
    Data columns (total 1 columns):
    Compound Score    449 non-null float64
    dtypes: float64(1)
    memory usage: 12.5+ KB



```python
grouped_df2 = grouped_df2.reset_index()
grouped_df2.head()
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
      <th>index</th>
      <th>Created Date</th>
      <th>Submission ID</th>
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1.190836e+09</td>
      <td>2toho</td>
      <td>-0.135145</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1.231573e+09</td>
      <td>7onmo</td>
      <td>-0.088925</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1.246539e+09</td>
      <td>8xi9s</td>
      <td>-0.251752</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1.272749e+09</td>
      <td>byq0y</td>
      <td>-0.174561</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>1.275696e+09</td>
      <td>cbgn8</td>
      <td>-0.429963</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df2, fit_reg=False, palette="Paired")

#plt.title("Food Poisoning Comment Sentiments on Reddit")

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

plt.savefig("Food_Poisoning_Sentiments.png", dpi=150)

plt.show()
```


![png](output_50_0.png)



```python
grouped_df3 = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "e. coli",:]
grouped_df3 = grouped_df3.reset_index()
del grouped_df3['index']
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
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>No.\n\nGalactus doesn't physically eat anythin...</td>
      <td>-0.0258</td>
      <td>0.121</td>
      <td>0.127</td>
      <td>0.751</td>
    </tr>
    <tr>
      <th>1</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>There is no living energy in zombies, so Galac...</td>
      <td>-0.3818</td>
      <td>0.106</td>
      <td>0.237</td>
      <td>0.657</td>
    </tr>
    <tr>
      <th>2</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>Does Galactus from the cancerverse have cancer...</td>
      <td>-0.5106</td>
      <td>0.156</td>
      <td>0.326</td>
      <td>0.519</td>
    </tr>
    <tr>
      <th>3</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>im pretty sure he had worst.</td>
      <td>0.1027</td>
      <td>0.437</td>
      <td>0.325</td>
      <td>0.238</td>
    </tr>
    <tr>
      <th>4</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>Go read marvel zombies, I guess?</td>
      <td>0.4215</td>
      <td>0.412</td>
      <td>0.000</td>
      <td>0.588</td>
    </tr>
    <tr>
      <th>5</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>No.\n\nGalactus doesn't physically eat anythin...</td>
      <td>-0.0258</td>
      <td>0.121</td>
      <td>0.127</td>
      <td>0.751</td>
    </tr>
    <tr>
      <th>6</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>There is no living energy in zombies, so Galac...</td>
      <td>-0.3818</td>
      <td>0.106</td>
      <td>0.237</td>
      <td>0.657</td>
    </tr>
    <tr>
      <th>7</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>Does Galactus from the cancerverse have cancer...</td>
      <td>-0.5106</td>
      <td>0.156</td>
      <td>0.326</td>
      <td>0.519</td>
    </tr>
    <tr>
      <th>8</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>im pretty sure he had worst.</td>
      <td>0.1027</td>
      <td>0.437</td>
      <td>0.325</td>
      <td>0.238</td>
    </tr>
    <tr>
      <th>9</th>
      <td>e. coli</td>
      <td>3807ij</td>
      <td>all</td>
      <td>1.433138e+09</td>
      <td>[Marvel Comics]If Galactus were to eat the ear...</td>
      <td>183</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>52</td>
      <td>https://www.reddit.com/r/AskScienceFiction/com...</td>
      <td>self.AskScienceFiction</td>
      <td>Go read marvel zombies, I guess?</td>
      <td>0.4215</td>
      <td>0.412</td>
      <td>0.000</td>
      <td>0.588</td>
    </tr>
    <tr>
      <th>10</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>11</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>12</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>13</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>14</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>15</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>16</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>17</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>18</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>19</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>20</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>21</th>
      <td>e. coli</td>
      <td>3vhh7u</td>
      <td>all</td>
      <td>1.449305e+09</td>
      <td>A widening U.S. E. coli outbreak has slammed s...</td>
      <td>129</td>
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
      <th>22</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>Soap is just used to help dirt/grease/microbes...</td>
      <td>0.9759</td>
      <td>0.336</td>
      <td>0.000</td>
      <td>0.664</td>
    </tr>
    <tr>
      <th>23</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>It doesn't necessarily do that to any large de...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>If properly washed by hand with hot water, yes...</td>
      <td>0.4417</td>
      <td>0.191</td>
      <td>0.097</td>
      <td>0.712</td>
    </tr>
    <tr>
      <th>25</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>1. That depends on the liquid dish soap you ha...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>Soap is just used to help dirt/grease/microbes...</td>
      <td>0.9759</td>
      <td>0.336</td>
      <td>0.000</td>
      <td>0.664</td>
    </tr>
    <tr>
      <th>27</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>It doesn't necessarily do that to any large de...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>If properly washed by hand with hot water, yes...</td>
      <td>0.4417</td>
      <td>0.191</td>
      <td>0.097</td>
      <td>0.712</td>
    </tr>
    <tr>
      <th>29</th>
      <td>e. coli</td>
      <td>4rxi01</td>
      <td>all</td>
      <td>1.468048e+09</td>
      <td>Does liquid dish soap (not dishwasher soap) ac...</td>
      <td>25</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/answers/comments/4rxi...</td>
      <td>self.answers</td>
      <td>1. That depends on the liquid dish soap you ha...</td>
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
      <th>5961</th>
      <td>e. coli</td>
      <td>3u8je8</td>
      <td>all</td>
      <td>1.448500e+09</td>
      <td>Multi-state E. coli outbreak linked to Costco'...</td>
      <td>26</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>8</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>consumeraffairs.com</td>
      <td>I will say that this is no joke. I now know my...</td>
      <td>0.9418</td>
      <td>0.212</td>
      <td>0.056</td>
      <td>0.733</td>
    </tr>
    <tr>
      <th>5962</th>
      <td>e. coli</td>
      <td>3u8je8</td>
      <td>all</td>
      <td>1.448500e+09</td>
      <td>Multi-state E. coli outbreak linked to Costco'...</td>
      <td>26</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>8</td>
      <td>http://www.consumeraffairs.com/news/multi-stat...</td>
      <td>consumeraffairs.com</td>
      <td>Their food taste like crap anyways. You ever h...</td>
      <td>-0.0258</td>
      <td>0.155</td>
      <td>0.161</td>
      <td>0.683</td>
    </tr>
    <tr>
      <th>5963</th>
      <td>e. coli</td>
      <td>3xrgva</td>
      <td>all</td>
      <td>1.450768e+09</td>
      <td>CDC investigating another outbreak of differen...</td>
      <td>27</td>
      <td>http://www.cnbc.com/2015/12/21/cdc-investigati...</td>
      <td>10</td>
      <td>http://www.cnbc.com/2015/12/21/cdc-investigati...</td>
      <td>cnbc.com</td>
      <td>Do you think this is just a conspiracy theory ...</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.139</td>
      <td>0.861</td>
    </tr>
    <tr>
      <th>5964</th>
      <td>e. coli</td>
      <td>3xrgva</td>
      <td>all</td>
      <td>1.450768e+09</td>
      <td>CDC investigating another outbreak of differen...</td>
      <td>27</td>
      <td>http://www.cnbc.com/2015/12/21/cdc-investigati...</td>
      <td>10</td>
      <td>http://www.cnbc.com/2015/12/21/cdc-investigati...</td>
      <td>cnbc.com</td>
      <td>I've had E. Coli! It was the worst. It was in ...</td>
      <td>-0.6275</td>
      <td>0.119</td>
      <td>0.179</td>
      <td>0.701</td>
    </tr>
    <tr>
      <th>5965</th>
      <td>e. coli</td>
      <td>3xrgva</td>
      <td>all</td>
      <td>1.450768e+09</td>
      <td>CDC investigating another outbreak of differen...</td>
      <td>27</td>
      <td>http://www.cnbc.com/2015/12/21/cdc-investigati...</td>
      <td>10</td>
      <td>http://www.cnbc.com/2015/12/21/cdc-investigati...</td>
      <td>cnbc.com</td>
      <td>Organic, local, non-GMO, fresh ingredients are...</td>
      <td>0.8313</td>
      <td>0.328</td>
      <td>0.000</td>
      <td>0.672</td>
    </tr>
    <tr>
      <th>5966</th>
      <td>e. coli</td>
      <td>4423l0</td>
      <td>all</td>
      <td>1.454565e+09</td>
      <td>AHS confirms E. coli outbreak in Calgary area</td>
      <td>26</td>
      <td>http://www.cbc.ca/news/canada/calgary/ecoli-ou...</td>
      <td>8</td>
      <td>http://www.cbc.ca/news/canada/calgary/ecoli-ou...</td>
      <td>cbc.ca</td>
      <td>&gt;Fourteen cases of the bacteria have been conf...</td>
      <td>-0.8316</td>
      <td>0.000</td>
      <td>0.164</td>
      <td>0.836</td>
    </tr>
    <tr>
      <th>5967</th>
      <td>e. coli</td>
      <td>4423l0</td>
      <td>all</td>
      <td>1.454565e+09</td>
      <td>AHS confirms E. coli outbreak in Calgary area</td>
      <td>26</td>
      <td>http://www.cbc.ca/news/canada/calgary/ecoli-ou...</td>
      <td>8</td>
      <td>http://www.cbc.ca/news/canada/calgary/ecoli-ou...</td>
      <td>cbc.ca</td>
      <td>Shit, this is serious. Just to be safe, I'm go...</td>
      <td>-0.7717</td>
      <td>0.092</td>
      <td>0.305</td>
      <td>0.603</td>
    </tr>
    <tr>
      <th>5968</th>
      <td>e. coli</td>
      <td>4423l0</td>
      <td>all</td>
      <td>1.454565e+09</td>
      <td>AHS confirms E. coli outbreak in Calgary area</td>
      <td>26</td>
      <td>http://www.cbc.ca/news/canada/calgary/ecoli-ou...</td>
      <td>8</td>
      <td>http://www.cbc.ca/news/canada/calgary/ecoli-ou...</td>
      <td>cbc.ca</td>
      <td>You can get e.coli from many different things,...</td>
      <td>-0.7579</td>
      <td>0.056</td>
      <td>0.101</td>
      <td>0.842</td>
    </tr>
    <tr>
      <th>5969</th>
      <td>e. coli</td>
      <td>7gu7q3</td>
      <td>all</td>
      <td>1.512153e+09</td>
      <td>I Think This Is The First Time All Four Of My ...</td>
      <td>27</td>
      <td>https://imgur.com/a/crjru</td>
      <td>11</td>
      <td>https://imgur.com/a/crjru</td>
      <td>imgur.com</td>
      <td>Also, kindly ignore the spring customs. I'll b...</td>
      <td>0.6908</td>
      <td>0.212</td>
      <td>0.065</td>
      <td>0.724</td>
    </tr>
    <tr>
      <th>5970</th>
      <td>e. coli</td>
      <td>7gu7q3</td>
      <td>all</td>
      <td>1.512153e+09</td>
      <td>I Think This Is The First Time All Four Of My ...</td>
      <td>27</td>
      <td>https://imgur.com/a/crjru</td>
      <td>11</td>
      <td>https://imgur.com/a/crjru</td>
      <td>imgur.com</td>
      <td>^(Hi, I'm a bot for linking direct images of a...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5971</th>
      <td>e. coli</td>
      <td>7gu7q3</td>
      <td>all</td>
      <td>1.512153e+09</td>
      <td>I Think This Is The First Time All Four Of My ...</td>
      <td>27</td>
      <td>https://imgur.com/a/crjru</td>
      <td>11</td>
      <td>https://imgur.com/a/crjru</td>
      <td>imgur.com</td>
      <td>Alright so I love it when my pet "picks a food...</td>
      <td>-0.7982</td>
      <td>0.163</td>
      <td>0.274</td>
      <td>0.562</td>
    </tr>
    <tr>
      <th>5972</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>Really informative man! I didn't believe I'd s...</td>
      <td>0.5487</td>
      <td>0.116</td>
      <td>0.000</td>
      <td>0.884</td>
    </tr>
    <tr>
      <th>5973</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>This is a great summary. \n\nBut I hope I'm no...</td>
      <td>0.8720</td>
      <td>0.268</td>
      <td>0.000</td>
      <td>0.732</td>
    </tr>
    <tr>
      <th>5974</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>Resistance profile for the sample in question:...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5975</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>Great job with the takeaway message bit. Anyon...</td>
      <td>0.6662</td>
      <td>0.190</td>
      <td>0.000</td>
      <td>0.810</td>
    </tr>
    <tr>
      <th>5976</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>I've been thinking. If a resistance gene is lo...</td>
      <td>0.4329</td>
      <td>0.049</td>
      <td>0.000</td>
      <td>0.951</td>
    </tr>
    <tr>
      <th>5977</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>I'm surprised more people haven't seen this! V...</td>
      <td>0.8682</td>
      <td>0.429</td>
      <td>0.000</td>
      <td>0.571</td>
    </tr>
    <tr>
      <th>5978</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>deleted  ^^^^^^^^^^^^^^^^0.7543  [^^^What ^^^i...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5979</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>deep shit</td>
      <td>-0.5574</td>
      <td>0.000</td>
      <td>0.783</td>
      <td>0.217</td>
    </tr>
    <tr>
      <th>5980</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>How do you treat/manage patients that have inf...</td>
      <td>0.3612</td>
      <td>0.152</td>
      <td>0.000</td>
      <td>0.848</td>
    </tr>
    <tr>
      <th>5981</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>To me it seems crazy that live stock are being...</td>
      <td>-0.8655</td>
      <td>0.000</td>
      <td>0.136</td>
      <td>0.864</td>
    </tr>
    <tr>
      <th>5982</th>
      <td>e. coli</td>
      <td>4lz7yf</td>
      <td>all</td>
      <td>1.464780e+09</td>
      <td>Colistin-resistant E. coli in the United State...</td>
      <td>199</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>31</td>
      <td>https://www.reddit.com/r/medicine/comments/4lz...</td>
      <td>self.medicine</td>
      <td>Hey! I've thought about this as well.\n You co...</td>
      <td>0.7177</td>
      <td>0.157</td>
      <td>0.084</td>
      <td>0.759</td>
    </tr>
    <tr>
      <th>5983</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>Read this as 'Check your panties!' lol</td>
      <td>0.4753</td>
      <td>0.340</td>
      <td>0.000</td>
      <td>0.660</td>
    </tr>
    <tr>
      <th>5984</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>These factories and plants need to get their s...</td>
      <td>-0.5574</td>
      <td>0.000</td>
      <td>0.286</td>
      <td>0.714</td>
    </tr>
    <tr>
      <th>5985</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>I am officially eating nothing but sushi and r...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5986</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>Thank you for sharing! I had one of these than...</td>
      <td>0.8122</td>
      <td>0.456</td>
      <td>0.000</td>
      <td>0.544</td>
    </tr>
    <tr>
      <th>5987</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>I'm getting a 404. Is it because I'm on a mobi...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5988</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>I'm not entirely worried about this to be quit...</td>
      <td>-0.0521</td>
      <td>0.077</td>
      <td>0.080</td>
      <td>0.842</td>
    </tr>
    <tr>
      <th>5989</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>Are you fucking kidding me.\n\nI literally jus...</td>
      <td>-0.7787</td>
      <td>0.051</td>
      <td>0.256</td>
      <td>0.693</td>
    </tr>
    <tr>
      <th>5990</th>
      <td>e. coli</td>
      <td>4lxo2a</td>
      <td>all</td>
      <td>1.464759e+09</td>
      <td>Check your pantries! General mills recalls flo...</td>
      <td>22</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>15</td>
      <td>http://www.foodsafetynews.com/2016/05/general-...</td>
      <td>foodsafetynews.com</td>
      <td>I also read this as "check your panties" but I...</td>
      <td>0.4012</td>
      <td>0.154</td>
      <td>0.116</td>
      <td>0.730</td>
    </tr>
  </tbody>
</table>
<p>5991 rows × 15 columns</p>
</div>




```python
grouped_df3 = grouped_df3.groupby(['Created Date','Submission ID'])
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
      <th>1.160777e+09</th>
      <th>lzjm</th>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1.214365e+09</th>
      <th>6osmp</th>
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
      <th>1.214373e+09</th>
      <th>6otb6</th>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
    </tr>
    <tr>
      <th>1.218673e+09</th>
      <th>6w5w3</th>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1.220546e+09</th>
      <th>6zksg</th>
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
      <th>1.160777e+09</th>
      <th>lzjm</th>
      <td>0.037929</td>
    </tr>
    <tr>
      <th>1.214365e+09</th>
      <th>6osmp</th>
      <td>0.077967</td>
    </tr>
    <tr>
      <th>1.214373e+09</th>
      <th>6otb6</th>
      <td>0.082729</td>
    </tr>
    <tr>
      <th>1.218673e+09</th>
      <th>6w5w3</th>
      <td>-0.077825</td>
    </tr>
    <tr>
      <th>1.220546e+09</th>
      <th>6zksg</th>
      <td>-0.220200</td>
    </tr>
    <tr>
      <th>1.243390e+09</th>
      <th>8ndug</th>
      <td>-0.159687</td>
    </tr>
    <tr>
      <th>1.249381e+09</th>
      <th>9791p</th>
      <td>-0.181600</td>
    </tr>
    <tr>
      <th>1.254658e+09</th>
      <th>9qmd0</th>
      <td>0.118015</td>
    </tr>
    <tr>
      <th>1.254694e+09</th>
      <th>9qpfc</th>
      <td>-0.000739</td>
    </tr>
    <tr>
      <th>1.255954e+09</th>
      <th>9vdza</th>
      <td>0.354508</td>
    </tr>
    <tr>
      <th>1.258148e+09</th>
      <th>a40eo</th>
      <td>-0.247700</td>
    </tr>
    <tr>
      <th>1.261965e+09</th>
      <th>aixym</th>
      <td>0.034849</td>
    </tr>
    <tr>
      <th>1.262310e+09</th>
      <th>akbaa</th>
      <td>0.080117</td>
    </tr>
    <tr>
      <th>1.263184e+09</th>
      <th>anww0</th>
      <td>0.006510</td>
    </tr>
    <tr>
      <th>1.263190e+09</th>
      <th>anxt4</th>
      <td>-0.085055</td>
    </tr>
    <tr>
      <th>1.263907e+09</th>
      <th>arb4r</th>
      <td>0.046153</td>
    </tr>
    <tr>
      <th>1.266574e+09</th>
      <th>b3ukz</th>
      <td>0.185800</td>
    </tr>
    <tr>
      <th>1.268761e+09</th>
      <th>bdz0w</th>
      <td>0.134118</td>
    </tr>
    <tr>
      <th>1.272778e+09</th>
      <th>byute</th>
      <td>0.210550</td>
    </tr>
    <tr>
      <th>1.276069e+09</th>
      <th>ccxge</th>
      <td>0.117794</td>
    </tr>
    <tr>
      <th>1.278539e+09</th>
      <th>cmvcm</th>
      <td>-0.530244</td>
    </tr>
    <tr>
      <th>1.283461e+09</th>
      <th>d8nux</th>
      <td>-0.155943</td>
    </tr>
    <tr>
      <th>1.291904e+09</th>
      <th>eiry5</th>
      <td>0.403100</td>
    </tr>
    <tr>
      <th>1.295354e+09</th>
      <th>f48f3</th>
      <td>0.090230</td>
    </tr>
    <tr>
      <th>1.295358e+09</th>
      <th>f49cw</th>
      <td>0.046455</td>
    </tr>
    <tr>
      <th>1.295645e+09</th>
      <th>f6geu</th>
      <td>0.110923</td>
    </tr>
    <tr>
      <th>1.300394e+09</th>
      <th>g5rtu</th>
      <td>0.392329</td>
    </tr>
    <tr>
      <th>1.300677e+09</th>
      <th>g7pgj</th>
      <td>-0.026109</td>
    </tr>
    <tr>
      <th>1.305861e+09</th>
      <th>hf9q1</th>
      <td>0.055093</td>
    </tr>
    <tr>
      <th>1.306648e+09</th>
      <th>hmggp</th>
      <td>-0.160600</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.515119e+09</th>
      <th>7o4wa4</th>
      <td>-0.200950</td>
    </tr>
    <tr>
      <th>1.515123e+09</th>
      <th>7o5enh</th>
      <td>0.301389</td>
    </tr>
    <tr>
      <th>1.515135e+09</th>
      <th>7o6k8g</th>
      <td>0.028617</td>
    </tr>
    <tr>
      <th>1.515188e+09</th>
      <th>7ob7rs</th>
      <td>0.011637</td>
    </tr>
    <tr>
      <th>1.515197e+09</th>
      <th>7oc2uq</th>
      <td>-0.079533</td>
    </tr>
    <tr>
      <th>1.515245e+09</th>
      <th>7ohc26</th>
      <td>0.726900</td>
    </tr>
    <tr>
      <th>1.515271e+09</th>
      <th>7oj1oa</th>
      <td>-0.091067</td>
    </tr>
    <tr>
      <th>1.515272e+09</th>
      <th>7oj3bo</th>
      <td>0.650567</td>
    </tr>
    <tr>
      <th>1.515279e+09</th>
      <th>7ojksz</th>
      <td>-0.080380</td>
    </tr>
    <tr>
      <th>1.515644e+09</th>
      <th>7piafj</th>
      <td>0.217900</td>
    </tr>
    <tr>
      <th>1.515731e+09</th>
      <th>7pr0eh</th>
      <td>0.250000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.516042e+09</th>
      <th>7qiz1r</th>
      <td>0.100039</td>
    </tr>
    <tr>
      <th>7qiz3n</th>
      <td>0.217825</td>
    </tr>
    <tr>
      <th>1.516065e+09</th>
      <th>7ql374</th>
      <td>-0.012300</td>
    </tr>
    <tr>
      <th>1.517511e+09</th>
      <th>7uhxit</th>
      <td>-0.110812</td>
    </tr>
    <tr>
      <th>1.517878e+09</th>
      <th>7vg1rk</th>
      <td>0.299809</td>
    </tr>
    <tr>
      <th>1.518031e+09</th>
      <th>7vvf4n</th>
      <td>-0.639025</td>
    </tr>
    <tr>
      <th>1.518328e+09</th>
      <th>7wohs5</th>
      <td>0.177424</td>
    </tr>
    <tr>
      <th>1.518645e+09</th>
      <th>7xi3vx</th>
      <td>0.273913</td>
    </tr>
    <tr>
      <th>1.519882e+09</th>
      <th>80ztql</th>
      <td>0.226867</td>
    </tr>
    <tr>
      <th>1.519886e+09</th>
      <th>810c2x</th>
      <td>0.540733</td>
    </tr>
    <tr>
      <th>1.520210e+09</th>
      <th>81yn45</th>
      <td>0.092967</td>
    </tr>
    <tr>
      <th>1.520342e+09</th>
      <th>82cl60</th>
      <td>0.045062</td>
    </tr>
    <tr>
      <th>1.520737e+09</th>
      <th>83h6t0</th>
      <td>-0.528400</td>
    </tr>
    <tr>
      <th>1.521250e+09</th>
      <th>84x64c</th>
      <td>-0.236575</td>
    </tr>
    <tr>
      <th>1.521439e+09</th>
      <th>85ekda</th>
      <td>-0.003486</td>
    </tr>
    <tr>
      <th>1.521799e+09</th>
      <th>86h538</th>
      <td>0.244600</td>
    </tr>
    <tr>
      <th>1.521882e+09</th>
      <th>86povb</th>
      <td>0.216574</td>
    </tr>
    <tr>
      <th>1.521930e+09</th>
      <th>86tc4m</th>
      <td>0.315667</td>
    </tr>
    <tr>
      <th>1.521934e+09</th>
      <th>86tp96</th>
      <td>-0.076838</td>
    </tr>
  </tbody>
</table>
<p>446 rows × 1 columns</p>
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
      <th>Compound Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.160777e+09</td>
      <td>lzjm</td>
      <td>0.037929</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.214365e+09</td>
      <td>6osmp</td>
      <td>0.077967</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.214373e+09</td>
      <td>6otb6</td>
      <td>0.082729</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.218673e+09</td>
      <td>6w5w3</td>
      <td>-0.077825</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.220546e+09</td>
      <td>6zksg</td>
      <td>-0.220200</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df3, fit_reg=False, palette="Paired")

#plt.title("E. Coli Comment Sentiments on Reddit")

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

plt.savefig("E_Coli_Sentiments.png", dpi=350)

plt.show()
```


![png](output_56_0.png)



```python
grouped_df4 = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "food allergy",:]
grouped_df4 = grouped_df4.reset_index()
del grouped_df4['index']
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
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am deathly allergic to peanuts and all nuts ...</td>
      <td>-0.7717</td>
      <td>0.037</td>
      <td>0.151</td>
      <td>0.812</td>
    </tr>
    <tr>
      <th>1</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>As a parent of a child with a peanut allergy I...</td>
      <td>0.7391</td>
      <td>0.150</td>
      <td>0.000</td>
      <td>0.850</td>
    </tr>
    <tr>
      <th>2</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bees, so if you guys could get...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.136</td>
      <td>0.864</td>
    </tr>
    <tr>
      <th>3</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to many different types of food a...</td>
      <td>-0.8625</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
    </tr>
    <tr>
      <th>4</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Alright. I am confident that this will get bur...</td>
      <td>-0.9365</td>
      <td>0.078</td>
      <td>0.109</td>
      <td>0.813</td>
    </tr>
    <tr>
      <th>5</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>First they came for the peanuts, and I was sil...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>THIS IS AMERICA!! How dare someone promote per...</td>
      <td>0.5386</td>
      <td>0.303</td>
      <td>0.000</td>
      <td>0.697</td>
    </tr>
    <tr>
      <th>7</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>The real question is:  How many people in this...</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.185</td>
      <td>0.815</td>
    </tr>
    <tr>
      <th>8</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I knew a girl in middle school. She couldn't b...</td>
      <td>-0.0108</td>
      <td>0.074</td>
      <td>0.066</td>
      <td>0.859</td>
    </tr>
    <tr>
      <th>9</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm quietly munching on peanuts as I read this...</td>
      <td>0.2975</td>
      <td>0.136</td>
      <td>0.000</td>
      <td>0.864</td>
    </tr>
    <tr>
      <th>10</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>my kid's class banned both nut and egg product...</td>
      <td>-0.8357</td>
      <td>0.049</td>
      <td>0.228</td>
      <td>0.723</td>
    </tr>
    <tr>
      <th>11</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I've had a "life-threatening peanut allergy" s...</td>
      <td>-0.5286</td>
      <td>0.084</td>
      <td>0.085</td>
      <td>0.831</td>
    </tr>
    <tr>
      <th>12</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>So precisely what is the argument against bann...</td>
      <td>0.4660</td>
      <td>0.097</td>
      <td>0.044</td>
      <td>0.859</td>
    </tr>
    <tr>
      <th>13</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I think these comments perfectly sum up the ar...</td>
      <td>0.4615</td>
      <td>0.062</td>
      <td>0.062</td>
      <td>0.876</td>
    </tr>
    <tr>
      <th>14</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Our oldest son is highly allergic to the uncoo...</td>
      <td>0.5273</td>
      <td>0.089</td>
      <td>0.048</td>
      <td>0.863</td>
    </tr>
    <tr>
      <th>15</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm deathly allergic to wheat dust, but I have...</td>
      <td>-0.1531</td>
      <td>0.000</td>
      <td>0.065</td>
      <td>0.935</td>
    </tr>
    <tr>
      <th>16</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>No kidding.  I had no idea people were even su...</td>
      <td>-0.7717</td>
      <td>0.051</td>
      <td>0.331</td>
      <td>0.618</td>
    </tr>
    <tr>
      <th>17</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Unfortunately we've already determined as a po...</td>
      <td>-0.9517</td>
      <td>0.053</td>
      <td>0.225</td>
      <td>0.722</td>
    </tr>
    <tr>
      <th>18</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>peanuts and peanut butter are kind of a staple...</td>
      <td>-0.2732</td>
      <td>0.040</td>
      <td>0.081</td>
      <td>0.879</td>
    </tr>
    <tr>
      <th>19</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>My little brother is deadly allergic to peanut...</td>
      <td>-0.9784</td>
      <td>0.029</td>
      <td>0.129</td>
      <td>0.842</td>
    </tr>
    <tr>
      <th>20</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I am inclined to agree with the responsibility...</td>
      <td>-0.0258</td>
      <td>0.054</td>
      <td>0.078</td>
      <td>0.868</td>
    </tr>
    <tr>
      <th>21</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm highly allergic to peanuts, but it's ridic...</td>
      <td>-0.8764</td>
      <td>0.033</td>
      <td>0.184</td>
      <td>0.783</td>
    </tr>
    <tr>
      <th>22</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>Peanut allergies kill more people than terrori...</td>
      <td>-0.8948</td>
      <td>0.000</td>
      <td>0.574</td>
      <td>0.426</td>
    </tr>
    <tr>
      <th>23</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I know this is going to turn into a lot of per...</td>
      <td>-0.4871</td>
      <td>0.078</td>
      <td>0.099</td>
      <td>0.823</td>
    </tr>
    <tr>
      <th>24</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>4-6 percent of kids dictate how things go for ...</td>
      <td>-0.9765</td>
      <td>0.104</td>
      <td>0.253</td>
      <td>0.643</td>
    </tr>
    <tr>
      <th>25</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>How about a ´allergic people´-free zone!?\n</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>If your or your child is so allergic that mere...</td>
      <td>-0.4882</td>
      <td>0.123</td>
      <td>0.172</td>
      <td>0.705</td>
    </tr>
    <tr>
      <th>27</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>For the record: I live in Germany and have NEV...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.099</td>
      <td>0.901</td>
    </tr>
    <tr>
      <th>28</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>I'm allergic to bullshit so TVs in businesses ...</td>
      <td>-0.7184</td>
      <td>0.000</td>
      <td>0.300</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>29</th>
      <td>food allergy</td>
      <td>e6dlg</td>
      <td>all</td>
      <td>1.289859e+09</td>
      <td>Allergy Expert Says Peanut Bans Are An Overrea...</td>
      <td>930</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>986</td>
      <td>http://www.npr.org/blogs/health/2010/11/12/131...</td>
      <td>npr.org</td>
      <td>here is what i want to know...where are all th...</td>
      <td>-0.6597</td>
      <td>0.051</td>
      <td>0.113</td>
      <td>0.835</td>
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
      <th>5482</th>
      <td>food allergy</td>
      <td>3ducbv</td>
      <td>all</td>
      <td>1.437349e+09</td>
      <td>Non-food allergy question.</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>self.Disneyland</td>
      <td>If you get the one day ticket they will need a...</td>
      <td>0.8360</td>
      <td>0.241</td>
      <td>0.000</td>
      <td>0.759</td>
    </tr>
    <tr>
      <th>5483</th>
      <td>food allergy</td>
      <td>3ducbv</td>
      <td>all</td>
      <td>1.437349e+09</td>
      <td>Non-food allergy question.</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>self.Disneyland</td>
      <td>I seem to recall that the hand stamps are no l...</td>
      <td>0.2500</td>
      <td>0.131</td>
      <td>0.090</td>
      <td>0.779</td>
    </tr>
    <tr>
      <th>5484</th>
      <td>food allergy</td>
      <td>3ducbv</td>
      <td>all</td>
      <td>1.437349e+09</td>
      <td>Non-food allergy question.</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>self.Disneyland</td>
      <td>Calling guest services is the better option, b...</td>
      <td>0.6858</td>
      <td>0.172</td>
      <td>0.087</td>
      <td>0.741</td>
    </tr>
    <tr>
      <th>5485</th>
      <td>food allergy</td>
      <td>3ducbv</td>
      <td>all</td>
      <td>1.437349e+09</td>
      <td>Non-food allergy question.</td>
      <td>8</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/Disneyland/comments/3...</td>
      <td>self.Disneyland</td>
      <td>They've changed the type of ink they use for t...</td>
      <td>0.7251</td>
      <td>0.271</td>
      <td>0.160</td>
      <td>0.569</td>
    </tr>
    <tr>
      <th>5486</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>Allergies are basically when your immune syste...</td>
      <td>-0.0859</td>
      <td>0.060</td>
      <td>0.033</td>
      <td>0.907</td>
    </tr>
    <tr>
      <th>5487</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>As allergies are mediated by the production of...</td>
      <td>0.7845</td>
      <td>0.139</td>
      <td>0.031</td>
      <td>0.830</td>
    </tr>
    <tr>
      <th>5488</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>I'd question whether there's an actual disease...</td>
      <td>-0.9612</td>
      <td>0.039</td>
      <td>0.167</td>
      <td>0.793</td>
    </tr>
    <tr>
      <th>5489</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>Partial because we understand them better and ...</td>
      <td>-0.6124</td>
      <td>0.095</td>
      <td>0.148</td>
      <td>0.757</td>
    </tr>
    <tr>
      <th>5490</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>Are they actually more frequent or did people ...</td>
      <td>-0.5994</td>
      <td>0.000</td>
      <td>0.245</td>
      <td>0.755</td>
    </tr>
    <tr>
      <th>5491</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>There si this hygiene hypothesis, that explain...</td>
      <td>0.1275</td>
      <td>0.057</td>
      <td>0.061</td>
      <td>0.882</td>
    </tr>
    <tr>
      <th>5492</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>I'd question the premise of the question. We'v...</td>
      <td>0.5182</td>
      <td>0.061</td>
      <td>0.000</td>
      <td>0.939</td>
    </tr>
    <tr>
      <th>5493</th>
      <td>food allergy</td>
      <td>7p2w69</td>
      <td>all</td>
      <td>1.515484e+09</td>
      <td>Why are food allergies more frequent now than ...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>9</td>
      <td>https://www.reddit.com/r/AskScienceDiscussion/...</td>
      <td>self.AskScienceDiscussion</td>
      <td>One group I know studies chemicals in food add...</td>
      <td>-0.3818</td>
      <td>0.054</td>
      <td>0.085</td>
      <td>0.861</td>
    </tr>
    <tr>
      <th>5494</th>
      <td>food allergy</td>
      <td>2encao</td>
      <td>all</td>
      <td>1.409105e+09</td>
      <td>Scientists may have discovered how to stop you...</td>
      <td>10</td>
      <td>http://mic.com/articles/97294/scientists-may-h...</td>
      <td>3</td>
      <td>http://mic.com/articles/97294/scientists-may-h...</td>
      <td>mic.com</td>
      <td>Ref:\n\nCommensal bacteria protect against foo...</td>
      <td>0.3818</td>
      <td>0.245</td>
      <td>0.000</td>
      <td>0.755</td>
    </tr>
    <tr>
      <th>5495</th>
      <td>food allergy</td>
      <td>2encao</td>
      <td>all</td>
      <td>1.409105e+09</td>
      <td>Scientists may have discovered how to stop you...</td>
      <td>10</td>
      <td>http://mic.com/articles/97294/scientists-may-h...</td>
      <td>3</td>
      <td>http://mic.com/articles/97294/scientists-may-h...</td>
      <td>mic.com</td>
      <td>Well if this pans out it is certainly the good...</td>
      <td>0.7506</td>
      <td>0.363</td>
      <td>0.000</td>
      <td>0.637</td>
    </tr>
    <tr>
      <th>5496</th>
      <td>food allergy</td>
      <td>2encao</td>
      <td>all</td>
      <td>1.409105e+09</td>
      <td>Scientists may have discovered how to stop you...</td>
      <td>10</td>
      <td>http://mic.com/articles/97294/scientists-may-h...</td>
      <td>3</td>
      <td>http://mic.com/articles/97294/scientists-may-h...</td>
      <td>mic.com</td>
      <td>Awww shit really... no seriously... I have TON...</td>
      <td>-0.8945</td>
      <td>0.000</td>
      <td>0.251</td>
      <td>0.749</td>
    </tr>
    <tr>
      <th>5497</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Gluten would pretty much end me.  Everything i...</td>
      <td>0.7845</td>
      <td>0.434</td>
      <td>0.000</td>
      <td>0.566</td>
    </tr>
    <tr>
      <th>5498</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>water would suck</td>
      <td>-0.4404</td>
      <td>0.000</td>
      <td>0.592</td>
      <td>0.408</td>
    </tr>
    <tr>
      <th>5499</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Garlic and onion. They are in almost every sav...</td>
      <td>0.6834</td>
      <td>0.209</td>
      <td>0.111</td>
      <td>0.680</td>
    </tr>
    <tr>
      <th>5500</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>This is a bit of a touchy subject for me. I ha...</td>
      <td>0.8652</td>
      <td>0.197</td>
      <td>0.076</td>
      <td>0.727</td>
    </tr>
    <tr>
      <th>5501</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Jesus, isn't this Reddit? \n\nBACON!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5502</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Garlic, kale, or mushrooms.\n\nI can't have gl...</td>
      <td>0.7467</td>
      <td>0.175</td>
      <td>0.057</td>
      <td>0.768</td>
    </tr>
    <tr>
      <th>5503</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Cheese or chocolate.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5504</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Potatoes</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5505</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Meat, specifically cow.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5506</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Lactose intolerant. I'm addicted to cheese.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>5507</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Being allergic to water. \rI drink 2 litres a ...</td>
      <td>-0.2960</td>
      <td>0.000</td>
      <td>0.081</td>
      <td>0.919</td>
    </tr>
    <tr>
      <th>5508</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Gluten would be bad, but there are lots of wor...</td>
      <td>-0.8687</td>
      <td>0.000</td>
      <td>0.214</td>
      <td>0.786</td>
    </tr>
    <tr>
      <th>5509</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Tomatoes or rice. God, I'd be so depressed.</td>
      <td>-0.4838</td>
      <td>0.170</td>
      <td>0.344</td>
      <td>0.486</td>
    </tr>
    <tr>
      <th>5510</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Coffee. It's not even about the caffeine, alth...</td>
      <td>0.6172</td>
      <td>0.200</td>
      <td>0.065</td>
      <td>0.734</td>
    </tr>
    <tr>
      <th>5511</th>
      <td>food allergy</td>
      <td>1757i0</td>
      <td>all</td>
      <td>1.359003e+09</td>
      <td>What would be the most personally life shatter...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>19</td>
      <td>https://www.reddit.com/r/AskReddit/comments/17...</td>
      <td>self.AskReddit</td>
      <td>Beer.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
  </tbody>
</table>
<p>5512 rows × 15 columns</p>
</div>




```python
grouped_df4 = grouped_df4.groupby(['Created Date','Submission ID'])
```


```python
grouped_df4.count().head()
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
      <th>1.193635e+09</th>
      <th>5zb67</th>
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
    <tr>
      <th>1.197338e+09</th>
      <th>62moz</th>
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
      <th>1.221520e+09</th>
      <th>71jjj</th>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1.228942e+09</th>
      <th>7ik85</th>
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
    <tr>
      <th>1.231780e+09</th>
      <th>7p2vw</th>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_df4 = pd.DataFrame(grouped_df4["Compound Score"].mean())
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
      <th>1.193635e+09</th>
      <th>5zb67</th>
      <td>0.434400</td>
    </tr>
    <tr>
      <th>1.197338e+09</th>
      <th>62moz</th>
      <td>-0.425750</td>
    </tr>
    <tr>
      <th>1.221520e+09</th>
      <th>71jjj</th>
      <td>-0.660780</td>
    </tr>
    <tr>
      <th>1.228942e+09</th>
      <th>7ik85</th>
      <td>-0.836000</td>
    </tr>
    <tr>
      <th>1.231780e+09</th>
      <th>7p2vw</th>
      <td>-0.042475</td>
    </tr>
    <tr>
      <th>1.233696e+09</th>
      <th>7uid4</th>
      <td>-0.565667</td>
    </tr>
    <tr>
      <th>1.240385e+09</th>
      <th>8ecso</th>
      <td>-0.185323</td>
    </tr>
    <tr>
      <th>1.248126e+09</th>
      <th>92tbs</th>
      <td>-0.982800</td>
    </tr>
    <tr>
      <th>1.253922e+09</th>
      <th>9o20b</th>
      <td>-0.073220</td>
    </tr>
    <tr>
      <th>1.268806e+09</th>
      <th>be900</th>
      <td>-0.127093</td>
    </tr>
    <tr>
      <th>1.272691e+09</th>
      <th>byig6</th>
      <td>0.019683</td>
    </tr>
    <tr>
      <th>1.273695e+09</th>
      <th>c32ey</th>
      <td>0.034136</td>
    </tr>
    <tr>
      <th>1.273783e+09</th>
      <th>c3kf0</th>
      <td>-0.143255</td>
    </tr>
    <tr>
      <th>1.273837e+09</th>
      <th>c3w0b</th>
      <td>0.456050</td>
    </tr>
    <tr>
      <th>1.274334e+09</th>
      <th>c62o2</th>
      <td>-0.353558</td>
    </tr>
    <tr>
      <th>1.289859e+09</th>
      <th>e6dlg</th>
      <td>-0.213017</td>
    </tr>
    <tr>
      <th>1.302875e+09</th>
      <th>gqjek</th>
      <td>0.107973</td>
    </tr>
    <tr>
      <th>1.304809e+09</th>
      <th>h63lv</th>
      <td>-0.161908</td>
    </tr>
    <tr>
      <th>1.305075e+09</th>
      <th>h88ga</th>
      <td>-0.164260</td>
    </tr>
    <tr>
      <th>1.305686e+09</th>
      <th>hdkbo</th>
      <td>-0.689950</td>
    </tr>
    <tr>
      <th>1.306365e+09</th>
      <th>hjtu0</th>
      <td>-0.028723</td>
    </tr>
    <tr>
      <th>1.311496e+09</th>
      <th>iy0xl</th>
      <td>0.086767</td>
    </tr>
    <tr>
      <th>1.313029e+09</th>
      <th>jetab</th>
      <td>0.538310</td>
    </tr>
    <tr>
      <th>1.317956e+09</th>
      <th>l3a0b</th>
      <td>-0.731933</td>
    </tr>
    <tr>
      <th>1.318493e+09</th>
      <th>la735</th>
      <td>-0.304333</td>
    </tr>
    <tr>
      <th>1.320549e+09</th>
      <th>m1mmp</th>
      <td>0.121663</td>
    </tr>
    <tr>
      <th>1.323000e+09</th>
      <th>mzelv</th>
      <td>0.936183</td>
    </tr>
    <tr>
      <th>1.324773e+09</th>
      <th>np7xa</th>
      <td>0.166686</td>
    </tr>
    <tr>
      <th>1.327463e+09</th>
      <th>ouuq1</th>
      <td>-0.160725</td>
    </tr>
    <tr>
      <th>1.327560e+09</th>
      <th>owoth</th>
      <td>-0.190707</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.515939e+09</th>
      <th>7qa9v4</th>
      <td>0.187567</td>
    </tr>
    <tr>
      <th>1.516105e+09</th>
      <th>7qprnr</th>
      <td>-0.088200</td>
    </tr>
    <tr>
      <th>1.516593e+09</th>
      <th>7rzzpk</th>
      <td>0.067371</td>
    </tr>
    <tr>
      <th>1.516885e+09</th>
      <th>7stt7h</th>
      <td>0.811943</td>
    </tr>
    <tr>
      <th>1.516957e+09</th>
      <th>7t0zuw</th>
      <td>0.239557</td>
    </tr>
    <tr>
      <th>1.517038e+09</th>
      <th>7t8la0</th>
      <td>-0.287686</td>
    </tr>
    <tr>
      <th>1.517045e+09</th>
      <th>7t9c1l</th>
      <td>-0.347133</td>
    </tr>
    <tr>
      <th>1.517280e+09</th>
      <th>7tuij1</th>
      <td>-0.053642</td>
    </tr>
    <tr>
      <th>1.517454e+09</th>
      <th>7ucaut</th>
      <td>0.424486</td>
    </tr>
    <tr>
      <th>1.517610e+09</th>
      <th>7urlbr</th>
      <td>-0.084750</td>
    </tr>
    <tr>
      <th>1.517912e+09</th>
      <th>7vk1lp</th>
      <td>-0.056200</td>
    </tr>
    <tr>
      <th>1.518314e+09</th>
      <th>7wmzj9</th>
      <td>0.170083</td>
    </tr>
    <tr>
      <th>1.518469e+09</th>
      <th>7x0ktd</th>
      <td>0.037537</td>
    </tr>
    <tr>
      <th>1.518483e+09</th>
      <th>7x22vl</th>
      <td>-0.570800</td>
    </tr>
    <tr>
      <th>1.518500e+09</th>
      <th>7x47le</th>
      <td>0.230950</td>
    </tr>
    <tr>
      <th>1.518521e+09</th>
      <th>7x6h51</th>
      <td>0.079950</td>
    </tr>
    <tr>
      <th>1.518582e+09</th>
      <th>7xcbtm</th>
      <td>-0.143900</td>
    </tr>
    <tr>
      <th>1.518680e+09</th>
      <th>7xmdrg</th>
      <td>-0.579900</td>
    </tr>
    <tr>
      <th>1.518849e+09</th>
      <th>7y2ggm</th>
      <td>-0.113900</td>
    </tr>
    <tr>
      <th>1.519278e+09</th>
      <th>7z9a55</th>
      <td>-0.141067</td>
    </tr>
    <tr>
      <th>1.519348e+09</th>
      <th>7zggwf</th>
      <td>-0.360582</td>
    </tr>
    <tr>
      <th>1.520132e+09</th>
      <th>81s2jk</th>
      <td>-0.191375</td>
    </tr>
    <tr>
      <th>1.520198e+09</th>
      <th>81xlsy</th>
      <td>-0.083678</td>
    </tr>
    <tr>
      <th>1.520469e+09</th>
      <th>82pjbx</th>
      <td>0.443150</td>
    </tr>
    <tr>
      <th>1.520564e+09</th>
      <th>82zzfe</th>
      <td>0.440580</td>
    </tr>
    <tr>
      <th>1.520785e+09</th>
      <th>83ljdq</th>
      <td>-0.343817</td>
    </tr>
    <tr>
      <th>1.520831e+09</th>
      <th>83plm7</th>
      <td>0.138611</td>
    </tr>
    <tr>
      <th>1.520889e+09</th>
      <th>83utfl</th>
      <td>0.025900</td>
    </tr>
    <tr>
      <th>1.521335e+09</th>
      <th>8550ou</th>
      <td>-0.111250</td>
    </tr>
    <tr>
      <th>1.521591e+09</th>
      <th>85tu76</th>
      <td>-0.406861</td>
    </tr>
  </tbody>
</table>
<p>452 rows × 1 columns</p>
</div>




```python
grouped_df4 = grouped_df4.reset_index()
grouped_df4.head()
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
      <td>1.193635e+09</td>
      <td>5zb67</td>
      <td>0.434400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.197338e+09</td>
      <td>62moz</td>
      <td>-0.425750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.221520e+09</td>
      <td>71jjj</td>
      <td>-0.660780</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.228942e+09</td>
      <td>7ik85</td>
      <td>-0.836000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.231780e+09</td>
      <td>7p2vw</td>
      <td>-0.042475</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df4, fit_reg=False, palette="Paired")

#plt.title("Food Allergy Comment Sentiments on Reddit")

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

plt.savefig("Food_Allergy_Sentiments.png", dpi=350)

plt.show()
```


![png](output_62_0.png)



```python
grouped_df5 = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "salmonella",:]
grouped_df5 = grouped_df5.reset_index()
del grouped_df5['index']
grouped_df5
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
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>He's comparing apples to oranges when he compa...</td>
      <td>-0.9583</td>
      <td>0.062</td>
      <td>0.113</td>
      <td>0.825</td>
    </tr>
    <tr>
      <th>1</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>I like to think that we have rather tough regu...</td>
      <td>0.5574</td>
      <td>0.063</td>
      <td>0.019</td>
      <td>0.918</td>
    </tr>
    <tr>
      <th>2</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>TIL only housewives cook chicken</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>And yet if the USDA regulates unpasteurized mi...</td>
      <td>-0.7003</td>
      <td>0.034</td>
      <td>0.184</td>
      <td>0.781</td>
    </tr>
    <tr>
      <th>4</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>May I insert a brief rant about food thermomet...</td>
      <td>0.9768</td>
      <td>0.177</td>
      <td>0.037</td>
      <td>0.786</td>
    </tr>
    <tr>
      <th>5</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>so imcredibly sexist!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>Man, that was fucked up. I don't see why the U...</td>
      <td>-0.7845</td>
      <td>0.000</td>
      <td>0.210</td>
      <td>0.790</td>
    </tr>
    <tr>
      <th>7</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>Smart enough to know to cook chicken properly,...</td>
      <td>-0.1531</td>
      <td>0.113</td>
      <td>0.137</td>
      <td>0.750</td>
    </tr>
    <tr>
      <th>8</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>He's comparing apples to oranges when he compa...</td>
      <td>-0.9583</td>
      <td>0.062</td>
      <td>0.113</td>
      <td>0.825</td>
    </tr>
    <tr>
      <th>9</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>I like to think that we have rather tough regu...</td>
      <td>0.5574</td>
      <td>0.063</td>
      <td>0.019</td>
      <td>0.918</td>
    </tr>
    <tr>
      <th>10</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>TIL only housewives cook chicken</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>And yet if the USDA regulates unpasteurized mi...</td>
      <td>-0.7003</td>
      <td>0.034</td>
      <td>0.184</td>
      <td>0.781</td>
    </tr>
    <tr>
      <th>12</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>May I insert a brief rant about food thermomet...</td>
      <td>0.9768</td>
      <td>0.177</td>
      <td>0.037</td>
      <td>0.786</td>
    </tr>
    <tr>
      <th>13</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>so imcredibly sexist!</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>Man, that was fucked up. I don't see why the U...</td>
      <td>-0.7845</td>
      <td>0.000</td>
      <td>0.210</td>
      <td>0.790</td>
    </tr>
    <tr>
      <th>15</th>
      <td>salmonella</td>
      <td>1at9cy</td>
      <td>all</td>
      <td>1.364005e+09</td>
      <td>It's still legal to sell poultry known to have...</td>
      <td>282</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>26</td>
      <td>http://nutritionfacts.org/video/salmonella-in-...</td>
      <td>nutritionfacts.org</td>
      <td>Smart enough to know to cook chicken properly,...</td>
      <td>-0.1531</td>
      <td>0.113</td>
      <td>0.137</td>
      <td>0.750</td>
    </tr>
    <tr>
      <th>16</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Chocolate induced weight loss? Perfect.</td>
      <td>0.3400</td>
      <td>0.411</td>
      <td>0.256</td>
      <td>0.333</td>
    </tr>
    <tr>
      <th>17</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>I'm going to risk it.</td>
      <td>-0.2732</td>
      <td>0.000</td>
      <td>0.344</td>
      <td>0.656</td>
    </tr>
    <tr>
      <th>18</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Ex-lax by any other name....still sprays the s...</td>
      <td>0.8020</td>
      <td>0.324</td>
      <td>0.000</td>
      <td>0.676</td>
    </tr>
    <tr>
      <th>19</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Eh. It's Mars. Barely qualifies as chocolate a...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Carefully melt it at above 140f and hope it do...</td>
      <td>0.5267</td>
      <td>0.216</td>
      <td>0.000</td>
      <td>0.784</td>
    </tr>
    <tr>
      <th>21</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Chocolate induced weight loss? Perfect.</td>
      <td>0.3400</td>
      <td>0.411</td>
      <td>0.256</td>
      <td>0.333</td>
    </tr>
    <tr>
      <th>22</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>I'm going to risk it.</td>
      <td>-0.2732</td>
      <td>0.000</td>
      <td>0.344</td>
      <td>0.656</td>
    </tr>
    <tr>
      <th>23</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Ex-lax by any other name....still sprays the s...</td>
      <td>0.8020</td>
      <td>0.324</td>
      <td>0.000</td>
      <td>0.676</td>
    </tr>
    <tr>
      <th>24</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Eh. It's Mars. Barely qualifies as chocolate a...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>salmonella</td>
      <td>6geeei</td>
      <td>all</td>
      <td>1.497116e+09</td>
      <td>Mars Salmonella Recall - Could be a lot of cho...</td>
      <td>148</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>14</td>
      <td>https://www.theguardian.com/business/2017/jun/...</td>
      <td>theguardian.com</td>
      <td>Carefully melt it at above 140f and hope it do...</td>
      <td>0.5267</td>
      <td>0.216</td>
      <td>0.000</td>
      <td>0.784</td>
    </tr>
    <tr>
      <th>26</th>
      <td>salmonella</td>
      <td>2toho</td>
      <td>all</td>
      <td>1.190836e+09</td>
      <td>The germ: Salmonella, best known as a culprit ...</td>
      <td>71</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>26</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>nytimes.com</td>
      <td>How do we know exactly how deadly those germs ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>27</th>
      <td>salmonella</td>
      <td>2toho</td>
      <td>all</td>
      <td>1.190836e+09</td>
      <td>The germ: Salmonella, best known as a culprit ...</td>
      <td>71</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>26</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>nytimes.com</td>
      <td>Here's the science:\r\nhttp://www.pnas.org/cgi...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>salmonella</td>
      <td>2toho</td>
      <td>all</td>
      <td>1.190836e+09</td>
      <td>The germ: Salmonella, best known as a culprit ...</td>
      <td>71</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>26</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>nytimes.com</td>
      <td>Anyone know what font settings the New York Ti...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>salmonella</td>
      <td>2toho</td>
      <td>all</td>
      <td>1.190836e+09</td>
      <td>The germ: Salmonella, best known as a culprit ...</td>
      <td>71</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>26</td>
      <td>http://www.nytimes.com/aponline/us/AP-Germs-in...</td>
      <td>nytimes.com</td>
      <td>"However, they think it's a force called fluid...</td>
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
      <th>4012</th>
      <td>salmonella</td>
      <td>85l5fi</td>
      <td>all</td>
      <td>1.521508e+09</td>
      <td>Salmonella outbreak in powdered plant suppleme...</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>i.redd.it</td>
      <td>https://nypost.com/2018/03/19/salmonella-outbr...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4013</th>
      <td>salmonella</td>
      <td>85l5fi</td>
      <td>all</td>
      <td>1.521508e+09</td>
      <td>Salmonella outbreak in powdered plant suppleme...</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>i.redd.it</td>
      <td>A Beejizz class action lawsuit = KNR Chapter 1...</td>
      <td>-0.2263</td>
      <td>0.000</td>
      <td>0.213</td>
      <td>0.787</td>
    </tr>
    <tr>
      <th>4014</th>
      <td>salmonella</td>
      <td>85l5fi</td>
      <td>all</td>
      <td>1.521508e+09</td>
      <td>Salmonella outbreak in powdered plant suppleme...</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>i.redd.it</td>
      <td>Kratom supposed to get you high af like weed. ...</td>
      <td>-0.3956</td>
      <td>0.097</td>
      <td>0.162</td>
      <td>0.740</td>
    </tr>
    <tr>
      <th>4015</th>
      <td>salmonella</td>
      <td>85l5fi</td>
      <td>all</td>
      <td>1.521508e+09</td>
      <td>Salmonella outbreak in powdered plant suppleme...</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>i.redd.it</td>
      <td>Kratom overrated. Not that I would have tried ...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4016</th>
      <td>salmonella</td>
      <td>85l5fi</td>
      <td>all</td>
      <td>1.521508e+09</td>
      <td>Salmonella outbreak in powdered plant suppleme...</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>i.redd.it</td>
      <td>Wouldja take 'eem?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4017</th>
      <td>salmonella</td>
      <td>85l5fi</td>
      <td>all</td>
      <td>1.521508e+09</td>
      <td>Salmonella outbreak in powdered plant suppleme...</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>11</td>
      <td>https://i.redd.it/r20sk71d6rm01.jpg</td>
      <td>i.redd.it</td>
      <td>"It might have Salmonella, it might not. Folks...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4018</th>
      <td>salmonella</td>
      <td>4puizu</td>
      <td>all</td>
      <td>1.466919e+09</td>
      <td>I miss the good ole days of salmonella!</td>
      <td>20</td>
      <td>https://i.redd.it/iby2x8ma9i5x.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/iby2x8ma9i5x.jpg</td>
      <td>i.redd.it</td>
      <td>And the ones who didn't live to tell about it?...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4019</th>
      <td>salmonella</td>
      <td>4puizu</td>
      <td>all</td>
      <td>1.466919e+09</td>
      <td>I miss the good ole days of salmonella!</td>
      <td>20</td>
      <td>https://i.redd.it/iby2x8ma9i5x.jpg</td>
      <td>2</td>
      <td>https://i.redd.it/iby2x8ma9i5x.jpg</td>
      <td>i.redd.it</td>
      <td>As far as I can tell, changes in egg productio...</td>
      <td>0.8689</td>
      <td>0.161</td>
      <td>0.028</td>
      <td>0.811</td>
    </tr>
    <tr>
      <th>4020</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Only white people can get salmonella. Dye your...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4021</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>try osmosis</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4022</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Easy solution: use a dental dam.</td>
      <td>0.6369</td>
      <td>0.634</td>
      <td>0.000</td>
      <td>0.366</td>
    </tr>
    <tr>
      <th>4023</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Smoke a salmon instead to offset the turkey. S...</td>
      <td>0.6988</td>
      <td>0.134</td>
      <td>0.000</td>
      <td>0.866</td>
    </tr>
    <tr>
      <th>4024</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>try getting into the oven with the turkey whil...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4025</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Use a bong it should filter out most of the ba...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4026</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>You must shove as much cold turkey up your anu...</td>
      <td>0.5994</td>
      <td>0.126</td>
      <td>0.037</td>
      <td>0.837</td>
    </tr>
    <tr>
      <th>4027</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Dip your turkey legs in bleach BEFORE you smok...</td>
      <td>0.6705</td>
      <td>0.216</td>
      <td>0.000</td>
      <td>0.784</td>
    </tr>
    <tr>
      <th>4028</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Heroin will both negate the salmonella and fee...</td>
      <td>0.0699</td>
      <td>0.222</td>
      <td>0.204</td>
      <td>0.574</td>
    </tr>
    <tr>
      <th>4029</th>
      <td>salmonella</td>
      <td>11adzp</td>
      <td>all</td>
      <td>1.349951e+09</td>
      <td>I'm trying to quit smoking 'cold turkey', but ...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>12</td>
      <td>https://www.reddit.com/r/shittyadvice/comments...</td>
      <td>self.shittyadvice</td>
      <td>Do some shit.</td>
      <td>-0.5574</td>
      <td>0.000</td>
      <td>0.643</td>
      <td>0.357</td>
    </tr>
    <tr>
      <th>4030</th>
      <td>salmonella</td>
      <td>74p4gg</td>
      <td>all</td>
      <td>1.507339e+09</td>
      <td>Second-hand Salmonella</td>
      <td>22</td>
      <td>https://www.reddit.com/r/Bandnames/comments/74...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Bandnames/comments/74...</td>
      <td>self.Bandnames</td>
      <td>Sal Monella and the Bad Eggs</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.412</td>
      <td>0.588</td>
    </tr>
    <tr>
      <th>4031</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>it doesn't say anything about "Vida la pita"</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.327</td>
      <td>0.673</td>
    </tr>
    <tr>
      <th>4032</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>... I love Vida la Pita.  I'm so happy I'm a v...</td>
      <td>0.5314</td>
      <td>0.283</td>
      <td>0.199</td>
      <td>0.518</td>
    </tr>
    <tr>
      <th>4033</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>I ate there a few weeks ago. Food wasn't that ...</td>
      <td>-0.3387</td>
      <td>0.108</td>
      <td>0.192</td>
      <td>0.699</td>
    </tr>
    <tr>
      <th>4034</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>Damn... I liked this place.</td>
      <td>0.4215</td>
      <td>0.483</td>
      <td>0.000</td>
      <td>0.517</td>
    </tr>
    <tr>
      <th>4035</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>Said it before, I'll say it again: Dirty store...</td>
      <td>-0.7003</td>
      <td>0.000</td>
      <td>0.345</td>
      <td>0.655</td>
    </tr>
    <tr>
      <th>4036</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>Sorry, made a mistake in the title. It's the o...</td>
      <td>-0.8225</td>
      <td>0.000</td>
      <td>0.290</td>
      <td>0.710</td>
    </tr>
    <tr>
      <th>4037</th>
      <td>salmonella</td>
      <td>q86km</td>
      <td>all</td>
      <td>1.330386e+09</td>
      <td>Possible Salmonella outbreak at Eat a Pita/Vid...</td>
      <td>17</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>9</td>
      <td>http://www.thespec.com/news/local/article/6769...</td>
      <td>thespec.com</td>
      <td>Falafels FTW</td>
      <td>0.5766</td>
      <td>0.789</td>
      <td>0.000</td>
      <td>0.211</td>
    </tr>
    <tr>
      <th>4038</th>
      <td>salmonella</td>
      <td>1o3d31</td>
      <td>all</td>
      <td>1.381382e+09</td>
      <td>CDC Brings Back 10 Furloughed Staff Members to...</td>
      <td>19</td>
      <td>http://abcnews.go.com/blogs/health/2013/10/08/...</td>
      <td>4</td>
      <td>http://abcnews.go.com/blogs/health/2013/10/08/...</td>
      <td>abcnews.go.com</td>
      <td>Wouldn't it have been better if they'd have be...</td>
      <td>0.4404</td>
      <td>0.172</td>
      <td>0.000</td>
      <td>0.828</td>
    </tr>
    <tr>
      <th>4039</th>
      <td>salmonella</td>
      <td>1o3d31</td>
      <td>all</td>
      <td>1.381382e+09</td>
      <td>CDC Brings Back 10 Furloughed Staff Members to...</td>
      <td>19</td>
      <td>http://abcnews.go.com/blogs/health/2013/10/08/...</td>
      <td>4</td>
      <td>http://abcnews.go.com/blogs/health/2013/10/08/...</td>
      <td>abcnews.go.com</td>
      <td>If you cook the chicken properly, you have not...</td>
      <td>-0.2249</td>
      <td>0.075</td>
      <td>0.094</td>
      <td>0.831</td>
    </tr>
    <tr>
      <th>4040</th>
      <td>salmonella</td>
      <td>3edniy</td>
      <td>all</td>
      <td>1.437720e+09</td>
      <td>Life sentence urged in peanut butter salmonell...</td>
      <td>22</td>
      <td>http://hosted.ap.org/dynamic/stories/U/US_SALM...</td>
      <td>2</td>
      <td>http://hosted.ap.org/dynamic/stories/U/US_SALM...</td>
      <td>hosted.ap.org</td>
      <td>"...Stewart Parnell never meant to hurt anyone...</td>
      <td>0.8152</td>
      <td>0.360</td>
      <td>0.000</td>
      <td>0.640</td>
    </tr>
    <tr>
      <th>4041</th>
      <td>salmonella</td>
      <td>3edniy</td>
      <td>all</td>
      <td>1.437720e+09</td>
      <td>Life sentence urged in peanut butter salmonell...</td>
      <td>22</td>
      <td>http://hosted.ap.org/dynamic/stories/U/US_SALM...</td>
      <td>2</td>
      <td>http://hosted.ap.org/dynamic/stories/U/US_SALM...</td>
      <td>hosted.ap.org</td>
      <td>Good luck with life sentence for that. Since w...</td>
      <td>0.7351</td>
      <td>0.419</td>
      <td>0.000</td>
      <td>0.581</td>
    </tr>
  </tbody>
</table>
<p>4042 rows × 15 columns</p>
</div>




```python
grouped_df5 = grouped_df5.groupby(['Created Date','Submission ID'])
```


```python
grouped_df5.count().head()
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
      <th>1.190836e+09</th>
      <th>2toho</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1.214952e+09</th>
      <th>6prw0</th>
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
      <th>1.215343e+09</th>
      <th>6qfho</th>
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
      <th>1.217003e+09</th>
      <th>6tdxc</th>
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
      <th>1.232204e+09</th>
      <th>7qe1w</th>
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
grouped_df5 = pd.DataFrame(grouped_df5["Compound Score"].mean())
grouped_df5
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
      <th>1.190836e+09</th>
      <th>2toho</th>
      <td>-0.135145</td>
    </tr>
    <tr>
      <th>1.214952e+09</th>
      <th>6prw0</th>
      <td>-0.291700</td>
    </tr>
    <tr>
      <th>1.215343e+09</th>
      <th>6qfho</th>
      <td>0.051410</td>
    </tr>
    <tr>
      <th>1.217003e+09</th>
      <th>6tdxc</th>
      <td>0.014200</td>
    </tr>
    <tr>
      <th>1.232204e+09</th>
      <th>7qe1w</th>
      <td>0.238200</td>
    </tr>
    <tr>
      <th>1.233031e+09</th>
      <th>7skvb</th>
      <td>-0.198883</td>
    </tr>
    <tr>
      <th>1.233170e+09</th>
      <th>7t0v8</th>
      <td>-0.549900</td>
    </tr>
    <tr>
      <th>1.233181e+09</th>
      <th>7t217</th>
      <td>-0.137338</td>
    </tr>
    <tr>
      <th>1.233525e+09</th>
      <th>7u100</th>
      <td>0.138708</td>
    </tr>
    <tr>
      <th>1.233657e+09</th>
      <th>7uepm</th>
      <td>-0.316700</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.233955e+09</th>
      <th>7vd19</th>
      <td>-0.050467</td>
    </tr>
    <tr>
      <th>7vd1l</th>
      <td>-0.390550</td>
    </tr>
    <tr>
      <th>1.234048e+09</th>
      <th>7vm6n</th>
      <td>-0.144980</td>
    </tr>
    <tr>
      <th>1.234059e+09</th>
      <th>7vn9c</th>
      <td>0.315450</td>
    </tr>
    <tr>
      <th>1.234129e+09</th>
      <th>7vrwl</th>
      <td>-0.233433</td>
    </tr>
    <tr>
      <th>1.234537e+09</th>
      <th>7x2ss</th>
      <td>-0.075263</td>
    </tr>
    <tr>
      <th>1.234585e+09</th>
      <th>7x8h3</th>
      <td>0.341200</td>
    </tr>
    <tr>
      <th>1.234617e+09</th>
      <th>7xbee</th>
      <td>-0.102480</td>
    </tr>
    <tr>
      <th>1.236759e+09</th>
      <th>83o8v</th>
      <td>0.017667</td>
    </tr>
    <tr>
      <th>1.236811e+09</th>
      <th>83tdp</th>
      <td>-0.188850</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.236981e+09</th>
      <th>84e04</th>
      <td>-0.221400</td>
    </tr>
    <tr>
      <th>84e0i</th>
      <td>-0.242200</td>
    </tr>
    <tr>
      <th>1.236987e+09</th>
      <th>84ey9</th>
      <td>0.195300</td>
    </tr>
    <tr>
      <th>1.260805e+09</th>
      <th>aeek9</th>
      <td>-0.028858</td>
    </tr>
    <tr>
      <th>1.262317e+09</th>
      <th>akc83</th>
      <td>-0.624250</td>
    </tr>
    <tr>
      <th>1.267831e+09</th>
      <th>b9o80</th>
      <td>-0.348380</td>
    </tr>
    <tr>
      <th>1.272778e+09</th>
      <th>byute</th>
      <td>0.210550</td>
    </tr>
    <tr>
      <th>1.273613e+09</th>
      <th>c2l7v</th>
      <td>-0.053055</td>
    </tr>
    <tr>
      <th>1.279517e+09</th>
      <th>cqzl7</th>
      <td>-0.036850</td>
    </tr>
    <tr>
      <th>1.281708e+09</th>
      <th>d0nyw</th>
      <td>0.136733</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.518851e+09</th>
      <th>7y2on7</th>
      <td>0.155555</td>
    </tr>
    <tr>
      <th>1.518883e+09</th>
      <th>7y5e9h</th>
      <td>0.120118</td>
    </tr>
    <tr>
      <th>1.518924e+09</th>
      <th>7y8nlq</th>
      <td>-0.288900</td>
    </tr>
    <tr>
      <th>1.519175e+09</th>
      <th>7yxi6o</th>
      <td>-0.275298</td>
    </tr>
    <tr>
      <th>1.519183e+09</th>
      <th>7yyn6i</th>
      <td>-0.389974</td>
    </tr>
    <tr>
      <th>1.519273e+09</th>
      <th>7z8qc0</th>
      <td>-0.089817</td>
    </tr>
    <tr>
      <th>1.519278e+09</th>
      <th>7z9cuf</th>
      <td>0.134250</td>
    </tr>
    <tr>
      <th>1.519454e+09</th>
      <th>7zs624</th>
      <td>-0.206200</td>
    </tr>
    <tr>
      <th>1.519632e+09</th>
      <th>808out</th>
      <td>0.114455</td>
    </tr>
    <tr>
      <th>1.519728e+09</th>
      <th>80ix22</th>
      <td>0.121145</td>
    </tr>
    <tr>
      <th>1.519930e+09</th>
      <th>814e8m</th>
      <td>-0.425000</td>
    </tr>
    <tr>
      <th>1.519994e+09</th>
      <th>81br4e</th>
      <td>-0.108933</td>
    </tr>
    <tr>
      <th>1.520052e+09</th>
      <th>81hya6</th>
      <td>-0.035964</td>
    </tr>
    <tr>
      <th>1.520057e+09</th>
      <th>81isyx</th>
      <td>-0.395437</td>
    </tr>
    <tr>
      <th>1.520077e+09</th>
      <th>81m5ax</th>
      <td>-0.015245</td>
    </tr>
    <tr>
      <th>1.520125e+09</th>
      <th>81rd1t</th>
      <td>0.593333</td>
    </tr>
    <tr>
      <th>1.520180e+09</th>
      <th>81wi4g</th>
      <td>0.103567</td>
    </tr>
    <tr>
      <th>1.520229e+09</th>
      <th>820v1q</th>
      <td>-0.143933</td>
    </tr>
    <tr>
      <th>1.520578e+09</th>
      <th>831tph</th>
      <td>-0.143960</td>
    </tr>
    <tr>
      <th>1.520737e+09</th>
      <th>83h6t0</th>
      <td>-0.528400</td>
    </tr>
    <tr>
      <th>1.520784e+09</th>
      <th>83li14</th>
      <td>-0.243167</td>
    </tr>
    <tr>
      <th>1.521156e+09</th>
      <th>84n751</th>
      <td>-0.470550</td>
    </tr>
    <tr>
      <th>1.521182e+09</th>
      <th>84qnoo</th>
      <td>-0.161367</td>
    </tr>
    <tr>
      <th>1.521224e+09</th>
      <th>84ucuq</th>
      <td>0.546300</td>
    </tr>
    <tr>
      <th>1.521242e+09</th>
      <th>84w40q</th>
      <td>-0.102843</td>
    </tr>
    <tr>
      <th>1.521330e+09</th>
      <th>854iyp</th>
      <td>-0.168200</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.521508e+09</th>
      <th>85l1yx</th>
      <td>0.561100</td>
    </tr>
    <tr>
      <th>85l5fi</th>
      <td>-0.104456</td>
    </tr>
    <tr>
      <th>1.521512e+09</th>
      <th>85lol6</th>
      <td>0.305700</td>
    </tr>
    <tr>
      <th>1.522025e+09</th>
      <th>871w0f</th>
      <td>-0.189763</td>
    </tr>
  </tbody>
</table>
<p>437 rows × 1 columns</p>
</div>




```python
grouped_df5 = grouped_df5.reset_index()
grouped_df5.head()
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
      <td>1.190836e+09</td>
      <td>2toho</td>
      <td>-0.135145</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.214952e+09</td>
      <td>6prw0</td>
      <td>-0.291700</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.215343e+09</td>
      <td>6qfho</td>
      <td>0.051410</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.217003e+09</td>
      <td>6tdxc</td>
      <td>0.014200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.232204e+09</td>
      <td>7qe1w</td>
      <td>0.238200</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df5, fit_reg=False, palette="Paired")

#plt.title("Salmonella Comment Sentiments on Reddit")

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

plt.savefig("Salmonella_Sentiments.png", dpi=350)

plt.show()
```


![png](output_68_0.png)



```python
grouped_df6 = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "Norovirus",:]
grouped_df6 = grouped_df6.reset_index()
del grouped_df6['index']
grouped_df6
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
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>Rodney's baby. I got some winter weight to los...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.197</td>
      <td>0.803</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>I still say it's the Lobster rolls from Rogers...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>My wife's entire family got the norovirus from...</td>
      <td>-0.3089</td>
      <td>0.000</td>
      <td>0.101</td>
      <td>0.899</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>Here's another link: http://vancouversun.com/n...</td>
      <td>-0.7994</td>
      <td>0.000</td>
      <td>0.146</td>
      <td>0.854</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>Rodney's baby. I got some winter weight to los...</td>
      <td>-0.4019</td>
      <td>0.000</td>
      <td>0.197</td>
      <td>0.803</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>I still say it's the Lobster rolls from Rogers...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>My wife's entire family got the norovirus from...</td>
      <td>-0.3089</td>
      <td>0.000</td>
      <td>0.101</td>
      <td>0.899</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Norovirus</td>
      <td>60w04m</td>
      <td>all</td>
      <td>1.490232e+09</td>
      <td>Norovirus stemming from oysters in BC -- gonna...</td>
      <td>46</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>15</td>
      <td>http://www.cbc.ca/news/canada/british-columbia...</td>
      <td>cbc.ca</td>
      <td>Here's another link: http://vancouversun.com/n...</td>
      <td>-0.7994</td>
      <td>0.000</td>
      <td>0.146</td>
      <td>0.854</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>I'm going to guess that Axe Capital has a huge...</td>
      <td>0.2263</td>
      <td>0.181</td>
      <td>0.110</td>
      <td>0.709</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Someone is trying to sabotage Chipotle</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.405</td>
      <td>0.595</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Great way to lose weight, albeit very uncomfor...</td>
      <td>-0.1263</td>
      <td>0.232</td>
      <td>0.316</td>
      <td>0.452</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Buy?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>I was just reminded that when Jack In the Box ...</td>
      <td>-0.9184</td>
      <td>0.000</td>
      <td>0.317</td>
      <td>0.683</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Thank god when I loaded up on my yearly OotM P...</td>
      <td>0.8519</td>
      <td>0.262</td>
      <td>0.000</td>
      <td>0.738</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Sabotage!</td>
      <td>-0.5707</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Chipotle is a fan favorite in a "good" economy...</td>
      <td>0.7351</td>
      <td>0.265</td>
      <td>0.054</td>
      <td>0.680</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Does anyone know of any funds or research shop...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>I'll still eat that shit twice a week to be ho...</td>
      <td>-0.0772</td>
      <td>0.221</td>
      <td>0.242</td>
      <td>0.537</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>For those who still plan to eat Chipotle.. her...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Website is pure AIDS on mobile</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Fuck chipotle</td>
      <td>-0.5423</td>
      <td>0.000</td>
      <td>0.778</td>
      <td>0.222</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>I'm going to guess that Axe Capital has a huge...</td>
      <td>0.2263</td>
      <td>0.181</td>
      <td>0.110</td>
      <td>0.709</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Someone is trying to sabotage Chipotle</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.405</td>
      <td>0.595</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Great way to lose weight, albeit very uncomfor...</td>
      <td>-0.1263</td>
      <td>0.232</td>
      <td>0.316</td>
      <td>0.452</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Buy?</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>I was just reminded that when Jack In the Box ...</td>
      <td>-0.9184</td>
      <td>0.000</td>
      <td>0.317</td>
      <td>0.683</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Thank god when I loaded up on my yearly OotM P...</td>
      <td>0.8519</td>
      <td>0.262</td>
      <td>0.000</td>
      <td>0.738</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Sabotage!</td>
      <td>-0.5707</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Chipotle is a fan favorite in a "good" economy...</td>
      <td>0.7351</td>
      <td>0.265</td>
      <td>0.054</td>
      <td>0.680</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Norovirus</td>
      <td>6o2355</td>
      <td>all</td>
      <td>1.500426e+09</td>
      <td>Chipotle Hit With Another Foodborne Illness – ...</td>
      <td>196</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>49</td>
      <td>http://ibankcoin.com/zeropointnow/2017/07/18/c...</td>
      <td>ibankcoin.com</td>
      <td>Does anyone know of any funds or research shop...</td>
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
      <th>2516</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>Stay home. We always have noro out breaks in t...</td>
      <td>-0.7264</td>
      <td>0.000</td>
      <td>0.132</td>
      <td>0.868</td>
    </tr>
    <tr>
      <th>2517</th>
      <td>Norovirus</td>
      <td>3ztzul</td>
      <td>all</td>
      <td>1.452172e+09</td>
      <td>Back to work tomorrow, but have norovirus (new...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>7</td>
      <td>https://www.reddit.com/r/nursing/comments/3ztz...</td>
      <td>self.nursing</td>
      <td>No, you're still contagious, you should not go...</td>
      <td>-0.7717</td>
      <td>0.000</td>
      <td>0.372</td>
      <td>0.628</td>
    </tr>
    <tr>
      <th>2518</th>
      <td>Norovirus</td>
      <td>2sh27m</td>
      <td>all</td>
      <td>1.421318e+09</td>
      <td>New evidence in mice suggests antibiotics may ...</td>
      <td>3</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>1</td>
      <td>http://www.sciguru.org/newsitem/18220/possible...</td>
      <td>sciguru.org</td>
      <td>So the virus uses bacteria in order to remain ...</td>
      <td>-0.8176</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
    </tr>
    <tr>
      <th>2519</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Soap! Wear gloves and clean all surfaces that ...</td>
      <td>0.5659</td>
      <td>0.182</td>
      <td>0.000</td>
      <td>0.818</td>
    </tr>
    <tr>
      <th>2520</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Norovirus is simply a viral GI "bug". It's not...</td>
      <td>0.6222</td>
      <td>0.178</td>
      <td>0.149</td>
      <td>0.674</td>
    </tr>
    <tr>
      <th>2521</th>
      <td>Norovirus</td>
      <td>5j7l9f</td>
      <td>all</td>
      <td>1.482197e+09</td>
      <td>What are the best safety precautions to take t...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/5j7l...</td>
      <td>self.AskDocs</td>
      <td>Use a 5-10% bleach solution to clean hard surf...</td>
      <td>0.5574</td>
      <td>0.214</td>
      <td>0.060</td>
      <td>0.726</td>
    </tr>
    <tr>
      <th>2522</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Norovirus is extraordinarily easy to spread an...</td>
      <td>0.8685</td>
      <td>0.116</td>
      <td>0.071</td>
      <td>0.813</td>
    </tr>
    <tr>
      <th>2523</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>You don't have to ingest food to contract noro...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2524</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Yikes, no fun, though you don't necessarily ha...</td>
      <td>0.8016</td>
      <td>0.288</td>
      <td>0.068</td>
      <td>0.644</td>
    </tr>
    <tr>
      <th>2525</th>
      <td>Norovirus</td>
      <td>41nkl8</td>
      <td>all</td>
      <td>1.453218e+09</td>
      <td>Norovirus from Chuys?</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/Dallas/comments/41nkl...</td>
      <td>self.Dallas</td>
      <td>Contact the city's health department.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2526</th>
      <td>Norovirus</td>
      <td>15w8xm</td>
      <td>all</td>
      <td>1.357261e+09</td>
      <td>Can people be immune/resistant to norovirus an...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/askscience/comments/1...</td>
      <td>self.askscience</td>
      <td>With regards to your comment on "higher stomac...</td>
      <td>0.4056</td>
      <td>0.053</td>
      <td>0.058</td>
      <td>0.889</td>
    </tr>
    <tr>
      <th>2527</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Gah, I hate when people think lying will help ...</td>
      <td>-0.7806</td>
      <td>0.143</td>
      <td>0.318</td>
      <td>0.539</td>
    </tr>
    <tr>
      <th>2528</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Also like to add, no crazy lovey dovey kissing...</td>
      <td>0.8268</td>
      <td>0.398</td>
      <td>0.149</td>
      <td>0.453</td>
    </tr>
    <tr>
      <th>2529</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Now Monday, still nothing. I'm getting more co...</td>
      <td>0.6361</td>
      <td>0.302</td>
      <td>0.000</td>
      <td>0.698</td>
    </tr>
    <tr>
      <th>2530</th>
      <td>Norovirus</td>
      <td>5qrl5v</td>
      <td>all</td>
      <td>1.485687e+09</td>
      <td>Significant other with potential Norovirus ear...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>8</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>So I didn't catch it during the week. I hung o...</td>
      <td>0.1007</td>
      <td>0.070</td>
      <td>0.057</td>
      <td>0.873</td>
    </tr>
    <tr>
      <th>2531</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>Down water, take vocal breaks, and just rest a...</td>
      <td>0.9273</td>
      <td>0.179</td>
      <td>0.016</td>
      <td>0.805</td>
    </tr>
    <tr>
      <th>2532</th>
      <td>Norovirus</td>
      <td>5lpsei</td>
      <td>all</td>
      <td>1.483445e+09</td>
      <td>Vocal Recovery After Vomiting Profusely from N...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/singing/comments/5lps...</td>
      <td>self.singing</td>
      <td>I would say rest it as much as possible. If wo...</td>
      <td>0.9690</td>
      <td>0.158</td>
      <td>0.021</td>
      <td>0.821</td>
    </tr>
    <tr>
      <th>2533</th>
      <td>Norovirus</td>
      <td>6wktp0</td>
      <td>all</td>
      <td>1.503969e+09</td>
      <td>Norovirus :(</td>
      <td>2</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/AskDocs/comments/6wkt...</td>
      <td>self.AskDocs</td>
      <td>It usually runs its course, its does generally...</td>
      <td>0.7750</td>
      <td>0.140</td>
      <td>0.053</td>
      <td>0.807</td>
    </tr>
    <tr>
      <th>2534</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Small sips of water every 10 minutes. See if s...</td>
      <td>-0.5267</td>
      <td>0.000</td>
      <td>0.091</td>
      <td>0.909</td>
    </tr>
    <tr>
      <th>2535</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>Go to the ER and get an IV.</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2536</th>
      <td>Norovirus</td>
      <td>7oqk3m</td>
      <td>all</td>
      <td>1.515361e+09</td>
      <td>Suffering from norovirus - Dehydrated and can’...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/AskDocs/comments/7oqk...</td>
      <td>self.AskDocs</td>
      <td>If you have a primary care physician, you can ...</td>
      <td>0.7096</td>
      <td>0.211</td>
      <td>0.000</td>
      <td>0.789</td>
    </tr>
    <tr>
      <th>2537</th>
      <td>Norovirus</td>
      <td>7w8d8d</td>
      <td>all</td>
      <td>1.518155e+09</td>
      <td>Norovirus at the Olympics</td>
      <td>2</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Jokes/comments/7w8d8d...</td>
      <td>self.Jokes</td>
      <td>That stuff is so ugly and spreads so fast. I w...</td>
      <td>-0.4101</td>
      <td>0.087</td>
      <td>0.148</td>
      <td>0.765</td>
    </tr>
    <tr>
      <th>2538</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>You could call your doctor to confirm, my unde...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2539</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>Agree with commenter above. And don't share to...</td>
      <td>0.1561</td>
      <td>0.162</td>
      <td>0.123</td>
      <td>0.715</td>
    </tr>
    <tr>
      <th>2540</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>A couple Thanksgivings ago, my sister brought ...</td>
      <td>-0.8555</td>
      <td>0.000</td>
      <td>0.120</td>
      <td>0.880</td>
    </tr>
    <tr>
      <th>2541</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I had norovirus when my lo was about 11 months...</td>
      <td>-0.1018</td>
      <td>0.000</td>
      <td>0.032</td>
      <td>0.968</td>
    </tr>
    <tr>
      <th>2542</th>
      <td>Norovirus</td>
      <td>7uuzd5</td>
      <td>all</td>
      <td>1.517638e+09</td>
      <td>Urgent: stopping baby from getting norovirus</td>
      <td>1</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>5</td>
      <td>https://www.reddit.com/r/beyondthebump/comment...</td>
      <td>self.beyondthebump</td>
      <td>I never updated here! Thanks so much for all y...</td>
      <td>-0.4100</td>
      <td>0.119</td>
      <td>0.195</td>
      <td>0.686</td>
    </tr>
    <tr>
      <th>2543</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Just wanted to give you a head's up! I went th...</td>
      <td>0.7333</td>
      <td>0.136</td>
      <td>0.045</td>
      <td>0.819</td>
    </tr>
    <tr>
      <th>2544</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>I'd be willing to bet that your brother got si...</td>
      <td>-0.9699</td>
      <td>0.083</td>
      <td>0.154</td>
      <td>0.762</td>
    </tr>
    <tr>
      <th>2545</th>
      <td>Norovirus</td>
      <td>7qyr5z</td>
      <td>all</td>
      <td>1.516195e+09</td>
      <td>Family member sick with possible norovirus</td>
      <td>5</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>6</td>
      <td>https://www.reddit.com/r/emetophobia/comments/...</td>
      <td>self.emetophobia</td>
      <td>Where are you located? I've seen in emetophobi...</td>
      <td>-0.8909</td>
      <td>0.065</td>
      <td>0.136</td>
      <td>0.799</td>
    </tr>
  </tbody>
</table>
<p>2546 rows × 15 columns</p>
</div>




```python
grouped_df6 = grouped_df6.groupby(['Created Date','Submission ID'])
```


```python
grouped_df6.count().head()
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
      <th>1.235956e+09</th>
      <th>8183h</th>
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
      <th>1.250740e+09</th>
      <th>9c73g</th>
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
    <tr>
      <th>1.309514e+09</th>
      <th>idtli</th>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1.322608e+09</th>
      <th>mtdrs</th>
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
    <tr>
      <th>1.325681e+09</th>
      <th>o232k</th>
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
grouped_df6 = pd.DataFrame(grouped_df6["Compound Score"].mean())
grouped_df6
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
      <th>1.235956e+09</th>
      <th>8183h</th>
      <td>-0.064000</td>
    </tr>
    <tr>
      <th>1.250740e+09</th>
      <th>9c73g</th>
      <td>0.612400</td>
    </tr>
    <tr>
      <th>1.309514e+09</th>
      <th>idtli</th>
      <td>0.016780</td>
    </tr>
    <tr>
      <th>1.322608e+09</th>
      <th>mtdrs</th>
      <td>0.077200</td>
    </tr>
    <tr>
      <th>1.325681e+09</th>
      <th>o232k</th>
      <td>0.493900</td>
    </tr>
    <tr>
      <th>1.326660e+09</th>
      <th>ohxh9</th>
      <td>0.093033</td>
    </tr>
    <tr>
      <th>1.328232e+09</th>
      <th>p7w4n</th>
      <td>0.460500</td>
    </tr>
    <tr>
      <th>1.328474e+09</th>
      <th>pbs0h</th>
      <td>0.023333</td>
    </tr>
    <tr>
      <th>1.328505e+09</th>
      <th>pc98v</th>
      <td>-0.329850</td>
    </tr>
    <tr>
      <th>1.328610e+09</th>
      <th>pe1ow</th>
      <td>-0.036867</td>
    </tr>
    <tr>
      <th>1.328697e+09</th>
      <th>pfmra</th>
      <td>0.196300</td>
    </tr>
    <tr>
      <th>1.328854e+09</th>
      <th>pieqh</th>
      <td>-0.024900</td>
    </tr>
    <tr>
      <th>1.329182e+09</th>
      <th>pnncq</th>
      <td>0.117002</td>
    </tr>
    <tr>
      <th>1.329364e+09</th>
      <th>pr4bx</th>
      <td>0.052560</td>
    </tr>
    <tr>
      <th>1.329518e+09</th>
      <th>ptw9l</th>
      <td>0.120500</td>
    </tr>
    <tr>
      <th>1.332383e+09</th>
      <th>r72wp</th>
      <td>0.226867</td>
    </tr>
    <tr>
      <th>1.334433e+09</th>
      <th>s9dvu</th>
      <td>0.077200</td>
    </tr>
    <tr>
      <th>1.345504e+09</th>
      <th>yix7v</th>
      <td>0.310825</td>
    </tr>
    <tr>
      <th>1.348883e+09</th>
      <th>10mmvt</th>
      <td>0.285167</td>
    </tr>
    <tr>
      <th>1.349811e+09</th>
      <th>116vqn</th>
      <td>-0.051453</td>
    </tr>
    <tr>
      <th>1.354213e+09</th>
      <th>13zkix</th>
      <td>0.185400</td>
    </tr>
    <tr>
      <th>1.354323e+09</th>
      <th>1423g8</th>
      <td>0.325450</td>
    </tr>
    <tr>
      <th>1.354716e+09</th>
      <th>14b56c</th>
      <td>-0.246650</td>
    </tr>
    <tr>
      <th>1.355108e+09</th>
      <th>14k3lt</th>
      <td>0.724800</td>
    </tr>
    <tr>
      <th>1.355607e+09</th>
      <th>14w69n</th>
      <td>-0.115814</td>
    </tr>
    <tr>
      <th>1.355701e+09</th>
      <th>14xz3d</th>
      <td>0.163783</td>
    </tr>
    <tr>
      <th>1.356236e+09</th>
      <th>15akfv</th>
      <td>0.113333</td>
    </tr>
    <tr>
      <th>1.356331e+09</th>
      <th>15ceaa</th>
      <td>-0.223750</td>
    </tr>
    <tr>
      <th>1.356404e+09</th>
      <th>15dusd</th>
      <td>0.420900</td>
    </tr>
    <tr>
      <th>1.356549e+09</th>
      <th>15gq4u</th>
      <td>-0.379570</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.517375e+09</th>
      <th>7u4a9u</th>
      <td>-0.078011</td>
    </tr>
    <tr>
      <th>1.517638e+09</th>
      <th>7uuzd5</th>
      <td>-0.242240</td>
    </tr>
    <tr>
      <th>1.517935e+09</th>
      <th>7vlzvi</th>
      <td>-0.312750</td>
    </tr>
    <tr>
      <th>1.517937e+09</th>
      <th>7vm63n</th>
      <td>0.059660</td>
    </tr>
    <tr>
      <th>1.517951e+09</th>
      <th>7vn610</th>
      <td>0.027208</td>
    </tr>
    <tr>
      <th>1.517968e+09</th>
      <th>7vp1fc</th>
      <td>0.765000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.517972e+09</th>
      <th>7vpj83</th>
      <td>-0.457400</td>
    </tr>
    <tr>
      <th>7vpjxv</th>
      <td>-0.865800</td>
    </tr>
    <tr>
      <th>1.517989e+09</th>
      <th>7vrodf</th>
      <td>-0.357400</td>
    </tr>
    <tr>
      <th>1.517991e+09</th>
      <th>7vrzmc</th>
      <td>-0.655500</td>
    </tr>
    <tr>
      <th>1.518016e+09</th>
      <th>7vucc0</th>
      <td>-0.090267</td>
    </tr>
    <tr>
      <th>1.518047e+09</th>
      <th>7vwyf1</th>
      <td>0.875000</td>
    </tr>
    <tr>
      <th>1.518127e+09</th>
      <th>7w4ye2</th>
      <td>-0.266400</td>
    </tr>
    <tr>
      <th>1.518137e+09</th>
      <th>7w63cn</th>
      <td>-0.000998</td>
    </tr>
    <tr>
      <th>1.518151e+09</th>
      <th>7w7w2i</th>
      <td>0.470300</td>
    </tr>
    <tr>
      <th>1.518153e+09</th>
      <th>7w85zi</th>
      <td>0.297100</td>
    </tr>
    <tr>
      <th>1.518155e+09</th>
      <th>7w8d8d</th>
      <td>-0.410100</td>
    </tr>
    <tr>
      <th>1.518166e+09</th>
      <th>7w9nx8</th>
      <td>0.360050</td>
    </tr>
    <tr>
      <th>1.518201e+09</th>
      <th>7wclxq</th>
      <td>0.261167</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.518220e+09</th>
      <th>7weanq</th>
      <td>-0.078100</td>
    </tr>
    <tr>
      <th>7web2l</th>
      <td>-0.612967</td>
    </tr>
    <tr>
      <th>1.518222e+09</th>
      <th>7wegqi</th>
      <td>-0.122480</td>
    </tr>
    <tr>
      <th>1.518264e+09</th>
      <th>7wj63u</th>
      <td>0.099475</td>
    </tr>
    <tr>
      <th>1.518782e+09</th>
      <th>7xw5y9</th>
      <td>0.480400</td>
    </tr>
    <tr>
      <th>1.518864e+09</th>
      <th>7y3yo7</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.518926e+09</th>
      <th>7y8xb9</th>
      <td>0.361417</td>
    </tr>
    <tr>
      <th>1.519216e+09</th>
      <th>7z2scp</th>
      <td>0.275043</td>
    </tr>
    <tr>
      <th>1.519775e+09</th>
      <th>80neel</th>
      <td>-0.148000</td>
    </tr>
    <tr>
      <th>1.520631e+09</th>
      <th>836ntd</th>
      <td>-0.198520</td>
    </tr>
    <tr>
      <th>1.521866e+09</th>
      <th>86nvwi</th>
      <td>0.311333</td>
    </tr>
  </tbody>
</table>
<p>403 rows × 1 columns</p>
</div>




```python
grouped_df6 = grouped_df6.reset_index()
grouped_df6.head()
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
      <td>1.235956e+09</td>
      <td>8183h</td>
      <td>-0.06400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.250740e+09</td>
      <td>9c73g</td>
      <td>0.61240</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.309514e+09</td>
      <td>idtli</td>
      <td>0.01678</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.322608e+09</td>
      <td>mtdrs</td>
      <td>0.07720</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.325681e+09</td>
      <td>o232k</td>
      <td>0.49390</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df6, fit_reg=False, palette="Paired")

#plt.title("Norovirus Comment Sentiments on Reddit")

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

plt.savefig("Norovirus_Sentiments.png", dpi=350)

plt.show()
```


![png](output_74_0.png)



```python
grouped_df7 = reddit_comments_df.loc[reddit_comments_df["Keyword"] == "foodborne illness",:]
grouped_df7 = grouped_df7.reset_index()
del grouped_df7['index']
grouped_df7
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
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>I wonder if they include every common misspell...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>My waiter had diarrhea of the mouth but on the...</td>
      <td>-0.9136</td>
      <td>0.000</td>
      <td>0.328</td>
      <td>0.672</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>&gt;When people feel sick after going out to eat,...</td>
      <td>-0.9118</td>
      <td>0.017</td>
      <td>0.109</td>
      <td>0.875</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>While interesting, actual food borne illness c...</td>
      <td>-0.2023</td>
      <td>0.045</td>
      <td>0.088</td>
      <td>0.867</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>Surely such a straightforward technological so...</td>
      <td>0.2477</td>
      <td>0.125</td>
      <td>0.091</td>
      <td>0.785</td>
    </tr>
    <tr>
      <th>5</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>They could just google Chinese restaurants and...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>Because Yelp is such a reputable site. They mi...</td>
      <td>0.2732</td>
      <td>0.123</td>
      <td>0.000</td>
      <td>0.877</td>
    </tr>
    <tr>
      <th>7</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>I wonder if they include every common misspell...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>My waiter had diarrhea of the mouth but on the...</td>
      <td>-0.9136</td>
      <td>0.000</td>
      <td>0.328</td>
      <td>0.672</td>
    </tr>
    <tr>
      <th>9</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>&gt;When people feel sick after going out to eat,...</td>
      <td>-0.9118</td>
      <td>0.017</td>
      <td>0.109</td>
      <td>0.875</td>
    </tr>
    <tr>
      <th>10</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>While interesting, actual food borne illness c...</td>
      <td>-0.2023</td>
      <td>0.045</td>
      <td>0.088</td>
      <td>0.867</td>
    </tr>
    <tr>
      <th>11</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>Surely such a straightforward technological so...</td>
      <td>0.2477</td>
      <td>0.125</td>
      <td>0.091</td>
      <td>0.785</td>
    </tr>
    <tr>
      <th>12</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>They could just google Chinese restaurants and...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>foodborne illness</td>
      <td>83z1bd</td>
      <td>all</td>
      <td>1.520921e+09</td>
      <td>TIL the NYC Dept of Health and researchers fro...</td>
      <td>175</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>12</td>
      <td>https://www.atlasobscura.com/articles/food-poi...</td>
      <td>atlasobscura.com</td>
      <td>Because Yelp is such a reputable site. They mi...</td>
      <td>0.2732</td>
      <td>0.123</td>
      <td>0.000</td>
      <td>0.877</td>
    </tr>
    <tr>
      <th>14</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>This has been know for at least 60 years.  It ...</td>
      <td>-0.1531</td>
      <td>0.000</td>
      <td>0.038</td>
      <td>0.962</td>
    </tr>
    <tr>
      <th>15</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>So they used an LED at 405nm and it's causing ...</td>
      <td>0.5389</td>
      <td>0.113</td>
      <td>0.070</td>
      <td>0.818</td>
    </tr>
    <tr>
      <th>16</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>Is this what the weird blue light boxes in som...</td>
      <td>-0.1779</td>
      <td>0.000</td>
      <td>0.124</td>
      <td>0.876</td>
    </tr>
    <tr>
      <th>17</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>Interestingly enough, certain blue wavelengths...</td>
      <td>0.8225</td>
      <td>0.167</td>
      <td>0.000</td>
      <td>0.833</td>
    </tr>
    <tr>
      <th>18</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>Yes. UV sanitation is already a thing.</td>
      <td>0.4019</td>
      <td>0.351</td>
      <td>0.000</td>
      <td>0.649</td>
    </tr>
    <tr>
      <th>19</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>This is probably referring to Blue Violet ligh...</td>
      <td>0.4035</td>
      <td>0.086</td>
      <td>0.094</td>
      <td>0.820</td>
    </tr>
    <tr>
      <th>20</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>My old department used to use this tech for no...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>I can imagine my old metaphysics lecturer want...</td>
      <td>0.2732</td>
      <td>0.075</td>
      <td>0.000</td>
      <td>0.925</td>
    </tr>
    <tr>
      <th>22</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>Given we have seen bacteria evolve to develop ...</td>
      <td>-0.1027</td>
      <td>0.000</td>
      <td>0.062</td>
      <td>0.938</td>
    </tr>
    <tr>
      <th>23</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>I work in HVAC and we use ultraviolet light in...</td>
      <td>-0.1531</td>
      <td>0.159</td>
      <td>0.182</td>
      <td>0.659</td>
    </tr>
    <tr>
      <th>24</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>I was at a poultry processing expo and there w...</td>
      <td>0.0258</td>
      <td>0.087</td>
      <td>0.084</td>
      <td>0.828</td>
    </tr>
    <tr>
      <th>25</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>Fun fact: This is why it is called ultra viole...</td>
      <td>-0.1531</td>
      <td>0.163</td>
      <td>0.193</td>
      <td>0.644</td>
    </tr>
    <tr>
      <th>26</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>I know somone that had a deep blue grow-light ...</td>
      <td>-0.2500</td>
      <td>0.090</td>
      <td>0.090</td>
      <td>0.820</td>
    </tr>
    <tr>
      <th>27</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>Ahh that bowl of pasta I left by my bedroom wi...</td>
      <td>0.2023</td>
      <td>0.107</td>
      <td>0.000</td>
      <td>0.893</td>
    </tr>
    <tr>
      <th>28</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>I thought this was well known for a while now.</td>
      <td>0.2732</td>
      <td>0.231</td>
      <td>0.000</td>
      <td>0.769</td>
    </tr>
    <tr>
      <th>29</th>
      <td>foodborne illness</td>
      <td>5x2dg0</td>
      <td>all</td>
      <td>1.488477e+09</td>
      <td>Specific wavelengths of blue and violet light ...</td>
      <td>2248</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>133</td>
      <td>http://acsh.org/news/2017/03/01/how-kill-bacte...</td>
      <td>acsh.org</td>
      <td>This might work great... If your food is clear...</td>
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
      <th>478</th>
      <td>foodborne illness</td>
      <td>809izw</td>
      <td>all</td>
      <td>1.519640e+09</td>
      <td>A steal at only $38! Now with more foodborne i...</td>
      <td>2</td>
      <td>https://i.imgur.com/0mTte0Q.jpg</td>
      <td>1</td>
      <td>https://i.imgur.com/0mTte0Q.jpg</td>
      <td>i.imgur.com</td>
      <td>That calamari looks frozen</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>479</th>
      <td>foodborne illness</td>
      <td>4rsq6n</td>
      <td>all</td>
      <td>1.467978e+09</td>
      <td>I trust Hillary Clinton about as much as I tru...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/The_Donald/comments/4...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/The_Donald/comments/4...</td>
      <td>self.The_Donald</td>
      <td>She is so fucking ugly, inside and out. Her vo...</td>
      <td>-0.6214</td>
      <td>0.086</td>
      <td>0.226</td>
      <td>0.688</td>
    </tr>
    <tr>
      <th>480</th>
      <td>foodborne illness</td>
      <td>3j6032</td>
      <td>all</td>
      <td>1.441102e+09</td>
      <td>[Serious]What is the best way to avoid foodbor...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/AskReddit/comments/3j...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/AskReddit/comments/3j...</td>
      <td>self.AskReddit</td>
      <td>**Attention!** Please keep in mind that the OP...</td>
      <td>0.9182</td>
      <td>0.115</td>
      <td>0.020</td>
      <td>0.864</td>
    </tr>
    <tr>
      <th>481</th>
      <td>foodborne illness</td>
      <td>5b8xzo</td>
      <td>all</td>
      <td>1.478361e+09</td>
      <td>Can foodborne illnesses be transmitted through...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/NoStupidQuestions/com...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/NoStupidQuestions/com...</td>
      <td>self.NoStupidQuestions</td>
      <td>Certain bacteria like salmonella could be tran...</td>
      <td>0.6249</td>
      <td>0.197</td>
      <td>0.082</td>
      <td>0.721</td>
    </tr>
    <tr>
      <th>482</th>
      <td>foodborne illness</td>
      <td>twxww</td>
      <td>all</td>
      <td>1.337598e+09</td>
      <td>[Seeking] Internship/fellowship/experience in ...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/MNJobs/comments/twxww...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/MNJobs/comments/twxww...</td>
      <td>self.MNJobs</td>
      <td>Are you interested in going down a route of di...</td>
      <td>0.4019</td>
      <td>0.044</td>
      <td>0.000</td>
      <td>0.956</td>
    </tr>
    <tr>
      <th>483</th>
      <td>foodborne illness</td>
      <td>5i69r4</td>
      <td>all</td>
      <td>1.481693e+09</td>
      <td>Content for a foodborne illness course geared ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/publichealth/comments...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/publichealth/comments...</td>
      <td>self.publichealth</td>
      <td>Talking about potential effects of climate cha...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>484</th>
      <td>foodborne illness</td>
      <td>5i69r4</td>
      <td>all</td>
      <td>1.481693e+09</td>
      <td>Content for a foodborne illness course geared ...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/publichealth/comments...</td>
      <td>4</td>
      <td>https://www.reddit.com/r/publichealth/comments...</td>
      <td>self.publichealth</td>
      <td>Food Systems: how farming/agriculture relate t...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>485</th>
      <td>foodborne illness</td>
      <td>69toqq</td>
      <td>all</td>
      <td>1.494219e+09</td>
      <td>Excuse my ignorance, but can fish TB be a food...</td>
      <td>3</td>
      <td>https://www.reddit.com/r/Aquariums/comments/69...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Aquariums/comments/69...</td>
      <td>self.Aquariums</td>
      <td>Cooking denatures DNA, which means that any ba...</td>
      <td>-0.8176</td>
      <td>0.000</td>
      <td>0.366</td>
      <td>0.634</td>
    </tr>
    <tr>
      <th>486</th>
      <td>foodborne illness</td>
      <td>4u33o6</td>
      <td>all</td>
      <td>1.469228e+09</td>
      <td>[Book] - Procedures for Investigating Foodborn...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Scholar/comments/4u33...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/Scholar/comments/4u33...</td>
      <td>self.Scholar</td>
      <td>http://moscow.sci-hub.cc/962ee2f76b1bd80bec329...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>487</th>
      <td>foodborne illness</td>
      <td>3ni418</td>
      <td>all</td>
      <td>1.444026e+09</td>
      <td>Foodborne Illness and Plastic Bag Bans</td>
      <td>1</td>
      <td>http://www.perc.org/articles/foodborne-illness...</td>
      <td>2</td>
      <td>http://www.perc.org/articles/foodborne-illness...</td>
      <td>perc.org</td>
      <td>&gt;We experienced two godawful smelling reusable...</td>
      <td>0.5996</td>
      <td>0.246</td>
      <td>0.000</td>
      <td>0.754</td>
    </tr>
    <tr>
      <th>488</th>
      <td>foodborne illness</td>
      <td>3ni418</td>
      <td>all</td>
      <td>1.444026e+09</td>
      <td>Foodborne Illness and Plastic Bag Bans</td>
      <td>1</td>
      <td>http://www.perc.org/articles/foodborne-illness...</td>
      <td>2</td>
      <td>http://www.perc.org/articles/foodborne-illness...</td>
      <td>perc.org</td>
      <td>I live in Austin. We experienced two godawful ...</td>
      <td>-0.1280</td>
      <td>0.035</td>
      <td>0.056</td>
      <td>0.909</td>
    </tr>
    <tr>
      <th>489</th>
      <td>foodborne illness</td>
      <td>z2i5y</td>
      <td>all</td>
      <td>1.346346e+09</td>
      <td>Foodborne illnesses: Origins and prevention</td>
      <td>2</td>
      <td>http://www.foxnews.com/health/2012/08/29/foodb...</td>
      <td>1</td>
      <td>http://www.foxnews.com/health/2012/08/29/foodb...</td>
      <td>foxnews.com</td>
      <td>This is probably a genuine article but I just ...</td>
      <td>-0.4215</td>
      <td>0.000</td>
      <td>0.123</td>
      <td>0.877</td>
    </tr>
    <tr>
      <th>490</th>
      <td>foodborne illness</td>
      <td>eom2a</td>
      <td>all</td>
      <td>1.292852e+09</td>
      <td>CDC Reports 37% Fewer Cases of Foodborne Illness</td>
      <td>2</td>
      <td>http://www.usatoday.com/yourlife/health/medica...</td>
      <td>1</td>
      <td>http://www.usatoday.com/yourlife/health/medica...</td>
      <td>usatoday.com</td>
      <td>FTA: The new numbers reflect what CDC official...</td>
      <td>-0.6486</td>
      <td>0.153</td>
      <td>0.288</td>
      <td>0.560</td>
    </tr>
    <tr>
      <th>491</th>
      <td>foodborne illness</td>
      <td>32verz</td>
      <td>all</td>
      <td>1.429261e+09</td>
      <td>ELI5:the reason why there is an incubation per...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>Usually, you're only eating a small number of ...</td>
      <td>0.1708</td>
      <td>0.119</td>
      <td>0.096</td>
      <td>0.785</td>
    </tr>
    <tr>
      <th>492</th>
      <td>foodborne illness</td>
      <td>xh5kc</td>
      <td>all</td>
      <td>1.343806e+09</td>
      <td>/r/news [spam filtered] As GOP Guts Food Safet...</td>
      <td>2</td>
      <td>http://readersupportednews.org/news-section2/3...</td>
      <td>1</td>
      <td>http://readersupportednews.org/news-section2/3...</td>
      <td>readersupportednews.org</td>
      <td>--- \n\n[As GOP Guts Food Safety Budgets Foodb...</td>
      <td>-0.3736</td>
      <td>0.076</td>
      <td>0.101</td>
      <td>0.823</td>
    </tr>
    <tr>
      <th>493</th>
      <td>foodborne illness</td>
      <td>1t3xg5</td>
      <td>all</td>
      <td>1.387337e+09</td>
      <td>ELI5: why is it that carrion-eaters can eat al...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>Robust GI tracts. Take a vulture: they've unus...</td>
      <td>0.8588</td>
      <td>0.391</td>
      <td>0.087</td>
      <td>0.522</td>
    </tr>
    <tr>
      <th>494</th>
      <td>foodborne illness</td>
      <td>6hp7j4</td>
      <td>all</td>
      <td>1.497674e+09</td>
      <td>What are my chances of getting a foodborne ill...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/NoStupidQuestions/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/NoStupidQuestions/com...</td>
      <td>self.NoStupidQuestions</td>
      <td>&gt; I didn't swallow any meat, but I'm afraid I ...</td>
      <td>-0.9231</td>
      <td>0.031</td>
      <td>0.170</td>
      <td>0.799</td>
    </tr>
    <tr>
      <th>495</th>
      <td>foodborne illness</td>
      <td>6hp7j4</td>
      <td>all</td>
      <td>1.497674e+09</td>
      <td>What are my chances of getting a foodborne ill...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/NoStupidQuestions/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/NoStupidQuestions/com...</td>
      <td>self.NoStupidQuestions</td>
      <td>If you didn't actually eat any of it, you'll b...</td>
      <td>0.2023</td>
      <td>0.153</td>
      <td>0.000</td>
      <td>0.847</td>
    </tr>
    <tr>
      <th>496</th>
      <td>foodborne illness</td>
      <td>4ijwsq</td>
      <td>all</td>
      <td>1.462835e+09</td>
      <td>Fighting Foodborne Illness Via Mobile App</td>
      <td>1</td>
      <td>http://www.foodqualityandsafety.com/article/fi...</td>
      <td>1</td>
      <td>http://www.foodqualityandsafety.com/article/fi...</td>
      <td>foodqualityandsafety.com</td>
      <td>FoodKeeper app gets updated to better educate ...</td>
      <td>0.4404</td>
      <td>0.182</td>
      <td>0.000</td>
      <td>0.818</td>
    </tr>
    <tr>
      <th>497</th>
      <td>foodborne illness</td>
      <td>18dgw0</td>
      <td>all</td>
      <td>1.360700e+09</td>
      <td>Death as a Foodborne Illness Curable by Veganism</td>
      <td>1</td>
      <td>http://www.sciencebasedmedicine.org/index.php/...</td>
      <td>1</td>
      <td>http://www.sciencebasedmedicine.org/index.php/...</td>
      <td>sciencebasedmedicine.org</td>
      <td>Before you immediately upvote because you agre...</td>
      <td>0.8126</td>
      <td>0.193</td>
      <td>0.091</td>
      <td>0.716</td>
    </tr>
    <tr>
      <th>498</th>
      <td>foodborne illness</td>
      <td>4296mr</td>
      <td>all</td>
      <td>1.453549e+09</td>
      <td>Chipotle Tried To Cover Up Foodborne Illness O...</td>
      <td>1</td>
      <td>http://thinkprogress.org/health/2016/01/22/374...</td>
      <td>1</td>
      <td>http://thinkprogress.org/health/2016/01/22/374...</td>
      <td>thinkprogress.org</td>
      <td>This is the best tl;dr I could make, [original...</td>
      <td>-0.7906</td>
      <td>0.047</td>
      <td>0.093</td>
      <td>0.860</td>
    </tr>
    <tr>
      <th>499</th>
      <td>foodborne illness</td>
      <td>817vsf</td>
      <td>all</td>
      <td>1.519961e+09</td>
      <td>Salmonella outbreak linked to raw sprouts appe...</td>
      <td>1</td>
      <td>https://www.foodsafety.gov/keep/types/fruits/s...</td>
      <td>1</td>
      <td>https://www.foodsafety.gov/keep/types/fruits/s...</td>
      <td>foodsafety.gov</td>
      <td>people are getting sick because they arent rin...</td>
      <td>-0.5106</td>
      <td>0.000</td>
      <td>0.125</td>
      <td>0.875</td>
    </tr>
    <tr>
      <th>500</th>
      <td>foodborne illness</td>
      <td>3cpud7</td>
      <td>all</td>
      <td>1.436503e+09</td>
      <td>[#16|+2939|526] TIL that after San Francisco's...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>1</td>
      <td>http://www.reddit.com/r/todayilearned/comments...</td>
      <td>reddit.com</td>
      <td>\n\nSnapshots:\n\n1. *This Post* - [1](https:/...</td>
      <td>-0.4574</td>
      <td>0.000</td>
      <td>0.143</td>
      <td>0.857</td>
    </tr>
    <tr>
      <th>501</th>
      <td>foodborne illness</td>
      <td>3r97gd</td>
      <td>all</td>
      <td>1.446524e+09</td>
      <td>ELI5: Foodborne illnesses being more prevalent...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>I mean, you have a small sample, so to make th...</td>
      <td>-0.1423</td>
      <td>0.072</td>
      <td>0.067</td>
      <td>0.862</td>
    </tr>
    <tr>
      <th>502</th>
      <td>foodborne illness</td>
      <td>3r97gd</td>
      <td>all</td>
      <td>1.446524e+09</td>
      <td>ELI5: Foodborne illnesses being more prevalent...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>2</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>There are other possibilities.\n\nChipotle is ...</td>
      <td>0.6908</td>
      <td>0.053</td>
      <td>0.000</td>
      <td>0.947</td>
    </tr>
    <tr>
      <th>503</th>
      <td>foodborne illness</td>
      <td>379pxq</td>
      <td>all</td>
      <td>1.432630e+09</td>
      <td>ELI5: Why have large-scale outbreaks of foodbo...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/explainlikeimfive/com...</td>
      <td>self.explainlikeimfive</td>
      <td>They haven't. They've become radically less co...</td>
      <td>-0.4767</td>
      <td>0.000</td>
      <td>0.114</td>
      <td>0.886</td>
    </tr>
    <tr>
      <th>504</th>
      <td>foodborne illness</td>
      <td>6de1vs</td>
      <td>all</td>
      <td>1.495792e+09</td>
      <td>I wonder if raisins have a higher on average r...</td>
      <td>0</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>1</td>
      <td>https://www.reddit.com/r/Showerthoughts/commen...</td>
      <td>self.Showerthoughts</td>
      <td>Asking the important questions is how we get t...</td>
      <td>0.7003</td>
      <td>0.362</td>
      <td>0.000</td>
      <td>0.638</td>
    </tr>
    <tr>
      <th>505</th>
      <td>foodborne illness</td>
      <td>305e55</td>
      <td>all</td>
      <td>1.427245e+09</td>
      <td>Shower In The Sink - the simple and effective ...</td>
      <td>0</td>
      <td>http://kck.st/1Cmzg0R</td>
      <td>1</td>
      <td>http://kck.st/1Cmzg0R</td>
      <td>kck.st</td>
      <td>You should have posted this:\n\nhttp://showeri...</td>
      <td>0.0000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>506</th>
      <td>foodborne illness</td>
      <td>1uzxu9</td>
      <td>all</td>
      <td>1.389517e+09</td>
      <td>10 Horrifying Effects Of Foodborne Illnesses</td>
      <td>0</td>
      <td>http://listverse.com/2014/01/11/10-horrifying-...</td>
      <td>1</td>
      <td>http://listverse.com/2014/01/11/10-horrifying-...</td>
      <td>listverse.com</td>
      <td>This is horrifying!! especially the mold on th...</td>
      <td>0.3147</td>
      <td>0.264</td>
      <td>0.163</td>
      <td>0.573</td>
    </tr>
    <tr>
      <th>507</th>
      <td>foodborne illness</td>
      <td>2x4q60</td>
      <td>all</td>
      <td>1.424914e+09</td>
      <td>Agencies develop new model for foodborne illne...</td>
      <td>0</td>
      <td>http://www.foodsafetynews.com/2015/02/federal-...</td>
      <td>1</td>
      <td>http://www.foodsafetynews.com/2015/02/federal-...</td>
      <td>foodsafetynews.com</td>
      <td>I am RelatedBot and I've found some related po...</td>
      <td>-0.4767</td>
      <td>0.051</td>
      <td>0.121</td>
      <td>0.828</td>
    </tr>
  </tbody>
</table>
<p>508 rows × 15 columns</p>
</div>




```python
grouped_df7 = grouped_df7.groupby(['Created Date','Submission ID'])
```


```python
grouped_df7.count().head()
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
      <th>1.266202e+09</th>
      <th>b1zip</th>
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
    <tr>
      <th>1.267744e+09</th>
      <th>b97hk</th>
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
    <tr>
      <th>1.280168e+09</th>
      <th>ctqwc</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1.292852e+09</th>
      <th>eom2a</th>
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
    <tr>
      <th>1.325334e+09</th>
      <th>nx4mp</th>
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
  </tbody>
</table>
</div>




```python
grouped_df7 = pd.DataFrame(grouped_df7["Compound Score"].mean())
grouped_df7
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
      <th>1.266202e+09</th>
      <th>b1zip</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.267744e+09</th>
      <th>b97hk</th>
      <td>-0.493900</td>
    </tr>
    <tr>
      <th>1.280168e+09</th>
      <th>ctqwc</th>
      <td>-0.080333</td>
    </tr>
    <tr>
      <th>1.292852e+09</th>
      <th>eom2a</th>
      <td>-0.648600</td>
    </tr>
    <tr>
      <th>1.325334e+09</th>
      <th>nx4mp</th>
      <td>-0.064325</td>
    </tr>
    <tr>
      <th>1.333135e+09</th>
      <th>rkrmx</th>
      <td>-0.387200</td>
    </tr>
    <tr>
      <th>1.337598e+09</th>
      <th>twxww</th>
      <td>0.401900</td>
    </tr>
    <tr>
      <th>1.337948e+09</th>
      <th>u3z8b</th>
      <td>0.170000</td>
    </tr>
    <tr>
      <th>1.340041e+09</th>
      <th>v7v3c</th>
      <td>-0.266900</td>
    </tr>
    <tr>
      <th>1.343806e+09</th>
      <th>xh5kc</th>
      <td>-0.373600</td>
    </tr>
    <tr>
      <th>1.346346e+09</th>
      <th>z2i5y</th>
      <td>-0.421500</td>
    </tr>
    <tr>
      <th>1.351147e+09</th>
      <th>1215r7</th>
      <td>-0.548967</td>
    </tr>
    <tr>
      <th>1.354105e+09</th>
      <th>13wzwt</th>
      <td>0.188200</td>
    </tr>
    <tr>
      <th>1.359666e+09</th>
      <th>17mkhy</th>
      <td>-0.525475</td>
    </tr>
    <tr>
      <th>1.360576e+09</th>
      <th>18a4hq</th>
      <td>0.570350</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.360700e+09</th>
      <th>18dgw0</th>
      <td>0.812600</td>
    </tr>
    <tr>
      <th>18dgwk</th>
      <td>0.370150</td>
    </tr>
    <tr>
      <th>1.366831e+09</th>
      <th>1d03yl</th>
      <td>-0.271150</td>
    </tr>
    <tr>
      <th>1.381238e+09</th>
      <th>1nyque</th>
      <td>-0.419500</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">1.381249e+09</th>
      <th>1nyzbc</th>
      <td>-0.101820</td>
    </tr>
    <tr>
      <th>1nyzm7</th>
      <td>-0.145733</td>
    </tr>
    <tr>
      <th>1nyzos</th>
      <td>-0.120850</td>
    </tr>
    <tr>
      <th>1.381265e+09</th>
      <th>1nzair</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.381270e+09</th>
      <th>1nzg8m</th>
      <td>0.035823</td>
    </tr>
    <tr>
      <th>1.381286e+09</th>
      <th>1o031r</th>
      <td>0.522800</td>
    </tr>
    <tr>
      <th>1.387337e+09</th>
      <th>1t3xg5</th>
      <td>0.858800</td>
    </tr>
    <tr>
      <th>1.389517e+09</th>
      <th>1uzxu9</th>
      <td>0.314700</td>
    </tr>
    <tr>
      <th>1.400833e+09</th>
      <th>26994g</th>
      <td>0.401900</td>
    </tr>
    <tr>
      <th>1.403826e+09</th>
      <th>295o4y</th>
      <td>-0.685300</td>
    </tr>
    <tr>
      <th>1.405889e+09</th>
      <th>2b7foq</th>
      <td>-0.250000</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1.476660e+09</th>
      <th>57rvhb</th>
      <td>-0.159125</td>
    </tr>
    <tr>
      <th>1.478361e+09</th>
      <th>5b8xzo</th>
      <td>0.624900</td>
    </tr>
    <tr>
      <th>1.478581e+09</th>
      <th>5boqr7</th>
      <td>-0.088950</td>
    </tr>
    <tr>
      <th>1.480503e+09</th>
      <th>5fn5j9</th>
      <td>-0.110275</td>
    </tr>
    <tr>
      <th>1.480634e+09</th>
      <th>5fx25a</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.481693e+09</th>
      <th>5i695a</th>
      <td>0.329100</td>
    </tr>
    <tr>
      <th>5i69r4</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.482640e+09</th>
      <th>5k4vdo</th>
      <td>-0.280243</td>
    </tr>
    <tr>
      <th>1.487806e+09</th>
      <th>5vjb9l</th>
      <td>0.064711</td>
    </tr>
    <tr>
      <th>1.488109e+09</th>
      <th>5w88pb</th>
      <td>-0.465183</td>
    </tr>
    <tr>
      <th>1.488477e+09</th>
      <th>5x2dg0</th>
      <td>0.137584</td>
    </tr>
    <tr>
      <th>1.488490e+09</th>
      <th>5x35j3</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.488574e+09</th>
      <th>5xa5wo</th>
      <td>-0.368200</td>
    </tr>
    <tr>
      <th>1.489625e+09</th>
      <th>5zkhrj</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.493352e+09</th>
      <th>67y50k</th>
      <td>-0.485711</td>
    </tr>
    <tr>
      <th>1.494219e+09</th>
      <th>69toqq</th>
      <td>-0.817600</td>
    </tr>
    <tr>
      <th>1.495792e+09</th>
      <th>6de1vs</th>
      <td>0.700300</td>
    </tr>
    <tr>
      <th>1.497674e+09</th>
      <th>6hp7j4</th>
      <td>-0.360400</td>
    </tr>
    <tr>
      <th>1.498122e+09</th>
      <th>6iq51j</th>
      <td>-0.091067</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1.500426e+09</th>
      <th>6o21s6</th>
      <td>-0.130814</td>
    </tr>
    <tr>
      <th>6o2355</th>
      <td>-0.072946</td>
    </tr>
    <tr>
      <th>1.504085e+09</th>
      <th>6wvusd</th>
      <td>0.037775</td>
    </tr>
    <tr>
      <th>1.510489e+09</th>
      <th>7cdcit</th>
      <td>0.136974</td>
    </tr>
    <tr>
      <th>1.513823e+09</th>
      <th>7l3bej</th>
      <td>-0.544700</td>
    </tr>
    <tr>
      <th>1.518183e+09</th>
      <th>7wbd28</th>
      <td>-0.070083</td>
    </tr>
    <tr>
      <th>1.519640e+09</th>
      <th>809izw</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1.519686e+09</th>
      <th>80dn9o</th>
      <td>-0.203000</td>
    </tr>
    <tr>
      <th>1.519961e+09</th>
      <th>817vsf</th>
      <td>-0.510600</td>
    </tr>
    <tr>
      <th>1.520029e+09</th>
      <th>81eiej</th>
      <td>0.549900</td>
    </tr>
    <tr>
      <th>1.520921e+09</th>
      <th>83z1bd</th>
      <td>-0.215257</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 1 columns</p>
</div>




```python
grouped_df7 = grouped_df7.reset_index()
grouped_df7.head()
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
      <td>1.266202e+09</td>
      <td>b1zip</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.267744e+09</td>
      <td>b97hk</td>
      <td>-0.493900</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.280168e+09</td>
      <td>ctqwc</td>
      <td>-0.080333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.292852e+09</td>
      <td>eom2a</td>
      <td>-0.648600</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.325334e+09</td>
      <td>nx4mp</td>
      <td>-0.064325</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sns.set()
sns.lmplot(x='Created Date', y='Compound Score', data=grouped_df7, fit_reg=False, palette="Paired")

#plt.title("foodborne illness Comment Sentiments on Reddit")

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

plt.savefig("foodborne_illness_Sentiments.png", dpi=350)

plt.show()
```


![png](output_80_0.png)



```python
reddit_comments_df.to_csv("foodborne_kws.csv",
                     encoding="utf-8", index=False)
```


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

    plt.savefig("foodborn_kws.png", dpi=350)

    plt.show()
    
```


![png](output_83_0.png)



![png](output_83_1.png)



![png](output_83_2.png)



![png](output_83_3.png)



![png](output_83_4.png)



![png](output_83_5.png)


food poisoning       7259
e. coli              5991
food allergy         5512
salmonella           4042
Norovirus            2546
foodborne illness     508
