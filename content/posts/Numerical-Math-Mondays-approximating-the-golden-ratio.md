---
title: "Numerical Math Mondays: Approximating the golden ratio."
date: 2021-05-10T3:15
---

## Numerical Math Mondays: Approximating the golden ratio.
---

### Introduction
---

The first in hopefully what will be many Numerical Math Mondays. My goal for this series of posts is to dive back into my
numerical mathematics algorithms from my undergraduate studies. I am a huge fan of [3blue1brown] (https://www.3blue1brown.com),
and so, I am looking to pay particular attention to the visual side of the mathematics.

I plan to repurpose my existing MATLAB programs across many different programming languages (Python, C++, R, and others). I am
excited to explore the capabilities of [Facebook’s Transcoder AI software](
https://ai.facebook.com/blog/deep-learning-to-translate-between-programming-languages/), which I am guessing will work great for
some scripts and horribly for others (for example, where a language-specific package is heavily employed). It’s worth noting
that this series was in part inspired by the [Algorithm Archive](https://www.algorithm-archive.org), an open-source ebook
containing physical, mathematical, and computational algorithms implemented across dozens of programming languages.


### Fibonacci Approximation
—--

I will start with a favorite among math and science circles: approximating the golden ratio (phi) by taking ratios of
consecutive terms in the Fibonacci sequence. This algorithm lets us peer into the underlying relationship between the
Fibonacci sequence and the golden ratio, helping us understand the many interesting applications therein. For more
reading on applications, see the appendix!

For a little background: What is the golden ratio anyways? Who was Fibonacci? The [golden ratio](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjVsumck77wAhVFLX0KHdj1Di0QFjAJegQIAxAD&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FGolden_ratio&usg=AOvVaw2xWnjTV-SdFz2WkhAdaL-s) is a mathematical phenomenon between two numbers, say, $$a$$ and $$b$$. Let $$a > b$$,
if the ratio of $$a/b$$ is the same as $${(a+b)}/a$$, then the ratio is $${~1.618}/1$$. This number is irrational (it
has decimal places that go on to infinity) and is classically denoted by the Greek  letter phi, $$/phi$$. It was probably
first discovered in Ancient Greece (likely via geometric analyses). For example, by the fifth century BC, mathematicians
determined $$phi$$ was an irrational number.

* It’s worth noting, $$/phi$$ is precisely the positive root of the quadratic equation $$x^2 - x - 1 = 0$$. Upon solving the equation we obtain $$x = {1 + 5^{0.5}}/2

Fibonacci numbers are closely related to the golden ratio, $$/phi$$. The first two Fibonacci numbers are zero and one. Each consecutive term is the sum of the previous two, i.e., the third term is also one, because $$0+1=1$$. The first few terms are $$(0, 1, 1, 2, 3, 5, 8, 13, 21, …). The ratio of consecutive terms closely mirrors $$/phi$$, approximations which get increasingly accurate.

So, lets cook up a simple algorithm that exploits this feature of the Fibonacci numbers. We want to approximate $$/phi$$ with to a high degree of accuracy; thus, we will design the algorithm to run until we converge on [the computer’s epsilon error](https://en.wikipedia.org/wiki/Machine_epsilon), i.e., the smallest digit recorded by my 64-bit Mac.

**Figure 1**.

### Python implementation
---

* See the Appendix for translations into more programming languages.

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

### Appendix: More Reading
---

* A well written Pixa article on [photography and design applications](https://www.pixpa.com/blog/golden-ratio). Is the golden ratio the genesis of photography’s rule of thirds? How close do natural patterns adhere to the golden ratio?

* A visualizations/applications oriented Ted talk covering [the basics of Fibonacci numbers](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjoi6TiiL7wAhUzFTQIHb2TAdgQtwIwA3oECAQQAw&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DSjSHVDfXHQ4&usg=AOvVaw2LofPkoDFw8s3EFUlOPdbe).

* The coolest visualization, IMO, is the [golden spiral](https://mathworld.wolfram.com/GoldenSpiral.html).


### Appendix: More Code
---

#### MATLAB implementation
---

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
