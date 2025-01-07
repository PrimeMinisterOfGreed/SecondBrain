gli LTI si possono classificare in vari modi oltre alla funzione di trasferimento. 4 tipi di filtri ideali sono descrivibili a partire dalla forma della funzione di magnitudine $|H(e^{ j\omega })|$ che però non sono realizzabili perchè non sono causali, è possibile però una loro approssimazione. 

## Classificazione della funzione di trasferimento basata sulla funzione di magnitudine 
### Filtri digitali con magnitudine ideale 
Una classificazione normalmente usata è quella basta sulla magnitudine ideale della risposta. Anche se questi filtri non sono realizzabili è possibile approssimarli con alcune tolleranze. Il range di frequenze in cui la risposta vale 1 è chiamata banda passante, mentre il range dove è 0 è chiamata banda stoppante. 
#### Risposte in frequenza dei 4 filtri più popolari 
filtro, banda stoppante, banda passante
- filtro passa basso ,  $\omega_{c} < \omega \leq \pi$, $0\leq \omega \leq \omega_{c}$
- filtro passa alto ,  $0\leq \omega\leq \omega_{c}$ , $\omega_{c}\leq\omega \leq \pi$
- filtro a banda passante, $0\leq\omega \leq\omega_{1} \land \omega_{c_{2}}<\omega<\pi$ , $\omega_{c_{1}} \leq \omega \leq\omega_{c_{2}}$
- filtro a banda stoppante inverso del precedente.

### Funzione di trasferimento legata 
Una funzione di trasferimento stabile a valori reali $H(z)$ è definita come **bounded real (BR) transfer function** se 
$$
|H(e^{ j\omega })|\leq 1; \forall \omega
 $$


Sia $H(z)= \frac{k}{1-\alpha z^{-1}}$ dove K è una costante reale. La sua magnitudine quadra è data da 
$$
|H(e^{ j\omega })|^{2}=H(z)H(z^{-1})|_{z=e^{ j\omega }}= \frac{K^{2}}{(1+\alpha^{2})-2\alpha \cos \omega}
$$
 Il valore massimo di $|H(e^{ j\omega })|^{2}$ è ottenuto quando $2\alpha \cos \omega$ al denominatore è massimo e il minimo quando è al minimo. La funzione di trasferimento di un filtro a media mobile passa basso soddisfa la proprietà BR. Quando questa condizione avviene si può vedere nelle rispettive trasformate che avviene $|Y(e^{ j\omega })|^{2} \leq |X(e^{ j\omega })|^{2}$ . Integrando in $-\pi ,\pi$ e applicando Parseval otteniamo 
 $$
\sum_{n=-\infty}^{\infty}y^{2}[n]\leq \sum_{n=-\infty}^{\infty}x^{2}[n]
$$
In altre parole per tutti gli input che hanno energia finita l'energia dell'output è minore di quella dell'input. Se invece $|H(e^{ j\omega })| = 1$ allora l'energia è uguale e quindi otteniamo un sistema **lossless bounded real (LBR) transfer function**. 

### Funzione di trasferimento passa tutto 
un tipo particolare di IIR sono quelli caratterizzati da magnitudine unitaria (=1) per tutte le frequenze. Queste funzioni di trasferimento sono chiamate **allpass transfer function**. Questa proprietà serve più che altro per sviluppare un test algebrico per sapere se un filtro è BIBO. 

Una funzione di trasferimento $A(z)$ con magnitudine unitaria è $|A(e^{ j\omega })|^{2}=1;\forall \omega$
La sua funzione di trasferimento di ordine M è nella forma 
$$
A_{M}(z)= \pm \frac{d_{M}+d_{m-1}z^{-1}+\dots+d_{1}z^{-M-1}+z^{-M}}{1+d_{1}z^{-1}+\dots+d_{M-1}z^{-M+1}+d_{M}z^{-M}}
$$
sia $D_{M}(z)= 1+d_{1}z^{-1}+\dots+d_{M-1}z^{-M+1}+d_{M}z^{-M}$ per cui riscriviamo A come 
$$
A_{M}(z)= \pm \frac{z^{-M}D_{M}(z^{-1})}{D_{M(z)}} 
$$
una funzione di ordine M con coefficienti reali e causali può essere espressa in forma fattorizzata 
$$
A_{M}(z)= \pm \prod_{i=1}^{M} \frac{-\lambda_{i}^{*}+z^{-1}}{1-\lambda_{i}^{-1}}
$$
questa funzione ha un polo a $z=r e^{ j\theta }$ e uno zero in $z=\frac{1}{r}e^{ -j\theta }$. Il numeratore di una funzione passa tutto è detto **mirror-image polynomial**  del denominatore denominato con $\tilde{D}_{M}(z)$. L'equazione precedente implica che i poli e gli zeri di una funzione di trasferimento di questo tipo esibisca **mirror image symmetry** nel piano z per poli e zeri. 

