## Scopo delle catene di markov

Le catene di markov rispondono a questo tipo di domande:
- Per quanto un giocatore potrà scommettere prima di andare in bancarotta? 
- Qual'é la probabilità che domani sarà sereno?

Le catene di markov sono un insieme di modelli che **evolvono col tempo** . 

## Concetti di probabilità base 
 - Una variabile aleatoria **discreta** X è completamente caratterizzata dalla sua  PDF $F_x(x)=P[X=x]$  o **probabilità che la VA X sia uguale a x**  
 - Una variabile aleatoria **continua** X è completamente caratterizzata dalla sua CDF $F_x(x)=P[X \leq x]$ , la PDF è anche espressa in termini di $f_x=\frac{dF_x(x)}{dx}$ 

Siano A,B due eventi => la loro probabilità condizionale è  $P[A|B] = \frac{P[A,B]}{P[B]}$ , da cui segue che $P[A,B]=P[A|B]*P[B]$  

## Processi stocastici  
Un processo stocastico è un insieme di variabili aleatorie $\{X(t), t \in T\}$ tutte definite in uno spazio degli stati definito da elementi indicizzati da T.
3 elementi devono essere specificati :
- Lo spazio degli stati del processo  
- Il parametro di indicizzazione 
- le dipendenze tra le variabili aleatorie in $\{X(t),t \in T\}$ 


### Spazio degli stati
Lo spazio degli stati di un processo stocastico sono tutti i valori che le Variabili Aleatorie $X(t)$ possono assumere.

- Se questo insieme è finito allora abbiamo un processo stocastico discreto nello spazio (o catena)
- Altrimenti è un processo con spazio degli stati continuo, rappresentati da un sottoinsieme dei numeri reali

### Indice
If the index set T is finite we have a discrete time stochastic process (at the end of the day ecc..). Otherwise the process is called continuous time. 

for discrete we denote it as $\{X_n,n \geq 0\}$ 
for continuous we denote it as $\{X(t),t \geq 0\}$  

### Dipendenze statistiche 
Denotiamo tutte le variabili aleatori con un vettore $X=[X(t_1),X(t_2),...]$ , per caratterizzare completamente la densità di probabilità congiunta (PDF) del processo stocastico, bisogna specificare :
- $F_x(x;t)=P[X(t_1) \leq x_1, X(t_2) \leq x_2,...,X(t_n) \leq x_n]$  
- $x=(x_1,x_2,...,x_n)$  e $t=(t_1,t_2,...,t_n)$ 
cosa che può essere fatta solo imponendo alcune restrizioni

usando la definizione di probabilità condizionata $P[A,B]=P[A|B]*P[B]$ , possiamo scrivere la PDF congiunta come prodotto di 2 fattori:
$$
\begin{align}
P[X(t_1) \leq x_1,..., X(t_n) \leq x_n,X(t_n+1) \leq x_n+1]= \\ P[X(t_{n+1}) \leq x_{n+1}| X(t_1) \leq x_1,...,X(t_n) \leq x_n]*P[X(t_1) \leq x_1,...,X(t_n) \leq x_n]
\end{align}
$$ 
 ripetendo lo stesso ragionamento otteniamo
$$
\begin{align}
P[X(t_{n+1}) \leq x_{n+1}| X(t_1) \leq x_1,...,X(t_n) \leq x_n]*\\
P[X(t_{n}) \leq x_{n}| X(t_1) \leq x_1,...,X(t_{n-1}) \leq x_{n-1}]*\\
P[X(t_{n-1}) \leq x_{n-1}| X(t_1) \leq x_1,...,X(t_{n-2}) \leq x_{n-2}]*\\...\\ 
P[X(t_1) \leq x_1]
\end{align}
$$

## Classi di processi stocastici
- Processi stazionari: per ogni costante $\tau$ è vero $F_x(x;t+\tau)=F_x(x;t)$  Dove: 
    - $t+\tau=(t_1+\tau,t_2+\tau,...,t_n+\tau)$ 
- Processi indipendenti: se la PDF congiunta ( CDF in caso di spazio continuo) fattorizza a : $f_X(x;t)=f_{X1}(x_1;t_1) ... f_{Xn}(x_n;t_n)$ 
- Processo Markovniano : un processo stocastico con spazio degli stati discreto (una catena) si dice che soddisfa la **proprietà di markov** se: $P[X(t_n+1) = x_n+1| X(t_n)=x_n,...,X(t_1)=x_1]=P[X(t_{n+1})=x_{n+1}| X(t_n)=x_n]$ 

## Catene di markov discrete 
una catena di markov è un processo stocastico con:
- spazio degli stati discreto 
- tempo discreto (insieme indice finito)
- soddisfa la proprietà di markov

per le  DTMC $\{X_n\}$ indichiamo la proprietà di markov come: 

>[!important] Proprietà di markov
$$P[X_n=j|X_1=x_1,...,X_{n-1}=x_{n-1}]=P[X_n=j|X_{n-1}=x_{n-1}]$$ 

se conosciamo la distribuzione di probabilità iniziale  $P[X_0=k]$ possiamo ottenere quella di ogni stato al tempo n.

La parte destra della proprietà di markov è detta :
- probabilità di transizione  $p_{ij}(n)=P[X_n=j|X_{n-1}=i]$ 

se le **probabilità di transizioni** sono indipendenti, abbiamo una DTMC dove:
-  $p_{ij}=P[X_n=j|X_{n-1}=i]$ sono le probabilità di transizione. 
- $\forall i , \sum_j p_{ij}=1$ 

