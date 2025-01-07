## Z Transform 
we define the z transform of sequence $f_n$ as $F(z)= \sum^{\infty}_{k=0}f_kz^k$  
where z is a complex variable such that $|z|<1$ . A property of z transform is that 
$$
f_n = \lim_{z \rightarrow 0} \frac{1}{n!}\frac{d^nF(z)}{dz^n} 
$$
because 
$$
\frac{d^nF(z)}{dz^n} = \frac{d^n}{dz^n}(\sum^{\infty}_{k=0}f_kz^k)=n!f_n+\sum^{\infty}_{k+n+1}\frac{k!}{(k-n)!}z^{k-n}f_k
$$

## laplace transform
transformation for continuous functions: 
$$
B^*(s)= \int^{\infty}_{0+}f(t)^{-st}dt=\mathcal{L}_s[f(t)] 
$$
Properties of laplace transform 
- $\mathcal{L}_s[af(t)+bg(t)]=a \mathcal{L}_s[f(t)]+ b \mathcal{L}_s[g(t)]$ 
- $\mathcal{L}_s[f'(t)]=s\mathcal{L}_s[f(t)]-f(0^+)$ 


# Probability 

### Conditional Probability 

$P[A|B] = P[A,B]/P[B]$  where $P[A,B]  = P[A|B] * P[B]$
