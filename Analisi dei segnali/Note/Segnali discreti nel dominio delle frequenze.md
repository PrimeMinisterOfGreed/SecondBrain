## La trasformata di Fourier continua
la rappresentazione nel dominio delle frequenze di un segnale continuo nel tempo $x_{a}(t)$ è data dalla 
>[!danger] Trasformata di Fourier tempo continua (CTFT)
> $$X_{a}(j\Omega)=\int x_{a}(t)e^{-j\Omega t} \, dt $$ 
> spesso ci si riferisce a questa come spettro di Fourier o semplicemente spettro del segnale, la sua anti trasformata ci permette di ottenere il segnale originale 
> $$x_{a}(t)=\frac{1}{2\pi}\int X_{a}(j\Omega)e^{j\Omega t} \, dt $$ 

denotiamo la coppia di equazioni in questo modo $x_{a}(t)\leftrightarrow^{CTFT}X_{a}(j\Omega)$. Dove:
- $\Omega$ => frequenza angolare tempo continua espressa in **radianti al secondo** 

La trasformata di Fourier inversa può essere interpretata come combinazione lineare di segnali complessi infinitamente piccoli nella forma $\frac{1}{2\pi}e^{j\Omega t}$ , pesati dalla costante complessa $X_{a}(j\Omega)$ nel range di frequenza angolare $(-\infty,+\infty)$. In generale la CTFT si può esprimere in 
>[!important] Forma polare 
>$$X_{a}(j\Omega)=|X_{a}(j\Omega)|e^{ j\theta_{a}(\Omega) }$$
>
>dove:
>- $\theta_{a}(\Omega)=\arg\{X_{a}(j\Omega)\}$ => **fase spettrale**
>- $|X_{a}(j\Omega)|$=> **magnitudine spettrale** 

entrambi gli spettri sono funzioni reali di $\Omega$ , La CTFT esiste se il segnale soddisfa le 
>[!important] Condizioni di Dirichlet 
> 1) Il segnale ha un numero finito di discontinuità e un numero finito di minimi e massimi in ogni intervallo finito 
> 2) Il segnale è **assolutamente integrabile** cioè $$\int |x_{a}(t)| \, dt < \infty$$ 

Se queste condizioni sono soddisfatte l'antitrasformata converge al segnale $x_{a}(t)$ per tutti i valori di t eccetto quelli in cui è presente una discontinuità. Si può mostrare che se $x_{a}(t)$ è assolutamente integrabile allora $|X_{a}(j\Omega)|<\infty$ , provando quindi l'esistenza della CTFT.

>[!example] CTFT della funzione impulso 
> $$\Delta(j\Omega)=\int \delta(t)e^{-j\Omega t} \, dt=1$$ 

>[!example] CTFT della funzione impulso shiftata 
>$$X_{a}(j\Omega)=\int \delta(t-t_{0})e^{ -j\Omega t } \, dt=e^{ -j\Omega t_{0} }$$

### Densità dello spettro energetico 
l'energia totale $\mathcal{E_{x}}$ di un segnale complesso a energia finita $x_{a}(t)$ è dato da 
$$
\mathcal{E_{x}}=\int |x_{a}(t)|^2 \, dt=\int x_{a}(t)x^{*}_{a}(t) \, dt  
$$
possiamo esprimere l'energia in termini della CTFT $X_{a}(j\Omega)$ 
$$
\mathcal{E_{x}}=^{!3}\frac{1}{2\pi}\int |X_{a}(j\Omega)|^{2} \, d\Omega 
$$
il cui integrando è noto come energy density spectrum. Denotato di solito dal simbolo $S_{xx}=|X_{a}(j\Omega)|^2$. Da cui si può ottenere:
>[!cite] Relazione di Parseval
> $$\int |x_{a}(t)|^{2}dt=\frac{1}{2\pi}\int |X_{a}(j\Omega)|^{2} \, d\Omega $$


## Trasformata di Fourier discreta 

>[!danger] Trasformata di Fourier discreta DTFT
>$$X(e^{ j\omega  })=\sum_{n=-\infty}^{\infty}x[n]e^{ -j\omega n }$$ 

>[!example] DTFT per sequenza unitaria 
>$$\Delta(e^{ j \omega  })=\sum_{n=-\infty}^{\infty}\updelta[n]e^{ -j\omega n }=1$$