### Rappresentazione grafica 
una DTMC può essere rappresentata come grafo direzionato pesato dove:
- il numero dei nodi è uguale al numero degli stati 
- esiste un arco dal nodo i al j solo se  $p_{ij}>0$ 
- il peso degli archi è uguale as $p_{ij}$ 
![[Pasted image 20231202154042.png]]
### Rappresentazione matriciale 
una DTMC può essere rappresentata come una matrice quadrata P dove:
- la dimensione d è uguale al numero degli stati 
- gli elementi nella **riga** i , **colonna** j sono => $p_{ij}$ 
- **tutte le righe di P sommano a 1** 

Questa è detta essere una matrice stocastico

$$
P = \begin{pmatrix}
p_{11} && p_{12} &&...&&p_{1d}\\
p_{21} && P_{22} &&...&&p_{2d}\\
...\\
p_{d1} && p_{d2} && ... && p_{dd}
\end{pmatrix}
$$

## DTMC omogenee nel tempo 
in una  DTMC omogenea le probabilità di transizione sono stazionarie, per cui **la probabilità di essere in un certo stato n dipende solo dai passi m** .
>[!important] Probabilità di transizione in m passi 
$$p_{ij}^{(m)}=P[X_{n+m}=j|X_n=i]$$

per la proprietà di markov =>  $p_{ij}^{(m)}=\sum_{k}p_{ik}^{(m-1)}p_{kj}$ .

### Proprietà di ricorrenza
>[!important]  Irriducibilità
 > - Una DTMC è irriducibile se ogni stato può essere raggiunto da ogni altro stato $$\forall i,j \ \exists m_0(i,j):p_{ij}^{(m_0(i,j))}>0$$
> - Un sottoinsieme C di uno spazio degli stati si dice chiuso se non è possibile una transizione a un passo da uno degli stati dentro C a fuori. Se |C|=1 quello stato è detto assorbente
 > -  se lo spazio degli stati è chiuso e non contiene nessun sottoinsieme chiuso la catena è **irriducibile**
>  

### Soluzione a una DTMC
Risolvere una  DTMC significa calcolare ==>
- $\pi_j^{(n)}=P[X_n=j]$ =>  che è la probabilità che al passo n la probabilità sia j.

Per farlo bisogna conoscere lo stato iniziale $P[X_0=k]$

in una  DTMC: **omogenea nel tempo, aperiodica e irrudicibile**. 

Le probabilità limite $\pi_j=\lim_{n \rightarrow \infty} \pi_j^{(n)}$ esistono sempre e sono indipendenti dallo stato iniziale. Inoltre:
- **se tutti gli stati sono transienti o ricorrenti nulli**--> $\pi_j=0$ per tutti gli stati e non esiste soluzione stabile 
- **se tutti gli stati sono ricorrenti positivi**  --> $\pi_j>0$ per tutti gli stati e $\{\pi_j\}$ allora è la soluzione stabile $\pi_j=\frac{1}{M_j}$ 

### Probabilità di ritorno 
Con lo scopo di classificare gli stati di una  DTMC definiamo:
- $f_j^{(n)}=$ P\[ritornare allo stato j dopo aver lasciato j]
-  $f_j=\sum^{\infty}_{n=1}f_j^{(n)}$ => probabilità totale di tornare allo stato j
    - se $f_j=1$ lo stato j è ricorrente 
    - se $f_j<1$ lo stato j è transiente
    - se i passi necessari a tornare allo stato j hanno un periodo $\gamma,2 \gamma, 3 \gamma$ dove $\gamma$ è il max(int) che soddisfa questa condizione lo stato j è chiamato periodico con periodo $\gamma$
    - se $\gamma = 1$ lo stato j è aperiodico 
⚠  $M_j=\sum^{\infty}_{n=1}nf_j^{(n)}$  => Tempo di ricorrenza medio
- se $M_j=\infty$ lo stato j è chiamato ricorrente nullo 
- se $M_j<\infty$ lo stato j è chiamato positivamente ricorrente  

### Tempo di soggiorno per DTMC 
Le unità di tempo spese ininterrottamente in un unico stato si distribuiscono geometricamente. Assumiamo di essere appena entrati nello stato j: 
- La probabilità che il prossimo stato sia j è $p_{jj}$ 
- caso duale $1-p_{jj}$ 

grazie alla proprietà di assenza di memoria di markov,  **la probabilità che il prossimo sia j non dipende da quante volte ci siamo entrati** . 

In questo modo la probabilità che il prossimo stato sia j dopo m passi è $(1-p_{jj})p_{jj}^m$ 
la distribuzione geometrica è l'unica che gode dell'assenza di memoria.
### DTMC Distribuzione degli stati transienti
sia:
- $\pi^{(n)} = [\pi^{(n)}_0,\pi^{(n)}_1,\pi^{(n)}_2,...]$ il vettore di probabilità di ogni stato della DTMC all'ennesimo passo (ogni elemento rappresenta la probabilità di essere nello stato i al passo n). 

così $\forall i, \pi_i^1=\pi_0^0p_{0i}+\pi_1^0p_{1i}+\pi_2^0p_{2i}+...$  , in forma matriciale=>

$\pi^{(1)}=\pi^{(0)}P$ (i.e. la distribuzione al passo 1 è uguale a sommare le probabilità al passo 0 col prodotto delle proabilità di transizione tra stati).

e così via $\pi^{(2)}=\pi^{(1)}P=\pi^{(0)}P^2$ . Così possiamo dire  $\pi^{(n)}=\pi^{(0)}P^n$. 

