## Markov chains purpose

the answer to those type of questions:
- How long a gambler will play before ruins? 
- What is the probability that tomorrow will be sunny?

The markov chains are a set of models that evolute over time (sequential indexes). 

## Basic probability theory
 - A discrete RV X is completely characterized by it's PDF $F_x(x)=P[X=x]$  or probability that RV X is equal to x 
 - A continuos RV X is completely characterized by it's CDF $F_x(x)=P[X \leq x]$ , the pdf is often defined also as $f_x=\frac{dF_x(x)}{dx}$ 

Recall that given 2 Events A,B the conditional probability $P[A|B] = \frac{P[A,B]}{P[B]}$ , thus it follows 
$P[A,B]=P[A|B]*P[B]$  
## Stochastic process 
A stochastic process is a collection of RVs $\{X(t), t \in T\}$ all defined on a sample space defined by elements in the index set T.
3 elements must be specified:
- The process state space 
- the index parameter 
- dependencies among RVs in $\{X(t),t \in T\}$ 


## State space 
The state space of a stochastic process is the set of all possible values RV $X(t)$ can assume.

- If the set is finite or countable we have a discrete state stochastic process (or chain)
- Else is a continuos state stochastic process whose state space is represent by a subset of the set of real number

## Index 
If the index set T is finite we have a discrete time stochastic process (at the end of the day ecc..). Otherwise the process is called continuous time. 

for discrete we denote it as $\{X_n,n \geq 0\}$ 
for continuous we denote it as $\{X(t),t \geq 0\}$  

## Statistical dependencies 
Denote all random variables as a vector $X=[X(t_1),X(t_2),...]$ , To fully characterize the joint probability distribution function (PDF) of the stochastic process:
$F_x(x;t)=P[X(t_1) \leq x_1, X(t_2) \leq x_2,...,X(t_n) \leq x_n]$  all $x=(x_1,x_2,...,x_n)$  and $t=(t_1,t_2,...,t_n)$ 
must be specified, and this can be only done by imposing some restrictions.

using the definition of conditional probability $P[A,B]=P[A|B]*P[B]$ we can write the joint pdf as the product of 2 factors:
$$
\begin{align}
P[X(t_1) \leq x_1,..., X(t_n) \leq x_n,X(t_n+1) \leq x_n+1]= \\ P[X(t_{n+1}) \leq x_{n+1}| X(t_1) \leq x_1,...,X(t_n) \leq x_n]*P[X(t_1) \leq x_1,...,X(t_n) \leq x_n]
\end{align}
$$ 
 repeating the same reasoning we obtain 
$$
\begin{align}
P[X(t_{n+1}) \leq x_{n+1}| X(t_1) \leq x_1,...,X(t_n) \leq x_n]*\\
P[X(t_{n}) \leq x_{n}| X(t_1) \leq x_1,...,X(t_{n-1}) \leq x_{n-1}]*\\
P[X(t_{n-1}) \leq x_{n-1}| X(t_1) \leq x_1,...,X(t_{n-2}) \leq x_{n-2}]*\\...\\ 
P[X(t_1) \leq x_1]
\end{align}
$$

## Class of stochastic processes 
- Stationary process: for any constant $\tau$ is true $F_x(x;t+\tau)=F_x(x;t)$  where $t+\tau=(t_1+\tau,t_2+\tau,...,t_n+\tau)$ 
- independent processes: if the joint PDF (in case of continuous space) factorize: $f_X(x;t)=f_{X1}(x_1;t_1) ... f_{Xn}(x_n;t_n)$ 
- Markov process: a discrete state stochastic process (a chain) is said to satisfy the markov property if $P[X(t_n+1) = x_n+1| X(t_n)=x_n,...,X(t_1)=x_1]=P[X(t_{n+1})=x_{n+1}| X(t_n)=x_n]$ 

## Discrete time markov chains
stochastic processes: discrete state space (chain), discrete time (index set is finite), satisfy markov property

for DTMC $\{X_n\}$ we write the markov property as $P[X_n=j|X_1=x_1,...,X_{n-1}=x_{n-1}]=P[X_n=j|X_{n-1}=x_{n-1}]$ 
if we know the initial probability distribution $P[X_0=k]$ we can obtain any state at time n.

The probability at the right hand side in the previous equation is called transition probability $p_{ij}(n)=P[X_n=j|X_{n-1}=i]$ , if transition probability are independent of n we have a time homogeneous DTMC where we denote $p_{ij}=P[X_n=j|X_{n-1}=i]$ the transition probabilities. Furthermore $\forall i , \sum_j p_{ij}=1$ 

### Graph representation 
A DTMC can be represented as a state transition diagram that is a weighted graph directed where:
- The number of nodes is equal to the number of states 
- there is an arc from node i to node j if $p_{ij}>0$ 
- the weight of arc is equal to $p_{ij}$ 
![[Pasted image 20231202154042.png]]
### Matrix representation
a DTMC can be represented as a square transition probability matrix P where:
- the dimension d is equal to the number of states 
- element in row i comlumn j is equal to $p_{ij}$ 
- all rows of P sum to 1
this matrix is said to be a stochastic matrix 