>[!example] DTFT di una sequenza esponenziale $x[n]=\alpha^{n}\micro[n]$
>$$X(e^{ j\omega  })=\sum_{n=-\infty}^{\infty}\alpha^{n}\micro[n]e^{ -j\omega n }=\sum_{n=0}^{\infty}\alpha^{n}e^{ -j\omega n }=\frac{1}{1-\alpha e^{ -j\omega  }}$$


Una proprietà fondamentale della DTFT è che è una funzione di $\omega$ ma **a differenza della CTFT è una funzione periodica con periodo $2\pi$**. Per dimostrarlo possiamo osservare che
$$X(e^{ j(\omega+2\pi k) })=\sum_{n=-\infty}^{\infty}x[n]e^{ -j(\omega+2\pi k)n }=\sum_{n=-\infty}^{\infty}x[n]e^{ -j\omega n }e^{ -j_{2}\pi kn }=X(e^{ j\omega })$$ cosa possibile sapendo che $e^{ -j_{2}\pi kn }=1$. Come risultato possiamo derivare 

>[!danger] Anti trasformata 
> $$x[n]=\frac{1}{2\pi}\int_{-\pi}^{\pi}X(e^{ j\omega  }e^{ j\omega n }) \, d\omega $$

proprio grazie al fatto che il periodo è $2\pi$. Per convenienza si delineano gli operatori:
- $\mathcal{F}\{x[n]\}$ => trasformata applicata alla sequenza 
- $\mathcal{F}^{-1}\{X(e^{ j\omega })\}$ => antitrasformata applicata alla sequenza 

Per verificare l'antitrasformata sostituiamo l'espressione per $X(e^{ j\omega })$ 
$$\begin{aligned}
x[n]= \frac{1}{2\pi}=\int_{-\pi}^{\pi} \left( \sum_{\mathcal{l}=-\infty}^{\infty}x[\mathcal{l}]e^{ -j\omega \mathcal{l} } \right) \, e^{ j\omega n }d\omega=\sum_{l=-\infty}^{\infty}x[l]\left( \frac{1}{2\pi}\int_{-\pi}^{\pi} \frac{1}{2\pi}e^{ j\omega(n-l) } \, d\omega \right)=\\ \sum_{l=-\infty}^{\infty}x[l] \frac{{\sin \pi (n-l)}}{\pi(n-l)}=\sum_{l=-\infty}^{\infty}x[l]\sin c(n-l)
\end{aligned}$$
per $n\neq l$ , $\sin \pi(n-l)=0$ e come risultato $\sin c(n-l)=0$ . 
Per determinare il valore corretto nel caso in cui $n=l$,$\sin c(n-l)=\frac{0}{0}$ osserviamo che $\sin c=\frac{\sin(\pi n)}{\pi n}$ è il valore campionato della funzione tempo continua $\frac{\sin(\pi t)}{\pi t}$ per t=n, per cui $\frac{\sin(\pi n)}{\pi n}=\frac{\sin(\pi t)}{\pi t}|_{t=n}$  usando quindi la regola di Hopital otteniamo. 

$$
\lim_{ t \to 0 } \frac{\sin(\pi t)}{\pi t}=\lim_{ t \to 0 } \frac{{\pi \cos(\pi t)}}{\pi}=1
$$
per cui $$\sin c(n-l)=\begin{cases}
1 & n=l \\ 0 & n=l 
\end{cases} = \updelta[n-l]$$
e quindi $$\sum_{l=-\infty}^{\infty}x[l]\sin c(n-l)=\sum_{l=-\infty}^{\infty}x[l]\updelta[n-l]=x[n]$$

### Forma rettangolare 
Una già verificata è la periodicità dell'antitrasformata. In generale la trasformata di Fourier si può scrivere nella sua 
>[!important] Forma rettangolare 
> $$X(e^{ j\omega })=X_{\mathrm{Re}}(e^{ j\omega })+jX_{\mathrm{Im}}(e^{ j \omega })$$
> dove gli addendi sono la parte immaginaria e reale della trasformata e funzioni reali di $\omega$
> 
>ne segue che 
>- $X_{\mathrm{Re}}=\frac{1}{2}\left\{ \frac{1}{2}X(e^{ j\omega })+X^{*}(e^{ j\omega }) \right\}$
>- $X_{\mathrm{Im}}(e^{ j\omega })=\frac{1}{2j}\{X(e^{ j\omega })-X^{*}(e^{ j\omega })\}$

