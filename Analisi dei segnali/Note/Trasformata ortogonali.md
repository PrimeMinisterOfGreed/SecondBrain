Spesso nella pratica è conveniente mappare una sequenza finita dal dominio del tempo in un altro dominio e vice versa. Questa tipologia di funzioni è chiamata trasformazioni di lunghezza finita. In particolare in questo caso si parla delle classi di **trasformate ortogonali** : **trasformata di Fourier discreta** , **Trasformata coseno** e **Haar trasform**. 

## Trasformate ortogonali
sia $x[n]$ una sequenza finita nel dominio del tempo con $\mathscr{X}[k]$ che denota i coefficienti della sua trasformata a N punti. Allora una forma generica della coppia di trasformate ortogonali è nella forma 
$$
\begin{align}
\symscr{X}[k]= \sum_{n=0}^{N-1}x[n]\psi ^{*}[k,n] ;0\leq k\leq N-1\\
x[n]=\frac{1}{N} \sum_{k=0}^{N-1} \symscr{X}[k]\psi[k,n] 0\leq n\leq N-1
\end{align}
$$

la prima equazione si chiama **equazione analitica** mentre la seconda è **equazione di sintesi**. $\psi[k,n]$ sono le **sequenze basi** che hanno lunghezza N in entrambi i domini. Che normalmente soddisfa la condizione 
$$
\frac{1}{N} \sum_{n=0}^{N-1}\psi[k,n]\psi ^{*}[l,n]=\begin{cases}
1, & l=k  \\
0, & l\neq k
\end{cases}
$$
Le sequenze base che soddisfano questa condizione sono dette ortogonali.  Un importante proprietà dell'ortogonalità è la **conservazione dell'energia** che permette di calcolare $\sum_{n=0}^{N-1}|x[n]|^{2}$ della sequenza nel dominio del tempo.Per dimostrare questa proprietà osserviamo 
$$
\begin{align}
\sum_{n=0}^{N-1}|x[n]|^{2}=\sum_{n=0}^{N-1}x[n]x^{*}[n]=\sum_{n=0}^{N-1} \left(  \frac{1}{N}   \sum_{k=0}^{N-1}\symscr{X}[k] \psi[k,n] \right) x^{*}[n]=\frac{1}{N} \sum_{k=0}^{N-1}\symscr{X}[k]\symscr{X}^{*}[k]=\\\frac{1}{N} \sum_{k=0}^{N-1}|\symscr{X}[k]|^{2}
\end{align}
$$
nota anche come **relazione di Parseval**. 


## La trasformata di Fourier discreta 

### Definizioni 
la DFT di lunghezza N di una sequenza $x[n]$ nel dominio del tempo è definita come 
$$
X[k]=\sum_{n=0}^{N-1}x[n]e^{ -j 2 \pi kn/N }
$$
 ottenuta impostando la sequenza base come $\psi[k,n]=e^{ j 2 \pi kn/N }$ che è una sequenza complessa. Per mostrare che questa sequenza è ortogonale osserviamo che 
 $$
 \frac{1}{N}\sum_{n=0}^{N-1} e^{\frac{ j 2 \pi kn}{N}} e^{ \frac{-j 2 \pi l n}{N}}  = \frac{1}{N} \sum_{n=0}^{N-1}e^\frac{ j 2 \pi(k-l)n}{N } 
$$
impostando $u=e^{ j 2 \pi(k-l)/N }$ otteniamo una somma finita nella forma 
$$S_{N-1}=\sum_{n=0}^{N-1}u^{n}\implies \sum_{n=0}^{N}u^{N}=1+u\sum_{n=0}^{N-1}u^{n}=1+uS_{N-1}=S_{N-1}+u^{N}\implies S_{N-1}= \frac{1-u^{N}}{1-u}$$ risostituiamo e otteniamo 
$$
\sum_{n=0}^{N-1} e^{ \frac{j 2 \pi(k-l) n}{N}}=\frac{1-e^{ j 2 \pi(k-l) }}{1- e^{ \frac{j 2 \pi(k-l)}{N} }} \implies \frac{1}{N}\sum_{n=0}^{N-1}e^{ \frac{j_{2} \pi (k-l)n}{N} }
=\begin{cases}
1 & k=l+rN \\
0 & k\neq l
\end{cases}$$

