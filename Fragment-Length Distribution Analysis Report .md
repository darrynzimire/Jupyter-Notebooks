### Introduction: Analysis report for modeling the fragment-length distributions of public RNA-seq data 

In this notebook I walk through fitting statistical distribution models to public RNA-sequencing data. The resulting models are used for simulating synthetic RNA-seq data. 



#### Imports 

The following standard data science, machine-learning and visualization libraries in Python will be used namely: Pandas, sklearn, numpy, scipy and matplotlib



```python
import numpy as np
import os
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler
from sklearn.mixture import GaussianMixture as GMM
from scipy.stats import norm

```




```python
samFile = ''
for file in os.listdir('.'):
    if file.endswith('.sam'):
        samFile = os.path.join('.', file)

FL = []
f = open(samFile, 'r')
for line in f:

    if line[0] != '@':
        parts = line.split('\t')
        TLEN = parts[8]
        FL.append(TLEN)

FL = list(map(int, FL))
FLS = FL.sort()
NEG = []
POS = []

for i in FL:
    if i < 0:
        NEG.append(i)
    else:
        POS.append(i)

data = np.array(POS)
datalog = np.log(data)
# datalog = datalog.reshape(-1, 1)
# print(type(datalog))
print(len(datalog))
```