abbiamo già visto anche la forma polare. che può essere messa in relazione con la forma rettangolare 

### Relazioni di simmetria 
- $X(e^{ j\omega })=X_{Re}(e^{ j\omega })+jX_{Im}(e^{ j\omega })$
- $X_{Re}(e^{ j\omega })$=> parte pari 
- $jX_{Im}(e^{ j\omega })$=> parte dispari 
- $X(e^{ j\omega })=X^{*}(e^{ -j\omega })$
- $X_{\mathrm{Re}}(e^{ j\omega })=X_{\mathrm{Re}}(e^{ -j\omega })$
- $X_{Im}(e^{ j\omega })=-X_{\mathrm{Im}}(e^{ -j\omega })$
- $|X(e^{ j\omega })|=|X(e^{ -j\omega })|$
- $\arg\{X(e^{ j\omega })\}=-\arg\{X(e^{ -j\omega })\}$
- $x[-n] \to X(e^{ -j\omega })$
- $x^{*}[-n] \to X^{*}(e^{ j\omega })$
- $x_{\mathrm{Re}}[n] \to X_{cs}(e^{ j\omega })=\frac{1}{2}\{X(e^{ j\omega })+X^{*}(e^{ -j\omega })\}$
- j$x_{\mathrm{Im}}[n] \to X_{ca}(e^{ j\omega })=\frac{1}{2}\{X(e^{ j\omega })-X^{*}(e^{ -j\omega })\}$
- $x_{cs}[n] \to X_{\mathrm{Re}}(e^{ j\omega })$
- $x_{ca}[n] \to jX_{\mathrm{Im}}(e^{ j\omega })$

dove xcs e xca sono rispettivamente coniugato simmetrico e antisimmetrico.

### Condizioni di convergenza 
La serie di Fourier converge sotto opportune condizioni, sia:
- $X_{K}(e^{ j\omega })=\sum_{n=-K}^{K}x[n]e^{ -j\omega n }$ => Somma parziale degli esponenti pesati complessi 

allora la convergenza uniforme di $X(e^{ j\omega })$ è $$\lim_{ K \to \infty } X_{K}(e^{ j\omega })=X(e^{ j\omega })$$
allora se $x[n]$è assolutamente sommabile ($\sum_{=-\infty}^{\infty}|x[n]|<\infty$) allora 
$$
|X(e^{ j\omega })|=|\sum_{n=-\infty}^{\infty}x[n]e^{ -j\omega n }|\leq \sum_{=-\infty}^{\infty}|x[n]||e^{ -j\omega n }|\leq \sum_{n=-\infty}^{\infty}|x[n]|<\infty \, \forall \omega
$$

garantendo quindi l'esistenza di $X(e^{ j\omega })$, in caso contrario la sommatoria diverge e non è possibile applicare la trasformata. O meglio è possibile utilizzando la **funzione di impulso ideale** o **funzione delta di Dirac** .
>[!important] Dirac Delta 
> $$\int \updelta(\omega) \, d\omega=1 $$

è definita anche dal limite della forma dell'area della funzione di impulso $p_{\Delta}(\omega)$ 
$$\updelta(\omega)=\lim_{ \Delta \to 0 } p_{\Delta}(\omega)$$
per fare questo ragionamento si consideri la seguente funzione esponenziale
$$x[n]=e^{ j\omega_{0}n }$$
la sua trasformata di Fuorier è $$X(e^{ j\omega })=\sum_{k=-\infty}^{\infty}2\pi \updelta(\omega-\omega_{0}+2\pi k)$$
per cui la sua anti trasformata sarà 
$$x[n]=\frac{1}{2\pi}\int_{-\pi}^{\pi} \sum_{k=-\infty}^{\infty}2\pi \updelta(\omega-\omega_{0}+2\pi k) e^{ j\omega n } \, d\omega=\int_{-\pi}^{\pi} \updelta(\omega-\omega_{0})e^{ j\omega n } \, d\omega=e^{ j\omega_{0}n }$$
### Forza di una DTFT 
Una misura della forza della DTFT è data dalla sua normal $\mathcal{L}_{p}$ definità come 

>[!important] Norma 
>$$||X||_{p}=\left( \frac{1}{2\pi}\int_{-\pi}^{\pi} |X(e^{ j\omega })|^p \, d\omega \right)^{1/p}$$

ne segue che la norma-1 sia il valor medio sull'integrale e la norma-2  il root-squared-mean della trasformata.

