## Sample mean and standard statistics
- Media campionaria: $\bar{X} = \frac{1}{p} \sum^{i=1}_{p}x_i$
- Varianza Campionaria: $\hat{s}^2 =\frac{1}{p-1}\sum^{i=1}_{p}(x_i-\bar{X})^2$    
- Sample standard deviation: $\hat{s} = \sqrt{\hat{s}^2}$
- Coefficient of variation: $\frac{\hat{s}}{\bar{X}}$ 

mean: measure of central tendency
variance , deviation: measure of dispersion about the mean
## Bias of an estimator
the bias (of a parameter) is the difference between the expected value of the estimator and the real value of the parameter.

a good estimator $\hat{\psi}$  of a parameter $\psi$  if:
- the distribution of $\hat{\psi}$ is centered over $\psi$ 
- the distribution of $\hat{\psi}$ is narrow enough so that $|\hat{\psi} - \psi|$  falls in the precision limits
- information and distribution of $\hat{\psi}$ can be obtained from sample values and specifically from the sample size.

## Unbiased sample mean
consider a sample of indipendent observation with p sample of a random variable X, with mean $\micro$ and variance $\sigma^2$, the expected value $E[X]=\micro$ , while $\hat{\micro}= \bar{X}$.
from the definition of $\hat{u}$  we can observe that $\bar{X}$ is an unbiased estimator for $\micro$ 
and plugging $VAR[\hat{u}] = E[(\hat{u}-E[\hat{u})^2]$ obtaining $VAR = \frac{\sigma^2}{p}$ we can conclude that $\bar{X}$ is a good estimator of $\micro$ 
## Unbiased sample variance 
similar to sample mean  define $\hat{s}^2=\frac{1}{K}\sum^{i=1}_{p}(x_i-\hat{\micro})^2$ , we want to show when $E[\hat{s}^2]=\sigma^2$ hold for which value of K. With some passages we can say that if we choose a value of K=(p-1) we can easily derive $E[\hat{s}^2] =  \frac{(p-1)p}{pK}* \sigma^2= \sigma^2$. We can then conclude that $s^2$ is an unbiased estimator of $\sigma^2$ , computed with $\frac{1}{p-1} \sum^{i=1}_{p}(x_i-\bar{X})^2$ 

## Variance of sample variance
let $X_j$ be the sub sample of the observations without the j-th one.  Compute:
- Sample mean: $\bar{X}_j = \frac{1}{p-1} \sum^{p}_{i=1;i \neq j}x_i$ 
- Sample variance: $s^2_j = \frac{1}{p-2} \sum^{p}_{i=1;i \neq j}(x_i-\bar{X}_j)^2 = \frac{1}{p-2} \sum^{p}_{i=1;i \neq j} x_i^2 \frac{p-1}{p-2}\bar{X}_j^2$.

It's easy to show that : $\bar{X} = \frac{1}{p} \sum^{p}_{j=1}\bar{X}_j$ , not the same could be said for 
$\hat{s}^2=\frac{1}{p}\sum^{p}_{j=1}\hat{s}_j^2$ 

Now we can use those results to get information about the distribution of the sample variance as a function of the sample size.
define the following auxiliary variable: $Z_j=p \hat{s}^2 - (p-1)\hat{s}^2$  we know by definition that $E[\hat{s}^2] = E[s_j^2]= E[\sigma^2]$ and so $E[Z_j]=\sigma^2$ . Consider a sample composed by those variables, then 
$\bar{Z}=\frac{1}{p} \sum^{p}_{j=1}Z_j$  and $\hat{s}^2= \frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$. It can be shown that $\Upsilon = \frac{(\bar{Z}-\sigma^2)}{\sqrt{\hat{s}^2_Z/p}}$  is distributed as a t-student with p grade of freedom (a distribution with expected value to be equal to 0 and variance that decreases as the grade of freedom increases). We can then conclude that $\bar{Z}$ is a good estimator for $\sigma^2$ and $\hat{s}^2$ as well.   
## Chebichev inequality
Chebyshev’s inequality relates to the number of points that lie within k standard deviation of the mean. 
A) Points farthest from the mean contribute most to s and $\hat{s}^2$  