$$
P = \begin{pmatrix}
p_{11} && p_{12} &&...&&p_{1d}\\
p_{21} && P_{22} &&...&&p_{2d}\\
...\\
p_{d1} && p_{d2} && ... && p_{dd}
\end{pmatrix}
$$

## Time homogeneous DTMC 
in a time-homogeneous DTMC transition probabilities are stationary, the probability to be in a certain state after m steps depends only on m.
$p_{ij}^{(m)}=P[X_{n+m}=j|X_n=i]$ is the m-step transition probabilities. 
For the markov property $p_{ij}^{(m)}=\sum_{k}p_{ik}^{(m-1)}p_{kj}$ .

### Definitions 
- A DTMC is irreducible if any state can be reached from any other state. Formally $\forall i,j \ \exists m_0(i,j):p_{ij}^{(m_0(i,j))}>0$ 
- A subset C of the state space is said to be closed if no 1 step transition is possible between states in C and outside C. if |C|=1 that state is absorbing 
- if the state space is closed and doesn't contain any closed subset then DTMC is irreducible 

### Solution To DTMC
Solve a DTMC means compute $\pi_j^{(n)}=P[X_n=j]$  that is the probability the state of the DTMC at the nth step is equal to j. This is can be done knowing the initial $P[X_0=k]$

In a time-homogeneous, irreducible and aperiodic DTMC the limit probabilities $\pi_j=\lim_{n \rightarrow \infty} \pi_j^{(n)}$ always exists and are idependent of the initial state. Also:
- if all states are transient or null recurrent --> $\pi_j=0$ for all state and a steady state solution do not exists 
- else if all are positive recurrent --> $\pi_j>0$ for all states and $\{\pi_j\}$ is the steady state solution with $\pi_j=\frac{1}{M_j}$ 

### Return probabilities 
In order to classify states of a DTMC define
$f_j^{(n)}=$ P\[return to state j occurs n step after leaving it]

we can then derive the probability to return to state j as $f_j=\sum^{\infty}_{n=1}f_j^{(n)}$ 

- if $f_j=1$ state j is recurrent
- if $f_j<1$ state j is transient 
- If the step necessary to return to state j is $\gamma,2 \gamma, 3 \gamma$ where $\gamma$ is the largest integer satisfy this condition the state j is called period with period $\gamma$
- if $\gamma = 1$ then state j is aperiodic
The average recurrence time is defined as $M_j=\sum^{\infty}_{n=1}nf_j^{(n)}$ 
- if $M_j=\infty$ state j is called null recurrent 
- if $M_j<\infty$ state j is called positive recurrent 

### Sojourn time DTMC
the units of time spent without interruptions in each state is distributed according to a geometric distribution. Assume state j is just entered: 
- The probability next state is still j is equal to $p_{jj}$ 
- dual for not being in j $1-p_{jj}$ 

thanks to the markov property (memoryless) the probability next state is still j doesn't depend on how many times we hit j. So the probability the state in j after m steps is 
$(1-p_{jj})p_{jj}^m$ 

the Geometric distribution is the only memoryless discrete distribution 
### Transient state distribution for DTMC
let $\pi^{(n)} = [\pi^{(n)}_0,\pi^{(n)}_1,\pi^{(n)}_2,...]$ be the probability vector of the state of the DTMC at the nth step (each element represent the probability to be in that state at time n). 

thus $\forall i, \pi_i^1=\pi_0^0p_{0i}+\pi_1^0p_{1i}+\pi_2^0p_{2i}+...$  in matrix form $\pi^{(1)}=\pi^{(0)}P$ (i.e. the distribution at the 1 pass is equal to summing probability at pass 0 with the product of the transition probabilities).

and so $\pi^{(2)}=\pi^{(1)}P=\pi^{(0)}P^2$ . Thus we can say $\pi^{(n)}=\pi^{(0)}P^n$  (this is the power matrix method).
Also $\pi^{(n)}=\pi^{(n-1)}P$ (we can compute the distribution at n just knowing the vector at the precedent pass i.e vector multiplication method). 


### Ergodicity
- a state i is said to be ergodic if it is aperiodic and positive recurrent 
- if all state of a DTMC are ergodic, the chain is ergodic.
 ![[Pasted image 20231203114257.png]]



### limit state distribution 
in this kind of chains the limit probabilities $\pi_j=\lim_{n \rightarrow \infty}\pi_j^{(n)}$  (i.e the steady state solution) always exists and are independent of the initial state.
By definition we have $\pi=[\pi_0,\pi_1,\pi_2,...] = \lim_{n \rightarrow \infty}\pi^{(n)}$ 
- if we start from $\pi^{(n)}=\pi^{(0)}P^n$ --> $\lim_{n \rightarrow \infty} \pi^{(n)} = \lim_{n \rightarrow \infty}\pi^{(0)}P^n$ , thus $\pi = \pi^{(0)}P^{\infty}$. 
- else from $\pi^{(n)}=\pi^{(n-1)}P$ --> $\lim_{n \rightarrow \infty}\pi^{(n)}=\lim_{\rightarrow \infty}\pi^{(n-1)}P$.
 