inoltre $\pi^{(n)}=\pi^{(n-1)}P$ (possiamo calcolare la probabilità al passo n conoscendo solo lo stato del vettore allo stato precedente i.e vector multiplication method). 


### Ergodicità
- uno stato i è ergodico se è positivamente ricorrente e aperiodico 
- Se tutti gli stati di una DTMC sono ergodici allora la catena è ergodica
 ![[Pasted image 20231203114257.png]]



### Distribuzione asintotiche degli stati
in questo tipo di catene le probabilità asintotiche $\pi_j=\lim_{n \rightarrow \infty}\pi_j^{(n)}$  (i.e la soluzione a regime) **esistono sempre e sono indipendenti dallo stato iniziale**.
Dalla definizione abbiamo $\pi=[\pi_0,\pi_1,\pi_2,...] = \lim_{n \rightarrow \infty}\pi^{(n)}$ 
- se partiamo da $\pi^{(n)}=\pi^{(0)}P^n$ --> $\lim_{n \rightarrow \infty} \pi^{(n)} = \lim_{n \rightarrow \infty}\pi^{(0)}P^n$ , così $\pi = \pi^{(0)}P^{\infty}$. 
- altrimenti partendo da $\pi^{(n)}=\pi^{(n-1)}P$ --> $\lim_{n \rightarrow \infty}\pi^{(n)}=\lim_{\rightarrow \infty}\pi^{(n-1)}P$.
 
in tutti i casi otteniamo $\pi = \pi P$ , questa matrice rappresenta il sistema di equazioni linearmente dipendenti $\pi_j=\sum_i \pi_i p_{ij}$ con la condizione di normalizzazione $\sum_i \pi_i = 1$ otteniamo un'unica soluzione . 

Le righe di  $P^\infty$ sono tutte uguali alla distribuzione asintotica $\pi$ , siccome $\pi=\pi^{(0)} P^\infty$ per ogni valore di $\pi^{(0)}$ 
$$
P^\infty=
\begin{bmatrix}
\pi_0 && \pi_1 && \pi_2 && ... \\
\pi_0 && \pi_1 && \pi_2 && ... \\
\pi_0 && \pi_1 && \pi_2 && ... \\
...
\end{bmatrix}
$$

### Trasformata Z
è possibile usare la trasformata z di  $\pi^{(n)}=\pi^{(n-1)}P$ in modo da ottenere $P^n=C+(n+1)(-\frac{1}{4})^n D_1+(-\frac{1}{4})^nD_2$ e utilizzare così un metodo computazionalmente meno costoso per calcolare la nostra soluzione, C e le due D sono kernels ben conosciuti.

Sia:
- $\Pi(z)= \sum^{\infty}_{n=0}\pi^{(n)}z^n$ dove :
    - z è valore complesso con $|z| \leq 1$

con un pò di algebra otteniamo $\Pi(z)= \pi^{(0)}[I-zP]^{-1}$ . Usando l'anti trasformata otteniamo $\pi^{(n)}=\frac{1}{n!}\frac{d^n \Pi(z)}{dz^n}$ e per inversione della matrice $[I-zP]^{-1}$ otterremo la soluzione.

## DTMC non omogenee
sia:
- $p_{ij}(m,n)= Pr\{X_n=j|X_m=i\}$ la probabilità che la catena sia nello stato j al passo n sapendo che era nello stato i al passo m $n \geq m$ . 
- 
La transizione tra i e j deve essere avvenuta allora in uno stato intermedio k (i-->k-->j). 
la cui probabilità può essere espressa come  $p_{ij}(m,n) =\sum_k Pr\{X_n=j,X_q=k|X_m=i\}$.

### Equazioni di chapman kolmogorov 
usando la definizione di probabilità condizionale, condizionando entrambi i lati di A$P[B,C|A]=P[B|A]*P[C|A,B]$ 
sia:
- A-->$X_m=i$ , B-->$X_q=k$ , C-->$X_n=j$ allora
- $p_{ij}(m,n)=\sum_kPr\{X_q=k|X_m=i\}Pr\{X_n=j|X_q=k,X_m=i\}$ 

Per cui usando la proprietà di markov otteniamo l'equazione 
>[!important] Chapman Kolmogrov
>$$
p_{ij}(m,n)=\sum_kp_{ik}(m,q)p_{kj}(q,n)
$$
 
(i.e la probabilità di transizione è la somma di tutte le probabilità di transizione da i a k e da k a j). 

per le DTMC omogenee si semplifica a  $p_{ij}^{(n-m)}=\sum_kp_{ik}^{(q-m)}p_{kj}^{(n-q)}$  
###  Probabilità di transizione 
la matrice P è questa volta una funzione del tempo n $P(n)=[p_{ij}(n,n+1)]$ . Perciò non essendo omogenea non possiamo dire che le probabilità saranno P alla m dopo m passi.
sia:
- $H(m,n)=[p_{ij}(m,n)]$ 
- :LiArrowRightCircle: $H(n,n+1)=P(n)$.

in forma matriciale le equazioni di CK si leggono come  
>[!important] Forward Chapman kolmogrov
>$$H(m,n)=H(m,q)H(q,n)$$ con la condizione addizionale $H(n,n)=I$ 

>[!important] Backward champan kolmogrov
> $$H(m,n)=P(m)H(m+1,n)$$ 
> 

entrambe descrivono lo stesso fenomeno, in modo simile si può mostrare che  $\pi^{(n+1)}=\pi^{(n)}P(n)$  la cui soluzione è  $\pi^{(n+1)}=\pi^{(0)}H(0,n+1)$ 
 
