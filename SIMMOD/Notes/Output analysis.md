# Finite horizon simulations  
A finite-horizon discrete event simulation is one for which the simulated operational time is finite. they are also know as terminating simulations. Often the system state is assumed to be idle at the beginning and at the end of the simulation. The terminating condition can be specified by the close the door time.
- Transient system statistics are produced by this simulation.
- Initial conditions affect finite horizon statistics
- No need to assume a static environment 
## Terminating conditions FHS
depending on statistics chosen they can be expressed in term of simulation time or number of processed events. 

in the case of an SSQ we want to estimate: 
- the average number of customers in the system up to time T (1)
- the average waiting time experienced by the first N customers (2)

Formally 
1) state variable $n(\cdot)$ is known as stochastic process. typical objective estimate time-averaged transient statistic $\bar{n}(T)=\frac{1}{T} \int^{T}_{0}n(t) dt$ .
2) $W_i$ also is a stochastic process. typical objective estimate sample-averaged transient statistic $\bar{W}(N)= \frac{1}{N}\sum^{N}_{i=1}W_i$ 
## Indipendent repications
the samples collected in a set of replication are not independent (output are correlated), so is possible to calculate mean and variance but they are not independent, so is necessary a system to overcome this problem.

Thus the simulation can be repeated varying only the seed of the generator, the totality of the replication is an ensemble or sample, the seed must be chosen so that there is no overlapping between simulations, tipically the final state of the previous simulation is used as seed for the new one.
### Replication and interval estimation
suppose the simulation is replicated p times, each time generating a state time history $x_i(t)$ -> $\bar{x_i}(T)=\int^{T}_{0}x_i(t) dt$ where i is the replication index.

- Each data point $\bar{x}_i(T)$ is a indipendent observation of the RV $\bar{X}(T)$ 
- if p is large enough, pdf of $\bar{X}(T)$ can be estimated from histogram of $\bar{x}_i(T)$  

Specifically if we want $E[\bar{X}(T)]$ :
- a point estimate is available as a sample average $\hat{\micro}=\frac{1}{p}\sum^{p}_{i=1}\bar{x}_i(T)$ 
- an interval estimate for $E[\bar{X}(T)]$ can be calculated: Using the [[Interval estimation.canvas|Interval estimation]] technique. This requires sample mean and std deviation of $\bar{x}_i(T)$ , this can be used to estimate $\bar{n}(T)$ and $\bar{W}(N)$ 

let $n(T)$ be the number of customers in the system at time T, suppose we want $E[n(T)]$ 
- n(T) is a RV and the result of the simulation at time T is an instance of RV
- in general the distribution of n(T) is far from being an approx Normal 
- repeating the simulation several times produces data that are hard to analyze with standard confidence interval techniques.
- subdivide the sample of size p into p/K subsample is a good way to compute the average results (with proper confidence intervals) that can be used as a set of measure for other computations.

### Probability of lying in a fixed interval 

Assume a sample of p observation of an RV $Y_i \in Y,i=1...p$ coming from p independent observation, we want to estimate the probability that Y takes values within interval I
$\psi = Prob\{Y \in I\}$ , let X be an RV derived from Y $X_i= \begin{cases} 1 \ \ if \ Y_i \in i \\ 0\end{cases}$   then $E[X]=E[X_i]=\psi$ 

define m to be the number of sample components $Y_i$ that belong to I -> $m = \sum^{p}_{i=1}X_i$ 

The unbiased estimate of this prob is $\psi = \frac{1}{p}\sum^{p}_{i=1}X_i=\frac{m}{p}$ where $E[\psi]=\frac{1}{p}\sum^{p}_{i=1}E[X_i]=\psi$ 
and $VAR[\hat{\psi}]=\frac{\psi(1-\psi)}{p}$ 

m has binomial distribution with parameter $\psi$  --> $Prob\{m=k\}= \frac{p!}{k!(p-k)!} \psi^k(1-\psi)^{p-k}$ 
expected value and variance of this RV are then 
$E[m]=p \psi$  and $VAR[m]=p \psi(1-\psi)$ 

estimating $\psi$ is equal to estimating the parameter of a binomial distribution when $\psi$ is the probability of success $Prob\{\hat{\psi}_L \leq \psi \leq \hat{\psi}_U\}$  where $\hat{\psi}_L$ and $\hat{\psi}_U$ can be obtained from resolving the following 2 equations 

$\sum^{p}_{k=m}[\frac{p!}{k!(p-k)!} \psi_L^k(1-\psi_L^k)^{p-k}] = \frac{\alpha}{2}$  for $\psi_L$      
$\sum^{m-1}_{i=0}[\frac{p!}{k!(p-k)!} \psi_U^k(1-\psi_U^k)^{p-k}] = \frac{\alpha}{2}$  for $\psi_U$    

when  p is large and both m and p-m are > 5  a simpler way to get the confidence interval for $\psi$ is to use a normal distribution as an approximation of the binomial. So we can claim that $\hat{\psi}$ has a normal distribution with mean $\psi$ and variance $\frac{\psi(1-\psi)}{p}$  