Ci si riferisce alla DFT di lunghezza N come una **DFT a N-punti** usando la notazione $W_{N}=e^{ -j 2 \pi /N }$ quindi possiamo scrivere trasformata e antitrasformata come 
$$
\begin{align}
X[k]=\sum_{n=0}^{N-1}x[n]W_{N}^{kn} \\
x[n]=\frac{1}{N} \sum_{k=0}^{N-1}X[k]W_{N}^{-kn}
\end{align}
$$
### Complessità computazionale 
come si può vedere dalle equazioni il calcolo della DFT e della IDFT ha complessità $N^{2}$ moltiplicazioni complesse e N(N-1) addizioni complesse. Per ridurre la complessità di quest'operazione sono stati studiati dei metodi come la FFT che abbassa la complessità a $N(\log_{2}N)$ . 

### Relazioni matriciali 
La DFT può essere espressa in forma matriciale in forma $X=D_{N}x$ dove X è il vettore composto dagli N campioni della DFT $X=[X[0] X[1]\dots X[N-1]]^{t}$ mentre x è il vettore in input $x=[x[0]x[1]\dots x[N-1]]^{t}$ e $D_{N}$ una matrice NxN di DFT data da 
$$
D_{N}=\begin{bmatrix}
1 & 1 & 1 & \dots & 1 \\
1 & W_{N}^{1} & W_{N}^{2} & \dots & W_{N}^{N-1} \\
1 & W_{N}^{2} & W_{N}^{4} & \dots & W_{N}^{2(N-1)} \\
\vdots & \vdots & \vdots & \diagdown & \vdots \\
1 & W_{N}^{N-1}  & W_{N}^{2(N-1)} & \dots &  W_{N}^{(N-1)(N-1)}
\end{bmatrix}
$$
le IDFT si possono esprimere invece come 
$$\begin{bmatrix}x[0] \\ x[1] \\ \dots \\x[N-1]
\end{bmatrix}=D_{N}^{-1}\begin{bmatrix} X[0]\\X[1]\\\dots\\X[N-1] \end{bmatrix}$$
dove $D_{N}^{-1}$ è la matrice IDFT data da 
$$D_{N}^{-1}=\frac{1}{N} \begin{bmatrix}
1 & 1 & 1 & \dots & 1 \\
1 & W_{N}^{-1} & W_{N}^{-2} & \dots & W_{N}^{-N-1} \\
1 & W_{N}^{-2} & W_{N}^{-4} & \dots & W_{N}^{-2(N-1)} \\
\vdots & \vdots & \vdots & \diagdown & \vdots \\
1 & W_{N}^{-N-1}  & W_{N}^{-2(N-1)} & \dots &  W_{N}^{-(N-1)(N-1)}
\end{bmatrix}$$

ne Segue che $D_{N}^{-1}=\frac{1}{N}D^{*}_{N}$

## Relazioni tra la Trasformata di Fourier la DFT e le sue inverse 
esaminiamo la relazione che esiste tra la DFT a N punti e la trasformata di Fourier di una sequenza di lunghezza M.

#### Relazione con la DTFT 
La DTFT di una sequenza a N punti è $$
X(e^{ j\omega })=\sum_{n=-\infty}^{\infty}x[n]e^{ -j\omega n }=\sum_{n=0}^{N-1}x[n]e^{ -j\omega n }
$$
**campionando uniformemente** X a N frequenze equamente spaziate $\omega_{k}=\frac{2\pi k}{N}$ otteniamo la seguente equazione 
$$X(e^{ j\omega })|_{\omega=\frac{2\pi k}{N}}=\sum_{n=0}^{N-1}x[n]e^{ -j_{2} \pi k/N }$$
A causa della relazione esplicita tra i campioni della DFT e le frequenze dei campioni della trasformata di Fourier, la frequenza normalizzata associata all'indice k del campione della DFT $X[k]$ è $\frac{2\pi k}{N}$ radianti. Per esempio con N=32 il campione di indice 11 rappresenta la frequenza normalizzata $\omega=\frac{11\pi}{16}$

