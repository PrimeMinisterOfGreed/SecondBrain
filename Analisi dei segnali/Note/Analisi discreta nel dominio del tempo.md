i segnali , quando convertiti in valori discreti, possono essere analizzati sia nel dominio del tempo che in quello delle frequenze.
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
> $$ n_{0}>0 \implies x_{c}[n]= \begin{cases} x[n-n_{0}] \forall n_{0}\leq n \leq N-1 \\ x[N-n_{0}+m] \forall 0 \leq n_{m} \leq n_{0}
\end{cases}$$ 

Visto che $<-n>_{N}= N-m \forall 1 \leq n \leq N-1$ lo shifting circolare si può anche scrivere come $$x[<-n>_{N}]=  \begin{cases}
x[N-n]\forall_{1} \leq n \leq N-1 \\ x[n]= 0
\end{cases} $$

## Classificazione delle sequenze 
I segnali si possono classificare in base a varie caratteristiche ricorrenti.

### Classificazione in base alla simmetria 

>[!definition] Coniugato simmetrico 
> Una sequenza si chiama coniugato simmetrico se $x[n] = x^{*}[-n]$ , un coniugato simmetrico reale è chiamato **sequenza pari**. 
> Un coniugato antisimmetrico è $x[n]= -x^*[-n]$, un coniugato anti simmetrico reale è chiamato **sequenza dispari** 

Ogni sequenza complessa $x[n]$ può essere espressa come somma del suo coniugato antisimmetrico $x[n]= x_{cs}[n]+x_{ca}[n]$  dove: 
- $x_{cs}[n]= \frac{1}{2}(x[n]+x^*)[n]$
- $x_{ca}[n]= \frac{1}{2}(x[n]-x^*[-n])$ 

### Classificazione in base al periodo 

>[!definition] Sequenza periodica 
>Una sequenza $\tilde{x} [n]= \tilde{x}[n+kN];\forall n$ con periodo N

La tilde si usa per dire che questa sequenza è periodica. Il periodo fondamentale $Nf$ è il valore $\min(N)$ per cui l'equazione precedente si verifica. 
La somma di due sequenze periodiche è anch'essa periodica. 
>[!theorem] Somma di sequenze periodiche 
> siano $N_{a}$ e $N_{b}$  i periodi della sequenza $\tilde{x}_{a}[n]$ e $\tilde{x}_{b} \implies \tilde{y}[n]= \tilde{x}_{a}[n]+\tilde{x}_{b}[n]$  è una sequenza con periodo fondamentale $N=MCM(N_{a},N_{b})$ che è anche $$MCM(N_{a},N_{b})= \frac{N_{a}*N_{b}}{MCD(N_{a},N_{b})}$$


### Classificazione in base a energia e potenza 
>[!definition] energia totale di un segnale 
>$x[n]$ è $$\mathit{e}_{x}= \sum^{+\infty}_{-\infty}|x[n]|^2$$ A seconda che la somma converga o meno il segnale potrebbe o no avere energia infinita. 

>[!definition] Potenza media 
>$$P_{x}= \lim_{ k \to \infty } \frac{1}{2k+1}\sum^{k}_{n=-k}|x[n]|^{2}\implies \lim_{ k \to \infty } \frac{1}{2k+1}\mathit{e}_{x}$$ 

## Sequenze tipiche e rappresentazioni 
### Sequenze sinusoidali 

>[!definition] Sinusoide Reale 
>  $x[n]=A-\cos(w_{0}*n+\phi);n<\infty$ dove: 
>- $A$ =>ampiezza 
>- $w_{0}$=>frequenza angolare normalizzata 
>- $\phi$=> fase 

tutte costanti $\in \mathbb{R}$ . Alternativamente questa sinusoide si può scrivere come $x[n]=x_{i}[n]+x_{q}[n]$ 
dove:
- $x_{i}[n]$ => in phase 
- $x_{q}[n]$=> componente di quadratura 
dati da $$\begin{align}
x_{i}[n]= A*\cos \phi \cos(w_{0}n) \\ x_{q}[n]=-A\sin \phi*\sin(w_{0n})
\end{align}
$$
negli esempi sopra $A\cos \phi$ e $A\sin \phi$ sono sequenze esponenziali, e la loro forma più generica è $x[n]=A\alpha^{n}$ riscrivendo $\alpha=e^{ (\sigma_{0}+j\omega_{0}) }$ e $A=|A|e^{ j\phi }$ la sequenza diventa 
$$
x[n]=Ae^{ (\sigma_{0}+j\omega_{0})n }=|A|e^{ \sigma_{0} n}\cos(\omega_{0}n+\phi)+j|A|e^{ \sigma_{0}n }\sin(\omega_{0}n+\phi)
$$


