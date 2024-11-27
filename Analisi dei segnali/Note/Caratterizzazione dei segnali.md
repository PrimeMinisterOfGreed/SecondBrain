un segnale può essere generato da:
- Una sorgente => **Segnale Scalare**
- Più sorgenti => **Segnale Vettoriale**
se un segnale è rappresentato da valori reali allora è reale, altrimenti è complesso.

Un segnale è caratterizzato da:
- **Ampiezza** => il suo valore numerico 
- Variazione di Ampiezza => forma d'onda

Un segnale può essere in base alla discretizzazione:
- Continuo => Segnale analogico => $u(t) \rightarrow u(t,y,z)$ (banalmente un video in questo caso)
- Discreto => Segnale digitale $v[n] \rightarrow v[x,y,z]$ (per esempio nel caso di un immagine) 

I valori dei segnali possono essere:
- Deterministici => seguono una legge matematica
- Aleatori => provengono da una fonte aleatoria (rumore)

# Operazioni di processamento
## Operazioni sul dominio del tempo 
- Scaling => moltiplicazione per costante 
- Delay  => $x(t) \rightarrow y(t)=x(t-t_{0})$ => ritardo su $t_{0}$ , se $t_{0} < 0$  allora è anticipo 
- Addizione => $y_{1}(t)= x_{1}(t)+x_{2}(t)\dots$ 
- Moltiplicazione => $y_{1}(t)=x_{1}(t)*x_{2}(t)\dots$
- Integrazione => $y(1)= \int^{-\infty}_{t}x(\tau)d\tau$
- Differenziazione => $y(1)= \frac{dx(t)}{dt}$ 

Alcune operazioni sono meglio eseguibili nel dominio delle frequenze, a cui si passa usando la 
>[!theorem] **trasformata di fourier**
>$$X(j\Omega) = \int^{t}_{-\infty}x(t)e^{-j\Omega t}dt$$
>definito anche **spettro di** $x(t)$ l'operazione di passaggio serve per eseguire il filtraggio del segnale. Il range di frequenze che può passare da un filtro è detto **banda passante** mentre quella che non passa è la **banda filtrata**.



In molti casi la **funzione filtrante** è lineare tempo invariante =>
Sia $h(t)$ => impulso di risposta => il segnale è $y(t)=\int^{\infty}_{-\infty}h(t-\tau)x(\tau)dt$. 

Assumendo che il filtro non abbia precondizioni allora si può riscrivere come $Y(j\Omega)=H(j\Omega)x(j\Omega)$ dove Y,X e H sono le trasformazioni di fourier di y,x,e h. 

Un **filtro passa basso** => blocca tutte le frequenze $>f_{s}$ 
Un **filtro passa alto** => blocca tutte le frequenze $<f_{s}$ 
Un **filtro a banda passante** => fa passare le frequenze in $f_{s_{1}}<f<f_{s_{2}}$ 
Un **filtro Multibanda** => è una composizione di più filtri a banda passante 
Un **filtro di Notch** => è un filtro che blocca una singola sequenza 

Queste operazioni sono molto importanti per recuperare un segnale ad esempio da un interferenza o un rumore. 

## Generazione di segnali a valori complessi

Una sequenza può avere valori reali o complessi (segnali reali/complessi). I segnali acquisiti di solito hanno valori reali, ma per esigenze di analisi potrebbe essere necessario generare un segnale complesso da uno reale. Per farlo generalmente si ricorre alla 

>[!theorem] **Trasformata di Hilbert**  
 >$$
h_{HT(T)}=\frac{1}{\pi t} \rightarrow H_{HT}(j\Omega)= 
\begin{cases}
-j \Omega >0 \\  \\
j\Omega <0
\end{cases}
$$


Sia $x(t)$ un segnale reale analogico con una trasformata di Fourier continua $X(j\Omega)$ .
Se il segnale è reale allora la magnitudine ha simmetria **pari** e  la fase ha simmetria **dispari** . Lo spettro può quindi avere sia frequenze positive che negative, il segnale 
$$
X(j\Omega) = X_{p}(j\Omega)+ X_{n}(j\Omega) 
$$
Dove:
- $X_{p}(j\Omega)$ => porzione di frequenze positive di $X(j\Omega)$  
- $X_{n}(j\Omega)$ => porzione di frequenze negative di $X(j\Omega)$ 

Se applichiamo a $X_{}(t)$ Hilbert , il suo output $\hat{x}(t)$ avrà spettro 
>[!corollary] Corollario
>$$\hat{X}(j\Omega) = H_{HT}(j\Omega)X(j\Omega)= -jX_{p}(j\Omega)+jX_{m}(j\Omega)$$
>Si può mostrare che **$x(t)$ è anch'esso reale**.
>
>Sia $y(t)=x(t)+j\hat{x}(t)$ , allora $x(t)$ è la **In-Phase**, mentre $j\hat{x}(t)$ è la **componente di quadratura** la cui Trasformata di fourier è $$
>Y(j\Omega) =x(j\Omega)+j\hat{x}(j\Omega)=2X_{p}(j\Omega)
$$

Il segnale ottenuto è un **segnale analitico** => dato solo da frequenze positive. 

## Modulazione in Ampiezza 
Ci sono 4 tipi di modulazioni possibili dei segnali analogici: 
- Modulazione dell'ampiezza 
- Modulazione della frequenza 
- della fase 
- dell'impulso dell'ampiezza 