### Trasformata di Fourier dalla DFT con interpolazione 
Data una trasformata a N punti si può determinare la sua DTFT unicamente interpolando $X[k]$ su tutti i valori di $\omega$. Usando l'espressione per la IDFT otteniamo 
$$
X(e^{ j\omega })=\frac{1}{N} \sum_{n=0}^{N-1}\left[ \sum_{k=0}^{N-1}X[k]W_{N}^{-kn} \right]e^{ -j\omega n }=\frac{1}{N}\sum_{k=0}^{N-1}X[k]\sum_{n=0}^{N-1}e^{ j 2 \pi k n/N }e^{ -j\omega n }
$$
possiamo riscrivere la sommatoria più a destra come 
$$
\sum_{n=0}^{N-1}e^{ -j \left( \frac{\omega- 2\pi k}{N} \right)n }= \frac{1-e^{ -j (\omega N - 2\pi k)}}{1-e^{ -j \frac{\omega-((2 \pi k)}{N}  }} =^{!2} \frac{\sin\left( \frac{\omega N-2\pi k}{2} \right)}{\sin\left( \frac{\omega N-2\pi k}{2N} \right) }e^{ -j[\omega-\frac{(2 \pi k)}{N}][(N-1)/2] }
$$
quindi sostituendo 
$$
X(e^{ j\omega })=\frac{1}{N}X[k]\frac{\sin\left( \frac{\omega N-2\pi k}{2} \right)}{\sin\left( \frac{\omega N-2\pi k}{2N} \right) }e^{ -j\left[ \omega-\frac{(2 \pi k)}{N} \right]\left[ \frac{(N-1)}{(2)} \right]}= \sum_{k=0}^{N-1}X[k]\Phi\left( \omega - \frac{2 \pi k }{N} \right)
$$

dove $\Phi(\omega)= \sin \frac{\left( \frac{\omega N}{2} \right)}{N \sin \left( \frac{\omega}{2} \right)} e^{ -j \omega[(N-1)/2] }$
l'equazione è sostanzialmente la relazione voluto con la trasformata di Fourier. Si può facilmente mostrare che $X(e^{ j\omega w })|_{\omega=2\pi l}=x[l]$ per cui possiamo ottenere la trasformata X tramite interpolazione. 

### Campionare la trasformata 
Sia $x[n]$ una sequenza con trasformata $X(e^{ j\omega })$ . Campioniamo $X(e^{ j\omega })$ a N punti equamente spaziati $\omega_{k}=\frac{2\pi k}{N}$ sviluppando i campioni in frequenza $X(e^{ j\omega_{k} })$ . Questi N campioni sono considerabili come una DFT a N punti $Y[k]$ i cui campioni inversi di DFT sono una sequenza di lunghezza N $y[n]$. Per cui 
$$
Y[k]=X(e^{ j\omega_{k} }) = X\left( e^{ j\frac{2 \pi k}{N}} \right)=\sum_{l=-\infty}^{\infty}x[l]W_{N}^{kl}
$$
Una inversa a N punti porta 
$$y[n]=\frac{1}{N}\sum_{k=0}^{N-1} Y[k]W_{N}^{-kn}=\frac{1}{N} \sum_{k=0}^{N-1} \sum_{l=-\infty}^{\infty}x[l]W_{N}^{kl}W_{N}^{-kn}=\sum_{l=-\infty}^{\infty}x[l]\left[ \frac{1}{N} \sum_{k=0}^{N-1}W_{N}^{-k(n-l)} \right]$$
sapendo che $\frac{1}{N}\sum_{k=0}^{N-1}W_{N}^{-k(n-l)}=\begin{cases}1& l=n+mN\\0\end{cases}$ allora otteniamo la relazione 
$$
y[n]=\sum_{m=-\infty}^{\infty}x[n+mN]
$$
che indica che y è ottenuta da x aggiungendo infinite repliche shiftate di x, ognuna di un intero multiplo di N momenti di campionamento. Questa relazione può essere usata per mostrare gli effetti del campionamento sulla trasformata.

## Convoluzione circolare 
Questa operazione è analoga alla convoluzione lineare ma con una sottile differenza 
Siano $g[n]$ e $h[n]$ due sequenze di lunghezza finita N. La loro convoluzione lineare è 
$$
y_{L}[n]=\sum_{m=0}^{N-1}g[m]h[n-m];0\leq n\leq 2N-2
$$
### Definizioni 
Per sviluppare quest'operazione dobbiamo prima applicare un operazione di inversione circolare alla sequenza e poi un time-shift. L'operazione risultante, chiamata **convoluzione circolare** diventa 
$$
y_{C}[n]=\sum_{m=0}^{N-1}g[m]h[<n-m>_{N}]
$$
di solito ci si riferisce ad essa come convoluzione circolare a N punti, denotata da 
$$
y_{C}[n]=g[n] \circledast_{n} h[n]\
$$
Esattamente come la convoluzione normale gode delle proprietà commutative e associative.  Può essere scritta in forma matriciale come. 
$$
\begin{bmatrix}
y_{C}[0] \\ y_{C}[1] \\ y_{C}[2] \\ \vdots \\ y_{C}[N-1]
\end{bmatrix}=
\begin{bmatrix}
h[0] & h[N-1] & h[N-2] & \dots & h[1] \\
h[1] & h[0]  &  h[N-1]  &  \dots  & h[2] \\
h[2]  & h[1] & h[0]  & \dots  & h[3] \\
\vdots & \vdots & \vdots  & \vdots &  \vdots \\
h[N-1] & h[N-2]  & h[N-3] & \dots & h[0]
\end{bmatrix}
\begin{bmatrix}
g[0] \\ g[1] \\ g[2] \\ \vdots \\ g[N-1]
\end{bmatrix}
$$
Questa convoluzione può anche essere valutata usando una forma alternativa del metodo tabulare. 

## Classificazione di sequenze lineari finite 
La proprietà di simmetria sviluppata per le sequenze infinite non si applica in questo contesto.  La definizione in questo è data in modo che le parti simmetriche e antisimmetriche della sequenza di lunghezza N siano anche'esse di lunghezza N e definite per lo stesso range di valori dell'indice di tempo n. 

### Classificazione in base al coniugato simmetrico 
Una delle definizioni di simmetria è data usando l'operazione modulo 
$$
x[n]=x_{cs}[n]+x_{ca}[n]
$$
dove :
- $x_{cs}[n]=\frac{1}{2}(x[n]+x^{*}[<-n>_{N}])$ => **coniugato simmetrico circolare** 
- $x_{ca}[n]= \frac{1}{2}(x[n]-x^{*}[<-n>_{N}])$ => **coniugato antisimmetrico circolare** 

per una sequenza reale $x[n]$ , il coniugato simmetrico è una sequenza reale chiamata **parte circolare pari** definita da $x_{ev}[n]$. Il coniugato antisimmetrico invece si chiama **parte circolare dispari** e si definisce $x_{od}[n]$ 

### Classificazione basate su simmetrie geometriche 
2 importanti tipi di simmetrie geometriche sono definite: simmetriche e antisimmetriche. Una sequenza simmetrica
- soddisfa la condizione $x[n]= x[N-1-n]$
- mentre una sequenza anti simmetrica $x[n]=-x[N-1-n]$

Si può considerare anche se la sequenza è pari o dispari, quindi le tipologie possibili diventano 4. 

1) Sequenze simmetriche con lunghezza dispari: (es. lunghezza 9)
La trasformata di Fourier per questo tipo di sequenze è nella forma 
$$
X(e^{ j\omega })=e^{ \frac{-j(N-1)\omega}{2} }\left\{ x \left[ \frac{N-1}{2} \right] +2 \sum_{n=1}^{\frac{(N-1)}{2}}x\left[ \frac{N-1}{2}-n \right] \cos(\omega n) \right\}
$$
con la funzione di fase data da $\theta(\omega)=-\left( \frac{N-1}{2} \right)\omega+\beta$ con $\beta=0 \lor \beta=\pi$
La DFT a N punti può essere derivata campionando uniformemente la sua trasformata con una frequenza angolare $\omega=\frac{2\pi k}{N}$ 
$$
X[k]=e^\frac{ (-j(N-1)\pi k)}{N }\left\{  x\left[ \frac{N-1}{2} \right]+2 \sum_{n=1}^{\frac{(N-1)}{2}}x\left[ \frac{N-1}{2}-n \right]  \cos\left( \frac{2 \pi k n}{N} \right) \right\}
$$

