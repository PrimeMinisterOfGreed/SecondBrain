eI segnali , quando convertiti in valori discreti, possono essere analizzati sia nel dominio del tempo che in quello delle frequenze.
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

Un applicazione della norma è stimare l'errore nella discretizzazione di un segnale partendo dalla sua forma continua. Una prima stima della qualità dell'approssimazione è il
>[!definition] **Mean Square Error** 
>$$MSE=\frac{1}{n}\sum^{N-1}_{i=0}(|y[n]-x[n]|)^2=\frac{1}{N}(\mid\mid y[n]-x[n]\mid\mid_{2})$$ 


un'altro approccio è 
>[!definition] **Errore relativo** 
> $$E_{rel}=^{!1} \frac{\mid\mid y[n]-x[n]\mid\mid_{2}}{\mid\mid x[n]\mid\mid_{2}}$$


## Operazioni sulle sequenze 
>[!definition] Prodotto  
> Siano $x[n]$ e $y[n]$ due sequenze. Il loro prodotto è una sequenza $w_{1}[n]=x[n]*y[n]$ 

%%metti un immagine modulatore qui %%  
In alcune applicazioni questo processo è noto come **modulazione** e il dispositivo che lo implementa è detto **modulatore**. La moltiplicazione per uno scalare invece $w_{2}[n]=Ax[n]$ è implementata da un **moltiplicatore**. 

>[!definition] Addizione
>$$w_{3}[n]=x[n]+y[n]$$

%%metti un immagine adder e moltiplicatore qua%%

il device che implementa questo processo è un **sommatore**. 

Un applicazione dell'operazione di somma è quella di migliorare la qualità della misura di un segnale disturbato da un rumore aleatorio sommato. 

>[!corollary] Ensemble average
Sia D il vettore di rumore aleatorio e $D_{i}$ un suo elemento, allora se S è il segnale $x_{i}=s_{i}+d_{i}$  il suo vettore di dati medio detto **Ensemble average** è  $$x_{ave}=\frac{1}{k}\sum^{k}_{i=1}(x_{i})=^{!1}s+\frac{1}{k}\left( \sum^{k}_{i=1}d_{i} \right)$$  

per un valore di k abbastanza grande , $x_{ave}$ è una replica ragionevole del segnale originale. Poichè la media del vettore dei rumori diventa sempre più piccola.  Una particolare applicazione di questo vettore è nella stima della potenza del rumore. 

>[!definition] Time shift 
>$$w_{H}[n]=x[n-N]$$ 
>- con $N<0$ si parla di avanzamento
>- con $N=1$ si parla di relazione input-output 

>[!definition] Avanzamento/ritardo unitario
>$$w_{h}[n]= x[n-1]$$ e $$w_{s}[n]=x[n+1]$$ scrivibile in termini della trasformata z come $$W_{H}(z)=z^{-1}X(z)$$ e $$W_{s}(z)=zX(z)$$

>[!definition] Inversione temporale 
> $$w[n]=x[-n]$$

## Combinazione di operazioni elementari 

in molti casi le operazioni semplici vengono combinate in circuiti più complessi. Un esempio è una sequenza generata da una combinazione pesata con i valori passati di un altra sequenza $$y[n]=b_{0}x[n]+b_{1}x[n-1]+b_{2}x[n-1]+a_{1}y[n-1]$$
Un'altra operazione è la 
>[!definition] Somma Convolutiva 
> Siano $x[n]$ e $h[n]$ due sequenze. Allora la loro somma convolutiva è $$y[n]=\sum^{\infty}_{k=-\infty}x[k]*h[n-k]$$ Scrivibile anche come $$y[n]=\sum^{\infty}_{k=-\infty}x[n-k]*h[k]$$

Per sintesi questa operazione si scrive come $y[n]=x[n] \oplus h[n]$. Se la lunghezza di $x[n]$ è N e $h[n]$ è M allora la **convoluzione** genera una sequenza lunga M+N-1

Se invece volessimo generare una sequenza con rateo modificato rispetto all'originale, bisogna ricorrere alla 
>[!definition] Alterazione del rateo di campionamento 
> Sia $x[n]$ una sequenza con rateo $F_{T}Hz$ usata per generare $y[x]$ che ha rateo $F_{T}'Hz$ allora il rateo di alterazione voluto è $$R=\frac{F_{T}'}{F_{T}}$$
> 

quando $R>1$ allora si ottiene una sequenza con frequenza più alta e il processo si chiama **sovracampionamento** , ed è implementato da un **interpolatore**. Viceversa se $R<0$ il processo si chiama **sottocampionamento** ed è implementato da un **decimatore**.  In sovracampionamento ogni $L-1 : L>1$ campioni equidistanti si inserisce un campione 0, otteniamo quindi una sequenza $$x[n]=\begin{cases}
x[nk]  \\ 0
\end{cases}$$
Viceversa nel sottocampionamento si tiene solo un campione ogni $M:M>1 \implies y[n]=x[nM]$ il cui rateo sarà quindi $\frac{1}{M}$ 

## Operazioni su sequenza finite 
Alcune operazioni precedentemente descritte, non sono applicabili su sequenze finite. Ad esempio l'inversione temporale e lo shifting escono dai confini della sequenza e anche la convoluzione genera sequenze di lunghezze non valide. Per ovviare a questo problema si usa può ricorrere spesso e volentieri al modulo.
>[!definition] Time Reversal circolare
> Sia $M=0\dots N-1$ una sequenza intera con $m \in M$ un generico elemento. Un operazione di modulo è $<m>_{mN}=m \mod{n}$, sia $r=<m>_{N}$ allora $r=m+lN$. Dove l è un intero scelto per soddisfare la relazione $0<m+lN<n-1$. Il time reversal circolare si scrive quindi $${y[n]}={x[<-n>_{N}]}$$


>[!definition] Shift Circolare 
> Questa operazione è definita come $x_{c}[n]=x[<n-n_0>_{N}]$ , con $n_{0}>0$ è uno shift circolare a destra, con $n_{0}<0$ è uno shift circolare a sinistra.

