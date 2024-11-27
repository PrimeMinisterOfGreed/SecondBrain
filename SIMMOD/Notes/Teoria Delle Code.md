

## Birth death process and queues 
times between death and births are described by independent RVs distributed according to neg exp laws.
- births can be interpreted as customer arrivals 
- deaths as customers departures 

so a birth-death process can be used as mathematical description for service stations, where customers arrive according to a Poisson process and service is provided by a service with neg exp distribution. queue management is carried by a particular queue discipline.
Solution of birth death process 
$$
\begin{align}
\pi_k=\frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\micro_1 \micro_2 ... \micro_k} \pi_0 

&& \pi_0=\frac{1}{1+\sum^{\infty}_{k=1} \prod^{k-1}_{j=0}\frac{\lambda_j}{\micro_j+1}}
\end{align}
$$

## Kendall notation 
Queues of type A/B/C/K/N/D where: 
- A arrival process: M is markovnian (poisson,exponential distribution), G general (non markov)
- B service process: M markovnian (exp. distribution), G general (non markovnian) 
- C number of identical servers 
- K maximum number of customers that can be queued (not specified --> infinite)
- N maximum number of customers that request a service (not specified --> infinite)
- D discipline used for queue ((not specified --> FCFS)

## M/M/1 queue
simplest case where: arrivals are poisson process, service are exponentially distributed, single server, infinite queue room, infinite customer population, FCFS discipline, arrival and service rate are constant $\lambda_k = \lambda$ and $\micro_k = \micro$ .

Using the solution to birth death process the probablity distribution of the number of customers in service station is
$$
\pi_k=\pi_0 \prod^{k-1}_{i=0}\frac{\lambda}{\micro
}=\pi_0(\frac{\lambda}{\micro})^k
$$
with ergodicity conditions 
$$
\begin{align}
S_1= \sum^{\infty}_{k=0}(\frac{\lambda}{\micro})^k < \infty && S_2=\sum^{\infty}_{k=0}\frac{1}{\lambda}(\frac{\micro}{\lambda})^k = \infty
\end{align}
$$

satisfied only if $\frac{\lambda}{\micro}<1$ normalization condition yields $\pi_0=1-\frac{\lambda}{\micro}= 1-\rho$  and $\pi_k=(1-\rho)\rho^k$ (refer to special case)

### Performance indexes M/M/1
System utilization is equal to $\rho$ --> $U=1-\pi_0=\rho$ 

the average number of customers is obtained as $E[n]=\bar{n}=\sum^{\infty}_{k=0}k \pi_k=\frac{\rho}{1-\rho}$ 
the second moment of this value is $E[n^2]=\bar{n^2}=\sum^{\infty}_{k=0}k^2\pi_k=2(\frac{\rho}{1-\rho})^2+\frac{\rho}{1- \rho}$ 
so the variance is obtained as $VAR[n]=E[n^2]-(E[n])^2=\frac{\rho}{(1-\rho)^2}$  

by little formula we obtain the avg time a customer spends in the system (sojourn time) as 
$$E[w]=\frac{E[n]}{\lambda}=\frac{1/\micro}{1- \rho}$$ 

We also can compute the probability that the queue length exceeds a given threshold as 
$$
Pr\{n \geq k\}= \sum^{\infty}_{i=k}\pi_i=\rho^k
$$


## M/M/1 queue with Discouraged arrivals 
the longer the queue the slower the arrivals. $\lambda_k = \frac{\lambda}{k+1}$  and $\micro_k=\micro$. Using the solution to birth death process we obtain  $\pi_k=\pi_0(\frac{\lambda}{\micro})^k \frac{1}{k!}$ it follows that 

$$
\begin{align}
\pi_0=e^{-\lambda/\micro} && \pi_k=\frac{(\lambda/\micro)^k}{k!}e^{-\lambda/\micro}
\end{align}
$$
Ergodicity is satisfied when $\lambda/\micro < \infty$

### Performance indexes M/M/1 Discouraged

System utilization is $U = 1-e^{-\lambda/\micro}$ 

the average number of customers is obtained as $E[n]=\bar{n}=\frac{\lambda}{\micro}$

to compute the sojourn time derive the throughput as $X=\micro \sum^{\infty}_{k=1}\pi_k=\micro(1-e^{-\lambda/\micro})$ 
and by little's formula $E[w]=\frac{E[n]}{X}=\frac{\lambda}{\micro^2(1-e^{-\lambda/\micro}})$  


## Distribution of Sojourn Time for M/M/1 queue 
### Pasta Property
probability of finding k customers in the system $\pi_k= \lim_{t \rightarrow \infty} Pr[N(t)=k]$ , can be interpreted as the fraction of time the system spends in state $E_k$. $\pi_k^{[a]}$ = Pr\[an arriving customer finds the system in state $E_k$]. 

Those 2 quantities aren't equals if we consider a D/D/1 queue (deterministic rates) such that $\lambda < \micro$ , where interarrival time are constants $\tau = 1/ \lambda$ as well as service times $\sigma = 1/ \micro$.  In this case we have 
$$
\begin{align}
\pi_0 = 1- \frac{\lambda}{\micro} && \pi_1 = \frac{\lambda}{\micro} &&(\pi_k=0,k>1)\\
\pi_0^{a}=1- \frac{\lambda}{\micro} && \pi_k^{a}=0 && k>0
\end{align}
$$
it follows that $\pi_k^a \neq \pi_k$ 

instead if we consider a Poisson arrival process this equality is true. let $A(t,t+\Delta t)$ be the event where an arrival occurs in time interval $(t,t+\Delta t)$ then $\pi_k^{a}(t)= \lim_{\Delta t \rightarrow 0} Pr[N(t)=k|A(t,t+\Delta t)]$ by exploiting the conditional probability
$$
\pi_k^{a}(t)=\lim_{\Delta t \rightarrow 0} \frac{
Pr[A(t,t+ \Delta t)| N(t)=k]Pr[N(t)=k]
}{
Pr[A(t,t+ \Delta t)]
}
$$
Since arrival process is Poisson (memory-less property) Event A must be independent of the state of the system from t itself and so
$Pr[A(t,t+ \Delta t)| N(t)=k] = Pr[A(t,t+ \Delta t)]$ that yields $\pi_k^{a}(t)=\pi_k(t)$ .

This is the PASTA property (Poisson arrivals see time averages): it states that an arrival from a Poisson process observes the system as if it was arriving in a random time instant. The average value of any queue parameter at Poisson arrivals is the long run time average of that parameter (avg queue length, p server is idle ecc...). 

## Distribution of sojourn time for M/M/1

let W be the RV representing the sojourn time of customers in FCFS M/M/1 station. 
let $W_n^{[a]}$ be the sojourn times given that an arriving customer finds n customers in the 
systems ($n^{[a]} = n)$ this RV can be written as: 
$$
W_n^{[a]}=\sigma + \omega_1 + \omega_2+...+\omega_{n-1}+R
$$

- where $\sigma$ represent the service time of the customer just arrived 
- $\omega_{1}, \omega_2,...,\omega_{n-1}$ represent service times of customers in the queue 
- R represent the remaining service time of the customer is service at arrival time. 

Since : All customers are statistically equivalent (they have same neg exp distribution with parameter $\micro$ and neg exp distribution is memoryless. Then $W_n^{[a]}$ is the sum of n+1 independent instances of the same neg exp RV X such that  $Pr\{X \leq t \} = 1 - e^{-\micro t}$ whose laplace transform of the ddp is $\frac{\micro}{s + \micro}$  

let $F_{W^{[a]}(n,t)=}Pr\{W_n^{[a]} \leq t\}$ be the CDF of RV $W_n^{[a]}$ and let $f_{W^[a]}(n,s)=(\frac{\micro}{s+\micro})^{n+1}$  be it's laplace transform. Thanks to the property of the Laplace transform of a convolution we observe that 
$$
Pr\{W \leq t\} = \sum^{\infty}_{k=0}Pr\{W_{k}^{[a]} \leq t| n^{[a]}=k\}Pr\{n^{[a]}=k\}
$$
When arrivals are represented by a Poisson process we have $\pi_{k}^{[a]}=\pi_{k},k \geq 0$ and then 
$$
F_{W}(t)=Pr\{W \leq t\}= \sum^{\infty}_{k=0}Pr\{W_{k}^{[a]} \leq t| n^{[a]}=k\}(1-\rho)\rho^{k}
$$
let $F^{*}_{W}(s)$ be the Laplace transform of this probability distribution 
let $f_{W}^{*}(s)$ be the Laplace transform of the PDF then 
$$
f_{W}^{*}=\sum^{\infty}_{k=0}f_{W^[a]}^{*}(k,s)(1-\rho)\rho^{k}=(1-\rho)\frac{\micro}{s+ \micro}(\frac{1}{1-\frac{\rho \micro}{s+ \micro}})=(\frac{\alpha}{s+\alpha})$$
where $\alpha=(1-\rho)\micro$ is the laplace transform of a neg exp distribution function with parameter $\alpha$ then $F_{W}(t)=Pr\{W \leq t\}= 1-e^{-\micro(1-\rho)t}$ 

## M/M/$\infty$ 
Dual system: the longer the queue the faster the service : $\lambda_k=\lambda$  and $\micro_k=k \micro$ , using the solution to birth death process. $\pi_k = \pi_0(\frac{\lambda}{\micro})^k \frac{1}{k!}$  yielding to 
$$
\begin{align}
\pi_0=e^{-\lambda/\micro} && \pi_k=\frac{(\lambda/\micro)^k}{k!}e^{-\lambda/\micro}
\end{align}
$$

where Ergodicity is satisfied when $\lambda/\micro < 1$ . Yielding to 

### Performance indices M/M/$\infty$
result are same as obtained for discouraged arrivals, it follows that $E[n]=\bar{n}=\frac{\lambda}{\micro}$

differ the average sojourn time: $E[w]=\frac{E[n]}{\lambda}=\frac{1}{\micro}$ , it depends only on the service time 

## M/M/m
same as M/M/1 but m identical servers working in parallel are available. Customers queue only when all servers are busy on arrival.  $\lambda_k-\lambda$  and $\micro_k = \begin{cases}k \micro & 0 \leq  k \leq m \\ m \micro & m < k\end{cases}$ plugging those rates in the solution to birth death process we obtain .
$$
\pi_k=
\begin{cases}
\pi_0 (\frac{\lambda}{\micro})^k \frac{1}{k!} & 0 \leq k \leq m \\ 
\pi_0 (\frac{\lambda}{\micro})^k \frac{1}{m!m^{k-m}} & m<k
\end{cases}
$$
Ergodicity conditions are satisfied when $\rho=\frac{\lambda}{m \micro}< 1$ yielding 
$$
\pi_k = 
\begin{cases}
\pi_0 \frac{(m \rho)^k}{k!} & 0 \leq k \leq m \\
\pi_0 \frac{\rho^k m^m}{m!} & m<k
\end{cases}
$$
with explicit expression for $\pi_k$ we obtain 
$$
\pi_0=[1+\sum^{m-1}_{k=1}\frac{(m \rho)^k}{k!}+ \sum^{\infty}_{k=m}(\frac{(m \rho)^m}{m!})(\frac{1}{1-\rho})]^{-1}
$$

previous result is computationally simple, but it doesn't allow the compute of the avg Sojourn time and avg number of customers. Instead we can compute the probability that has a client to queue up (with the Erlang C formula)

Pr{queue up}= 
$$
\sum^{\infty}_{k=m}\pi_k = \frac{ 
    (\frac{(m \rho)^m}{m!})(\frac{1}{1-\rho})
}{
[1+\sum^{m-1}_{k=1}\frac{(m \rho)^k}{k!}+(\frac{(m \rho)^m}{m!})(\frac{1}{1-\rho})
}
$$


## M/M/1/B queue with finite buffer 
same as M/M/1 but with finite room for queueing customers. If a customers arrives and the queue is full it leave the system. $\lambda_k = \begin{cases} \lambda & 0 \leq k \leq B \\ 0 & k > B\end{cases}$  and $\micro_k=\micro$ , plugging them in the BDP solution we obtain 
$$
\pi_k= 
\begin{cases}
\pi_0(\frac{\lambda}{\micro})^k & 0 \leq k \leq B \\
0 &k > B
\end{cases}
$$
The number of possible states is equal to B+1 so Ergodicity is not an issue. This yields to 
$$
\begin{align}
\pi_0=[\sum^{B}_{k=0}(\frac{\lambda}{\micro})^k]^{-1} = \frac{1-\lambda/\micro}{1- (\lambda/\micro)^{B+1}} && \pi_k=
\begin{cases}
\pi_0 (\frac{\lambda}{\micro})^k & 0 \leq k \leq B \\ 0 & k>B
\end{cases}
\end{align}
$$


No closed form expression is available for the avg number of customers and the avg sojourn time. For the case B=1 we obtain 

$$
\pi_k= 
\begin{cases}
\frac{1}{1+(\lambda/\micro)} & k=0 \\
\frac{\lambda/\micro}{1+(\lambda/\micro)} & k =1\\ 
0 & k>1
\end{cases}
$$


## M/M/1//N queue with finite population 
same as M/M/1 but with maximum number of customers equal to N. the arrival rate decrease as the number of customers in the queue increases: $\lambda_k= \begin{cases}\lambda(N-k) & 0 \leq k \leq N \\ 0 & k>N\end{cases}$ and $\micro_k=\micro$ , plugging them in the solution of BDP we obtain. 
This system is ergodic and then 
$$
\pi_k= 
\begin{cases}
\pi_0 \prod^{k-1}_{i=0}\frac{\lambda(N-i)}{\micro} & 0 \leq k \leq N \\
0 & k>N
\end{cases}
$$
that is 
$$
\pi_k = 
\begin{cases}
\pi_0(\frac{\lambda}{\micro})^k \frac{N!}{(N-k)!} & 0 \leq k \leq N \\
0 & k>N
\end{cases}
$$
obtaining 
$$
\pi_0 = [1+\sum^{N}_{k=1}(\frac{\lambda}{\micro})^k \frac{N!}{(n-k)!}]^{-1}
$$


Again no closed form expression for the avg number of customer in the system or sojourn time


## Constant batch size 
- Single queue
- customers arrive in a batch composed of K elements and are served one at a time
- queue has infinite room and distribution of times between arrival $\lambda$ and service $\mathcal{v}$ are independent RV with neg exp distribution 
![[Pasted image 20231208151614.png]]
assume that $P_{j}=0\  \ j<0$  then balanced equations becomes 
$$
\begin{align}
\lambda P_{0}= vP_{1} && (\lambda+\mathcal{v})P_{j}= \lambda P_{j-k}+\mathcal{v}P_{j+1}
\end{align}
$$
Direct solution is difficult, easier with [[Formulas#Z Transform | ZTransform]] . 
let $\mathcal{P}(z)= \sum^{\infty}_{j=0}P_{j}z^{j}$ , then multiply both sides of jth equation by $z^{j}$ , sum over all possible values of j, pay attention to the first equation (that involve $P_0$ ) 
we get 
$$
\sum^{\infty}_{j=0}(\lambda+\mathcal{v})P_{j}z^{j}-vP_0=\sum^{\infty}_{j=1}\lambda P_{j-k}z^{j}+\sum^{\infty}_{j=0}vP_{j+1}z^{j}
$$
that after some passages become (and z trasform application) becomes 
$$\mathcal{P}(z)=P_{0}\frac{v(1-z)}{\lambda z^{k+1}-(\lambda+v)z+v}$$
to compute $P_0$ we use $\lim_{z \rightarrow 1 }\mathcal{P}(z)=1$ because $P_j$ are prob distribution for $\mathcal{P}(z)$  both numerator and denominator tends t 0 as z tends to 1 therefore using Hospital rule 
$$
1= \lim_{z \rightarrow 1}P_{0}\frac{v(1-z)}{\lambda z^{k+1}-(\lambda+v)z+v}= P_{0}\frac{v}{v- k \lambda}
$$
yielding $P_0=1-\frac{k \lambda}{v}$ 

### Performance indices
the utilization of the queue can be defined as $\rho = \frac{k \lambda S}{v}=k \lambda s$ , so the initial expression can become $\mathcal{P}(z)= (1-\rho)\frac{v(1-z)}{\lambda z^{k+1}-(\lambda+v)z+v}$ before attempting to obtain the probability distribution of the number of customers in the system $P_j$ we exploit z trasform to obtain avg number of customers $\bar{N}_s$ 
$$
\bar{N}_{s}= \sum^{\infty}_{j=1}jP_{j}=\lim_{z \rightarrow 1}\sum^{\infty}_{j=1}jP_{j}z^{j-1}
$$
let's rewrite $\mathcal{P}(z) = (1 - \rho)\frac{v(1-z)}{\lambda z^{k+1}-(\lambda + v)z+v}=(1-\rho)\frac{N(z)}{D(z)}$  where 
$N(z)=v(1-z)$ and $D(z)=\lambda z^{k+1}-(\lambda+v)z+v$  we obtain 
$$
\begin{align}
\lim_{z \rightarrow 1}N(z)=N(z)|_{z=1}= 0 && \lim_{z \rightarrow 1}D(z)=D(z)|_{z=1}=0
\end{align}
$$
By so doing 
$$
\bar{N}_{s}= \lim_{z \rightarrow 1}\frac{d}{dz}[(1-\rho)\frac{N(z)}{D(z)}]=(1-\rho)\lim_{z \rightarrow 1}\frac{N'(z)D(z)-N(z)D'(z)}{D(z)^{2}}
$$
by repeatingly applying hospital rule we get 
$$
\bar{N}_s=(1-\rho)\lim_{z \rightarrow 1}\frac{N'''(z)D(z)+N''(z)D'(z)-N'(z)D''(z)-N(z)D'''(z)}{2[D'(z)]^{2}+2D(z)D''(z)} 
$$  

it follows that 
$$
\begin{align}
N'(z)|_{z=1}= -v|_{z=1}= -v && D'(z)|_{z=1}=(k+1)\lambda z^{k}-(\lambda+v)|_{z=1}= k \lambda - v\\
N''(z)|_{z=1}=0   && D''(z)|_{z=1}=k(k+1) \lambda z^{k+1}|_{z=1}= k(k+1) \lambda 
\end{align}
$$ 
substituting in  previous $\bar{N}_{s}$ we obtain 
$$
\bar{N}_{s}= \frac{\rho}{(1-\rho)}\frac{k+1}{2}
$$
to obtain the probability distribution of the number of customers in the service station $P_j$ we:
-compute the k+1 roots $(z_{0},z_{1},...,z_{k})$ of the denominator in $\mathcal{P}(z)$ as  $D(z)=v(1-z)(1-\frac{z}{z_1})(1-\frac{z}{z_{2}})...(1-\frac{z}{z_k})$ and simplify $$\mathcal{P}(z)=\frac{1-\rho}{\prod^{i=1}_{k}(1-\frac{z}{z_i})}$$  partial decomposition yield $\mathcal{P}(z)=(1-\rho)\sum^{k}_{i=1}\frac{A_i}{1-\frac{z}{z_i}}$  where $A_i=\prod^{k}_{h=1;h \neq i}\frac{1}{(1-\frac{z_i}{z_h})}$   
by using antitrasformation we obtain 
$$
    P_j=(1-\rho)\sum^{k}_{i=1}(z_{i})^{-j}A_{i}
$$ 
knowing that $P_0=(1-\rho)$ 

## Queue with variable batch size 
single queue, customers arrive in a batch whose size is represented by a strictly positive discrete RV with probability distribution 
$g_i=Pr[Bs= i]$  where $Bs$ is the batch size . Customers are served one at a time, infinite room for queueing, distribution of arrival times and service times are neg exp RVs. 

![[Pasted image 20231208185828.png]]
Assume $P_{j}=0$ then balance equations are 
$$
\begin{align}
\lambda P_{0}= vP_{1} && (\lambda+v)P_{j}= \sum^{j-1}_{i=0}\lambda P_{i}g_{j-1} +v P_{j+1}
\end{align}
$$
direct solution difficult, need to use Z transform 

let $\mathcal{P}(z)=\sum^{\infty}_{j=0}P_{j}z^{j}$  and let $\mathcal{G}(z)=\sum^{\infty}_{j=1}g_{j}z^{j}$ be the z transforms. Now multiply both sides of jth equation by $z^{j}$ , sum over all possible values of j, pay attention to the first equation $P_0$ . 
From the balance equations we obtain 
$$
(\lambda+v)\sum^{\infty}_{j=1}P_{j}z^{j}=\frac{v}{z}P_{j+1}z^{j+1}+\sum^{\infty}_{j=1}\sum^{j-1}_{i=0}P_{i}\lambda g_{j-i}z^{j}
$$
that can be transformed in  
$$
(\lambda +v) \sum^{\infty}_{j=1}P_{j}z^{j}= \frac{v}{z}P_{j+1}z^{j+1}+\lambda \sum^{\infty}_{i=0}P_{i}z^{i} \sum^{\infty}_{h=1}g_{h}z^{h}
$$
we indentify z trasforms and get 
$$
(\lambda + v)[\mathcal{P}(z)-P_{0}]= \frac{v}{z}[\mathcal{P}(z) - P_{0}-P_{1}z]+\lambda \mathcal{P}(z)\mathcal{G}(z) 
$$
so $\mathcal{P}(z)=P_{0}\frac{v(1-z)}{v(1-z)- \lambda z[1-\mathcal{G}(z)}$ in order to remove P0 we need to use hospital rule knowing $\lim_{z \rightarrow 1}\mathcal{P}(z)=1$  then we obtain 
$$
\begin{align}
P_0=1-\frac{\lambda \bar{g}}{v}=1 - \rho && \mathcal{P}(z)=(1-\rho)\frac{v(1-z)}{v(1-z)- \lambda z[1- \mathcal{G}(z)}
\end{align}
$$ 
### Performance indices for Variable batch
to compute the avg number in the system 
let $\mathcal{P}(z)=(1-\rho)\frac{N(z)}{D(z)}$ where 
$$
\begin{align}
N(z)=v(1-z) && D(z)=\lambda z G(z)-(\lambda+v) z + v
\end{align}
$$
then 
$$
\bar{N}_{s}=(1-\rho)\lim_{z \rightarrow 1} \frac{N'(z)D(z)-N(z)D'(z)}{[D(z)]^{2}}= \lim_{z \rightarrow 1} \frac{d}{dz}[(1-\rho)\frac{N(z)}{D(z)}=(1-\rho)\lim_{z \rightarrow 1} \frac{N'(z)D(z) - N(z)D'(z)}{[D(z)]^2} ^24a585
$$  
 by repeatingly using de l'hospital 
$$
 \bar{N}_s=(1-\rho)\lim_{z \rightarrow 1}\frac{N'''(z)D(z)+N''(z)D'(z)-N'(z)D''(z)-N(z)D'''(z)}{2[D'(z)]^{2}+2D(z)D''(z)} 
$$ 
the limit must be computed using l'hospital $\bar{N}_{s}= (1- \rho)\lim_{z \rightarrow 1}\frac{-N'(z)D''(z)}{2[D'(z)]}$ we observe 
$$
\begin{align}
N'(z) = -v|_{z=1}=-v && D'(z)|_{z=1}=\lambda G(z)+ \lambda G'(z)z-(\lambda+v)|_{z=1}=\lambda \bar{g}- v \\
N''(z)|_{z=1}=0 && D''(z)=2 \lambda G'(z)+ \lambda G''(z)z|_{z=1}= \lambda(\bar{g}+\bar{g^2})
\end{align}
$$
then $\bar{N}_{s}= \frac{\rho}{1-\rho}(\frac{1+ \bar{g}(CV^2[g]+1}{2})$  where $CV^2[g]=\frac{\bar{g^{2}-}(\bar{g})^2}{(\bar{g})^{2}}$

## M/$Er_k$/1 queue 
A RV X is distributed as an Erlang-k if it correspond to the distribution of a sum of k neg exp RVs with parameter $k \micro$ .
PDF: $$
b_{X}(x)=\frac{k \micro(k \micro x)^{k-1}e^{-k\micro x}}{(k-1)!}
$$  Avg: $E[X]=\frac{1}{\micro}$ , variance : $VAR[X]=\frac{1}{k}(\frac{1}{\micro^2})$ , coefficient of variation : $CV^{2}[X]=\frac{VAR[X]}{(E[X])^2}=\frac{1}{k}$ 

it doesn't enjoy memoryless property, then we cannot describe the state of the system just by using the number of customers. 
So describe the state as a pair (n,s) where n represents the number of customers in the service station and $1 \leq s \leq k$ represent which stage of the Erlang-k the served customer is at. Since service at each stage is distributed as a neg exp RV it follows we have a markov chain. The future state depends only on the current  state and not on the entire history of the process. 

![[Pasted image 20231209145233.png]]

- let $\pi(n,s)$ be the probability to have n customers in the service station (n-1 are waiting).
- let $P(n)=\sum^{k}_{s=1} \pi(n,s)$ be the marginal distribution as the probability n customers are in the service station regardless of the service stage the served customer is at.
- let $\mathcal{P}(s)=\sum^{\infty}_{n=1}\pi(n,s)$ be the marginal distribution as the probability that the sth stage is used by the served customer regardless the number of customer in the service station 
for both we assume $P(0)=\mathcal{P}(0)= \pi(0,0)$. 

### M/Er/1 direct solution 
Solution of balance equation is $0= \pi Q$  plus normalization condition $\pi(0,0) + \sum^{\infty}_{n=1}\sum^{k}_{s=1}\pi(n,s)=1$ whose explicit form is 
$$
\begin{cases}
\lambda \pi(0,0)= k \micro \pi(1,k) \\
 \\
(\lambda + k \micro) \pi(1,1)= \lambda \pi(0,0)+ k \micro \pi(2,k)  \\
(\lambda+ k \micro) \pi(1,s)= k \micro \pi(1,s-1) & s=2...k  \\
 \\
(\lambda + k \micro)\pi(n,1)= \lambda \pi(n-1,1)+k \micro \pi(n+1,k) & {n>1} \\
(\lambda + k \micro)\pi(n,s)=  \lambda \pi(n-1,s)+k \micro \pi(n,s-1) & n>1,s=2...k  \\
 \\
\pi(0,0) + \sum^{\infty}_{n=1}\sum^{k}_{s=1}\pi(n,s)=1
\end{cases}
$$
summing equations we get 
$$
\begin{cases}
\lambda \pi(0,0)= k \micro \pi (1,k) \\
\lambda \sum^{\infty}_{n=1}\pi(n,1) + k \micro \sum^{\infty}_{n=1}\pi(n,1)=\lambda \pi(0,0)+\lambda \sum^{\infty}_{n=2}\pi(n-1,1)+ k \micro \sum^{\infty}_{n=1}\pi(n+1,k) \\

\lambda \sum^{\infty}_{n=1}\pi(n,s) + k \micro \sum^{\infty}_{n=1}\pi(n,s)=\lambda \sum^{\infty}_{n=2}\pi(n-1,s)+ k \micro \sum^{\infty}_{n=1}\pi(n+1,s)  & s=2...k \\
\pi(0,0) + \sum^{\infty}_{n=1}\sum^{k}_{s=1}\pi(n,s)=1
\end{cases}
$$

let $\alpha(k)=\frac{\pi(1,k)}{\mathcal{P}(k)}$  and $\beta(k)=1-\alpha(k)$  the previous system becomes 
$$
\begin{cases}
\lambda \mathcal{P}(0)= k \micro \alpha(k) \mathcal{P}(k) \\
k \micro \mathcal{P}(1)= \lambda \mathcal{P}(0)+ k \micro \beta(k) \mathcal{P}(k) \\
k \micro \mathcal{P}(s)= k \micro \mathcal{P}(s-1) \\
\mathcal{P}(0)+\sum^{k}_{s=1}\mathcal{P}(s)=1
\end{cases}
$$

3rd equation yields $\mathcal{P}(1)=\mathcal{P}(2)=...=\mathcal{P}(k)$ and normalization conditions suggests they are equal to $\frac{(1-\mathcal{P}(0))}{k}$ 

### M/Er/1 Transformed diagram 

we now redefine the state of the system as the number of service stages to be completed before the service station empties. 

If n customers are in the station at time t and the served one is being serviced at the ith stage then the total stages before the station empties is 
$$
j = (n-1)k + (k-i+1)= nk -i + 1
$$
each arrival increase j by k and the departure decrease by 1. The state transition diagram is ![[Pasted image 20231209182726.png]]
same as the M/M/1 with fixed size batch. 

### M/Er/1 Performance parameters 
state probability is  $\phi=$ Pr{j service stages must be provided before emptying}, we are interested in 
$$
P(n)= \sum^{nk}_{j=k(n-1)+1}\phi(j)= \sum^{k}_{j=1}\phi(k(n-1)+j) 
$$
that is the probability n customer are in station regardless the stage received by the served one.  We can use the z trasform of M/M/1 fixed size by using $v = k \micro$
yielding $\rho = \frac{k \lambda}{k \micro}= \frac{\lambda}{\micro}$ and knowing that $\phi(0)= \pi(0,0) = (1-\rho)$

let $\bar{n}_s$ be the avg number of stages to complete and $\bar{n}$ the avg number of clients in the station.

$$
\bar{n}_{s}=\sum^{\infty}_{n=1}\sum^{kn}_{j=k(n-1)+1}j \phi(j)= \sum^{\infty}_{n=1}kn \sum^{k}_{I=1}\phi(k(n-1)+I)+\sum^{k}_{I=1}I \sum^{\infty}_{n=1}\phi(k(n-1)+I)
$$
let $P(n)=\sum^{k}_{I=1}\phi(k(n-1)+I)$  and $\mathcal{P(i)}= \frac{(1-\mathcal{P}(0)}{k}=\frac{\rho}{k}$  we obtain 
$$
\bar{n}_{s}=k\bar{n}+ \frac{\rho}{2}(k+1)- k \rho
$$
and $\bar{n}=\frac{1}{k}[\bar{n}_{s+}k \rho - \frac{\rho}{2}(k+1)]$ 

from M/M/1 model we know $\bar{n}_s=\frac{\rho}{1-\rho}\frac{k+1}{2}$ and by substituting in $\bar{n}$ 
$$
\bar{n} = \frac{\rho}{1-\rho}[1+\frac{\rho}{2}(C^2_{s}-1)]
$$
## M/Hk/1 queue 

PDF 
$$
b_{X(x)=}\sum^{R}_{i=1}\alpha_{i}\micro_{i}e^{-u_{i}x}, x \geq 0
$$
weights are such that 
$$
\sum^{R}_{i=1}\alpha_{i} = 1
$$

Average is  $E[X] =\sum^{R}_{i=1}\frac{\alpha_i}{\micro_i}$
variance is $VAR[X]=\sum^{R}_{i=1}\frac{\alpha_{i}}{\micro_{i}^2}$ 
state transition diagram is 
![[Pasted image 20231209204809.png]]

it can be shown that 
$\bar{n}=\frac{\rho}{1-\rho}[1+\frac{\rho}{2}(C_{s}^2-1)]$ also expressed as $\bar{n}=\rho +\frac{\rho^2[C_{s}^2+1]}{2(1-\rho)}$ 
and also as $\bar{n}=\rho +\frac{\rho^2+\lambda Var(S)}{2(1-\rho)}$  where Var(S) is the variance of service time distributions

service station is represented by 
![[Pasted image 20231209204949.png]]
