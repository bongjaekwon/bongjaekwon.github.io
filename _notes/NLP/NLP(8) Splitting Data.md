---
title: NLP(8) Splitting Data
feed: show
date: 05-08-2024
---
#### Posting information

- Posting Date : 05-08-2024  
- Last Edit : 05-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_08 : Splitting Data

  

import pandas as pd

import numpy as np

from sklearn.model_selection import train_test_split

  

#Supervised Learning

  

'''

Mail label

last sale chance!... SPAM

Hello Pooh! Long time... OK

About your honey jar... OK

(Ad) Select you number... SPAM

'''

  

'''

<train data>

X_train : train data

y_train : train answer data

  

<test data>

X_test : test data

Y_test : test answer data

'''

  

# splitting X and Y

  

x, y = zip(['a', 1], ['b', 2], ['c', 3])

print('x data :', x)

print('y data :', y)

  

'''

x data : ('a', 'b', 'c')

y data : (1, 2, 3)

'''

  

sequences = (['a', 1], ['b', 2], ['c', 3])

x, y = zip(*sequences)

print('x data :', x)

print('y data :', y)

  

'''

x data : ('a', 'b', 'c')

y data : (1, 2, 3)

'''

  
  

#splitting by dataframe

  

columns = ['Mail', 'label']

values = [['last sale chance!...', 1],

['Hello Pooh! Long time...', 0],

['About your honey jar...', 0],

['(Ad) Select you number...', 1]]

  

df = pd.DataFrame(values, columns=columns)

df

  

print(df)

# Mail label

# 0 last sale chance!... 1

# 1 Hello Pooh! Long time... 0

# 2 About your honey jar... 0

# 3 (Ad) Select you number... 1

  
  

x = df['Mail']

y = df['label']

  

print('x :', x.to_list())

print('y :', y.to_list())

# x : ['last sale chance!...', 'Hello Pooh! Long time...', 'About your honey jar...', '(Ad) Select you number...']

# y : [1, 0, 0, 1]

  
  

#splitting by Numpy

  

np_array = np.arange(0,16).reshape(4,4)

print(np_array)

'''

[[ 0 1 2 3]

[ 4 5 6 7]

[ 8 9 10 11]

[12 13 14 15]]

'''

  

x = np_array[:, :3]

y = np_array[:,3]

  

print(x)

'''

[[ 0 1 2]

[ 4 5 6]

[ 8 9 10]

[12 13 14]]

'''

  

print(y)

#[ 3 7 11 15]
```