in all case we obtain $\pi = \pi P$ , this matrix equation represent the system of linearly dependent
equations $\pi_j=\sum_i \pi_i p_{ij}$ with the normalizing condition $\sum_i \pi_i = 1$ we obtain a unique solution. 

The rows of $P^\infty$ are all equal to the limit distribution $\pi$ , since $\pi=\pi^{(0)} P^\infty$ for any value of $\pi^{(0)}$ 
$$
P^\infty=
\begin{bmatrix}
\pi_0 && \pi_1 && \pi_2 && ... \\
\pi_0 && \pi_1 && \pi_2 && ... \\
\pi_0 && \pi_1 && \pi_2 && ... \\
...
\end{bmatrix}
$$

### Using the Z transform 
it is possible to use to Z transform of $\pi^{(n)}=\pi^{(n-1)}P$ in order to obtain $P^n=C+(n+1)(-\frac{1}{4})^n D_1+(-\frac{1}{4})^nD_2$ and have a more simple computation respect to the power matrix method in order to compute steady state solutions. 

let $\Pi(z)= \sum^{\infty}_{n=0}\pi^{(n)}z^n$ where z is a complex variable such that $|z| \leq 1$ and after some algebra 
$\Pi(z)= \pi^{(0)}[I-zP]^{-1}$ . Using anti transformation we obtain $\pi^{(n)}=\frac{1}{n!}\frac{d^n \Pi(z)}{dz^n}$ matrix inversion for $[I-zP]^{-1}$ 
will lead to the solution.

## Non homogeneous DTMC
let $p_{ij}(m,n)= Pr\{X_n=j|X_m=i\}$ that is the probability the chain is in state j at time n given that it was in sate i at time m $n \geq m$ . 
Transition from state i to state j must occur through some intermediate state k at time q (i-->k-->j). 

probability can be espressed as  $p_{ij}(m,n) =\sum_k Pr\{X_n=j,X_q=k|X_m=i\}$.

### Chapman kolmogorov equation 
using the definition of conditional probability and conditioning both sides of A $P[B,C|A]=P[B|A]*P[C|A,B]$ 

- let A-->$X_m=i$ , B-->$X_q=k$ , C-->$X_n=j$ => $p_{ij}(m,n)=\sum_kPr\{X_q=k|X_m=i\}Pr\{X_n=j|X_q=k,X_m=i\}$ 

Then from markov property we derive the chapman kolmogrov equation 
$$
p_{ij}(m,n)=\sum_kp_{ik}(m,q)p_{kj}(q,n)
$$
 
(i.e the probability of transition is the sum of all probabilities of transition from state i to k and to k to j). For time homogeneous DTMC it simplifies to $p_{ij}^{(n-m)}=\sum_kp_{ik}^{(q-m)}p_{kj}^{(n-q)}$  
### Transition probabilities DTMC
matrix P is actually a function of time n $P(n)=[p_{ij}(n,n+1)]$ . So after k steps transition probabilities is not the kth power of P.

let $H(m,n)=[p_{ij}(m,n)]$ , hence $H(n,n+1)=P(n)$.

in matrix form Chapman-Kolmogrov equations reads as  $H(m,n)=H(m,q)H(q,n)$ with the additional condition $H(n,n)=I$ , known also as forward chapman kolmogorov

backward is just $H(m,n)=P(m)H(m+1,n)$ both describe the same phenomenon.

Similarly is possible to show that $\pi^{(n+1)}=\pi^{(n)}P(n)$  whose solution is $\pi^{(n+1)}=\pi^{(0)}H(0,n+1)$ 
 
and also in the time homogeneous case  $\pi^{(n+1)}=\pi^{(0)}P^{n+1}$

### Global balance equation DTMC
matrix equation for the limit solution of state probabilities is $\pi=\pi P$ and the jth component is $\pi_j=\sum_i \pi_ip_{ij}$ that can be also written as 
$$
(1-p_{jj})\pi_j=\sum_{i \neq j}\pi_i p_{ij}
$$
Left hand side:
$P_{jj}$ is the probability that the probability mass $\pi_j$ does not flow out state j. And so the dual for $(1-p_{jj})$ . Thus $(1-p_{jj})\pi_j$ is the fraction of probability mass flowing out of state j. 

Right hand side
for any other state i where $i \neq j$ quantity $\pi_ip_{ij}$ is the probability mass flowing out state i and entering state j. It follows that $\sum_{i \neq j} \pi_i p_{ij}$ is the total probability mass flowing into state j. 

### Detailed balance equation DTMC
for a vector $\pi$ detailed balance equation is satisfied for all i,j if 
$$
\pi_ip_{ij}=\pi_jp_{ji}
$$
left hand side:
fraction of probability mass $\pi_i$ flowing out from state i to state j

