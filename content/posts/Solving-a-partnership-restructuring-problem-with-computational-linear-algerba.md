---
title: "Solving a partnership restructuring problem with linear algebra and Markov processes."
date: 2021-04-20T21:22:42-07:00
---

<br><br>

## Solving a partnership restructuring problem with linear algebra and Markov processes.

---

Consider a partnership restructuring its assets. The N partners currently share each of the M assets at a particular percentage stake. The assets carry both a value and a debt. Our task is to re-distribute the assets such that each is under majority ownership by a single partner. Critically, we need to divvy the assets without altering the overall value and debt under each partner's stake. In effect, we want to split up the partnership fairly so that nobody gains or loses stake in the business.

Linear algebra - to the rescue!  We can explore the restructuring possibilities by turning the problem into a system of matrix operations and permuting across all the different asset ownership scenarios.

First, create an NxM matrix encoding the restructured shares, for example, partner N1 gets 100% of asset M1, 0% of asset M2, and so on. Each row represents a partner, each column represents an asset. As expected, each column must sum to one, hence the matrix is a probability matrix. If we think of each new structuring as a state, we are very much in the realm of [Markov processes](https://en.wikipedia.org/wiki/Markov_decision_process). We then multiply the NxM probability matrix with an Mx2 matrix encoding each of the assets' values and the debts. Subtract the result from the current ownership shares (a Nx2 matrix), making sure that the rows match up to the correct partner rows in the original probability matrix. Finally, we take the absolute values and sum the entries. Our result encodes the cumulative difference between the restructured partnership and the original ownerships.

$$
sum(abs(
\left[
\begin{array}{cccccc}
1 & 0 & 0 & 1 & 0 & 0 \\
0 & 1 & 0 & 0 & 1 & 0\\
0 & 0 & 1 & 0 & 0 & 1
\end{array}
\right]
\left[
\begin{array}{cc}
val_1 & debt_1 \\
val_2 & debt_2 \\
val_3 & debt_3 \\
val_4 & debt_4 \\
val_5 & debt_5 \\
val_6 & debt_6
\end{array}
\right]
-
\left[
\begin{array}{cc}
N_{1val} & N_{1debt}  \\
N_{2val} & N_{2debt} \\
N_{3val} & N_{3debt}
\end{array}
\right]
))
$$

**Figure 1**. System of matrix operations for a partnership with 6 assets and 3 partners. The first matrix is the probability Markov matrix, the second is the values/debts of each asset, and the third is the partner's total current ownership values/debts.   

The critical step in the algorithm is to then shuffle the columns, re-run the system of matrix operations, and record the next cumulative difference. We do this for all permutations of the column indices, search for the minimum difference (which may turn up more than once, if repeated permutations exist), and voila, we have an "optimal" solution.



### How close can we get to the original partnership?

---

Why was optimal in quotes above? Well, after all that, our result many turn out to be, well, not so great. Consider a simplified case: 2 partners evenly share 3 assets, but the assets are all equivalent, and, therefore, there is no way to split up the assets into majority stake ownerships.

Another unattractive feature of our methodology was that we preemptively chose how many assets in total went to each partner, a step in the analytics pipeline that requires experimenting with. Some intuition must go into this initial decision after examining the original ownership stakes and the assets' values and debts.

### When does this function's run-time become unwieldy?

---

This approach is certainly a brute force method, as we are testing across all the possible scenarios. I wouldn't want to run these calculations for more than a dozen or so assets, as the runtime would become quite large. The for loops should decompose roughly to a [O(n) time complexity](http://web.mit.edu/16.070/www/lecture/big_o.pdf). For example, if we have 11 assets (11! ~40 mill states), the runtime is approximately ten minutes on Google Colab's CPU.

$$runtime \propto n^{0.966}$$

<p align="center"> <img src="/posts/assets-runtime.png"/ width = "550" height = "366"> </p>

**Figure 2**. Run-time complexity analysis for the restructuring algorithm (in log/log space). The power law relationship exhibits a n ~ 0.996 slope, indicating the linearity in the algorithm's time complexity (i.e., O(n)).

### Code

---

<p align="center"> <img src="/posts/assets-code.png"/ width = "550" height = "636"> </p>
