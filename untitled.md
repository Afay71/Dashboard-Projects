## libraries

Required libraries are being loaded.

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import math 
import random
```

## reading data
```python
data = pd.DataFrame(pd.read_csv("C:\\Users\\Arif Furkan\\OneDrive\\Belgeler\\Python_kullanirken\\Ads_CTR_Optimisation.csv"))
print(data)
```

## Random Selection

In the loop, a random ad is selected with the random.randrange(d) function and this ad is added to the chosen list. The reward (click) of the selected ad is added to the total variable. Finally, the total reward and histogram are shown.

```python
N = 10000
d = 10
total = 0
chosen = []
for n in range(0,N):
    ad = random.randrange(d)
    chosen.append(ad)
    award = data.values[n,ad]
    total = total + award
print('Toplam Odul:') 
print(total)

plt.hist(chosen)
plt.show()
```

## UCB

At first, each ad is assigned ucb = N*10 until it is selected at least once. The ad with the maximum UCB value is selected and added to the chosen list. The number of clicks and rewards for the selected ad are updated. Finally, the total reward and histogram are shown.

```python
N=10000
d=10
awards = [0] * d
clicks=[0] * d
total = 0 
chosen = []
for n in range(1,N):
    ad = 0 
    max_ucb = 0
    for i in range(0,d):
        if(clicks[i] > 0):
            ortalama = awards[i] / clicks[i]
            delta = math.sqrt(3/2* math.log(n)/clicks[i])
            ucb = ortalama + delta
        else:
            ucb = N*10
        if max_ucb < ucb: 
            max_ucb = ucb
            ad = i          
    chosen.append(ad)
    clicks[ad] = clicks[ad]+ 1
    award = data.values[n,ad] 
    awards[ad] = awards[ad]+ award
    total = total + award
print('Toplam Odul:')   
print(total)

import math
```

## UCB-2

```python
N = 10000 
d = 10  
#Ri(n)
awards = [0] * d 
#Ni(n)
clicks = [0] * d 
total = 0 
chosen = []
for n in range(1,N):
    ad = 0 
    max_ucb = 0
    for i in range(0,d):
        if(clicks[i] > 0):
            ortalama = awards[i] / clicks[i]
            delta = math.sqrt(3/2* math.log(n)/clicks[i])
            ucb = ortalama + delta
        else:
            ucb = N*10
        if max_ucb < ucb: 
            max_ucb = ucb
            ad = i          
    chosen.append(ad)
    clicks[ad] = clicks[ad]+ 1
    award = data.values[n,ad] 
    awards[ad] = awards[ad]+ award
    total = total + award
print('Toplam Odul:')   
print(total)

plt.hist(chosen)
plt.show()
```

## General Operation of the Code
The first part of the code performs ad optimization by random selection. The second part of the code uses the Upper Confidence Interval algorithm to make smarter choices and try to maximize the click-through rate of ads. It shows the distribution and total reward of ads selected at the end of both algorithms.