#### trasformate comuni 
- $\updelta[n]\implies 1$
- $1,(-\infty<n<\infty)\implies \sum_{k=-\infty}^{\infty}2\pi \updelta(\omega+2\pi k)$
- $\micro[n]\implies \frac{1}{1-e^{ j\omega }}+\sum_{k=-\infty}^{\infty}\pi \updelta(\omega+2\pi k)$
- $e^{ j\omega_{0}n }\implies \sum_{k=-\infty}^{\infty}2\pi \updelta(\omega-\omega_{0}+2\pi k)$
- $\alpha^{n}\micro[n],|\alpha|<1\implies \frac{1}{(1-\alpha e^{ -j\omega) }}$ 
- $(n+1)\alpha^{n}\micro[n],(|\alpha<1|)\implies \frac{1}{(1-\alpha e^{ -j\omega })^{2}}$

lowpass filter $h_{LP}[n]= \frac{{\sin \omega_{c}n}}{\pi n}$  => trasformata $H_{LP}(e^{ j\omega })=\begin{cases}1 & 0\leq |\omega|\leq \omega_{c}\\ 0 & \omega_{c}\leq |\omega|\leq \pi\end{cases}$
## Teoremi della DTFT 
usiamo come indicazione gli operatori introdotti precedentemente 
- $g[n] \xtofrom{\mathcal{F}}G(e^{ j\omega })$
- $h[n] \xtofrom{\mathcal{F}}H(e^{ j\omega })$

>[!important] Linearità
>sia $x[n]=\alpha g[n]+\beta h[n]$ una sequenza ottenuta da una combinazione lineare di g e h, dove $\alpha$ e $\beta$ sono costanti arbitrarie. La trasformata di Fourier è data da 
>$$
>\alpha g[n]+\beta h[n] \xtofrom{\mathcal{F}}\alpha G(e^{ j\omega })+\beta H(e^{ j\omega })
>$$

>[!important] Inversione temporale 
>$$g[-n]\xtofrom{\mathcal{F}}G(e^{ -j\omega })$$

>[!important] Shifting 
>$$
g[n-n_{0}]\xtofrom{\mathcal{F}}e^{ -j\omega n_{0} }G(e^{ j\omega })
$$

>[!important] Shifting della frequenza 
>$$e^{ j\omega_{0}n }g[n]\xtofrom{\mathcal{F}}G(e^{ j(\omega-\omega_{0}) })$$

>[!important] Differenziazione in frequenza 
>$$ng[n]\xtofrom{F}j \frac{dG(e^{ j\omega })}{d\omega}$$

>[!important] Convoluzione 
>$$g[n]\circledast h[n] \xtofrom{\mathcal{F}}G(e^{ j\omega })H(e^{ j\omega })$$

sia $y[n]=g[n]\circledast h[n]$ allora 
$$
y[n]=\sum_{k=-\infty}^{\infty}g[k]h[n-k]\implies Y(e^{ j\omega })=\sum_{n=-\infty}^{\infty}\left( \sum_{k=-\infty}^{\infty}g[k]h[n-k] \right)e^{ -j\omega n }
$$
riarrangiando m=n-k otteniamo 
$$
\begin{align}
Y(e^{ j\omega })=\sum_{m=-\infty}^{\infty}\sum_{k=-\infty}^{\infty}g[k]h[m]e^{ -j\omega(m+k) } =\sum_{k=-\infty}^{\infty}g[k]\left( \sum_{m=-\infty}^{\infty}h[m] e^{ -j\omega m } \right)e^{ -j\omega k }\\ =\sum_{k=-\infty}^{\infty}g[k]H(e^{ j\omega })e^{ -j\omega k }=G(e^{ j\omega })H(e^{ j\omega })
\end{align}
$$


>[!important] Modulazione o Teorema della finestra 
>$$g[n]h[n]\xtofrom{\mathcal{F}} \frac{1}{2\pi}\int_{-\pi}^{\pi} G(e^{ j\theta })H(e^{ j(\omega-\theta) }) \, d\theta$$