è interessante esaminare il comportamento della funzioni di fase di questo tipo di funzioni. La unwrapped phase function di questa funzione mostra un comportamento di decrescita monotona sia per $A_{M}(z)$ e $-A_{M}(z)$ , il libro fa riferimento a una funzione con coefficienti causali. Il group delay di queste funzioni è 
$$
\tau_{g}(\omega)= \frac{1-r^{2}}{|1+r e^{ -j(\omega-\phi) }|^{2}}
$$
#### Proprietà 
1) una funzione di trasferimento stabile a coefficienti reali è LBR o equivalentemente un filtro stabile causale passa tutto è una struttura lossless. 
2) la magnitudine è $|A_{M}(z)| = \begin{cases}<1& |z|>1\\ =1 & |z|=1 \\ >1 & |z|<1 \end{cases}$
3) il group delay di questo tipo di funzioni di trasferimento è positivo nell'intervallo $0 \leq \omega \leq \pi$ e quindi $$\int_{0}^{\pi}\tau_{g}(\omega) \, d\omega = M\pi$$

#### Una semplice applicazione 
un filtro passa tutto è spesso usato per costruire un **equalizzatore ritardante**. Sia  $G(z)$ la funzione di trasferimento di un filtro digitale che è stato sviluppato per avere una risposta di magnitudine prescritta. La non linearità della risposta in fase può essere corretta mettendolo in cascata con un filtro passa tutto $A(z)$ così che la funzione di trasferimento totale sia $H(z)=G(z)A(z)$ , che ha cosi un group delay costante sul dominio in frequenza di interesse. La magnitudine della risposta della cascata è 
$$
|H(e^{ j\omega })|=|G(e^{ j\omega })||A(e^{ j\omega })|=|G(e^{ j\omega })|
$$
il group delay del filtro sono dati da 
$$
\tau_{G}(\omega)= - \frac{d\theta G(\omega)}{d\omega}, \tau_{A}(\omega)=- \frac{d\theta A(\omega)}{d\omega}
$$
dove rispettivamente $\theta_{G}(\omega)=\arg\{G(e^{ j\omega })\}$ e $\theta_{A}(\omega)=\arg\{A(e^{ j\omega })\}$
per cui $\theta_{H}=\theta_{G}(\omega)+\theta_{H}(\omega)$ e $\tau_{H}(\omega)=\tau_{G}(\omega)+\tau_{A}(\omega)$


