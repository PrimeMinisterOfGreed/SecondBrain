# Simulazioni a orizzonte finito
Una simulazione con orizzonte finito è quella che ha un tempo operativo finito, sono anche chiamate simulazioni terminanti. Spesso si suppone che il sistema sia fermo all'inizio e alla fine della simulazione. Le condizioni di terminazione potrebbero essere specificate ad esempio da un certo punto nel tempo che termina la simulazione.
- **Questa simulazione produce statistiche del transitorio**.
- Le condizioni iniziali **hanno impatto** sulle statistiche del transitorio 
- Non c'é bisogno di assumere un ambiente statico 
## Condizioni di terminazione
A seconda delle misure scelte questo possono essere espresse in termini di tempo passato nella simulazione o numero di eventi processati. 

Nel caso ad esempio di una coda a singolo server vorremmo stimare : 
1. il numero medio di clienti fino al tempo T 
2. il tempo medio d'attesa w sperimentato dai primi N clienti 

formalmente 
1)  $n(\cdot)$ è anche conosciuto come processo stocastico. tipicamente il suo obiettivo è di stimare la statistica transiente $\bar{n}(T)=\frac{1}{T} \int^{T}_{0}n(t) dt$  => numero di clienti medio.
2) $W_i$ anche è un processo stocastico. tipicamente il suo obiettivo è stimare la statistica transiente $\bar{W}(N)= \frac{1}{N}\sum^{N}_{i=1}W_i$ => tempo d'attesa medio.