so with the following auxiliary variable $Z=\frac{\hat{\psi} - \psi}{\sqrt{\psi(1-\psi}/p}$ , that has a standard normal distribution we can search $Pr(-z_{\alpha/2} \leq Z \leq z_{\alpha/2}) = 1-\alpha$  and then the desired confidence interval becomes 

$$
Pr\{\frac{m}{p}-z_{\alpha/2}\sqrt{\frac{m(p-m)}{p}} \leq \psi \leq Pr\{\frac{m}{p}+z_{\alpha/2}\sqrt{\frac{m(p-m)}{p}}\}= 1-\alpha
$$
### Waiting time of the K-th customer (jackknifing)
$W_k^{[i]} :i =1,2,...p$ = sample of measurement of waiting time of the k-th customer (only).

$\bar{W}_k=\frac{1}{p}\sum^{p}_{i=1}W_k^{[i]}$  ,     $\hat{s}^2_{W_k}=\frac{1}{p-1}\sum^{p}_{i=1}(W_k^{[i]} - \bar{W}_k)^2$ 
- we obtain confidence interval for $\micro = E[W_k]$  --> $Pr\{\bar{W}_k-t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_{W_k}}{\sqrt{p}} \leq \micro \leq \bar{W}_k+t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_{W_k}}{\sqrt{p}}\} \approx (1-\alpha)$ 
- we compute the point estimate of the variance 
$\hat{s}^2 = \frac{1}{p-1}\sum^{p}_{i=1}(W_k^{[i]}-\bar{W}_k)^2$     $E[\hat{s}^2]=\sigma^2$ 
- subdivide the original sample into p sub sample of size p-1 items $(W_k)_j$ 
$\bar{W_k}_j=\frac{1}{p-1}\sum^{p}_{i=1;i \neq j}W_k^{[i]}$        $\hat{s}^2=\frac{1}{p-2}\sum^{p}_{i=1;i \neq j}(W_k^{[i]})^2 - \frac{p-1}{p-2}\bar{(W_k)_j^2}$  

define $Z_j=p \hat{s}^2- (p-1)\hat{s}_j^2$  knowing $E[Z_j]=\sigma^2$ we can form a new sample of $Z_i$ 
$\bar{Z}=\frac{1}{p}Z_j$     $\hat{s}_Z^2=\frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$ 

we can then define $\Upsilon = \frac{(\bar{Z}-\sigma^2)}{s_Z/\sqrt{p}}$ , and show that is a RV distributed as a t-student with p-1 grade of freedom  and then obtain the confidence interval for $\sigma^2$ 
$$
Pr\{\bar{Z} - t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_Z}{\sqrt{p}} \leq \sigma^2 \leq \bar{Z} + t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_Z}{\sqrt{p}} \} \approx (1-\alpha)
$$

this method is know as jackknifing

# Infinite horizon simulations (steady state)
Steady state statistics are produced by this type of simulations, in this case the initial conditions doesn't affect the statistics produced (system loses memory of the initial state). Thus the system environment is assumed to remain static.


## Terminating conditions
depending on the statistics chosen, the terminating conditions may assume different aspects. In general state variables $X(t)$ and $Y_i$ of a system are known formally as stochastic process. 

Tipical objective are:
-  time-averaged steady state statistics: $\bar{x} = \lim_{T \rightarrow \infty} \frac{1}{T} \int^{T}_{0}X(t)dt$ 
- sample-averaged steady state statistics: $\bar{y}=\lim_{N \rightarrow \infty} \frac{1}{N} \sum^{N}_{i=0}Y_i$ 
both $\bar{x}$ and $\bar{y}$ are not random variables.

### The challenge
using $\{W_n:n =1,2,3,...\}$ suppose we are interested in estimating the waiting time distribution in steady state: $\lim_{n \rightarrow \infty} Prob\{W_n \leq x\} = F(x)$.
As in the case of transitory state we are interested in calculate expected value and variance of this value. 

In this case we don't need independent replications, because all RVs have all the same distribution. There are elements to take in consideration however:
- The observation of the RV must be made after a set of initial observations
- The observations made in a single simulation are in general highly correlated, and so many of the simple statistical method are ineffective since there is no independence

## The length of the initial transient period 
The initial condition must not:
- affect the steady state behaviour 
- require a very long initial simulation before getting a stable condition. 

The effect of those observation is that we must discard a long initial simulation.
The identification of the conditions is a difficult task that can only be addressed with preliminary simulations (pilot simulations).  The idea is to perform many simulation and collect statistics at different simulation times in order to construct samples that can be used to compute the probability distributions at these instant. So when compared they can be assumed as the steady state distribution of the process


### Comparing distributions 
- let $Y(t)$ be # of person in the system at time t and assume we made many observation $t_1,t_2,...,t_n$ --> $\{Y_i(t_n),i=1...p\} \ \ n=1,2,3...$ 
- let $m_k(t_n)$ be # of times $Y_i(t_n) = k$ --> $\{m_k(t_n),k=1...N_{max}\}$ 
- let $\psi_k(t_n)$ be P of observing k person in the system at time $t_n$ 
Thus we can compute $\{\psi_k(t_n)=\frac{m_k(t_n)}{p}\} \ \ k=1...N_{max}$ where at most $N_{max}$ customers have been observed in the system. 