e anche nella versione omogenea nel tempo  $\pi^{(n+1)}=\pi^{(0)}P^{n+1}$

### Equazioni di bilanciamento globale 
l'equazione matriciale per le probabilità degli stati asintotiche è $\pi=\pi P$ il cui j-esimo componente è $\pi_j=\sum_i \pi_ip_{ij}$ che può anche essere scritto come 
$$
(1-p_{jj})\pi_j=\sum_{i \neq j}\pi_i p_{ij}
$$
Lato sinistro:
- $P_{jj}$ probabilità che la massa di probabilità $\pi_j$ non fluisca fuori da j. 
- $(1-p_{jj})$ => caso duale al precedente. 
- $(1-p_{jj})\pi_j$ frazione di massa di probabiltà che fluisce fuori da j. 

Lato destro:
per ogni altro stato i dove $i \neq j$ :
- la quantità $\pi_ip_{ij}$ è la massa di probabilità che fuoriesce da i e entra in j. 
- Ne segue che $\sum_{i \neq j} \pi_i p_{ij}$ è la probabilità totale che fluisce dentro j. 

###  DTMC: Equazione di bilanciamento dettagliata
per un vettore $\pi$ l'equazione di bilanciamento dettagliata è valida per ogni  i,j Se 
$$
\pi_ip_{ij}=\pi_jp_{ji}
$$
lato sinistro :
frazione di massa di probabilità $\pi_i$ uscente da i che va in j

lato destro:
frazione di probabilità di massa $\pi_j$ uscente da j che va in i

### DTMC: Processo di nascita e morte
caso speciale di  DTMC, in cui:
- Esiste una popolazione formata da N individui (stati)
- lo stato può cambiare di una sola unità alla vota.
- le probabilità di transizione non cambiano col tempo (**tempo omogenea**)

$$
p_{ij}=
\begin{cases}
&d_i && j=i-1\\
&1-b_i-d_i && j=i\\
&b_i && j=i+1\\
&0
\end{cases}
$$
Quando la DTMC è nello stato i:
- $b_i$ probabilità che ci sia una nascita, se la popolazione è limitata allora $b_N=0$ e la N+1 esima riga è $[0...0 \ d_n \ 1- d_n]$ 
- $d_i$ probabilità che una morte occorra
- $1-b_i-d_i$ probabilità che non succeda nulla

#### Equazioni di bilanciamento 
- per tutti gli stati i>0: $\pi_i(b_i+d_i)=\pi_{i-1}b_{i-1}+\pi_{i+1}d_{i+1}$
- se i = 0 : $\pi_0b_0=\pi_1d_1 \Rightarrow \pi_1=\pi_0 \frac{b_0}{d_1}$ 

per cui, per ogni i
$$
\pi_i=\pi_0*\frac{b_0 b_1 ... b_{i-1}}{d_1 d_2 ... d_i} 
$$
con la condizione di normalizzazione $\sum_i \pi_i=1$ per cui otteniamo anche $\pi_0=\frac{1}{\sum^{\infty}_{i=0}\prod^{i}_{h=1}\frac{b_h-1}{d_h}}$ 
quando entrambe le probabilità di nascita e morte sono indipendenti $\begin{cases}b_i=b & \forall i \\ d_i=d & \forall i\end{cases}$  e $\pi_i=\pi_0(\frac{b}{d})^i$ 

se $b<d$ tutti gli stati sono positivamente ricorrenti  $\pi_0=(1-\frac{b}{d})$  e $\pi_i=(1-\frac{b}{d})(\frac{b}{d})^i$ 


## Catene di markov a tempo continuo
un processo stocastico $\{X(t)\}$ è una catena di markov a tempo continuo se:
per ogni intero  n e per ogni sequenza di istanti di tempo $t_0,t_1,t_2,...,t_n$ tali che 
 ($t_0<t_1<...<t_n<t$) allora

$$
Pr\{X(t)=x|X(t_n)=x_n,X(t_{n-1})=x_{n-1},...,X(t_0)=0\}=Pr\{X(t)=x|X(t_n)=x\}
$$
Di nuovo , lo stato futuro dipende solo dallo stato corrente

### Sojourn time in CTMC
 a causa della proprietà di assenza di memoria, i tempi di soggiorno nelle CTMC sono distribuiti come Variabili aleatorie negative esponenziali.

sia:
- $\tau_i$ la variabile aleatoria di cui vogliamo calcolare il tempo di soggiorno

la distribuzione del tempo aggiuntivo in cui si sta i non dipende dal tempo già passato in esso. Per cui si può dire che $Pr\{\tau_i > s+t|\tau_i >s\} = h(t)$ . dove:
- h(t) è una funzione del tempo aggiuntivo t che non dipende dal tempo già speso s. 

usando la probabilità condizionale $h(t)=\frac{Pr\{\tau_i> s+t\}}{Pr\{\tau_i>s\}}$  , poichè $\tau_i>s+t$ => $\tau_i>s$ 
$Pr\{\tau_i>s+t\}=Pr\{\tau_i>s\}h(t)$ 

se impostiamo s=0 osserviamo che $Pr\{\tau_i>0\}=1$ otteniamo quindi $Pr\{\tau_i>t\}=h(t)$ per cui 
$$Pr\{\tau_i>s+t\}=Pr\{\tau_i>s\}Pr\{\tau_i>t\}$$

