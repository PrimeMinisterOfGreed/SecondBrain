
## Quantità assiomatiche

-  $T$ => lunghezza del periodo d'osservazione
-  $B$ => frazione di tempo per cui il sistema è occupato 
-  $C$ => Job completati 
-  $A$ => Numero di arrivi

### Quantità derivate 

-  $\lambda = \frac{A}{T}$  job/sec -> Rateo di arrivi
-  $X= \frac{C}{T}$ => throughput
-  $U= \frac{B}{T}$ => Utilizzo
-  $S = \frac{B}{C}$ => tempo di servizio medio 


### Saturation
- $U = X*S$  -> legge dell'utilizzazione
- $A = C$  -> equilibrio dei flussi/ equilibrio operazionale 
- $U= \lambda*S$ 
- Saturation =>  $U \leq 1$ -> $X \leq  \frac{1}{S}$  e $\lambda \leq \frac{1}{S}$ 
Se $X = \frac{1}{S}$  =>  **il sistema è saturato**

## Statistiche del cliente 
- $a_k$  = tempo di arrivo del k-th cliente 
- $c_k$ = Instante in cui il cliente lascia il sistema  ( $c_k \gt a_k \geq 0$)
- $w_k = c_k - a_k$ Tempo di attesa del k-esimo cliente
- $\bar{w} = \frac{1}{C} \sum^{C}_{k=1}{w_k}$ tempo d'attesa medio 
## Formula di little ⚠

- $\bar{n} = X*\bar{w}$ -> legge del tempo d'attesa :LiAward:
- $\bar{n} = \lambda*\bar{w}$ -> formula di little :LiAward:

![[Pasted image 20231001123801.png]]

formula di little senza equilibrio operazionale 
$\bar{n} = \frac{G(T)}{T}$  e $\bar{w} = \frac{G(T)}{A(T)}$  --> $\bar{n} = \frac{A(T)}{G(T)} \bar{w} X$ 

## Reti di code
i = 1,...,M ->Indice per ogni stazione. 0 sta ad indicare una stazione esterna. :LiArrowLeftCircle:

- $U_i= X_iS_i$ , $X_0= \frac{C_0}{T}$ , $\lambda_0 = \frac{A_0}{T}$  --> in equilibrio operazionale. $\lambda_0 = X_0$ ⚠
- $V_i$  Numero di richieste di servizio alla stazione i $V_i = \frac{C_i}{C_0}$ ⚠
- $D_i$ Domanda totale di servizio  $D_i = V_iS_i=\frac{B_i}{C_0}$ 


### Leggi di consistenza
- $X_0 = \frac{C_0}{T} =\frac{1}{V_i}X_i = \frac{X_i}{V_i}$  -> throughput in termini di visite 
- $X_0 = \frac{C_0}{T} = \frac{1}{D_i} = \frac{U_i}{D_i}$  -> throughput in termini di utilizzazioni

>[!definition] Leggi di consistenza  
>$$\frac{X_i}{X_j} = \frac{V_i}{V_{j}}\implies\frac{U_i}{U_j} = \frac{V_iS_i}{V_jS_j} = \frac{D_i}{D_j}$$ 
>

il throughput e l'utilizzazione sono misure che variano a seconda del carico del sistema, i rapporti rimangono stabili tra una stazione e l'altra.
Le visite sono invece una caratteristica che varia da stazione a stazione.

### Rappresentazione matriciale 

- $C_i$ Numero di partenze dalla stazioni i
- $C_{i,j}$ Porzioni di partenze che si muovono da i a j
==>$C_i=\sum^{M}_{j=0}{C_{i,j}}$ :LiXSquare:

- $q_{i,j} = \frac{C_{i,j}}{C_i}$ Tasso di transizioni da i a j ==>  $\frac{C_{i,j}}{T} = q_{i, j}X_i$ :LiXSquare:

Se siamo in equilibrio operazionale -> $A_i = C_i$, e quindi  $X_j = \sum^{M}_{i=0}{X_iq_{i,j}}$  che può essere scritto come  $\boldsymbol{X}= \boldsymbol{X}\boldsymbol{Q}$   

