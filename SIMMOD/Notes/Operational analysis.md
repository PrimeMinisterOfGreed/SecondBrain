
## Basic quantities
$T$ length of observation period
$B$ amount of time in which the system is busy
$C$ Number of completions
$A$ Number of arrivals

### Derived quantities
$\lambda = \frac{A}{T}$  job/sec -> arrival rate
$X= \frac{C}{T}$ output rate
$U= \frac{B}{T}$ utilization 
$S = \frac{B}{C}$ mean service time


### Saturation
$U = X*S$  -> utilization law
$A = C$  -> flow balance| operational equilibrium
$U= \lambda*S$ 

Saturation: $U \leq 1$ -> $X \leq  \frac{1}{S}$  and $\lambda \leq \frac{1}{S}$ 
if $X = \frac{1}{S}$  the system is saturated ^1c8519
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

## Network of queue
i = 1,...,M -> index for each station in the network. 0 is the outside(or whole system).

$U_i= X_iS_i$ , $X_0= \frac{C_0}{T}$ , $\lambda_0 = \frac{A_0}{T}$  --> in op eq. $\lambda_0 = X_0$ 
$V_i$  number of service request for queue i $V_i = \frac{C_i}{C_0}$ 
$D_i$ total service (time) demand for i $D_i = V_iS_i=\frac{B_i}{C_0}$ 


### Consistency law
$X_0 = \frac{C_0}{T} =\frac{1}{V_i}X_i = \frac{X_i}{V_i}$  -> X in terms of visits
$X_0 = \frac{C_0}{T} = \frac{1}{D_i} = \frac{U_i}{D_i}$  -> X in terms of utilization
it follows $\frac{X_i}{X_j} = \frac{V_i}{V_j}$ and $\frac{U_i}{U_j} = \frac{V_iS_i}{V_jS_j} = \frac{D_i}{D_j}$ . 
X and U depend in general on the load of the system , relative values remains stable while change from station to station.
V are characteristics of each client

### Matrix representation

$C_i$ number of departures from station i
$C_{i,j}$ number of customers that move from i to j
it follows $C_i=\sum^{M}_{j=0}{C_{i,j}}$ 

$q_{i,j} = \frac{C_{i,j}}{C_i}$ transition frequency from i to j
it follows $\frac{C_{i,j}}{T} = q_{i, j}X_i$ 

if op eq -> $A_i = C_i$, then  $X_j = \sum^{M}_{i=0}{X_iq_{i,j}}$  --> can be written as $\boldsymbol{X}= \boldsymbol{X}\boldsymbol{Q}$   
where $\textbf{X} = (X_0,...,X_M)$  --> vector of M+1 components
$\textbf{Q}$ square matrix (M+1) x (M+1) filled with  $q_{i,j} = \frac{C_{i,j}}{C_i}$ , this matrix characterize the system. it follows that
$\frac{X_j}{X_0}  = \sum^{M}_{i=0}\frac{X_i}{X_0}q_{i,j}$ --> rewrite of flow balance equation

#### little law for Network of queues
using $V_j=\frac{X_j}{X_0}$  and knowing $V_0 = 1$ is possible to define $\textbf{V} = \textbf{V}\textbf{Q}$ that can be used to describe the system. this is possible because of the Consistency Laws. it follows also that $\bar{n_i} = X_i\bar{w_i}$  where $\bar{n_i}$ are mean number of customers and $\bar{w_i}$ are the mean waiting times.

## load dependency
- $T(n)$ time spent by the system with n customers inside
- $K_{max}$  maximum number of customers  simultaneously present inside the system 

$T = \sum^{K_{max}}_{n=0}T(n)$  and $B=T-T(0)$  

#### load dependent behaviour

$\phi(k) = \frac{T(k)}{T}$    $k=0,...,K_{max}$  -> fraction of time spent by the system in each state

$C(k)$ -> number of completions with k customers in the systems  -> $\sum^{K_{max}}_{k=1}{C(k)} = C$ 

$S(k) = \frac{T(k)}{C(k)}$ -> load dependent mean service time or service function 