The initial transient period is defined as the value of index n where the difference between $t_n$ and $t_{n+1}$ becomes smaller than a certain threshold 
$$
t_n:min_n\{\frac{\sum^{N_{max}}_{k=1}[\psi_k(t_n)-\psi_k(t_{n+1}]^2}{N_{max}} < \epsilon\}
$$


### Comparing moments 
comparing distribution need a big amount of data, a reasonable compromise is to compare moments instead of distributions. In this case we can compute 
$$
t_n^{[h]}:min_n\{|\frac{\sum^{p}_{i=1}[Y_i(t_n)]^h}{p} - \frac{\sum^{p}_{i=1}[Y_i(t_{n+1})]^h}{p}|<\epsilon\}
$$
Different moments yields different informations, so the actual length may be computed as $t_n:max_h\{t_n^{[h]}\}$ , the cost is high so reducing the compute cost to just the first moments is a good option. Averages computed at different times may oscillate, so we can compute moving averages :

let $\hat{\micro}(t_n)$ be the sample calculated at time $t_n$ --> $\hat{\micro(t_n)}= \frac{\sum^{p}_{i=1}Y_i(t_n)}{p}$ 
from these derived quantities we can compute moving averages over 2L+1 subsequent instants $\hat{\micro}^{[L]}(t_n)= \frac{\sum^{L}_{i=-L}\hat{\micro}(t_{n+i})}{2L+1}$ 

### Comparing auto correlation
we can identify the length of the initial period by measuring auto correlation: i.e measure the influence accross observations 

Consider a sequence of RVs $\{Y_1,Y_2,...,Y_n\}$ :
- Compute the auto covariance function $Cov(d)= \frac{1}{N-d}\sum^{N-d}_{i=1}(Y_i-E[Y])(Y_{i+d}-E[Y])$
- Since we don't know $E[Y]$ we can approximate using an experimental covariance $\phi(d)=\frac{1}{N-d-1}\sum^{N-d}_{i=1}(Y_i-\bar{Y})(Y_{i+d}-\bar{Y})$  
with the experimental mean $\bar{Y}$ expressed as always.

$\phi(0)$ is the usual variance $\hat{s}^2$, we can thus compute the experimental auto-correlation 
$\rho(d)=\frac{\phi(d)}{\hat{s}^2}$  that is a normalized auto covariance with interval values (-1,1), values next to 0 mean that influence accross measures are negligible. Thus we can search for this value to state where is the end of the initial transient period $d_0=min_d\{|\rho(d)| \leq \epsilon \}$ 


## Overcome statistical dependency amongst observation 

if we have a set of indipendent variables $Y_n$ and we want to estimate the characteristics, we can consider this set as a set of instance of the same RV but highly correlated, thus we need a method to reduce the dependency amongst those instances:

- independent replications 
- Batch means
- Regeneration points 


## independent replications
the components of the sample are obtained by running the simulations many times with different random generator seeds, with identical initial conditions, disregarding the data obtained by the initial simulation run

### Mean and variance (indipendent replications)
Determined $n_0$ we run p independent simulations and obtain a sequence of variable of interests 
$\{ Y_{j1},Y_{j2},...,Y_{jn_0},...,Y_{jk},...,Y_{jN}:j=1...p \}$   from each of this realization we construct measures that become the components of our sample. 

As for the finite horizon analysis we can easily compute interval estimates. Starting from the mean: $\bar{Y}_j = \frac{1}{N-n_0}\sum^{N}_{k=n_0+1}Y_{jk}$, the data can be then organized in this manner 
$$
\begin{aligned}
\{ Y_{11},Y_{12},...,Y_{1n_0},...,Y_{1k},...,Y_{1N}\} \Rightarrow \bar{Y}_1
\\
\{ Y_{21},Y_{22},...,Y_{2n_0},...,Y_{2k},...,Y_{2N}\} \Rightarrow \bar{Y}_2
\\
\{ Y_{p1},Y_{p2},...,Y_{pn_0},...,Y_{pk},...,Y_{pN}\} \Rightarrow \bar{Y}_p
\end{aligned}
$$
out of these values we compute 
the unbiased sample mean $\hat{\micro}=\bar{Y} =\frac{1}{p}\sum^{p}_{j=1}\bar{Y}_j$ and variance  $\hat{s}^2 = \frac{1}{p-1}\sum^{p}_{j=1}(\bar{Y_j} - \bar{Y})^2$ 
when $N-n_0$ is large those RVs can be assumed to have a normal distribution and so the confidence interval is $Pr\{\bar{Y} - t_{p-1,\alpha/2}\sqrt{\hat{s}^2/p} \leq \micro \leq \bar{Y} + t_{p-1,\alpha/2}\sqrt{\hat{s}^2/p}\} \approx 1- \alpha$  
As usual is possible to control the size of the confidence interval by controlling the number of replications P and the number of observations N that has important effects on $\hat{s}^2$ 

When p>40 the t-student is approximate as a Normal so that $t_{p-1,\alpha/2}$ can be replaced with $z_{\alpha/2}$ 

### Probability of falling within an interval 
estimate as the other case $\psi_n=Pr\{Y^{[n]} \in I\}$ , where $Y^{[n]}$ is the observation of interest during a simulation of length n. we can assume that $\psi = \lim_{n \rightarrow \infty} \psi_n$ . After having determined $n_0$ we can assume the process to be stationary and so $\psi_n \approx \psi$ . 

Given $n_0$ we perform p runs that will provide an interval estimate for $\psi$  and yield a set $\{Y_{ij} :i=1..p;j=1...N\}$  assuming $N>>n_0$ . From each simulation we compute the unbiased estimate of the desired prob $\hat{\psi}_i=\frac{v_i}{N-n_0}$ . where $v_i$ is # of times Y fells in I. Thus $\hat{\psi}_i$ values obtained are independent --> $E[\hat{\psi}_i]=\psi$ 

We can compute then the sample mean and variance:
$\hat{\psi}= \frac{1}{p}\sum^{p}_{i=1}\hat{\psi}_i$   ,    $\hat{s}^2(\hat{\psi})=\frac{1}{p-1}(\hat{\psi}_i - \hat{\psi})^2$ . Let's define $Z = \frac{\hat{\psi}-\psi}{\sqrt{\hat{s}^2(\hat{\psi})/p}}$ that has a t-student(p-1). 
An interval estimate is expressed as $Pr\{\hat{\psi}-t_{p-1,\alpha/2}\frac{s(\hat{\psi})}{\sqrt{p}} \leq \psi \leq \hat{\psi}+t_{p-1,\alpha/2}\frac{s(\hat{\psi})}{\sqrt{p}}\}$ where as usual if p is large we can replace $t_{p-1,\alpha/2}$ with $z_{\alpha/2}$ .

## Batch means
the components of sample are collected by a single simulation run after having discarded the data obtained by the transient period and subdividing the data collected into subsamples which are assumed to be approximately independent because of the inter collection time long. 

### Discard the transient period
in order to identify the transient period, the auto covariance technique is recommended. Let $Y_{i,j}$ be the j-th observation belonging to the i-th sequence. Let's generate 2 subsequences $\{Y_{i,j}:j=1...m\}$ and $\{Y_{i+1,j}:j=1...m\}$ with $m>n_0$ , since this precondition those 2 subsequences are independent, repeating this consideration for the pair $\{Y_{i+1,j};Y_{i,j}\}$ j=2...m we can consider the whole sample made of independent observations. Thus we can apply the techniques used for the independent replication here as well

### Mean and variance (Batch means)
we can compute sample and mean with this formula 
$$
\bar{Y}_j=\frac{1}{N-n_0}\sum^{n_0+(j+1)*m}_{k=n_0+j*m+1}Y_{jk}
$$
the data can organized in this way
$$
\begin{aligned}
\{ Y_{11},Y_{12},...,Y_{1n_0},...,Y_{1k},...,Y_{1N}\} \Rightarrow \bar{Y}_1
\\
\{ Y_{21},Y_{22},...,Y_{2n_0},...,Y_{2k},...,Y_{2N}\} \Rightarrow \bar{Y}_2
\\
\{ Y_{p1},Y_{p2},...,Y_{pn_0},...,Y_{pk},...,Y_{pN}\} \Rightarrow \bar{Y}_p
\end{aligned}
$$
and then apply the techniques used before

## Regenerative method
the components of the sample are obtained by a single simulation run splitted into regenerative cycles. Defined as regeneration points where the simulated stochastic process naturally loses the memory of the past.

### Initial conditions
- The component of the sample are derived from successive regeneration cycles
- Regenerations cycles are random length subsequences identified within the simulation run, starting the simulation from one of these regeneration points it's possible to avoid wasting the initial part of the simulation. 
- RVs in different sequences are independent and equally distributed 
- If the sequence is regenerative and certain weak conditions hold the sequence has a steady state.
![[Pasted image 20231118103525 1.png]]
from this queue we can take the following subsequences $\{W_1,W_2,W_3,W_4,W_5,W_6,W_5\}$ , $\{W_8,W_9\}$ , $\{W_{10},W_{11},W_{12},W_{13}\}$  characterized by the fact that the first element (sequence) is always the waiting time of a customer that arrives and find the queue empty. These subsequences are called regeneration cycles. The data can be organized as p subsequences expressed in this form
$$
\begin{aligned}
\{ W_{11},W_{12},...,W_{1k},...,W_{1m_1}\} 
\\
\{ W_{21},W_{22},...,W_{2k},...,W_{2m_2}\}
\\
\{ W_{p1},W_{p2},...,W_{pk},...,W_{pm_p}\}
\end{aligned}
$$

### Initial considerations
Let $A_j=\sum^{m_j}_{k=1}W_{jk}$ be the sum of the waiting times observed during the j-th regeneration cycle. Where $m_j$ is the number of customers served in the j-th cycle and can be used as a measure of length of the cycle. Thus from each regeneration cycle we get $\bar{W}_j=\frac{1}{m_j}\sum^{m_j}_{k=1}W_{jk}=\frac{A_j}{m_j}$ that is the ratio between 2 correlated variables. 

In a generic form $A_j= \int^{\beta_j}_{\beta_{j-1}}n(t)dt$ can be expressed as integral of n(t) computed in the j-th regeneration cycle. Denoting with $\delta_j=\beta_j-\beta_{j-1}$ the length of the cycle we get a point estimate $\bar{n}_j=\frac{1}{\delta_j}\int^{\beta_j}_{\beta_{j-1}}n(t)dt=\frac{A_j}{\delta_j}$ .
Running the simulation up to the point of observing p regeneration cycles we collect samples that cannot be used in a standard way because of their correlation. Such that the distribution of $\bar{W}_i$ is different from $\bar{W}$. It is thus mandatory taking into account the correlated nature of the measures coming from different regeneration cycles. 

Given a random variable $Y$ that we measure we can summarize the outcomes with a series of independent and identically distributed random pairs $\{(A_1,v_1),...,(A_p,v_p)\}$ : where 
- $A_j$ is the sum or integral computed over the j-th regeneration cycle 
- $v_j$ is the length of the j-th regeneration cycle expressed as the number of occurrences of $Y$ or as the distance in time between its end points. 


### Point estimate 
under some conditions is possible to show $E[\hat{r}] = r = \frac{E[A_1]}{E[v_1]}=\frac{E[A_j]}{E[v_j]}$ so that $\hat{r}$ is the estimate point of interest. 
Let $Z_j=A_j-rv_j$  for which $E[Z_j]=0$  and $VAR[Z_j]=VAR[A_j]-2rCOV[A_j,v_j]+r^2VAR[v_j]$  , the covariance is present due to the mutual dependence between elements of our ratio. 
We can define $\bar{Z} = \frac{1}{p}\sum^{p}_{j=1}Z_j=\bar{A}-r \bar{v}$  so that $E[\bar{Z}]=0$ and $VAR[\bar{Z}]=\frac{VAR[Z_j]}{p}=\frac{\sigma^2_Z}{p}$.
The central limit theorem allows to state $\frac{\bar{Z}}{\sigma_z/\sqrt{p}}=\frac{\bar{A}-r \bar{v}}{\sigma_Z/\sqrt{p}}= \frac{\bar{A}/\bar{v}-r}{\sigma_Z/(\bar{v}\sqrt{p})}=\frac{\hat{r}-r}{\sigma_Z/(\bar{v}\sqrt{p})}$  has a std normal distribution. So we can compute $Pr\{\hat{r}-z_{\alpha/2}\frac{\sigma_Z}{\bar{v}\sqrt{p}} \leq r \leq \hat{r}+z_{\alpha/2}\frac{\sigma_Z}{\bar{v}\sqrt{p}}\} \approx 1-\alpha$ but $\sigma^2_Z$ is unknown so we must use sample variance 
$\sigma^2_Z \approx \hat{s}^2_Z=\hat{s}^2_A-2\hat{r}\hat{s}_{Av}+\hat{r}^2\hat{s}^2_v$ so that the solution has not std normal but a t-student distribution and then the confidence interval becomes 
$$
Pr\{\hat{r}-t_{1,\alpha/2}\frac{\hat{s}_Z}{\bar{v}\sqrt{p}} \leq r \leq \hat{r}+t_{1,\alpha/2}\frac{\hat{s}_Z}{\bar{v}\sqrt{p}} \} \approx 1-\alpha
$$
 
 ### Width of confidence interval 
to compute the previous conf interval, we must estimate the variance of $Z_j$ 
- $VAR[A_j] \approx \hat{s}^2_A=\frac{1}{p-1}\sum^{p}_{j=1}(A_j-\bar{A})^2=\frac{1}{p-1}[\sum^{p}_{j=1}A^2_j-p \bar{A}^2]=\frac{1}{p-1}\{\hat{S}_{AA}-p \bar{A}^2\}$  
- $COV[A_j,v_j] \approx \hat{s}_{av}=\frac{1}{p-1}\sum^{p}_{j=1}(A_j-\bar{A})(v_j-\bar{v})=\frac{1}{p-1}[\sum^{p}_{j=1}A_jv_j-p \bar{A}\bar{v}] = \frac{1}{p-1}\{\hat{S}_{Av} - p \bar{A}\bar{v}\}$   
- $VAR[v_j] \approx \hat{s}^2_v = \frac{1}{p-1}\sum^{p}_{j=1}(v_j-\bar{v})^2=\frac{1}{p-1}[\sum^{p}_{j=1}v^2_j-p \bar{v}^2]=\frac{1}{p-1}\{\hat{S}_{vv}-p \bar{v}^2\}$   
where
$\hat{S}_A= \sum^{p}_{j=1}A_j$ , $\hat{S}_{AA} = \sum^{p}_{j=1}A^2_j$ , $\hat{S}_{Av}=\sum^{p}_{j=1}A_jv_j$ ,$\hat{S}_v= \sum^{p}_{j=1}v_j$ , $\hat{S}_{vv} = \sum^{p}_{j=1}v^2_j$, $\hat{r}=\frac{\hat{S}_A}{\hat{S}_v}$ 
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1^*\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p^*\} \Rightarrow Y_{2p}
\end{align}
recalling $\sigma^2_Z \approx \hat{s}^2_Z=\hat{s}^2_A-2\hat{r}\hat{s}_{Av}+\hat{r}^2\hat{s}^2_v$ we can write $\hat{s}^2_Z=\frac{1}{p-1}\{\hat{S}_{AA}-2\hat{r}\hat{S}_{Av}+\hat{r}^2\hat{S}_{vv}\}$  so that the width can be 
$$
\Delta= \frac{\hat{s}_Z}{\bar{v}\sqrt{p}}=\sqrt{\frac{p}{p-1}}\frac{\sqrt{\hat{S_{AA}-2\hat{r}\hat{S}_{Av}+\hat{r}^2+\hat{S}_{vv}}}}{\hat{S}_v}
$$
despite the complexity of computing this confidence interval 
$Pr\{\hat{r}-t_{1,\alpha/2}\Delta \leq r \leq \hat{r}+t_{1,\alpha/2}\Delta \} \approx 1-\alpha$ the values needed $A_j,A^2_j,v_j,v^2_j,A_jv_j$ can be accumulated at the end of each regeneration cycle. 