Dove :
- $\textbf{X} = (X_0,...,X_M)$  --> è un vettore di M+1 componenti che rappresenta i throughput
- $\textbf{Q}$ Matrice quadrata (M+1) x (M+1) composta dai  $q_{i,j} = \frac{C_{i,j}}{C_i}$ , questa matrice caratterizza completamente il sistema. 

Ne segue che l'equazione di bilanciamento dei flussi può essere riscritta come $$\frac{X_j}{X_0}  = \sum^{M}_{i=0}\frac{X_i}{X_0}q_{i,j}$$ 

#### Regola di Little per Reti di Code 
usando $V_j=\frac{X_j}{X_0}$  e sapendo che $V_0 = 1$ è possibile definire la matrice  $\textbf{V} = \textbf{V}\textbf{Q}$ che può essere usata per descrivere il sistema. Ciò è possibile grazie alle leggi di consistenza. Ne segue anche che  $$\bar{n_i} = X_i\bar{w_i}$$  Dove:
- $\bar{n_i}$ => numero medio di clienti alla stazione i
- $\bar{w_i}$ => tempo d'attesa medio

## Dipendenza dal carico 
- $T(n)$ => Tempo speso dal cliente dentro al sistema
- $K_{max}$ => Massimo numero di clienti simultaneamente presenti dentro al sistema  

==> $T = \sum^{K_{max}}_{n=0}T(n)$  e $B=T-T(0)$  

#### Comportamento dipendente dal carico 

- $\phi(k) = \frac{T(k)}{T}; k=0,...,K_{max}$ => frazione di tempo spesa dal sistema nello stato k
- $C(k)$ -> numero di completamenti con k clienti   -> $\sum^{K_{max}}_{k=1}{C(k)} = C$ 
- $S(k) = \frac{T(k)}{C(k)}$ -> tempo medio di servizio dipendente dal carico o **funzione di servizio** 
- $X = \sum^{K_{max}}_{k=1}{\frac{1}{S(k)}{\phi(k)}}$ => throughput generalizzato 

### Comportamento dipendente dal carico per reti di code 
- $T_i(k)$ => Tempo speso dal cliente nella stazione i (i=1,...,M) 
Usando questa quantità possiamo scrivere:
- $\sum^{K_{max}}_{k=0}T_i(k) = T;i=0\dots M$  e quindi 
- $\phi_i(k) = \frac{T_i(k)}{T}$ => frazione di tempo spesa da ogni cliente nella stazione I. 

Sia:
- $C_i(k)$  (i=1,...,M) => il numero di completamenti con k clienti in coda alla stazione i
 - $\sum^{K_{max}}_{k=1}C_i(k)=C_i$   (i=0,..,M) anche in questo caso 
Si può quindi definire nuovamente => $S_i(k)= \frac{T_i(k)}{C_i(k)}$  (i=0,...,M;k=1,...,$K_{max}$)  

e di nuovo $X_i=\sum^{K_{max}}_{k=1}\frac{1}{S_i(k)}\phi_i(k)$  (i=0,...,M)

## Tempo di Risposta 

Con $V_i$ e $\bar{w_i}$ è possibile calcolare il tempo impiegato dal cliente per attraversare il sistema in 
2 tipi di sistema :
- Sistemi aperti:
    - I nuovi clienti arrivano con tasso $\lambda$ .
    - Il loro numero può aumentare a $\infty$ .
    - fino a che il sistema non è saturato abbiamo $X_0 = \lambda$ 
- Sistemi chiusi: 
    - Numero fisso N di clienti nel sistema
    - I clienti che escono vengono rimpiazzati subito con nuovi clienti 
### Tempo di risposta: Caso dei sistemi aperti