2) Sequenze simmetriche con lunghezza pari 
Trasformata di Fourier 
$$
X(e^{ j\omega })=e^{ \frac{-j(N-1)\omega}{2 }}\left\{  2 \sum_{n=1}^{\frac{N}{2}x\left[ \frac{N}{2} -n \right]} x\left[ \frac{N}{2}-n \right] \cos\left( \omega\left( n-\frac{1}{2} \right) \right) \right\}
$$
$\theta(\omega)=-\left( \frac{N-1}{2} \right)\omega+\beta$
DFT 
$$
X[k]=e^\frac{ -j(N-1)\pi k }{N }\left\{ 2 \sum_{n=1}^{\frac{N}{2}} x\left[ \frac{N}{2} -n \right] \cos\left( \frac{\pi k(2n-1)}{N} \right)  \right\}
$$

3) Antisimmetrica con lunghezza dispari 

Trasformata 
$$
X(e^{ j\omega })=je^{ \frac{-j(N-1)\omega}{2 }}\left\{  2 \sum_{n=1}^{\frac{N-1}{2}}x\left[ \frac{N-1}{2} -n \right]\sin(\omega n) \right\}
$$

con funzione di fase $\theta(\omega)=-\frac{N-1}{2}\omega+\frac{\pi}{2}+\beta$

