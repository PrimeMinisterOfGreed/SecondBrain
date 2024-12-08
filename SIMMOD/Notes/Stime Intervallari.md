## Media campionaria e statistica standard
- Media campionaria: $\bar{X} = \frac{1}{p} \sum^{i=1}_{p}x_i$
- Varianza Campionaria: $\hat{s}^2 =\frac{1}{p-1}\sum^{i=1}_{p}(x_i-\bar{X})^2$    
- Deviazione standard campionaria : $\hat{s} = \sqrt{\hat{s}^2}$
- Coefficiente di variazione : $\frac{\hat{s}}{\bar{X}}$ 

La media misura la tendenza centrale, mentre la varianza e la deviazione standard sono misure di dispersione della media.
## Polarizzazione di uno stimatore
la polarità di un parametro è la differenza tra il valore dello stimatore e il valore vero dell'indicatore

>[!important] 
>$\hat{\psi}$ è un buono stimatore  di un parametro $\psi$  se:
>- la distribuzione di $\hat{\psi}$ è centrata su $\psi$ 
>- la distribuzione di $\hat{\psi}$ è stretta abbastanza per cui $|\hat{\psi} - \psi|$  è preciso abbastanza 
>- informazioni e distribuzione di $\hat{\psi}$ possono essere ottenuti dai valori osservati e più nello specifico dalla dimensione del campione stesso.


## Media campionaria non polarizzata 
consideriamo un campione di p osservazioni di una variabile aleatoria X, con media $\micro$ e varianza $\sigma^2$, valore atteso  $E[X]=\micro$ , mentre $\hat{\micro}= \bar{X}$.