B) define the set $S_k=\{x_i|\bar{X}-k \hat{s} < x_i < \bar{X} + k \hat{s}\}$ from the sample variance definition we have 

$$
(p-1) \hat{s}^2= \sum_{x_i \in S_k}(x_i - \bar{X})^2 + \sum_{x_i \in \bar{S}_k} (x_i - \bar{X})^2
$$
Where $\bar{S}_k$ is the complement of $S_k$ , ignoring the contribution to $\hat{s}^2$ from all the points close to mean we get $(p-1)\hat{s}^2 \geq \sum_{x_i \in \bar{S}_k}(x_i-\bar{X})^2 \geq \sum_{x_i \in \bar{S}_k}(k \bar{s})^2 = |\bar{S}_k|(k \hat{s})^2$. using $q_k=|S_k|/p$ ad the proportion of $x_i$ within $\underline{+} k \hat{s}$ of $\bar{X}$  and removing $\hat{s}^2$ we get chebichev inequality
$$
q_k \geq 1- \frac{(p-1)/p}{k^2} \geq 1 - \frac{1}{k^2}
$$
- For any sample at least 75% of the points lie within $\underline{+}2 \hat{s}^2$ of $\bar{X}$ 
- For k=2 is very conservative (tipically the 95% lie in $\underline{+}2 \hat{s}^2$ of $\bar{X}$) 
- $\bar{X} \underline{+}2 \hat{s}^2$  defines the effective width of a sample (and so is 4s) , most but not all points lie in this interval (except outliers) 
## Time averaged statistics
x(t) is the sample path of a stochastic process ($0<t< \tau$) 
- Sample path mean $\bar{X} = \frac{1}{\tau} \int^{\tau}_{0}x(t) dt$ 
- Sample path variance $s^2=\frac{1}{\tau} \int^{\tau}_{0}(x(t)- \bar{X})^2 dt$ 
- Sample path std deviation $s=\sqrt{s^2}$
- One pass equation for variance $s^2=(\frac{1}{\tau} \int^{\tau}_{0}x^2(t)dt) - \bar{X}^2$ 


in discrete event simulation sample path is piecewise, and so integrals reduce to summations.
## Preliminary result

if $X_1,X_2,...,X_p$ is an iid sequence of Normal Random Variables with common $\micro$ and $\sigma$ and $\bar{X}$ is the mean of the sequence, then $\bar{X}$ is a $Normal(\micro,\sigma,\sqrt{p})$ Random Variable independently of the value of p.

