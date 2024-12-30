La funzione di un sistema tempo discreto è di processare una certa sequenza in input per generarne un altra in output con le caratteristiche che si desiderano oppure per estrarre certe informazioni sul segnale originale. Matematicamente il sistema a tempo discreto è caratterizzato da un operatore $\mathcal{H}(\vcenter{.})$ che trasforma la sequenza. L'output è computato sequenzialmente elemento per elemento. Nella pratica tutti i segnali presi in considerazione sono digitali che vengono passati in questi sistemi discreti, che sono anche chiamati filtri digitali. 
## Esempi di sistemi 
Di seguito ci sono vari sistemi a singolo input singolo output, matematicamente $y[n]=\mathcal{H(x[n])}$ , i sistemi più complicati sono ottenuti in genere combinando questi sistemi di base. 

### Accumulatore (IIR) 
l'accumulatore è definito tramite la relazione input-output 
$$
y[n]= \sum_{l=0}^{M-1} x[n-\mathcal{l}] 
$$
l'output all'istante n è la somma degli input fino a quell'istante. L'accumulatore può essere considerato come l'equivalente discreto dell'integratore. 

### Media mobile (FIR)
Come visto nella prima sezione se vogliamo separare un segnale e un rumore casuale possiamo ricorrere alla ensemble average. Nelle applicazioni dove la misura non pùo essere ripetuta , una stima più comune è rappresentata dalla media a M-punti o media data da $$y[n]=\frac{1}{M}\sum_{l=0}^{M-1}x[n-l]$$
una stima dello spread rispetto al valore medio è data naturalmente dalla deviazione standard. $$\sigma[n]=\frac{\sqrt{ \sum_{l=0}^{M-1}(x[n-l]-y[n])^{2} }}{M}$$
un'implementazione diretta della moving average potrebbe essere inefficiente, è possibile quindi ricorrere alla seguente versione migliorata (coinvolge meno operazioni).
$$y[n]=^{!3} \frac{1}{M}\left( \sum_{l=0}^{M-1}x[n-1-l]+x[n]-x[n-M] \right)=y[n-1]+\frac{1}{M}(x[n]-x[n-M])$$

questo sistema agisce come un **filtro passa basso** e come risultato raffina i dati in input rimuovendo le componenti ad alta frequenza. La scelta di M è molto importante poichè un M troppo grande potrebbe rimuovere componenti anche di media frequenza che fanno parte del segnale portante. 

### Filtro medio esponenzialmente pesato in corsa  (IIR)
Nel filtro precedente la media pone enfasi su tutti i campioni di dati. In alcune applicazioni potrebbe essere necessario metterla su dei campioni vicino a n e meno su altri per determinare la media. Cosa che può essere fatta con questo filtro 
$$
y[n]=\alpha y[n-1]+x[n] 
$$
per $0<\alpha<1$ il filtro mette enfasi sul dato corrente e meno su quelli passati. 
### Interpolatore lineare (FIR)
questo filtro serve per stimare i valori dei campioni in mezzo a coppie adiacenti di una sequenza discreta. l'interpolatore è implementato attraverso un up-samples il cui output $x_{u}[n]$ viene passato attraverso un secondo sistema che riempie i valori a zero inseriti dall'up-sampler con valori ottenuti dall'interpolazione lineare. Per cui 
$$
y[n]=x_{u}[n]+\frac{1}{2}(x_{u}[n-1]+x_{u}[n+1]) 
$$
questo filtro è anche conosciuto come **interpolatore bilineare**, cioè se $x_{u}[n]$ è 0 allora prende la media tra il valore precedente e il successivo, altrimenti usa direttamente il valore corrente. una sua variante è data dall'**interpolatore trilineare** 
$$
y[n]=x_{u}[n]+\frac{2}{3}(x_{u}[n-1]+ x_{u}[n+1])+ \frac{1}{3}(x_{u}[n-2]+x_{u}[n+2])
$$
Questo filtro ha delle applicazioni pratiche frequentemente utilizzate, come lo zoom di un immagine di fattori interi in entrambe le direzioni verticale e orizzontale.

