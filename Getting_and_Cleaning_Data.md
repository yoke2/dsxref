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

R:

```r
library(xlsx)
library(httr)
url <- "https://rawgit.com/yoke2/dsxref/master/iris.xlsx"
# note that we are handling HTTPS connection using httr package.
GET(url, write_disk("iris.xlsx", overwrite=TRUE))
```

```
## Response [https://raw.githubusercontent.com/yoke2/dsxref/master/iris.xlsx]
##   Date: 2015-03-04 00:18
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
