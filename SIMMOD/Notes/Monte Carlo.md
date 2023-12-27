
## Monte carlo simulation
computerized mathematical technique that allows to account for stochastic phenomena. First used by scientist that were working on the atomic bomb. Using stochastic assumption for service and arrival times we can generate a random but plausible trace for the simulation.

## Poisson process (negative exponential)
events are rare and occur in a completely random manner. Assume that p of one event in interval of length $\Delta$ is $\lambda \Delta+ o(\Delta)$ dividing the interval T in m part of length $\Delta$ and count the events we obtain 
![[Pasted image 20231101180122.png]]
$P(k,T|\Delta) = \binom{m}{k} (\lambda \Delta)^k(1-\lambda \Delta) ^{(m-k)} + o(\Delta)$ 
the limit of this probability for $m \rightarrow \infty$ 
$P(k,T) = \frac{(\lambda T)^k}{k!}e^{-\lambda T}$ , with $\tau$ as distance between successive arrivals we have 
$P(\tau > T) = P(0,T)= \frac{(\lambda T)^0}{0!}e^{-\lambda T} = e^{-\lambda T}$  so that $P(\tau < t) = 1- e^{-\lambda T}$ 

CDF = $F_X(x)=Pr[X \leq x] = 1-e^{-\lambda x}$ , PDF= $f_X(x)=\frac{dF_X(x)}{dx}= \lambda e^{-\lambda x}$ 
$E[X] = \sigma = \frac{1}{\lambda}$ , $VAR[X]= \sigma^2 = \frac{1}{\lambda^2}$, $CV[X]=\frac{Std[X]}{E[X]}= \frac{\sqrt{VAR[X]}}{E[X]}= 1$ 
## Random number generation
an ideal random number generator produces output such that each value in the interval 0.0 <u< 1.0 is equally likely to occur.

a good random generator produces output that is almost statistically indistinguishable from an ideal generator 

### Conceptual model 
- choose a large positive integer m, this defines the set $\chi_m =1...m-1$.
- fill a urn with the elements of $\chi_m$ , each time a random number u is needed draw an integer at random from the urn and let $u=x/m$ 

Each draw simulates a sample from a Uniform(0,1) distributed RV, it is important from m to be large so possible values are densely distributed between 0.0 and 1.0

### Lehmer's algorithm
the Linear congruential generator algorithm takes 2 parameters: modulus m (large prime) and multiplier a ($I \in \chi_m)$ 
the integer sequence $x_0,x_1,...$ is defined by the iterative equation
$x_{i+1}=g(x_i)$  with $g(x)=ax \mod{m}$ ,  $x_0 \in \chi_m$ is called seed.  Because of mod operator $0 \leq g(x) < m$ . 
0 must not occur since $g(0)=0$ , since m is prime $g(x) \neq 0$ if $x \in \chi_m$ . if $x_0 \in \chi_m$ then $x_i \in \chi_m$ for all $i \geq 0$.

There is nothing random in this generator, this is why is called pseudo random generator

## Full period 
the choice of m is dictated in part by system consideration because it cannot be the same in 64,32 or 16 bit system.So this choice must be done with great care. 
Given a modulus m a full period sequence contains all the numbers in the set (1,m-1) before repeating itself. 

## Basic probability
Empirical probability: perform an experiment many times counting the times a certain event occurs $A$ :  Relative frequency : $n_a/n$ , converges as $Pr(A)=\lim_{n \rightarrow \infty}\frac{n_a}{n}$ 

Axiomatic probability: theoretic approach by mathematically build the sample space.

## Discrete random variables
A random variable X is discrete if the set of possible values $\chi$ is finite. 
Is uniquely determined if its probability distribution function is a real value function determined for each element in the set $\chi$  

PDF: $f(x)=Pr(X=x)$ 
By definition: $\sum_xf(x)=1$ 

### CDF (Discrete)
the cumulative distribution function cdf of X is defined as 
$F(x)= Pr(X \leq x)= \sum_{t \leq x} f(t)$ 

A cdf can be generated from pdf by recursion:
$\chi=\{x|x=a,a+1,...b\}$ --> $F(a)=f(a) \ \ \ \ F(x)=F(x-1)+f(x)$ 

A pdf also can be generated from cdf:
$f(a)=F(a) \ \ \ \ \ f(x)=F(x)-F(x-1)$ 

A cdf is strictly monotone increasing: 
- if $x_1<x_2$ then $F(x_1)<F(x_2)$ 
- CDF values are $\in (0.0,1.0)$ , Monotonicity of F(x) is the basis to generate discrete RVs