$X = \sum^{K_{max}}_{k=1}{\frac{1}{S(k)}{\phi(k)}}$  generalized throughput

### load dependent behaviour for queues
$T_i(k)$ time spent at the i station with k customers inside (i=1,...,M) 
we can then write $\sum^{K_{max}}_{k=0}T_i(k) = T$  (i=0,...,M) and then we can define 
$\phi_i(k) = \frac{T_i(k)}{T}$ the fraction of time spent by each station with k customers. 

Let $C_i(k)$  (i=1,...,M) be the number of completions from the i-th station with k customers inside, also in this case $\sum^{K_{max}}_{k=1}C_i(k)=C_i$   (i=0,..,M)
Trivially we can define again $S_i(k)= \frac{T_i(k)}{C_i(k)}$  (i=0,...,M;k=1,...,$K_{max}$)  

and again $X_i=\sum^{K_{max}}_{k=1}\frac{1}{S_i(k)}\phi_i(k)$  (i=0,...,M)

## Response time

with $V_i$ and $\bar{w_i}$ we can compute the amount of time taken by customers to go through the system (response time).

2 types of system:
- Open System: new customers enter with rate $\lambda$ . The number of customers can grow to $\infty$ . If the system is not saturated $X_0 = \lambda$ 
- Closed System: fixed number of N customers is present in the system. Customers leaving are replaced with new customers
### Response time: Closed
N customers in system, index i=0 is meaningless and visits must be computed using a generic index k inside the system (arbitrary station) so $\Omega_i$ are dependent on k.

$R_k = \sum^{i=1,i \neq k}_{M}{\Omega_i}$  average amount of time taken by customers to return to station k (Response time).

$Y_k = \bar{w_k}+R_k = \sum^{M}_{i=1}{\Omega_i}$  average amount of time take by a customer to make a complete tour in the system starting from station k (cycle time).

if we generalize taking in consideration explicitly the station K
$V_j^{[k]} = \frac{C_j}{C_k} = \frac{X_j}{X_k} = \sum^{M}_{i=1}V_i^{[k]}q_{i,j}$          $j=1,...,m$    
we can relate this notation referring to a second station h
$V_j^{[h]} = \frac{C_j}{C_h} = \frac{V_j^{[k]}}{V_h^{[k]}}$              $j,h,k=1,...,M$ 
and for this chosen station we can compute 
$Y_k = \sum^{M}_{i=1}{\Omega_i}^{[k]} = \sum^{M}_{i=1}{V_i^{[k]}}\bar{w_i}$  
and also 
$Y_h = \sum^{M}_{i=1}\Omega_i^{[h]} = Y_k\frac{1}{V_h^{[k]}}$  and obtaining the general form
$R_h = Y_h - \bar{w_h}$ 


### Closed system with delay station
$Z$ average delay of station 0, using the delay station to compute visits counts (as reference station). We can write
$R_0 = \sum^{M}_{i=1}{\Omega_i}$ ,  $Y_0= Z+R_0$. In whole system the number of customers is constant, so using little law's on the black box:
![[Pasted image 20231001173621.png]]

in operational eq. we have $X_0=\frac{A_0}{T} = \frac{C_0}{T}$. And denoting $\bar{n_d}$ the avg number of customers in the delay station and $\bar{n_{cs}}$ the avg number of customer in the central system we have.

$N=X_0Y_0= X_0(Z+R)= \bar{n_d} + \bar{n_{cs}}$ . it follows $R_0 = \frac{N_{cs}}{X_0} - Z$ 
$U= n_{cs}/N$ 

### Response time: Open 

$\Omega_i=V_i\bar{w_i}$ (i=1,...,M) average time spent by customer in queue i
$R = \sum^{M}_{i=1}\Omega_i$  average response time of the system (or average response time spent by customer in the system).

using little law's
$\bar{n}=\lambda R=\sum^{M}_{i=1}X_i\bar{w_i}= \sum^{M}_{i=1}{\lambda \Omega_i}=\sum^{M}_{i=1}\bar{n_i}$ 

## Bottleneck Analysis
using $V_i$ and $S_i$  we can observe the behaviour of the system under stress condition ($\lambda$ grow in case of open system and $N$ grow  in case of closed system).  