### Interval estimation of simulated random variables 
the regenerative method is well suited for interval estimation of functions of simulated RVs, the unique requirement is to define well the expression of $A_j$ . For example 
- average queue length $A_j=\int^{\beta_j}_{\beta_{j-1}}N(t)dt$  $v_j=\beta_j-\beta_{j-1}$ 
- second moment of queue length $A_j=\int^{\beta_j}_{\beta_{j-1}}N(t)^2dt$  $v_j=\beta_j-\beta_{j-1}$ 
- mean waiting time $A_j=\int^{\beta_j}_{\beta_{j-1}}N(t)dt$  $v_j=C_j$
- probability of finding k customers in queue $A_j=\int^{\beta_j}_{\beta_{j-1}}I_k(t)dt$   $v_j=\beta_j-\beta_{j-1}$ Ik is # of times N(t)=k
- Average cost of waiting $A_j=\int^{\beta_j}_{\beta_{j-1}}R(N(t)) dt$        $v_j=\beta_j-\beta_{j-1}$ where R(k) is cost rate due to the presence of k customers in system 

## Finding regeneration points
a regeneration point correspond to a state reached by the system when the future evolution can be considered as a replica of the previous one. When the system gets to such a point we can answer question on its future behavior without the need of information on its past, thus a regeneration point is defined by the occurrence of a particular event in a defined state. 