Con $A,\alpha \in \mathbb{R}$ la sequenza si riduce a una sequenza reale esponenziale. Con $|\alpha|<1$ decade e con $|\alpha|>1$ Cresce. Notare che la precedente sinusoide reale e la complessa con $\sigma_{0}=0$ sono sequenze periodiche con periodo N finchè 
>[!definition] Periodo fondamenetale 
>$w_{0}N=2\pi r$ dove N e r sono $\mathbb{I}>0$. Il $\min(N)$ che soddisfa questa condizione è il periodo fondamentale della sequenza. 
>Siano $$
>\begin{align}
x_{1}[n]= \cos(w_{0}n+\phi), x_{2}[n]=\cos(w_{0}(n+N)+\phi) \implies\\ x_{2}^*[n]=\cos(w_{0}n+\phi)*\cos w_{0}N-\sin(w_{0}n+\phi)\sin w_{0}N\implies\\ \cos(w_{0}n + \phi)=x_{1}[n] \leftrightarrow w_{0}N=2\pi
\end{align}$$

#### Proprietà di sequenze sinusoidali 
Si considerino due sequenze esponenziali complesse $x_{1}[n]=e^{jw_{1}n}$ e $x_{2}[n]=e^{jw_{2}n}$ con $0 \leq \omega_{1} \leq 2\pi$ e $2 \pi k \leq \omega _2\leq 2\pi(k+1)$  
>[!definition] Proprietà 1
> Se $$\omega _2=\omega_{1}+2\pi k \implies x_{2}[n]=e^{j\omega_{2}n}=e^{j(\omega_{1}+2\pi k)n}= e^{j\omega_{1}n}=x_{1}[n]$$ le due sequenze sono quindi indistinguibili. In altre parole una sequenza sinusoidale con frequenza angolare normalizzata $\omega_{2}$ che è fuori dall'intervallo $0\leq \omega \leq 2\pi$ , allora questa sequenza è equivalente a un altra sinusoidale con frequenza normalizzata $\omega_{2} \bmod 2\pi$

 
La second proprietà segue questa precedente
>[!definition] Proprietà 2
>siano $$x_{1}[n]=\cos(\omega_{1}n),x_{2}[n]= \cos(\omega_{2}n)$$ con $0\leq \omega_{1}<\pi$ e $\pi \leq \omega_{2}<2\pi$  Allora se $$\omega_{2}=2\pi-\omega_{1} \implies x_{2}[n]=\cos(2\pi n-\omega_{1}n)=\cos(\omega_{1}n)=x_{1}[n]$$
>che di nuovo rende le 2 sequenze indistinguibili

Così una sinusoidale con frequenza angolare normalizzata $\omega_{2}$ nel range $\pi \leq \omega_{2}<2\pi$ assume l'identità di una sinusoidale con frequenza $\omega_{1}=2\pi-\omega_{2}$ nel range $0\leq \omega_{1}<\pi$. La frequenza $\pi$ diventa così nota come **frequenza di piegamento**.  


## Sequenza finestra rettangolare
la **sequenza a finestra rettangolare** anche chiamata box-car è una sequenza del tipo 
>[!definition] Sequenza rettangolare
>$$w_{R}[n]=\begin{cases} 0,& n<N_{1}\\ 
> 1, & N_{1}\leq n \leq N_{2} \\
> 0, & n > N_{2}
\end{cases}$$

un applicazione di questa sequenza è quella di estrarre dati da un altra sequenza in una specifica partizione $N_{1} \leq n \leq N_{2}$ di una sequenza infinita o molto grande. 

$$x[n]*w_{R}[n]=\begin{cases}
0, & n<N_{1}\\ 
x[n],& N_{1}\leq n\leq N_{2},  \\
0, & n>N_{2}
\end{cases}$$
## Generazione di sequenze con forme d'onda complesse