### Bottleneck Analysis: open systems
$S_i$ and $V_i$ are independent of $\lambda$. The same is not true for $X_i$ and $U_i$ so they can be represented as function of $\lambda$ --> $X_i(\lambda)$ and $U_i(\lambda)$. For the Consistency Law we have $\frac{X_i(\lambda)}{X_j(\lambda)} = \frac{V_i}{V_j}$ and $\frac{U_i}{U_j} = \frac{V_iS_i}{V_jS_j}$ , independent from $\lambda$. it follows then 
$\lambda_i = \lambda_0V_i$ and in op.eq $\lambda \leq \frac{1}{S_i}$ (i=1,...,M).  And so $X_i(\lambda) = \lambda_i = \lambda_0V_i$ and $U_i(\lambda) = X_i(\lambda)S_i$ .

Denote with b the first station to reach 1 of utilization. This station is the Bottleneck of the system  and is used to identify the value of $\lambda_{max}$ after which the system loses the operation eq. property. If $\lambda>\lambda_{max}$ the system reach a point in which the queues grow to infinity and the system becomes unstable. Since $\frac{U_i(\lambda)}{U_j(\lambda)}$ is fixed for any pair i,j then the station that becomes saturated first is whose the utilization becomes the largest in any loading conditions. Formally: $\frac{U_b(\lambda)}{U_i(\lambda)}=\frac{V_bS_b}{V_iS_i}=\frac{D_b}{D_i} > 1$, in order to identify the index of the bottleneck $V_bS_b=max_i(V_iS_i)$ , then we can state the maximum throughput of the bottleneck station $X_b^{[max]}(\lambda)=\frac{U_b^{[max]}(\lambda)}{S_b} = \frac{1}{S_b}$ --> $\lambda_{max}=\frac{1}{V_bS_b}$ 

### Beyond $\lambda_{max}$ (asymptotic analysis)
in certain cases is possible for $\lambda$ to grow beyond $\lambda_{max}$. This may yield to saturation also the other stations that have $V_iS_i < V_bS_b$ (depend on topology). 2 cases can arise:
1) $V_iS_i > V_jS_j$  $\forall j > i; i,j=1,2,...,M$  in this network b = 1 and only the first station can have $U = 1$ 
2) $V_iS_i \leq V_jS_j$   $\forall j > i; i,j=1,2,...,M$  in this network b=M and all the queues can have $U=1$  if $\lambda$ becomes sufficiently large. 

in both cases $X \leq \frac{1}{S_b}$  independently of $\lambda$

![[Pasted image 20231002213059.png]]

### Bottleneck Analysis: closed systems
Assume that $S_i$ and $V_i$ are independent of the load system $N$, and concentrate the analysis on $X$ $U$ and $Y$  --> $X_i(N)$ ,$U_i(N)$ and $Y(N)$ (valid for the whole system) that are dependent. Consistency law is valid also there
$\frac{X_i(N)}{X_j(N)} = \frac{V_i}{V_j}$ and $\frac{U_i(N)}{U_j(N)} = \frac{V_iS_i}{V_jS_j}$ independently of N.

denote with b the station whose $U=1$ first when $N$ grows, this is the bottleneck of the network, since $\frac{U_i(N)}{U_j(N)}$ is fixed for all station i,j=1,2,...,M. The station that becomes saturated first is the one whose $U$ is largest in any loading conditions 
$\frac{U_b}{U_i}>1$ i=1,...,M $i \neq b$  so that $V_bS_b=max_i(V_iS_i)$  

#### Asymptotic analysis for closed systems
large values of $N$ yield $U \approxeq 1$ and $X_i(N) \approxeq \frac{1}{S_i}$, all the $V_i$ are computed on an arbitrary chosen station k, then the throughput of the system is $X_k(N) = \frac{U_b(N)}{V_bS_b} \approxeq \frac{1}{V_bS_b}$  the value derived is the possible maximum throughput of the station, is then possible to write 
$\lim_{N \rightarrow \infty}X_i(N)=\frac{1}{V_bS_b}$. using $D_i$ as the total average service time received by station i describe $D=\sum^{i=1}_{M}V_iS_i = \sum^{i=1}_{M}D_i$ as the total average time for a client to make a tour of the system (in this case N=1). D is then the cycle time of the system $D = Y(1)$ with little formula we can state $X_k(1)= \frac{1}{Y(1)}$ , if the networks is build so that the station doesn't interfere with each other then $Y(N)=Y(1)$  and $X_k(N)=\frac{N}{Y(N)}= \frac{N}{Y(1)}$.