right hand side:
fraction of probability mass $\pi_j$ flowing out from state j to state i

### Birth Death process  DTMC
special case of DTMC,
- state change can be only of 1 unit at a time (1 birth,1death).
- transition probabilities don't change with time (time homogeneous)

$$
p_{ij}=
\begin{cases}
&d_i && j=i-1\\
&1-b_i-d_i && j=i\\
&b_i && j=i+1\\
&0
\end{cases}
$$
when DTMC is in state i:
- $b_i$ represent the probability that a bird occurs, if the max population N is limited then $b_N=0$ and the N+1 row is $[0...0 \ d_n \ 1- d_n]$ 
- $d_i$ represent the probability that a death occurs 
- $1-b_i-d_i$ represent the probability that no event occurs.

### Balance equations BDP
- for all states i>0: $\pi_i(b_i+d_i)=\pi_{i-1}b_{i-1}+\pi_{i+1}d_{i+1}$
- if i = 0 : $\pi_0b_0=\pi_1d_1 \Rightarrow \pi_1=\pi_0 \frac{b_0}{d_1}$ 

and so for any i
$$
\pi_i=\pi_0*\frac{b_0 b_1 ... b_{i-1}}{d_1 d_2 ... d_i} 
$$
with the normalization condition $\sum_i \pi_i=1$ we also get $\pi_0=\frac{1}{\sum^{\infty}_{i=0}\prod^{i}_{h=1}\frac{b_h-1}{d_h}}$ 
when both birth and death probabilities are independent $\begin{cases}b_i=b & \forall i \\ d_i=d & \forall i\end{cases}$  and $\pi_i=\pi_0(\frac{b}{d})^i$ 

if $b<d$ all states are positive recurrent  $\pi_0=(1-\frac{b}{d})$  and $\pi_i=(1-\frac{b}{d})(\frac{b}{d})^i$ 


## Continuos time Markov chains
a stochastic process $\{X(t)\}$ is continuous time markov chains if for any integer n and for any sequence of time instants $t_0,t_1,t_2,...,t_n$ and t (such that $t_0<t_1<...<t_n<t$)  it holds that 

$$
Pr\{X(t)=x|X(t_n)=x_n,X(t_{n-1})=x_{n-1},...,X(t_0)=0\}=Pr\{X(t)=x|X(t_n)=x\}
$$
Again the future state depends only on the current state.


### Sojourn time in CTMC
 because of memoryless property, soujourn times in CTMC are distributed as negative exponential RV.

let $\tau_i$ be the RV we are looking for the sojourn time in state i. The distribution of the additional time in state i does not depend on the time the process has already spent in state i. We can then write $Pr\{\tau_i > s+t|\tau_i >s\} = h(t)$ . Where h(t) is a function of the additional time t and not a function of the time already spent s. 

using conditional probability $h(t)=\frac{Pr\{\tau_i> s+t\}}{Pr\{\tau_i>s\}}$  , because $\tau_i>s+t$ implies $\tau_i>s$ 
$Pr\{\tau_i>s+t\}=Pr\{\tau_i>s\}h(t)$ 

if we set s=0 we observe that $Pr\{\tau_i>0\}=1$ obtaining $Pr\{\tau_i>t\}=h(t)$ and so
$Pr\{\tau_i>s+t\}=Pr\{\tau_i>s\}Pr\{\tau_i>t\}$ 

let $f_{\tau_i} = \frac{d}{dx}(P[\tau_i \leq x])$ be the PDF of RV $\tau_i$ , then 
1) $\frac{d}{dx}(P[\tau_i>x])=\frac{d}{dx}(1-P[\tau_i \leq x])=-f_{\tau_i}(x)$ 
2) derive $P\{\tau_i>s+t\}= P\{\tau_i\}P\{\tau_s\}$ with respect to s $\frac{dP\{\tau_i>t+s\}}{ds}=-f_{\tau_i}(s)P\{\tau_i>t\}$ 
3) let s= 0 and divide by $P\{\tau_i>t\}$ --> $\frac{dP\{\tau_i>t\}}{P\{\tau_i>t\}}=-f_{\tau_i}(0)ds$ 
4) $\int^{t}_{0}-f_{\tau_i}(0)ds=\log_eP\{\tau_i>t\}=-f_{\tau_i}(0)t$ --> $P\{\tau_i>t\}=e^{-f_{\tau_i}(0)t}$ 
5) from 1 --> $f_{\tau_i}(t)=f_{\tau_i}(0)e^{-f_{\tau_i}(0)t}$  
h(t) is the distribution of both additional and global sojourn time, so the only possible distribution is $f_X(x)=\lambda e ^{-\lambda x}$ with $E[X]=\frac{1}{\lambda}$  

### Transient solution CTMC
let $p_{ij}(m,n)=P[X_n=j|X_m=i]$ , define $p_{ij}(s,t)=P[X(t)=j|X(s)=i]$.
as for DTMC $p_{ij}=\sum_kp_{ik}(s,u)p_{kj}(u,t) \ \ \ s \leq u \leq t$ --> matrix form $H(s,t)=[p_{ij}(s,t)]$ 