- $\Omega_i=V_i\bar{w_i}$ (i=1,...,M) => tempo medio speso dal cliente nella stazione i
- $R = \sum^{M}_{i=1}\Omega_i$ => Tempo medio di risposta del sistema (o tempo di risposta medio dei clienti all'interno del sistema 

usando la regola di Little 
$$\bar{n}=\lambda R=\sum^{M}_{i=1}X_i\bar{w_i}= \sum^{M}_{i=1}{\lambda \Omega_i}=\sum^{M}_{i=1}\bar{n_i}$$
### Tempo di Risposta: Caso dei sistemi chiusi 
N clienti nel sistema. In questo caso la stazione di indice 0 non ha significato e bisogna quindi selezionarne una di riferimento (qui definita **stazione arbitraria** ) perciò $\Omega_i$ sono dipendenti da k.

- $R_k = \sum^{i=1,i \neq k}_{M}{\Omega_i}$  => Tempo di risposta => Tempo impiegato dal cliente per tornare alla stazione k
- $Y_k = \bar{w_k}+R_k = \sum^{M}_{i=1}{\Omega_i}$  => Tempo di ciclo => Tempo medio impiegato dal cliente per fare un tour completo del sistema 

Si può generalizzare prendendo in considerazione un arbitraria stazione k
$$
\begin{aligned}
V_j^{[k]} = \frac{C_j}{C_k} = \frac{X_j}{X_k} = \sum^{M}_{i=1}V_i^{[k]}q_{i,j} &&  j=1,...,m
\end{aligned}
$$

Possiamo espandere la notazione prendendo in considerazione una seconda stazione h
$$
\begin{align}
V_j^{[h]} = \frac{C_j}{C_h} = \frac{V_j^{[k]}}{V_{h^{[k]}}}&& j,h,k=1,...,M
\end{align}
$$      
E per questa stazione scelta calcolare 
$$Y_k = \sum^{M}_{i=1}{\Omega_i}^{[k]} = \sum^{M}_{i=1}{V_i^{[k]}}\bar{w_i}$$ 
e anche 
$$Y_h = \sum^{M}_{i=1}\Omega_i^{[h]} = Y_k\frac{1}{V_h^{[k]}}$$  ottenendo quindi la forma generale 
$$R_h = Y_h - \bar{w_h}$$ ⚠ 


### Sistemi chiusi con stazione di ritardo 
- $Z$ => Ritardo medio della stazione 0 (stazione di ritardo)
usando la stazione di ritardo come referenza si possono calcolare tutte le visite nel sistema. 
Possiamo scrivere 
- $R_0 = \sum^{M}_{i=1}{\Omega_i}$ 
- $Y_0= Z+R_0$. 
Visto che il numero di clienti all'interno del sistema è costante possiamo usare la regola di Little sul sistema come fosse una black box.
![[Pasted image 20231001173621.png]]

in equilibrio operazionale abbiamo => $X_0=\frac{A_0}{T} = \frac{C_0}{T}$. 
Siano:
- $\bar{n_d}$  => il numero medio di clienti nella stazione di ritardo  
- $\bar{n_{cs}}$ => il numero medio di clienti nel sistema centrale 

$$N=X_0Y_0= X_0(Z+R)= \bar{n_d} + \bar{n_{cs}} \implies R_0 = \frac{N_{cs}}{X_0} - Z$$
- $U= n_{cs}/N$ => utilizzo del sistema centrale 



## Analisi del collo di bottiglia 
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

#### Simplify transition rates (Balance equations)
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


## One step behavior

![[Pasted image 20231006152829.png]]
since $T(n)$ sum to $T$ we can add the normalization condition $\sum_np(n)=1$. in this way the unique changes that can happen is the arrival or the departure of a customer.

## State balance of a network of queues
set of all possible states $S(M) = \{\underline{n} =(n_1,n_2,...,n_M), n_i \geq 0 i=1,2,...,M\}$  

$\underline{k}, \underline{m}$ and $\underline{n}$ will be generic states.

### Intermediate behavior
$T(n)$ = total time spent by the system in state $\underline{n}$ during observation period, with $\sum T(n) = T$. 
Let $P(n)= T(n)/T$ be the fraction of time spent by the system in state $\underline{n}$. 

the set of fractions of time spent by the system in each state in $S(M)$ or $\{P(\underline{n}), \underline{n} \in S(M)\}$ is called "distribution of the fractions of time spent by the system in its states". The objective is to derive P(n) not through direct measures but by using the parameters of the model. 

let $C(\underline{n}, \underline{m})$ be # of direct transition made by the system from state $\underline{n}$ to state $\underline{m}$. In our measurement we can't observe transition within the same state so $C(\underline{n},\underline{n}) = 0$ for any n

### Operational equilibrium : steady state
also in this case $A=C$ is required for every station. The number of departures and arrivals must be $n_i(0)= n_i(T) \ \ \  i=1...M$.

this means that the op eq condition is satisfied every time the measurement start with a state and ends with that state. For a single server in isolation then 
$$
\sum_kC(\underline{k},\underline{n}) = \sum_mC(\underline{n},\underline{m}) \ \ \ \forall \underline{n}
$$

then we can say "the flow balance condition among customer of a system is equivalent to balancing the number of transition among the  state of the system" 

Define now the transition rate from n to m as $r(\underline{n},\underline{m})= \frac{C(\underline{n},\underline{m})}{T(\underline{n})}$ . 
$T(\underline{n})=0$ implies $C(\underline{n}, \underline{m})=0$. Now we can introduce those variables in balance equation 
$$
\sum_\underline{k} P(\underline{k})r(\underline{k},\underline{n}) = P(\underline{n}) \sum_\underline{m}r(\underline{n},\underline{m}) 
$$
the definition of P(n) allows to add a normalization equation 
$\sum_\underline{n}P(\underline{n})=1$ 

### Derived Measures (One step behaviour)
denoting with H the total number of equations of this system, his value can be $H=(N_{max}+1)^M$  and $H = \binom{N+M-1}{M-1}$  in the case of a open system with Nmax customers observed or closed with N respectively.

According to the one step behavior hypothesis the transition can occur only within adjacent states.  Let's introduce the following definitions 
$\underline{n_{ij}} = (n_1,...,n_i+1,...,n_j-1,...,n_M)$ 
$\underline{n_{i0}} = (n_1,...,n_i+1,...,n_j,...,n_M)$ 
$\underline{n_{0j}} = (n_1,...,n_i,...,n_j-1,...,n_M)$ 
that we can use to indicates the states that are adjacent to 
$\underline{n} = (n_1,...,n_i,...,n_j,...,n_M)$ 


### Homogeneity
1) the output of a station of the system is completely determined by the length of its input queue, but independent of the length of the others stations.
2) the transition frequencies among the stations of the system are independent of the state of the system and may depend at most on the total load of the system(N)