### Finding regeneration points in FCFS single server system
Deciding if the system is entered a regenerative conditions correspond to answer to:
**"what is probability that the system leaves the current state in less then $\Delta$ time units"?**
without the needs of having information on the past of the system. Depending on the distribution of service time and inter arrival different consideration can be made:
- G/G/1 queue: general distribution for both inter arrival and service time 
- M/G/1: inter arrival with neg exp and service time with general 
- G/M/1: inter arrival with general and service time with neg exp
- M/M/1: both inter arrival and service time with neg exp distribution
lets define the following variables 
- let $\tau$ and $\sigma$ be inter arrival and service time. 
- $\rho$ and $v$ remaining service time and required time for next arrival 
## Negative exponential distribution 
let X be a RV with neg exp distribution with parameter $\micro=\frac{1}{\lambda}$
$$
\begin{align}
f_X(x)=\lambda e^{-\lambda x} && F_X(x)=1-e^{-\lambda x}\\
E[X] = \micro=\frac{1}{\lambda} && VAR[X]=\micro^2=\frac{1}{\lambda^2} && CV^2[X]=\frac{VAR[X]}{(E[X])^2}=1
\end{align}
$$
### Minimum among Neg Exp RVs
Given 2 RVs with neg exp distribution 
$$
\begin{align}
f_X(x)=\lambda e^{\lambda-x}\  \ \ (x \geq 0)  && f_Y(y)=\delta e^{\delta y} \ \ \ (y \geq0)
\end{align}
$$
Define new RV $Z=min(X,Y)$ :
- Z is neg exp with parameter $\lambda+\delta$ 
- $F_Z(z)=1-e^{\lambda z} e^{-\delta z}= 1- e^{-(\lambda+\delta)z}$ 