chapman kolmogorov is given by $H(s,t)=H(s,u)H(u,t)$ , with $H(t,t)=I$ (identify matrix)

let $P(t)=[p_{ij}(t,t+\Delta t)]$ , then rewrite as $H(s,t+ \Delta t)=H(s,t)P(t)$. Apply some algebra and obtain $\frac{H(s,t+\Delta t)-H(s,t)}{\Delta t}=H(s,t)\frac{P(t)-I}{\Delta t}$ , let $Q(t)=\lim_{\Delta t \rightarrow \infty}\frac{P(t)-I}{\Delta t}$ , then 
$$
\frac{\updelta H(s,t)}{\updelta t} = H(s,t)Q(t)
$$

Q(t) is the infinitesimal generator (transition rates matrix) for transition matrix H(s,t).
elements of Q(t) are defined as 
$$
q_{ij}(t)=\begin{cases}
\lim_{\updelta t \rightarrow 0}\frac{p_{ij}(t,t+\Delta t)-1}{\Delta t} & i = j \\ 
\lim_{\Delta t \rightarrow 0} \frac{p_{ij}(t,t+ \Delta t)}{\Delta t} i & i \neq j
\end{cases}
$$
interpretation:
set state of CTMC equal to i at time t and wait for $\Delta t$ time units. If state at $t+ \Delta t$ is j the experiment is positive, repeat the experiment.

We observe: The number of experiments in a time unit is $\frac{1}{\Delta t}$ , then the average number of positive experiments is $\frac{p_{ij}(t,t+\Delta t)}{\Delta t}$ , when $\Delta t \rightarrow 0$ quantity $q_{ij}(t)$ represent the avg number of transition from state i to state j in a time unit.

$-q_{ii}(t)$ is the rate the system leaves state i at time t. Since it's always true that $\sum_jp_{ij}(s,t)=1$ it follows that $\sum_jq_{ij}(t)=0$ for all states i. It follows that $q_{ii}(t)= -\sum_{j \neq i}q_{ij}(t) \ \ \ \forall i$   

### Steady state solution
remember ergodicity --> $\lim_{t \rightarrow \infty} \pi_j(t)=\pi_j$. If we apply the time limit to the differential equation for the transient solution we obtain 
$$
\lim_{t \rightarrow \infty}\frac{d \pi_j(t)}{dt}=\lim_{t \rightarrow \infty}q_{jj}(t)\pi_j(t)+\lim_{t \rightarrow \infty}\sum_{k \neq j}q_{kj}(t)\pi_k(t)
$$



with a time homogeneous CTMC it simplifies to $0=q_{jj}\pi_j+\sum_{k \neq j}q_{kj}\pi_k$ , in matrix form $\pi Q =0$ 
adding the normalizing conditions $\sum_j \pi_j=1$ the steady state solution can be obtained.


### Chapman kolmogorov equations CTMC

- $\frac{\updelta H(s,t)}{\updelta t} = H(s,t)Q(t)$ is the forward champan kolmogorov equation.
- $\frac{\updelta H(s,t)}{\updelta s} = -Q(s)H(s,t)$ is the backward Chapman kolmogorov equation.
a Generic component of the forward eq. is 
$$
\frac{\updelta p_{ij}(s,t)}{\updelta t} = q_{jj}(t)p_{ij}(s,t)+ \sum_{k \neq j}q_{kj}(t)p_{ik}(s,t)
$$
with  initial condition $p_{ij}(s,s)=\begin{cases}1 & j=i \\ 0 & j \neq i\end{cases}$
same equations hold for state probabilities $\pi_j(t)=P[X(t)=j]$  in the discrete case. It can be shown that $\pi(t)=\pi(0)H(0,t)$ similar to $\pi^{(n+1)}=\pi^{(0)}H(0,n+1)$  in discrete time.