sia $f_{\tau_i} = \frac{d}{dx}(P[\tau_i \leq x])$ la pdf della variabile aleatoria $\tau_i$ , allora 
1) $\frac{d}{dx}(P[\tau_i>x])=\frac{d}{dx}(1-P[\tau_i \leq x])=-f_{\tau_i}(x)$ 
2) deriviamo $P\{\tau_i>s+t\}= P\{\tau_i\}P\{\tau_s\}$ rispetto a s $\frac{dP\{\tau_i>t+s\}}{ds}=-f_{\tau_i}(s)P\{\tau_i>t\}$ 
3) sia s= 0 e dividiamo per $P\{\tau_i>t\}$ --> $\frac{dP\{\tau_i>t\}}{P\{\tau_i>t\}}=-f_{\tau_i}(0)ds$ 
4) $\int^{t}_{0}-f_{\tau_i}(0)ds=\log_eP\{\tau_i>t\}=-f_{\tau_i}(0)t$ --> $P\{\tau_i>t\}=e^{-f_{\tau_i}(0)t}$ 
5) da 1 --> $f_{\tau_i}(t)=f_{\tau_i}(0)e^{-f_{\tau_i}(0)t}$  
h(t) è la distribuzione sia del tempo aggiuntivo sia del tempo di soggiorno, per cui l'unica possibile distribuzione è $f_X(x)=\lambda e ^{-\lambda x}$ con $E[X]=\frac{1}{\lambda}$  

### CTMC: Soluzione del transitorio
sia:
- $p_{ij}(m,n)=P[X_n=j|X_m=i]$ per il caso discreto 
- $p_{ij}(s,t)=P[X(t)=j|X(s)=i]$. per il caso continuo (in funzione del tempo in sostanza)

come nel caso delle  DTMC $p_{ij}=\sum_kp_{ik}(s,u)p_{kj}(u,t) \ \ \ s \leq u \leq t$ --> in forma matriciale $H(s,t)=[p_{ij}(s,t)]$ 

le equazioni di chapman hanno la forma $H(s,t)=H(s,u)H(u,t)$ , con $H(t,t)=I$ (matrice identità).

sia:
- $P(t)=[p_{ij}(t,t+\Delta t)]$ , 
- $H(s,t+ \Delta t)=H(s,t)P(t)$. 

applicando un pò di algebra otteniamo $$\frac{H(s,t+\Delta t)-H(s,t)}{\Delta t}=H(s,t)\frac{P(t)-I}{\Delta t}$$ sia:
- $Q(t)=\lim_{\Delta t \rightarrow \infty}\frac{P(t)-I}{\Delta t}$ , allora
$$
\frac{\updelta H(s,t)}{\updelta t} = H(s,t)Q(t)
$$

Q(t) è il generatore infinitesimale, per la matrice di transizioni H(s,t), i cui elementi sono
$$
q_{ij}(t)=\begin{cases}
\lim_{\updelta t \rightarrow 0}\frac{p_{ij}(t,t+\Delta t)-1}{\Delta t} & i = j \\ 
\lim_{\Delta t \rightarrow 0} \frac{p_{ij}(t,t+ \Delta t)}{\Delta t} i & i \neq j
\end{cases}
$$
interpretazione:
impostiamo lo stato della  CTMC uguale a i al tempo t  e aspettiamo $\Delta t$ unità di tempo. Se lo stato al tempo $t+ \Delta t$ è j l'esperimento è positivo, ripetere l'esperimento.

Osserviamo che il numero di esperimenti in questa quantità di tempo è $\frac{1}{\Delta t}$ ,allora la media di esperimenti positivi è $\frac{p_{ij}(t,t+\Delta t)}{\Delta t}$ .

Quando $\Delta t \rightarrow 0$ la quantità $q_{ij}(t)$ **rappresenta le transizioni medie da i a j in una unità di tempo**.

$-q_{ii}(t)$ => è il rateo con cui il sistema lascia i al tempo t. Siccome è sempre vero che $\sum_jp_{ij}(s,t)=1$ ne consegue che $\sum_jq_{ij}(t)=0$ per tutti gli stati i. per cui $$q_{ii}(t)= -\sum_{j \neq i}q_{ij}(t) \ \ \ \forall i$$  


###  CTMC: Chapman kolmogrov 

- $\frac{\updelta H(s,t)}{\updelta t} = H(s,t)Q(t)$=> forward chapman kolmogrov.
- $\frac{\updelta H(s,t)}{\updelta s} = -Q(s)H(s,t)$  backward Chapman kolmogorov .

un componente generico dell'equazione forward è
$$
\frac{\updelta p_{ij}(s,t)}{\updelta t} = q_{jj}(t)p_{ij}(s,t)+ \sum_{k \neq j}q_{kj}(t)p_{ik}(s,t)
$$
con condizioni iniziali $p_{ij}(s,s)=\begin{cases}1 & j=i \\ 0 & j \neq i\end{cases}$
stesse equazioni sono vere per le probabilità di stato $\pi_j(t)=P[X(t)=j]$ del caso discreto. può essere mostrato che $\pi(t)=\pi(0)H(0,t)$ similarmente a $\pi^{(n+1)}=\pi^{(0)}H(0,n+1)$ 
che avviene nel tempo discreto.

usando l'equazione forward con s=0 e introducendo $\pi(0)$ otteniamo $\frac{d \pi(t)}{dt}=\pi(t)Q(t)$ 
la cui forma esplicita ci fa ottenere
$$
\frac{d \pi_j(t)}{dt}=q_{jj}(t)\pi_j(t)+\sum_{k \neq j}q_{kj}(t)\pi_k(t)
$$
Questo sistema di equazioni differenziali si risolve tramite la trasformata di Z e di Laplace. 
Un equazione esplicita è possibile se Q(t)=Q (q non dipende dal tempo t). la soluzione si semplifica a $\pi(t)=\pi(0)H(t)$ dove:
- $H(t)=e^{Qt}$  e quindi 
$$
e^{Qt}=\sum^{\infty}_{k=0}\frac{(Qt)^k}{k!} 
$$