## Caratteristiche delle funzioni di trasferimento in base alle caratteristiche della fase  
### Funzioni di trasferimento a fase zero 
in molte applicazioni è necessario assicurarsi che il filtro digitale non distolga la fase delle componenti del segnale in input. Una maniera di evitare ogni distorsione delle fasi è far si che la risposta in frequenza del filtro sia reale e non negativa , quindi bisogna sviluppare un filtro con caratteristica **zero phase**. Sia $H(z)$ una razionale a coefficienti reali senza poli nel cerchio unitario. Allora la funzione  
$$
F(z)=H(z)H(z^{-1})
$$
ha una fase zero nel cerchio unitario. I poli e gli zeri della funzione sono allocati nel piano z con **mirror-image symmetry**,. Un polinomio $A(z)=\sum_{i=0}^{L}a_{i}z^{-i}$ di grado L con radici allocate nel piano z con mirror image symmetry è chiamato **polinomio simmetrico** i cui coefficienti soddisfano la proprietà $a_{i}=a_{L-i}$. Un **polinomio a fase zero** deve essere quindi nella forma $$
B(z)=\sum_{l=0}^{N}b_{l}(z^{l}+z^{-l})
$$
è impossibile implementare un filtro digitale causale con fase zero in tempo reale, invece nel non real time possiamo implementarlo abbastanza facilmente visto che non abbiamo la restrizione di causalità. Uno degli schemi per farlo è il seguente 
sia:
- $v[-n]=u[n]$ 
- $X(e^{ j\omega }),V(e^{ j\omega }),U(e^{ j\omega }),W(e^{ j\omega }),Y(e^{ j\omega })$ le trasformate di x,v,u,w e y.
Facendo uso delle relazioni di simmetria arriviamo a (aggiungi $(e^{ j\omega })$)
$$
\begin{align}
V=HX,W=HU,U=V^{*},Y=W^{*}
\end{align}
$$
combinandole otteniamo 
$$
Y=W^{*}=H^{*}U^{*}=H^{*}V=H^{*}HX=|H|^{2}X
$$
per cui tutto lo schema implementa un zero phase filter con risposta in frequenza $|H(e^{ j\omega })|^{2}$

### Funzione di trasferimento fase lineare 
Nel caso degli LTI causali con risposta in fase non zero la distorsione può essere evitata facendo si che l'output sia una versione ritardata dell'input $y[n]=x[n-D]$. Prendendo la trasformata di Fourier di entrambi i lati e facendo uso del time shifting otteniamo 
$$
Y(e^{ j\omega })=e^{ -j\omega D }X(e^{ j\omega })
$$
Per cui la risposta in frequenza di un LTI è data da 
$$
H(e^{ j\omega })= \frac{Y(e^{ j\omega })}{X(e^{ j\omega })}=e^{ -j\omega D }
$$
con $|H(e^{ j\omega })|=1$ e $\tau(\omega)=D$. L'output di questo filtro a un input $x[n]=Ae^{ j\omega n }$ è quindi 
$$
y[n]=Ae^{ -j\omega D }e^{ j\omega n }=Ae^{ j\omega(n-D) }
$$
Se x e y rappresentano i segnali continui le cui sequenze campionati a t=nT sono le sequenze $x[n]$ e $y[n]$ allora il delay tra x e y è esattamente il group delay D. Se D è intero la sequenza è ritardata di D campioni, se non lo è la sequenza y non sarà identica x ma ritardata di d unità di tempo. 

Come esempio determiniamo la risposta all'impulso di un filtro passa basso con risposta in fase lineare. 
$$
H_{LP}(e^{ j\omega })=\begin{cases}
e^{ j\omega n_{0} } & 0<|\omega|<\omega_{c} \\
0 & \omega_{c}\leq|\omega|\leq\pi
\end{cases}
$$
applicando la proprietà di shifting alla trasformata di Fourier abbiamo la risposta all'impulso di un filtro passa basso a fase lineare 
$$
h_{LP}[n]= \frac{\sin\omega_{c}(n-n_{0})}{\pi(n-n_{0})}
$$
questo non è realizzabile perchè descritto per un range infinito, restringendo a N otteniamo un filtro FIR
$$
\hat{h}_{LP}[n]= \frac{\left( \sin\omega_{c}\left( n-\frac{N}{2} \right) \right)}{\pi\left( n-\frac{N}{2} \right)} ; 0\leq n\leq N
$$
A causa della simmetria della risposta all'impulso la risposta in frequenza dell'approssimazione troncata può essere espressa come 
$$
\DeclareMathOperator{\phaserr}{H_{LP}^{zp}(\omega)}

\hat{H}_{LP}(e^{ j\omega })= \sum_{n=0}^{N}\hat{h}_{LP}[n]e^{ -j\omega n }=e^{\frac{ j\omega N}{2 }} \phaserr
$$
dove $H^{zp}_{LP}(\omega)$ è la **risposta in ampiezza** o **zero phase response** ed è una funzione reale di $\omega$

### Funzioni di trasferimento fase minima e fase massima

Siano due funzioni di trasferimento causali  $H_{1}(z),H_{2}(z)$ con 
$$
\begin{align}
H_{1}(z)= \frac{z+b}{z+a} \\
H_{2}(z)= \frac{bz+1}{z+a}
\end{align}
$$