The intersection among the asymptotes identify a unique saturation point $N^*=\frac{Y(1)}{V_bS_b}$. Similarly for the cycle time is possible to note $Y(N)=\frac{N}{X_k(N)}$ with $Y(1)$ as lower limit and $Y'(N)=N*V_bS_b$ which is a second lower limit (slanting asymptote).

![[Pasted image 20231003110041.png]]

### Bottleneck analysis: case with load dependent behaviour
in order to extend the analysis, we can remove the constant constraint from $S_i$, that now became $S_i(N)$ , this is possible only if this function has an upper bound limit for $N \rightarrow \infty$ .
Using $S_i(1) \leq S_i^{[max]} = \lim_{h->\infty} S_i(h)$ , the discussion made for closed system  $D=Y(1)=\sum^{i=1}_{M}V_iS_i = \sum^{i=1}_{M}D_i$ and $Y(N)=NV_bS_b$  can be generalized to 
$Y(1) = \sum^{i=1}_{M}V_iS_i$ and $Y(N)=NV_bS_b^{[max]}$  --> $V_bS_b^{[max]} = max_i(V_iS_i)^{[max]}$. If the service speed of i goes to 0 all the customers will be blocked by that station so this discussion  is not valid, and so is a generalization for all the stations whose service speed is not an increasing function of the load. 

NOTE: the expression for D is equal to R(1).

#### Case of queues with load dependent behaviour
using $S_i(1) \geq S_i^{[min]} = \lim_{h \rightarrow \infty} S_i(h)$ , the discussion can now be generalized in $Y(1) = \sum^{i=1}_{M}V_iS_i(1)$ and $Y(N)=NV_bS_b^{[min]}$  the problem now is that $Y(1) = \sum_{i=1}^{M}V_iS_i(1)$ can be larger that the minimum cycle of the network

#needclarify
note: is not clear what min is referring to

#### Case of infinite server 
infinite Server stations are such that their service function is $S_i(h)= \frac{S_i(1)}{h} = \frac{Z}{h}$. Because of this, the load dependent service speeds are non-decreasing, but also not limited so that these station cannot be bottlenecks because their limit service times are equal to 0. **They must be skipped during the search of a bottleneck**.

![[Pasted image 20231003212636.png]]

Let's study the case of a central server time sharing composed by N terminals connected to the central server. Assume that Z represent the delay associated with the terminal station and that $S_i$ and $V_i$ are constant. What would be the impact on the behavior if we connect more terminals. The response can be found using the delay station as reference to calculate the performance of the others in the systems.

in this case we have $Y(N) = Z+R(N)$  where R is the response time with N terminals connected. The slanted asymptote for $X(N)$ is given by $X'(N)= \frac{N}{Y(1)} = \frac{N}{[Z+R(1)]}$ on the other hand $X$ is bounded by horizontal asymptote $\lim_{N \rightarrow \infty}X_0(N)=\frac{1}{V_bS_b}$.

The saturation point is $N^*= \frac{Z}{V_bS_b}+\frac{R(1)}{V_bS_b}$ considering cycle and response time we have 
$Y(N)=\frac{N}{X(N)} \geq \frac{N}{1/V_bS_b} = NV_bS_b$ consequently the slanted asymptote for the response time is $R'(N)= N(V_bS_b) - Z$ 


# Operational Analysis: intermediate state  

## Intermediate state
steady state analysis is not enough to understand the behavior of the system in intermediate conditions, additional measure are needed. 
The state of the system can be represented with a vector $\underline{n} = (n_1,n_2,...,n_m)$  $n_i \geq 0$  $i=1,2,...,M$  the set of all the possible state is called state space $S(M)$     


