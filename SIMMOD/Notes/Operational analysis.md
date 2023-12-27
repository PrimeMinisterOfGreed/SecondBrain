
## Basic quantities
$T$ length of observation period
$B$ amount of time in which the system is busy
$C$ Number of completions
$A$ Number of arrivals

## Derived quantities
$\lambda = \frac{A}{T}$  job/sec -> arrival rate
$X= \frac{C}{T}$ output rate
$U= \frac{B}{T}$ utilization 
$S = \frac{B}{C}$ mean service time


## Saturation
$U = X*S$  -> utilization law
$A = C$  -> flow balance| operational equilibrium
$U= \lambda*S$ 

Saturation: $U \leq 1$ -> $X \leq  \frac{1}{S}$  and $\lambda \leq \frac{1}{S}$ 
if $X = \frac{1}{S}$  the system is saturated
## Customer quantities
$a_k$  = the arrival of the k-th customer
$c_k$ = instant in which leaves the system (must be $c_k \gt a_k \geq 0$)
$w_k = c_k - a_k$ waiting time for k-th customer
$\bar{w} = \frac{1}{C} \sum^{C}_{k=1}{w_k}$ average waiting time
## Little's formula

$\bar{n} = X*\bar{w}$ -> waiting law
$\bar{n} = \lambda*\bar{w}$ -> little's formula

![[Pasted image 20231001123801.png]]

 little formula without op eq
$\bar{n} = \frac{G(T)}{T}$  and $\bar{w} = \frac{G(T)}{A(T)}$  --> $\bar{n} = \frac{A(T)}{G(T)} \bar{w} X$ 


## load dependency
- $T(n)$ time spent by the system with n customers inside
- $K_{max}$  maximum number of customers  simultaneously present inside the system 

$T = \sum^{K_{max}}_{n=0}T(n)$  and $B=T-T(0)$  

#### load dependent behaviour

$\phi(k) = \frac{T(k)}{T}$    $k=0,...,K_{max}$  -> fraction of time spent by the system in each state

$C(k)$ -> number of completions with k customers in the systems  -> $\sum^{K_{max}}_{k=1}{C(k)} = C$ 

$S(k) = \frac{T(k)}{C(k)}$ -> load dependent mean service time or service function 

$X = \sum^{K_{max}}_{k=1}{\frac{1}{S(k)}{\phi(k)}}$  generalized throughput

## individual queue
i = 1,...,M -> index for each station in the network. 0 is the outside(or whole system).

$U_i= X_iS_i$ , $X_0= \frac{C_0}{T}$ , $\lambda_0 = \frac{A_0}{T}$  --> in op eq. $\lambda_0 = X_0$ 
$V_i$  number of service request for queue i $V_i = \frac{C_i}{C_0}$ 
$D_i$ total service (time) demand for i $D_i = V_iS_i=\frac{B_i}{C_0}$ 


