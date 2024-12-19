

## Processi di nascita e morte e code
i tempi tra morti e nascite sono descritte da variabili aleatorie distribuite secondo una negativa esponenziale .
- Le nascite sono interpretabili come arrivi dei clienti  
- Le morti come partenze dei clienti 

Perciò questi processi possono essere usati come descrizione matematica delle stazioni di servizio, dove i clienti arrivano con un processo di poisson e i tempi di servizio sono distribuiti come VA negative esponenziali. La gestione della coda ha una policy particolare.
Soluzione al processo di nascita e morte
$$
\begin{align}
\pi_k=\frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\micro_1 \micro_2 ... \micro_k} \pi_0 

&& \pi_0=\frac{1}{1+\sum^{\infty}_{k=1} \prod^{k-1}_{j=0}\frac{\lambda_j}{\micro_j+1}}
\end{align}
$$

## Notazione di kendall
Le code sono del tipo  A/B/C/K/N/D dove: 
- A processo d'arrivo: M is markovnian (poisson,exponential distribution), G general (non markov)
- B processo di servizio : M markovnian (exp. distribution), G general (non markovnian) 
- C numero di servitori
- K massimo numero di clienti accodabili (not specified --> infinite)
- N massimo numero di clienti che richiedono un servizio (not specified --> infinite)
- D disciplina usata per la coda ((not specified --> FCFS)

## M/M/1 queue
è il caso più semplice dove:
gli arrivi sono processi poisson, i tempi di servizio sono distribuiti come esponenziali, server singolo, massima lunghezza di coda infinita, poplazione di clienti infinita, FCFS discipline, 
i tassi di arrivi e partenze sono costanti $\lambda_k = \lambda$ e $\micro_k = \micro$ .

Usando la soluzione ai processi di nascita e morte, la distribuzione delle probabilità degli stati è
$$
\pi_k=\pi_0 \prod^{k-1}_{i=0}\frac{\lambda}{\micro
}=\pi_0(\frac{\lambda}{\micro})^k
$$
con condizioni di ergodicità

$$
\begin{align}
S_1= \sum^{\infty}_{k=0}(\frac{\lambda}{\micro})^k < \infty && S_2=\sum^{\infty}_{k=0}\frac{1}{\lambda}(\frac{\micro}{\lambda})^k = \infty
\end{align}
$$

soddisfatte solo se  $\frac{\lambda}{\micro}<1$ , le condizioni di normalizzazione 
portrano a :
- $\pi_0=1-\frac{\lambda}{\micro}= 1-\rho$  
- $\pi_k=(1-\rho)\rho^k$ (refer to special case)

### Indici di performance M/M/1
l'utilizzo del sistema è uguale a $\rho$ --> $U=1-\pi_0=\rho$ 

-  $E[n]=\bar{n}=\sum^{\infty}_{k=0}k \pi_k=\frac{\rho}{1-\rho}$  numero medio di clienti
-  $E[n^2]=\bar{n^2}=\sum^{\infty}_{k=0}k^2\pi_k=2(\frac{\rho}{1-\rho})^2+\frac{\rho}{1- \rho}$ => secondo momento 
-  $VAR[n]=E[n^2]-(E[n])^2=\frac{\rho}{(1-\rho)^2}$  => varianza

Usando la formula di little otteniamo il tempo di soggiorno dei clienti in coda
$$E[w]=\frac{E[n]}{\lambda}=\frac{1/\micro}{1- \rho}$$ 

Possiamo anche stimare la probabilità che una coda ecceda una certa soglia
$$
Pr\{n \geq k\}= \sum^{\infty}_{i=k}\pi_i=\rho^k
$$


## M/M/1 coda con arrivi scoraggiati 
più lunga la coda più gli arrivi sono lenti. $\lambda_k = \frac{\lambda}{k+1}$  e $\micro_k=\micro$.
Usando la soluzione ai processi di nascita e morte $\pi_k=\pi_0(\frac{\lambda}{\micro})^k \frac{1}{k!}$ ne segue che

$$
\begin{align}
\pi_0=e^{-\lambda/\micro} && \pi_k=\frac{(\lambda/\micro)^k}{k!}e^{-\lambda/\micro}
\end{align}
$$
l'ergodicità è soddisfatta se $\lambda/\micro < \infty$

### indici di performance

utlizzo del sistema: $U = 1-e^{-\lambda/\micro}$ 

numero medio di clienti $E[n]=\bar{n}=\frac{\lambda}{\micro}$

throughput:  $X=\micro \sum^{\infty}_{k=1}\pi_k=\micro(1-e^{-\lambda/\micro})$ 
e usando la formula di little possiamo calcolare il tempo di soggiorno $E[w]=\frac{E[n]}{X}=(\frac{\lambda}{\micro^2(1-e^{-\lambda/\micro}})$  


## Distribuzione dei tempi di soggiorno per code M/M/1
### Pasta Property
la probabilità di trovare k clienti in coda  $\pi_k= \lim_{t \rightarrow \infty} Pr[N(t)=k]$ ,può essere interpretata come frazione del tempo speso nello stato $E_k$.
$\pi_k^{[a]}$ = Pr\[un cliente che arriva trova il sistema nello stato $E_k$]. 

Queste 2 quantità non sono uguali se consideriamo una coda D/D/1 (tassi deterministici) cosi che $\lambda < \micro$ , dove:
- i tempi di inter-arrivo sono costanti $\tau = 1/ \lambda$ 
- cosi come i tempi di servizio $\sigma = 1/ \micro$.  

In questo caso abbiamo 
$$
\begin{align}
\pi_0 = 1- \frac{\lambda}{\micro} && \pi_1 = \frac{\lambda}{\micro} &&(\pi_k=0,k>1)\\
\pi_0^{a}=1- \frac{\lambda}{\micro} && \pi_k^{a}=0 && k>0
\end{align}
$$
da cui segue che $\pi_k^a \neq \pi_k$ 

Se invece consideriamo una distribuzione di arrivo poissoniana le due quantità si equivalgono. sia:
- $A(t,t+\Delta t)$ => evento per cui un arrivo avviene nel tempo $(t,t+\Delta t)$ 

allora $\pi_k^{a}(t)= \lim_{\Delta t \rightarrow 0} Pr[N(t)=k|A(t,t+\Delta t)]$ , condizionando questa probabilità
$$
\pi_k^{a}(t)=\lim_{\Delta t \rightarrow 0} \frac{
Pr[A(t,t+ \Delta t)| N(t)=k]Pr[N(t)=k]
}{
Pr[A(t,t+ \Delta t)]
}
$$
Siccome l'arrivo è poissoniano  (memory-less property) **l'evento A deve essere indipendente dal tempo t**, per cui
$Pr[A(t,t+ \Delta t)| N(t)=k] = Pr[A(t,t+ \Delta t)]$ che porta $\pi_k^{a}(t)=\pi_k(t)$ .

questa è la PASTA property (Poisson arrivals see time averages): dice che **un arrivo da un sistema poissoniano vede la coda come se stesse arrivando in un tempo aleatorio** . il valor medio di ogni parametro della coda all'arrivo poissoniano è la media a regime di quel parametro (avg queue length, p server is idle ecc...). 

### Distribuzione del tempo di soggiorno M/M/1

sia:
- W la variabile aleatoria che rappresenta il tempo di soggiorno dei clienti in una FCFS M/M/1 station. 
-  $W_n^{[a]}$ il tempo di soggiorno di un cliente in arrivo dato che ci sono n clienti in coda nel sistema  ($n^{[a]} = n)$, questa variabile aleatoria si può scrivere come : 
$$
W_n^{[a]}=\sigma + \omega_1 + \omega_2+...+\omega_{n-1}+R
$$
dove:
-  $\sigma$ rappresenta il tempo di servizio del cliente appena entrato 
- $\omega_{1}, \omega_2,...,\omega_{n-1}$ rappresenta il tempo di servizio per i clienti che erano già in coda  
- R rappresenta il tempo rimanente di servizio per il cliente che era in servizio. 

Siccome : tutti i clienti sono statisticamente equivalenti (hanno tutti la stessa distribuzione del parametro $\micro$ e questa gode dell'assenza di memoria) 
allora $W_n^{[a]}$ è la somma delle n+1 esime variabili aleatorie della stessa variabile negativa esponenziale così che $Pr\{X \leq t \} = 1 - e^{-\micro t}$ la cui trasformata di laplace è $\frac{\micro}{s + \micro}$  

sia:
- $F_{W^{[a]}(n,t)=}Pr\{W_n^{[a]} \leq t\}$ => CDF della variabile aleatoria $W_n^{[a]}$ 
- $f_{W^[a]}(n,s)=(\frac{\micro}{s+\micro})^{n+1}$ la sua trasformata di laplace .

Grazie alla proprietà della trasformata di laplace sulle convoluzione osserviamo che
$$
Pr\{W \leq t\} = \sum^{\infty}_{k=0}Pr\{W_{k}^{[a]} \leq t| n^{[a]}=k\}Pr\{n^{[a]}=k\}
$$
Quando gli arrivi sono poissoniani abbiamo $\pi_{k}^{[a]}=\pi_{k},k \geq 0$ e quindi
$$
F_{W}(t)=Pr\{W \leq t\}= \sum^{\infty}_{k=0}Pr\{W_{k}^{[a]} \leq t| n^{[a]}=k\}(1-\rho)\rho^{k}
$$
sia:
- $F^{*}_{W}(s)$ trasformata di laplace di questa probabilità  
- $f_{W}^{*}(s)$ trasformata di laplace della sua PDF
$$
f_{W}^{*}=\sum^{\infty}_{k=0}f_{W^[a]}^{*}(k,s)(1-\rho)\rho^{k}=(1-\rho)\frac{\micro}{s+ \micro}(\frac{1}{1-\frac{\rho \micro}{s+ \micro}})=(\frac{\alpha}{s+\alpha})$$
dove:
- $\alpha=(1-\rho)\micro$ è la trasformata di laplace di una negativa esponenziale con parametro $\alpha$

allora  $F_{W}(t)=Pr\{W \leq t\}= 1-e^{-\micro(1-\rho)t}$ 

## M/M/$\infty$ 
Sistema duale a m/m/1 con arrivi scoraggiati: più lunga a la coda più veloce il servizio : $\lambda_k=\lambda$  e $\micro_k=k \micro$ 
con la soluzione ai PNS. $\pi_k = \pi_0(\frac{\lambda}{\micro})^k \frac{1}{k!}$  porta a  
$$
\begin{align}
\pi_0=e^{-\lambda/\micro} && \pi_k=\frac{(\lambda/\micro)^k}{k!}e^{-\lambda/\micro}
\end{align}
$$

l'ergodicità è soddisfatta quando $\lambda/\micro < 1$ .

### Performance indices M/M/$\infty$
i risultati sono gli stessi degli arrivi scoraggiati, ne segue che $E[n]=\bar{n}=\frac{\lambda}{\micro}$

il tempo di soggiorno invece: $E[w]=\frac{E[n]}{\lambda}=\frac{1}{\micro}$ , dipende solo dal tempo di servizio

## M/M/m
come M/M/1 ma con m server identici che lavorano insieme. I clienti si accodano solo se tutti i server sono occupati.
$\lambda_k=\lambda$  e $\micro_k = \begin{cases}k \micro & 0 \leq  k \leq m \\ m \micro & m < k\end{cases}$ Usando la soluzione ai PNS otteniamo.
$$
\pi_k=
\begin{cases}
\pi_0 (\frac{\lambda}{\micro})^k \frac{1}{k!} & 0 \leq k \leq m \\ 
\pi_0 (\frac{\lambda}{\micro})^k \frac{1}{m!m^{k-m}} & m<k
\end{cases}
$$
Le condizioni di ergodicità sono soddisfatta per $\rho=\frac{\lambda}{m \micro}< 1$ portando 
$$
\pi_k = 
\begin{cases}
\pi_0 \frac{(m \rho)^k}{k!} & 0 \leq k \leq m \\
\pi_0 \frac{\rho^k m^m}{m!} & m<k
\end{cases}
$$
con espressione esplicita $\pi_k$ otteniamo
$$
\pi_0=[1+\sum^{m-1}_{k=1}\frac{(m \rho)^k}{k!}+ \sum^{\infty}_{k=m}(\frac{(m \rho)^m}{m!})(\frac{1}{1-\rho})]^{-1}
$$

il risultato precedente è computazionalmente semplice ma non ci permette di estrarre clienti medi e tempi soggiorno. Possiamo invece calcolare la probabilità che un cliente si acodi (con la Erlang C formula)
$$
Pr\{queue\ up\}= 

\sum^{\infty}_{k=m}\pi_k = \frac{ 
    (\frac{(m \rho)^m}{m!})(\frac{1}{1-\rho})
}{
[1+\sum^{m-1}_{k=1}\frac{(m \rho)^k}{k!}+(\frac{(m \rho)^m}{m!})(\frac{1}{1-\rho})
}
$$


## M/M/1/B coda con buffer finito
come M/M/1 ma con spazio finito in coda per i clienti. **se un cliente arriva e trova la coda troppo piena lascia il sistema** 
 $\lambda_k = \begin{cases} \lambda & 0 \leq k \leq B \\ 0 & k > B\end{cases}$  e $\micro_k=\micro$ , usando la soluzione ai PNS
$$
\pi_k= 
\begin{cases}
\pi_0(\frac{\lambda}{\micro})^k & 0 \leq k \leq B \\
0 &k > B
\end{cases}
$$
Il numero di possibili stati è limitato a B+1 per cui l'ergodicità non è un problema. Questo porta a
$$
\begin{align}
\pi_0=[\sum^{B}_{k=0}(\frac{\lambda}{\micro})^k]^{-1} = \frac{1-\lambda/\micro}{1- (\lambda/\micro)^{B+1}} && \pi_k=
\begin{cases}
\pi_0 (\frac{\lambda}{\micro})^k & 0 \leq k \leq B \\ 0 & k>B
\end{cases}
\end{align}
$$


Non è disponibile un espressione chiusa per il sistema , per cui non è possibile calcolare tempi di soggiorno e clienti medi. per il caso B=1 otteniamo 

$$
\pi_k= 
\begin{cases}
\frac{1}{1+(\lambda/\micro)} & k=0 \\
\frac{\lambda/\micro}{1+(\lambda/\micro)} & k =1\\ 
0 & k>1
\end{cases}
$$


## M/M/1//N Coda con popolazione finita 
come M/M/1 ma con numero massimo di clienti N (sistema chiuso). Il tasso di arrivo decresce man mano che i clienti arrivano: $\lambda_k= \begin{cases}\lambda(N-k) & 0 \leq k \leq N \\ 0 & k>N\end{cases}$ e $\micro_k=\micro$ , usando la soluzione ai PNS e sapendo che il sistema è già ergodico otteniamo. 
$$
\pi_k= 
\begin{cases}
\pi_0 \prod^{k-1}_{i=0}\frac{\lambda(N-i)}{\micro} & 0 \leq k \leq N \\
0 & k>N
\end{cases}
$$
che è
$$
\pi_k = 
\begin{cases}
\pi_0(\frac{\lambda}{\micro})^k \frac{N!}{(N-k)!} & 0 \leq k \leq N \\
0 & k>N
\end{cases}
$$
ottenendo
$$
\pi_0 = [1+\sum^{N}_{k=1}(\frac{\lambda}{\micro})^k \frac{N!}{(n-k)!}]^{-1}
$$


di nuovo **non è disponibile nessuna forma chiusa che permetta il calcolo dei tempi di soggiorno e lunghezza media della coda** 


## Arrivi a batch costanti  
- Coda singola 
- i clienti arrivano in batch composti da k clienti, un batch per volta
- la coda ha capienza infinita e i tempi di inter-arrivo  $\lambda$ e servizio $\mathcal{v}$ sono variabili aleatorie indipendenti con distribuzione negativa esponenziale
![[Pasted image 20231208151614.png]]
assumiamo che  $P_{j}=0\  \ j<0$  allora le equazioni di bilanciamento diventano
$$
\begin{align}
\lambda P_{0}= vP_{1} && (\lambda+\mathcal{v})P_{j}= \lambda P_{j-k}+\mathcal{v}P_{j+1}
\end{align}
$$
La soluzione diretta è difficile da calcolare, più facile con la  [[Formulas#Z Transform | ZTransform]] . 
sia:
- $\mathcal{P}(z)= \sum^{\infty}_{j=0}P_{j}z^{j}$ 

moltiplichiamo entrambi i lati dell'equazione per  $z^{j}$ , sommando su tutti i valori possibili di j, ponendo attenzione alla prima equazione (che include $P_0$ ) 
otteniamo
$$
\sum^{\infty}_{j=0}(\lambda+\mathcal{v})P_{j}z^{j}-vP_0=\sum^{\infty}_{j=1}\lambda P_{j-k}z^{j}+\sum^{\infty}_{j=0}vP_{j+1}z^{j}
$$
che dopo alcuni passaggi algebrici, diventa dopo aver applicato la trasformata 
$$\mathcal{P}(z)=P_{0}\frac{v(1-z)}{\lambda z^{k+1}-(\lambda+v)z+v}$$
per calcolare $P_0$ usiamo $\lim_{z \rightarrow 1 }\mathcal{P}(z)=1$ poichè $P_j$ sono distribuzioni di probabilità pers $\mathcal{P}(z)$, sia il numeratore che il denominatore tendono a 0 fintanto che z->1. Per cui applicando la regola di de l'hopital
$$
1= \lim_{z \rightarrow 1}P_{0}\frac{v(1-z)}{\lambda z^{k+1}-(\lambda+v)z+v}= P_{0}\frac{v}{v- k \lambda}
$$
che porta $P_0=1-\frac{k \lambda}{v}$ 

### Performance indices
l'utilizzazione della coda può essere espressa come $\rho = \frac{k \lambda S}{v}=k \lambda s$ , per cui l'espressione iniziale diventa $\mathcal{P}(z)= (1-\rho)\frac{v(1-z)}{\lambda z^{k+1}-(\lambda+v)z+v}$ 
prima di tentare di estrarre l'espressione per i clienti medi,  usiamo $P_j$ applicandogli la trasformata z per ottenere $\bar{N}_s$ 
$$
\bar{N}_{s}= \sum^{\infty}_{j=1}jP_{j}=\lim_{z \rightarrow 1}\sum^{\infty}_{j=1}jP_{j}z^{j-1}
$$
 fattorizziamo  $\mathcal{P}(z) = (1 - \rho)\frac{v(1-z)}{\lambda z^{k+1}-(\lambda + v)z+v}=(1-\rho)\frac{N(z)}{D(z)}$  dove: (notare denom e num)
  
$N(z)=v(1-z)$ e $D(z)=\lambda z^{k+1}-(\lambda+v)z+v$  otteniamo 
$$
\begin{align}
\lim_{z \rightarrow 1}N(z)=N(z)|_{z=1}= 0 && \lim_{z \rightarrow 1}D(z)=D(z)|_{z=1}=0
\end{align}
$$
da questo otteniamo 
$$
\bar{N}_{s}= \lim_{z \rightarrow 1}\frac{d}{dz}[(1-\rho)\frac{N(z)}{D(z)}]=(1-\rho)\lim_{z \rightarrow 1}\frac{N'(z)D(z)-N(z)D'(z)}{D(z)^{2}}
$$
a cui applichiamo ripetutamente la regola di de l'hopital
$$
\bar{N}_s=(1-\rho)\lim_{z \rightarrow 1}\frac{N'''(z)D(z)+N''(z)D'(z)-N'(z)D''(z)-N(z)D'''(z)}{2[D'(z)]^{2}+2D(z)D''(z)} 
$$  

ne segue che
$$
\begin{aligned}
N'(z)|_{z=1}= -v|_{z=1}= -v && D'(z)|_{z=1}=(k+1)\lambda z^{k}-(\lambda+v)|_{z=1}= k \lambda - v\\
N''(z)|_{z=1}=0   && D''(z)|_{z=1}=k(k+1) \lambda z^{k+1}|_{z=1}= k(k+1) \lambda 
\end{aligned}
$$ 
sostituendo nell'espressione di  $\bar{N}_{s}$ otteniamo 
>[!important]
>$$
\bar{N}_{s}= \frac{\rho}{(1-\rho)}\frac{k+1}{2}
$$


per ottenere la distribuzione del numero dei clienti in coda $P_j$ :
- compute the k+1 roots $(z_{0},z_{1},...,z_{k})$ of the denominator in $\mathcal{P}(z)$ as  $D(z)=v(1-z)(1-\frac{z}{z_1})(1-\frac{z}{z_{2}})...(1-\frac{z}{z_k})$ 
- semplifica $$\mathcal{P}(z)=\frac{1-\rho}{\prod^{i=1}_{k}(1-\frac{z}{z_i})}$$
- applichiamo la decomposizione parziale $\mathcal{P}(z)=(1-\rho)\sum^{k}_{i=1}\frac{A_i}{1-\frac{z}{z_i}}$  dove: 
    - $A_i=\prod^{k}_{h=1;h \neq i}\frac{1}{(1-\frac{z_i}{z_h})}$   
    -  usando l'antitrasformata
>[!important] 
>$$
 >   P_j=(1-\rho)\sum^{k}_{i=1}(z_{i})^{-j}A_{i}
>$$

sapendo che $P_0=(1-\rho)$ 

## Coda con batch variabili
una singola coda, in cui i clienti arrivano con batch la cui dimensione è una variabile aleatoria con distribuzione $g_i=Pr[Bs= i]$  dove:
- $Bs$ è la dimensione del batch .

i clienti sono serviti uno alla volta , la coda ha capienza infinita, la distribuzione dei tempi d'arrivo e di servizio è negativa esponenziale 

![[Pasted image 20231208185828.png]]
assumiamo $P_{j}=0$ le equazioni di bilanciamento diventano quindi
$$
\begin{align}
\lambda P_{0}= vP_{1} && (\lambda+v)P_{j}= \sum^{j-1}_{i=0}\lambda P_{i}g_{j-1} +v P_{j+1}
\end{align}
$$
direct solution difficult, need to use Z transform 

sia:
- $\mathcal{P}(z)=\sum^{\infty}_{j=0}P_{j}z^{j}$  la distribuzione dei clienti
- $\mathcal{G}(z)=\sum^{\infty}_{j=1}g_{j}z^{j}$ la trasformata z

moltiplichiamo entrambi i lati per $z^{j}$ , sommando su tutti i possibili valori di j, prestando attenzione alla prima equazione con  $P_0$ . 
Dall'equazione di bilanciamento otteniamo  
$$
(\lambda+v)\sum^{\infty}_{j=1}P_{j}z^{j}=\frac{v}{z}P_{j+1}z^{j+1}+\sum^{\infty}_{j=1}\sum^{j-1}_{i=0}P_{i}\lambda g_{j-i}z^{j}
$$
che può essere trasformato in 
$$
(\lambda +v) \sum^{\infty}_{j=1}P_{j}z^{j}= \frac{v}{z}P_{j+1}z^{j+1}+\lambda \sum^{\infty}_{i=0}P_{i}z^{i} \sum^{\infty}_{h=1}g_{h}z^{h}
$$
identifichiamo le trasformate z e otteniamo 
$$
(\lambda + v)[\mathcal{P}(z)-P_{0}]= \frac{v}{z}[\mathcal{P}(z) - P_{0}-P_{1}z]+\lambda \mathcal{P}(z)\mathcal{G}(z) 
$$
per cui $\mathcal{P}(z)=P_{0}\frac{v(1-z)}{v(1-z)- \lambda z[1-\mathcal{G}(z)]}$ per rimuovere $P_{0}$ è necessario usare la regola di le l'hopital sapendo che $\lim_{z \rightarrow 1}\mathcal{P}(z)=1$  per cui otteniamo 
$$
\begin{align}
P_0=1-\frac{\lambda \bar{g}}{v}=1 - \rho && \mathcal{P}(z)=(1-\rho)\frac{v(1-z)}{v(1-z)- \lambda z[1- \mathcal{G}(z)}
\end{align}
$$ 
### Indici di performance 
per calcolare il numero medio di clienti nel sistema 

sia:
- $\mathcal{P}(z)=(1-\rho)\frac{N(z)}{D(z)}$ dove:
$$
\begin{align}
N(z)=v(1-z) && D(z)=\lambda z G(z)-(\lambda+v) z + v
\end{align}
$$
allora
$$
\bar{N}_{s}=(1-\rho)\lim_{z \rightarrow 1} \frac{N'(z)D(z)-N(z)D'(z)}{[D(z)]^{2}}= \lim_{z \rightarrow 1} \frac{d}{dz}[(1-\rho)\frac{N(z)}{D(z)}=(1-\rho)\lim_{z \rightarrow 1} \frac{N'(z)D(z) - N(z)D'(z)}{[D(z)]^2}
$$  
di nuovo applicando ripetutamente la regola di de l'hopital
$$
 \bar{N}_s=(1-\rho)\lim_{z \rightarrow 1}\frac{N'''(z)D(z)+N''(z)D'(z)-N'(z)D''(z)-N(z)D'''(z)}{2[D'(z)]^{2}+2D(z)D''(z)} 
$$ 
il limite va calcolate usando la regola di de l'hopital $\bar{N}_{s}= (1- \rho)\lim_{z \rightarrow 1}\frac{-N'(z)D''(z)}{2[D'(z)]}$ osserviamo che 
$$
\begin{align}
N'(z) = -v|_{z=1}=-v && D'(z)|_{z=1}=\lambda G(z)+ \lambda G'(z)z-(\lambda+v)|_{z=1}=\lambda \bar{g}- v \\
N''(z)|_{z=1}=0 && D''(z)=2 \lambda G'(z)+ \lambda G''(z)z|_{z=1}= \lambda(\bar{g}+\bar{g^2})
\end{align}
$$
per cui $\bar{N}_{s}= \frac{\rho}{1-\rho}(\frac{1+ \bar{g}(CV^2[g]+1}{2})$  dove:
- $CV^2[g]=\frac{\bar{g^{2}-}(\bar{g})^2}{(\bar{g})^{2}}$

# Metodo degli stadi 
## M/$Er_k$/1 queue 
una variabile aleatoria è distribuita come una Erlang K se è la somma di più VA distribuite come negative esponenziali $k \micro$ .
PDF: $$
b_{X}(x)=\frac{k \micro(k \micro x)^{k-1}e^{-k\micro x}}{(k-1)!}
$$ 
- Media: $E[X]=\frac{1}{\micro}$ , 
- Varianza : $VAR[X]=\frac{1}{k}(\frac{1}{\micro^2})$ 
- Coefficiente di variazione : $CV^{2}[X]=\frac{VAR[X]}{(E[X])^2}=\frac{1}{k}$ 

non gode della proprietà di assenza di memoria , per cui non possiamo descriverne lo stato solo usando il numero di clienti . 
Possiamo però descriverne lo stato come coppia (n,s) dove:
- n rappresenta il numero di clienti nella stazione  
- $1 \leq s \leq k$ rappresenta lo stadio in cui la Erlang-K si trova

Siccome ogni stadio è distribuito come una negativa esponenziale abbiamo una catena di markov . Il futuro dipende solo dallo stato corrente ed è indipendente dalla storia del sistema.

![[Pasted image 20231209145233.png]]

sia:
- $\pi(n,s)$ => la probabilità di avere n clienti nella stazione di servizio .
- $P(n)=\sum^{k}_{s=1} \pi(n,s)$ => distribuzione marginale come probabilità che n clienti siano nella stazione di servizio al di là dello stadio corrente .
-  $\mathcal{P}(s)=\sum^{\infty}_{n=1}\pi(n,s)$ distribuzione marginale che lo stadio s sia usato per servire il cliente al di la del numero di clienti nella stazione  
per entrambe assumiamo  $P(0)=\mathcal{P}(0)= \pi(0,0)$. 

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

ridefiniamo lo stato del sistema come il numero di stadi da completare prima che la stazione di servizio si svuoti

se n clienti sono in stazione al tempo  t e quello in servizio è servito dall i-esimo allora il numero di stadi totali da completare è  
$$
j = (n-1)k + (k-i+1)= nk -i + 1
$$
ogni arrivo incrementa j di k  e le partenze decrementano di 1. il diagramma degli stati è ![[Pasted image 20231209182726.png]]
**esattamente come M/M/1 con batch di dimensione fissa .**

### Parametri di performance 
la probabilità di essere in uno stato è
$\phi=$ Pr{j stadi di servizio devono essere eseguiti per poter svuotare la coda}

 siamo interessati in
$$
P(n)= \sum^{nk}_{j=k(n-1)+1}\phi(j)= \sum^{k}_{j=1}\phi(k(n-1)+j) 
$$
che è la **probabilità che n clienti siano in stazione al di là dello stadio di servizio**.  Possiamo usare la trasformata z usata nel caso M/M/1 con batch fissi impostando:
- $v = k \micro$
che porta  $\rho = \frac{k \lambda}{k \micro}= \frac{\lambda}{\micro}$ e sapendo $\phi(0)= \pi(0,0) = (1-\rho)$

sia:
- $\bar{n}_s$ il numero medio di stadi completati 
- $\bar{n}$ il numero medio di clienti nella stazione 

$$
\bar{n}_{s}=\sum^{\infty}_{n=1}\sum^{kn}_{j=k(n-1)+1}j \phi(j)= \sum^{\infty}_{n=1}kn \sum^{k}_{I=1}\phi(k(n-1)+I)+\sum^{k}_{I=1}I \sum^{\infty}_{n=1}\phi(k(n-1)+I)
$$
sia:
- $P(n)=\sum^{k}_{I=1}\phi(k(n-1)+I)$  
- $\mathcal{P(i)}= \frac{(1-\mathcal{P}(0)}{k}=\frac{\rho}{k}$  

otteniamo: 
$$
\begin{aligned}
\bar{n}_{s}=k\bar{n}+ \frac{\rho}{2}(k+1)- k \rho \\
\bar{n}=\frac{1}{k}[\bar{n}_{s+}k \rho - \frac{\rho}{2}(k+1)]
\end{aligned}
$$ 

dal modello M/M/1 sappiamo che $\bar{n}_s=\frac{\rho}{1-\rho}\frac{k+1}{2}$ e sostituendo in  $\bar{n}$ otteniamo  
$$
\bar{n} = \frac{\rho}{1-\rho}[1+\frac{\rho}{2}(C^2_{s}-1)]
$$
anche chiamata formula di Pollaczeck
## M/Hk/1 queue 

ha pdf
$$
b_{X(x)=}\sum^{R}_{i=1}\alpha_{i}\micro_{i}e^{-u_{i}x}, x \geq 0
$$
i pesi hanno una condizione di normalizzazione 
$$
\sum^{R}_{i=1}\alpha_{i} = 1
$$

la media è   $E[X] =\sum^{R}_{i=1}\frac{\alpha_i}{\micro_i}$
la varianza è $VAR[X]=\sum^{R}_{i=1}\frac{\alpha_{i}}{\micro_{i}^2}$ 
con diagramma di transizione di stato 
![[Pasted image 20231209204809.png]]

può essere mostrato che 
$\bar{n}=\frac{\rho}{1-\rho}[1+\frac{\rho}{2}(C_{s}^2-1)]$ anche espresso come  $\bar{n}=\rho +\frac{\rho^2[C_{s}^2+1]}{2(1-\rho)}$ 
e anche come $\bar{n}=\rho +\frac{\rho^2+\lambda Var(S)}{2(1-\rho)}$  dove:
- Var(S) è la distribuzione della varianza dei tempi di servizio 

la stazione di servizio è
![[Pasted image 20231209204949.png]]