## Random interval 
define $Z = \frac{\bar{X} - \micro}{\sigma/\sqrt{p}}$ , Z has a standard normal distribution with $\micro$ = 0 and $\sigma$ = 1.
given a parameter $\alpha \in (0.0,1.0)$ exists a positive number $z_{\alpha/2}$ such that 
$$
Pr(-z_{\alpha/2} \leq Z \leq z_{\alpha/2}) = 1- \alpha
$$
or replacing with the definition of Z
$$
Pr(\bar{X}- \frac{z_{\alpha/2} \sigma}{\sqrt{p}} \leq \micro \leq \bar{X}+ \frac{z_{\alpha/2} \sigma}{\sqrt{p}})
$$
NB: $\bar{X}$ is a RV, meanwhile $\micro$ is constant (=0)
## Central limit theorem 
following the definition of the sequence. $\bar{X}$ approaches a $Normal(\micro,\sigma,\sqrt{p})$ RV as $p \rightarrow \infty$ 
## Discrete data histogram
given a discrete data sample multiset $S=\{x_1,x_2,...,x_p\}$ with possible value $\chi$ , the relative frequency is $\hat{f}(x)= \frac{\# \ of \ x_i \in S \ with \ x_i=x}{p}$ , a discrete data histogram is a graphical display of $\hat{f}(x)$ versus x.

- Discrete data histogram mean $\bar{X} = \sum_{x in \chi}x \hat{f}(x)$ 
- Ddh std deviation $s=\sqrt{(\sum_{x}x^2\hat{f}(x)) - \bar{X}^2}$ 
- Ddh variance $s^2$ 

sample mean and std deviation of ddh is mathematically equivalent to the sample version, if the frequencies have already been computed then $\bar{X}$ and s should be computed using ddh equations.

If the cumulative version of a distribution is preferred, use 
$\hat{F}(x) = \frac{\# \ of \ x_i \in S \ with \ x_i\leq x}{p}$ , useful for quantiles.
## Continuos data histogram
real valued sample $S={x_1,x_2,...,x_p}$ , data value are generally distinct, lower and upper bounds a,b $a \leq x_i < b$. Defines interval of possible values for random var X $\chi=[a,b)=\{x|a \leq x < b\}$.

## Binning
partition the interval $\chi= [a,b)$ into k equal width intervals. The bins are 
$B_0=[a,a+\delta)$ , $B_1=[a+\delta,a+2\delta),...$ The width of each bin is 
$\delta=(b-a)/k$ . For each $x \in [a,b)$ there is a unique $B_j$ with $x \in B_j$ 
- Estimated frequency of data values in $B_j$ is $\phi_j=\frac{\# \ x_i \in S \ for \ which \ x_i \in B_j}{p}$ 
- Estimated density of random variable X $\hat{f}(x)= \hat{f}_j(x)=\frac{\phi_j}{\delta}$ if $x \in B_j$ 
- Density: frequency normalized via division by $\delta$ 
- Frequency: density multiplied by $\delta$ 

Raising or lowering $\delta$ create smooth or noisy histograms
## Relative frequency
Define $p_j$ as the relative frequency of points in bin $B_j$ 
Define the bin midpoints $m_j=a+(j+\frac{1}{2})\delta$.

Then $p_j=\delta \hat{f}(m_j)$ 
## Histogram mean and standard deviation
$\bar{X} = \int^{b}_{a}x \hat{f}(x) dx$        $s=\sqrt{\int^{b}_{a}(x-\bar{X})^2\hat{f}(x)dx}$ 
X and s can be evaluated by summation 
$\bar{X} = \sum^{k-1}_{j=0}m_jp_j$           $s=\sqrt{(\sum^{k-1}_{j=0}m_j^2p_j)-\bar{X}^2 + \frac{\delta^2}{12}}$  (some choose to ignore the delta fraction). This is possible due to derivation of equation from those integrals 
$\int^{b}_{a} x \hat{f}(x)dx$  and $\int^{b}_{a}x^2\hat{f}(x)dx$  due to the fact that $\hat{f}(m_j)= \frac{p_j}{\delta}$ 
## Properties of sample mean histogram
- the histogram mean is approximately $\micro$
- the histogram std deviation is approx $\sigma/\sqrt{p}$ 
-  if p is sufficiently large the histogram density approximate the $Normal(\micro,\sigma,\sqrt{p})$ pdf.

I.E whatever is the distribution of the generated var (exponential, neg exp ecc...) if we put the values on an hist the density always approximate a normal RV
## Standardize sample mean distribution 
we can standardize the sample means $\bar{x}_1,\bar{x}_2,...$ by substracting $\micro$ and divide by $\sigma/\sqrt{p}$ to form standardize sample means $z_1,z_2,...$ and so 
$$
z_j=\frac{\bar{x}_j- \micro}{\sigma/\sqrt{p}} 
$$

## Properties of standardized sample mean histogram
- the histogram mean is approximately 0
- the histogram std dev is approximately 1
- if p is sufficiently large the histogram density approximates the Normal(0,1) pdf
## T statistic distribution
replace population std dev $\sigma$ with sample std dev $\hat{s}_j$ in $z_j$ equation. recall that:
- each $\bar{x}_j$ is a point estimate of $\micro$ 
- each $\hat{s}_j^2$ is a point estimate of $\sigma$^2 (and so for sj)
$$
t_j=\frac{\bar{x_j}-\micro}{\hat{s}_j/\sqrt{p}} 
$$
## Properties of t statistic histogram 
- if p>2 the histogram mean is approx 0
- if p>3 the histogram std dev is approx $\sqrt{\frac{p-1}{p-3}}$ 
- if p is sufficiently large the histogram density approx a Student(p-1) RV
## Interval estimation
if $x_1,x_2,...,x_p$ is an independent random sample from a source of data with unknown $\micro$ , if $\bar{x}$ and $\hat{s}$  are the mean and std dev of this sample and if p is large it is approximately true that $t = \frac{\bar{x}-\micro}{\hat{s}/\sqrt{p}}$ is a Student(p-1) random variate.

- this theorem provide a justification for estimating an interval that is likely to contain the mean $\micro$ 
- as $p \rightarrow \infty$ the Student(p-1) is indistinguishable from Normal(0,1)
## Confidence parameter
Suppose: T is a Student(p-1) RV, $\alpha$ is a confidence parameter $\in (0.0,1.0)$ then exists a corresponding positive real number $t^*$ also denoted as $t_{(p-1,\alpha/2)}$ 
$$
Pr(-t^*\leq T \leq t^*) = 1- \alpha
$$

suppose $\micro$ is unknown. Since $t \approx Student(p-1)$ then
$$
-t^* \leq \frac{\bar{x}-\micro}{\hat{s}/\sqrt{p}} \leq t^*
$$
will be approximately true with probability $1-\alpha$ . So with probability $1-\alpha$ :
$$
\bar{x}- \frac{t^*\hat{s}}{\sqrt{p}} \leq \micro \leq \bar{x}+\frac{t^*\hat{s}}{\sqrt{p}}
$$
NB $\micro = 0$ 
Theorem: if 
- $x_1,x_2,...,x_p$ is an independent random sample froma  source of data with unknown $\micro$ 
- $\bar{x}$ and $\hat{s}$ are the sample mean and sample std deviation
- p is large 
then given a confidence parameter $\alpha \in (0.0,1.0)$ there exist an associated positive real number $t^*$ such that  $Pr(\bar{x}- \frac{t^*\hat{s}}{\sqrt{p}} \leq \micro \leq \bar{x}+\frac{t^*\hat{s}}{\sqrt{p}}) \approx 1-\alpha$  

## Confidence interval 
given a random sample $x_1,x_2,...,x_p$ if we can calculate $\bar{x}$ and $\hat{s}$ , the interval with endpoints $\bar{x} \underline{+} \frac{t^*\hat{s}}{\sqrt{p}}$ is a random range of values that contains the true parameter $\micro$ with $(1-\alpha)\%$  confidence.

For calculate an interval estimate for the unknown $\micro$ :
- Pick a level of confidence $1-\alpha$ (tipically $\alpha=0.05$) 
- Calculate $\bar{x}$ and $\hat{s}$ 
- Calculate critical value $t^*=t-Student(p-1,1-\alpha/2)$ 
- Calculate interval endpoints $\bar{x} \underline{+} \frac{t^*\hat{s}}{\sqrt{p}}$ 

## Stopping rule
the asymptotic value of $t^*$ is $t^*_\infty= \lim_{p \rightarrow \infty}t-Student(p-1,1-\alpha/2) = Normal(0.0,1.0,1-\alpha/2)$ , unless $\alpha$ is very close to 0.0 if p>40 we can use $p^*_\infty$ 

Given a reasonable guess for $\hat{s}$ and a user specified half-width w, how much sample we must collect?
using $w = \frac{t^*\hat{s}}{\sqrt{p}}$ we can resolve for $p=\lfloor (\frac{t_\infty^*\hat{s}}{w})^2 \rfloor$   

## Sequential Stopping rule
if a reasonable guess of $\hat{s}$ is not available, w can be specified as a proportion of $\hat{s}$ eliminating it from the previous equation

for example if w is 10% of $\hat{s}$  and 95% of confidence is desired, p=384 should be used to estimate $\micro$ to within $\underline{+}w$ , after having generated an initial sample of this size, check whether the required precision has been achieved, if not use the sample derived from this sample to predict a new larger sample size.

w can be used as a precision parameter, assuming an initial value of p>40:
- Compute a first value for $\bar{x}$ and $\hat{s}$ and check $\frac{w}{\bar{x}} = \frac{t^*\hat{s}}{\bar{x}\sqrt{p}} < \epsilon$ 
- If the inequality is not satisfied the value of p can be guessed to be at least $p=\lfloor (\frac{t_\infty^*\hat{s}}{\bar{x}\epsilon})^2 \rfloor$
- Repeat until the desired precision is not reached