Le [operazioni descritte precedentemente](#Operazioni sulle sequenze)  possono essere combinate per formare sequenze con forme d'onda più complesse. 
>[!example] Generazione di una quadra 
> $$\begin{align} 
> x_{1}[n]=\sin(0.05\pi n)u[n] \\ 
> x_{2}[n]=\sin(0.15\pi n)u[n] \\ 
> x_{3}[n]=\sin(0.25\pi n)u[n]
\end{align}
> $$

una nuova sequenza può essere formata sommando $y[n]=x_{1}[n]+\frac{1}{3}x_{2}[n]+\frac{1}{5}x_{3}[n]$ 



### Componenti fondamentali e armoniche 
Una sinusoidale può essere composta da più forme d'onda che hanno una frequenza angolare che sono multipli tra di loro. La frequenza minima in quest'onda è chiamata **frequenza fondamentale o componente fondamentale** mentre i suoi multipli di ordine k sono **k-esima armonica** (o più genericamente armoniche). Ogni onda periodica è rappresentabile tramite somme pesate delle sue componenti, quest'operazione si chiama **espansione in serie di Fourier** , i cui pesi sono chiamati coefficienti della serie. 

### Rappresentazione di una sequenza arbitraria
è possibile rappresentare una sequenza nel dominio del tempo usando combinazioni di sequenze ritardate/anticipate, di solito si usa la sequenza unitaria per eseguire questa operazione. Ad esempio si può esprimere come 
$$x[n]=0.5\updelta[n+2]+1.5\updelta[n-1]-\updelta[n-2]+\updelta[n-4]+0.75\updelta[n-6]$$

## Il processo di campionamento 
è un processo che prende un segnale continuo $x_{a}(t)$ e lo converte in una sequenza discreta, mettendo in relazione la variabile continua t e l'indice della sequenza n 
$$
t_{n}=nT=\frac{n}{F_{T}}=\frac{2\pi n}{\Omega_{T}}
$$
dove:
- $F_{T}$=> è la frequenza di campionamento 
- $\Omega_{T}=2\pi F_{T}$ => frequenza angolare di campionamento. 

Per esempio se il segnale continuo $x_{a}(t)=A\cos(2\pi f_{0}t+\phi)=A \cos(\Omega_{0}t+\phi)$ viene convertito in discreto $x[n]=A\cos(\Omega_{0}nT+\phi)=A\cos(\omega _{0}n+\phi)$ 
%%ci sono dei passaggi intermedi qui%%
dove:
- $\omega_{0}=\frac{2\pi \Omega_{0}}{\Omega_{T}}=\Omega_{0}T$ => frequenza angolare normalizzata del segnale discreto x, che ha unità **radianti per campione**, mentre l'unità della frequenza angolare nel continuo è **radianti al secondo** 

In generale a una certa frequenza è possibile campionare una certa varietà di sinuosoidi le cui frequenze angolari sono multiple tra di loro, rendendo quindi impossibile discriminare una sequenza da un'altra. Questo fenomeno è in generale noto come **aliasing**. (Un esempio è prendere 3 segnali con sequenze multiple, convertirle in un segnale discreto e mostrare che sono equivalenti se campionate a una certa frequenza {3hz,7hz,13hz} e {10hz camp}).

Nel caso generale , la famiglia di sinusoidi continue $$
x_{a,k}(t)= A \cos(\pm(\Omega_{0}t+\phi)+k\Omega_{T}t);k=0,\pm 1,\pm 2\dots
$$
Portano allo stesso identico segnale campionato 
$$
x_{a,k}(nT)= A\cos((\Omega_{0}+k\Omega_{T})nT+\phi)=^{!2}A \cos(\omega_{0}n+\phi)=x[n]
$$

## Correlazione dei segnali 
è una misura di similarità tra segnali, usata quando abbiamo necessità di confrontare due segnali. Utile per esempio per capire nel caso delle comunicazioni se è avvenuta la trasmissione di un certo segnale, oppure nei radar per determinare l'oggetto rilevato. s

### Definizioni 

>[!important] Cross Correlazione
> è una misura di similarità tra **l'energia** di due segnali, definita come $r_{xy}[l]$ 
> $$
> r_{xy}[l]=\sum_{n=-\infty}^\infty x[n]y[n-l]
>$$ 
>questa somma infinita converge 

dove: 
- $l$ => indica il time-shift tra i campioni, parametro chiamato **lag** 

l'ordine di xy nella funzione indica che la sequenza $x[n]$ è la sequenza di riferimento che rimane fissa nel tempo mentre $y[n]$ è shiftata rispetto a x. Se vogliamo invece usare y come sequenza di riferimento, si può invertire il tutto facendo 
$$
r_{yx}[l]=\sum_{n=-\infty}^{\infty} y[n]x[n-l]=\sum_{n=-\infty}^{\infty}y[m+l]x[m]=r_{xy}[-l] 
$$
per cui basta invertire la sequenza originale.

>[!important] Autocorrelazione 
>l'autocorrelazione è data da $$r_{xx}[l]=\sum_{n=-\infty}^{\infty}x[n]x[n-l]$$ 

per cui $r_{xx}[l]=r_{xx}[-l]$. Esaminando l'equazione si può intravedere che la cross correlazione è abbastanza simile alla convoluzione , infatti su può riscrivere come 
$r_{xy}[l]=\sum_{n=-\infty}^{\infty} x[n]y[-(l-n)]=x[l] \circledast y[-l]$

### Proprietà dell'autocorrelazione e della cross correlazione 
Siano $x[n]$ e $y[n]$ due sequenze a energia finita. **L'energia delle sequenze combinate $ax[n]+y[n-l]$ anche è finita** , per cui 
$$
\sum_{n=-\infty}^{\infty}(ax[n]+y[n-l])^2=^{!1}a^2r_{xx}[0]+2ar_{xy}[l]+r_{yy}[0]\geq 0
$$
dove:
- $r_{xx}[0]=\mathcal{E}_{x}>0$ e $r_{yy}[0]=\mathcal{E}_{x}>0$  sono le energie delle sequenze x e y. 
Possiamo riscrivere le precedenti equazioni in forma matriciale 
$$
\begin{bmatrix}
a & 1
\end{bmatrix}* \begin{bmatrix}
r_{xx}[0] & r_{xy}[l]\\ \\
r_{xy}[l] & r_{yy}[0]
\end{bmatrix}
\begin{bmatrix}
a  \\
1
\end{bmatrix} \geq 0
$$
la matrice centrale è positvamente semi definita per ogni a positivo. Che implica 
$r_{xx}[0]r_{yy}[0]-r^2_{xy}[l]\geq 0$ o equivalentemente $|r_{xy}[l]|\leq \sqrt{ r_{xx}[0]r_{yy}[0] }=\sqrt{ \mathcal{E_{x}}\mathcal{E_{y}} }$ . Questa diseguaglianza porta a un 
>[!important] **limite superiore**
> per la cross correlazione $$|r_{xx}[l]|\leq r_{xx}[0]=\mathcal{E_{x}}$$ 

che ci dice che con lag $l=0$ , **l'autocorrelazione assume il suo valore massimo**. 

considerando una sequenza del tipo $y[n]=\pm bx[n-N]$ possiamo derivare una seconda proprietà considerando N intero e b>0 $\sqrt{ \mathcal{E_{x}\mathcal{E_{y}}} }=\sqrt{ b^2\mathcal{E_{x}}^2 }=b^2\mathcal{E_{x}}$  per cui 
$$
-br_{xx}[0]\leq r_{xy}[l]\leq br_{xx}[0]
$$
### Correlazione per sequenze periodiche
nel caso di sequenze periodiche queste misure sono definite in modo leggermente differente. Per una coppia di segnali x e y 
>[!important]  Cross correlazione 
>$$r_{xy}[l]=\lim_{ K \to \infty } \frac{1}{2K+1}\sum_{n=-K}^{K}x[n]y[n-l]$$

>[!important] Auto correlazione 
>$$r_{xx}[l]=\lim_{ K \to \infty } \frac{1}{2K+1}\sum_{n=-K}^{K}x[n]x[n-l]$$ 

entrambe le sequenze generate rxy e rxx sono anch'esse periodiche, questa proprietà può essere usata per recuperare la periodicità di un segnale che subisce un interruzione improvvisa. 

sia:
- $\tilde{x}[n]$ =>sequenza x interrotta da un segnale di disturbo 
- $d[i]$=> sequenza di disturbo 

il segnale risultante sarà $w[n]=\tilde{x}[n]+d[n]$, che è osservato in $0\leq n\leq M-1$ con $M\gg N$ 
l'autocorrelazione di $w[n]$ è data da 
$$
r_{ww}[l]=\frac{1}{M}\sum_{n=0}^{M-1} w[n]w[n-l]=^{!2}r_{\tilde{x}\tilde{x}}[l]+r_{dd}[l]+r_{\tilde{x}d}[l]+r_{d\tilde{x}}[l] 
$$
per cui rxx è una sequenza periodica con periodo N, per cui avrà picchi a $l=0,N,2\mathbf{N}\dots$ con la stessa ampiezza allorchè $l$ tende a M. Siccome $\tilde{x}[n]$ e $d[n]$ non sono correlati, ci aspettiamo che le loro cross correlazioni siano molto piccole. L'autocorrelazione del segnale di disturbo d mostrerà un picco a l=0 per cui i picchi di $r_{ww}[l]$ con l>0 possono essere usati per ricostruire la periodicità del segnale originale. 