### Simplify state transition balance equation (homogeneity)

First part of hypothesis allows to simplify the definition of the state transition rates in 
$$
r(\bar{n},\bar{n}_{ij})=\frac{C_{ij}(n_{j})}{T_{j}(n_{j})}
$$
the second part implies that $C_{ji}(n_{j})=C_{j(n_{j})}q_{ji}$
so that overall we obtain 
$$
r(\bar{n},\bar{n}_{ij})= 
\begin{cases}
\frac{q_{ji}}{S_{j(n_{j})}}  &  j \rightarrow i  \\
\frac{q_{j_{0}}}{S_{j}(n_{j})} & j \rightarrow 0 \\
\lambda_{0i}  &  0 \rightarrow i
\end{cases}
$$


let's introduce an indicator function defined in this way $\sigma(n)= \begin{cases}1 \ \ \ n>0 \\0 \ \ \ n=0\end{cases}$ 
using $\lambda_{0j}$ as the external arrival rate directed toward the station of index j
With all those hypothesis the transition balance equations assume the following form 
$$
\sum^{M}_{i,j=1}P(\underline{n}_{ij}) \frac{q_{ij}}{S_i(n_i+1)}\sigma(n_j) + \sum^{M}_{j=1}P(\underline{n}_{0j})\lambda_{0j}\sigma(n_j) + \sum^{M}_{i=1}P(\underline{n}_{i0})\frac{q_{i0}}{S_i(n_i+1)}= P(\underline{n})[\sum^{M}_{i=1}\frac{\sigma(n_i)}{S_i(n_i)} +  \sum^{M}_{j=1}\lambda_{0j}]
$$