### Memory less property 
let r(t) be the distribution of the remaining portion of X $r(t)=Pr\{X >s+t|X>s\}$ 
using conditional probability we can show  $r(t)=\frac{Pr\{X>s+t\}}{Pr\{X>s\}}$ Since X has a negative distribution we have :
$r(t)=\frac{e^{-\lambda(s+t)}}{e^{-\lambda(s)}}=e^{-\lambda(t)}$ which says that the distribution of the remaining part of X is identical to that of X.

The memory less property can be formally expressed as 
$$
Pr\{X> x+\alpha|X>\alpha\}=Pr\{X>x\}
$$


### G/G/1 case 
no negative exponential, The only regeneration point is the arrival of a customer that finds the server idle. 
- if t be the time of arrival to an empty system --> the answer is $Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\}$  
- if t is arrival of a new customer while another is already in service, let $\rho$ be the remaining service time -->  $Pr\{[\delta=min(\tau,\rho)]\leq \Delta\}$   
- if t is time of departure of a customer let $v$ be the time required for the next arrival to happen --> $Pr\{[\delta=min(v,\sigma)]\leq \Delta\}$   

### M/G/1 case 
arrival process is Poisson and inter-arrival times have neg exp distribution , thus departure times are regeneration points because their occurrence requires the characterization of the remaining time
$$
Pr\{[\delta'=min(v,\sigma)]\leq \Delta\} = Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\}
$$
The same doesn't apply if we choose the time of the arrival of a customer that find the server busy 
$$
Pr\{[\delta* =min(\tau,\rho)]\leq \Delta\} \neq Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\} 
$$

### G/M/1 case 
dual to M/G/1 case:  any arrival time identifies a regeneration point because $\rho$ has the same distribution of $\sigma$ 
$$
Pr\{[\delta*=min(\tau,\rho)]\leq \Delta\} = Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\}
$$
### M/M/1 case 
when both $\tau$ and $\sigma$ have neg exp distribution their memory less property ensure that any arrival or departure times are regeneration points
$$
Pr\{[\delta'=min(v,\sigma)]\leq \Delta\} = Pr\{[\delta*=min(\tau,\rho)]\leq \Delta\}= Pr\{[\delta'=min(\tau,\sigma)]\leq \Delta\}
$$

