# Linear Algebra

### How do I create a matrix?

R:

```r
a <- matrix(c(1,2,3,11,12,13), nrow=2, ncol=3, byrow=TRUE) # fill values by row
a
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]   11   12   13
```

Python:

```python
import numpy as np
a = np.matrix([[1,2,3],[11,12,13]])
print a
```

```
## [[ 1  2  3]
##  [11 12 13]]
```

### How do I find the dimension of a matrix?

R:

```r
a <- matrix(c(1,2,3,11,12,13), nrow=2, ncol=3, byrow=TRUE) # fill values by row
dim(a) # shows row x column dimension
```

```
## [1] 2 3
```

Python:

```python
import numpy as np
a = np.matrix([[1,2,3],[11,12,13]])
print a.shape # shows row x column dimension
```

```
## (2L, 3L)
```


### How do I perform matrix multiplication?

R:

```r
a <- matrix(c(1,2,3), nrow=1)
b <- matrix(c(1,1,1), ncol=1)
a
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
```

```r
b
```

```
##      [,1]
## [1,]    1
## [2,]    1
## [3,]    1
```

```r
a%*%b
```

```
##      [,1]
## [1,]    6
```

Python:

```python
import numpy as np
a = np.matrix([1,2,3])
b = np.matrix([[1],[1],[1]])
print "a:"
print a
print "b:"
print b
print "a dot b"
print a*b
print "a dot b with numpy method"
print np.dot(a,b)
```

```
## a:
## [[1 2 3]]
## b:
## [[1]
##  [1]
##  [1]]
## a dot b
## [[6]]
## a dot b with numpy method
## [[6]]
```

### How do I transpose a matrix?

R:

```r
a <- matrix(c(1,2,3), nrow=1)
a
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
```

```r
t(a)
```

```
##      [,1]
## [1,]    1
## [2,]    2
## [3,]    3
```

Python:

```python
import numpy as np
a = np.matrix([1,2,3])
print a
print a.T
```

```
## [[1 2 3]]
## [[1]
##  [2]
##  [3]]
```

### How do I bind rows of vectors/matrices?

R:

```r
a <- matrix(c(1,2,3,11,12,13), nrow=2, byrow=TRUE)
b <- c(21,22,23)
a
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]   11   12   13
```

```r
b
```

```
## [1] 21 22 23
```

```r
rbind(a,b)
```

```
##   [,1] [,2] [,3]
##      1    2    3
##     11   12   13
## b   21   22   23
```

Python:

```python
import numpy as np
a = np.matrix([[1,2,3],[11,12,13]])
b = np.matrix([[21,22,23]])
print a
print b
print np.vstack((a,b))
```

```
## [[ 1  2  3]
##  [11 12 13]]
## [[21 22 23]]
## [[ 1  2  3]
##  [11 12 13]
##  [21 22 23]]
```

### How do I bind columns?

R:

```r
a <- matrix(c(1,11,2,12,3,13), nrow=3, ncol=2, byrow=TRUE)
b <- matrix(c(21,22,23), ncol=1)
a
```

```
##      [,1] [,2]
## [1,]    1   11
## [2,]    2   12
## [3,]    3   13
```

```r
b
```

```
##      [,1]
## [1,]   21
## [2,]   22
## [3,]   23
```

```r
cbind(a,b)
```

```
##      [,1] [,2] [,3]
## [1,]    1   11   21
## [2,]    2   12   22
## [3,]    3   13   23
```

Python:

```python
import numpy as np
a = np.matrix([[1,11],[2,12],[3,13]])
b = np.matrix([[21],[22],[23]])
print "a:"
print a
print "b:"
print b
print "after hstack:"
print np.hstack((a,b))
```

```
## a:
## [[ 1 11]
##  [ 2 12]
##  [ 3 13]]
## b:
## [[21]
##  [22]
##  [23]]
## after hstack:
## [[ 1 11 21]
##  [ 2 12 22]
##  [ 3 13 23]]
```
