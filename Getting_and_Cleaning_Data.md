# Getting and Cleaning Data

### How do I read a csv file?

We are using the iris dataset hosted on Github by [Vincent Arel-Bundock](http://vincentarelbundock.github.io/Rdatasets/datasets.html).

R:

```r
url = "http://vincentarelbundock.github.io/Rdatasets/csv/datasets/iris.csv"
download.file(url, "iris.csv", quiet=TRUE)
iris <- read.csv("iris.csv", header=TRUE, stringsAsFactors=FALSE)
head(iris, 3)
```

```
##   X Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1 1          5.1         3.5          1.4         0.2  setosa
## 2 2          4.9         3.0          1.4         0.2  setosa
## 3 3          4.7         3.2          1.3         0.2  setosa
```

Python:

```python
import pandas as pd
import urllib
url = "http://vincentarelbundock.github.io/Rdatasets/csv/datasets/iris.csv"
urllib.urlretrieve(url, "iris.csv")
iris = pd.read_csv("iris.csv", header=0)
print iris.head(n=3)
```

```
##    Unnamed: 0  Sepal.Length  Sepal.Width  Petal.Length  Petal.Width Species
## 0           1           5.1          3.5           1.4          0.2  setosa
## 1           2           4.9          3.0           1.4          0.2  setosa
## 2           3           4.7          3.2           1.3          0.2  setosa
```

### How do I read an Excel(xlsx) file?

We are using the iris dataset saved in the Excel xlsx format.

Using the xlsx package in R (requires Java JRE to be installed):

```r
library(xlsx)
```

```
## Loading required package: rJava
## Loading required package: xlsxjars
```

```r
library(httr)
url <- "https://rawgit.com/yoke2/dsxref/master/iris.xlsx"
# note that we are handling HTTPS connection using httr package.
GET(url, write_disk("iris.xlsx", overwrite=TRUE))
```

```
## Response [https://raw.githubusercontent.com/yoke2/dsxref/master/iris.xlsx]
##   Date: 2015-03-07 00:23
##   Status: 200
##   Content-Type: application/octet-stream
##   Size: 14.1 kB
## <ON DISK>  iris.xlsx
```

```r
iris <- read.xlsx("iris.xlsx", sheetIndex=1, header=TRUE)
head(iris, 3)
```

```
##   NA. Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1   1          5.1         3.5          1.4         0.2  setosa
## 2   2          4.9         3.0          1.4         0.2  setosa
## 3   3          4.7         3.2          1.3         0.2  setosa
```

Using the readxl package in R (no external dependencies):


```r
library(readxl)
library(httr)
url <- "https://rawgit.com/yoke2/dsxref/master/iris.xlsx"
GET(url, write_disk("iris.xlsx", overwrite=TRUE))
```

```
## Response [https://raw.githubusercontent.com/yoke2/dsxref/master/iris.xlsx]
##   Date: 2015-04-07 00:03
##   Status: 200
##   Content-Type: application/octet-stream
##   Size: 14.1 kB
## <ON DISK>  iris.xlsx
```

```r
iris <- read_excel("iris.xlsx")
head(iris, 3)
```

```
##     Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1 1          5.1         3.5          1.4         0.2  setosa
## 2 2          4.9         3.0          1.4         0.2  setosa
## 3 3          4.7         3.2          1.3         0.2  setosa
```

Python:

```python
import pandas as pd
import urllib
url = "https://rawgit.com/yoke2/dsxref/master/iris.xlsx"
urllib.urlretrieve(url, "iris.xlsx")
iris = pd.read_excel("iris.xlsx", sheetname=0, header=0)
print iris.head(n=3)
```

```
##    Sepal.Length  Sepal.Width  Petal.Length  Petal.Width Species
## 1           5.1          3.5           1.4          0.2  setosa
## 2           4.9          3.0           1.4          0.2  setosa
## 3           4.7          3.2           1.3          0.2  setosa
```

### How do I read a json file?

We are using [JSONPlaceHolder](http://jsonplaceholder.typicode.com/) to simulate JSON dataset.

R:

```r
library(jsonlite)
```

```
## 
## Attaching package: 'jsonlite'
## 
## The following object is masked from 'package:utils':
## 
##     View
```

```r
url <- "http://jsonplaceholder.typicode.com/users"
data <- fromJSON(url)
head(data, 3)
```

```
##   id             name  username              email    address.street
## 1  1    Leanne Graham      Bret  Sincere@april.biz       Kulas Light
## 2  2     Ervin Howell Antonette  Shanna@melissa.tv     Victor Plains
## 3  3 Clementine Bauch  Samantha Nathan@yesenia.net Douglas Extension
##   address.suite  address.city address.zipcode address.geo.lat
## 1      Apt. 556   Gwenborough      92998-3874        -37.3159
## 2     Suite 879   Wisokyburgh      90566-7771        -43.9509
## 3     Suite 847 McKenziehaven      59590-4157        -68.6102
##   address.geo.lng                 phone       website       company.name
## 1         81.1496 1-770-736-8031 x56442 hildegard.org    Romaguera-Crona
## 2        -34.4618   010-692-6593 x09125 anastasia.net       Deckow-Crist
## 3        -47.0653        1-463-123-4447   ramiro.info Romaguera-Jacobson
##                      company.catchPhrase                       company.bs
## 1 Multi-layered client-server neural-net      harness real-time e-markets
## 2         Proactive didactic contingency synergize scalable supply-chains
## 3      Face to face bifurcated interface  e-enable strategic applications
```

Python:

```python
import pandas as pd
import requests
url = "http://jsonplaceholder.typicode.com/users"
response = requests.get(url)
data = response.json()
df = pd.io.json.json_normalize(data)
print df.head(n=3)
```

```
##     address.city address.geo.lat address.geo.lng     address.street  \
## 0    Gwenborough        -37.3159         81.1496        Kulas Light   
## 1    Wisokyburgh        -43.9509        -34.4618      Victor Plains   
## 2  McKenziehaven        -68.6102        -47.0653  Douglas Extension   
## 
##   address.suite address.zipcode                        company.bs  \
## 0      Apt. 556      92998-3874       harness real-time e-markets   
## 1     Suite 879      90566-7771  synergize scalable supply-chains   
## 2     Suite 847      59590-4157   e-enable strategic applications   
## 
##                       company.catchPhrase        company.name  \
## 0  Multi-layered client-server neural-net     Romaguera-Crona   
## 1          Proactive didactic contingency        Deckow-Crist   
## 2       Face to face bifurcated interface  Romaguera-Jacobson   
## 
##                 email  id              name                  phone   username  \
## 0   Sincere@april.biz   1     Leanne Graham  1-770-736-8031 x56442       Bret   
## 1   Shanna@melissa.tv   2      Ervin Howell    010-692-6593 x09125  Antonette   
## 2  Nathan@yesenia.net   3  Clementine Bauch         1-463-123-4447   Samantha   
## 
##          website  
## 0  hildegard.org  
## 1  anastasia.net  
## 2    ramiro.info
```

### How do I search and retrieve Tweets from Twitter? (via packages)

You will need Twitter developer account set up for consumer key, consumer secret, access token and access secret. We are using twitteR package in R and tweepy package in Python.

R:

```r
library(twitteR)
consumerKey <- readLines("twitterkey.txt")
consumerSecret <- readLines("twittersecret.txt")
accessToken <- readLines("twitteraccesstoken.txt")
accessTokenSecret <- readLines("twitteraccesstokensecret.txt")
```

```
## Warning in readLines("twitteraccesstokensecret.txt"): incomplete final
## line found on 'twitteraccesstokensecret.txt'
```

```r
setup_twitter_oauth(consumerKey,consumerSecret,accessToken,accessTokenSecret)
```

```
## [1] "Using direct authentication"
```

```r
tweets <- searchTwitter("#datascience", n=5)
tweetsDF <- twListToDF(tweets)
head(tweetsDF,3)
```

```
##                                                                                                                             text
## 1    Predictions, #DataScience #DataPrep join the tweetchat 3/11;11:00PST with @JulesMayhem @superlilia \nhttp://t.co/Fz71QSkZyh
## 2 RT @BigDataGal: #rstats #datascience Very gentle resource for speeding up R code http://t.co/SLtXqN3Crp http://t.co/pLXVUbVOiS
## 3                                                      We've been honored as a top #DataScience resource: http://t.co/ylfbjpRqLi
##   favorited favoriteCount replyToSN             created truncated
## 1     FALSE             1        NA 2015-03-06 16:22:39     FALSE
## 2     FALSE             0        NA 2015-03-06 16:21:53     FALSE
## 3     FALSE             0        NA 2015-03-06 16:20:42     FALSE
##   replyToSID                 id replyToUID
## 1         NA 573881388455211009         NA
## 2         NA 573881192182849536         NA
## 3         NA 573880897004511235         NA
##                                                                         statusSource
## 1 <a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>
## 2                 <a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>
## 3                    <a href="http://www.hootsuite.com" rel="nofollow">Hootsuite</a>
##    screenName retweetCount isRetweet retweeted     longitude    latitude
## 1        JAdP            0     FALSE     FALSE -122.51167131 37.52982376
## 2   civilstat            4      TRUE     FALSE          <NA>        <NA>
## 3 SmartDataCo            0     FALSE     FALSE          <NA>        <NA>
```

Python:

```python
import tweepy
import pandas as pd
file1 = open('twitterkey.txt', 'r')
file2 = open('twittersecret.txt', 'r')
file3 = open('twitteraccesstoken.txt', 'r')
file4 = open('twitteraccesstokensecret.txt', 'r')
consumerKey = file1.readline().strip()
consumerSecret = file2.readline().strip()
accessToken = file3.readline().strip()
accessTokenSecret = file4.readline().strip()

auth = tweepy.OAuthHandler(consumerKey, consumerSecret)
auth.set_access_token(accessToken, accessTokenSecret)
api = tweepy.API(auth)
tweets = api.search("datascience",rpp=10)
new = pd.DataFrame()
for tweet in tweets:
    new = new.append(pd.DataFrame.from_dict(tweet.__dict__,orient="index").transpose())
# some columns are in object form that requires more processing
print new.head(n=3)
```

```
##                                             _api  \
## 0  <tweepy.api.API object at 0x0000000006498550>   
## 0  <tweepy.api.API object at 0x0000000006498550>   
## 0  <tweepy.api.API object at 0x0000000006498550>   
## 
##                                                _json  \
## 0  {u'contributors': None, u'truncated': False, u...   
## 0  {u'contributors': None, u'truncated': False, u...   
## 0  {u'contributors': None, u'truncated': False, u...   
## 
##                                               author contributors  \
## 0  User(follow_request_sent=False, profile_use_ba...         None   
## 0  User(follow_request_sent=False, profile_use_ba...         None   
## 0  User(follow_request_sent=False, profile_use_ba...         None   
## 
##                                          coordinates           created_at  \
## 0  {u'type': u'Point', u'coordinates': [-122.5116...  2015-03-06 16:22:39   
## 0                                               None  2015-03-06 16:21:53   
## 0                                               None  2015-03-06 16:20:42   
## 
##                                             entities favorite_count favorited  \
## 0  {u'symbols': [], u'user_mentions': [{u'id': 34...              1     False   
## 0  {u'symbols': [], u'user_mentions': [{u'id': 89...              0     False   
## 0  {u'symbols': [], u'user_mentions': [], u'hasht...              0     False   
## 
##                                                  geo  \
## 0  {u'type': u'Point', u'coordinates': [37.529823...   
## 0                                               None   
## 0                                               None   
## 
##                          ...                          \
## 0                        ...                           
## 0                        ...                           
## 0                        ...                           
## 
##                                                place possibly_sensitive  \
## 0  Place(_api=<tweepy.api.API object at 0x0000000...              False   
## 0                                               None              False   
## 0                                               None              False   
## 
##   retweet_count retweeted                                   retweeted_status  \
## 0             0     False                                                NaN   
## 0             4     False  Status(contributors=None, truncated=False, tex...   
## 0             0     False                                                NaN   
## 
##                source                          source_url  \
## 0  Twitter for iPhone  http://twitter.com/download/iphone   
## 0  Twitter Web Client                  http://twitter.com   
## 0           Hootsuite            http://www.hootsuite.com   
## 
##                                                 text truncated  \
## 0  Predictions, #DataScience #DataPrep join the t...     False   
## 0  RT @BigDataGal: #rstats #datascience Very gent...     False   
## 0  We've been honored as a top #DataScience resou...     False   
## 
##                                                 user  
## 0  User(follow_request_sent=False, profile_use_ba...  
## 0  User(follow_request_sent=False, profile_use_ba...  
## 0  User(follow_request_sent=False, profile_use_ba...  
## 
## [3 rows x 29 columns]
```

### How do I test for NA/null values in a variable?


R:

```r
url = "http://vincentarelbundock.github.io/Rdatasets/csv/datasets/airquality.csv"
download.file(url, "airquality.csv", quiet=TRUE)
airquality <- read.csv("airquality.csv", header=TRUE, stringsAsFactors=FALSE)
table(is.na(airquality$Ozone))
```

```
## 
## FALSE  TRUE 
##   116    37
```

Python:

```python
import pandas as pd
import urllib
url = "http://vincentarelbundock.github.io/Rdatasets/csv/datasets/airquality.csv"
urllib.urlretrieve(url, "airquality.csv")
airquality = pd.read_csv("airquality.csv", header=0)
print pd.crosstab('Ozone',pd.isnull(airquality['Ozone']))
```

```
## Ozone  False  True 
## row_0              
## Ozone    116     37
```

