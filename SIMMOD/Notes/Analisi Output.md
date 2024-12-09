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
when the model admits many regeneration points, one of them must be chosen as a reference and regeneration cycles begin and end when this point is reached. 

for example if in a M/M/1 queue if we decide that a regeneration cycle start start when a departures leaves m customers we cannot end it if it leaves m+k customers. This is because the statistics collected must be identical and independent instances of the same RV.  identify regeneration cycles in a network is more difficult because we lose the memory less property.

### Identify regeneration cycles  with passage times
consider the case of a sub system identified in a system. Assume a single entry point for this sub system, **we are interested in measuring the average time spent by customers in the sub system**. Candidate regeneration points are the arrival or a departure from the entry point of the sub system (because of memory less). If there exists stations outside the sub system with general time distributions they must be empty when the two previous events are considered. 

### Identify regeneration cycles  with tagged customer
All customers are statistically identical. This approach arbitrarily selects one customer in the system and follows its way through the system, recording: the time it enters $t_{en}$  and it exit $t_{ex}$ . The difference $\tau=t_{ex}-t_{en}$ is a measure of the passage time.

Let $\tau_j^{[i]}$ be the j-th passage time of the tagged customer.
Let $A^{[i]}=\sum^{k^{[i]}}_{j=1}\tau_j^{[i]}$ be the sum of the $k^{[i]}$ passage times. 

The pair $(A^{[i]},k^{[i]})$ becomes the component of a sample of independent observation that can provide estimates with the regenerative method. 

### Grouping regeneration cycles
When there are many regeneration points it can happen that the chosen ones yield regeneration cycles that are too short. In this case we cannot rely on the central limit theorem stating that the distribution are "quasi-normal", if possible we must choose a new regeneration point that avoid this problem. 

If not is possible to aggregate several regeneration cycles, the unique constraint is that the grouping criteria is always applied during the simulation run. Without conditioning its application on the specific characteristics of the regeneration cycles that need to be aggregated.

## Improve results 
The precision of the simulation rise proportionally to the size of p, an alternative to that is working on the sample variance to make it smaller. 2 interesting cases exists:
- Antithetic variates to make the sample components pairwise negatively correlated 
- Comparing alternative results by positively correlating the corresponding components of the samples obtained for the two alternatives 

### Antithetic variates 
Assume we want to estimate the expected value of an RV Y --> $Y(\micro=E[Y])$ , suppose we run a simulation and produce a sample of 2p observations $\{Y_1...Y_p,Y_{p+1}...Y_{2p}\}$. In normal conditions we would retrieve $\hat{\micro}=\bar{Y}=\frac{1}{2p}\sum^{2p}_{i=1}Y_i$  and $VAR[\bar{Y}]=\frac{\sigma^2}{2p}$  knowing $E[\bar{Y}]=\micro$. 

Suppose to divide the sample in 2 sub samples of size p $\{Y_1...Y_p,Y_{p+1}...Y_{2p}\}= \{Y_{11}...Y_{1p}\},\{Y_{21}...Y_{2p}\}$ .
Let $Z_i=\frac{Y_{1i}+Y_{2i}}{2}$  that we use to obtain $\bar{Z}=\frac{1}{p}\sum^{p}_{i=1}Z_i=\bar{Y}$. The expected value and variance of $\bar{Z}$ are:
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

### Alternative comparison
if we must compare 2 systems with different management policies, is possible to reduce the variance. If we want to obtain estimates of a measure computed for the 2 alternatives to decide which is the best we can: simulate the 2 alternatives separately and produce $\{Y_{11}...Y_{1p}\},\{Y_{21}...Y_{2p}\}$  , then compute $\bar{Y_1};\bar{Y_2}$ and then make a decision. 

Let $Z_i=(Y_{1i}-Y_{2i})$ , the sample $\{Z_1...Z_p\}$ can be used to obtain:
- Point estimate (sample average) $\bar{Z} = \frac{1}{p}\sum^{p}_{i=1}Z_i=\bar{Y}_1-\bar{Y}_2$ 
- Sample variance $\hat{s}_Z^2=\frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$ 