### Soluzione a regime
rigordando l'ergodicità --> $\lim_{t \rightarrow \infty} \pi_j(t)=\pi_j$. Se applichiamo il limite temporale alla soluzione del transitorio otteniamo
$$
\lim_{t \rightarrow \infty}\frac{d \pi_j(t)}{dt}=\lim_{t \rightarrow \infty}q_{jj}(t)\pi_j(t)+\lim_{t \rightarrow \infty}\sum_{k \neq j}q_{kj}(t)\pi_k(t)
$$



in una CTMC omogenea si semplifica, ovvero una in qui il generatore infinitesimale Q non cambia nel tempo, a $0=q_{jj}\pi_j+\sum_{k \neq j}q_{kj}\pi_k$ , **in forma matriciale** 
>[!important] soluzione esplicita al sistema 
>$$\pi Q =0$$

aggiungendo la condizione di normalizzazione $\sum_j \pi_j=1$ la soluzione a regime può essere ottenuta.


### Derivazione alternativa delle equazioni CK
information contained in Q can be graphically represented as a state transition diagram. A node for each state and weighted arcs with rate $q_{i,j}$ . Diagonal elements of Q are not represented (they depend on the row values, they are the sum*-1 of the row.). $o(\Delta t)$ is probability of Multiple deaths and births

[continue on slides]

### Processo di nascita e morte a tempo continuo
- una nascita è una transizione da j a j + 1, occorre con tasso $\lambda_i$ 
- una morte è una transizione da  j a j-1, occorre con tasso  $\micro_j$ .
per cui abbiamo $\lambda_j=q_{j,j+1}$  e $\micro_j=q_{j,j-1}$ 

quando $|j-k|>1$ . Siccome sappiamo da $\sum^{}_{k}q_{j,k}=0$ allora $q_{j,j}=-(\lambda_{j}+\micro_{j})$

$$
q=\begin{bmatrix}
-\lambda_{0} & \lambda_{0}  & \dots \\
\micro_{1} & -(\lambda_{1}+\micro_{1}) & \lambda_{1}  & \dots \\
 & \micro_{2} & -(\lambda_{2}+\micro_{2}) & \dots
\end{bmatrix}
$$

assumiamo:
- $p_{k,k+1}=$P\[1 nascita in $(t,t+\Delta t)$ | stato è k\]= $\lambda_k \Delta t + o(\Delta t)$ 
- $p_{k,k-1}$=P\[1 death in $(t,t+\Delta t)$  | stato è k\]= $\micro_k \Delta t + o(\Delta t)$
- P\[0 nascite in $(t,t+\Delta t)$ | stato è k \] = $1 - \lambda_k \Delta t+ o(\Delta t)$
- P\[0 morti in $(t,t + \Delta t)$| state è k] = $1 -\micro_k \Delta t+o(\Delta t)$ 
- $p_{k,k}=$ P\[0 nascite in $(t,t+ \Delta t)$, 0 morti in $(t,t+ \Delta t)$| stato è k\]

 la probabilità di multiple nascite o morti è $o(\Delta t)$ 



### Processo di nascita e morte continuo: diagramma 
![[Pasted image 20231207130743.png]]

Vogliamo ottenere $\pi_{k}(t)=P\{X(t)= k\}$

per derivare CK notiamo che se assumiamo di essere in k a t, allora in $t+\Delta t$ 3 eventi esclusivi possono accadere:
- a $t+ \Delta t$ lo stato è k e non è successo nulla 
- è avvenuta una nascita 
- è avvenuta una morte 

### equazioni di Chapman Kolmogrov
Formalmente CK al tempo $t+\Delta t$ diviene 

---
$\forall k\geq 1$
$$
\pi_{k}(t+\Delta t) = \pi_{k}(t)p_{k,k}(\Delta t)+\pi_{k-1}(t)*p_{k-1,k}(\Delta t)+\pi_{k+1}(t)p_{k+1,k}(\Delta t)+o(\Delta t)
$$
---
$k=0$

$$
\pi_{0}(t+\Delta t)= \pi_{0}(t)p_{0,0}(\Delta t)+\pi_{1}(t)p_{1,0}(\Delta t)+o(\Delta t)
$$
---

con la condizione che $\sum_{k}\pi_{k}(t)= 1$

- usando le ipotesi precedenti su nascita e morte in $t+\Delta t$
- raggruppando i quantili moltiplicati per $o(\Delta t)$ e negando $[o(\Delta t)]^2$ 
- manipolando algebricamente , otteniamo: 

---
$\forall k\geq 1$ 
$$
\frac{\pi_{k}(t+\Delta t)-\pi_{k}(t)}{\Delta t}= -\pi_{k}(t)(\lambda_{k}+\micro_{k})+\pi_{k-1}(t)\lambda_{k-1}+\frac{o(\Delta t)}{\Delta t}
$$
---
$k=0$
$$
\frac{\pi_{0}(t+\Delta t)-\pi_{0}(t)}{\Delta t}=-\pi_{0}(t)\lambda_{0}+\pi_{1}(t)\micro_{1}+\frac{o(\Delta t)}{\Delta t}
$$
---
prendendo il limite $\lim_{ t \to 0 }\left( \frac{o(\Delta t)}{\Delta t} \right)$