### Filtro mediano 
la mediana di un insieme di (2K+1) numeri è il numero tale che K numero dal set hanno un valore maggiore di questo numero, mentre gli altri K sono minori. La mediana può essere calcolata mediante ordinamento dei numeri scegliendo quello di mezzo. Il filtro mediano è implementato attraverso una finestra semovente di lunghezza dispari sulla sequenza di input campione per campione. Ad ogni istante l'output del filtro è la mediana dei campioni in input dentro la finestra. Per cui 
$$
y[n]=med\{ x[n-K],\dots,x[n-1],x[n],x[n+1],\dots,x[n+K]\} 
$$
in pratica, per processare una sequenza finita $x[n]$ di lunghezza N bisogna creare una nuova sequenza 
$$
x_{e}[n]=\begin{cases}
0  & -\frac{M-1}{2}\leq n\leq-1\\ 
x[n] & 0\leq n\leq N-1 \\
0 & N\leq n\leq N-1+ \frac{M-1}{2}
\end{cases}
$$
questa sequenza quando processata da un filtro mediano genera una sequenza in output $y[n]$ anch'essa di lunghezza N. Questo filtro serve tipicamente per rimuovere rumori additivi casuali con valori molto elevati da un segnale corrotto, poichè in questo caso un filtro basato sulla media raffinerebbe anche il rumore senza rimuoverlo, questo avviene ad esempio molto nella telefonia. 

## Classificazione dei sistemi discreti 
### Sistemi lineari 
sono i più usati, in un sistema lineare il principio di superposizionamento è sempre vero. 
Siano: $y_{1}[n],y_{2}[n]$ le risposte alle sequenze di input $x_{1}[n],x_{2}[n]$ allora per un input $x[n]=\alpha x_{1}[n]+\beta x_{2}[n]$ la risposta è data da 
$$
y[n]=\alpha y_{1}[n]+\beta y_{2}[n]
$$
la superposizione deve essere vera per ogni costante arbitraria $\alpha,\beta$ e per tutti i possibili input. Questa proprietà rende molto semplice calcolare la risposta di un sistema discreto lineare anche di sequenze complesse, che possono essere decomposte mediante l'utilizzo di opportuni pesi. Un esempio di sistema lineare è l'accumulatore. 

### Sistemi shift invarianti 
la proprietà di invarianza allo spostamento è la seconda condizione imposta a molti filtri digitali usati. Sia $y_{1}[n]$ la risposta a un input $x_{1}[n]$ allora la risposta a un input $x_{1}[n-n_{0}]$ è $y_{1}[n-n_{0}]$. In caso di indici n relativi a istanti di tempo discreti è questa proprietà è comunemente chiamata **tempo invarianza** . La proprietà di tempo invarianza asserisce che per ogni input del sistema il suo output è indipendente dall'istante in cui il filtro è applicato.

### Sistemi causali 
In un sistema causale l'n0 esimo campione in output $y[n_{0}]$ dipende solo dal campione in input $x[n]$ per $n\leq 0$ e non dipende dai campioni in input per $n>n_{0}$ . Per cui siano $y_{1}[n],y_{2}[n]$ le risposte agli input $u_{1}[n],u_{2}[n]$ allora 

$$u_{1}[n]=u_{2}[n];n<N\implies y_{1}[n]=y_{2}[n];n<N$$
per cui **il cambiamento dei campioni in output non precede i cambiamenti nei campioni in input**.  Alcuni filtri già visti non sono causali, come l'interpolatore, ma lo possono diventare ritardando l'output di uno o due campioni. 

### Sistemi stabili 
un sistema è stabile se l'input è limitato anche l'output lo è. Siano $Bx,By$ due costanti positive e $y[n]$ la risposta a $x[n]$ allora 
$$|x[n]|<Bx\implies |y[n]|<By$$
questo tipo di stabilità si chiama BIBO (bounded input, bounded output)