osserviamone la trasformata di fourier 
$$Y(e^{ j \omega })=\sum_{n=-\infty}^{\infty}g[n]h[n]e^{ -j\omega n }$$
usando l'inversa per esprimere g possiamo scrivere 
$$
\begin{align}
Y(e^{ j\omega })=\frac{1}{2\pi} \sum_{n=-\infty}^{\infty}\int_{-\pi}^{\pi} h[n]e^{ -j\omega n }G(e^{ j\theta })e^{ j\theta n } \, d\theta=\\ \frac{1}{2\pi} \int_{-\pi}^{\pi} G(e^{ j\theta })H(e^{- j(\omega-\theta)n }) \, d\theta=\\ \frac{1}{2\pi}\int_{-\pi}^{\pi} G(e^{ j\theta })H(e^{ -j(\omega-\theta) }) \, d\theta
\end{align}
$$

>[!important] Parseval 
>$$\sum_{n=-\infty}^{\infty}g[n]h^{*}[n]=\frac{1}{2\pi} \int_{-\pi}^{\pi} G(e^{ j\omega })H^{*}(e^{ j\omega }) \, d\omega$$

$$
\begin{align}
\sum_{n=-\infty}^{\infty}g[n]h^{*}[n]=\sum_{n=-\infty}^{\infty}g[n]\left( \frac{1}{2\pi} \int_{-\pi}^{\pi} H^{*}(e^{ j\omega }e^{ -j\omega n }) \, d\omega \right)\\=\frac{1}{2\pi} \int_{-\pi}^{\pi} H^{*}(e^{ j\omega })\left( \sum_{=-\infty}^{\infty}g[n]e^{ -j\omega n } \right) \, d\omega = \frac{1}{2\pi}\int_{-\pi}^{\pi} H^{*}(e^{ j\omega })G(e^{ j\omega }) \, d\omega
\end{align}
$$

## Spettro di energia di una sequenza discreta 
usando il teorema di parseval, se $h[n]=g[n]$
$$
\mathcal{E_{g}}=\sum_{n=-\infty}^{\infty}|g[n]|^{2}=\frac{1}{2\pi} \int_{-\pi}^{\pi} |G(e^{ j\omega })|^{2} \, d\omega
$$
per cui è possibile calcolare l'energia usando l'integrale alla destra mentre lo spettro $S_{gg}(e^{ j\omega })=|G(e^{ j\omega })|^{2}$

l'energia di un filtro passa basso discreto è $<\infty$. Ed è quindi una sequenza a energia limitata.

## Segnali discreti limitati in banda 
Dato che lo spettro di un segnale è una funzione periodica di $\omega$ con periodo $2\pi$ , un segnale a banda piena ha uno spettro che occupa tutto il range $-\pi\leq \omega \leq \pi$. Un segnale limitato in banda occuperà solo una parte di questo spettro. Anche in questo caso esiste un segnale ideale a banda limitata, ma in pratica non può essere generato. I segnali a banda limitata si possono classificare in base al **range di frequenza in cui il segnale si concentra**. Un segnale reale passa basso occuperà un spettro sotto un certo $\omega$ , al contrario un filtro passa alto, mentre un filtro limitato sarà ristretto a una certa banda. Anche in questo caso le definizioni dipendono dalla soglie fissate per l'applicazione in oggetto.
## Funzione Fase unwrapped 
Nei calcoli numerici quando la funzione della fase è fuori dal range $[-\pi,\pi]$ questa è calcolata modulo $2\pi$ , per portare il risultato entro questo intervallo. Ne consegue che la funzione della fase mostra alcune discontinuità di $2\pi$ radianti nel grafico. In questi casi è utile considerare un tipo alternativo di funzione di fase che è una funzione continua di $\omega$ derivata dalla funzione originale per rimuovere le discontinuità. Questo processo si chiama **"Unwrapping phase"**  e la nuova funzione di fase verrà denotata da $\theta_{c}(\omega)$ , la c **indica che la funzione è continua**. Le condizioni per poter dire che questa funzione sarà continua.
il logaritmo naturale della trasformata si può esprimere come 
$$\ln X(e^{ j\omega })=\ln |X(e^{ j\omega })|+j\theta(\omega)$$
dove:
- $\theta(\omega)=\arg\{X(e^{ j \omega })\}$ 