## State balance of a single queue
assume that the state are defined on the base of the number of customer waiting in the queue with states k,m,n.

let $C(m,n)$ = number of transitions from state m to state n, then the state balance equation is $\sum_{k}C(n,k)= \sum_mC(n,m)$ .  This holds in general for all state but for first and last, except when in Operational equilibrium, then it holds for all states.

![[Pasted image 20231006125755.png]]
### State balance measures

$r(n,m)=\frac{C(n,m)}{T(n)}$ => transition rate from m to n, while n is occupied
$p(n)=\frac{T(n)}{T}$ fraction of time spent by the system with n customers waiting

the state balance equation can be rewritten with $\sum_kp(k)r(k,n)=p(n)\sum_mr(n,m) \space |\forall n$    
### Balance equations

$$
\begin{equation}
    \begin{cases}
      p(1)r(1,0)=p(0)r(0,1)\\
      \\
      p(n-1)r(n-1,n)+p(n+1)r(n+1,n)=p(n)[r(n,n+1)+r(n,n-1)]\ \ \ \ 0<n<N \\
      \\
      p(N-1)r(N-1,N)=p(N)r(N,N-1) \\
      \\
      \sum_np(n)=1
    \end{cases}\
\end{equation}
$$

#### Simplify transition rates 
using
- $C(n,n+1)= A(n)$ = # arrivals observed when the system is in state n; $A(N)=0$
- $C(n,n-1)=C(n)$ = # completions observed when the system is in state n; $C(0)=0$

we can generalize to 
$r(n,n+1)= \frac{A(n)}{T(n)}= \lambda(n)$
$r(n,n-1)= \frac{C(n)}{T(n)}= \micro(n)$ 

#### Result
the system can now be rewritten as
$$
\begin{equation}
    \begin{cases}
    p(n)\micro(n)=p(n-1)\lambda(n-1) \ \ \ 0<n \leq N \\
    \\
    \sum_np(n)=1
    \end{cases}\
\end{equation}
$$

nb this is the final form, you can take the other system and perform the substitution to see the intermediate one
 

### Solution: load dependent rates 
the previous solution provide a new interesting relationship 
$$
\begin{equation}
\begin{cases}
p(n) = p(0)\prod^{n}_{k=1}\frac{\lambda(k-1)}{\micro(k)} \ \ \ 0<n \leq N \\ 
\\
p(0)= (1+\sum^{N}_{n=1}[\prod^{n}_{k=1}\frac{\lambda(k-1)}{\micro(k)}])^{-1}
\end{cases}
\end{equation}
$$
and performance indices

- $X= \sum^{N}_{n=1}p(n)\micro(n)$ 
- $\bar{n} = \sum^{N}_{n=1}np(n)$ 
- $\bar{W}=\frac{\bar{n}}{X}$ 

### Solution: homogeneous 
arrival rates are independent from the state of the system 
$\lambda(0)= \lambda(1)...=\lambda(N-1)=\lambda$
service rates are also indipendent of the state of the system 
$\micro(1)=\micro(2)...=\micro(N)=\micro$

we can define $\rho=\frac{\lambda}{\micro}$ and conclude that $p(n)= \frac{1-\rho}{1-\rho^{N+1}}\rho^n \ \ \ 0\leq n \leq N$  
#### Asymptotic homogeneous performance indices

when $\rho < 1$ taking the limit for N that goes to $\infty$ we observe that the fraction of time spent by the system in each of its possible states assume the connotation of a probability
$p(n)= (1-\rho)\rho^n$ 

we can then derive 
- throughput $X= \lambda$ 
- average queue length $\bar{n}=\frac{\rho}{1-\rho}$ 
- average waiting time $\bar{W} = \frac{1}{\micro(1-\rho)}$ 


## Generalization 
suppose that measurement of service rates change for possible values of the state k. The result obtained can be summarized in the following manner:

- Discouraged arrivals
- Multiple Server queue 
- infinite server queue 
- queue with a finite waiting room
- queue with fixed population

### Discouraged arrivals 
$\lambda(k)=\frac{\lambda}{k+1}$ , $\micro(k)=\micro \ \ k \geq 1$  from this result we obtain 