## Solving transition balance 
assume all the $V_i$ are computed so that we can assume $\lambda_i=\begin{cases}\lambda V_i \ \ \ open\ system \\ V_i \ \ \ closed\ system \end{cases}$ , where $\lambda$ represent the total arrival rate of external customers to the system.  Define also the following function 
$$
f_i(k)= \begin{cases}
1 \ \ \ k = 0 \\
\lambda_iS_i(k)f_i)k-1 \ \ \ k>0
\end{cases}
$$
is it possible to show that the time spent by the system in each of its states is $$P(\underline{n})= \frac{1}{G} \prod^{M}_{i=1}f_i(n_i)$$
This is called product form solution , G is a normalization constant defined in this way 
$$
1= \sum_{\underline{n}}P(\underline{n}) = \frac{1}{G}\sum_{\underline{n}}\prod^{M}_{i=1}f_i(n_i) \rightarrow G= \sum_{\underline{n}}\prod^{M}_{i=1}f_i(n_i)
$$
### Queue length distribution 

using the recursive expression of $p(\underline{n})$ we obtain (no intermediary)
$$
\begin{cases}
P(\underline{n}_{i0}) = \lambda_iS_i(n_i+1)P(\underline{n}) \\
\\
P(\underline{n}_{0j}) = \frac{1}{\lambda_jS_j(n_j)}\\
\\
P(\underline{n}_{ij}) = \frac{\lambda_iS_i(n_i+1)}{\lambda_jS_j(n_j)}P(\underline{n})
\end{cases}
$$

define the number of distribution of the number of customer at station 
$$
p_i(k) = \sum_{\underline{n_{n_i = k}}}P(\underline{n})
$$
recall $F(k)= \lambda S(k)f(k-1)$ for k>0 and F(0)=1
- Case 1: Single server queue $p(n)=p(0)F(n)$    n>0
- Case 2: Single Server queue embedded in Open network $P_M(n)=\frac{1}{G_M}F_M(n)$ n>0
- Case 3: Single Server queue in closed netork $P_M(n)=\frac{g(N-m,M-1)}{G(N,M)}F_M(n)$    $0 \leq n \leq N$ 
in Case 1 the normalizing constant p(0) is different from zero if the queue is stable
$\lambda*S(k)<1$  for k>k0
in Case 2 the normalizing constant Gm is != 0 if the queue is stable $\lambda_M*S_m(k)<1$ 
in Case 3 the normalization factor is not constant.

We then obtain the following performance indices 

- $X_i=\sum^{n}_{k=1}p_i(k)\frac{1}{S_i(k)}$ 
- $U_i=1-P_i(0)$ 
- $\overline{n}_i=\sum_kkp_i(k)$ 
- $\overline{w_i} = \frac{n_i}{X_i}$ 

### The BCMP theorem
A queueing network has a product form solution if it satisfies the following criteria:
- The network has a finite number of stations 
- Customer belong to an arbitrary and finite number of closed or open classes and can change class memberships
- Routing probability are defined for each class identified by a DTMC (markov chain) (so as a matrix)
- The station of the network may be of 4 different types:
	- FCFS with negative exponential distribution of service times
	- LCFS with a rationale laplace transform distribution of service times 
	- Processor Sharing with a rationale laplace transform distribution of service times 
	- Infinite server with a rationale laplace transform distribution of service times

FCFS is commonly associated to negative exponential distribution, this is the standard first come first served policy.

LCFSpr (preemptive resume) last come first served: studied as a simple approximation of server undergoing high priority interruptions. When a new customer join a non empty queue, the customer in service is interrupted, pushed into an input stack and resumed later.

