## Birth death process with constant rates 
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