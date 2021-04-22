---
title: "Solving a partnership restructuring problem with linear algebra."
date: 2021-04-20T21:22:42-07:00
---

<br><br>

## Solving a partnership restructuring problem with linear algebra.

---

If you’d like to skip straight to the code, jump ahead to the end.

Let’s consider a partnership that is restructuring its assets, with N partners and M assets. The partners currently share the business at differing shares, for example, partner N1 owns 33% of the company, partner N2 owns 20%, and so on. Each of the M assets carries a current value and a debt owed. Our task is to re-distribute the ownerships of the assets such that each is owned outright by one of the partners. Critically, we need to divvy the assets up without altering the partners' ownership shares. In effect, we want to split up the partnership in a fair manner, preserving each partner's stake in the business.

Linear algebra - to the rescue! First, create an NxM probability matrix encoding the ownership percentages (for example, partner N1 gets 100% of asset M1, 0% of asset M2, etc.). Multiply the NxM probability matrix with the Mx2 matrix encoding the assets' values and the debts. Subtract the result from the current ownership shares (a Nx2 matrix) (making sure that the entries match up to the correct partner). Take the absolute values and sum the entries, encoding the cumulative differences between the restructured ownership shares and the partners' original ownership shares. We then shuffle the columns up, re-run the pipeline, and record the new cumulative difference. Do this for all the different permutations of the column order and voila, find out whether or not your restructured partnership can get close to the original one.

### How good can this search algorithm do?

---

And after all that, our result many turn out to be, well, pretty bad. Consider a simplified case: 2 partners own 3 assets shared evenly, but the assets are all equivalent, and, therefore, there is no way to split up the majority ownerships.

Another unattractive feature of our methodology was that we preemptively chose how many assets in total went to each partner, a step in the analytics pipeline that requires experimenting with. For example, in the matrix multiplications above, we decided that each partner got two properties. Some intuition must go into this initial decision after examining the original ownership stakes and the value/debts of the assets. This approach forces you to test all of the reasonable arrangements, which is only feasible for smaller order problems.

### When does this approach become unwieldy?

---

The approach is certainly a "brute force" method. The for loop through the permutations should theoretically be O(n) time complexity. However, the M! term mushrooms quickly, and your runtime can grow with large M accordingly, even though it’s a O(n) function. Let’s confirm that runtime is linearly proportional:

<img src="https://render.githubusercontent.com/render/math?math=\runtime \propto n">

<p align="center"> <img src="/assets-runtime.png"/ width = "450" height = "300"> </p>

**Figure 1.** Loglog plot of the runtime versus the number of loops through the function (i.e., for M assets we conduct M! loops). The loglog slope indicates the data’s power law exponent, which in this case, is equal to one (at least, for the second half).

### Appendix Code

---

<p align="center"> <img src="/assets-code.png"/ width = "550"> </p>