dalla definizione di  $\hat{u}$  possiamo osservare che $\bar{X}$ è uno stimatore non polarizzato per $\micro$ 
e mettendo $VAR[\hat{u}] = E[(\hat{u}-E[\hat{u})^2]$ otteniamo $VAR = \frac{\sigma^2}{p}$ e possiamo concludere che $\bar{X}$  è un buono stimatore per $\micro$. 
## Varianza campionaria non polarizzata
come per la media definiamo $\hat{s}^2=\frac{1}{K}\sum^{i=1}_{p}(x_i-\hat{\micro})^2$ , vogliamo mostrare che quando $E[\hat{s}^2]=\sigma^2$ è vera per certi valori di K. Con qualche passaggio possiamo dire che se scegliamo K=(p-1) possiamo facilmente derivare $E[\hat{s}^2] =  \frac{(p-1)p}{pK}* \sigma^2= \sigma^2$. Concludendo quindi che $s^2$ è uno stimatore non polarizzato di  $\sigma^2$ , calcolato con $\frac{1}{p-1} \sum^{i=1}_{p}(x_i-\bar{X})^2$ 

##  Varianza della varianza campionaria
Stimare la varianza di $\hat{s}^{2}$ è compilcato poichè il parametro dipende fortemente dalle caratteristiche della distribuzione. Dato il solito campione $x_{1}\dots x_{p}$ calcoliamo la varianza campionaria con stimatore non polarizzato $\hat{s}^{2}=\frac{1}{p-1}\sum^{P}_{i=1}(x_{i}-\bar{x})^2$ 

sia $X_j$ il sottocampione di osservazioni senza il j-esimo.  Calcoliamo:
- Media campionaria : $\bar{X}_j = \frac{1}{p-1} \sum^{p}_{i=1;i \neq j}x_i$ 
- Varianza campionaria : $s^2_j = \frac{1}{p-2} \sum^{p}_{i=1;i \neq j}(x_i-\bar{X}_j)^2 = \frac{1}{p-2} \sum^{p}_{i=1;i \neq j} x_i^2 \frac{p-1}{p-2}\bar{X}_j^2$.

Si può mostrare che : $\bar{X} = \frac{1}{p} \sum^{p}_{j=1}\bar{X}_j$ 
Non si può dire lo stesso per $\hat{s}^2=\frac{1}{p}\sum^{p}_{j=1}\hat{s}_j^2$ 

Adesso possiamo usare questi risultati per ottenere informazioni sulla varianza campionaria in funzione del dimensione del campione.
definiamo=> $Z_j=p \hat{s}^2 - (p-1)\hat{s}^2$
Per definizione sappiamo che  $E[\hat{s}^2] = E[s_j^2]= E[\sigma^2]$ and so $E[Z_j]=\sigma^2$ . Consideriamo un campione formato da queste variabili, allora $\bar{Z}=\frac{1}{p} \sum^{p}_{j=1}Z_j$  e $\hat{s}^2= \frac{1}{p-1}\sum^{p}_{j=1}(Z_j-\bar{Z})^2$. 

Si può mostrare che $\Upsilon = \frac{(\bar{Z}-\sigma^2)}{\sqrt{\hat{s}^2_Z/p}}$  è distribuita come una t-student con p gradi di libertà  (distribuzione che ha valore centrato in 0 e varianza che decresce con l'aumentare dei gradi di libertà). Possiamo concludere che $\bar{Z}$ è un buono stimatore per $\sigma^2$ e $\hat{s}^2$ perchè $\bar{Z}=\hat{s}^2$.   

Considerando la varianza $\hat{s}=\sqrt{ \frac{1}{p-1} \sum^{P}_{i=1} (x_{i}-\bar{x})^2}$  diventa subito chiaro quanto la sua computazione sia dispendiosa, sopratutto considerando che bisogna ciclare sul campione 2 volte.

### Algoritmo a passaggio unico convenzionale 
una equazione equivalente per calcolare 
$$\hat{s}^{2}=^{!4} \frac{1}{p}\sum^{p}_{i=1}x_{i}^{2}-\bar{x}^2$$ 
che però possiede problemi di approssimazione. 

### Algoritmo di Welford 
- Media campionaria in corso=> $\bar{x}_{k}=\frac{1}{k}(x_{1}+\dots x_{k})$ 
- Somma quadratica dei campioni in corsa => $v_{k}=(x_{1}-\bar{x}_{k})^{2}+\dots+(x_{k}-\bar{x}_{k})^2$

sia $\bar{x}_{k}$ che $v_{k}$ possono essere accumulati (con $\bar{x}_{0}=0,v_{0}=0$ )

$$
\bar{x}_{k}=\bar{x}_{k-1}+\frac{1}{k}(x_{k}-\bar{x}_{k-1});v_{k}=v_{k-1}+\left( k-\frac{1}{k} \right)(x_{k}-\bar{x}_{k-1})
$$
quindi $\bar{x}_{n}$è la media campionaria e $\frac{v_{n}}{(n-1)}$ è la varianza non polarizzata.
dalla definizione di varianza campionaria in corsa otteniamo:
$s_{k}^{2}= \frac{1}{k}\sum^{k}_{j=1}x^2_{j}-(\bar{x}_{k})^2$ e definiamo $v_{k}=\sum^{k-1}_{i=1}x_{j}^2+x^2_{k}-k(\bar{x}_{k})^2$ 
usando $(k-1)(\bar{x}_{k}-1)^2$ e i risultati precedenti otteniamo 
$v_{k}=v_{k-1}+\frac{k-1}{k}(x_{k}-\bar{x}_{k-1})^2$ 

I vantaggi dell'algoritmo di welford è che non ha problemi numerici di approssimazione e non serve sapere quanto è grosso il campione, la convergenza di $\bar{x}$ e s non è necessariamente monotona

## Diseguaglianza di Chebichev
La diseguaglianza di Chebichev è relazionata al numero di punti che giacciono dentro k deviazioni standard dalla media. 
**I punti più lontani dalla media sono quelli che contribuiscono di più a  s e $\hat{s}^2$**  

 definiamo l'insieme $S_k=\{x_i|\bar{X}-k \hat{s} < x_i < \bar{X} + k \hat{s}\}$ 
 dalla definizione di varianza campionaria abbiamo: 

$$
(p-1) \hat{s}^2= \sum_{x_i \in S_k}(x_i - \bar{X})^2 + \sum_{x_i \in \bar{S}_k} (x_i - \bar{X})^2
$$
Dove:
 $\bar{S}_k$ è il complemento di $S_k$ , ignorando il contributo a $\hat{s}^2$ dato da tutti i punti vicino alla media otteniamo  $$(p-1)\hat{s}^2 \geq \sum_{x_i \in \bar{S}_k}(x_i-\bar{X})^2 \geq \sum_{x_i \in \bar{S}_k}(k \bar{s})^2 = |\bar{S}_k|(k \hat{s})^2$$ Usando  $q_k=|S_k|/p$ come proporzione di $x_i$ dentro l'intervallo $\underline{+} k \hat{s}$ di $\bar{X}$  e rimuovendo $\hat{s}^2$ Otteniamo 
 >[!important] Disuguaglianza di Chebichev
>$$
q_k \geq 1- \frac{(p-1)/p}{k^2} \geq 1 - \frac{1}{k^2}
$$


- Per ogni campione almeno il 75% dei punti giacciono in  $\underline{+}2 \hat{s}^2$ di $\bar{X}$ 
- Per k=2 è molto conservativo (tipicamente il 95% giacciono in $\underline{+}2 \hat{s}^2$ di $\bar{X}$) 
- $\bar{X} \underline{+}2 \hat{s}^2$  definisce la larghezza effettiva di un campione (così come 4s) , molti ma non tutti i punti giacciono in questo intervallo (ad eccezione degli outliers) 
## Statistiche temporali
x(t) => processo stocastico ($0<t< \tau$) 
- Media del processo stocastico $\bar{X} = \frac{1}{\tau} \int^{\tau}_{0}x(t) dt$ 
- Varianza del processo stocastico $s^2=\frac{1}{\tau} \int^{\tau}_{0}(x(t)- \bar{X})^2 dt$ 
- Deviazione standard  $s=\sqrt{s^2}$
- Equazione a un passo per la varianza $s^2=(\frac{1}{\tau} \int^{\tau}_{0}x^2(t)dt) - \bar{X}^2$ 


nella simulazione a eventi discreti il sample path è discreto e quindi gli integrali si riducono a somme.

Consideriamo il seguente tracciato 
$$x(t)= \begin{cases}
x_{1} && t_{0}<t\leq t_{1} \\
x_{p} && t_{p-1}<t\leq t_{p}
\end{cases}$$
e definiamo $\sigma_{i}=t_{i}-t_{i-1}$ 
otteniamo 
- media: $\bar{x}=\frac{1}{\tau}\int^{\tau}_{0} x(t) \, dt= \frac{1}{\tau p}\sum^{p}_{i=1}x_{i}\sigma_{i}$ 
- varianza: $s^2=\frac{1}{\tau}\int^{\tau}_{0}(x(t)-\bar{x})^2 \, dt=\left( \frac{1}{\tau p}\sum^{p}_{i=1}x_{i}^2*\sigma_{i} \right)-\bar{x}^2$
Welford è applicabile anche in questo caso
## Risultati preliminari

se $X_1,X_2,...,X_p$ è una sequenza identicamente e indipendentemente distribuita di variabili aleatorie normali con comune $\micro$ e $\sigma$. $\bar{X}$ è la media della sequenza, allora $\bar{X}$ è una $Normal(\micro,\sigma,\sqrt{p})$ Variabile aleatoria normale indipendentemente dal valore di p.

## Intervallo aleatorio 
Sia $Z = \frac{\bar{X} - \micro}{\sigma/\sqrt{p}}$ , Z ha distribuzione standard normale con $\micro$ = 0 e $\sigma$ = 1.
dato un parametro $\alpha \in (0.0,1.0)$ esiste un numero positivo $z_{\alpha/2}$ cosi che 
$$
Pr(-z_{\alpha/2} \leq Z \leq z_{\alpha/2}) = 1- \alpha
$$
o inserendo direttamente la definizione
$$
Pr(\bar{X}- \frac{z_{\alpha/2} \sigma}{\sqrt{p}} \leq \micro \leq \bar{X}+ \frac{z_{\alpha/2} \sigma}{\sqrt{p}})
$$
NB: $\bar{X}$ è una variabile aleatoria , mentre $\micro$ è una costante (=0)
## Central limit theorem 
Seguendo la definizione di sequenza . $\bar{X}$ tende a una $Normal(\micro,\sigma,\sqrt{p})$ RV quando $p \rightarrow \infty$ 
## Discrete data histogram
Dato un multi insieme di campioni discreto $S=\{x_1,x_2,...,x_p\}$ con valore possibile $\chi$ , la frequenza relativa è  $\hat{f}(x)= \frac{\# \ of \ x_i \in S \ with \ x_i=x}{p}$ , un discrete data histogram è una rappresentazione grafica di $\hat{f}(x)$ con  x.

- Media  $\bar{X} = \sum_{x in \chi}x \hat{f}(x)$ 
- Deviazione standard  $s=\sqrt{(\sum_{x}x^2\hat{f}(x)) - \bar{X}^2}$ 
- Varianza  $s^2$ 

media campionaria  e deviazione standard dell'istogramma  sono matematicamente equivalente a quelle campionarie, se le frequenze sono già state calcolate allora $\bar{X}$ e s dovrebbero essere calcolate usando le equazioni dell'istogramma.

Se si preferisce la versione cumulata, si usa 
$\hat{F}(x) = \frac{\# \ of \ x_i \in S \ with \ x_i\leq x}{p}$ , utile per i quantili.
## Continuos data histogram
Si consideri un campione di valori reali $S=\{x_{1}\dots x_{s}\}$ con 
- a,b => confini minimi e massimi e $a\leq x_{i}<b$
- $\chi=[a,b)=\{x|a\leq x<b\}$ => intervalli possibili in R $\forall x$
## Binning
partizionare l'intervallo $\chi= [a,b)$ in k sotto intervalli di eguale larghezza. i bins sono:  
:LiAward: $B_0=[a,a+\delta)$ , $B_1=[a+\delta,a+2\delta),...$  la cui larghezza è 
:LiArrowRightCircle: $\delta=\frac{b-a}{k}$ . per ogni $x \in [a,b)$ c'é un unico  $B_j$ con $x \in B_j$ 
- Frequenza stimata dei valori in $B_j$ è $\phi_j=\frac{\# \ x_i \in S \ for \ which \ x_i \in B_j}{p}$ 
- Densità stimata della variabile aleatoria X: $\hat{f}(x)= \hat{f}_j(x)=\frac{\phi_j}{\delta}$ se $x \in B_j$ 
- Densità: frequenza normalizzata dalla divisione per $\delta$ 
- Frequency: densità molitplicata per $\delta$ 

Aumentare o diminuire $\delta$ creerà diverse granularità dell'istogramma
## Frequenze relative 
Sia: 
- $p_j$ => frequenza relativa del bin = $B_j$ 
- $m_j=a+(j+\frac{1}{2})\delta$=> punto medio del bin

allora $p_j=\delta \hat{f}(m_{j)}$ con condizione $\int^{b}_{a}\hat{f}(x)  \, dx=\sum^{k}_{j=0}p_{j}= 1$

## Integrali dell'istogramma 
Consideriamo i due integrali $\int^{b}_{a}\hat{f}(x)  \, dx$ e $\int^{b}_{a}x^{2}\hat{f}(x)  \, dx$  , questi due integrali diventano somme e visto che $\hat{f}(m_{j})=\frac{P_{j}}{\sigma}$ e $\int^{}_{B_{j}} x  \, dx = m_{j}\sigma$ 
allora $\int^{}_{B_{j}} x^{2  \, dx}= \int^{m_{j}+ \frac{\sigma}{2}}_{mj-\frac{\sigma}{2}} x^{2} \, dx = m_{j}^2\sigma+\frac{\sigma^3}{12}$ 

la media e la varianza del CDH sono definiti in base a questi integrali 

- Media => $\int^{b}_{a}x\hat{f}(x)  \, dx=\bar{x}$ 
- Varianza => $s=\sqrt{ \int^{b}_{a}(x-\bar{x})^{2}\hat{f}(x)  \, dx }$ 

entrambe possono essere calcolate mediante somma 
- Media => $\bar{x}=\sum^{k-1}_{j=0}m_{j}P_{j}$
- Varianza=> $s=\sqrt{ \left( \sum^{k-1}_{j=0}(m_{j}-\bar{x})^2p_{j} \right)+\frac{\sigma^2}{12} }$
Il grafico di questi due stimatori differirà leggermente dal campione poichè a causa del binning si introduce un certo errore di quantizzazione. 

Nell usare i CDH l'unico svantaggio sta nel dover scegliere opportunamente k , cosa che non succede nei DDH quando si usa una distribuzione cumulata.


## Properties of sample mean histogram
- la media dell'istogramma è  $\micro$
- la deviazione standard dell'istogramma è circa $\sigma/\sqrt{p}$ 
-  se p è sufficientemente grande l'isogramma approssima una $Normal(\micro,\sigma,\sqrt{p})$ pdf.

>[!important]
> qualunque sia la distribuzione della variabile generata (exponential, neg exp ecc...) se la mettiamo su un istogramma la densità approssima sempre quella di una normale
## Standardizzare la distribuzione della media campionaria
possiamo standardizzare la media campionaria $\bar{x}_1,\bar{x}_2,...$ sottraendo $\micro$ e dividendo per $\sigma/\sqrt{p}$ in modo da formare un insieme di $z_1,z_2,...$ e quindi
$$
z_j=\frac{\bar{x}_j- \micro}{\sigma/\sqrt{p}} 
$$

## Proprietà dell'istogramma standardizzato 
- la media è approssimativamente  0
- la deviazione standard è approssimativamente 1
- se p è sufficientemente grande allora approssima una normale(0,1) pdf
## T statistic distribution
bisogna rimpiazzare la deviazione standard della popolazione $\sigma$ con quella campionaria $\hat{s}_j$ nell'equazione di  $z_j$ . 
ricordiamo che:
- ogni $\bar{x}_j$ è uno stimatore puntuale di  $\micro$ 
- ogni $\hat{s}_j^2$ è uno stimatore puntuale di  $\sigma$^2 (uguale per $\hat{s}_{j}$) 
$$
t_j=\frac{\bar{x_j}-\micro}{\hat{s}_j/\sqrt{p}} 
$$
## Proprietà di un istogramma t-student 
- con p>2 l'istogramma è approssimativamente  0
- se p>3 la deviazione è standard è circa $\sqrt{\frac{p-1}{p-3}}$ 
- con p  sufficientemente grande si approssima a una student con (p-1) gradi di libertà
## Stime intervallari
sia:
- $x_1,x_2,...,x_p$  un campione proveniente da una sorgente con  $\micro$ sconosciuta 
-  $\bar{x}$ e $\hat{s}$  sono media e deviazione standard campionarie  
- p è grande 

allora è approssimativamente vero che $t = \frac{\bar{x}-\micro}{\hat{s}/\sqrt{p}}$ è una Student(p-1).
questo teorema giustifica la ricerca tramite intervalli di una media sconosciuta $\micro$ . Più $p \rightarrow \infty$ più la Student(p-1) diviene indistinguibile da una Normal(0,1)
## Parametro di confidenza
Sia: 
- T una Student(p-1) RV, 
- $\alpha$ un parametro di confidenza  $\in (0.0,1.0)$ 

allora esiste un numero positivo  $t^*$ anche noto come $t_{(p-1,\alpha/2)}$ per il quale
$$
Pr(-t^*\leq T \leq t^*) = 1- \alpha
$$

supponendo $\micro$ sia sconosciuto. Poiché $t \approx Student(p-1)$ allora
$$
-t^* \leq \frac{\bar{x}-\micro}{\hat{s}/\sqrt{p}} \leq t^*
$$
sarà approssimativamente vero con probabilità$1-\alpha$ . così con probabilità $1-\alpha$ :
$$
\bar{x}- \frac{t^*\hat{s}}{\sqrt{p}} \leq \micro \leq \bar{x}+\frac{t^*\hat{s}}{\sqrt{p}}
$$
NB $\micro = 0$ 
>[!Theorem] Dell intervallo di confidenza 
>sia:
>- $x_1,x_2,...,x_p$ un campione aleatorio di una variabile indipendente con$\micro$ sconosciuta 
>- $\bar{x}$ e $\hat{s}$ sono la media campionaria e la varianza campionaria
>- p è grande 
>
>allora esiste un parametro di confidenza $\alpha \in (0.0,1.0)$ associato a un numero positivo $t^*$ cosi che  $Pr(\bar{x}- \frac{t^*\hat{s}}{\sqrt{p}} \leq \micro \leq \bar{x}+\frac{t^*\hat{s}}{\sqrt{p}}) \approx 1-\alpha$  

## Intervallo di confidenza
dato un campione aleatorio $x_1,x_2,...,x_p$ se possiamo calcolare $\bar{x}$ e $\hat{s}$ , l'intervallo con confini $\bar{x} \underline{+} \frac{t^*\hat{s}}{\sqrt{p}}$ è un range aleatorio che contiene il vero parametro $\micro$ con $(1-\alpha)\%$  confidenza.

Per calcolare una stima intervallare su un parametro $\micro$ :
- Scegliere un livello di confidenza $1-\alpha$ (tipicamente $\alpha=0.05$) 
- Calcola $\bar{x}$ e $\hat{s}$ 
- Calcola il valore critico $t^*=t-Student(p-1,1-\alpha/2)$ 
- Calcola i confini dell'intervallo $\bar{x} \underline{+} \frac{t^*\hat{s}}{\sqrt{p}}$ 

## Stopping rule
il valore asintotico di $t^*$ è $t^*_\infty= \lim_{p \rightarrow \infty}t-Student(p-1,1-\alpha/2) = Normal(0.0,1.0,1-\alpha/2)$ , fino a che $\alpha$ è molto vicino a 0.0 se p>40 possiamo usare $p^*_\infty$ 

Data una ragionevole stima di  $\hat{s}$ è un parametro di larghezza specificato w, quanti campioni bisogna raccogliere?
usando: $w = \frac{t^*\hat{s}}{\sqrt{p}}$ ==> possiamo risolvere per $p=\lfloor (\frac{t_\infty^*\hat{s}}{w})^2 \rfloor$   

## Sequential Stopping rule
Se una ragionevole stima per $\hat{s}$ non è disponibile, w può essere specificato in funzione di  $\hat{s}$ eliminandola dall'equazione precedente

per esempio se w e il 10% di $\hat{s}$  e si vuole avere una confidenza del 95% , p=384 dovrebbe essere usato per stimare $\micro$ per dire che giace in $\underline{+}w$ , dopo aver generato un campione di questa dimensione, bisogna controllare se si è raggiunta la precisione richiesta, altrimenti si cerca di ingrandire il campione.

w può essere usato come parametro per la precisione, ma solo dopo aver raccolto un campione di dimensione p>40:
- calcolare un primo valore per $\bar{x}$ e $\hat{s}$ e contollare $\frac{w}{\bar{x}} = \frac{t^*\hat{s}}{\bar{x}\sqrt{p}} < \epsilon$ 
- Se la disuguaglianza non è soddisfatta si può pensare che di generare un campione di dimensione $p=\lfloor (\frac{t_\infty^*\hat{s}}{\bar{x}\epsilon})^2 \rfloor$
- Ripetere finchè la precisione richiesta non è stata raggiunta