PS Process sharing discipline: represent a limit for the round robin discipline as its quantum size goes to 0

IS infinte server discipline makes the server equivalent to a delay station.

## Computing normalization constant in open systems 

Denote with $N_i,i=1,...,M$ the maximum number of customers observed at station i during all observation (0,T].
In the case of open systems those $N_i$ can be arbitrarily large (and in fact grow to infinity). This means that there is not dependency among $N_i$ so the normalization constant G becomes .
$$
G=\sum_\underline{n}\prod^{M}_{i=1}f_i(n_i) = \prod^{M}_{i=1}\sum^{N_i}_{i=1}f_i(n_i) = \prod^{M}_{i=1}G_i
$$
and then the product form solution become 
$$
P(\underline{n}) = \frac{1}{G} \prod^{M}_{i=1}f_i(n_i)=\prod^{M}_{i=1}\frac{f_i(n_i)}{G_i} = \prod^{M}_{i=1}p_i(n_i) 
$$
## Computing normalization constant in closed systems 

The indipendece of $N_i$ doesn´t apply for closed network. In closed systems there aren't new arrivals, so the only possibility are customers that move from one station to another. The global balance equations assumes a much simpler form. 
$$
\sum^{M}_{i,j=1}P(\underline{n_{ij}})\frac{q_{ij}\delta(n_j)}{S_i(n_i+1)}=P(\underline{n})\sum^{M}_{i=1}\frac{\delta(n_i)}{S_i(n_i)}
$$

the formal definitions remains the same.  for G: $P(\underline{n}) = \frac{1}{G}\prod^{M}_{i=1}f_i(n_i)$  where 
$$
f_i(k)= \begin{cases}
1 \ \ \ k=0 \\
V_iS_i(k)f_i(k-1) \ \ k>0
\end{cases}
$$
and $G = \sum_\underline{n}\prod^{M}_{i=1}f_i(n_i)$ 

### The Convolution method
In a closed system a state $\underline{n}$ is feasible if $n_i \geq 0,i=1\dots M$  and $\sum^{M}_{i=1}n_i=N$ the second condition introduce dependency among the stations of the system.