se questo logaritmo esiste allora la sua derivata rispetto $\omega$ anche esiste ed è data da 
$$
\frac{{d \ln X(e^{ j \omega })}}{d\omega}= \frac{1}{X(e^{ j\omega })}  \frac{[dX(e^{ j \omega })]}{d\omega}= \frac{1}{X(e^{ j\omega })}\left[  \frac{dX_{\mathrm{Re}}(e^{ j\omega })}{d\omega} + j \frac{dX_{\mathrm{Im}}(e^{ j\omega })}{d\omega} \right]
$$
per cui deriviamo anche 
$$
\frac{d\theta(\omega )}{d\omega}=\frac{1}{|X(e^{ j\omega })|^{2}} [X_{\mathrm{Re}}(e^{ j\omega }) \frac{dX_{\mathrm{Im}}(e^{ j\omega })}{d\omega}- X_{\mathrm{Im}}(e^{ j\omega }) \frac{dX_{\mathrm{Re}}(e^{ j\omega })}{d\omega}]
$$
la funzione di fase $\theta(\omega)$ può quindi essere definita dalla sua derivata $\frac{d\theta(\omega)}{d\omega}$ 
>[!important] unwrapped phase function 
>$$
>\theta(\omega)=\int_{0}^{\omega} \frac{d\theta(\eta)}{d \eta } \, d \eta 
>$$
>con il vincolo che $\theta(0)=0$

## Processamento dei segnali digitali 
I segnali digitali per essere manipolati e analizzati vanno discretizzati da una sorgente analogica, pertanto è necessario comprendere a pieno le relazioni che ci sono e gli effetti di questo processo, in modo da evitare che vi siano errori durante il campionamento. 
Il device che trasforma un segnale analogico in uno digitale si chiama analog-to-digital converter (ADC). L'inverso di questa operazione è un digital-to-analog converter (DAC). Visto che la conversione analogica digitale prende un tempo finito è necessario assicurarsi che il segnale rimanga costante in ampiezza durante la conversione, meccanismo svolto da un circuito sample-and-hold (SH) 

### Effetto del campionamento nel dominio delle frequenze 
Sia $g_{a}(t)$ un segnale continuo campionato uniformemente con $t=nT$ con T periodo di campionamento. Il segnale campionato genera una sequenza $g[n]=g_{a}(nT)$ . La rappresentazione nel dominio delle frequenze è data dalla CTFT di questo segnale $G_{a}(j\Omega)=\int g_{a}(t)e^{ -j\Omega t } \, d\Omega$, mentre la stessa cosa vale per la sequenza ma usando una DTFT $G(e^{ j\omega })=\sum_{n=-\infty}^{\infty}g[n]e^{ -j\omega n }$. Per stabilire una relazione tra le due operazioni trattiamo l'operazione di campionamento matematicamente come fosse una moltiplicazione tra il segnale continuo e un treno di impulso periodico $p(t)= \sum_{n=-\infty}^{\infty} \updelta(t-nT)$. Per cui dobbiamo valutare
$$g_{p}(t)=g_{a}(t)p(t)=\sum_{n=-\infty}^{\infty}g_{a}(nT)\updelta(t-nT)$$
La CTFT di questo segnale assume due forme, la prima è derivabile semplicemente usando la sua equazione sapendo che la CTFT di $\updelta(t-nT)=e^{ -j\Omega n t }$ per cui otteniamo 
$$
G_{p}(j\Omega)=\sum_{n=-\infty}^{\infty}g_{a}(nT)e^{ -j\Omega nT }
$$
usando la formula delle somme di Poisson ed eseguendo qualche passaggio otteniamo la seconda forma 
$$G_{p}(j\Omega)=\frac{1}{T}\sum_{k=-\infty}^{\infty}G_{a}(j(\Omega+k\Omega_{T}))$$
in questa forma Gp diventa una funzione periodica della frequenza $\Omega$ che consiste nella somma di repliche scalate di $\frac{1}{T}$ e shiftate di $\Omega_{T}$ di Ga.  Per k=0 il termine sulla destra dell'equazione è la porzione di banda base, e ogni termine rimanente sono le porzioni traslate in frequenza di Gp. Il range di frequenza $-\frac{\Omega_{T}}{2}\leq \Omega< \frac{\Omega_{T}}{2}$ è chiamato banda base o **banda di Nyquist**.  è possibile recuperare Ga da questo segnale composito (usando un filtro passa basso) solo se $\Omega_{T}\geq 2\Omega_{m}$ perchè in questo modo i due segnali non si sovrappongono, in caso contrario non si potrà a causa della sovrapposizione dei duye spettri, e della distorsione causata da parte delle repliche immediatamente fuori dalla banda base che vengono piegate all'indietro (o aliased). 
La metà della frequenza di campionamento $\frac{\Omega_{T}}{2}$ è conosciuta come frequenza di Nyquist o frequenza di piegamento o ancora **frequenza di cut-off**. Questo comportamento è anche conosciuto col nome di 

