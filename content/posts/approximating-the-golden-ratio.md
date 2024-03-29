---
title: "Using numerical mathematics to approximate the golden ratio"
date: 2021-05-10
katex: true
markup: "mmark"
---

## Using numerical mathematics to approximate the golden ratio
---

<br>

<p align="center"> <img src="/posts/golden-spiral.png"/ width = "550" height = "347"> </p>

<br>

### Introduction and historical context
---

I will approximate the golden ratio by iteratively taking ratios of consecutive terms in the Fibonacci sequence. This algorithm lets us peer into the underlying relationship between the Fibonacci sequence and the golden ratio, illuminating a number of interesting patterns. 

The [golden ratio](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjVsumck77wAhVFLX0KHdj1Di0QFjAJegQIAxAD&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FGolden_ratio&usg=AOvVaw2xWnjTV-SdFz2WkhAdaL-s) is a mathematical phenomenon between two numbers, say, a and b. Let a > b, if the ratio of $\frac{a}{b}$ is the same as $\frac{(a+b)}{a}$, then the ratio is ~$\frac{1.618}{1}$. This number is irrational, i.e., its decimal places never converge, classically denoted by the Greek  letter phi, $\varphi$. $\varphi$ is the positive root of the quadratic equation x$^2$ - x - 1 = 0. Upon solving the equation we obtain x = $\frac{1 + 5^{0.5}}{2}$. The golden ratio was (probably) first discovered in Ancient Greece through applications in geometry, which the Greeks emphasized. Greek mathematicians determined $\varphi$ was an irrational number all the way back in the fifth century BC (woa). 

Fibonacci numbers are closely related to the golden ratio.

> "[Fibonacci] was an Italian mathematician from the Republic of Pisa, considered to be 'the most talented Western mathematician of the Middle Ages'". [[Wikipedia](https://en.m.wikipedia.org/wiki/Fibonacci)]

The first two Fibonacci numbers are zero and one. Each consecutive term is the sum of the previous two, i.e., the third term is also one, because 0+1=1. The first few terms are (0, 1, 1, 2, 3, 5, 8, 13, 21). The ratio of consecutive terms closely mirrors $\varphi$, and the approximations get increasingly more accurate. Hmm, this seems like an important property if we, say, wanted to approximate the golden ratio!

<br>

### Approximating the golden ratio with Fibonacci numbers
---

Lets cook up a simple sequence of operations exploiting the last feature of the Fibonacci numbers discussed above. We want to approximate $\varphi$ to a high degree of accuracy; thus, we will design the algorithm to run until we converge on [the computer’s epsilon error](https://en.wikipedia.org/wiki/Machine_epsilon) ($\varepsilon$), i.e., the last digit recorded on my 64-bit computer. Upon running the algorithm, we find that it takes 39 iterations for our approximation errors to converge to $\varepsilon$.

<p align="center"> <img src="/posts/fib-errors.png"/ width = "550" height = "431"> </p>

**Figure 1**. The absolute errors between our Fibonacci ratio approximations and the golden ratio itself. Notice that the errors trend towards zero, indicating that our approximations are getting closer and closer to the true solution.

<br>

**Python implementation**:

Runtime ~ 123 $\mu$s (native | Zsh)

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

<br>

### Appendix: More Reading
---

* The coolest golden ratio visualization, imo, is the [golden spiral](https://mathworld.wolfram.com/GoldenSpiral.html) (see the first picture!). Consider a rectangle whose length is the golden ratio $\varphi$ with height 1. Successive points that divide this "golden rectangle" into perfect squares fall on a logarithmic spiral with a growth factor equal to $\varphi$. 
* A well written Pixa article on [photography and design applications of the golden ratio](https://www.pixpa.com/blog/golden-ratio). Is the golden ratio the genesis of photography’s rule of thirds? How close do natural patterns adhere to the golden ratio?
* A visualizations/applications oriented Ted talk on [using the Fibonacci numbers in magical ways](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjoi6TiiL7wAhUzFTQIHb2TAdgQtwIwA3oECAQQAw&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DSjSHVDfXHQ4&usg=AOvVaw2LofPkoDFw8s3EFUlOPdbe).

<br>

### Appendix: More Code
---

**C++ implementation**:

Runtime ~ 62 $\mu$s (native | Zsh, g++ compiler)

```cpp
//Libraries
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

int main(void){

    //Var Init
    const double phi = (1 + sqrt(5)) / 2;
    const double tol = 1e-16;
    std :: vector <double> fib;
    fib.push_back(0);
    fib.push_back(1);
    fib.push_back(1);
    std :: vector <double> erval;
    erval.push_back(1);
    std :: vector <double> ratio;
    int n = 0;
    
    //While Loop
    while (erval [n] >= tol) {
        fib.push_back(fib[n + 2] + fib[n + 1]);
        ratio.push_back(fib[n + 3] / fib[n + 2]);
        erval.push_back(std::abs(ratio[n] - phi));
        ++ n;
    }

    //Tests
    if (ratio.back() == phi) {
        std :: cout << "done" << std :: endl;
    }
}

```
