

```python
import tweepy
import json
import numpy as np
import pandas as pd
```


```python
from config import consumer_key, consumer_secret, access_token, access_token_secret

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth, parser=tweepy.parsers.JSONParser())
```


```python
target="@iwaspoisoned_"
date_list=[]
tweet_list=[]

public_tweets = api.user_timeline(target, count=2000)

for tweet in public_tweets:
#    print(tweet)
    date_list.append(tweet['created_at'])
    tweet_list.append(tweet['text'])

    
        
#for status in tweepy.Cursor(api.user_timeline, screen_name='@realDonaldTrump').items():
#    print status._json['text']    

len(tweet_list)
```




    200




```python
target="@iwaspoisoned_"
date_list=[]
tweet_list=[]

tweet_array = []
oldest_tweet = ""

for x in range(16):
    public_tweets = api.user_timeline(target,count=200)
#    print(len(public_tweets))
    for tweet in public_tweets:

        date_list.append(tweet['created_at'])
        tweet_array.append(tweet['text'])

        oldest_tweet = tweet["id_str"]

# Print total number of tweets
print(len(tweet_array))


```

    3200



```python
#tweet_array

df=pd.DataFrame(columns=['Date','Text','Venue','Location','City','State'])
df['Date']=date_list
df['Text']=tweet_array
for i,row in df.iterrows():
    df.iloc[i,2]=df.iloc[i,1].split(' - ')[0]
    df.iloc[i,3]=df.iloc[i,1].split(' - ')[1]
    df.iloc[i,4]=df.iloc[i,3].split(',')[0]
    df.iloc[i,5]=df.iloc[i,3].split(',')[1]

df_filtered=df[['Venue','City','State']]

```


```python
#pass to csv
df_filtered.to_csv('offenders.csv')
```


```python
offenders=[]
offenders=df_filtered['Venue'].value_counts()[1:11]
offenders
```




    Chipotle Mexican Grill    320
    McDonalds                 240
    Subway                    176
    Taco Bell                 144
    Wendy's                   128
    Domino's Pizza             96
    Burger King                80
    Costco                     80
    Popeyes                    80
    Panda Express              80
    Name: Venue, dtype: int64