using formward CK equation for s=0 and introducing $\pi(0)$ we obtain $\frac{d \pi(t)}{dt}=\pi(t)Q(t)$ 
whose explicit form yields 
$$
\frac{d \pi_j(t)}{dt}=q_{jj}(t)\pi_j(t)+\sum_{k \neq j}q_{kj}(t)\pi_k(t)
$$
this system of differential equation is resolvable through transformations. An explicit solution can be made if Q(t)=Q (q doesn't depend on time t). The solution simplifies to 
$\pi(t)=\pi(0)H(t)$ where $H(t)=e^{Qt}$  and then 
$$
e^{Qt}=\sum^{\infty}_{k=0}\frac{(Qt)^k}{k!} 
$$


### Alternative derivation of the CK equations 
information contained in Q can be graphically represented as a state transition diagram. A node for each state and weighted arcs with rate $q_{i,j}$ . Diagonal elements of Q are not represented (they depend on the row values, they are the sum*-1 of the row.). $o(\Delta t)$ is probability of Multiple deaths and births

[continue on slides]

### Continuous birth death process 
birth is transition from state j to state j+1, occurs at rate $\lambda_i$ 
death is transition from state j to state j-1, occurs at rate $\micro_j$ .
we have then $\lambda_j=q_{j,j+1}$  and $\micro_j=q_{j,j-1}$ 

we assume:
- $p_{k,k+1}=$P\[1 birth in $(t,t+\Delta t)$ state | state is k\]= $\lambda_k \Delta t + o(\Delta t)$ 
- $p_{k,k-1}$=P\[1 death in $(t,t+\Delta t)$ state | state is k\]= $\micro_k \Delta t + o(\Delta t)$
- P\[0 births in $(t,t+\Delta t)$ | state is k \] = $1 - \lambda_k \Delta t+ o(\Delta t)$
- P\[ deaths in $(t,t + \Delta t)$| state is k] = $1 -\micro_k \Delta t+o(\Delta t)$ 
- $p_{k,k}=$ P\[0 births in $(t,t+ \Delta t)$, 0 deaths in $(t,t+ \Delta t)$| state is k\]
probability of multiple births and deaths is $o(\Delta t)$ 

### Continuous birth death process : state diagram 
![[Pasted image 20231207130743.png]]
$\frac{d \pi_k(t)}{dt}$ = incoming rate in state k - outgoing rate from k= $\pi_{k-1}(t)\lambda_{k-1}+\pi_{k+1}(t)\micro_{k+1} - \pi_k(t)(\lambda_k+\micro_k)$
already derived in CK equations $\frac{d\pi_j(t)}{dt}=q_{jj}(t)\pi_j(t)+\sum_{k \neq j}q_{kj}(t)\pi_k(t)$ 
for a set of states up to k $\frac{d(\sum^{k}_{h=0}\pi_h(t))}{dt}=-\pi_k(t)\lambda_k+\pi_{k+1}(t)\micro_{k+1}$ 

### Pure birth process 
defined as : all rates $\micro_k=0$ for any $k \geq  1$ , $\lambda_k=\lambda$ for any $k \geq 0$ , the system of differential equations become 
$$
\begin{cases}
\frac{d \pi_k(t)}{dt}= -\lambda \pi_k(t)+ \lambda \pi_{k-1}(t) & k \geq 1 \\
\frac{d \pi_0(t)}{dt} = -\lambda \pi_0(t)
\end{cases}
$$
with initial conditions : $\pi_k(0)=1$ for k=0 and $\pi_k(0)=0$ otherwise (0 elements at time 0).
for the second diff eq $\pi_0(t)=e^{-\lambda t}$ , using in general eq for k=1 
$$
\frac{d \pi_1(t)}{dt}= -\lambda \pi_1(t)+\lambda e ^{-\lambda t}
$$
with solution $\pi_1(t)=(\lambda t)e^{-\lambda t}$ , and by induction 
$$\pi_k(t)=\frac{(\lambda t)^k}{k!}e^{-\lambda t}$$  for k>0 and $t \geq 0$ 

This is the poisson distribution, it follows that: 
- a pure birth process with rate $\lambda$ constant generate a sequence of events that is a poisson process.
- The distribution of time between successive events is distributed according to a neg exp RV with parameter $\lambda$ 
- probability at time $\tau$ between 2 consecutive births is $\leq t$ is $1-Pr\{\tau>t\}=1-\pi_0(t)=1-e^{\lambda t}$ 
### Pure birth process: Z transform 
an alternative method to obtain the equation for pure birth process is to use z trasform.
let $f_n$ be $F(z)= \sum^{\infty}_{k=0}f_kz^k$ , a known property of the z trasform is $f_n=\lim_{z \rightarrow 0} \frac{1}{n!}\frac{d^nF(z)}{dz^n}$.

to obtain the z trasform of our sequence $\pi_k(t)$ for all k:
$$P(z,t)=\sum^{\infty}_{k=0} \pi_k(t)z^k$$
multiply each differential equation for state k by $z^k$ as 
$$
\begin{cases}
z^0 \frac{d \pi_0(t)}{dt}= -\lambda \pi_0(t)z^0 \\
z^k \frac{d \pi_k(t)}{dt} = -\lambda \pi_k(t)z^k+\lambda \pi_{k-1}(t)z^k & k \geq 1
\end{cases}
$$
sum over all k both sides 
$$
\sum^{\infty}_{k=0}z^k \frac{d \pi_k(t)}{dt}=-\lambda \sum^{\infty}_{k=0}\pi_k(t)z^k+\lambda z \sum^{\infty}_{k=1}\pi_{k-1}(t)z^{k-1} 
$$
we then obtain $\frac{d P(z,t)}{dt}= -\lambda(1-z)P(z,t)$ , since $\lim_{z \rightarrow 1}P(z,t)=1$ we have $P(z,t)=e^{-\lambda(1-z)t}$ 

then $\pi_0(t)=\lim_{z \rightarrow 0}P(z,t)=e^{-\lambda t}$ 
and $\pi_k(t)=\lim_{z \rightarrow 0}\frac{1}{k!}\frac{d^kP(z,t)}{dz^k}=e^{-\lambda t}\frac{(\lambda t)^k}{k!}$ 


### Derivation from CK equations 

1) CK equations at time $t + \Delta t$  , we want to obtain $\pi_k=Pr\{X(t)=k\}$ state at time $t+\Delta t$ is k and only one events can occur at time t: state is k and no event occurred, state is k-1 and one birth occurred, state is k+1 and one death occurred 
for $k \geq 1$  we obtain :
$$
\pi_k(t+\Delta t)= \pi_k(y)p_{kk}(\Delta t)+\pi_{k-1}(t)p_{k-1,k}(\Delta t)+ \pi_{k+1}(t)p_{k+1,k}(\Delta t) + o(\Delta t) 
$$
last term account for multiple events whose probability tends to 0 (is trascurable)
for k=0:
$$
\pi_0(t+\Delta t)= \pi_0(t)p_{0,0}(\Delta t)+ \pi_1(t)p_{1,0}(\Delta t) + o(\Delta t)
$$