## Continuos random variables 
A RV X is continuous if possible values $\chi$ is a continuum and determined by:
 PDF that is $\int^{b}_{a}f(x)dx= Pr(a \leq X \leq b)$ 

by definition $\int_\chi f(x)dx =1$ 


### CDF (Continuos)
CDF is $F(x)=Pr(X \leq x) = \int_{t \leq x} f(t)dt$ 
strictly monotone increasing and bounded to 0.0 and 1.0

cdf can be obtained from pdf by integration 
pdf can be obtained from cdf by differentation $f(x)= \frac{d}{dx}F(x)$ 

## Summary of Distributions 
### Discrete 

|Generator|Range (x)| Mean| Variance|
|---|----|---|---|
|Bernoulli (p)| x=0,1| p| p(1-p)|
|Binomial (n,p)|x=0,...,n|np|np(1-p)|
|Equilikely(a,b)|x=a,...,b|(a+b)/2|($(b-a+1)^2$-1)/12|
|Geometric(p)| $x=0,...$ | p/(1-p)| $np/(1-p)^2$
|Pascal(n,p)| $x=0,...$ |np/(1-p)| $np/(1-p)^2$ 
|Poisson(m)| $x=0,...$ |m|m


### Continuos 

|Generator|Range (x)| Mean| Variance|
|---|----|---|---|
|Uniform(a,b)| a < x < b| (a+b)/2| $(b-a)^2/12$ 
|Exponential(m)| x>0 | m| $m^2$
|Erlang (n,b)| x>0| nb| $nb^2$ 
|Normal(m,s)| $\forall x$ | m| $s^2$ 
|Lognormal(a,b)|x>0|$\exp(a+\frac{1}{2}b^2)$| $(\exp(b^2) -1) \exp(2a+b^2)$ 
|Chisquare(n)|x>0|n|2n
|Student(n)| $\forall x$ |0|n/(n-2)

## Generating random distributions 
The generation of non uniform random variables can be performed with 3 methods:
- Inverse transformation
- Acceptance rejection
- Composition 

Inverse transformation relies on explicit knoweledge of the cumulative distribution function. 

Acceptance rejection and composition assume that Distribution or Density (continuos case) function are known.

## Uniform random variable 

We can generate a uniform(a,b) from a uniform(0,1) a.k.a lehmer generator. This is possible by simply scaling and shifting transformation using a:
Scaling coefficient $\alpha=(b-a)$ and a Shifting coefficient $\beta=a$ . 
```C
double Uniform(double a, double b){return (a+(b-a)*Random());}
```

### Inverse distribution function 
The inverse distribution function (idf) of X is the function $F^{-1}:(0,1) \rightarrow \chi$ for all $u \in (0,1)$ as $F^{-1}(u)=x$ 
where $x \in \chi$ is the unique possible value for $F(x)=u$ 

There is correspondence between possible values $x \in \chi$ and cdf values $u=F(x) \in (0,1)$ 

Follow a list of idf with u for the mean from value and x for the value from mean 
#### IDF Uniform
Uniform(a,b)
$u= F(x)= \frac{x-a}{b-a}$  for $a<x<b$ 
$x= F^{-1}(u)=a+(b-a)u$  for $0  < u < 1$ 

#### IDF Exponential 
Exponential($\eta$) 
$u = F(x)= 1-\exp\ ( -\frac{x}{\eta} )$  for $x>0$
$x= F^{-1}(u)= - \eta \ln(1-u)$ for $0<u<1$ 

#### IDF for pareto type1
Pareto($L,\alpha$)
$u=F(x)=1-\left( \frac{L}{x} \right)^{\alpha}$ for $x \geq L$ 


#### IDF for quadratic 
if X is a continuous variable with possible value $0<x<b$ 
- pdf $f(x)=\frac{2x}{b^2}$ 
- cdf is $u = F(x)=\left( \frac{x}{b} \right)^{2}$    
- $x= F^{-1}(u)=b\sqrt{ u }$ for $0<u<1$ 

## Composition method 
usually used for continuous random variates , for distribution whose idf is not efficient to compute. 
Distributions are weighted sum of simpler distributions that can be computed efficiently.

Algorithm to generate random variate with distribution $f_{x}(X)=\sum^{n}_{i=1}\alpha_{i}g_{i}(x)$ 
```python
# Initialization
A = []
alpha = [] 
A[0] = alpha[0]
for i in range(1,n):
    A[i] = A[i-1]+alpha[i]


```
