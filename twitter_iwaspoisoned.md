

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

public_tweets = api.search(target, count=1500000)

#for tweet in public_tweets['statuses']:
#    print(tweet)
#    date_list.append(tweet['created_at'])
#    tweet_list.append(tweet['text'])
    
        
for status in tweepy.Cursor(api.user_timeline, screen_name='@realDonaldTrump').items():
    print status._json['text']    

#len(tweet_list)
```


      File "<ipython-input-36-ae734e7d5048>", line 14
        print status._json['text']
                   ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(int status._json['text'])?




```python
def get_all_tweets(screen_name):
    
    alltweets=[]
    new_tweets=api.user_timeline(screen_name, count=200)
    alltweets.extend(new_tweets)
#    print(alltweets)
    oldest=alltweets[-1]['id']
    
    while len(new_tweets)>0:
        new_tweets=api.user_timeline(screen_name = screen_name,count=200,max_id=oldest)
        alltweets.extend(new_tweets)
        oldest=alltweets[-1]['id']
    
    outtweets = [[tweet.id_str, tweet.created_at, tweet.text.encode("utf-8")] for tweet in alltweets]    
    
    with open('iwaspoisoned.csv') as f:
        writer=csv.writer(f)
        writer.writerow(['id','created_at','text'])
        writer.writerows(outtweets)

get_all_tweets('@iwaspoisoned_')
```


    ---------------------------------------------------------------------------

    RateLimitError                            Traceback (most recent call last)

    <ipython-input-28-eb0147ceddfd> in <module>()
         19         writer.writerows(outtweets)
         20 
    ---> 21 get_all_tweets('@iwaspoisoned_')
    

    <ipython-input-28-eb0147ceddfd> in get_all_tweets(screen_name)
          8 
          9     while len(new_tweets)>0:
    ---> 10         new_tweets=api.user_timeline(screen_name = screen_name,count=200,max_id=oldest)
         11         alltweets.extend(new_tweets)
         12         oldest=alltweets[-1]['id']


    ~/anaconda3/lib/python3.6/site-packages/tweepy/binder.py in _call(*args, **kwargs)
        248             return method
        249         else:
    --> 250             return method.execute()
        251 
        252     # Set pagination mode


    ~/anaconda3/lib/python3.6/site-packages/tweepy/binder.py in execute(self)
        230 
        231                 if is_rate_limit_error_message(error_msg):
    --> 232                     raise RateLimitError(error_msg, resp)
        233                 else:
        234                     raise TweepError(error_msg, resp, api_code=api_error_code)


    RateLimitError: [{'message': 'Rate limit exceeded', 'code': 88}]