2) with normalizing equation $\sum_k \pi_k(t)=1$. Using this hypothesis in time interval $(t + \Delta t)$ 
for $k \geq 1$ :
$$
\begin{align}
\pi_k(t+\Delta t)= \pi_k(t)[1- \lambda_k \Delta t+o(\Delta t)][1-\micro_k \Delta t + o(\Delta t)]+ \\
\pi_{k-1}(t)[\lambda_{k-1} \Delta t+ o(\Delta t)] + \pi_{k+1}(t)[\micro_{k+1} \Delta t+ o(\Delta t)]+ o(\Delta t)
\end{align}
$$
$k=0$:
$$
\pi_0(t+ \Delta t)= \pi_0(t)[1-\lambda_0 \Delta t+o(\Delta t)]+ \pi_1(t)[\micro_1 \Delta t+o(\Delta t)]+o(\Delta t)
$$

3) group all quantities multiplied by $o(\Delta t)$ and neglect $[o(\Delta t)]^2$ terms 
$k \geq 1$:
$\pi_k(t + \Delta t)= \pi_k(t)- \pi_k(t)[(\lambda_k+\micro_k) \Delta t] + \pi_{k-1}(t)[\lambda_{k-1}\Delta t]+ \pi_{k+1}(t)[\micro_{k+1}\Delta t]+o(\Delta t)$ 

$k=0$
$\pi_0(t+\Delta t)= \pi_0(t)-\pi_0(t)\lambda_0 \Delta t+ \pi_1(t)\micro_1 \Delta t+ o(\Delta t)$ 

4) Apply some algebra 
$k \geq 1$  
$$
\frac{\pi_k(t+\Delta t) - \pi_k(t)}{\Delta t}= -\pi_k(t)(\lambda_k+\micro_k)+\pi_{k-1}(t)\lambda_{k-1}+\pi_{k+1}(t)\micro_{k+1}+\frac{o(\Delta t)}{\Delta t} 
$$
$k=0$
$$
\frac{\pi_0(t+ \Delta t)- \pi_0(t)}{\Delta t} = -\pi_0(t)\lambda_0+ \pi_1(t) \micro_1+ \frac{o(\Delta t)}{\Delta t} 
$$


5) taking the limit for $\Delta t \rightarrow 0$ and recalling $\lim_{\Delta t \rightarrow 0}\frac{o(\Delta t)}{\Delta t} = 0$ 
$k \geq 1$
$$
\frac{d \pi_k(t)}{dt}= -\pi_k(t)(\lambda_k+\micro_k)+\pi_{k-1}(t)\lambda_{k-1}+\pi_{k+1}(t)\micro_{k+1}
$$
$k=0$
$$
\frac{d \pi_0}{dt}= -\pi_0(t)\lambda_0+\pi_1(t)\micro_1
$$

### Birth death process with constant rates 
focus on $\lambda_k = \lambda$  and $\micro_k=\micro$ for k=0,1,2.... with CK equations 
$k \geq 1$ 
$$
\frac{d \pi_k(t)}{dt}= -(\lambda+\micro)\pi_k(t)+\lambda \pi_{k-1}(t)+\micro \pi_{k+1}(t)
$$
k =0 
$$
\frac{d \pi_0(t)}{dt}= -\lambda \pi_0(t)+\micro \pi_1(t)
$$
using the z transform (see other block) we obtain 