---
$\forall k\geq 1$ 
$$
\frac{d\pi_{k}}{dt}=-\pi_{k}(t)(\lambda_{k}+\micro_{k})+\pi_{k-1}(t)\lambda_{k-1}+\pi_{k+1}\micro_{k+1}
$$
---
$k=0$
$$
\frac{d\pi_{0}}{dt}=-\pi_{0}(t)\lambda_{0}+\pi_{1}(t)\micro_{1}
$$
---

la soluzione a questi sistemi è difficile da calcolare perchè si tratta di equazioni differenziali

### Processo di pura nascita 
definito come : all rates $\micro_k=0$ per ogni $k \geq  1$ , $\lambda_k=\lambda$ per ogni $k \geq 0$ , il sistema di equazioni differenziali diventa
$$
\begin{cases}
\frac{d \pi_k(t)}{dt}= -\lambda \pi_k(t)+ \lambda \pi_{k-1}(t) & k \geq 1 \\
\frac{d \pi_0(t)}{dt} = -\lambda \pi_0(t)
\end{cases}
$$
al tempo 0 assumiamo 0 elementi nella popolazione => $\pi_{k}(0)=1$ per k = 0 oppure $\pi_{k}(0)=0$ altrimenti.

La seconda equazione differenziale porta $\pi_{0}(t)=e^{-\lambda t}$, usando questo valore per k=1 nell'equazione globale otteniamo 
$$
\frac{d \pi_1(t)}{dt}= -\lambda \pi_1(t)+\lambda e ^{-\lambda t}
$$
con soluzione $\pi_1(t)=(\lambda t)e^{-\lambda t}$ , e per induzione 
$$\pi_k(t)=\frac{(\lambda t)^k}{k!}e^{-\lambda t}$$  per k>0 e $t \geq 0$ 

che è una distribuzione di poisson, ne segue che un processo di pura nascita il cui rateo $\lambda$ è costante genera una sequenza di eventi che rappresenta un processo di Poisson. la probabilità che il tempo $\tau$ tra 2 nascite consecutive sia $\leq t$ è 
$$
1-P\{\tau-t\} = 1-\pi_{0}(t)= 1-e^{-\lambda t}
$$
### Processo di pura nascita: trasformata z
Un metodo alternativo per ottenere l'equazione del processo di pura nascita è usare la trasformata Z.
sia:
- $f_n$ => $F(z)= \sum^{\infty}_{k=0}f_kz^k$ 
- una nota proprietà della trasformata Z è che $f_n=\lim_{z \rightarrow 0} \frac{1}{n!}\frac{d^nF(z)}{dz^n}$.

poichè $$
\frac{d^{nF(z)}}{dz^{n}} = \frac{d^n}{dz^n}\left( \sum^{\infty}_{k=0}f_{kz^n} \right)=n!f_{n}+\sum^{\infty}_{k=n+1}\left( \frac{k}{(k-n)!} \right)z^{k-n}
$$

per ottenere la trasformata z di una sequenza $\pi_k(t)$ per tutti i k:
$$P(z,t)=\sum^{\infty}_{k=0} \pi_k(t)z^k$$
moltiplica ogni equazione differenziale di stato k per $z^k$
$$
\begin{cases}
z^0 \frac{d \pi_0(t)}{dt}= -\lambda \pi_0(t)z^0 \\
z^k \frac{d \pi_k(t)}{dt} = -\lambda \pi_k(t)z^k+\lambda \pi_{k-1}(t)z^k & k \geq 1
\end{cases}
$$
somma su k tutti i lati 
$$
\sum^{\infty}_{k=0}z^k \frac{d \pi_k(t)}{dt}=-\lambda \sum^{\infty}_{k=0}\pi_k(t)z^k+\lambda z \sum^{\infty}_{k=1}\pi_{k-1}(t)z^{k-1} 
$$
otteniamo quindi $$\frac{d P(z,t)}{dt}= -\lambda(1-z)P(z,t)$$ siccome $\lim_{z \rightarrow 1}P(z,t)=1$ abbiamo $P(z,t)=e^{-\lambda(1-z)t}$ 

per cui $\pi_0(t)=\lim_{z \rightarrow 0}P(z,t)=e^{-\lambda t}$ 
e $\pi_k(t)=\lim_{z \rightarrow 0}\frac{1}{k!}\frac{d^kP(z,t)}{dz^k}=e^{-\lambda t}\frac{(\lambda t)^k}{k!}$ 




### Processo di nascita e morte costante 
processo con tassi $\lambda_k = \lambda$  e $\micro_k=\micro$ per k=0,1,2.... 

le equazioni CK si ottengono in questo modo

$k \geq 1$ 
$$
\frac{d \pi_k(t)}{dt}= -(\lambda+\micro)\pi_k(t)+\lambda \pi_{k-1}(t)+\micro \pi_{k+1}(t)
$$
k =0 
$$
\frac{d \pi_0(t)}{dt}= -\lambda \pi_0(t)+\micro \pi_1(t)
$$
Usiamo la trasformata Z come nel caso precedente

