# Random Number Generation

### How do I set the seed and generate random numbers of the normal distribution?

R:

```r
set.seed(39)
# generates 10 values with mean = 0, standard deviation = 1
rnorm(10, mean = 0, sd = 1) 
```

```
##  [1] -0.1855657 -1.2292427 -0.4272029 -0.5959819  0.4673236  0.4216390
##  [7] -1.0216521 -0.6224770  0.8370017  0.9616270
```

Python:

```python
import numpy as np
np.random.seed(seed=39)
# generates 10 values with mean = 0, standard deviation = 1
a = np.random.randn(10)
print a
```

```
## [ 1.40483957  0.22112104 -0.14532731  0.12319917  0.60602697  2.42277001
##  -1.91660854 -2.42252709  0.64629422  0.20150064]
```

### How do I generate random numbers of the uniform distribution?

R:

```r
set.seed(39)
# generates 10 values with mean = 0, standard deviation = 1
runif(10, min = 0, max = 1) 
```

```
##  [1] 0.4263927 0.2063405 0.1094904 0.0797075 0.3346158 0.7733796 0.2755937
##  [8] 0.4671497 0.6798658 0.4191414
```

Python:

```python
import numpy as np
np.random.seed(seed=39)
# generates 10 values with mean = 0, standard deviation = 1
a = np.random.uniform(low=0.0, high=1.0, size=10)
print a
```

```
## [ 0.54688916  0.79789902  0.82040188  0.12204987  0.60200201  0.52551458
##   0.46390841  0.47144574  0.63271284  0.92566388]
```