#### Teorema del campionamento 
>[!danger] **Teorema del campionamento** 
> sia $g_{a}(t)$ un segnale limitato in banda con $G_{a}(j\Omega)=0$ per $|\Omega|>\Omega_{m}$ . Allora $g_{a}(t)$ è unicamente determinato dai suoi campione $g_{a}(nT)$ se (**condizione di Nyquist**):
> $$\Omega_{T} \geq 2\Omega_{m}$$
> dove: $\Omega_{T}=\frac{2\pi}{T}$ 


se si campiona a più del rateo di Nyquist ($2\Omega_{m}$) allora si è in sovraccampionamento, altrimenti in sottocampionamento, se si sta campionando esattamente a essa siamo in campionamento critico. Tipici ratei di campionamento sono ad esempio 8khz nella telefonia e 44.1khz nell'audio. 

### Relazioni tra DTFT e CTFT 
Esiste una relazione tra le due , prendiamo in esame le due trasformate discreta $G(e^{ j\omega })$ e continua $G_{a}(j\Omega)$ osserviamo che: 
$$G(e^{ j\omega })=G_{p}(j\Omega)|_{\Omega=\frac{\omega}{T}} \iff G_{p}(j\Omega)=G(e^{ j\omega })|\omega=\Omega T$$

per cui possiamo arrivare al risultato desiderato dato da 
$$
\begin{align}
G(e^{ j\omega })=\frac{1}{T}\sum_{k=-\infty}^{\infty}(j\Omega+jk\Omega_{T})|_{\Omega=\frac{\omega}{T}} = \frac{1}{T}\sum_{k=-\infty}^{\infty}G_{a}\left( j \frac{\omega}{T}+ j \frac{{2\pi k}}{T} \right)
\end{align} 
$$
che può essere espresso come $G(e^{ j\Omega T })=\frac{1}{T} \sum_{k=-\infty}^{\infty}G_{a}(j\Omega+jk\Omega_{T})$ , possiamo vedere da queste equazioni che $G(e^{ j\omega })$ è ottenuto da Gp semplicemente scalando l'asse delle frequenze usando la relazione $\Omega=\frac{\omega}{T}$ 

### Recupero del segnale analogico 
usando il treno di impulsi è possibile osservare come si può recuperare il segnale originale facendolo passare attraverso un filtro passa basso ideale con frequenza di cutoff $\Omega_{C}$, deriviamo l'espressione per l'output $\hat{g}_{a}(t)$ del filtro come funzione dei campioni $g[n]$. La risposta all'impulso $h_{r}(t)$ del filtro ideale è ottenuta mediante trasformata inversa della risposta in frequenza $H_{r}(j\Omega)= \begin{cases}T& |\Omega|\leq \Omega_{c}\\ 0& |\Omega|>\Omega_{c}\end{cases}$ ed è data da 
$$
h_{r}(t)=\frac{1}{2\pi}\int H_{r}(j\Omega)e^{ j\Omega t } \, d\Omega=\frac{T}{2\pi}\int_{-\Omega_{c}}^{\Omega_{c}}e^{ j\Omega t } \, d\Omega = \frac{\sin(\Omega_{c}t)}{\Omega_{T}t/2}
$$
osservando come è costruito il treno di impulsi possiamo dire che l'output del filtro è una convoluzione con esso che ha una certa risposta all'impulso e quindi:
$$\hat{g}_{a}(t)=\sum_{n=-\infty}^{\infty}g[n]h_{r}(t-nT)=\sum_{n=-\infty}^{\infty} g[n] \frac{{\sin[\pi(t-nT)/T]}}{\pi(t-nT)/T}$$
che significa sostanzialmente che il segnale originale è ricostruito shiftando nel tempo la risposta d'impulso del filtro passa passo $h_{r}(t)$ di $nT$ e scalarne l'ampiezza di un fattore $g[n]$
per tutti gli n e poi sommandone tutte le versioni shiftate. Tuttavia è irrelizzabile visto che stiamo usando un filtro ideale (noncausale e instabile e sena funzione di trasferimento razionale) . Infatti è necessario un filtro analogico passa basso che limiti la banda del segnale continuo prima del campionamento per assicurarsi che le condizioni vengano rispettate.  