$p(n)= p(0)\prod^{n-1}_{k=0}\frac{\lambda/(k+1)}{\micro}=p(0)(\frac{\lambda}{\micro})^n \frac{1}{n!}$  

p(0) can be computed using its explicit expression 

$$
p(0)= [1+ \sum^{\infty}_{n=1}(\frac{\lambda}{\micro})^n \frac{1}{n!}]^{-1}=e^\frac{-\lambda}{\micro}
$$  
and then 

$$
p(n)= \frac{(\lambda/\micro)^n}{n!}e^\frac{-\lambda}{\micro} 
$$



### Infinite server queue 
$\lambda(k) = \lambda$ , $\micro(k) = k \micro$ 
distribution of number of customers 
$$
p(n)=p(0) \prod^{n-1}_{k=0}\frac{\lambda}{(k+1)\micro} = p(0)(\frac{\lambda}{\micro})^n \frac{1}{n!} 
$$
a simple expression for p(0) can be obtained for $N \rightarrow \infty$ 
$p(0) = [1+\sum^{\infty}_{n=1}(\frac{\lambda}{\micro})^n \frac{1}{n!}]^{-1} = e^{-\lambda/\micro}$ 
and the general expression becomes then 
$$
p(n) = \frac{(\lambda/\micro)^n}{n!}e^\frac{-\lambda}{\micro}
$$

### Multiple server queue 
$\lambda(k) = \lambda$  , $\micro(k)= \begin{equation} \begin{cases}  k \micro \ \ \ 0 \leq k \leq m \\ m \micro \ \ m<k \end{cases} \end{equation}$   
the distribution of the number of customers is then 
$$
p(n) = 
\begin{equation}
\begin{cases}
p(0)\prod^{n-1}_{k=0} \frac{\lambda}{(k+1)\micro} = p(0)(\frac{\lambda}{\micro})^n \frac{1}{n!} \ \ \ 0 \leq n \leq m \\
\\
p(0) \prod^{m-1}_{k=0} \frac{\lambda}{(k+1)\micro} \prod^{n-1}_{k=m} \frac{\lambda}{m \micro} = p(0)(\frac{\lambda}{\micro})^n \frac{1}{m!m^{n-m}} \ \ \ m<n
\end{cases}
\end{equation}
$$
p(0) can be derived from normalization, or obtained taking the limit $N \rightarrow \infty$ under the assumption that $\frac{\lambda}{m \micro} < 1$ 

### queue with a finite waiting room

$\lambda(k) = \begin{cases} \lambda \ \ \ 0 \leq k \leq B \\ 0 \ \ \ k>B\end{cases}$  , $\micro(k)= \micro$ 
we obtain 
$$
p(n) = \begin{cases}
p(0) \prod^{n-1}_{k=0} \frac{\lambda}{\micro} = p(0) (\frac{\lambda}{\micro})^n \ \ \ 0 \leq n \leq B 
\\
0
\end{cases}
$$
in this case $p(0)= \frac{1-\lambda/\micro}{1-(\lambda/\micro)^{B+1}}$
and the general expression becomes 
$$
p(n) = \begin{cases}
\frac{1-\lambda/\micro}{1-(\lambda/\micro)^{B+1}} \ \ \ 0 \leq n \leq B
\\0 \ \ \ n> B
\end{cases}
$$


### Single queue with fixed number of customers
$\lambda(k)= \begin{cases}(N-k)\lambda \ \ \ 0 \leq k \leq N \\ 0 \ \ \ k > N\end{cases}$, $\micro(k)= \micro$ 
 we have 
$$
p(n)= \begin{cases}
p(0) \prod^{n-1}_{k=0}\frac{(N-k)\lambda}{\micro} = p(0)(\frac{\lambda}{\micro})^n \frac{N!}{(N-n)!} \ \ \ 0 \leq n \leq N \\
0 \ \ \ n > N
\end{cases}
$$
from which we can derive 
$p(0) = [1+\sum^{N}_{n=1}(\frac{\lambda}{\micro})^n \frac{N!}{(N-n)!}]^{-1}$  