Let $\micro_1$ and $\sigma_1^2$ be expected value and variance for $Y_1$ ,same $\micro_2;\sigma_2^2$ for $Y_2$ . The comparison would be made on the basis of $E[\bar{Z}]=E[\bar{Y}_1]-E[\bar{Y}_2]=\micro_1-\micro_2$ and of $VAR[\bar{Z}]=VAR[\bar{Y}_1] + VAR[\bar{Y}_2] - 2COV[\bar{Y}_1,\bar{Y}_2]= \frac{\sigma_1^2+\sigma_2^2}{p} -2 COV[\bar{Y}_1,\bar{Y}_2]$ 


The individual $Z_i$ and $\bar{Z}$ as well may assume positive or negative values (and also the extremes of confidence interval). If both are positive or negative the decision is easier. 

If the simulations for the 2 alternatives are performed in an independent manner $COV[\bar{Y}_1,\bar{Y}_2]=0$ so that 
$VAR[\bar{Z}]=VAR[\bar{Y}_1-\bar{Y}_2]= \frac{\sigma^2_1+\sigma^2_2}{p}$ also the decision is easy. 

if instead the different replications of the 2 experiments are performed with the following scheme:
$$
\begin{align}
X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{11}; && X_{01} \Rightarrow \{U_1\} \Rightarrow Y_{21} \\
...\\
X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{1p}; && X_{0p} \Rightarrow \{U_p\} \Rightarrow Y_{2p}
\end{align}
$$
where X are the seeds. $\bar{Y}_1$ and $\bar{Y}_2$ are positively correlated so that $VAR[\bar{Z}]=VAR[\bar{Y}_1-\bar{Y}_2] < \frac{\sigma_1^2+\sigma_2^2}{p}$ 
then the estimate is more precise with the same computational cost. 

### Result precision 
Interval estimates allow to get confidence in the robustness of the computed results with respect to possible variation, part of the problem however is the precision we want to reach with our estimate. 

Let $\epsilon$ be the required precision and $\Delta= \frac{\hat{s}_Z}{\bar{v}\sqrt{p}}$ the semi width of the confidence interval. Knowing that $\Delta$ depend on the sample size and sample standard deviation we can work on this values to get a better precision, expressed as 
$$
\frac{\Delta}{\bar{Y}} \leq \epsilon
$$
It is better to use a sequential stopping rule to check if the desired precision is reached

## Tuning 
tuning consist of: assessing the adequacy of the distributions assumed as part of the specification models, estimating parameters, testing the quality of the variate generators, checking that variations of the parameters produce coherent variations of the results. 

## Validation
check whether the simulator provides reliable estimates : comparing the simulation output with measures from the real system and with the theoretical values obtained with independent mathematical methods.

It is also important to use simplified version of the required simulator in order to check it's components. Different version should be considered to make sure that various aspects of the original simulator are checked. 

A first way of checking whether the simulator provides reliable estimates is comparing confidence interval (low,up) with a theoretical value $\micro$ to see if it's covered by the interval. 

A more reliable way is implementing the definition of confidence level $1-\alpha$ which says that:
_if the experiment is repeated n times, the theoretical value $\micro$ should be covered by the interval estimates approximate $n(1-\alpha)$ times, while (approx) for $n \alpha$ times the confidence interval should not cover the theoretical value._  In practice we may proceed that way:
- Each experiment consist of repeating the simulation run with different seeds
- From each experiment compute the point estimate $\hat{\micro}$ and the confidence interval $(\hat{\micro}-\Delta,\hat{\micro}+\Delta)$  of the true parameter $\micro$ 
- Given those hypothesis: (approx) 50% of the experiments should provide a point estimate $\hat{\micro}$ that is larger than the theoretical value, while others should be smaller. 
- (approx) $(1-\alpha )\%$  of the experiments should provide intervals that include the theoretical value $\micro$ while $\alpha\%$ should not provide intervals which include $\micro$ 