DFT
$$
X[k]=je^\frac{ -j(N-1)\pi k}{N }\left\{ 2 \sum_{n=1}^{\frac{(N-1)}{2}} x\left[ \frac{N-1}{2} -n \right]\sin\left( \frac{2\pi kn}{N} \right)  \right\}
$$


4) Antisimmetrica con lunghezza pari

Trasformata 
$$
X(e^{ j\omega })=je^{ \frac{-j(N-1)\omega}{2} } \left\{  2 \sum_{n=1}^{\frac{N}{2}x}x\left[ \frac{N}{2}-n \right]\sin\left( \omega\left( n-\frac{1}{2} \right) \right) \right\}
$$
DFT 
$$
X[k]= je^{\frac{ -j(N-1)\pi k}{N }}\left\{  2 \sum_{n=1}^{\frac{N}{2}} x\left[ \frac{N}{2}-n \right]   \sin\left( \frac{\pi k(2n-1)}{N} \right) \right\}
$$
## Teoremi della DFT 
#### Relazioni di simmetria 
$$
\begin{align}
X[k]=X^{*}[<-k>_{N}] \\
X_{\mathrm{Re}}[k]=X_{\mathrm{Re}}[<-k>_{N}] \\
X_{\mathrm{Im}}[k]=-X_{\mathrm{Im}}[<-k>_{N}] \\
|X[k]|=|X[<-k>_{N}]| \\
\arg X[k]=-\arg X[<-k>_{N}]
\end{align}
$$
### Teoremi 
l'applicazione dei teoremi è importante perchè ci permette in alcuni casi di trasformare una sequenza complessa partendo dalla combinazione di sequenze più semplici. Siano $g[n]$ e $h[n]$ due sequenze di cui abbiamo calcolato la DFT $G[k]$ e $H[k]$

