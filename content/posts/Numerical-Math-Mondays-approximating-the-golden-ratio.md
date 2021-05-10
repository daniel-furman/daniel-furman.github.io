---
title: "Numerical Math Mondays: Approximating the golden ratio."
date: 2021-05-10
katex: true
markup: "mmark"
---

## Numerical Math Mondays: Approximating the golden ratio.
---

The first in hopefully what will be many Numerical Math Mondays. My goal for this series of posts is to dive back into the numerical mathematics topics I learned during my undergraduate studies. I am a huge fan of [3blue1brown] (https://www.3blue1brown.com), and so, I am looking to pay particular attention to the visual side of the mathematics, as well as the computational.

I plan to repurpose my existing MATLAB programs across many different programming languages (Python, C++, R, and others). I am excited to explore the capabilities of [Facebook’s Transcoder AI software](https://ai.facebook.com/blog/deep-learning-to-translate-between-programming-languages/), which I am guessing will work great for some scripts and not so well for others. It’s worth noting that this series was in part inspired by the [Algorithm Archive](https://www.algorithm-archive.org), an open-source ebook
containing physical, mathematical, and computational algorithms implemented across dozens of programming languages.

<br><br>

### Introducing Fibonacci and the golden ratio
---

I will start with a favorite among math and science circles: approximating the golden ratio by taking ratios of consecutive terms in the Fibonacci sequence. This algorithm lets us peer into the underlying relationship between the Fibonacci sequence and the golden ratio, helping us understand the many interesting applications therein. For more reading on applications, see the appendix!

For a little background: What is the golden ratio anyways? Who was Fibonacci? The [golden ratio](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjVsumck77wAhVFLX0KHdj1Di0QFjAJegQIAxAD&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FGolden_ratio&usg=AOvVaw2xWnjTV-SdFz2WkhAdaL-s) is a mathematical phenomenon between two numbers, say, a and b. Let a > b, if the ratio of $$\frac{a}{b}$$ is the same as $$\frac{(a+b)}{a}$$, then the ratio is $$\frac{~1.618}{1}$$. This number is irrational, i.e., its decimal places never converge, classically denoted by the Greek  letter phi, $$\varphi$$. $$\varphi$$ is the positive root of the quadratic equation x$$^2$$ - x - 1 = 0. Upon solving the equation we obtain x = $$\frac{1 + 5^{0.5}}{2}$$.It was probably first discovered in Ancient Greece (likely through geometry, which the Greeks were quite into). Greek mathematicians determined $$\varphi$$ was an irrational number all the way back in the fifth century BC. 

Fibonacci numbers are closely related to the golden ratio, $$\varphi$$. The first two Fibonacci numbers are zero and one. Each consecutive term is the sum of the previous two, i.e., the third term is also one, because 0+1=1. The first few terms are (0, 1, 1, 2, 3, 5, 8, 13, 21). The ratio of consecutive terms closely mirrors $$\varphi$$, and the approximations get increasingly more accurate. Hmm, this seems like an important property if we, say, wanted to approximate the golden ratio!

<br><br>

### The algorithm
---

Lets cook up a simple sequence of operations exploiting the last feature of the Fibonacci numbers discussed above. We want to approximate $$\varphi$$ to a high degree of accuracy; thus, we will design the algorithm to run until we converge on [the computer’s epsilon ($$\varepsilon$$) error](https://en.wikipedia.org/wiki/Machine_epsilon), i.e., the smallest digit recorded by my 64-bit Mac. Upon running the algorithm, we find that it takes 39 iterations for the approximation errors to converge to $$\varepsilon$$.

<p align="center"> <img src="/posts/fib-errors.png"/ width = "550" height = "431"> </p>

**Figure 1**. The absolute error between our Fibonacci ratio approximation and the golden ratio itself. Notice that the errors trend towards zero, indicating that our approximations are getting closer and closer to the solution.

**Python implementation**:

```python
### Libraries ###
import numpy as np
import matplotlib.pyplot as plt

### Var Init ###
phi = (1+5**0.5)/2 # this is golden ratio
tol = 1e-16 #tolerance
fib, ratio, erval = list(), list(), list()
fib.extend([0,1,1])
erval.append(1)
n = 0 #iterator

### While Loop ###
while erval[n] >= tol:
    fib.append(fib[n+2]+fib[n+1]) # calculates next fib number
    ratio.append(fib[n+3]/fib[n+2]) # ratio between cons. terms
    erval.append(np.abs(ratio[n]-phi)) # absolute error
    n += 1

### Tests ###
assert erval[-1] == 0.0 # absolute error equal to 0.0
if ratio[-1] == phi:  # the golden ratio
    print('done')
```

<br><br>


### Appendix: More Reading
---

* A well written Pixa article on [photography and design applications of the golden ratio](https://www.pixpa.com/blog/golden-ratio). Is the golden ratio the genesis of photography’s rule of thirds? How close do natural patterns adhere to the golden ratio?

* A visualizations/applications oriented Ted talk on [using the Fibonacci numbers in magical ways](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjoi6TiiL7wAhUzFTQIHb2TAdgQtwIwA3oECAQQAw&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DSjSHVDfXHQ4&usg=AOvVaw2LofPkoDFw8s3EFUlOPdbe).

* The coolest golden ratio visualization application, IMO, is the [golden spiral](https://mathworld.wolfram.com/GoldenSpiral.html). Consider a rectangle whose length is the golden ratio $$\varphi$$ with height 1. Successive points that divide this "golden rectangle" into perfect squares fall on a logarithmic spiral with a growth factor equal to $$\varphi$$. 

<br><br>

### Appendix: More Code
---

**MATLAB implementation**:

```
format long e
clear all; clc; clf;
phi = (1+sqrt(5))/2; % the golden ratio
tol = eps; % computer epsilon error tolerance
z = ones(3,3);  
n = 2; %iterator
while z(n,3) >= tol
  n = n+1; 
  z(n,1) = z(n-1,1)+z(n-2,1); % nth Fibonacci
  z(n,2) = z(n,1)/z(n-1,1); % consecutive terms ratio
  z(n,3) = abs(z(n,2)-phi); % absolute error
end

fib = z(:,1);
ratio = z(:,2);
erval = z(:,3);

T = table(fib, ratio, erval)
```
