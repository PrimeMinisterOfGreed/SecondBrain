la DTFT è una funzione complessa della frequenza angolare che genera una una sequenza nel dominio delle frequenze. A causa della condizione di convergenza in molti casi questa potrebbe non esistere e quindi potrebbe non essere utilizzabile. Una generalizzazione della DTFT è la trasformata z che è una funzione complessa di una variabile complessa z. La rappresentazione di un LTI nel dominio z è data dalla sua funzione di trasferimento, che è la trasformata z della risposta all'impulso del sistema. 

## Definizione 
Per una data sequenza $g[n]$ la trasformata z è definita come 
>[!danger] Trasformata Z
> $$
> \mathcal{Z}\{g[n]\}=G(z)=\sum_{n=-\infty}^{\infty}g[n]z^{-n}
$$

dove $z=Re(z)+jIm(z)$ è una variabile complessa continua. Se esprimiamo z in termini polari $z=r e^{ j\omega }$ l'equazione si riduce a 
$$
G(r e^{ j\omega })=\sum_{n=-\infty}^{\infty}g[n]r^{-n}e^{ -j\omega n }
$$
comparandola con la DFT $G(e^{ j\omega })=\sum_{n=-\infty}^{\infty}g[n]e^{ -j\omega n }$ si può osservare che l'equazione è interpretabile come la trasformata della sequenza $g[n]r^{-n}$. Un interpretazione geometrica alla trasformata z si può dare considerando in punti nel piano complesso z. Per $\omega,r$ fissi il punto $z=r e^{ j\omega }$ nel piano complesso z è alla punta del vettore di lunghezza r che si origina nel punto z=0 e sotto intende un angolo $\omega$ rispetto all'asse reale. Per r=1 la trasformata z di G si riduce alla trasformata di Fourier se esiste.
- con z=1 il valore di $G(z)$ è $G(e^{ j_{0} })$ = valore $G(e^{ j\omega })$ con $\omega=0$
- con z = j $G(z)=G(e^{ j\pi/2 })$ 
e cosi via. Per cui se valutiamo $G(z)$ lungo tutto il cerchio unitario in senso antiorario per tutti i valori di $\omega$ iniziando da z=1 e terminando a z=1 abbiamo calcolato effettivamente $G(e^{ j\omega })$ per tutti i valori di $\omega \in[0,2\pi)$ , se andiamo in senso orario invece con $\omega \in [-2\pi,0)$ , quindi attraversando il cerchio unitario in entrambi i sensi possiamo valutare $\omega \in(-\infty,\infty)$ .

Esattamente come per la DTFT esistono condizioni per cui la sommatoria converga. Per una data sequenza, il set $\mathcal{R}$ di valori di z per cui la sua trasformata z converge è chiamata **regione di convergenza** , che sono quei numeri che soddisfano 
$$
\sum_{n=-\infty}^{\infty}|g[n]r^{-n}|<\infty
$$
Ne segue che scegliendo opportunamente r possiamo rendere la sommatoria assolutamente sommabile anche quando non lo è. Così una sequenza $g[n]$ per cui la DTFT non converge può avere una trasformata z con una ROC $\mathcal{R_{g}}$. Ne segue anche che se esiste un valore specifico di $z = r e^{ j\omega }$ per cui la trasformata $G(z)$ esiste allora esiste su tutto il cerchio di raggio r nel piano z. In generale la regione di convergenza $\mathcal{R}$ di una trasformata z della sequenza g è un anulre del piano z: $R_{g-}<|z|<R_{g+}$ . Dove $0 \leq R_{g-}\leq R_{g+}\leq \infty$. Più di una sequenza può avere la stessa trasformata z, per cui è importante associarvi anche la ROC $R_{g}$ per cui: $g[n] \xtofrom{z}G(z),ROC=\mathcal{R_{g}}$ .