## Finding regeneration points in a network of queue
the discussion for FCFS easily extends to the case of more complex models. basic criteria remains interrupt the evolution of the model only in situations where there are no activities characterized by a general probability distribution. To make discussion simple let's use a queue with just 2 station in tandem with a fixed number N of customers , summarizing the criteria in the following table

|Service time distribution of first queue| Service time distribution of second queue| Criteria for regeneration point |
|----|----|-----------|
|General|General|Any departure that leaves behin exactly n-1 customers from one of the two servers of the network|
|markov(neg-exp)|General| any departure from the second server
|General|markov| any departure from the first server
|markov|markov|any departure in the system

## Identify regeneration cycles  
when the model admits many regeneration points, one of them must be chosen as a reference and regeneration cycles begin and end when this point is reached. 

for example if in a M/M/1 queue if we decide that a regeneration cycle start start when a departures leaves m customers we cannot end it if it leaves m+k customers. This is because the statistics collected must be identical and independent instances of the same RV.  identify regeneration cycles in a network is more difficult because we lose the memory less property.

### Identify regeneration cycles  with passage times
consider the case of a sub system identified in a system. Assume a single entry point for this sub system, **we are interested in measuring the average time spent by customers in the sub system**. Candidate regeneration points are the arrival or a departure from the entry point of the sub system (because of memory less). If there exists stations outside the sub system with general time distributions they must be empty when the two previous events are considered. 

### Identify regeneration cycles  with tagged customer
All customers are statistically identical. This approach arbitrarily selects one customer in the system and follows its way through the system, recording: the time it enters $t_{en}$  and it exit $t_{ex}$ . The difference $\tau=t_{ex}-t_{en}$ is a measure of the passage time.

Let $\tau_j^{[i]}$ be the j-th passage time of the tagged customer.
Let $A^{[i]}=\sum^{k^{[i]}}_{j=1}\tau_j^{[i]}$ be the sum of the $k^{[i]}$ passage times. 

The pair $(A^{[i]},k^{[i]})$ becomes the component of a sample of independent observation that can provide estimates with the regenerative method. 

### Grouping regeneration cycles
When there are many regeneration points it can happen that the chosen ones yield regeneration cycles that are too short. In this case we cannot rely on the central limit theorem stating that the distribution are "quasi-normal", if possible we must choose a new regeneration point that avoid this problem. 

If not is possible to aggregate several regeneration cycles, the unique constraint is that the grouping criteria is always applied during the simulation run. Without conditioning its application on the specific characteristics of the regeneration cycles that need to be aggregated.

## Improve results 
The precision of the simulation rise proportionally to the size of p, an alternative to that is working on the sample variance to make it smaller. 2 interesting cases exists:
- Antithetic variates to make the sample components pairwise negatively correlated 
- Comparing alternative results by positively correlating the corresponding components of the samples obtained for the two alternatives 

### Antithetic variates 
Assume we want to estimate the expected value of an RV Y --> $Y(\micro=E[Y])$ , suppose we run a simulation and produce a sample of 2p observations $\{Y_1...Y_p,Y_{p+1}...Y_{2p}\}$. In normal conditions we would retrieve $\hat{\micro}=\bar{Y}=\frac{1}{2p}\sum^{2p}_{i=1}Y_i$  and $VAR[\bar{Y}]=\frac{\sigma^2}{2p}$  knowing $E[\bar{Y}]=\micro$. 

Suppose to divide the sample in 2 sub samples of size p $\{Y_1...Y_p,Y_{p+1}...Y_{2p}\}= \{Y_{11}...Y_{1p}\},\{Y_{21}...Y_{2p}\}$ .
Let $Z_i=\frac{Y_{1i}+Y_{2i}}{2}$  that we use to obtain $\bar{Z}=\frac{1}{p}\sum^{p}_{i=1}Z_i=\bar{Y}$. The expected value and variance of $\bar{Z}$ are:
- $E[\bar{Z}]=\frac{E[Y_1]+E[Y_2]}{2}=\micro$ 
- $VAR[\bar{Z}]=\frac{1}{p}VAR[\frac{Y_1+Y_2}{2}]= \frac{\sigma^2}{2p}+\frac{COV[Y_1,Y_2]}{2p}$  
If 2p of the original sample are independent then also those 2 sub samples are, thus $COV[Y_1,Y_2]=0$ and know that the introduction of the new variable doesn't perturb the experiment $VAR[\bar{Z}]=VAR[\bar{Y}]=\frac{\sigma^2}{2p}$ . 

