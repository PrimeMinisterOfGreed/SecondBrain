I segnali , quando convertiti in valori discreti, possono essere analizzati sia nel dominio del tempo che in quello delle frequenze.
## Rappresentazione nel dominio del tempo
i segnali sono rappresentati da sequenze numeriche dette campioni, questi valori sono una qualche funzione nel tempo che rappresenta il segnale, ad esempio $x[n]$ ne rappresenta l'ampiezza. Il periodo di tempo tra un acquisizione e l'altra è detto **intervallo di campionamento** T, il cui reciproco è la **frequenza di campionamento** $F_{T}=\frac{1}{T}$  in Hz. Questa sequenza può essere composta da numeri interi, reali o complessi (a cui corrispondono sequenze intere, reali o complesse). Le complesse si possono scrivere come 

>[!definition] 
>$${x[n]}= {x_{Re}[n]}+j{x_{Im}[n]}$$ 

dove $x_{Re}$ è la sequenza della parte reale mentre $x_{Im}$ è la sequenza immaginaria.

## Lunghezza di una sequenza 
Una sequenza può essere finita $N_{1}\leq n\leq N_{2}$ o infinita $-\infty<n<+\infty$ . Una sequenza di lunghezza finita è spesso chiamata sequenza a N punti, si può passare da finito a infinito semplicemente mettendo a 0 tutti i valori fuori range rispetto alla sequenza finita. 

Ci sono 3 tipi di sequenza infinite:
- $x[n] =0 ;\forall n<N_{1}$ => sequenza destrorsa => **sequenza causale**
- $x[n]=0;\forall n>N_{2}$ => sequenza mancina => **sequenza anticausale** 
le sequenze finite nel dominio delle frequenze sono indicate con $x[k]$ per esempio 
>[!definition] sequenza finita
>Sia $x=[x[0],x[1],\dots,x[N-1]]$ una sequenza finita, allora la sua trasformata è $$X=[X[0],X[1],\dots,X[N-1]]^t$$
>ottenuta moltiplicando x per una matrice NxN $D:X=Dx$  per recuperare la sequenza originale è sufficiente $x=D^{-1}X$

## Potenza di un segnale discreto 
>[!definition] Norma
>Generalmente è data dalla sua norma $\mathcal{l}_{p}$ definita come $$| | x| |_{p} = \left( \sum^{\infty} |x[n]|^{p} \right)^\frac{1}{p}$$ 
>dove $p$ è un intero positivo (tipicamente 1,2,p)
>a $\infty$ la norma è $||x||_{\infty}=|x|_{max}$
>ne consegue che $\mid\mid x\mid\mid_{2}$ => è la media delle radici di ${x[n]}$ e 
>che $\frac{\mid\mid x\mid\mid_{1}}{N}$  => mean absolute value. 

Un applicazione della norma è stimare l'errore nella discretizzazione di un segnale partendo dalla sua forma continua. Una prima stima della qualità dell'approssimazione è il **Mean Square Error** $$MSE=\frac{1}{n}\sum^{N-1}_{i=0}()$$