come si può vedere dal grafico dei poli zero entrambe le funzioni di trasferimento hanno un polo dentro il cerchio unitario nella stessa posizione a $z=-a$  e sono quindi stabili. D'altro canto lo zero di $H_{1}(z)$ è dentro il cerchio unitario a $z=-b$. Le due funzioni di trasferimento hanno identica funzione di magnitudine siccome $H_{1}(z)H_{1}(z^{-1})=H_{2}(z)H_{2}(z^{-1})$ dalle due equazioni precedenti 
$$
\arg[H_{1}(e^{ j\omega })]=\theta_{1}(\omega)=\tan ^{-1} \frac{\sin \omega}{b+\cos(\omega)} -\tan ^{-1} \frac{\sin \omega}{a+\cos \omega} 
$$
$$
\arg[H_{2}(e^{ j\omega })]=\theta_{2}(\omega)=\tan ^{-1} \frac{b\sin \omega}{1+b\cos \omega} - \tan ^{-1} \frac{\sin \omega}{a+\cos \omega}
$$
La proprietà di eccesso di lag di $H_{2}(z)$ rispetto a $H_{1}(z)$ può essere spiegata osservando che si può riscrivere 
$$
H_{2}(z)= \frac{bz+1}{z+a}=H_{1}(z)A(z)
$$
dove $A(z)= \frac{bz+1}{z+b}$ , per cui la relazione tra le due funzioni di fase diviene 
$$
\arg[H_{2}(e^{ j\omega })]=arg[H_{1}(e^{ j\omega })]+\arg[A(e^{ j\omega })]

$$

#### Proprietà 
 una funzione di trasferimento stabile a minima fase $H_{m}(z)$ ha un group delay $\tau_{g}^{H_{m}}(\omega)$ che è più piccolo di quello di una funzione di trasferimento causale non minima. Per dimostrare questa proprietà si può osservare che $\grpd^{(H)}= \grpd^{(H_{m})} + \grpd^{(A)}$ . Da cui segue che tutte le funzioni sono non negative su $\omega$ e quindi $\grpd^{H}>\grpd^{(H_{m})}$ 

Un altra proprietà interessante la otteniamo valutando la magnitudine di una funzione minima e una non minima. Siano $h_{m}[n],h[n]$ le sequenze di una funzione minima e una non, allora $|h_{m}[0]| \geq |h[0]|$ e quindi 
$$
\forsum{l=1}{n}|h_{m}[l]|^{2} \geq \forsum{l=1}{n}|h[l]|^{2}
$$
la quantità $\forsum{l=0}{n}h[l]$ è generalmente chiamata **energia parziale di $H(z)$**. Bisogna notare comunque che le energie totali delle due sequenze sono uguali 
$$
\forsum{l=0}{\infty}|h_{m}[l]|^{2}= \forsum{l=0}{\infty}|h[l]|^{2}
$$
Questo risultato è simile a quello ottenuto dalla relazione di Parseval. 

## Tipi di funzioni di trasferimento FIR lineari 
visto che è molto importante avere una funzione di trasferimento a fase lineare, esiste un modo di costruire le funzioni di trasferimento dei filtri FIR con una esatta fase lineare, non è possibile fare lo stesso con gli IIR. La forma di un FIR con questa risposta è  
$$
H(z)=\forsum{n=0}{N}h[n]z^{-n}
$$
se H ha fase lineare allora la sua funzione di fase deve essere del tipo 
$$
\theta(\omega)=c\omega+\beta
$$
dove $c,\beta$ sono costanti e quindi la sua risposta in frequenza deve essere nella forma 
$$
H(e^{ j\omega })= e^{ j(c\omega+\beta) } H^{zp}_{LP}(\omega)
$$
essendo che la funzione di fase è lineare allora $\grpd=-\frac{d\theta(\omega)}{d\omega}=-c$  che è quindi costante.

Se $H^{zp}_{LP}(\omega)$ è una funzione pari allora $\beta=0\lor \pi$ e quindi avrà una funzione lineare in fase se ha una risposta impulso simmetrica con condizione $h[n]=h[N-n]$.