La modulazione dell'ampiezza parte da un segnale sinusoidale $A\cos(\Omega_{0}t)$, chiamato **carrier** o **portante**, variato da un segnale limitato in banda di frequenza detto **segnale modulante** $$y(t)=Ax(t)*\cos(\Omega_{0}t)$$ La modulazione si implementa moltiplicando i due segnali, lo spettro ottenuto è 
>[!definition]  Modulazione 
>$$f_{Y}(j\Omega)=\frac{A}{2}+f_{X}(j(\Omega-\Omega_{0})) + \frac{A}{2}f_{X}(j(\Omega+\Omega_{0}))$$
>Assumendo che $\Omega_{0}>\Omega_{m}$ dove $\Omega_{m}$ => massima frequenza del segnale. Adesso $y(t)$  è un segnale limitato in banda ad alta frequenza, in cui :
>- le frequenze in  $\Omega_{0}$ e $\Omega_{0}+\Omega_{m}$ è detta **banda superiore** 
> - invece quelle in $\Omega_{0}-\Omega_{m}$ è detta **banda inferiore** 

La procedura , poiché genera due banda omettendo il segnale portante è chiamata **Double Sideband Suppressed Carrier** (DSBSC) Modulation. 

### Demodulazione  
La demodulazione di $y(t)$ è fatta in 2 fasi 
1) $r(t) = y(t)*\cos(\Omega_{0})*t=Ax(t)*\cos^2\Omega_{0}t=\frac{A}{2}x(t)+\frac{A}{2}x(t)*\cos(2\Omega_{0}t)$ il prodotto è un segnale composto dal segnale originale modulato ma scalato di 1/2 e un segnale modulato in ampiezza con **frequenza portante** $2\Omega_{0}$ . 
2) Il segnale può essere recuperato da $r(t)$ facendolo passare da un filtro passa basso con **cutoff** $\Omega_{c}$ purché si soddisfi $\Omega_{m}<\Omega<2\Omega_{0}-2\Omega_{m}$, il risultato di questo filtraggio è un segnale scalato rispetto all'originale. 
Siccome è difficile che il **segnale demodulante** abbia la stessa frequenza portante di quello modulato, il processo viene modificato per includere il segnale portante. $y(t)= A[1+mx(t)]*\cos(\Omega_{0t})$ dove :
- m => costante scalata per far si che $\forall t[1+mx(t)]>0$  

Una versione alternativa della modulazione si chiama **Single Sideband Modulation** (SSB) e prevede di trasmettere solo la parte superiore o inferiore della banda modulata, per poi demodularlo con il processo speculare di demodulazione.

## Multiplexing e Demultiplexing 
il multiplexing è un processo che combina più segnali in uno, il demultiplexing è l'operazione contraria. Viene generalmente impiegato nella telefonia sotto la forma di **Frequency Division Multiplexing** (FDM), in cui ogni segnale vocale, tipicamente limitato in banda a bassa frequenza con larghezza $2\Omega_{m}$ è traslato in una banda di frequenza più alta usando la modulazione in ampiezza. La frequenza portante dei segnali modulati adiacenti è separata da $\Omega_{0}$ , con $\Omega_{0} > \Omega_{m}$ per assicurarsi che non ci siano segnali sovrapposti nello spettro del segnale modulato che sarà la composizione dei vari segnali.  Il ricevente dopo aver demodulato il segnale dovrà applicare vari filtri a banda passante con larghezza $2\Omega_{m}$ per riottenere il segnale portante.

## Modulazione della quadratura dell'ampiezza 

Questo metodo si chiama **Quadrature Amplitude Modulation** (QAM), usa DSB per modulare 2 differenti segnali cosi che occupino la stessa banda. In questo modo QAM riesce ad occupare la stessa qantità di banda di SSB sebbene DSB. 

Siano $x_{1}(t)$ e $x_{2}(t)$ due segnali limitati in banda a bassa frequenza con larghezza $\Omega_{m}$. Allora $y(t)= Ax_{1(t)}*\cos(\Omega_{0}t)+ Ax_{2(t)}*\sin(\Omega_{0}t)$ dove: $A\cos(\Omega_{0t})$ e $A\sin(\Omega_{0}t)$ sono le modulazioni per i segnali portanti, che hanno ora la stessa frequenza $\Omega_{0}$ ma sono sfasati di 90 gradi. In generale la prima componente è la In-Phase mentre la seconda è quella di quadratura.

Lo spettro di questo segnale è 
>[!definition] Spettro  QAM
>$$Y(j\Omega)=\frac{A}{2}\{x{1(j(\Omega-\Omega_{0}))+x_{1}(j(\Omega-\Omega_{0}))}\}+\frac{A}{2j}\{x_{2}j(\Omega-\Omega_{0})-x_{2}(j(\Omega-\Omega_{0}))\}$$

Il quale occupa la stessa banda che avrebbe occupato DSB. Per recuperare il vecchio segnale da quello composito deve questo deve essere moltiplicato per entrambe le componenti del carrier separatamente ottenendo il seguente risultato 
$r_{1}(t)=y(t)\cos(\Omega_{0}t)$ e $r_{2}(t)=y(t)\sin(\Omega_{0}t)$, sostituendo nell'equazione precedente e applicando un filtro passa basso con cutoff $\Omega_{m}$ riotteniamo il segnale originale.