#### Trasformata z di una sequenza causale esponenziale 
Sia $x[n]=\alpha^{n}\mu[n]$ , calcoliamo trasformata e regione di convergenza. Applichiamo la definizione 
$$
X(z)=\sum_{n=-\infty}^{\infty}\alpha^{n} \mu[n]z^{-n}=\sum_{n=0}^{\infty}\alpha^{n}z^{-n}
$$
questa sommatoria converge a $X(z)=\frac{1}{1-\alpha z^{-1}}$ per $|\alpha z^{-1}|<1$ , indicando che la ROC è la regione anulare $|z|>|\alpha|$ . Impostando $\alpha =1$ otteniamo la trasformata z della step sequence $\mu(z)=\frac{1}{1-z^{-1}}$ con ROC $1<|z|<\infty$ la cui DTFT non converge e per cui non esiste. 
La trasformata di una anticausale esponenziale è la medesima della causale con ROC però che è $|z|<|\alpha|$
 
#### Trasformata z di una sequenza finita 
sia $x[n]=\begin{cases}\alpha^{n}& M\leq n\leq N-1 \\ 0\end{cases}$ qui abbiamo 
$$
X(z)=\sum_{n=M}^{N-1}\alpha^{n}z^{-n}=\alpha^{M}z^{-M}\sum_{n=0}^{N-M-1}(\alpha z^{-1})^{n}=^{!1} \frac{\alpha^{M}z^{-M}-\alpha^{N}z^{-N}}{1-\alpha z^{-1}}
$$
(usando l'identità usata per la sommatoria della DFT 5.9). Per determinare la ROC di questa trasformata bisogna esaminare $\sum_{n=M}^{N-1}|\alpha z^{-1}|^{n}$ e determinare per quali valori questa sommatoria è finita. 

La trasformata di Fourier di una sequenza di lunghezza finita esiste sempre, poichè la ROC include sempre il cerchio unitario indipendentemente da M e N. Questa regola vale più in generale, se la ROC include il cerchio unitario alla esiste la trasformata di Fourier di quella sequenza poichè la sequenza originale g converge in questa condizione. 

| Sequenza | Trasformata-z | ROC |
| -------- | ------------- | --- |
$\updelta[n]\to 1\to \forall z$
$\mu[n], \frac{1}{1-z^{-1}},|z|>1$
$\alpha^{n}\mu[n], \frac{1}{1-\alpha z^{-1}},|z|>|\alpha|$
$n\alpha^{n}\mu[n], \frac{\alpha z^{-1}}{(1-\alpha z^{-1})^{2}}, |z|>|\alpha|$
$(n+1)\alpha^{n}\mu [n], \frac{1}{1-\alpha z^{-1}}^{2},|z|>|\alpha|$
$(r^{n}\cos \omega_{0}n)\mu[n], \frac{1-(r\cos \omega_{0})z^{-1}}{1-(2r \cos \omega_{0})z^{-1}+r^{2}z^{-2}},|z|>|r|$
$(r^{n}\sin \omega_{0}n)\mu[n], \frac{(r\sin \omega_{0})z^{-1}}{1-(2r \cos \omega_{0})z^{-1}+r^{2}z^{-2}},|z|>|r|$

## Trasformata Z razionale 
nel caso degli LTI , le trasformate z sono funzioni razionali di $z^{-1}$ che è il rapporto tra 2 polinomi $P(z)$ e $D(z)$ in $z^{-1}$ 
$$
H(z)= \frac{P(z)}{D(z)}= \frac{p_{0}+p_{1}z^{-1}+\dots+p_{M-1}z^{-M(M-1)}+p_{M}z^{-M}}{d_{0}+d_{1}z^{-1}+\dots+d_{N-1}z^{-N-1}+d_{N}z^{-N}}
$$
dove il grado di P(z) è M e di D(z) è N. Una rappresentazione alternativa è come rateo di due polinomi in z 
$$
H(z)=z^{N-M}\frac{p_{0}z^{M}+p_{1}z^{M-1}+\dots+p_{M-1}z+p_{M}}{d_{0}z^{N}+d_{1}z^{N-1}+\dots +d_{N-1}z+d_{N}}
$$
in alcune applicazioni è conveniente rappresentarla come polinomi di secondo ordine 
$$
H(z)=\frac{p_{0}}{d_{0}} \frac{\prod^{M/2}_{l=1}(1+p_{1l}z^{-1}+p_{2l}z^{-2})}{\prod_{l=1}^{N/2}(1+d_{1l}z^{-1}+d_{2l}z^{-2})}
$$
che può essere scritta in versione fattorizzata 
$$
H(z)= \frac{p_{0}}{d_{0}} \frac{\left( \prod_{l=1}^{M} 1-\mathcal{E}_{l}z^{-1} \right)}{\prod_{l=1}^{N}1-\lambda_{l}z^{=-1}}=z^{N-M} \frac{\left( \prod_{l=1}^{M}z-\mathcal{E}_{l} \right)}{\prod_{l=1}^{N}z-\lambda_{l}} 
$$
a una radice $z=\mathcal{E}_{l}$  del numeratore polinomiale $H(\mathcal{E}_{l})=0$ e come risultato questi valori di z sono conosciuti come zeri di $H(z)$ (zeri del numeratore). Similmente a una radice $z=\lambda_{l}$ del denominatore polinomiale, $H(\lambda_{l})\to \infty$ e questi punti nel piano z sono chiamati poli di $H(z)$ (in pratica gli zero del denominatore). 

## Regioni di convergenza di una trasformata z razionale 
la ROC di una razionale è legata alle posizioni dei suoi poli. Per questo motivo è interessante studiare le relazioni tra la ROC e i suoi poli ed è utile esaminare il grafico degli 0 della trasformata e la locazione dei poli. 

#### ROC di una z di una sequenza esponenziale 
sia $h[n]=(-0.6)^{n}\mu[n]$ e $H(z)$ la trasformata, usando l'equazione della trasf otteniamo 
$$
H(z)=\frac{1}{1+0.6^{z-1}}=\frac{z}{z+0.6}; |z|>0.6
$$

In generale, la ROC dipende dal tipo di sequenza di interesse. 

#### ROC di una sequenza finita bi laterale 
Sia $g[n]$ definita per $-M\leq n\leq N$ e $|g[n]|<\infty$ la sua z è 
$$
G(z)=\sum_{n=-M}^{N}g[n]z^{-n}= \left( \frac{\sum_{n=0}^{N+M}g[n_{0}M]z^{N+M-n}}{z^{N}} \right)
$$
$G(z)$ ha M poli a $z=\infty$ e N poli a $z=0$ , in generale la trasformata z di una sequenza finita converge sempre eccetto a $z=0$ o $z=\infty$ 

#### ROC di una sequenza infinita destra 
una sequenza $u_{1}[n]$ con valori non-zero solo per $n\geq 0$ è chiamata sequenza causale la cui trasformata z è 
$$
U_{1}(z)=\sum_{n=0}^{\infty}u_{1}[n]z^{-n}
$$
questa sequenza converge esteriormente a un cerchio $|z|=R_{1}$ con il punto $z=\infty$.

#### ROC di una sequenza mancina infinita 
chiamata anche sequenza anti causale con campioni non zero solo per $n\leq 0$ ha una trasformata z 
$$
V_{1}(z)=\sum_{n=-\infty}^{0}v_{1}[n]z^{-n}
$$
converge esteriormente interiormente a un cerchio $|z|=R_{3}$ con il punto $z=0$.

#### Inesistenza di una trasformata z di una sequenza infinita bilaterale
una sequenza infinita del tipo $u[n]=\alpha^{n}$ non ha una trasformata z . Questo si può notare perchè 
$$
U(z)=\sum_{n=0}^{\infty}\alpha^{n}z^{-n}+\sum_{n=-\infty}^{-1}\alpha^{n}z^{-n}
$$
la cui prima sommatoria converge per $|z|>|\alpha|$ mentre la seconda $|z|<|\alpha|$ e quindi non vi è sovrapposizione tra le due ROC. Una z razionale è infinita a un polo e per cui non converge per definizione. Per cui una z razionale non può contenere nessun polo. Inoltre la ROC di una z razionale è legata alle posizioni dei suoi poli.


## Trasformata Z inversa 
è importante definire l'inversa della z perchè è possibile implementare metodi efficienti per il calcolo della convoluzione come nel caso delle DFT. Ne esiste un'espressione generale analitica che coinvolge l'utilizzo di integrali curvilinei chiusi
$$
g[n]=\frac{1}{2\pi j} \int_{c}  G(z)z^{n-1}  \, dz 
$$
ma spesso e volentieri si usa un metodo di lookup tabellare inclusi in molti libri. 

ad esempio sia la trasformata di h 
$$
H(z)=\frac{0.5z}{z^{2}-z+0.25}=\frac{0.5z}{(z-0.5)^{2}}=\frac{0.5z^{-1}}{1-0.5z^{-1}}^{2}
$$
adesso dalla tabella delle z conosciute osserviamo che 
$$
n\alpha^{n}\mu[n] \xtofrom{z} \frac{\alpha z^{-1}}{(1-\alpha z^{-1})^{2}} , |z|>|\alpha|
$$
comparando con l'equazione della trasformata concludiamo che 
$$
h[n]=n(0.5)^{n}\mu[n]
$$
### Trasformata z da espansione di frazione parziale 

l'espressione generale può essere calcolata in un certo numero di modi. Una z razionale di una inversa causale ha una ROC che è esterna al cerchio. In questo caso è più conveniente esprimere $G(z)$ in forma di frazioni parziali espanse e determinare g sommando le inverse dei termini più semplici individualmente. Una razionale si esprime come 
$$
G(z)=\frac{P(z)}{D(z)}
$$
Se $M>N$ la frazione si chiama **frazione impropria**. In questo caso possiamo dividere P con Z e riesprimere G come 
$$
G(z)=\sum_{l=0}^{M-N}\eta_{l}z^{-l}+ \frac{P_{1}(z)}{D(z)}
$$
dove questa volta $N<M$ ed è quindi chiamata frazione propria. 

#### Poli Semplici 
in molti casi pratici G è una frazione propria con poli semplici . Siano i poli di G a $z=\lambda_{k}$ dove $\lambda_{k}$ sono distinte e $1\leq k\leq N$ . Una espansione parziale di G è nella forma 
$$
G(z)= \sum_{l=1}^{N} \frac{p_{l}}{1-\lambda_{l}z^{-1}}
$$
dove la costante $p_{l}$ è chiamata residui ed è data da 
$$
p_{l}-=(1-\lambda_{l}z^{-1})G(z)|_{z=\lambda_{l}}
$$
ogni termine nel lato destro ha una ROC $|z|>|\lambda_{l}|$ e quindi la sua trasformata inversa è 
$$g[n]=\sum_{l=1}^{N}p_{l}(\lambda_{l}^{n})\mu[n]$$
lo stesso approccio è utilizzabile per trovar la trasformata z di sequenze anti causali 

#### Poli multipli 
Se $G(z)$ è una frazione propria con multipli poli, l'espansione parziale ha una forma leggermente diversa. Per esempio se il polo a $z=v$ è un multiplo di L e i rimanenti N-L poli sono semplici e a $z=\lambda_{l},1\leq l \leq N-L$ allora l'espansione di G è 
$$
G(z)=\sum_{l=1}^{N-L} \frac{p_{l}}{1-\lambda_{l}z^{-1}}+ \sum_{i=1}^{L} \frac{\gamma_{i}}{(1-vz^{i-1})^{i}}
$$
dove le costanti $\gamma_{i}$ sono calcolate con la formula 
$$
\gamma_{i}= \frac{1}{(L-i)!(-v)^{L-i}} \frac{d^{L-i}}{d(z^{-1})^{L-i}}[(1-vz^{-1})^{L}G(z)]|_{z=v}
$$

## Proprietà della trasformata z
come nel caso della DFT anche la trasformata z soddisfa alcune importanti proprietà. 

### Coniugazione 
$$g^{*}[n]\xtofrom{z}G^{*}(z^{*}), ROC=R_{g}$$
### Tempo invertibilità 
$$g[-n] \xtofrom{z}G\left( \frac{1}{z} \right), ROC=\frac{1}{R_{g}}$$

### Linearità 
$$
\alpha g[n]+\beta h[n] \xtofrom{z}\alpha G(z)+\beta H(z), ROC=R_{g}\cap R_{h}
$$

### Time Shifting 
$$
g[n-n_{0}] \xtofrom{z}z^{-n_{0}}G(z), ROC=\mathcal{R_{g}}
$$
### Moltiplicazione per una sequenza esponenziale 
$$
\alpha^{n}g[n] \xtofrom{z}G\left( \frac{z}{\alpha} \right), ROC=|\alpha|R_{g}
$$
### Differenziazione 
$$
ng[n] \xtofrom{z}-z \frac{d(Gz)}{dz}, ROC=R_{g}
$$
### Convoluzione 
$$
g[n]\circledast h[n] \xtofrom{z} G(z)H(z)
$$
### Modulazione  
$$
g[n]h^{*}[n] \xtofrom{z} \frac{1}{2\pi j}\int _{C}G(v)H^{*}\left( \frac{z^{*}}{v^{*}} \right)v^{-1} \, dv, ROC=R_{g}R_{h} 
$$
### Parseval 
$$
\sum_{n=-\infty}^{\infty}g[n]h^{*}[n]=\frac{1}{2\pi j} \int _{C} G(v)H^{*} \frac{1}{v^{*}}v^{-1} \, dv 
$$

## Somma convolutiva di sequenze a lunghezza finita 
### Convoluzione lineare usando moltiplicazione polinomiale 
Sia $x[n],h[n]$ due sequenze causali di lunghezza L+1 e M+1. Le z , X e H sono polinomiali in $z^{-1}$  di grado L e M per cui 
$$
\begin{align}
X(z)= x[0]+x[1]z^{-1}+\dots+x[L]z^{-L} \\
H(z)= h[0]+h[1]z^{-1}+\dots+h[N]z^{-M}
\end{align}
$$
usando la proprietà di convoluzione otteniamo la z di Y che è l'output della convoluzione che è $Y(z)=H(z)X$ che è un polinomio in $z^{-1}$ di grado L+M
$$
Y(z)=y[0]+y[1]^{z-1}+\dots+y[L+M]z^{-(L+M)}
$$
il cui n esimo coefficiente è (quando anti trasformato)
$$
y[n]=\sum_{k=0}^{L+M}x[k]h[n-k], 0\leq n\leq L+M
$$
il processo si riduce quindi alla moltiplicazione tra 2 polinomi.
### Convoluzione circolare 
come nel caso della convoluzione lineare anche qui ci si riduce alla moltiplicazione tra due polinomi ma richiede l'operazione modulo dopo la moltiplicazione. Sia X e H due polinomi di grado N-1 in $z^{-1}$ 
$$
\begin{align}
X(z)= x[0]+x[1]z^{-1}+\dots+x[N]z^{-N-1} \\
H(z)= h[0]+h[1]z^{-1}+\dots+h[N]z^{-N-1}
\end{align}
$$
allora il loro prodotto $Y_{L}(z)=X(z)H(z)$ è un polinomio di grado 2N-1
$$
Y(z)=y[0]+y[1]^{z-1}+\dots+y[L+M]z^{-(2N-1)}
$$
sia $Y_{C}(z)$ il polinomio di grado N-1 i cui coefficienti $y_{C}[n]$ sono la convoluzione circolare a N punti di x e h $y_{C}[h]=x[n]\circledast_{N}h[n]$ allora 
$$
Y_{C}(z)= <Y_{L}(z)>_{(z^{-N}-1)}
$$
l'operazione di modulo rispetto a $z^{-N}-1$ è usata impostando $z^{-N}=1$ quindi 
$$
<z^{-N-1}>_{z^{-N}-1}=z^{-1};<z^{-N-2}>_{z^{-N}-1}=z^{-2}\dots
$$
## La funzione di trasferimento 
la frequenza della funzione di risposta $H(e^{ j\omega })$ di un LTI discreto è data dalla DTFT della risposta all'impulso del sistema. Essendo che la funzione è complessa della variabile di frequenza angolare $\omega$ è difficile manipolarla per la realizzazione di filtri digitali. Invece la z di una risposta impulso di un LTI , chiamata **funzione di trasferimento** è un polinomio in $z^{-1}$ e per un filtro con risposta nei reali ha coefficienti reali. In molti casi il filtro è caratterizzato da una equazione differenziale lineare con coefficienti reali e costanti. La funzione di trasferimento di un filtro del genere è una funzione razionale della variabile $z^{-1}$ che è quindi il rapporto tra due polinomi in $z^{-1}$ con coefficienti reali ed è quindi più abbordabile alla sintesi. 

### Definizione 
Consideriamo un LTI con una risposta impulso $h[n]$. La relazione input output di questo sistema è data da 
$$
y[n]=\sum_{k=-\infty}^{\infty}h[k]x[n-k]
$$
dove x e y sono l'input e l'output del sistema. Sia $Y(z),X(z),H(z)$ le z di y,x e h. Applichiamo il teorema della convoluzione e arriviamo alla relazione input output dell'LTI in z
$$
Y(z)=H(z)X(z)
$$
dove $$
H(z)=\sum_{n=-\infty}^{\infty}h[n]z^{-n}
$$
la quantità H è normalmente conosciuta come **funzione di trasferimento o del sistema** . Per l'equazione precedente abbiamo 
$$
H(z)= \frac{Y(z)}{X(z)}
$$
per cui la funzione di trasferimento è data dal rapporto tra le z di output e input. La z inversa di questo rapporto ci da la risposta originale h. 

### Espressioni della funzione di trasferimento 
#### Filtro FIR 
in caso di filtri FIR la relazione input-output nel dominio del tempo l'abbiamo già vista. La sua risposta all'impulso $h[n]$ è definita per $N_{1}\leq n\leq N_{2}$ e quindi $h[n]=0$ per $n<N_{1}$ e $n>N_{2}$ , per cui la funzione di trasferimento è data da 
$$
H(z)=\sum_{n=N_{1}}^{N_{2}}h[n]z^{-n}
$$
per un filtro causale $0\leq N_{1}\leq N_{2}$ tutti i poli di $H(z)$ di un filtro causale sono all'origine del piano z e come risultato la ROC è l'intero piano z escluso z=0.

funzione di trasferimento del filtro a media mobile 
$$
H(z)=\frac{1}{M}\sum_{n=0}^{M-1}z^{-n}=^{!1} \frac{z^{M}-1}{M[z^{M-1}(z-1)]}
$$

### IIR lineare finito dimensionale 
per un filtro IIR caratterizzato dall'equazione alle differenze, l'espressione per la funzione di trasferimento può essere derivata applicando la z a entrambi i lati dell'equazione e usando le proprietà di linearità e time shifting.
$$
\sum_{k=0}^{N}d_{k}z^{-k}Y(z)=\sum_{k=0}^{M}p_{k}z^{-k}X(z)
$$
da questa arriviamo all'equazione della funzione di trasferimento definita precedentemente $H(z)=\frac{Y(z)}{X(z)}$ , moltiplicando numeratore e denominatore del lato destro per $z^{M}$ e $z^{N}$ la funzione di trasferimento può essere espressa come z razionale. Per un IIR causale la risposta all'impulso è causale quindi la ROC è esterna al cerchio che passa attraverso il  polo più lontano dall'origine per cui la ROC è 
$$
|z|>max_{k}|\lambda_{k}|
$$
### Risposta in frequenza dalla funzione di trasferimento 
possiamo scrivere la funzione di trasferimento H nella forma rettangolare 
$$
H(z)=H_{\mathrm{Re}}(z)+jH_{\mathrm{Im}}(z)
$$
o alternativamente in forma polare 
$$
H(z)=|H(z)|e^{ j \arg H(z) }
$$
dove $\arg H(z)=\tan ^{-1}\left[ \frac{H_{\mathrm{Im}(z)}}{H_{\mathrm{Re}}(z)} \right]$. Se la ROC di $H(z)$ include il cerchio unitario allora la risposta in frequenza $H(e^{ j\omega })$ di un LTI può essere ottenuta dalla sua funzione di trasferimento $H(z)$ semplicemente valutandola nel cerchio unitario cioè 
$$
H(e^{ j\omega })=H(z)|_{z=e^{ j\omega }}
$$
la z di una sequenza può essere determinata dalla sua trasformata di Fourier da continuazione analitica 
$$
H(z)=H(e^{ j\omega })|_{\omega=\frac{1}{j}\ln z}
$$
per una funzione di trasferimento stabile nella la forma fattorizzata della risposta in frequenza $H(e^{ j\omega })$ è ottenibile sostituendo $z=e^{ j\omega }$ 
$$
H(e^{ j\omega })=\frac{p_{0}}{d_{0}}e^{ j\omega(N-M) } \frac{\prod_{k=1}^{M}(e^{ j\omega }-\mathcal{E}_{k})}{\prod_{k=1}^{N}e^{ j\omega }-\lambda_{k}}
$$
la funzione di magnitudine è quindi data da 
$$
|H(e^{ j\omega })|=| \frac{p_{0}}{d_{0}}| \frac{\prod_{k=1}^{M}|e^{ j\omega }-\mathcal{E_{k}}|}{\prod_{k=1}^{N}|e^{ j\omega } - \lambda_{k}|}
$$
la risposta di fase $\theta(\omega)$ di una funzione di trasferimento razionale è 
$$
\theta(\omega)=\arg H(e^{ j\omega })= \arg\left( \frac{p_{0}}{d_{0}} \right)+ \omega(N-M)+ \sum_{k=1}^{M}\arg(e^{ j\omega }-\mathcal{E_{k}})- \sum_{k=1}^{N}\arg(e^{ j\omega }-\lambda_{k})
$$
per una funzione di trasferimento $H(z)$ a coefficienti reali si può mostrare che 
$$
|H(e^{ j\omega })|^{2} = H(e^{ j\omega })H^{*}(e^{ j\omega })=H(e^{ j\omega })H(e^{ -j\omega })=H(z)H(z^{-1})|_{z=e^{ j\omega }}
$$
la magnitudine al quadrato per una funzione razionale di trasferimento si può calcolare come 
$$
|H(e^{ j\omega })|^{2}=H(e^{ j\omega })H(e^{ -j\omega })=|\frac{p_{0}}{d_{0}}|^{2} \frac{\prod_{k=1}^{M}(e^{ j\omega }-\mathcal{E_{k}})(e^{ -j\omega }-\mathcal{E_{k}^{*}})}{\prod_{k=1}^{N}(e^{ j\omega } - \lambda_{k})(e^{ -j\omega } - \lambda_{k}^{*})}
$$
la risposta di fase di un LTI con funzione di trasferimento a coefficienti reali è dato da 
$$
\theta(\omega)=\tan ^{-1}\left[ \frac{H_{\mathrm{Im}}(z)}{H_{\mathrm{Re}}(z)} \right]=\frac{1}{2j}\ln\left[ \frac{H(z)}{H(z^{-1})} \right]_{z=e^{ j\omega }}
$$
il group delay $\tau_{g}(\omega)$ di un LTI con funzione di trasferimento con coefficienti reali è 
$$
\tau_{g}^{H}=- \frac{d\theta(\omega)}{d\omega}=-Re\left( z \frac{d[\ln H(z)]}{dz} \right)|_{z=e^{ j\omega }}
$$
### Interpretazione geometrica del calcolo della risposta in frequenza 
per un filtro LTI con funzione razionale di trasferimento è conveniente sviluppare un interpretazione geometrica alla sua risposta in frequenza, partendo dal grafico del polo zero della funzione di trasferimento, osservando $\omega$ che varia tra $0,2\pi$ . Se esaminiamo l'espressione per la risposta in frequenza osserviamo che un fattore tipico è della forma 
$$
(e^{ j\omega }-\rho e^{ j\phi }) 
$$
dove $\rho e^{ j\phi }$ è uno zero se il fattore è dal numeratore detto fattore zero. Oppure viene dal denominatore ed è detto fattore di polo. Nel piano z il fattore $(e^{ j\omega }-\rho e^{ j\phi })$ rappresenta un vettore che parte dal punto $z=\rho e^{ j\phi }$ e finisce nel cerchio unitario a $z=e^{ j\omega }$ . Siccome $\omega$ varia in $0,2\pi$ la punta del vettore si muove in senso anti orario dal punto z=1 tracciando il cerchio unitario, e poi torna indietro al punto z=1. La magnitudine della risposta $|H(e^{ j\omega })|$ a uno specifico valore di $\omega$ è data dal prodotto delle magnitudini di tutti i vettori zero divisi per il prodotto delle magnitudini dei vettori poli. Allo stesso modo osserviamo che la risposta di fase $\arg H(e^{ j\omega })$ a uno specifico valore di $\omega$ è ottenuta aggiungendo il termine di fase $\frac{p_{0}}{d_{0}}$ e il termine di fase lineare $\omega(N-M)$ alla somma degli angoli di tutti i vettori zero meno la somma degli angoli dei vettori poli.  Cosi un grafico approssimato della magnitudine e della fase della funzione di trasferimento può essere ottenuto esaminando i suoi poli e le posizioni dei suoi zeri. Un vettore zero (polo) ha la minima magnitudine quando $\omega=\phi$. Se vogliamo costruire un filtro attenuante dobbiamo piazzare i suoi zero molto vicini al cerchio unitario. Per enfatizzarle poniamo i poli vicini al cerchio. 

### Condizioni di stabilità in termini di posizione dei poli 
Un LTI è BIBO solo se la sua risposta all'impulso è assolutamente sommabile 
$$
\sum_{n=-\infty}^{\infty}|h[n]|<\infty 
$$
che è difficile da testare nel caso di risposte all'impulso di lunghezza infinita. Per questo si sono sviluppate tecniche che usano invece la posizione dei poli 

#### Condizioni per LTI IIR del primo ordine 
sono gli IIR con risposta all'impulso causale $h_{1}[n]=\alpha^{n}\mu[n]$ ed è BIBO per $|\alpha|<1$ . La funzione di trasferimento del sistema è $H_{1}(z)=\frac{1}{1-\alpha z^{-1}}$ con una ROC data da $|z|>|\alpha|$. La funzione di trasferimento $H_{1}(z)$ ha un polo a $z=\alpha$ che è dentro il cerchio unitario se $|\alpha|<1$ di conseguenza il cerchio unitario è dentro la ROC della funzione di trasferimento.

Nel caso di un filtro anti causale la risposta all'impulso è $h_{2}[n]=-\beta^{n}\mu[-n-1]$ ed è BIBO se $|\beta|>1$ così anche h2 rispetta le condizioni di stabilità. La funzione di trasferimento in questo caso è $H_{2}(z)=\frac{1}{1-\beta z^{-1}}$ con una ROC data da $|z|<|\beta|$ che ha un polo in $z=\beta$ che è fuori dal cerchio unitario se $|\beta|>1$ di conseguenza il cerchio unitario è nel ROC della funzione di trasferimento. 

#### Stabilità di un filtro di second'ordine 
consideriamo 
$$
H(z)= \frac{(\alpha-\beta)z^{-1}}{(1-\alpha z^{-1})(1-\beta z^{-1})} , |\alpha|<1<|\beta|
$$
la funzione di trasferimento ha un polo dentro il cerchio a $z=\alpha$ e un polo fuori dal cerchio $z=\beta$ . Per cui questa funzione ha 3 possibili ROC. Bisogna esaminare la risposta all'impulso associata a ogni ROC e investigarne la stabilità .
Per determinare la risposta all'impulso $h[n]$ rifattorizziamo 
$$
H(z)=\frac{1}{1-\alpha z^{-1}}-\frac{1}{1-\beta z^{-1}}
$$
per ROC in $|z|>|\beta|$ la risposta all'impulso è data dalla somma di due sequenze causali 
$$
h[n]=\alpha^{n}\mu[n]-\beta^{n}\mu[n]
$$
siccome $|\beta|>1$ la seconda sequenza è instabile perchè non assolutamente sommabile. 
Per la ROC in $|\alpha|<|z|<|\beta|$ la risposta all'impulso è data dalla somma di una sequenza causale e una anti causale 
$$
h[n]=\alpha^{n}\mu[n]+\beta^{n}\mu[-n-1]
$$
entrambe sono assolutamente sommabili e quindi il sistema è stabile. Per la rimanente $|z|<|\alpha|$ anche in questo caso la risposta è instabile. 

La presenza dell'assoluta sommabilità della risposta all'impulso garantisce l'esistenza della trasformata di Fourier 
$$
|H(z)|=|\sum_{n=-\infty}^{\infty}h[n]z^{-n}|\leq \sum_{n=-\infty}^{\infty}|h[n]z^{-n}|= \sum_{n=-\infty}^{\infty}|h[n]||z^{-n}|
$$
Per cui sul cerchio unitario questa si riduce a 
$$
|H(z)|_{z=e^{ j\omega }}=|H(e^{ j\omega })|\leq \sum_{n=-\infty}^{\infty}|h[n]|
$$