## Repliche indipendenti
i campioni raccolti durante una simulazione non sono indipendenti (l'output è correlato), perciò nonostante sia possibile calcolare media e varianza queste non sono indipendenti, per cui bisogna adottare delle tecniche .

La simulazione può essere ripetuta variando solo il seme del generatore, il campione così ottenuto è un super-campione di campioni.
Il seme va scelto così che non ci siano sovrapposizioni tra le simulazioni, tipicamente lo stato finale del sistema viene usato come stato iniziale della prossima simulazione.
### Replication and interval estimation
supponiamo che la simulazione sia replicata p volte, ogni volta generando uno stato  $x_i(t)$ -> $\bar{x_i}(T)=\int^{T}_{0}x_i(t) dt$  dove i è l'indice della replica.

- Ogni dato $\bar{x}_i(T)$ è un'osservazione indipendente della variabile aleatoria $\bar{X}(T)$ 
- con p grande abbastanza, la densità di $\bar{X}(T)$ può essere stimata tramite un istogramma di  $\bar{x}_i(T)$  

nello specifico se vogliamo $E[\bar{X}(T)]$ :
- uno stimatore puntuale è disponibile come media campionaria $\hat{\micro}=\frac{1}{p}\sum^{p}_{i=1}\bar{x}_i(T)$ 
- una stima intervallare per $E[\bar{X}(T)]$ può essere calcolata: usando la tecnica delle [[Stime Intervallari]] . cosa che però richiede varianza e media campionaria di $\bar{x}_i(T)$.


Per stimare $\bar{n}(T)$ e $\bar{W}(N)$, ricorriamo al seguente procedimento:

sia : $n(T)$ => numero di clienti nel sistema al tempo T
supponiamo di voler ottenere $E[n(T)]$:
n(T) è una variabile aleatoria, il risultato al tempo T  è un istanza anch'esso di una variabile aleatoria , in generale la distribuzione di n(T) è molto lontana dall'essere approssimativamente normale. 

Ripetere la simulazione molte volte produce dati che sono difficili da analizzare con le tecniche standard di stima intervallare, motivo per il quale di solito si suddivide il campione in $\frac{p}{K}$  sotto-campioni, una buona mossa per calcolare i risultati medi con gli opportuni intervalli di confidenza che possono essere usati come insieme di misure per altre computazioni.


### Probabilità di giacere in un certo intervallo

Assumiamo un insieme di p osservazioni della variabile aleatoria  $Y_i \in Y,i=1...p$ ottenuta da p osservazioni indipendenti. Vogliamo stimare la probabilità che Y assuma valori entro l'intervallo I.
Sia:
- $\psi = Prob\{Y \in I\}$ 
- X una variabile aleatoria derivata da Y in questo modo $X_i= \begin{cases} 1 \ \  \ Y_i \in i \\ 0\end{cases}$   
Allora $E[X]=E[X_i]=\psi$ .
Sia:
- m => numero di elementi in $Y_i$ che appartengono a I allora ->$m = \sum^{p}_{i=1}X_i$ 

lo stimatore non polarizzato di questa probabilità è $$\psi = \frac{1}{p}\sum^{p}_{i=1}X_i=\frac{m}{p}$$ dove:
- $E[\psi]=\frac{1}{p}\sum^{p}_{i=1}E[X_i]=\psi$ 
- $VAR[\hat{\psi}]=\frac{\psi(1-\psi)}{p}$ 

m ha distribuzione binomiale con:
- parametro $\psi$  --> $Prob\{m=k\}= \frac{p!}{k!(p-k)!} \psi^k(1-\psi)^{p-k}$ 
- valore atteso $E[m]=p \psi$  
- varianza $VAR[m]=p \psi(1-\psi)$ 

stimare $\psi$ è equivalente a stimare un parametro di una distribuzione binomiale con:
$\psi$  $Prob\{\hat{\psi}_L \leq \psi \leq \hat{\psi}_U\}$ => probabilità di successo 

dove: $\hat{\psi}_L$ e $\hat{\psi}_U$ possono essere ottenuti risolvendo le seguenti equazioni: 
- $\sum^{p}_{k=m}[\frac{p!}{k!(p-k)!} \psi_L^k(1-\psi_L^k)^{p-k}] = \frac{\alpha}{2}$  for $\psi_L$      
- $\sum^{m-1}_{i=0}[\frac{p!}{k!(p-k)!} \psi_U^k(1-\psi_U^k)^{p-k}] = \frac{\alpha}{2}$  for $\psi_U$    

quando  p è grande e sia m che p-m sono  > 5  una maniera più semplice per ottenere l'intervallo di confidenza di  $\psi$ è usare una **distribuzione normale come approssimazione di una binomiale** . cosi da poter dire che  $\hat{\psi}$ ha una distribuzione normale con media $\psi$ e varianza $\frac{\psi(1-\psi)}{p}$  

usando quindi la seguente variabile ausiliaria $Z=\frac{\hat{\psi} - \psi}{\sqrt{\psi(1-\psi}/p}$ , che ha una distribuzione normale standardizzata possiamo cercare $Pr(-z_{\alpha/2} \leq Z \leq z_{\alpha/2}) = 1-\alpha$  per cui l'intervallo di confidenza desiderato diventa

$$
Pr\{\frac{m}{p}-z_{\alpha/2}\sqrt{\frac{m(p-m)}{p}} \leq \psi \leq Pr\{\frac{m}{p}+z_{\alpha/2}\sqrt{\frac{m(p-m)}{p}}\}= 1-\alpha
$$
### Tempo d'attesa del k-esimo cliente (jackknifing)
Sia:
- $W_k^{[i]} :i =1,2,...p$ => campione formato dal tempo d'attesa del solo k-esimo cliente.
- media: $\bar{W}_k=\frac{1}{p}\sum^{p}_{i=1}W_k^{[i]}$  
- varianza: $\hat{s}^2_{W_k}=\frac{1}{p-1}\sum^{p}_{i=1}(W_k^{[i]} - \bar{W}_k)^2$ 

otteniamo l'intervallo di confidenza per  $\micro = E[W_k]$  --> $$Pr\{\bar{W}_k-t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_{W_k}}{\sqrt{p}} \leq \micro \leq \bar{W}_k+t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_{W_k}}{\sqrt{p}}\} \approx (1-\alpha)$$ 
Calcoliamo lo stimatore puntuale per la varianza:

$$\hat{s}^2 = \frac{1}{p-1}\sum^{p}_{i=1}(W_k^{[i]}-\bar{W}_k)^2$$  con $E[\hat{s}^2]=\sigma^2$

suddividiamo il campione originale in un altro sotto-campione in cui manca la j-esima osservazione $(W_k)_j=\{ w_{i} \in W| i\neq j \}$:
- media: $\bar{W_k}_j=\frac{1}{p-1}\sum^{p}_{i=1;i \neq j}W_k^{[i]}$        
- varianza: $\hat{s}^2=\frac{1}{p-2}\sum^{p}_{i=1;i \neq j}(W_k^{[i]})^2 - \frac{p-1}{p-2}\bar{(W_k)_j^2}$ 


Sia:  $Z_j=p \hat{s}^2- (p-1)\hat{s}_j^2$  
sapendo che  $E[Z_j]=\sigma^2$ possiamo formare un nuovo campione $Z_i$ che ha:
- media: $\bar{Z}=\frac{1}{p}Z_j$
- varianza: $\hat{s}_Z^2=\frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$ 

definiamo quindi $\Upsilon = \frac{(\bar{Z}-\sigma^2)}{s_Z/\sqrt{p}}$ , che una variabile aleatoria distribuita come una t-student con p-1 gradi di libertà, ora otteniamo l'intervallo di confidenza per $\sigma^2$ 
$$
Pr\{\bar{Z} - t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_Z}{\sqrt{p}} \leq \sigma^2 \leq \bar{Z} + t_{(p-1,\frac{\alpha}{2})} \frac{\hat{s}_Z}{\sqrt{p}} \} \approx (1-\alpha)
$$

questo metodo è anche conosciuto come jackknifing

# Simulazioni con orizzonte infinito 
 Questo tipo di simulazioni genera dati statistici a regime, in this case the initial conditions doesn't affect the statistics produced (system loses memory of the initial state). In questo caso l'ambiente è assunto essere statico.


## Condizioni di terminazione
a seconda delle statistiche che si vogliono raccogliere, le condizioni di terminazione possono essere le più disparate.

In generale le variabili di stato $X(t)$ e $Y_i$ di un sistema sono conosciute come processi stocastici.

Tipicamente gli obiettivi sono:
- statistiche a regime temporali : $\bar{x} = \lim_{T \rightarrow \infty} \frac{1}{T} \int^{T}_{0}X(t)dt$ 
- statistiche a regime discretizzate: $\bar{y}=\lim_{N \rightarrow \infty} \frac{1}{N} \sum^{N}_{i=0}Y_i$ 
sia $\bar{x}$ che $\bar{y}$ **non sono variabili aleatorie** .


usando $\{W_n:n =1,2,3,...\}$ supponiamo di essere interessati a calcolare la distribuzione dei tempi di attesa a regime: $\lim_{n \rightarrow \infty} Prob\{W_n \leq x\} = F(x)$.
come nel caso dell'analisi del transitorio siamo interessati a stimare media e varianza di questa variabile. 

In questo caso non abbiamo bisogno di repliche indipendenti, perchè tutte le variabili aleatorie hanno la medesima distribuzione. Ci sono degli elementi comunque che vanno presi in considerazione:
- l'osservazione delle variabili aleatorie va effettuata dopo un certo numero di osservazioni preliminari 
- Siccome i risultati in una singola simulazione sono altamente correlati, le tecniche statistiche standard non restituiscono i risultati voluti perchè le variabili aleatorie non sono indipendenti 

## Lunghezza del transitorio iniziale
le condizioni **non devono** :
- avere impatti sul comportamento a regime 
- richiedere una simulazione molto lunga prima di diventare a regime 

l'effetto di queste osservazioni è che dobbiamo scartare un periodo iniziale della simulazione. Identificare queste condizioni è un compito difficile e va fatto mediante simulazioni di prova (pilot simulations).  L'idea è di costruire un campione statistico fatto da queste osservazioni iniziali , così che quando comparate con le distribuzione a regime si possa identificare la condizione per cui il sistema è entrato a regime.


### Confrontare le distribuzioni  
Sia:
- $Y(t)$ => di clienti al tempo t, supponiamo di aver fatto un buon numero di osservazioni 
- $t_1,t_2,...,t_n$ --> $\{Y_i(t_n),i=1...p\} \ \ n=1,2,3...$ 
- $m_k(t_n)$ => numero di volte $Y_i(t_n) = k$ --> $\{m_k(t_n),k=1...N_{max}\}$ 
-  $\psi_k(t_n)$ => probabilità di osservare k clienti nel sistema a  $t_n$ 
Cosi possiamo calcolare $\{\psi_k(t_n)=\frac{m_k(t_n)}{p}\} \ \ k=1...N_{max}$ 
dove:
- al più $N_{max}$ clienti sono stati osservati nel sistema. 

Il transitorio iniziale è definito come indice n dove la differenza tra $t_n$ e $t_{n+1}$ diventa più piccola di una certa soglia
$$
t_n:min_n\{\frac{\sum^{N_{max}}_{k=1}[\psi_k(t_n)-\psi_k(t_{n+1}]^2}{N_{max}} < \epsilon\}
$$


### Confrontare i momenti
confrontare le distribuzioni richiede un grande ammontare di dati, una via alternativa è quella di comparare i momenti, in questo modo:
$$
t_n^{[h]}:min_n\{|\frac{\sum^{p}_{i=1}[Y_i(t_n)]^h}{p} - \frac{\sum^{p}_{i=1}[Y_i(t_{n+1})]^h}{p}|<\epsilon\}
$$
Momenti differenti portano informazioni diverse, così che la lunghezza del periodo corrente possa essere calcolata come $t_n:max_h\{t_n^{[h]}\}$ , il costo computazionale è comunque alto, perciò si raccomanda di ridurlo ai primi momenti. 

### Media mobili
Le medie calcolate a differenti istanti di tempo possono oscillare, per cui è possibile utilizzare le medie mobili :

sia:
- $\hat{\micro}(t_n)$ la media campionaria calcolata al tempo $t_n$ =>$\hat{\micro(t_n)}= \frac{\sum^{p}_{i=1}Y_i(t_n)}{p}$ 

da queste quantità derivate possiamo calcolare le medie su 2L+1 istanti sequenziali $$\hat{\micro}^{[L]}(t_n)= \frac{\sum^{L}_{i=-L}\hat{\micro}(t_{n+i})}{2L+1}$$


### Confrontare l'auto correlazione
possiamo identificare la lunghezza del periodo iniziale usando l'auto correlazione: ossia la **misura dell'influenza tra le osservazioni**

Sia 
- $\{Y_1,Y_2,...,Y_n\}$ => un campione di variabili aleatorie indipendenti.

 1. Calcolare la funzione di autocorrelazione $Cov(d)= \frac{1}{N-d}\sum^{N-d}_{i=1}(Y_i-E[Y])(Y_{i+d}-E[Y])$
 2.  Siccome non conosciamo $E[Y]$ possiamo approssimarla con una covarianza sperimentale $\phi(d)=\frac{1}{N-d-1}\sum^{N-d}_{i=1}(Y_i-\bar{Y})(Y_{i+d}-\bar{Y})$ , con la media campionaria $\bar{Y}$ espressa come di consueto.

$\phi(0)$ è equivalente alla varianza $\hat{s}^2$, possiamo quindi calcolare la covarianza sperimentale come $\rho(d)=\frac{\phi(d)}{\hat{s}^2}$  che è una auto covarianza normalizzata nell'intervallo (-1,1)

valori vicini a 0 significano che l'influenza tra le osservazioni è poca. così possiamo cercare questo valore per determinare la fine del periodo transitorio $d_0=min_d\{|\rho(d)| \leq \epsilon \}$.

## Superare le dipendenze statistiche tra le osservazioni 

sia:
- $Y_n$ => un set di variabili aleatorie indipendenti 

vogliamo stimarne le caratteristiche, possiamo considerare questo insieme come insieme di **istanze della stessa** variabile aleatoria ma con elementi altamente correlati, abbiamo bisogno perciò di un metodo che riduca questa correlazione:

- Repliche indipendenti 
- Batch means
- Punti di rigeneramento


## Repliche indipendenti
i componenti del campione ottenuto facendo girare la simulazione molte volte devono essere raccolti a queste condizioni:
- le condizioni iniziali devono essere sempre le stesse
- il periodo iniziale di simulazione va scartato con le metodologie di prima

### Media e varianza 
determinato $n_0$ eseguiamo p simulazioni indipendenti e otteniamo una sequenza di variabili di interesse $\{ Y_{j1},Y_{j2},...,Y_{jn_0},...,Y_{jk},...,Y_{jN}:j=1...p \}$   da ognuna di queste osservazioni costruiamo il campioni che ci servirà per effettuare le nostre misure

Come per il caso del transitorio possiamo facilmente calcolare le stime intervallari. 

partendo dalla media: $\bar{Y}_j = \frac{1}{N-n_0}\sum^{N}_{k=n_0+1}Y_{jk}$, i dati possono essere organizzati in questo modo
$$
\begin{aligned}
\{ Y_{11},Y_{12},...,Y_{1n_0},...,Y_{1k},...,Y_{1N}\} \Rightarrow \bar{Y}_1
\\
\{ Y_{21},Y_{22},...,Y_{2n_0},...,Y_{2k},...,Y_{2N}\} \Rightarrow \bar{Y}_2
\\
\{ Y_{p1},Y_{p2},...,Y_{pn_0},...,Y_{pk},...,Y_{pN}\} \Rightarrow \bar{Y}_p
\end{aligned}
$$
da questi valori calcoliamo 
- la media campionaria $\hat{\micro}=\bar{Y} =\frac{1}{p}\sum^{p}_{j=1}\bar{Y}_j$ 
- la varianza campionaria  $\hat{s}^2 = \frac{1}{p-1}\sum^{p}_{j=1}(\bar{Y_j} - \bar{Y})^2$ 

quando $N-n_0$ è grande queste  variabili aleatorie si può assumere abbiano una distribuzione t-student perciò l'intervallo di confidenza è $$Pr\{\bar{Y} - t_{p-1,\alpha/2}\sqrt{\hat{s}^2/p} \leq \micro \leq \bar{Y} + t_{p-1,\alpha/2}\sqrt{\hat{s}^2/p}\} \approx 1- \alpha$$  
Anche qui la dimensione del campione ha importanti effetti sulla larghezza dell'intervallo agendo quindi su la dimensione del campione P e sul numero di osservazioni N si possono avere importanti effetti su $\hat{s}^2$ 

quando p>40 la t-student è approsimativamente una normale, si può quindi sostituire $t_{p-1,\alpha/2}$ con $z_{\alpha/2}$ 

### Probabilità di giacere in un certo intervallo 
stimare come nell'altro caso $\psi_n=Pr\{Y^{[n]} \in I\}$ 
dove:
- $Y^{[n]}$è la variabile di interesse durante il periodo d'osservazione n. 

Possiamo assumere che  $\psi = \lim_{n \rightarrow \infty} \psi_n$ . Poichè aver determinato $n_0$ possiamo assumere che il processo sia stazionario e che quindi $\psi_n \approx \psi$ . 

Dato $n_0$  eseguiamo p sessioni che daranno una stima intervallare per $\psi$  con risultato l'insieme $\{Y_{ij} :i=1..p;j=1...N\}$  assumendo $N>>n_0$ .Per ogni simulazione calcoliamo la stima non polarizzata $\hat{\psi}_i=\frac{v_i}{N-n_0}$ . 
Dove:
- $v_i$ => numero di volte Y cade in I. 

Cosi i valori ottenuti $\hat{\psi}_i$ sono indipendenti --> $E[\hat{\psi}_i]=\psi$ 

Possiamo quindi calcolare :
- Media $\hat{\psi}= \frac{1}{p}\sum^{p}_{i=1}\hat{\psi}_i$   
- varianza $\hat{s}^2(\hat{\psi})=\frac{1}{p-1}(\hat{\psi}_i - \hat{\psi})^2$ . 

Come di consueto, definiamo  $Z = \frac{\hat{\psi}-\psi}{\sqrt{\hat{s}^2(\hat{\psi})/p}}$ che è una t-student(p-1). 
esprimiamo l'intervallo di confidenza con $Pr\{\hat{\psi}-t_{p-1,\alpha/2}\frac{s(\hat{\psi})}{\sqrt{p}} \leq \psi \leq \hat{\psi}+t_{p-1,\alpha/2}\frac{s(\hat{\psi})}{\sqrt{p}}\}$ 
Dove:
- se p è grande possiamo rimpiazzare  $t_{p-1,\alpha/2}$ con $z_{\alpha/2}$ .

## Batch means
I componenti del campione sono ottenuti con una lunga sessione, scartando i campioni che fanno parte del periodo transitorio e dividendo questo campione massiccio in p sottocampioni, che si suppone siano scorrelati grazie all'intervallo di tempo che intercorre tra di essi. 

### Scartare il transitorio
è raccomandabile usare la tecnica dell'autocorrelazione per individuare il transitorio.

Sia:
- $Y_{i,j}$ la j-esima osservazione appartenente alla sequenza i-esima. 
- $\{Y_{i,j}:j=1...m\}$ => sotto-sequenza dal campione di riferimento 
- $\{Y_{i+1,j}:j=1...m\}$ altra sotto-sequenza dal campione di riferimento con $m>n_0$ 

a queste condizioni le due sequenze sono indipendenti,ripetendo queste considerazioni per le coppie $\{Y_{i+1,j};Y_{i,j}\}$ j=2...m , possiamo considerare il campione composto da osservazioni indipendenti . Che ci consente di applicare le stesse tecniche di indagine statistica usate per le repliche indipendenti

### Media e varianza
Possiamo calcolare un insieme composto da medie così
$$
\bar{Y}_j=\frac{1}{N-n_0}\sum^{n_0+(j+1)*m}_{k=n_0+j*m+1}Y_{jk}
$$
organizzare i dati in questo modo
$$
\begin{aligned}
\{ Y_{11},Y_{12},...,Y_{1n_0},...,Y_{1k},...,Y_{1N}\} \Rightarrow \bar{Y}_1
\\
\{ Y_{21},Y_{22},...,Y_{2n_0},...,Y_{2k},...,Y_{2N}\} \Rightarrow \bar{Y}_2
\\
\{ Y_{p1},Y_{p2},...,Y_{pn_0},...,Y_{pk},...,Y_{pN}\} \Rightarrow \bar{Y}_p
\end{aligned}
$$
e applicare le tecniche precedenti 

## Metodo Rigenerativo
I componenti del campione sotto ottenuti da una sola simulazione divisa in cicli rigenerativi che si verificano ogni **punto di rigeneramento** . 

 ⚠ punto di rigeneramento => **dove il processo stocastico simulato naturalmente perde memoria del suo passato**.

### Condizioni iniziali
- I componenti del campione sono derivati da successivi cicli di rigeneramento
- I cicli rigenerativi sono sotto-sequenze di lunghezza aleatoria identificate durante la simulazione, **iniziando da uno di questi punti è possibile evitare di sprecare la parte iniziale della simulazione** . 
- le variabili aleatorie in sequenze diverse sono **indipendenti e identicamente distribuite
- Se la sequenza è rigenerativa e tengono alcune deboli condizioni allora il sistema è a regime
![[Pasted image 20231118103525 1.png]]
da questa coda possiamo prendere le seguenti sotto-sequenze $\{W_1,W_2,W_3,W_4,W_5,W_6,W_5\}$ , $\{W_8,W_9\}$ , $\{W_{10},W_{11},W_{12},W_{13}\}$  caratterizzato dal fatto che il primo elemento della sotto-sequenza è il tempo d'attesa di un cliente che arriva e trova il sistema vuoto. Le sotto-sequenze sono chiamati **cicli di rigeneramento** e possono essere organizzati in questo modo
$$
\begin{aligned}
\{ W_{11},W_{12},...,W_{1k},...,W_{1m_1}\} 
\\
\{ W_{21},W_{22},...,W_{2k},...,W_{2m_2}\}
\\
\{ W_{p1},W_{p2},...,W_{pk},...,W_{pm_p}\}
\end{aligned}
$$

### Considerazioni iniziali
Sia:
- $A_j=\sum^{m_j}_{k=1}W_{jk}$ la somma dei tempi d'attesa osservati durante il j-esimo ciclo di rigeneramento. 
Dove: 
- $m_j$ => numero di clienti serviti durante il ciclo di rigeneramento, che può essere usato come indicazione della lunghezza del ciclo

Così da ogni ciclo di rigeneramento otteniamo:
- $\bar{W}_j=\frac{1}{m_j}\sum^{m_j}_{k=1}W_{jk}=\frac{A_j}{m_j}$=> che è un rateo da due variabili correlate  

In forma generica si può esprimere come $A_j= \int^{\beta_j}_{\beta_{j-1}}n(t)dt$ calcolato nel j-esimo ciclo di rigeneramento. Denotando con:
- $\delta_j=\beta_j-\beta_{j-1}$ la lunghezza del ciclo 

otteniamo uno stimatore puntuale: =>  $\bar{n}_j=\frac{1}{\delta_j}\int^{\beta_j}_{\beta_{j-1}}n(t)dt=\frac{A_j}{\delta_j}$ .

Simulando fino ad ottenere P cicli di rigeneramento otteniamo delle osservazioni che sono altamente correlate e su cui le normali tecniche statistiche non funzionano. Questo porta a far si che la distribuzione di  $\bar{W}_i$ è diversa da quella di  $\bar{W}$. Perciò è bisogna prendere in considerazione la natura correlata di misure che vengono da diversi cicli di rigeneramento. 

SIa $Y$ un parametro che vogliamo misurare, possiamo riassumere le osservazioni con coppie di valori identicamente e indipendentemente distribuiti$\{(A_1,v_1),...,(A_p,v_p)\}$ 
Dove:
- $A_j$ è la somma o l'integrale di Y calcolato durante il j-esimo ciclo di rigeneramento
- $v_j$ è la lunghezza del ciclo di rigeneramento, contato come occorrenze di  $Y$ oppure come distanza di tempo tra i suoi terminali. 


### Stima puntuale
Sotto alcune condizioni è possibile mostrare che: $E[\hat{r}] = r = \frac{E[A_1]}{E[v_1]}=\frac{E[A_j]}{E[v_j]}$ 
così che $\hat{r}$ è lo stimatore puntuale della variabile d'interesse. 

Sia:  $Z_j=A_j-rv_j$ 
- Media $E[Z_j]=0$
- Varianza $VAR[Z_j]=VAR[A_j]-2rCOV[A_j,v_j]+r^2VAR[v_j]$  , la covarianza è presente a causa della natura correlata del rateo. 

Definiamo quindi $\bar{Z} = \frac{1}{p}\sum^{p}_{j=1}Z_j=\bar{A}-r \bar{v}$ :
- Media:$E[\bar{Z}]=0$ 
- $VAR[\bar{Z}]=\frac{VAR[Z_j]}{p}=\frac{\sigma^2_Z}{p}$.

Il teorema del limite centrale ci permette di dire che $$\frac{\bar{Z}}{\sigma_z/\sqrt{p}}=\frac{\bar{A}-r \bar{v}}{\sigma_Z/\sqrt{p}}= \frac{\bar{A}/\bar{v}-r}{\sigma_Z/(\bar{v}\sqrt{p})}=\frac{\hat{r}-r}{\sigma_Z/(\bar{v}\sqrt{p})}$$ha una distribuzione normale standardizzata . così che possiamo calcolare  $$Pr\{\hat{r}-z_{\alpha/2}\frac{\sigma_Z}{\bar{v}\sqrt{p}} \leq r \leq \hat{r}+z_{\alpha/2}\frac{\sigma_Z}{\bar{v}\sqrt{p}}\} \approx 1-\alpha$$ 
purtroppo però $\sigma^2_Z$ è sconosciuto e dobbiamo usare la varianza campionaria: $\sigma^2_Z \approx \hat{s}^2_Z=\hat{s}^2_A-2\hat{r}\hat{s}_{Av}+\hat{r}^2\hat{s}^2_v$ che porta la soluzione a non avere più distribuzione normale ma t-student, per cui l'intervallo diventa:
$$
Pr\{\hat{r}-t_{1,\alpha/2}\frac{\hat{s}_Z}{\bar{v}\sqrt{p}} \leq r \leq \hat{r}+t_{1,\alpha/2}\frac{\hat{s}_Z}{\bar{v}\sqrt{p}} \} \approx 1-\alpha
$$
 
### Larghezza dell'intervallo di confidenza  
per calcolare l'intervallo di confidenza precedente dobbiamo calcolare la varianza di $Z_j$ 

- $VAR[A_j] \approx \hat{s}^2_A=\frac{1}{p-1}\sum^{p}_{j=1}(A_j-\bar{A})^2=\frac{1}{p-1}[\sum^{p}_{j=1}A^2_j-p \bar{A}^2]=\frac{1}{p-1}\{\hat{S}_{AA}-p \bar{A}^2\}$  
- $COV[A_j,v_j] \approx \hat{s}_{av}=\frac{1}{p-1}\sum^{p}_{j=1}(A_j-\bar{A})(v_j-\bar{v})=\frac{1}{p-1}[\sum^{p}_{j=1}A_jv_j-p \bar{A}\bar{v}] = \frac{1}{p-1}\{\hat{S}_{Av} - p \bar{A}\bar{v}\}$  
- $VAR[v_j] \approx \hat{s}^2_v = \frac{1}{p-1}\sum^{p}_{j=1}(v_j-\bar{v})^2=\frac{1}{p-1}[\sum^{p}_{j=1}v^2_j-p \bar{v}^2]=\frac{1}{p-1}\{\hat{S}_{vv}-p \bar{v}^2\}$   
Dove
- $\hat{S}_A= \sum^{p}_{j=1}A_j$ 
- $\hat{S}_{AA} = \sum^{p}_{j=1}A^2_j$ 
- $\hat{S}_{Av}=\sum^{p}_{j=1}A_jv_j$ 
- $\hat{S}_v= \sum^{p}_{j=1}v_j$ 
- $\hat{S}_{vv} = \sum^{p}_{j=1}v^2_j$, $\hat{r}=\frac{\hat{S}_A}{\hat{S}_v}$ 

$$
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1^*\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p^*\} \Rightarrow Y_{2p}
\end{align}
$$
sapendo che $\sigma^2_Z \approx \hat{s}^2_Z=\hat{s}^2_A-2\hat{r}\hat{s}_{Av}+\hat{r}^2\hat{s}^2_v$  si può dire che ==> $\hat{s}^2_Z=\frac{1}{p-1}\{\hat{S}_{AA}-2\hat{r}\hat{S}_{Av}+\hat{r}^2\hat{S}_{vv}\}$
per cui la larghezza dell'intervallo in questione diviene
$$
\Delta= \frac{\hat{s}_Z}{\bar{v}\sqrt{p}}=\sqrt{\frac{p}{p-1}}\frac{\sqrt{\hat{S_{AA}-2\hat{r}\hat{S}_{Av}+\hat{r}^2+\hat{S}_{vv}}}}{\hat{S}_v}
$$
nonostante la complessità di calcolare questo intervallo di confidenza $Pr\{\hat{r}-t_{1,\alpha/2}\Delta \leq r \leq \hat{r}+t_{1,\alpha/2}\Delta \} \approx 1-\alpha$ i valori necessari$A_j,A^2_j,v_j,v^2_j,A_jv_j$ possono essere accumulati alla fine di ogni ciclo di rigeneramento. 

### Stima intervallare di variabili aleatorie simulate 
il metodo rigenerativo è comodo per calcolare la distribuzione di determinati tipi di variabili aleatorie, l'unico requisito è definire correttamente l'accumulatore $A_j$ . 

>[!example] 
>per esempio: 
>- lunghezza media della coda $A_j=\int^{\beta_j}_{\beta_{j-1}}N(t)dt$  $v_j=\beta_j-\beta_{j-1}$ 
>- secondo momento della lunghezza media della coda $A_j=\int^{\beta_j}_{\beta_{j-1}}N(t)^2dt$  $v_j=\beta_j-\beta_{j-1}$ 
>-  tempo d'attesa medio $A_j=\int^{\beta_j}_{\beta_{j-1}}N(t)dt$  $v_j=C_j$
>- probabilità di trovare k clienti in coda $A_j=\int^{\beta_j}_{\beta_{j-1}}I_k(t)dt$   $v_j=\beta_j-\beta_{j-1}$ con:
>    - $I_{k}$ => numero di volte che N(t)=k
>- costo medio d'attesa $A_j=\int^{\beta_j}_{\beta_{j-1}}R(N(t)) dt$        $v_j=\beta_j-\beta_{j-1}$ dove:
>    - R(k) is cost rate due to the presence of k customers in system 

## Trovare i punti di rigeneramento
un punto di rigeneramento corrisponde a un momento raggiunto dal sistema in cui il suo futuro è una replica del suo passato. Quando il sistema raggiunge questo punto siamo in grado di fare considerazioni sul futuro del sistema ignorando il suo passato , un punto di rigeneramento è definito come **coppia (evento,stato)**. 


### Distribuzione negativa esponenziale  
un riassunto delle propietà della distribuzione negativa esponenziale, si consideri una variabile aleatoria X con $\micro=\frac{1}{\lambda}$
$$
\begin{align}
f_X(x)=\lambda e^{-\lambda x} && F_X(x)=1-e^{-\lambda x}\\
E[X] = \micro=\frac{1}{\lambda} && VAR[X]=\micro^2=\frac{1}{\lambda^2} && CV^2[X]=\frac{VAR[X]}{(E[X])^2}=1
\end{align}
$$
### Minimo tra 2 variabile aleatorie negative esponenziali
Date 2 variabili aleatorie negative esponenziali X e Y  
$$
\begin{align}
f_X(x)=\lambda e^{\lambda-x}\  \ \ (x \geq 0)  && f_Y(y)=\delta e^{\delta y} \ \ \ (y \geq0)
\end{align}
$$
Definiamo una nuova variabile aleatoria $Z=min(X,Y)$ :
- Z è negativa esponenziale con parametro $\lambda+\delta$ 
- $F_Z(z)=1-e^{\lambda z} e^{-\delta z}= 1- e^{-(\lambda+\delta)z}$ 

### Proprietà di assenza di memoria
sia:
- r(t) la distribuzione della porzione rimanente di X : $r(t)=Pr\{X >s+t|X>s\}$ 
usando la probabilità condizionale si può mostrare che   $r(t)=\frac{Pr\{X>s+t\}}{Pr\{X>s\}}$ 

Siccome X ha distribuzione negativa esponenziale abbiamo che :
$r(t)=\frac{e^{-\lambda(s+t)}}{e^{-\lambda(s)}}=e^{-\lambda(t)}$ che dice che la distribuzione della porzione rimanente di X (di r(t)) è la stessa di X.

Per cui si può esprimere la proprietà di assenza di memoria formalmente come 
$$
Pr\{X> x+\alpha|X>\alpha\}=Pr\{X>x\}
$$

### Trovare i punti di rigeneramento in una coda FCFS
Decidere se il sistema è entrato in una condizione di rigeneramento equivale a chiedersi:
^3ea7fc
**"Qual'é la probabililtà che il sistema lasci lo stato corrente in meno di $\Delta$ unità di tempo"?**
Vogliamo rispondere senza sapere il passato del sistema. 
A seconda della distribuzione dei tempi di servizio e di inter-arrivo diverse considerazioni possono essere fatte : 
- G/G/1 : distribuzione generica per entrambi i tempi
- M/G/1: gli inter arrivi hanno distribuzione negativa esponenziale, mentre i tempi di servizio generale 
- G/M/1: inter-arrivo generale, servizio negativa esponenziale 
- M/M/1: distribuzione negativa esponenziale per tutti i tempi

definiamo le seguenti variabili 
-  $\tau$ => tempo di inter-arrivo 
- $\sigma$ => tempo di servizio . 
- $\rho$ => tempo di servizio rimanente al cliente servito.
- $v$ => tempo rimanente all'arrivo seguente.

### G/G/1
non c'é la negativa esponenziale, l'unico punto di rigeneramento è un cliente che trova il server scarico.
sia:
- se t è il tempo di arrivo a un sistema vuoto --> la risposta alla domanda sopra è $Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\}$  
- se t è il tempo di arrivo di un cliente mentre un altro è servito:
    - sia $\rho$ il tempo di servizio rimanente -->  $Pr\{[\delta=min(\tau,\rho)]\leq \Delta\}$   
- se t è il tempo di partenza di un cliente:
    - sia $v$ il tempo richiesto perchè avvenga un altro arrivo --> $Pr\{[\delta=min(v,\sigma)]\leq \Delta\}$   

### M/G/1  
il tempo di arrivo è markoviano mentre il tempo di servizio è generico ,quindi i tempi di partenza sono punti di rigeneramento, la cui caratterizzazione dipende dal tempo di servizio rimanente, per cui:
$$
Pr\{[\delta'=min(v,\sigma)]\leq \Delta\} = Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\}
$$
Lo stesso non si applica se scegliamo il tempo di arrivo di un cliente che trova il server occupato:
$$
Pr\{[\delta* =min(\tau,\rho)]\leq \Delta\} \neq Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\} 
$$

### G/M/1 
dual to M/G/1 case:  any arrival time identifies a regeneration point because $\rho$ has the same distribution of $\sigma$ 
$$
Pr\{[\delta*=min(\tau,\rho)]\leq \Delta\} = Pr\{[\delta=min(\tau,\sigma)]\leq \Delta\}
$$
### M/M/1  
quando entrambi $\tau$ e $\sigma$ hanno distribuzione markovniana allora ogni partenza o arrivo è un punto di rigeneramento.
$$
Pr\{[\delta'=min(v,\sigma)]\leq \Delta\} = Pr\{[\delta*=min(\tau,\rho)]\leq \Delta\}= Pr\{[\delta'=min(\tau,\sigma)]\leq \Delta\}
$$

### Trovare punti di rigeneramento in una rete di code
la discussione fatta per le  FCFS si può estendere facilmente a modelli più complessi. Il criterio base rimane **interrompere l'evoluzione del modello solo quando ci sono comportamenti caratterizzati da distribuzioni generali** . 

Immaginando un sistema composto da due stazioni, possiamo riassumere i risultati nella seguente tabella

| Service time distribution of first queue | Service time distribution of second queue | Criteria for regeneration point                                                            |
| ---------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------ |
| General                                  | General                                   | Qualunque partenza che lascia indietro esattamente n-1 clienti da qualunque dei due server |
| markov(neg-exp)                          | General                                   | Qualunque partenza dal secondo server                                                      |
| General                                  | markov                                    | Qualunque partenza dal primo server                                                        |
| markov                                   | markov                                    | Qualunque partenza nel sistema                                                             |

## Identificare i cicli di rigeneramento
Quando il modello ammette più punti di rigeneramento , solo uno di loro va scelto come punto da usare per iniziare e terminare un ciclo. 

>[!example]
>in una coda M/M/1  se decidiamo che un ciclo inizia quando una partenza lascia m clienti dietro di se non possiamo terminarlo quando ne lascia m+k. Questo proprio perchè le istanze raccolte della stessa variabile aleatoria devono essere indipendenti e identicamente distribuiti.  Identificare i cicli di rigeneramento all'interno del sistema è più difficile perchè perdiamo la proprietà di assenza di memoria.

### Identificare i cicli di rigeneramento con i tempi di passaggio 
Consideriamo il caso di un sotto-sistema identificato in un sistema. Assumiamo un solo punto di entrata per questo sotto sistema, **siamo interessati a quantificare il tempo di soggiorno di un cliente all'interno di questo sotto sistema**. I punti di rigeneramento candidati sono l'entrata e l'uscita da questo sotto sistema (che garantiscono la proprietà di assenza di memoria). **Se esistono stazioni con distribuzioni generali allora queste devono essere vuote quando uno dei due punti di rigeneramento considerati viene innescato**. 

### Identificare i cicli di rigeneramento con il tagged customer
Tutti i clienti sono statisticamente identici. Questo approccio seleziona un singolo cliente arbitrario e lo segue nell'attraversamento del sistema registrando: 
- il momento in cui entra $t_{en}$  
- il momento in cui esce $t_{ex}$ 

la differenza $\tau=t_{ex}-t_{en}$ è **una misura del tempo di passaggio**.

Sia:
- $\tau_j^{[i]}$ => j-esimo tempo di passaggio del cliente.
- $A^{[i]}=\sum^{k^{[i]}}_{j=1}\tau_j^{[i]}$ somma dei $k^{[i]}$ tempi di passaggio. 

la coppia $(A^{[i]},k^{[i]})$ diventa un campione di osservazione indipendenti che può essere analizzato con le stesse tecniche utilizzate per il metodo rigenerativo. 

### Raggruppare cicli di rigeneramento 
Quando ci sono molti punti di rigeneramento può capitare di scegliere quelli che generano cicli che sono troppo corti. In questo caso perdiamo la proprietà del limite centrale e **non possiamo più affermare che la distribuzione sia quasi normale**, se possibile bisognerebbe scegliere un altro punto di rigeneramento. 

Se non si può allora bisogna raggruppare tra loro i cicli di rigeneramento, con l'unica restrizione di **applicare consistentemente il metodo di raggruppamento nella simulazione** . Senza condizionare in nessun modo le misure su cui questo raggruppamento viene applicato

## Metodi di riduzione della varianza
La precisione della simulazione aumenta all'aumentare della dimensione del campione p, un alternativa è lavorare direttamente sulla varianza cercando di ridurla.

2 metodi sono interessanti:
- Variazione antitetiche per generare componenti del campione che siano a coppie negativamente correlati
- Confrontare risultati alternativi correlandone positivamente i componenti del campione ottenuto dalle due alternative 

### Variazioni antitetiche
Assumiamo di voler stimare il valore atteso di una variabile aleatoria Y --> $Y(\micro=E[Y])$ , supponiamo di eseguire una simulazione e di generare un campione di 2p osservazioni $\{Y_1...Y_p,Y_{p+1}...Y_{2p}\}$.
in condizioni normali otterremmo $\hat{\micro}=\bar{Y}=\frac{1}{2p}\sum^{2p}_{i=1}Y_i$  e $VAR[\bar{Y}]=\frac{\sigma^2}{2p}$  sapendo $E[\bar{Y}]=\micro$. 

Supponiamo di dividere il campione in 2 campioni di dimensioni p $\{Y_1...Y_p,Y_{p+1}...Y_{2p}\}= \{Y_{11}...Y_{1p}\},\{Y_{21}...Y_{2p}\}$ .
Sia:
- $Z_i=\frac{Y_{1i}+Y_{2i}}{2}$ che usiamo per ottenere $\bar{Z}=\frac{1}{p}\sum^{p}_{i=1}Z_i=\bar{Y}$. 
    - $E[\bar{Z}]=\frac{E[Y_1]+E[Y_2]}{2}=\micro$ 
    - $VAR[\bar{Z}]=\frac{1}{p}VAR[\frac{Y_1+Y_2}{2}]= \frac{\sigma^2}{2p}+\frac{COV[Y_1,Y_2]}{2p}$  


If 2p of the original sample are independent then also those 2 sub samples are, thus $COV[Y_1,Y_2]=0$ and know that the introduction of the new variable doesn't perturb the experiment $VAR[\bar{Z}]=VAR[\bar{Y}]=\frac{\sigma^2}{2p}$ . 

If they are correlated the division yield different results, if the variables $Y_1$ and $Y_2$ are negatively correlated the variance of $\bar{Z}$ decrease and we obtain $VAR[\bar{Z}] \leq VAR[\bar{Y}]$ . To induce this correlation is sufficient store the seeds used for the first p observations and use them to obtain the observations for the second sub sample. The unique constraint is using Antithetic sequence of random numbers. 

2 sequences of RN  $\{U_i \in (0,1);i=1...m\}$  and $\{U^*_i \in (0,1);i=1...m\}$  are Antithetic if $U_i^*=(1-U_i)$.
Let $\{X_{01},X_{02},...,X_{0p}\}$ be the set of seeds used to produce the first p components of the sample ,then results are stored in this way:
$$
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1^*\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p^*\} \Rightarrow Y_{2p}
\end{align}
$$
The observation produced here are then Antithetic and the size of the confidence interval becomes smaller (because of COV is negative) as equal cost. 

### Confronto delle alternative
se dobbiamo confrontare 2 sistemi con politiche di gestione differenti, è possibile ridurre la varianza. Possiamo confrontare le misure estratte dai 2 sistemi per decidere qual'é la migliore per farlo :
- simulare le 2 alternative separatamente
- produrre le sequenze  $\{Y_{11}...Y_{1p}\},\{Y_{21}...Y_{2p}\}$  
- calcolare $\bar{Y_1};\bar{Y_2}$ e prendere una decisione. 

Sia :
- $Z_i=(Y_{1i}-Y_{2i})$  il campione $\{Z_1...Z_p\}$ che può essere usato per ottenere:
    - Media campionaria (stimatore puntuale) $\bar{Z} = \frac{1}{p}\sum^{p}_{i=1}Z_i=\bar{Y}_1-\bar{Y}_2$ 
    - Varianza campionaria $\hat{s}_Z^2=\frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$ 

Siano :
- $\micro_1$ e $\sigma_1^2$ il valore atteso e la varianza di $Y_1$ 
- $\micro_2;\sigma_2^2$ per $Y_2$ .

il confronto avviene sulla base che $E[\bar{Z}]=E[\bar{Y}_1]-E[\bar{Y}_2]=\micro_1-\micro_2$ e di $VAR[\bar{Z}]=VAR[\bar{Y}_1] + VAR[\bar{Y}_2] - 2COV[\bar{Y}_1,\bar{Y}_2]= \frac{\sigma_1^2+\sigma_2^2}{p} -2 COV[\bar{Y}_1,\bar{Y}_2]$ 


gli $Z_i$ individuali e $\bar{Z}$ possono entrambi assumere valori positivi o negativi (e anche agli estremi dell'intervallo di confidenza). Se entrambi sono dello stesso segno la scelta è più semplice. 

se la simulazione per le 2 alternative è effettuata separatamente allora $COV[\bar{Y}_1,\bar{Y}_2]=0$ così che 

$$VAR[\bar{Z}]=VAR[\bar{Y}_1-\bar{Y}_2]= \frac{\sigma^2_1+\sigma^2_2}{p}$$ anche la decisione a questo punto è semplice. 

Se invece effettuiamo la simulazione con il seguente schema:
$$
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{2p}
\end{align}
$$
dove:
- X sono i semi del generatore.

 allora $\bar{Y}_1$ e $\bar{Y}_2$ sono positivamente correlati, così che  $$VAR[\bar{Z}]=VAR[\bar{Y}_1-\bar{Y}_2] < \frac{\sigma_1^2+\sigma_2^2}{p}$$ 
per cui la stima è più precisa a un costo di calcolo più basso.

### Precisione del risultato
Le stime intervallari permettono di ottenere una certa sicurezza nei parametri calcolati , tuttavia parte del problema è la precisione che vogliamo raggiungere con la nostra stima. 

sia:
- $\epsilon$ la precisione richesta 
- $\Delta= \frac{\hat{s}_Z}{\bar{v}\sqrt{p}}$ la semi estensione dell'intervallo.

sapendo che $\Delta$ dipende dalla grandezza del campione e dalla deviazione standard, possiamo calcolarla come 
$$
\frac{\Delta}{\bar{Y}} \leq \epsilon
$$
usando naturalmente una regola di stop sequenziale per sapere quando fermarsi

## Tuning 
Consiste nel verificare l'adeguatezza delle distribuzioni come parte del modello simulato, stimando i parametri e verificando la qualità dei generatori casuali, controllando che parametrizzando il modello i risultati siano coerenti tra di loro . 

## Validation
Controllare che il simulatore dia risultati affidabili :
- comparare i risultati della simulazione con un sistema reale
- con modelli matematici indipendenti 

è importante anche usare una versione semplificata del simulatore, per verificare che i vari componenti si comportino come atteso. Le diverse versioni del simulatore devono concedere una visione chiara sugli aspetti del sistema in esame.

Un primo modo per capire se il simulatore sta generando risultati affidabili è prendere gli intervalli di confidenza (low,up) e compararli con un valore teorico $\micro$ controllando se è  coperto dall'intervallo. 

Una via più sicura consiste nell'implementare la definizione di intervallo di confidenza con livello $1-\alpha$ che dice:
**Se l'esperimento è effettuato N volte, il valore teorico $\micro$ dovrebbe essere coperto dalla stima intervallare $n(1-\alpha)$ volte, mentre approssimativamente per  $n \alpha$ volte l'intervallo non dovrebbe coprire il valore teorico .**  
in pratica si può applicare questo metodo:
- Ogni esperimento consiste nel ripetere la simulazione con un seed diverso
- Da ogni esperimento calcolare lo stimatore puntuale $\hat{\micro}$ e l'intervallo di confidenza $(\hat{\micro}-\Delta,\hat{\micro}+\Delta)$  del vero parametro $\micro$ 
    - Date queste ipotesi: (approssimativamente) 50% dovrebbe restituire un $\hat{\micro}$ che è più grande del valore teorico, mentre gli altri dovrebbero essere più piccoli. 
    - (approssimativamente) $(1-\alpha )\%$  degli esperimenti dovrebbero restituire intervalli di confidenza che coprono $\micro$ mentre $\alpha\%$ non dovrebbero coprire $\micro$ 