

```python
# Dependencies
import tweepy
import time
import yaml
```


```python
TWITTER_CONFIG_FILE = 'auth1.yaml'

with open(TWITTER_CONFIG_FILE, 'r') as config_file:
    config = yaml.load(config_file)
    
# Twitter API Keys
consumer_key = config['twitter']['consumer_key']
consumer_secret = config['twitter']['consumer_secret']
access_token = config['twitter']['access_token']
access_token_secret = config['twitter']['access_token_secret']
```


```python
# Twitter Credentials
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth, parser=tweepy.parsers.JSONParser())
```


```python
# Target Term
my_username = "JagTest1"
conversation_partner = "@JagathaTest2"
response_lines = [
                  #"%s Analyze user 1 %s" % (conversation_partner, "@CBS"),
                  #"%s Analyze user 2 %s" % (conversation_partner, "@BBC"),
                  #"%s Analyze user 4 %s" % (conversation_partner, "@nytimes"),
                  #"%s Analyze user 1 %s" % (conversation_partner, "@BarackObama"),
                  #"%s Analyze user (music) %s" % (conversation_partner, "@ladygaga"),
                  #"%s Analyze user (arts) %s" % (conversation_partner, "@ladygaga"),
                  #"%s Analyze user (politics) %s" % (conversation_partner, "@BarackObama"),
                  #"%s Analyze user (business) %s" % (conversation_partner, "@BillGates")
                  "%s Analyze User: %s" % (conversation_partner, "@ladygaga"),
                  "%s Analyze User: %s" % (conversation_partner, "@BarackObama"),
                  "%s Analyze User: %s" % (conversation_partner, "@BillGates"),
                  "%s Analyze User: %s" % (conversation_partner, "@realDonaldTrump")
                 ]
```


```python
# Create Tweet_Test function
def Tweet_Test(n):
    try:
        api.update_status(response_lines[n])
        print("Tweeted Successfully.")
    except tweepy.TweepError as e:
        print("Exception :"+ e.reason)
```


```python
# Set timer to run every 5 minutes
counter = 0

while(True):
    try:
        print("Iteration :"+str(counter+1))
        Tweet_Test(counter)
        time.sleep(300)
        counter = counter + 1
        if counter == 3:
            break
    except RuntimeError:
        print("Runtime Error.")
        pass
    finally:
        print("Executing finally clause.")
```

    Iteration :1
    Tweeted Successfully.
    Executing finally clause.
    Iteration :2
    Tweeted Successfully.
    Executing finally clause.
    Iteration :3
    Tweeted Successfully.
    Executing finally clause.
    