Se $H^{zp}_{LP}(\omega)$ è una funzione dispari allora $\beta=\frac{\pi}{2} \lor -\frac{\pi}{2}$ e quindi avrà risposta lineare in fase se ha una risposta all'impulso asimmetrica con condizione $h[n]=-h[N-n]$. In entrambi i casi $c=-\frac{N}{2}$

#### Funzione di trasferimento di un FIR di tipo 1
La risposta impulso di questo filtro è di lunghezza dispari, quindi N è pari e soddisfa la condizione di simmetria $h[n]=h[N-n]$. La sua risposta in ampiezza $H^{zp}_{LP}(\omega)$ è 
$$
H^{zp}_{LP}(\omega) =h\left[ \frac{N}{2} \right]+2 \forsum{n=1}{\frac{N}{2}}h\left[ \frac{N}{2}-n \right]\cos(\omega n)
$$
Proprietà utili: 3 funzioni di trasferimento di tipo diverso con risposta in frequenze diverse si possono generare data una funzione di trasferimento FIR di tipo 1 H 
$$
\begin{align}
E(z)=z^{-N/2}-H(z) \\
F(z)=(-1)^{N/2}H(-z) \\
G(z)=z^{-N/2}-(-1)^{N/2}H(-z)
\end{align}
$$
dalla prima si nota che $H(z)+E(z)=z^{-N/2}$ e quindi i filtri E e H sono chiamati **delay complementary filters** . Stessa cosa vale per F e G. La risposta in ampiezza delle funzioni di trasferimento E e G sono in relazione con H 
$$
\begin{align} 
E^{zp}_{LP}(\omega)= 1-H^{zp}_{LP}(\omega) \\
F^{zp}_{LP}(\omega) = H^{zp}_{LP}(\pi-\omega) \\ 
G^{zp}_{LP}(\omega) =  1-H^{zp}_{LP}(\pi-\omega)
\end{align}
$$

#### Type 2 FIR 
lunghezza pari , N dispari e soddisfa la condizione di simmetria 
$$
H^{zp}_{LP}(\omega)=2 \forsum{n=1}{\frac{N+1}{2}} h\left[ \frac{N+1}{2} -n \right] \cos\left( \omega\left( n-\frac{1}{2} \right) \right)
$$

#### Type 3 FIR
lunghezza dispari, N pari e soddisfa la condizione di antisimmetria 
$$
H^{zp}_{LP}(\omega)=2 \forsum{n=1}{\frac{N}{2}}h\left[ \frac{N}{2}-n \right]\sin(\omega n)
$$
#### Type 4 FIR 
lunghezza pari, N dispari e soddisfa la condizione di asimmetria 
$$
H^{zp}_{LP}(\omega)=2 \forsum{n=1}{\frac{N+1}{2}}h\left[ \frac{N+1}{2}-n \right]\sin\left( \omega\left( n-\frac{1}{2} \right) \right)
$$
#### Forma generale di risposta in frequenza 
in ognuno dei 4 tipi la risposta in frequenza $H(e^{ j\omega })$ è nella forma 
$$
H(e^{ j\omega })=e^{ -jN\omega/2 }e^{ j\beta }H^{zp}_{LP}(\omega)
$$
dove $\beta=0 \lor \pi$

la risposta in fase di ogni filtro FIR a fase lineare è 
$$
\theta(\omega)= - \frac{N\omega}{2}+\beta
$$
la magnitudine della risposta è 
$$
|H(e^{ j\omega })|= |H^{zp}_{LP}(\omega)|
$$
e il group delay è $\grpd=\frac{N}{2}$


#### filtro FIR a fase zero 
un fir la cui risposta in frequenza è una funzione reale di $\omega$ è spesso chiamata **zero phase filter** . Questo filtro deve avere una risposta non causale. Un tipo 1 o tipo 3 FIR causale con risposta all'impulso h di lunghezza N+1 può essere convertito in un zero phase FIR con risposta all'impulso $h_{ZP}[n]$ shiftando 
$$
h_{ZP}[n]=h\left[ n+\frac{N}{2} \right]
$$
### Posizione degli zeri di una funzione di trasferimento di un FIR fase lineare 
