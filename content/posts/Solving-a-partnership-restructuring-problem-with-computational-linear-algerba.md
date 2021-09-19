---
title: "Solving a partnership restructuring problem with Markov processes."
date: 2021-04-20T21:22:42-07:00
katex: true
markup: "mmark"
---

## Solving a partnership restructuring problem with Markov processes.

---

### Intro

Consider a partnership restructuring its assets into majority ownerships among N partners, who originally shared M assets (debt + value) at uneven percentages reflecting each partner's unique stake in the business. I aimed to re-distribute the assets without altering each partner's stake, minimizing restructuring taxes levied if the partnership structure significantly changed. 

In application, I used a Markov model to exhaustively search for solutions to a three partner/eleven asset case, testing over 200 million potential restructuring states. The optimal solution incurred a 2.9mm cumulative stake change against 159mm in total business assets, an acceptably small magnitude of change (<2%) that allows the client to effectively avoid significant restructuring taxes.

### Markov Algorithm

We can explore the restructuring possibilities by turning the problem into a system of matrix operations and permuting across majority ownership scenarios. First, create an NxM matrix encoding the restructured shares; for example, partner N1 gets 100% of asset M1, 0% of asset M2, and so on. Each row represents a partner, each column represents an asset. As expected, each column must sum to one, hence the matrix is a probability matrix. If we think of each new structuring as a state, we are very much in the realm of [Markov processes](https://en.wikipedia.org/wiki/Markov_decision_process). We then multiply the NxM probability matrix with an Mx2 matrix encoding each of the assets' values and the debts. Subtract the result from the current ownership shares (a Nx2 matrix), making sure that the rows match up to the correct partner rows in the original probability matrix. Finally, we take the absolute values and sum the entries. Our result encodes the cumulative difference between the restructured partnership and the original one. The for loop then iterates through all possible permutations of the column indices, recording the cumulative stake change for the M! potential restructurings. The best restructuring occurs at the minimum stake change, which may turn up more than once, if permutation states repeat.

<br><br>
<div>$$sum(abs(\left[\begin{array}{cccccc}1 & 0 & 0 & 1 & 0 & 0 \\0 & 1 & 0 & 0 & 1 & 0\\0 & 0 & 1 & 0 & 0 & 1\end{array}\right]\left[\begin{array}{cc}val_1 & debt_1 \\val_2 & debt_2 \\val_3 & debt_3 \\val_4 & debt_4 \\val_5 & debt_5 \\val_6 & debt_6\end{array}\right]-\left[\begin{array}{cc}N_{1val} & N_{1debt}  \\N_{2val} & N_{2debt} \\N_{3val} & N_{3debt}\end{array}\right]))$$</div>
<br>
**Figure 1**. System of matrix operations for a partnership with 6 assets and 3 partners. The first matrix is the probability Markov matrix, the second is the values/debts of each asset, and the third is the partner's total current ownership values/debts.   
<br><br>

### Model Flexibility

Why was optimal in quotes above? Well, after all that, our result may turn out to be, well, not so "optimal". Consider a simplified case: two partners evenly share three assets, but the assets are all equivalent, and, therefore, there is no way to split up the assets into majority stake ownerships. Due to this feature, I ran our Markov model across several majority ownership split scenarios, changing the total number of assets each partner is allowed to recieve. For example, in our real-world case, the optimal state was found by giving 4 properties to partner 1, 3 to partner 2, and 4 to partner 3, which was the fifth scenario tested.

The Markov model approach is by nature a brute force method, as we are testing across a huge number of possible scenarios. The for loops decompose to a [O(n) time complexity](http://web.mit.edu/16.070/www/lecture/big_o.pdf), yet the runtime can become large becuase we we are looping over M! states. For example, if we have eleven assets (11! ~40 mill states), the runtime is approximately ten minutes on CPU. 

$$runtime \propto n^{0.966}$$

<p align="center"> <img src="/posts/assets-runtime.png"/ width = "550" height = "366"> </p>

**Figure 2**. Run-time complexity analysis for the restructuring algorithm (in log/log space). The power law relationship exhibits a n ~ 0.996 slope, indicating the linearity in the algorithm's time complexity (i.e., O(n)).
<br><br>
### Code

---

```python
### Libraries ###
import numpy as np
from sympy.utilities.iterables import multiset_permutations
import time

### Data I/O ###
restructure_probabilities = np.genfromtext(...) # probability matrix
assets_value_debt = np.genfromtext(...) # asset value/debt df
previous_stake = np.genfromtext(...) # previous asset value/debt df
num_assets = len(assets_value_debt[:,0]) # num of assets to restructure, M
n_factorial = np.math.factorial(num_assets) # num of scenarios, M!

### Algorithm ###
start = time.time()
permutations = np.zeros((n_factorial, num_assets)) 
index = np.arange(0, num_assets) 
iter = 0
# store all M permutations
for p in multiset_permutations(index):
    permutations[iter,:] = p 
    iter+=1
permutations = permutations.astype(int)
results = np.zeros(n_factorial) 
for iter in np.arange(0, n_factorial):
  # shuffle columns
  probabilities_looped = restructure_probabilities[:, permutations[iter,:]]
  # Markov multiplication
  results_lopped = np.matmul(probabilities_looped, assets_value_debt)
  # difference between partnership states
  final_differences = np.abs(results_lopped - previous_stake)
  results[iter] = np.sum(final_differences)

print(np.min(results)) # the optimal restructuring difference
print(np.argmin(results))
end = time.time()
print(f"Runtime of the program is {end - start}")
```

---

