
a stochastic process is a family of random variables $\{ X(t),t \in t \}$

3 characteristics :
- [Process state space](#State space) 
- [index](#index) (time parameter)
- [dependencies](#Statistical dependencies) amongs other variables in $\{X(t), t\in t\}$

### State space

set of all possible values a random variables $X(t)$ can assume. If finite then is a discrete state stochastic process or **chain**. Otherwise is a continuous stochastic process represented by a set of real numbers. 

### Index 

if index $T$ is finite or countable then we have a discrete time stochastic process. Otherwise is continuous and the time is picked as a real number.


### Basic probability theory

For discrete random variable, characterization:
probability mass function => $F_x(x)= P[X=x]$ probability that variable x is equal to a certain x. 

For continuous random variable, characterization:
cumulative distribution function (CDF) or #PDF (prob. dist. func) => $F_X(x) = P[X<x]$
#PDF  is often defined as => $f(x)_x = dF_x(x)/dx$

 #conditional_probability => $P[A|B] = P[A,B]/P[B]$  where $P[A,B]  = P[A|B] * P[B]$



### Statistical dependencies

denote all Random variables as a vector $X = [X(t_1), X(t_2)...]$, then to fully characterize this statistic process we shall use the
#joint_pdf => $F_X(x;t)=P[X(t_1) \leq x_1 , X(t_2) \leq x_2,..., X(t_n) \leq x_n, X(t_n+1) \leq x_n+1]$ . Generally this is impossible, except if we introduce some restrictions. 

We can exploit #conditional_probability  to reduce the #joint_pdf to 2 factor  =>
$$
F_X(x;t)=P[X(t_{n+1}) \leq x_{n+1}|X(t_1) \leq x_1 , X(t_2) \leq x_2,..., X(t_n) \leq x_n] * P[X(t_1) \leq x_1 , X(t_2) \leq x_2,..., X(t_n) \leq x_n]
$$ 

by repeating the reasoning we can obtain #joint_pdf 
$$
F[x;t] = 
P[X(t_{n+1}) \leq x_{n+1} | X(t_1) \leq x_1 ,..., X(t_n) \leq x_n] *
P[X(t_{n}) \leq x_{n} | X(t_1) \leq x_1 ,..., X(t_{n-1}) \leq x_{n-1}]*
P[X(t_{n-1}) \leq x_{n-1} | X(t_1) \leq x_1 ,..., X(t_{n-2}) \leq x_{n-2}]*...
P[X(t_{1}) \leq x_{1}]
$$

# Classes of stochastic process 

### Stationary Process 

if for any constant $\tau$ is true $F_X(x;t+\tau) = F_X(x;t)$ where $t+\tau= \sum^{n}_{i=1} (t_i+\tau)$
 
 

