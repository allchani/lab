---
title: "[Udemy03] 02. Bayes Rule Review" 
excerpt: Bayes Rule & Probability Review
mathjax : True
---
# Bayes Rule & Probability Review

$$p(A|B)=p(A,B)/p(B)$$  

---


- $p(A \| B)$ - conditional
- $p(A,B)$ - joint
- $p(B)$ - marginal

# Bayes Example

A = {Buys, Does Not Buy}, B = {USA, Canada, Mexico}  
Suppose we want to find p(Buy? | Country)

|                           | CA  | US  | MX  |
|:-------------------------:|:---:|:---:|:---:|
| __Buy = 1(did buy)__      |20   |50   |10   |
| __Buy = 0(did not buy)__  |300  |500  |200  |

- let's find p(Country) first
    + p(Country=Mexico) = 210 / (210+550+320) = 0.19
    + p(Country=US) = 550 / (210+550+320) = 0.51
    + p(Country=Canada) = 320 / (210+550+320) = 0.30
- Joint probabilities
    + p(Buy=1, Country=CA) = 0.019
    + p(Buy=0, Country=CA) = 0.28
    + p(Buy=1, Country=US) = 0.046
    + p(Buy=0, Country=US) = 0.46
    + p(Buy=1, Country=MX) = 0.0093
    + p(Buy=0, Country=MX) = 0.19

---
- Curse of dimensionality is a bad thing,
- Because as the volume grows:
- We need to do more computation
- Need more samples to get accurate estimates

---
- These seem a lot smaller than the marginals p(Country) we calculated earlier
- Sum of all possible outcomes must = 1
- If number of total possibilities grows exponentially, actual probability values will shrink exponontially
- Another consequence of "curse of simensionality"
- Computers have finite precision - 32-bit float holds 32-bits of info
- Can't store infinite number of values

----
- Underflow 
    - As probability → 0, eventually computer will round down to 0
    - Called the "Underflow" problem
    - Common in probability - use the log probability instead
    - Log grows slowly as its argument increases

---
- Conditional probabilities
    + p(Buy=1 \| Country=CA) = 0.19/0.30 = 0.06
    + p(Buy=0 \| Country=CA) = 0.28/0.30 = 0.93
    + p(Buy=1 \| Country=US) = 0.046/0.51 = 0.09
    + p(Buy=0 \| Country=US) = 0.46/0.51 = 0.91
    + p(Buy=1 \| Country=MX) = 0.009/0.19 = 0.05
    + p(Buy=0 \| Country=MX) = 0.185/0.19 = 0.97

No longer sums to 1, sums to 3! why?  
We are <U>given</U> country - the space of random variables is only buy/not buy.  
Country is not random here.  

- Another way to calculate.  
We are given country, so we only need to consider the counts for that country. 
```
p(Buy=1 | Country=US) = p(Buy=1, Country=US)/ p(Country=US)  
= (50/1080) / [(50+500)/1080]  
= 50/(50+500)  
= 0.09
```

---

- Similar but different problem
    + p(Buy=1 \| Country=CA) = 0.1
    + p(Buy=1 \| Country=US) = 0.1
    + p(Buy=1 \| Country=MX) = 0.1

- Independence  
When 2 variables are independent, the joint becomes the multiple of the marginals, e.g if A&B are independent:  

$$p(A,B) = p(A)p(B)$$  

So, if Buy & Country are independent:  
```
p(Buy | Country) = p(Buy, Country)/p(Country) = p(Buy)p(Country)/p(Country)  
                 = p(Buy)
```

---

- Manipulating Bayes Rule  
Let's make it look more like the form we'll use in this course. We know:  

$$p(A|B) = p(A,B) / p(B)$$  

The opposite is also ture:  

$$p(B|A) = p(B,A) / p(A)$$  

Since p(A,B) = p(B,A):  

$$p(A|B) = p(B|A)p(A) / p(B)$$  

```
Combine : p(A|B)p(B) = p(B|A)p(A) 
```

We don't typically have p(B) directly but can calculate it from the numerator, e.g.  


$$p(B)=\sum _{ A }^{  }{ p(A,B) } =\sum _{ A }^{  }{ p(B|A)p(A) }$$  


If working with continuous distributions, sum turns into integral:
$$p(A|B)=\frac { p(B|A)p(A) }{ \int { p(B|A)p(A)dA }  } $$

---

$$p(A|B) = p(B|A)p(A) / Z$$  

Can also think of the bottom term as a "normalization constant" so that the distribution sums to 1  

$$p(A|B)\quad \propto \quad p(B|A)p(A)$$  

Many times, we just want the ${ argmax }_{ A }p(A|B)$  
Z is independent of A, so:  

$${ argmax }_{ A }p(A|B)\quad =\quad { argmax }_{ A }p(B|A)p(A)$$  


---

- Bayes for Classification  

$$p(y|x) = p(x|y)p(y) / p(x)$$

p(x \| y) is a "generative distribution" - it tells us "what dose x look like?" given "the class is y"  

While a Bayes classifier makes use of Bayes rule, it does NOT necessarily make use of Bayesian statistics.  