### Sistemi passivi e senza perdita 
Un sistema discreto si dice passivo se per ogni input con energia finita $x[n]$ la sequenza in output $y[n]$ ha almeno la stessa energia, per cui 
$$
\sum_{n=-\infty}^{\infty}|y[n]|^{2}\leq \sum_{n=-\infty}^{\infty}|x[n]|^{2}<\infty 
$$
## Impulso e Risposte a passi 
la risposta di un filtro digitale a una funzione unitaria $\updelta[n]$ è chiamata unit sample response o **risposta impulso** ed è denotata da $h[n]$. La risposta di un sistema discreto ad una sequenze a passo unitario $\mu[n]$ è una **riposta a un passo** $s[n]$. Un filtro lineare tempo invariante (LTI) è completamente caratterizzato nel dominio del tempo dalla sua risposta all'impulso.
## Caratterizzazione nel dominio del tempo di sistemi discreti LTI 
un sistema discreto tempo invariante lineare soddisfa sia il criterio di linearità che di tempo invarianza. Questi sistemi sono particolarmente semplici da analizzare matematicamente e da intersecare tra di loro per costruire sistemi discreti più complessi. 

### Relazione input-output 
una conseguenza dei vincoli a cui un LTI è sottoposto è il fatto di essere **completamente caratterizzato dalla sua risposta impulso**. Che vuol dire che conoscendola possiamo calcolare l'output del sistema ad ogni input arbitrario.

Sia $h[n]$ la risposta impulso dell'LTI di interesse all'input $\updelta[n]$. Vogliamo calcolare la risposta di questo filtro a un input , per prima cosa calcoliamo la risposta di questo filtro a un input $x[n]$ costruito usando dei pesi arbitrari, poichè il filtro è lineare la risposta a questo input 
$$
x[n]=0.5\updelta[n+2]+1.5\updelta[n-1]-\updelta[n-2]+\updelta[n-4]+0.75\updelta[n-6]
$$
sarà semplicemente 
$$
y[n]=0.5h[n+2]+1.5h[n-1]-h[n-2]+h[n-4]+0.75h[n-6]
$$

perciò una sequenza di input arbitraria $x[n]$ può essere espressa come pesi di combinazioni lineari di unit sample ritardati o avanzati nella forma 
$$
x[n]=\sum_{k=-\infty}^{\infty}x[k]\updelta[n-k]
$$
il risultato è che la risposta $y[n]$ del sistema discreto a $x[n]$ è data da 
$$
y[n]=\sum_{k=-\infty}^{\infty}x[k]h[n-k]=\sum_{k=-\infty}^{\infty}x[n-k]h[k]
$$
che è la **somma convolutiva** delle sequenza $x[n]$ e $h[n]$. La quale gode di diverse utili proprietà.
1) commutatività : $x_{1}[n]\circledast x_{2}[n]=x_{2}[n]\circledast x_{1}[n]$
2) associatività per sequenze stabili e single sided: $$(x_{1}[n] \circledast x_{2}[n]) \circledast x_{3}[n]= x_{1}[n] \circledast (x_{2}[n] \circledast x_{3}[n])$$
3) distributività $$x_{1}[n] \circledast (x_{2}[n] + x_{3}[n] ) = x_{1}[n] \circledast x_{2}[n]+ x_{1}[n] \circledast x_{3}[n]$$ una possibile interpretazione della somma convolutiva è la somma pesata e ritardata di varie versione della risposta impulso $h[n]$ (stessa cosa per la seconda versione ma per $x[n]$) , gli input ritardati del segnale sono anche chiamati **echo**. Le operazioni in questi casi sono semplici, somme , sottrazioni e moltiplicazioni. Dobbiamo però tenere conto della natura di queste sequenze, che sono di lunghezza finita, perciò va data un'altra interpretazione della somma convolutiva che tenga conto di questa limitazione. 

### Metodo tabulare per la somma convolutiva 
il calcolo della somma convolutiva per sequenze finite può essere svolto con il seguente metodo. 
Siano $g[n],0\leq n\leq 2$ e $h[n],0\leq n\leq 2$ due sequenze di cui vogliamo calcolare la convoluzione $y[n]=g[n] \circledast h[n] ,0\leq n\leq 5$
1) ogni campione di $g[n]$ è moltiplicato con $h[0]$ e i campioni della sequenza prodotto sono piazzati in una riga a n=0.
2) ogni campione di $g[n]$ è moltiplicato con $h[1]$ e  piazzati in una seconda riga a n=2
e si continua per ogni riga. 

