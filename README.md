
# File Case
- This is used to cache the Dataframe result, even there are multiply Dataframe
- It also support to log the function time cost and parameters


## Installation
pip install file_cache

## Sample case


```python
from  file_cache.cache import file_cache
import numpy  as np
import pandas as pd

@file_cache()
def test_cache_normal(name):
    import time
    import numpy  as np
    time.sleep(3)
    return pd.DataFrame(data= np.arange(0,10).reshape(2,5))

normal_df = test_cache_normal('Felix')
normal_df.head()
```

  




<div>
 
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



## Return mulpiple DF with tuple
Support to cache multiple DF with tuple


```python
import time
from functools import lru_cache

@lru_cache()
@file_cache()
def test_cache_tuple(name):
    time.sleep(3)
    df0 = pd.DataFrame(data= np.arange(5,15).reshape(2,5))
    df1 = pd.DataFrame(data= np.arange(20,30).reshape(2,5))
    return df0, df1

df0, df1 = test_cache_tuple('Felix2')
print(df0 , '\n')
print(df1)
```

 

        0   1   2   3   4
    0   5   6   7   8   9
    1  10  11  12  13  14 
    
        0   1   2   3   4
    0  20  21  22  23  24
    1  25  26  27  28  29


## For the input paras can not be cached
If the input is DF or cannot be hashed, ignore the cache, run the function directly


```python
@file_cache()
def test_cache_ignore(name):
    df0 = pd.DataFrame(data= np.arange(5,15).reshape(2,5))
    return df0

df = pd.DataFrame(data= np.arange(5,15).reshape(2,5))
ignore = test_cache_ignore(df)

```

 
## Log the function time and parameter


```python
from file_cache.utils.util_log import *
@timed()
def log_time(arg):
    return f'{arg} msg'

print(log_time("hello"))
```

 
    hello msg