If they are correlated the division yield different results, if the variables $Y_1$ and $Y_2$ are negatively correlated the variance of $\bar{Z}$ decrease and we obtain $VAR[\bar{Z}] \leq VAR[\bar{Y}]$ . To induce this correlation is sufficient store the seeds used for the first p observations and use them to obtain the observations for the second sub sample. The unique constraint is using Antithetic sequence of random numbers. 

2 sequences of RN  $\{U_i \in (0,1);i=1...m\}$  and $\{U^*_i \in (0,1);i=1...m\}$  are Antithetic if $U_i^*=(1-U_i)$.
Let $\{X_{01},X_{02},...,X_{0p}\}$ be the set of seeds used to produce the first p components of the sample ,then results are stored in this way:
$$
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1^*\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p^*\} \Rightarrow Y_{2p}
\end{align}
$$
The observation produced here are then Antithetic and the size of the confidence interval becomes smaller (because of COV is negative) as equal cost. 

### Alternative comparison
if we must compare 2 systems with different management policies, is possible to reduce the variance. If we want to obtain estimates of a measure computed for the 2 alternatives to decide which is the best we can: simulate the 2 alternatives separately and produce $\{Y_{11}...Y_{1p}\},\{Y_{21}...Y_{2p}\}$  , then compute $\bar{Y_1};\bar{Y_2}$ and then make a decision. 

Let $Z_i=(Y_{1i}-Y_{2i})$ , the sample $\{Z_1...Z_p\}$ can be used to obtain:
- Point estimate (sample average) $\bar{Z} = \frac{1}{p}\sum^{p}_{i=1}Z_i=\bar{Y}_1-\bar{Y}_2$ 
- Sample variance $\hat{s}_Z^2=\frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$ 

Let $\micro_1$ and $\sigma_1^2$ be expected value and variance for $Y_1$ ,same $\micro_2;\sigma_2^2$ for $Y_2$ . The comparison would be made on the basis of $E[\bar{Z}]=E[\bar{Y}_1]-E[\bar{Y}_2]=\micro_1-\micro_2$ and of $VAR[\bar{Z}]=VAR[\bar{Y}_1] + VAR[\bar{Y}_2] - 2COV[\bar{Y}_1,\bar{Y}_2]= \frac{\sigma_1^2+\sigma_2^2}{p} -2 COV[\bar{Y}_1,\bar{Y}_2]$ 


The individual $Z_i$ and $\bar{Z}$ as well may assume positive or negative values (and also the extremes of confidence interval). If both are positive or negative the decision is easier. 

If the simulations for the 2 alternatives are performed in an independent manner $COV[\bar{Y}_1,\bar{Y}_2]=0$ so that 
$VAR[\bar{Z}]=VAR[\bar{Y}_1-\bar{Y}_2]= \frac{\sigma^2_1+\sigma^2_2}{p}$ also the decision is easy. 

if instead the different replications of the 2 experiments are performed with the following scheme:
$$
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{2p}
\end{align}
$$
where X are the seeds. $\bar{Y}_1$ and $\bar{Y}_2$ are positively correlated so that $VAR[\bar{Z}]=VAR[\bar{Y}_1-\bar{Y}_2] < \frac{\sigma_1^2+\sigma_2^2}{p}$ 
then the estimate is more precise with the same computational cost. 

### Result precision 
Interval estimates allow to get confidence in the robustness of the computed results with respect to possible variation, part of the problem however is the precision we want to reach with our estimate. 

Let $\epsilon$ be the required precision and $\Delta= \frac{\hat{s}_Z}{\bar{v}\sqrt{p}}$ the semi width of the confidence interval. Knowing that $\Delta$ depend on the sample size and sample standard deviation we can work on this values to get a better precision, expressed as 
$$
\frac{\Delta}{\bar{Y}} \leq \epsilon
$$
It is better to use a sequential stopping rule to check if the desired precision is reached

## Tuning 
tuning consist of: assessing the adequacy of the distributions assumed as part of the specification models, estimating parameters, testing the quality of the variate generators, checking that variations of the parameters produce coherent variations of the results. 

## Validation
check whether the simulator provides reliable estimates : comparing the simulation output with measures from the real system and with the theoretical values obtained with independent mathematical methods.

It is also important to use simplified version of the required simulator in order to check it's components. Different version should be considered to make sure that various aspects of the original simulator are checked. 

A first way of checking whether the simulator provides reliable estimates is comparing confidence interval (low,up) with a theoretical value $\micro$ to see if it's covered by the interval. 

A more reliable way is implementing the definition of confidence level $1-\alpha$ which says that:
_if the experiment is repeated n times, the theoretical value $\micro$ should be covered by the interval estimates approximate $n(1-\alpha)$ times, while (approx) for $n \alpha$ times the confidence interval should not cover the theoretical value._  In practice we may proceed that way:
- Each experiment consist of repeating the simulation run with different seeds
- From each experiment compute the point estimate $\hat{\micro}$ and the confidence interval $(\hat{\micro}-\Delta,\hat{\micro}+\Delta)$  of the true parameter $\micro$ 
- Given those hypothesis: (approx) 50% of the experiments should provide a point estimate $\hat{\micro}$ that is larger than the theoretical value, while others should be smaller. 
- (approx) $(1-\alpha )\%$  of the experiments should provide intervals that include the theoretical value $\micro$ while $\alpha\%$ should not provide intervals which include $\micro$ 