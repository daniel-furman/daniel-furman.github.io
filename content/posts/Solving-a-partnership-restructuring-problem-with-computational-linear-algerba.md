---
title: "Solving a partnership restructuring problem with linear algebra and Markov processes."
date: 2021-04-20T21:22:42-07:00
---

<br><br>

## Solving a partnership restructuring problem with linear algebra and Markov processes.

---

Consider a partnership restructuring its assets. The N partners currently share each of the M assets at a particular percentage stake. The assets carry both a value and a debt. Our task is to re-distribute the assets such that each is under majority ownership by a single partner. Critically, we need to divvy the assets without altering the overall value and debt under each partner's stake. In effect, we want to split up the partnership fairly so that nobody gains or loses stake in the business.

Linear algebra - to the rescue!  We can explore the restructuring possibilities by turning the problem into a system of matrix multiplications and permuting across all the different asset ownership scenarios.

First, create an NxM matrix encoding the restructured shares, for example, partner N1 gets 100% of asset M1, 0% of asset M2, and so on. Each row represents a partner, each column represents an asset. As expected, each column must sum to one, hence the matrix is a probability matrix. If we think of each new structuring as a state, we are very much in the realm of [Markov processes](https://en.wikipedia.org/wiki/Markov_decision_process). We then multiply the NxM probability matrix with an Mx2 matrix encoding each of the assets' values and the debts. Subtract the result from the current ownership shares (a Nx2 matrix), making sure that the rows match up to the correct partner rows in the original probability matrix. Finally, we take the absolute values and sum the entries, a number which encodes the cumulative difference between the restructured partnership and the original. We now shuffle the columns, re-run the system of matrix multiplications, and record the next cumulative difference. Do this for all permutations of the columns, find the minimum difference, and voila, we have an "optimal" solution.

### How close can we get to the original partnership?

---

Why was optimal in quotes above? Well, after all that, our result many turn out to be, well, not so great. Consider a simplified case: 2 partners evenly share 3 assets, but the assets are all equivalent, and, therefore, there is no way to split up the assets into majority stake ownerships.

Another unattractive feature of our methodology was that we preemptively chose how many assets in total went to each partner, a step in the analytics pipeline that requires experimenting with. Some intuition must go into this initial decision after examining the original ownership stakes and the assets' values and debts.

### When does this function's run-time become unwieldy?

---

This approach is certainly a brute force method, as we are testing across all the possible scenarios. I wouldn't want to run these calculations for more than a dozen or so assets, as the runtime would become quite large. The for loops should decompose roughly to a [O(n) time complexity](). For example, if we have 11 assets (11! ~40 mill states), the runtime is approximately ten minutes on Google Colab's CPU.

<img src="https://render.githubusercontent.com/render/math?math=\runtime \propto n">

<p align="center"> <img src="/assets-runtime.png"/ width = "550" height = "366"> </p>

**Figure 1.** Run-time complexity analysis for the restructuring algorithm (in loglog space). The power law relationship falls on a n ~ 0.996 slope, indicating the linear O(n) complexity. This is the expected result, given the use of simple for loops within the function.

### Code

---

<p align="center"> <img src="/assets-code.png"/ width = "550" height = "747"> </p>