#### Teorema di linearità 
Consideriamo la sequenza $x[n]=\alpha g[n]+\beta h[n]$ con $\alpha,\beta$ costanti reali. La DFT di X sarà allora  
$$
X[n]=\alpha G[k]+\beta H[k]
$$
#### Time shifting circolare 
la DFT di una sequenza circolare shifted $x[n]=g[<n-n_{0}>_{N}]$ è data da $X[k]=W_{N}^{kn_{0}}G[k]$ che è :
$$
g[<n-n_{0}>_{N}] \to W_{N}^{kn_{0}}G[k]
$$
#### Frequency shift circolare 
la DFT inversa di una DFT frequency shifted circolare è data da $x[n]=W_{N}^{-k_{0}n}$ che è 
$$
W_{N}^{-k_{0}n}g[n]\to G[<k-k_{0}>_{N}]
$$
#### Teorema di dualità 
$$
g[n]\to ^{DFT} G[k] \iff G[n]\to ^{DFT}Ng[<-k>_{N}]
$$
#### Teorema di convoluzione circolare 
la DFT a n punti di una sequenza $y[n]=g[n]\circledast_{n}h[n]$ è data da 
$$g[n]\circledast_{n}h[n]\to G[k]H[k]$$
per provarlo 
$$
\begin{align}
Y[k]=\sum_{m=0}^{N-1}y[n]W_{N}^{kn}=\sum_{n=0}^{N-1}\left( \sum_{m=0}^{N-1}g[m]h[<n-m>_{N}] \right)w_{N}^{kn}=\sum_{m=0}^{N-1}g[m]\left( \sum_{l=0}^{N-1}h[l]W_{N}^{k(l+m+Nr)} \right)=\\ \\
\sum_{m=0}^{N-1}g[m]\left( \sum_{l=0}^{N-1}h[l]W_{N}^{kl} \right)W_{N}^{km}=\sum_{m=0}^{N-1}g[m]W_{N}^{km}*H[k]=G[k]H[k]
\end{align}
$$

quindi il prodotto di due DFT non è altro che la convoluzione delle sue inverse. Quindi è possibile calcolare la convoluzione sfruttando la DFT e risparmiando calcoli. Inoltre permette di recuperare una sequenza sconosciuta partendo dalla sequenza di convoluzione e da una sequenza conosciuta. 

#### Teorema di modulazione 
la sequenza $y[n]=g[n]h[n]$ è data dalla convoluzione circolare delle loro DFT diviso N 
$$
g[n]h[n]\to ^{DFT} \frac{1}{N} \sum_{l=0}^{N-1}G[l]H[<k-l>_{N}]
$$

#### Teorema di Parseval
l'energia totale di una sequenza $g[n]$ può essere calcolata sommando il quadrato dei valori assoluti 
$$
\sum_{n=0}^{N-1}|g[n]|^{2}=\frac{1}{N}\sum_{k=0}^{N-1}|G[k]|^{2}
$$
una versione più generale è 
$$
\sum_{n=0}^{N-1}g[n]h^{*}[n]=\frac{1}{N}\sum_{k=0}^{N-1}G[k]H^{*}[k]
$$
## Filtraggio nel dominio delle frequenze 
Spesso si interessati nel rimuovere le componenti di una sequenza finita in una o più bande di frequenza. Se si conosce a priori quali esse siano allora l'approccio più veloce è implementare un filtro nel dominio delle frequenze. Siano $X(e^{ j\omega })$ e $H(e^{ j\omega })$ le trasformate di Fourier dell'input e della risposta del filtro, allora la sequenza in output Y sarà semplicemente il prodotto delle due trasformate $Y(e^{ j\omega })=H(e^{ j\omega })X(e^{ j\omega })$ . A questo punto basterà anti trasformare Y per ottenere l'output filtrato. L'unico problema è che la parte immaginaria di questo segnale dovrebbe essere zero, ma a causa di errori computazionali saranno numeri molto piccoli, per questo motivo solo la parte reale di questo segnale filtrato viene tenuta. 

## Calcolare le DFT di sequenze reali.
In molte applicazioni di interesse pratico le sequenze di interesse sono reali. In questi casi le proprietà di simmetria possono essere usate per rendere la DFT più veloce. 