for convenience let's define the state space of the system with m station and n customers as
$$
S(n,m)=\{(n_1 \dots n_M | n_i \geq 0, i=1 \dots m; \sum^{m}_{i=1}n_i=n \}
$$
define the following auxiliary function $g(n,m)= \sum_{\underline{n} \in S(n,m)} \prod^{m}_{i=1}f_i(n_i)$  with $g(N,M)=G$ 
with a little manipulation is possible to prove that 
$$
g(n,m) = \sum^{n}_{k=0}f_m(k)g(n-k,m-1) 
$$
the definition of g(n,m) can be made recursive introducing the following base conditions
$g(0,m) = 1(m=0 \dots )$ and $g(n,0) = 0 (n=1 \dots)$. This definition is a convolution sum (Convolution algorithm) used for compute the normalization constant in efficient manner. 

### Computational Scheme for G
in order for this scheme to work we must have first computed all the values of $f_m(k)$ and of $g(k,m-1)$ , every row of the recursion of g correspond to a specific load of the system and every column correspond to a specific station. The recursion is made first on the loading level (n) and then on the components of the network(m) starting from the upper left corner and ending to the bottom right.
The complexity of the computation is in order of : $N^2*M$  in the general case and $N*M$ if all the stations are load indipendent (is much simpler to calculate). 
```
//Input -> M: int,N: int,V[i]: Array<double>, S[i](k): Array<Array<double>>, ST[i]: Array<SType>
//Output -> G(k): Array<double>

G[0] = 1.0;
for k in 1...N{
	G[k]= 0.0;
}
for i in 1...M{
	if(ST[i] == LI){
		d = V[i] * S[i][1];
		for k in 1...N{
			G[k] = G[k] + d*G[k-1];
		}
	}

	else{
		f[0] = 1.0
		for k in 1...N{
			f[k] = f[k-1]*V[i]*S[i][k];
		}
		for n in N...1{
			sum = G[n];
			for k in 1...n{
				sum += f[k] * G[n-k];
			}
		}
	}
}
```
### Computation of performance figures
using explicit expression of $P(\underline{n})$ we have $p_m(k)= f_m(k)\frac{g(n-k,m-1)}{g(n,m)}$.
note: for the rest of the scheme $p_m(k,n)$ will be simplified in $p_m(k)$ omitting the explicit dependence with the size of the population. Here some perfomance indices that can be calculated:
- $X_m= \sum^{n}_{k=1}p_m(k)\frac{1}{S_m(k)} = V_m \frac{g(n-1,m)}{g(n,m)}$ 
- $U_m=1-p_m(0)=1- \frac{g(n,m-1)}{g(n,m)}$ 
notice that X and U can be also picked from the table produced by the computation of g.
- $\overline{n}_m = \sum^{n}_{k=1}kp_m(k)$ 
- $\overline{w}_m = \frac{\overline{n}_m}{X_m}$ 
In case of load indipendent station the following can be applied 
- $U_m= X_m S_m = V_m S_m \frac{g(n-1,m)}{g(n,m)}$ (standard formula)
- $\overline{n}_m(n)= U_m(n)[1+\overline{n}_m(n-1)]$ 
- $\overline{w}_m(n)= S_m[1+\overline{n}_m(n-1)]$ 

### Arrival theorem 
$\overline{w}(n)= S_m[1+\overline{n}_m(n-1)$ this is known as the Arrival theorem that states: "if a single server has a poisson input process then the arriving customers see the queue as if they were external observers not involved in this operation".

In the case of closed queueing networks with Product form solution the same theorem say: when network has n customers, arriving customer see queue i as external observers which monitor the queue in equilibrium when only n-1 customers are is the system
## Mean value analysis 
Let's group all the recurrent expression
-  $\overline{w}_i(n) = S_i[1+\overline{n}_i(n-1)]$
- $U_i(n)=X_i(n)S_i$ 
- $\overline{n}_i(n)= U_i(n)[1+\overline{n}_i(n-1)]$ 
The missing $X_i$ equation can be derived by using the little's law 
- $X_{ref}(n)= \frac{n}{\sum^{M}_{j=1}V_j \overline{w_j}(n)}$ (derived from the definition of $Y_k(n)$)   
- $X_i(n)= V_i X_{ref}(n)$ 
### MVA for LI stations 
```
Input -> M: int, N: int, V[i] : Array<double>, S[i]: Array<double>
Output -> X[i][k]: Array<Array<double>>, U[i][k]:Array<Array<double>>, n[i][k]:Array<Array<int>>, w[i][k] : Array<Array<double>>

for k in 1...N{
	for i in 1...M{
		w[i][k] = S[i]*(1+n[i][k-1]);
	}
	sum = 0;
	for i in 1...M{
		sum += V[i]*w[i][k];
	}
	Xref = k/sum;
	for i in 1...M{
		X[i][k]= V[i]*Xref;
		U[i][k]=S[i]*X[i][k];
		n[i][k]=U[i][k]*(1+n[i][k-1]);
	}
}

```

### Mean value analysis with delay stations
in the case of delay station $\overline{w}_i(n)= Z$ always. The algorithm can so modified observing that 
- $\overline{w}_i(n)= \begin{cases}Z_i \ \ \ delay\ station \\ S_i[1+\overline{n}_i(n-1)] \ \ \ LI \  station \end{cases}$  
- $\overline{n}_i(n)= \begin{cases}Z_iX_i(n) \ \ \ Delay \ Station \\ U_i(n)[1+\overline{n}_i(n-1)] \ \ \  LI \end{cases}$ 
- $U_i(n)= \begin{cases}\frac{\overline{n}_i(n)}{n} \ \ \ DI \\ X_i(n)S_i \ \ \ LI \end{cases}$ 
### MVA for LI&D stations 
```
Input -> M: int, N: int, V[i] : Array<double>, S[i]: Array<double>, ST[i]: Array<StationType>,Z[i] : Array<double>
Output -> X[i][k]: Array<Array<double>>, U[i][k]:Array<Array<double>>, n[i][k]:Array<Array<int>>, w[i][k] : Array<Array<double>>

for k in 1...N{
	for i in 1...M{
		if(ST[i] == "D){w[i][k] = Z[i]}
		else{w[i][k] = S[i]*(1+n[i][k-1]);}
	}
	sum = 0;
	for i in 1...M{
		sum += V[i]*w[i][k];
	}
	Xref = k/sum;
	for i in 1...M{
		X[i][k]= V[i]*Xref;
		if(ST[i] == "D){
			n[i][k] = Z[i]*X[i][k];
			U[i][k] = n[i][k]/k;
		}
		else{
		U[i][k]=S[i]*X[i][k];
		n[i][k]=U[i][k]*(1+n[i][k-1]);
		}
	}
}

```

### Mean value analysis with  Load dependent stations

consider the expression for the queue length distribution $p_m(k,n)= f_m(k)\frac{g(n-k,m-1)}{g(n,m)}$ , recall: the explicit expression of the service function $f_m(k)=V_mS_m(k)f_m(k-1)$  and throughput $X_m(n)= V_m \frac{g(n-1,m)}{g(n,m)}$  , substituting in the expression of queue length distribution we obtain  $p_m(k,n)= X_m(n)S_m(k)p_m(k-1,n-1)$ (intermediate passage omitted). since expression of $X_m$ hold for any index i we can use that expression for any index. The new recursive expression let us to obtain: 

- $\overline{w}_i(n) = \frac{\overline{n}_i}{X_i(n)} = \frac{\sum^{n}_{k=1}kp_i(k,n)}{X_i(n)} = \sum^{n}_{k=1}kS_i(k)p_i(k-1,n-1)$ latter passage with queue length distribution 
- $X_{ref}(n)= \frac{n}{\sum^{M}_{j=1}V_j \overline{w}_j(n)}$ 
- $X_i(n)= V_iX_{ref}(n)$ 
- $\overline{n}_i(n)=\overline{w}_i(n) * X_i(n)$ 
- $p_i(k,n)= X_i(n)S_i(k)p_i(k-1,n-1)$
- $p_i(0,n)= 1- \sum^{n}_{k=1}p_i(k,n)$ 
- $U_i(n)= 1-p_i(0,n)= \sum^{n}_{k=1}p_i(k,n)$ 

embedding these equation is easy, at each step the queue can be computed as $p_i(0,n)=1.0-U_i(n)$  and is initialized $p(0,0)=1.0$ 

### MVA for LD stations 
not usable when the bottleneck station is load dependent.
```
Input -> M: int, N: int, V[i] : Array<double>, S[i]: Array<double>
Output -> X[i][k]: Array<Array<double>>, U[i][k]:Array<Array<double>>, n[i][k]:Array<Array<int>>, w[i][k] : Array<Array<double>>, p[i][k][n]: Array<Matrix<2,double>>

cum = 0.0;wait=0.0;y=0.0
for i in 1...M{
	p[i](0,0) = 1.0;
	for j in 1...N{p[i](j,0) = 0.0;}
}

for k in 1...N{
	for i in 1...M{
		for j in 1...k{
			wait += j * S[i][j]*p[i](j-1,k-1);
			w[i][k]=wait;
		}
	}
	for i in 1...M{
		Y+= V[i]*w[i][k];
	}
	Xref= k/Y;
	for i in 1...M{
		X[i][k] = V[i]*Xref;
		for j in 1...k{
			p[i](j,k)=X[i][k]*S[i][j]*p[i](j-1,k-1);
			cum += p[i](j,k);
		}
		p[i](0,k) = 1.0-cum;
		u[i][k]=cum;
		n[i][k]=X[i][k]*w[i][k];
	}
}


```