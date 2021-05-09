---
title: "Solving a partnership restructuring problem with Markov processes."
date: 2021-04-20T21:22:42-07:00
katex: true
markup: "mmark"
---

<br><br>

## Solving a partnership restructuring problem with Markov processes.

---

Consider a partnership restructuring its assets. The N partners currently share each of the M assets at a given percentage. Our task is to re-distribute the assets such that each is under majority ownership. Critically, we need to divvy the assets without altering the overall value and debt associated with each partner. In effect, we want to split up the assets fairly.

Linear algebra - to the rescue!  We can explore the restructuring possibilities by turning the problem into a system of matrix operations and permuting across all the different  ownership scenarios.

First, create an NxM matrix encoding the restructured shares, for example, partner N1 gets 100% of asset M1, 0% of asset M2, and so on. Each row represents a partner, each column represents an asset. As expected, each column must sum to one, hence the matrix is a probability matrix. If we think of each new structuring as a state, we are very much in the realm of [Markov processes](https://en.wikipedia.org/wiki/Markov_decision_process). We then multiply the NxM probability matrix with an Mx2 matrix encoding each of the assets' values and the debts. Subtract the result from the current ownership shares (a Nx2 matrix), making sure that the rows match up to the correct partner rows in the original probability matrix. Finally, we take the absolute values and sum the entries. Our result encodes the cumulative difference between the restructured partnership and the original one.
<br><br>
<div>$$sum(abs(\left[\begin{array}{cccccc}1 & 0 & 0 & 1 & 0 & 0 \\0 & 1 & 0 & 0 & 1 & 0\\0 & 0 & 1 & 0 & 0 & 1\end{array}\right]\left[\begin{array}{cc}val_1 & debt_1 \\val_2 & debt_2 \\val_3 & debt_3 \\val_4 & debt_4 \\val_5 & debt_5 \\val_6 & debt_6\end{array}\right]-\left[\begin{array}{cc}N_{1val} & N_{1debt}  \\N_{2val} & N_{2debt} \\N_{3val} & N_{3debt}\end{array}\right]))$$</div>
<br>
**Figure 1**. System of matrix operations for a partnership with 6 assets and 3 partners. The first matrix is the probability Markov matrix, the second is the values/debts of each asset, and the third is the partner's total current ownership values/debts.   
<br><br>
The next step is to shuffle the columns by all the indices' permutations, while doing so, recording the cumulative differences for all of the possible restructurings. The best restructuring occurs at the global minimum (which may turn up more than once, if repeated permutations exist). Voila, we have an "optimal" solution.

### How close can we get to the original partnership?

---

Why was optimal in quotes above? Well, after all that, our result many turn out to be, well, not so great. Consider a simplified case: two partners evenly share three assets, but the assets are all equivalent, and, therefore, there is no way to split up the assets into majority stake ownerships.

Another unattractive feature of our methodology was that we preemptively chose how many assets in total went to each partner, a step in the analytics pipeline that requires experimenting with. Some intuition must go into this initial decision after examining the original ownership stakes and the assets' values and debts.

### When does this function's run-time become unwieldy?

---

This approach is certainly a brute force method, as we are testing across all the possible scenarios. I wouldn't want to run these calculations for more than a dozen or so assets, as the runtime would become quite large. The for loops should decompose roughly to a [O(n) time complexity](http://web.mit.edu/16.070/www/lecture/big_o.pdf). For example, if we have eleven assets (11! ~40 mill states), the runtime is approximately ten minutes on Google Colab's CPU.

$$runtime \propto n^{0.966}$$

<p align="center"> <img src="/posts/assets-runtime.png"/ width = "550" height = "366"> </p>

**Figure 2**. Run-time complexity analysis for the restructuring algorithm (in log/log space). The power law relationship exhibits a n ~ 0.996 slope, indicating the linearity in the algorithm's time complexity (i.e., O(n)).
<br><br>
### Code

---

<p align="center"> <img src="/posts/assets-code.png"/ width = "550" height = "636"> </p>

{{< highlight go "linenos=table,hl_lines=1 4 7,linenostart=1" >}}
// ### Libraries ###
import numpy as np
from sympy.utilities.iterables import multiset_permutations import time
### Data I/O ###
restructure_probabilities = np.genfromtext(...) # probability matrix assets_value_debt = np.genfromtext(...) # asset value/debt df previous_stake = np.genfromtext(...) # previous asset value/debt df num_assets = len(assets_value_debt[:,0]) # num of assets to restructure, M n_factorial = np.math.factorial(num_assets) # num of scenarios, M!
### Algorithm ###
start = time.time()
permutations = np.zeros((n_factorial, num_assets)) index = np.arange(0, num_assets)
iter = 0
# store all M permutations
for p in multiset_permutations(index):
    permutations[iter,:] = p
iter+=1
permutations = permutations.astype(int) results = np.zeros(n_factorial)
for iter in np.arange(0, n_factorial):
# shuffle columns
  probabilities_looped = restructure_probabilities[:, permutations[iter,:]]
  # Markov multiplication
  results_lopped = np.matmul(probabilities_looped, assets_value_debt)
  # difference between partnership states
final_differences = np.abs(results_lopped - previous_stake) results[iter] = np.sum(final_differences)
print(np.min(results)) # the optimal restructuring difference print(np.argmin(results))
end = time.time()
print(f"Runtime of the program is {end - start}")
{{< / highlight >}}