| n      | 0          | 1          | 2          | 3          | 4          | 5          |
| ------ | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| $g[n]$ | $g[0]$     | $g[1]$     | $g[2]$     | $g[3]$     |            |            |
| $h[n]$ | $h[0]$     | $h[1]$     | $h[2]$     |            |            |            |
|        | $g[0]h[0]$ | $g[1]h[0]$ | $g[2]h[0]$ | $g[3]h[0]$ |            |            |
|        |            | $g[0]h[1]$ | $g[1]h[1]$ | $g[2]h[1]$ | $g[3]h[1]$ |            |
|        |            |            | $g[0]h[2]$ | $g[1]h[2]$ | $g[2]h[2]$ | $g[3]h[2]$ |
| $y[n]$ |            |            |            |            |            |            |

### Condizioni di stabilità in termini di risposta impulso
usando la definizione di BIBO, possiamo sviluppare condizioni di stabilità per un LTI. Per cui un filtro LTI è BIBO se la sua risposta è assolutamente sommabile 
$$S=\sum_{n=-\infty}^{\infty}|h[n]|<\infty$$
se la sequenza in input è bounded allora anche l'ampiezza in output all'istante n lo è 

$$|y[n]|=|\sum_{k=-\infty}^{\infty}h[k]x[n-k]|\leq \sum_{k=-\infty}^{\infty}|h[k]||x[n-k]|\leq B_{x}\sum_{k=-\infty}^{\infty}|h[k]|=B_{x}S<\infty$$

Così $S<\infty$ implica che $|y[n]|\leq B_{y}=B_{x}S<\infty$ , adesso si consideri l'input $x[n]=sgn(h[-n])$ con $sgc(c)= \begin{cases} +1 , c\geq 0\\-1,c<0\end{cases}$ siccome $|x[n]|=1$ è ovviamente bounded. Per questo input $y[n]$ a n=0 è 
$$y[0]=\sum_{k=-\infty}^{\infty}sgn(h[k])h[k]=\sum_{k=-\infty}^{\infty}|h[k]|=S$$
### Condizioni di causalità in termini di risposta all'impulso 
Siano $y_{1}[n],y_{2}[n]$ le sequenze in output di un LTI con una risposta $h[n]$ per le sequenze in input $x_{1}[n],x_{2}[n]$ Assumendo che 
- $x_{1}[n]=x_{2}[n];n\leq n_{0}$
- $x_{1}[n]\neq x_{2}[n];n>n_{0}$ 

le corrispondenti sequenze in output a n=n0 saranno 
$$
\begin{align}
y_{1}[n_{0}]=\sum_{k=-\infty}^{\infty}h[k]x_{1}[n_{0}-k]=\sum_{k=0}^{\infty}h[k]x_{1}[n_{0}-k]=\sum_{k=-\infty}^{-1}h[k]x_{1}[n_{0}-k]\\ \\

y_{2}[n_{0}]=\sum_{k=-\infty}^{\infty}h[k]x_{2}[n_{0}-k]=\sum_{k=0}^{\infty}h[k]x_{2}[n_{0}-k]=\sum_{k=-\infty}^{-1}h[k]x_{2}[n_{0}-k]
\end{align}
$$
per cui se il sistema è davvero causale y1 al tempo n0 deve essere uguale a y2 a n0. Come risultato sarà causale solo se la sua risposta $h[n]$ è una sequenza causale che soddisfa $h[k]=0 ; k<0$

## Schemi di interconnessione 
gli LTI più complessi sono di solito costruiti dall'assemblamento di LTI più semplici.