### DFT a N punti di due sequenze reali usando una singola DFT a N punti 
Siao $g[n]$ e $h[n]$ 2 sequenze di lunghezza N. Con $G[k]$ e $H[k]$ le loro trasformate a N punti. Queste due trasformate a N punti possono essere calcolate efficientemente con una sola DFT definita da 
$$
x[n] = g[n]+jh[n]
$$
per cui $g[n]=Re\{x[n]\}$ mentre $h[n]=Im\{x[n]\}$, usando le proprietà nella tabella arriviamo a 
$$
\begin{align}
G[k]=\frac{1}{2}\{X[k]+X^{*}[<-k>_{N}]\} \\
H[k]=\frac{1}{2j}\{X[k]-X^{*}[<-k>_{N}]\}
\end{align}
$$
### DFT a 2N punti con una sola DFT 
Sia $v[n]$ una sequenza reale lunga 2N con V la trasformata. Siano $g[n],h[n]$ due sequenza di lunghezza n tali che $g[n]=v[2n],h[n]=v[2n+1]$. Con G e H le loro DFT a N punti. 
$$
V[k]=\sum_{n=0}^{2N-1}v[n]W_{2N}^{nk} =^{!3} \sum_{n=0}^{N-1}g[n]W_{N}^{nk}+W_{2N}^{k}\sum_{n=0}^{N-1}h[n]W_{N}^{nk}=G[<k>_{N}]+W_{2N}^{k}H[<k>_{N}]
$$
## Convoluzione lineare usando la DFT 
Siccome la DFT può essere calcolata in modo efficiente, vale la pena sviluppare algoritmi che possano farne uso per il calcolo della convoluzione.

### Convoluzione lineare di due sequenze finite 
Dalla definizione di convoluzione circolare il processo usa somma di prodotti di campioni di due sequenze della stessa lunghezza con la seconda sequenza che è invertita e shiftata circolarmente rispetto all prima sequenza. L'operazione di shifting circolare causa il wraparound della seconda sequenze per portare tutti gli indici dei campioni a rimanere nel range della prima sequenza. Invece nella convoluzione circolare il processo usa la somma di prodotti di campioni di due sequenze con la seconda sequenza tempo invertita e linearmente shiftata rispetto alla prima sequenza. Per cui il numero di campioni prodotti è esattamente uguale alla lunghezza delle sequenze, che quindi crescono linearmente. Per cui per implementare la convoluzione circolare si possono estendere le sequenze aggiungendo zeri dove necessario. 

Sia $g[n],h[n]$ due sequenze a lunghezza N e M rispettivamente. L'obiettivo è ottenere 
$$
y_{L}[n]=g[n]\circledast h[n]
$$
usando una convoluzione circolare. Sia L la lunghezza della sequenza $y_{L}[n]$ dove 
$L=M+N-1$ m definiamo 2 sequenze di lunghezza L 
$$
\begin{align}
g_{e}[n]=\begin{cases}
g[n] & 0\leq n\leq N-1 \\
0  & N\leq n\leq L-1
\end{cases} \\
h_{e}[n]=\begin{cases}
h[n] & 0\leq n\leq M-1 \\
0 & M\leq n \leq L-1
\end{cases}
\end{align}
$$
ottenuta aggiungendo gli elementi a 0. Allora $y_{L}[n]=y_{C}[n]=g_{e}[n]\circledast h_{e}[n]$

### Il prefisso ciclico
La DFT inversa a L-punti della sequenza calcolata precedentemente porta alla somma convolutiva $y[n]$ di $x[n]$ e $h[n]$ . In alcuni applicazioni è richiesto di calcolare solo una porzione della sequenza $y[n]$ di lunghezza N che può essere portata fuori usando una DFT a N punti e la sua inversa aggiungendo alla sequenza più lunga una sequenza più corta chiamata **prefisso ciclico** . 
Siano $x[n],h[n]$ due sequenze di lunghezza N e M con M < N. il prefisso ciclico di x è dato dalla sequenza $x[N-M+1],x[N-M+2,\dots,x[N-1]]$ di lunghezza M-1, consiste negli $M-1$ campioni di $x[n]$. 