$$
\pi_k(t) = e^{-(\lambda+\micro)t}[\rho^{\frac{k-n}{2}} I_{k-n}(\alpha t) + \rho^{\frac{k-n-1}{2}}I_{k+n+1}(\alpha t) + (1-\rho)\rho^k \sum^{\infty}_{j=k+n+2}\rho^{-\frac{j}{2} I_j(\alpha t)}]
$$
where $\rho = \frac{\lambda}{\micro}$  and $\alpha = 2 \micro \rho ^{\frac{1}{2}}$   and
$$
I_k(x)= \sum^{\infty}_{m=0} \frac{(\frac{x}{2})^{k+2m}}{(k+m)!m!}
$$
is the modified bessel function of the first kind of order k. 
### Birth death process with constant rates: steady state 
we are interested in $\pi_k = \lim_{t \rightarrow \infty}\pi_k(t)$ , CK equations for the general case are 
$k \geq 1$ 
$$
\frac{d \pi_k(t)}{dt}= -\pi_k(t)(\lambda_k+ \micro_k)+ \pi_{k-1}(t)\lambda_{k-1}+ \pi_{k+1}(t)\micro_{k+1}
$$

k = 0
$$
\frac{d \pi_0(t)}{dt}=-\pi_0(t)\lambda_0+ \pi_1(t)\micro_1
$$
in the long run variation nulloify, so $0=-(\lambda_k+\micro_k)\pi_k+\lambda_{k-1}\pi_{k-1}+\micro_{k+1}\pi_{k+1}$ and 
$0=-\lambda_0\pi_0+ \micro_1\pi_1$ with norm condition $\sum^{\infty}_{k=0}\pi_k=1$ 

set $\lambda_{-1}=\lambda_{-2}=...=0$ and $\micro_{-1}=\micro_{-2}=...=0$ and $\pi_{-1}=\pi_{-2}=...=0$  therefore we need only
$0=-(\lambda_k+\micro_k)\pi_k+\lambda_{k-1}\pi_{k-1}+\micro_{k+1}\pi_{k+1}$ and the norm condition 

for a set of states up to k $\frac{d(\sum^{k}_{h=0}\pi_h(t)}{dt}= -\pi_k(t)\lambda_k+\pi_{k+1}(t)\micro_{k+1}$ in equilibrium $\lambda_k \pi_k = \micro_{k+1} \pi_{k+1}$ 
yielding 
### Solution to birth death process
$$
\begin{align}
\pi_k=\frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\micro_1 \micro_2 ... \micro_k} \pi_0 

&& \pi_0=\frac{1}{1+\sum^{\infty}_{k=1} \prod^{k-1}_{j=0}\frac{\lambda_j}{\micro_j+1}}
\end{align}
$$
previous solution is a probability distribution if $\pi_0 > 0$  this implies that some limitations are necessary to birth and death rates: 
- let $S_1 = \frac{1}{\pi_0}=\sum^{\infty}_{k=0} = \sum^{\infty}_{k=0} \prod^{k-1}_{j=0} \frac{\lambda_j}{\micro_j+1}$ 
- $S_2 = \pi_0 \sum^{\infty}_{k=0}\frac{1}{\pi_k \lambda_k}= \sum^{\infty}_{k=0}\frac{1}{\frac{\pi_k}{\pi_0}\lambda_k}= \sum^{\infty}_{k=0}\frac{1}{\lambda_k \prod^{k-1}_{j=0}\frac{\lambda_j}{\micro_j+1}}$ 
$\pi_k \lambda_k$ represents the rate of population growth.

|all states are | if | that is|
|---|----|----|
|ERGOIC| $S_1 < \infty, S_2= \infty$ | $\forall k, \pi_k>0$ 
|NULL RECURRENT| $S_1= \infty, S_2=\infty$| $\pi_k \lambda_k \rightarrow 0$ 
|TRANSIENT| $S_1= \infty, S_2< \infty$| $\pi_k \lambda_k \nrightarrow 0$ 
Ergodicity is guaranteed if $\exists k_0<\infty$ such that $\frac{\lambda_k}{\micro_{k+1}}<1$ ,$\forall k > k_0$  that is $\micro_{k+1} \pi_{k+1} > \lambda_k \pi_k$.
#### Limit case 
$$
\frac{\lambda_k}{\micro_{k+1}} = 1
$$
constant $\lambda$ we obtain $S_1=\sum^{\infty}_{k=0}\prod^{k-1}_{\infty}1=\infty$ , $S_2=\sum^{\infty}_{k=0} \frac{1}{\lambda}$  (both $\infty$ so null recurrent states)

set $\lambda_k=\lambda k ^\alpha,k=0,1,2...$  for $\alpha=1,2,...$ we obtain  $S_1=\infty$ (as before) $S_2=\frac{1}{\lambda}\sum^{\infty}_{k=0}\frac{1}{k^\alpha}$ 

#### Special case 
$\lambda_k = \lambda$  k = 0,1,2,...  | $\micro_k = \micro$ k=1,2,3... such that $\rho= \frac{\lambda}{\micro}<1$ , equations become 

$$
\begin{align}
\pi_0 = \frac{1}{1+\sum^{\infty}_{k=1}\rho^k}= 1- \rho && \pi_k = \frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\micro_1 \micro_2 ... \micro_k} \pi_0 = \pi_0\rho^k
\end{align}
$$

with solution $$\pi_k = (1-\rho)\rho^k$$