### Cascade 
la connessione a cascata di due LTI è data semplicemente dalla loro convoluzione $h[n]=h_{1}[n] \circledast h_{2}[n]$. In generale visto che l'ordinamento dei sistemi non ha alcun effetto sull'output grazie alla **proprietà commutativa** allora è possibile metterne un certo numero in cascata e calcolare semplicemente la loro convoluzione.  Se 2 sistemi stabili sono in cascata, il sistema che ne risulta è stabile stessa cosa se sono passivi. Un applicazione della cascata è quella di sviluppare sistemi inversi , in cui cioè $h_{1}[n] \circledast h_{2}[n]=\delta[n]$. Allora il sistema LTI $h_{2}[n]$ è detto inverso di h1, sistema utile per esempio per recuperare un segnale distorto. (backward difference system è l'inverso di un accumulatore) 

### Parallel
la risposta di due sistemi collegati in parallelo è $h[n]=h_{1}[n]+h_{2}[n]$ . Estendibile ovviamente a N sistemi connessi in parallelo, il parallelo di due sistemi stabili e stabile, ma di due sistemi passivi potrebbe non esserlo. 


## LTI a dimensioni finite 
Un importante sottoclasse degli LTI è caratterizzata dall'equazione di differenza lineare a coefficiente costante della forma 
$$
\sum_{k=0}^{N}d_{k}y[n-k]=\sum_{k=0}^{M}p_{k}x[n-k] 
$$
dove x e y sono rispettivamente l'input e l'output del sistema. Mentre d e p sono costanti. **l'ordine** del sistemi è dato dal MAX(N,M), che è l'ordine delle equazioni di differenza che caratterizzano il sistema. è possibile sviluppare un LTI con quest'equazione perchè sebbene le sommatorie siano di sequenza finita , la risposta ha invece lunghezza infinita. Se assumiamo che il sistema sia causale allora :
$$y[n]=-\sum_{k=1}^{N} \frac{d_{k}}{d_{0}}y[n-k]+\sum_{k=0}^{M} \frac{p_{k}}{d_{0}}x[n-k]$$
avendo quindi $d_{0}\neq 0$ possiamo calcolare l'output per tutti gli $n>n_{0}$ 

### Total solution calculation 
La procedura per computare la soluzione dell'equazione dei coefficienti costanti è molto simile a quella impiegata nella soluzione della stessa nel caso di un LTI continuo. La risposta in output $y[n]$ anche consiste di due componenti che sono computate indipendentemente e poi aggiunte per portare alla soluzione $y[n]=y_{c}[n]+y_{p}[n]$. In questa equazione $y_{c}$ è la soluzione  all'equazione omogenea alle differenze (la prima della sezione) con input $x[n]=0$. 
$$
\sum_{k=0}^{N}d_{k}y[n-k]=0
$$
mentre la componente $y_{p}[n]$ è la soluzione con $x[n]\neq 0$ . yc è quindi la soluzione complementare o omogenea, mentre yp è la soluzione particolare o forzata. La somma delle due porta alla soluzione totale. 
Per risolvere la soluzione complementare assumiamo che sia nella forma $y_{c}[n]=\lambda^{n}$ sostituendo nell'equazione arriviamo a 
$$
\sum_{k=0}^{N}d_{k}y[n-k]=\sum_{k=0}^{N}d_{k}\lambda^{n-k} = \lambda^{n-N}(d_{0}\lambda^{N}+d_{1}\lambda^{N-1}+\dots+d_{N-1}\lambda+d_{N})=0
$$
questo polinomio è detto polinomio caratteristico del sistema discreto con $\lambda$ le sue N radici. Se queste radici sono tutte distinte allora la forma generale della soluzione complementare è data da 
$$y_{c}[n]=\alpha_{1}\lambda_{1}^{n}+\alpha_{2}\lambda_{2}^{n}+\dots+\alpha_{N}\lambda_{N}^{n}$$
ed è anche chiamata **soluzione del transitorio** se invece sono N-L le radici distinte
$y_{c}[n]=\alpha_{1}\lambda_{1}^{n}+\alpha_{2}n\lambda_{1}^{n}+\alpha_{3}n^{2}\lambda_{1}^{n}+\dots+\alpha_{L}n^{L-1}\lambda_{1}^{n}+\alpha_{L+1}\lambda_{2}^{n}+\dots+\alpha_{N}\lambda_{N-L}^{n}$ 


## Classificazione di sistemi LTI 
di solito sono classificati in base alla lunghezza delle risposte o in base al metodo di calcolo dei campioni in output 

### Classificazione in base alla lunghezza della risposta 
se $h[n]$ è di lunghezza finita allora il sistema è conosciuto come **finite impulse response** (FIR), per cui la somma convolutiva si riduce a 
$$
y[n]=\sum_{k=N_{1}}^{N_{2}}h[k]x[n-k]
$$
con $N_{1}<N_{2}$ e $h[n]=0;n<N_{1} \lor n>N_{2}$ . Esempi sono il sistema a medie mobili o l'interpolatore lineare. 

Se la lunghezza è invece infinita allora si chiamano **infinite impulse response** (IIR). Con input causale $x[n]$  e quindi la somma convolutiva può essere espressa come 
$$
y[n]=\sum_{k=0}^{n}x[k]h[n-k]
$$
la cui complessità aumenta con n, poichè il numero di campioni con cui effettuare il calcolo aumenta, esempi sono l'accumulatore o average filter con pesi esponenziali 

### Classificazione in base al processo di calcolo dell'output 
Se l'output può essere calcolato sequenzialmente, sapendo solo il presente e l'input passati allora il filtro è detto **non ricorsivo**. Altrimenti se il filtro coinvolge anche l'output passato del filtro è detto **ricorsivo**. Un esempio di filtro ricorsivo è **l'average moving filter** . 

### Classificazione in base ai coefficienti della risposta 
A seconda che l'output di un filtro sia complesso o reale si differenziano anche i sistemi. 

## Rappresentazione nel dominio della frequenza
Le sinusoidali possono essere compose partendo da combinazioni lineari di diverse frequenze angolari. Per questo conoscendo la risposta a una sinusoide semplice di un LTI possiamo determinarne anche la risposta a un onda più complessa. 

### Risposte in frequenza 
Un importante proprietà di un LTI è che per certi tipi di input, chiamati eigenfunctions il segnale in output è l'input moltiplicato per una costante complessa. Sia $x[n]=e^{ j\omega n }$ la eigenfunction in input. l'output sarà quindi, per la relazione input-output 
   $$y[n]=\sum_{k=-\infty}^{\infty}h[k]e^{ j\omega(n-k) }=\left( \sum_{k=-\infty}^{\infty}h[k]e^{ -j\omega k } \right)e^{ j\omega k }=H(e^{ j\omega })e^{ j\omega n }$$dove $H(e^{ j\omega })=\sum_{n=-\infty}^{\infty}h[n]e^{ -j\omega n }$ chiamata **risposta i frequenza**  , e darà una descrizione nel dominio delle frequenze del sistema (in questo caso è la trasformata di Fourier di h). Quindi per una sinusoidale complessa di frequenza angolare $\omega$ l'output anche è una sinusoidale complessa ma pesata da un ampiezza complessa $H(e^{ j\omega })$ che è una funzione della frequenza in input $\omega$ . 

Come ogni altra DTFT anche $H(e^{ j\omega })$ è una funzione complessa di $\omega$ con periodo $2\pi$ e può essere espressa in termini di 
$$
H(e^{ j\omega })=H_{\mathrm{Re}}(e^{ j\omega })+jH_{\mathrm{Im}}(e^{ j\omega })=|H(e^{ j\omega })|e^{ j\theta(\omega) }
$$
dove:
- $\theta(\omega)=arg\{H(e^{ j\omega })\}$ => **fase della risposta**  
- $|H(e^{ j\omega })|$ =>  **magnitudine della risposta** .

un esempio di magnitudine della risposta sono i decibel in un suono.
$$\mathcal{G}(\omega)=20\log_{10}|H(e^{ j\omega })|dB$$
dove la funzione G è la funzione di gain, che quando negativizzata $A(\omega)=\mathcal{G}(\omega)$ viene chiamata attenuazione o **funzione di perdita**.

### Caratterizzazione nel dominio delle frequenze degli LTI 

Deriviamo la rappresentazione nel dominio delle frequenze di un LTI stabile. Sia  $Y(e^{ j\omega }),X(e^{ j\omega })$ le trasformate di fourier dell'output e dell'input. Applicando la convoluzione otteniamo che 
$$
Y(e^{ j\omega })=H(e^{ j\omega })X(e^{ j\omega })
$$
dove H è la risposta in frequenza del sistema. Otteniamo quindi 
$$H(e^{ j\omega })= \frac{Y(e^{ j\omega })}{X(e^{ j\omega })}$$
per cui la risposta in frequenza del sistema è data dal rapporto tra le trasformate dell'input e dell'output.

### Risposta in frequenza degli LTI 

#### FIR 
gli LTI FIR sono caratterizzati dalla relazione input output $y[n]=\sum_{k=N_{1}}^{N_{2}}h[k]x[n-k]$ . Applicando una DTFT arriviamo a $$
Y(e^{ j\omega })=\sum_{k=N_{1}}^{N_{2}}h[k]e^{ -j\omega k }X(e^{ j\omega })
$$
dove X e Y sono le trasformate di input e output. Da questa equazione deriviamo 
$$H(e^{ j\omega })=\sum_{k=N_{1}}^{N_{2}}h[k]e^{ -j\omega k }$$
#### IIR 
sono caratterizzati dalla equazione alle differenze con coefficienti costanti $\sum_{k=0}^{N}d_{k} y[n-k]=\sum_{k=0}^{M}p_{k}x[n-k]$ . Applicandogli Fourier facendo uso della linearità e della tempo invarianza arriviamo a 
$$\sum_{k=0}^{N}d_{k}e^{ -j\omega k }Y(e^{ j\omega })=\sum_{k=0}^{M}p_{k}e^{ -j\omega k }X(e^{ j\omega })$$
a questo punto deriviamo la risposta in frequenza 
$$H(e^{ j\omega })=\frac{Y(e^{ j\omega })}{X(e^{ j\omega })}= \frac{\sum_{k=0}^{M}p_{k}e^{ -j\omega k }}{\sum_{k=0}^{N}d_{k}e^{ -j\omega k }}$$
### Soluzione del transitorio e stabile 
parlando delle soluzioni di un LTI finito, ci si è riferiti a $y_{c}[n]$ come la soluzione del transitorio $$y_{c}[n]=\alpha_{1}\lambda_{1}^{n}+\alpha_{2}\lambda_{2}^{n}+\dots+\alpha_{N}\lambda_{N}^{n}$$
Supponendo un input della forma $x[n]=A \cos(\omega_{0}n+\phi)$ con A reale, abbiamo che la soluzione del transitorio è $y_{c}$ mentre quella stabile , dopo opportuni calcoli si riduce alla costante di ampiezza $x[n]=A$ e perciò $y[n]=A|H(e^{ j_{0} })|$
### Risposta a una sequenza causale esponenziale 
Il sistema LTI di solito viene applicato a un insieme ristretto di una sequenza partendo da $n_{0}$ , per cui esibirà caratteristiche transitorie e stabili assieme. Sia una x una sequenza esponenziale  $x[n]=e^{ j\omega n }\mu [n]$ dove $\mu[n]$ è la unit step sequence. Siccome $x[n]=0$ per n<0 abbiamo $y[n]=0$ per n<0. Invece per $n\geq 0$ abbiamo 
$$
y[n]=\sum_{k=0}^{\infty}h[k]e^{ j\omega(n-k) }\mu[n-k]=\left( \sum_{k=0}^{n}h[k]e^{ -j\omega k } \right)e^{ j\omega n }
$$
per $k>n$ riscriviamo l'espressione ottenendo 
$$
y[n]=\left( \sum_{k=0}^{\infty}h[k]e^{ -j\omega k } \right)e^{ j\omega n }-\left( \sum_{k=n+1}^{\infty}h[k]e^{ -j\omega k } \right)e^{ j\omega n }= H(e^{ j\omega })e^{ j\omega n }-\left( \sum_{k=n+1}^{\infty}h[k]e^{ -j\omega k } \right)e^{ j\omega n }
$$

Il primo termine è la risposta stabile 
$$y_{sr}[n]=H(e^{ j\omega })e^{ j\omega n }$$
la seconda è la risposta transitoria 
$$y_{tr}[n]=-\left( \sum_{k=n+1}^{\infty}h[k]e^{ -j\omega n } \right)e^{ j\omega n }$$
## Il concetto di filtraggio 
Un compito degli LTI è passare un segnale a un filtro per rimuoverne certe componenti in frequenza. La chiave di questo meccanismo è la trasformata inversa di Fourier che può esprimere una sequenza di input arbitraria come somma pesata di un numero infinito di sequenze esponenziali o come somma pesata lineare di sequenze sinusoidali. Quindi scegliendo opportunamente i pesi possiamo attenuare o filtrare alcuni range di frequenza. Consideriamo un LTI con magnitudine  $|H(e^{ j\omega })|=\begin{cases}1, & 0\leq |\omega|\leq \omega_{c}\\0,& \omega_{c}\leq |\omega|<\pi\end{cases}$
a cui applichiamo $x[n]=A\cos \omega_{1}n+B\cos \omega_{2}n$ dove $0<\omega_{1}<\omega_{c}<\omega_{2}<\pi$
 Grazie alla linearità, l'output sarà 
$$
y[n]=A|H(e^{ j\omega_{1} })|\cos(\omega_{1}n+\theta(\omega_{1}))+B|H(e^{ j\omega_{2} })|\cos(\omega_{2}n+\theta(\omega_{2}))
$$
considerando la magnitudine otterremo 
$$
y[n]\approx A|H(e^{ j\omega_{1} })|\cos(\omega_{1}n+\theta(\omega_{1}))
$$
perciò il sistema sta agendo come un filtro passa basso 

### Design di un semplice filtro 
consideriamo un input che consiste nella somma di due frequenze coseno di frequenza angolare 0.1 rad/campione e 0.4 rad/campione. Vogliamo costruire un filtro passa alto che blocchi le parti basse della frequenza. Assumiamo che sia un filtro FIR con lunghezza 3 e con risposta implusiva $h[0]=h[2]=\alpha_{0},h[1]=\alpha$. Per cui il filtraggio è effettuato usando l'equazione alle differenze 
$$
y[n]=h[0]x[n]+h[1]x[n-1]+h[2]x[n-2]=\alpha_{0}x[n]+\alpha_{1}x[n-1]+\alpha_{0}x[n-2]
$$
dove y è l'output e x è l'input. Per cui ora bisogna scegliere opportunamente $\alpha_{0},\alpha_{1}$ così che l'output sia una cosinusoide con frequenza 0.4 rad/campione. La risposta in frequenza di questo filtro è data da 
$$
\begin{align}
H(e^{ j\omega })=h[0]+h[1]e^{ -j\omega }+h[2]e^{ -j 2 \omega } = \alpha_{0}(1+e^{ -j 2 \omega })+\alpha_{1}e^{ -j\omega }=2\alpha_{0}\left( \frac{{e^{ j\omega }+ e^{ -j\omega }}}{2}  \right)e^{ -j\omega }+\alpha_{1}e^{ -j\omega }\\=(2\alpha_{0}\cos \omega+\alpha_{1})e^{ -j\omega }
\end{align}
$$
dove:
- magnitudine $|H(e^{ j\omega })|=|2\alpha_{0}\cos \omega+\alpha_{1}|$ 
- fase $\theta(\omega)=-\omega+\beta$
    - $\beta=0$ quando $2\alpha_{0}\cos \omega+\alpha_{1}>0$ 
    - $\beta=\pi$ quando $2\alpha_{0}\cos \omega+\alpha_{1}<0$

per fermare la bassa frequenza, la funzione di magnitudine deve essere 0 con $\omega=0.1$, mentre a $\omega=0.4$ deve essere 1. Quindi 
$$
\begin{align}
2\alpha_{0}\cos(0.1)+\alpha_{1} =0\\
2\alpha_{0}\cos(0.4)+\alpha_{1}=1
\end{align}
$$
risolvendole si arriva a $\alpha_{0}=-6.761$ e $\alpha_{1}=13.456$ sostituendo nell'equazione del FIR otteniamo 
$$
y[n]=-6.761(x[n]+x[n-2])+13.456x[n-1]
$$
con $x[n]=\{\cos(0.1n)+\cos(0.4n)\}\mu[n]$

## Ritardo della fase e del gruppo