$$
\pi_k(t) = e^{-(\lambda+\micro)t}[\rho^{\frac{k-n}{2}} I_{k-n}(\alpha t) + \rho^{\frac{k-n-1}{2}}I_{k+n+1}(\alpha t) + (1-\rho)\rho^k \sum^{\infty}_{j=k+n+2}\rho^{-\frac{j}{2} I_j(\alpha t)}]
$$
dove:
- $\rho = \frac{\lambda}{\micro}$  
- $\alpha = 2 \micro \rho ^{\frac{1}{2}}$   
$$
I_k(x)= \sum^{\infty}_{m=0} \frac{(\frac{x}{2})^{k+2m}}{(k+m)!m!}
$$
è la funzione di bessel modificata di ordine k.
### Processo di nascita e morte costante: soluzione a regime 
vogliamo calcolare $\pi_k = \lim_{t \rightarrow \infty}\pi_k(t)$ , 

riprendendo le equazioni di CK

$k \geq 1$ 
$$
\frac{d \pi_k(t)}{dt}= -\pi_k(t)(\lambda_k+ \micro_k)+ \pi_{k-1}(t)\lambda_{k-1}+ \pi_{k+1}(t)\micro_{k+1}
$$

k = 0
$$
\frac{d \pi_0(t)}{dt}=-\pi_0(t)\lambda_0+ \pi_1(t)\micro_1
$$
durante una lunga esecuzione le variazioni si annullano, per cui 
- $0=-(\lambda_k+\micro_k)\pi_k+\lambda_{k-1}\pi_{k-1}+\micro_{k+1}\pi_{k+1}$ 
e
- $0=-\lambda_0\pi_0+ \micro_1\pi_1$ 

(ha portato a 0 i differenziali)

con la condizione di normalizzazione : $\sum^{\infty}_{k=0}\pi_k=1$ 

impostiamo:
- $\lambda_{-1}=\lambda_{-2}=...=0$ 
- $\micro_{-1}=\micro_{-2}=...=0$ 
- $\pi_{-1}=\pi_{-2}=...=0$

per cui abbiamo bisogno solo di 
$0=-(\lambda_k+\micro_k)\pi_k+\lambda_{k-1}\pi_{k-1}+\micro_{k+1}\pi_{k+1}$ e la condizione di normalizzazione

per un insieme di stati fino a k $\frac{d(\sum^{k}_{h=0}\pi_h(t)}{dt}= -\pi_k(t)\lambda_k+\pi_{k+1}(t)\micro_{k+1}$ 
in equilibrio$\lambda_k \pi_k = \micro_{k+1} \pi_{k+1}$ 

 
### Soluzione ai processi di nascita e morte
$$
\begin{align}
\pi_k=\frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\micro_1 \micro_2 ... \micro_k} \pi_0 

&& \pi_0=\frac{1}{1+\sum^{\infty}_{k=1} \prod^{k-1}_{j=0}\frac{\lambda_j}{\micro_j+1}}
\end{align}
$$
la soluzione precedente è una distribuzione se $\pi_0 > 0$  ciò implica che alcune limitazioni sono necessarie ai tassi di nascita e morte, sia:
- $S_1 = \frac{1}{\pi_0}=\sum^{\infty}_{k=0} = \sum^{\infty}_{k=0} \prod^{k-1}_{j=0} \frac{\lambda_j}{\micro_j+1}$ 
- $S_2 = \pi_0 \sum^{\infty}_{k=0}\frac{1}{\pi_k \lambda_k}= \sum^{\infty}_{k=0}\frac{1}{\frac{\pi_k}{\pi_0}\lambda_k}= \sum^{\infty}_{k=0}\frac{1}{\lambda_k \prod^{k-1}_{j=0}\frac{\lambda_j}{\micro_j+1}}$ 
$\pi_k \lambda_k$ rappresenta il tasso di crescita della popolazione .

| tutti gli stati sono | se                          | per cui                          |
| -------------------- | --------------------------- | -------------------------------- |
| ERGOIC               | $S_1 < \infty, S_2= \infty$ | $\forall k, \pi_k>0$             |
| NULL RECURRENT       | $S_1= \infty, S_2=\infty$   | $\pi_k \lambda_k \rightarrow 0$  |
| TRANSIENT            | $S_1= \infty, S_2< \infty$  | $\pi_k \lambda_k \nrightarrow 0$ |
l'ergodicità è garantita se $\exists k_0<\infty$ tale che $\frac{\lambda_k}{\micro_{k+1}}<1$ ,$\forall k > k_0$  per cui $\micro_{k+1} \pi_{k+1} > \lambda_k \pi_k$.
#### Caso limite
$$
\frac{\lambda_k}{\micro_{k+1}} = 1
$$
 $\lambda$ costanti otteniamo:
 -  $S_1=\sum^{\infty}_{k=0}\prod^{k-1}_{\infty}1=\infty$ 
 - $S_2=\sum^{\infty}_{k=0} \frac{1}{\lambda}$  
 
 entrambi $\infty$ per cui gli stati sono ricorrenti nulli

impostiamo $\lambda_k=\lambda k ^\alpha,k=0,1,2...$  per $\alpha=1,2,...$ otteniamo: 
- $S_1=\infty$ 
- $S_2=\frac{1}{\lambda}\sum^{\infty}_{k=0}\frac{1}{k^\alpha}$ 

#### Caso speciale 
$\lambda_k = \lambda$  k = 0,1,2,...  | $\micro_k = \micro$ k=1,2,3... tale che $\rho= \frac{\lambda}{\micro}<1$ , le equazioni diventano

$$
\begin{align}
\pi_0 = \frac{1}{1+\sum^{\infty}_{k=1}\rho^k}= 1- \rho && \pi_k = \frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\micro_1 \micro_2 ... \micro_k} \pi_0 = \pi_0\rho^k
\end{align}
$$

con soluzione $$\pi_k = (1-\rho)\rho^k$$

