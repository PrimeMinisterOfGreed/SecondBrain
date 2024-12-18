
## Quantità assiomatiche

-  $T$ => lunghezza del periodo d'osservazione
-  $B$ => frazione di tempo per cui il sistema è occupato 
-  $C$ => Job completati 
-  $A$ => Numero di arrivi

### Quantità derivate 

-  $\lambda = \frac{A}{T}$  job/sec -> Rateo di arrivi
-  $X= \frac{C}{T}$ => throughput
-  $U= \frac{B}{T}$ => Utilizzo
-  $S = \frac{B}{C}$ => tempo di servizio medio 


### Saturation
- $U = X*S$  -> legge dell'utilizzazione
- $A = C$  -> equilibrio dei flussi/ equilibrio operazionale 
- $U= \lambda*S$ 
- Saturation =>  $U \leq 1$ -> $X \leq  \frac{1}{S}$  e $\lambda \leq \frac{1}{S}$ 
Se $X = \frac{1}{S}$  =>  **il sistema è saturato**

## Statistiche del cliente 
- $a_k$  = tempo di arrivo del k-th cliente 
- $c_k$ = Instante in cui il cliente lascia il sistema  ( $c_k \gt a_k \geq 0$)
- $w_k = c_k - a_k$ Tempo di attesa del k-esimo cliente
- $\bar{w} = \frac{1}{C} \sum^{C}_{k=1}{w_k}$ tempo d'attesa medio 
## Formula di little ⚠

- $\bar{n} = X*\bar{w}$ -> legge del tempo d'attesa :LiAward:
- $\bar{n} = \lambda*\bar{w}$ -> formula di little :LiAward:

![[Pasted image 20231001123801.png]]

formula di little senza equilibrio operazionale 
$\bar{n} = \frac{G(T)}{T}$  e $\bar{w} = \frac{G(T)}{A(T)}$  --> $\bar{n} = \frac{A(T)}{G(T)} \bar{w} X$ 

## Reti di code
i = 1,...,M ->Indice per ogni stazione. 0 sta ad indicare una stazione esterna. :LiArrowLeftCircle:

- $U_i= X_iS_i$ , $X_0= \frac{C_0}{T}$ , $\lambda_0 = \frac{A_0}{T}$  --> in equilibrio operazionale. $\lambda_0 = X_0$ ⚠
- $V_i$  Numero di richieste di servizio alla stazione i $V_i = \frac{C_i}{C_0}$ ⚠
- $D_i$ Domanda totale di servizio  $D_i = V_iS_i=\frac{B_i}{C_0}$ 


### Leggi di consistenza
- $X_0 = \frac{C_0}{T} =\frac{1}{V_i}X_i = \frac{X_i}{V_i}$  -> throughput in termini di visite 
- $X_0 = \frac{C_0}{T} = \frac{1}{D_i} = \frac{U_i}{D_i}$  -> throughput in termini di utilizzazioni

>[!definition] Leggi di consistenza  
>$$\frac{X_i}{X_j} = \frac{V_i}{V_{j}}\implies\frac{U_i}{U_j} = \frac{V_iS_i}{V_jS_j} = \frac{D_i}{D_j}$$ 
>

il throughput e l'utilizzazione sono misure che variano a seconda del carico del sistema, i rapporti rimangono stabili tra una stazione e l'altra.
Le visite sono invece una caratteristica che varia da stazione a stazione.

### Rappresentazione matriciale 

- $C_i$ Numero di partenze dalla stazioni i
- $C_{i,j}$ Porzioni di partenze che si muovono da i a j
==>$C_i=\sum^{M}_{j=0}{C_{i,j}}$ :LiXSquare:

- $q_{i,j} = \frac{C_{i,j}}{C_i}$ Tasso di transizioni da i a j ==>  $\frac{C_{i,j}}{T} = q_{i, j}X_i$ :LiXSquare:

Se siamo in equilibrio operazionale -> $A_i = C_i$, e quindi  $X_j = \sum^{M}_{i=0}{X_iq_{i,j}}$  che può essere scritto come  $\boldsymbol{X}= \boldsymbol{X}\boldsymbol{Q}$   

Dove :
- $\textbf{X} = (X_0,...,X_M)$  --> è un vettore di M+1 componenti che rappresenta i throughput
- $\textbf{Q}$ Matrice quadrata (M+1) x (M+1) composta dai  $q_{i,j} = \frac{C_{i,j}}{C_i}$ , questa matrice caratterizza completamente il sistema. 

Ne segue che l'equazione di bilanciamento dei flussi può essere riscritta come $$\frac{X_j}{X_0}  = \sum^{M}_{i=0}\frac{X_i}{X_0}q_{i,j}$$ 

#### Regola di Little per Reti di Code 
usando $V_j=\frac{X_j}{X_0}$  e sapendo che $V_0 = 1$ è possibile definire la matrice  $\textbf{V} = \textbf{V}\textbf{Q}$ che può essere usata per descrivere il sistema. Ciò è possibile grazie alle leggi di consistenza. Ne segue anche che  $$\bar{n_i} = X_i\bar{w_i}$$  Dove:
- $\bar{n_i}$ => numero medio di clienti alla stazione i
- $\bar{w_i}$ => tempo d'attesa medio

## Dipendenza dal carico 
- $T(n)$ => Tempo speso dal cliente dentro al sistema
- $K_{max}$ => Massimo numero di clienti simultaneamente presenti dentro al sistema  

==> $T = \sum^{K_{max}}_{n=0}T(n)$  e $B=T-T(0)$  

#### Comportamento dipendente dal carico 

- $\phi(k) = \frac{T(k)}{T}; k=0,...,K_{max}$ => frazione di tempo spesa dal sistema nello stato k
- $C(k)$ -> numero di completamenti con k clienti   -> $\sum^{K_{max}}_{k=1}{C(k)} = C$ 
- $S(k) = \frac{T(k)}{C(k)}$ -> tempo medio di servizio dipendente dal carico o **funzione di servizio** 
- $X = \sum^{K_{max}}_{k=1}{\frac{1}{S(k)}{\phi(k)}}$ => throughput generalizzato 

### Comportamento dipendente dal carico per reti di code 
- $T_i(k)$ => Tempo speso dal cliente nella stazione i (i=1,...,M) 
Usando questa quantità possiamo scrivere:
- $\sum^{K_{max}}_{k=0}T_i(k) = T;i=0\dots M$  e quindi 
- $\phi_i(k) = \frac{T_i(k)}{T}$ => frazione di tempo spesa da ogni cliente nella stazione I. 

Sia:
- $C_i(k)$  (i=1,...,M) => il numero di completamenti con k clienti in coda alla stazione i
 - $\sum^{K_{max}}_{k=1}C_i(k)=C_i$   (i=0,..,M) anche in questo caso 
Si può quindi definire nuovamente => $S_i(k)= \frac{T_i(k)}{C_i(k)}$  (i=0,...,M;k=1,...,$K_{max}$)  

e di nuovo $X_i=\sum^{K_{max}}_{k=1}\frac{1}{S_i(k)}\phi_i(k)$  (i=0,...,M)

## Tempo di Risposta 

Con $V_i$ e $\bar{w_i}$ è possibile calcolare il tempo impiegato dal cliente per attraversare il sistema in 
2 tipi di sistema :
- Sistemi aperti:
    - I nuovi clienti arrivano con tasso $\lambda$ .
    - Il loro numero può aumentare a $\infty$ .
    - fino a che il sistema non è saturato abbiamo $X_0 = \lambda$ 
- Sistemi chiusi: 
    - Numero fisso N di clienti nel sistema
    - I clienti che escono vengono rimpiazzati subito con nuovi clienti 
### Tempo di risposta: Caso dei sistemi aperti

- $\Omega_i=V_i\bar{w_i}$ (i=1,...,M) => tempo medio speso dal cliente nella stazione i
- $R = \sum^{M}_{i=1}\Omega_i$ => Tempo medio di risposta del sistema (o tempo di risposta medio dei clienti all'interno del sistema 

usando la regola di Little 
$$\bar{n}=\lambda R=\sum^{M}_{i=1}X_i\bar{w_i}= \sum^{M}_{i=1}{\lambda \Omega_i}=\sum^{M}_{i=1}\bar{n_i}$$
### Tempo di Risposta: Caso dei sistemi chiusi 
N clienti nel sistema. In questo caso la stazione di indice 0 non ha significato e bisogna quindi selezionarne una di riferimento (qui definita **stazione arbitraria** ) perciò $\Omega_i$ sono dipendenti da k.

- $R_k = \sum^{i=1,i \neq k}_{M}{\Omega_i}$  => Tempo di risposta => Tempo impiegato dal cliente per tornare alla stazione k
- $Y_k = \bar{w_k}+R_k = \sum^{M}_{i=1}{\Omega_i}$  => Tempo di ciclo => Tempo medio impiegato dal cliente per fare un tour completo del sistema 

Si può generalizzare prendendo in considerazione un arbitraria stazione k
$$
\begin{aligned}
V_j^{[k]} = \frac{C_j}{C_k} = \frac{X_j}{X_k} = \sum^{M}_{i=1}V_i^{[k]}q_{i,j} &&  j=1,...,m
\end{aligned}
$$

Possiamo espandere la notazione prendendo in considerazione una seconda stazione h
$$
\begin{align}
V_j^{[h]} = \frac{C_j}{C_h} = \frac{V_j^{[k]}}{V_{h^{[k]}}}&& j,h,k=1,...,M
\end{align}
$$      
E per questa stazione scelta calcolare 
$$Y_k = \sum^{M}_{i=1}{\Omega_i}^{[k]} = \sum^{M}_{i=1}{V_i^{[k]}}\bar{w_i}$$ 
e anche 
$$Y_h = \sum^{M}_{i=1}\Omega_i^{[h]} = Y_k\frac{1}{V_h^{[k]}}$$  ottenendo quindi la forma generale 
$$R_h = Y_h - \bar{w_h}$$ ⚠ 


### Sistemi chiusi con stazione di ritardo 
- $Z$ => Ritardo medio della stazione 0 (stazione di ritardo)
usando la stazione di ritardo come referenza si possono calcolare tutte le visite nel sistema. 
Possiamo scrivere 
- $R_0 = \sum^{M}_{i=1}{\Omega_i}$ 
- $Y_0= Z+R_0$. 
Visto che il numero di clienti all'interno del sistema è costante possiamo usare la regola di Little sul sistema come fosse una black box.
![[Pasted image 20231001173621.png]]

in equilibrio operazionale abbiamo => $X_0=\frac{A_0}{T} = \frac{C_0}{T}$. 
Siano:
- $\bar{n_d}$  => il numero medio di clienti nella stazione di ritardo  
- $\bar{n_{cs}}$ => il numero medio di clienti nel sistema centrale 

$$N=X_0Y_0= X_0(Z+R)= \bar{n_d} + \bar{n_{cs}} \implies R_0 = \frac{N_{cs}}{X_0} - Z$$
- $U= n_{cs}/N$ => utilizzo del sistema centrale 



## Analisi del collo di bottiglia 
Usando $V_i$ e $S_i$  possiamo osservare come $\lambda$ cresce in caso di un sistema aperto e di un sistema chiuso a seconda del carico.  

### Analisi del collo di bottiglia: Sistemi aperti 
$S_i$ e $V_i$ sono indipendenti da  $\lambda$ (sono caratteristiche della topologia di rete).

Lo stesso non si può dire per $X_i$ e $U_i$  e quindi devono essere rappresentati in funzione di : $\lambda$ --> $X_i(\lambda)$ e $U_i(\lambda)$. 
[Per la legge di consistenza](###Leggi di consistenza) $\frac{X_i(\lambda)}{X_j(\lambda)} = \frac{V_i}{V_j}$ e $\frac{U_i}{U_j} = \frac{V_iS_i}{V_jS_j}$ , Indipendentemente da $\lambda$. Ne segue che  
- $\lambda_i = \lambda_0V_i$ 
-  In equilibrio operazionale $\lambda \leq \frac{1}{S_i}$ (i=1,...,M).  
- $X_i(\lambda) = \lambda_i = \lambda_0V_i$ e $U_i(\lambda) = X_i(\lambda)S_i$ .

Sia b la prima stazione a raggiungere utilizzo pari a 1. Questa stazione verrà usata per individuare il collo di bottiglia del sistema associato a $\lambda_{max}$ per cui quando superato il **sistema perde l'equilibrio operazionale**.
Se $\lambda>\lambda_{max}$ il sistema raggiunge un punto in cui le code crescono a $\infty$ e il sistema diventa instabile.
Siccome $\frac{U_i(\lambda)}{U_j(\lambda)}$ è fisso per ogni coppia di $i,j$ allora la stazione che si satura prima è quella la cui utilizzazione diviene 1 con la minima condizione di carico. 
Formalmente: $\frac{U_b(\lambda)}{U_i(\lambda)}=\frac{V_bS_b}{V_iS_i}=\frac{D_b}{D_i} > 1$, per identificare l'indice della stazione bottleneck $V_bS_b=max_i(V_iS_i)$ . Possiamo quindi dire che $X_b^{[max]}(\lambda)=\frac{U_b^{[max]}(\lambda)}{S_b} = \frac{1}{S_b}$ --> $\lambda_{max}=\frac{1}{V_bS_b}$ 

### Oltre $\lambda_{max}$ (analisi asintotica)
In alcuni casi è possibile per $\lambda$ crescere oltre $\lambda_{max}$. Questo potrebbe portare a saturare anche le altre stazioni per cui $V_iS_i < V_bS_b$ (a seconda della topologia). 
2 casi sorgono:
1) $V_iS_i > V_jS_j$  $\forall j > i; i,j=1,2,...,M$  in questa rete di code b = 1 e solo la prima stazione può avere $U = 1$ 
2) $V_iS_i \leq V_jS_j$   $\forall j > i; i,j=1,2,...,M$  in questa stazione b=M e tutte le code possono avere $U=1$ , se $\lambda$ diventa sufficientemente grande. 

in entrambi i casi $X \leq \frac{1}{S_b}$ indipendentemente da $\lambda$

![[Pasted image 20231002213059.png]]

### Analisi del collo di bottiglia: sistemi chiusi
Assumendo che $S_i$ e $V_i$ siano indipendenti dal carico del sistema $N$, e concentrando l'analisi su $X$ e $U$ 
- $Y$  --> $X_i(N)$ ,$U_i(N)$ e $Y(N)$ (valido per tutto il sistema) sono dipendenti. 
- anche in questo caso le [leggi di consistenza](###leggi di consistenza) sono valide $\frac{X_i(N)}{X_j(N)} = \frac{V_i}{V_j}$ e $\frac{U_i(N)}{U_j(N)} = \frac{V_iS_i}{V_jS_j}$  indipendentemente da N.

Sia b la stazione che raggiunge prima $U=1$ quando $N$ cresce, questo è il collo di bottiglia della rete, visto che  $\frac{U_i(N)}{U_j(N)}$ è fisso per tutti gli i,j=1,2,...,M. La stazione che raggiunge il massimo  $U$ nella condizione di carico minima 
$\frac{U_b}{U_i}>1$ i=1,...,M $i \neq b$  cosi che $V_bS_b=max_i(V_iS_i)$  

#### Analisi asintotica per sistemi chiusi 
Valori grandi per $N$ portano a:
- $U \approxeq 1$ 
- $X_i(N) \approxeq \frac{1}{S_i}$

Tutte le $V_i$ sono calcolate a partire da una stazione arbitraria k, quindi il throughput del sistema è:
- :LiAward: $X_k(N) = \frac{U_b(N)}{V_bS_b} \approxeq \frac{1}{V_bS_b}$ => massimo throughput possibile nel sistema
    -  :LiArrowRightCircle: $\lim_{N \rightarrow \infty}X_i(N)=\frac{1}{V_bS_b}$
- :LiAward: $D_i$ =>  tempo medio totale di servizio ricevuto dalla stazione i
    - :LiArrowRightCircle: $D=\sum^{i=1}_{M}V_iS_i = \sum^{i=1}_{M}D_i$ => tempo totale medio per un cliente per fare un tour completo del sistema (in questo caso N=1)

D è quindi il tempo di ciclo del sistema $D = Y(1)$ con la formula di little possiamo affermare che se la rete di code è costruita così che i clienti non interferiscono tra di loro :
- :LiAward: $X_k(1)= \frac{1}{Y(1)}$ 
    - :LiArrowRightCircle:  $Y(N)=Y(1)$  
    - :LiArrowRightCircle: $X_k(N)=\frac{N}{Y(N)}= \frac{N}{Y(1)}$ 


Le intersezioni tra gli asintoti identificano un unico punto di saturazione : 
:LiArrowRightSquare: $N^*=\frac{Y(1)}{V_bS_b}$. 
Come per il tempo di ciclo è possibile usare :
- $Y(N)=\frac{N}{X_k(N)}$ con $Y(1)$ => asintoto orizzontale inferiore 
- $Y'(N)=N*V_bS_b$ => secondo limite inferiore che è un asintoto obliquo.

![[Pasted image 20231003110041.png]]

### Analisi del Collo di bottiglia: caso del comportamento dipendente dal carico
Col fine di estendere l'analisi è possibile rendere variabile $S_i$, che adesso diventa una funzione dei clienti $S_i(N)$ , **cosa possibile solo se N ha un limite superiore se** $N \rightarrow \infty$ .

Usando:
:LiArrowRightCircle: $S_i(1) \leq S_i^{[max]} = \lim_{h->\infty} S_i(h)$ 

la discussione fatta per i sistemi chiusi parlando di
:LiArrowRightCircle: $D=Y(1)=\sum^{i=1}_{M}V_iS_i = \sum^{i=1}_{M}D_i$ e $Y(N)=NV_bS_b$  

può essere generalizzata portando a 
:LiArrowRightSquare: $Y(1) = \sum^{i=1}_{M}V_iS_i$ e $Y(N)=NV_bS_b^{[max]}$  --> $V_bS_b^{[max]} = max_i(V_iS_i)^{[max]}$. 

>[!important] Nota
 > 1) Questa discussione perde di significato se la velocità di servizio va 0: questo perchè i clienti verranno proprio bloccati dalla stazione. Perciò la generalizzazione è valida solo per quelle stazioni la cui velocità di servizio non è una funzione del carico. 
> 2) l'espressione per D è uguale a R(1).

#### Caso di code con comportamento dipendente dal carico 
Usando:
:LiArrowRightCircle: $S_i(1) \geq S_i^{[min]} = \lim_{h \rightarrow \infty} S_i(h)$ 

si può generalizzare per :
:LiArrowRightSquare: $Y(1) = \sum^{i=1}_{M}V_iS_i(1)$ e $Y(N)=NV_bS_b^{[min]}$ 

il problema adesso è che $Y(1) = \sum_{i=1}^{M}V_iS_i(1)$ può essere più grande del minimo ciclo di attività del sistema.

#### caso degli infinite server 
Le stazioni infinite server sono quelle con funzione di servizio  $S_i(h)= \frac{S_i(1)}{h} = \frac{Z}{h}$. Queste stazioni hanno una funzione di servizio che non decresce, ma anche non limitata quindi la loro velocità di servizio è 0, motivo per il quale **devono essere scartate durante l'analisi del collo di bottiglia**.

#### caso del server centrale in time sharing

![[Pasted image 20231003212636.png]]

In questo caso un server centrale è time shared da  N terminali connessi al server centrale.

Sia :
- Z => il ritardo associato al singolo terminale 
-  $S_i$ e $V_i$ sono costanti.

:LiQuestionMarkGlyph: Quale sarebbe l'impatto sul comportamento se collegassimo più terminali?
:LiAward: La risposta si può trovare usando la stazione di delay come riferimento per calcolare le performance delle altre stazioni nel sistema.

in questo caso abbiamo: $Y(N) = Z+R(N)$
dove :
- R(N) => tempo di risposta con N terminali connessi.
- l'asintoto obliquo per  $X(N)$ è dato da $X'(N)= \frac{N}{Y(1)} = \frac{N}{[Z+R(1)]}$ 
- $X$ è vincolato da un limite inferiore  $\lim_{N \rightarrow \infty}X_0(N)=\frac{1}{V_bS_b}$.

Il punto di saturazione è quindi $$N^*= \frac{Z}{V_bS_b}+\frac{R(1)}{V_bS_b}$$
Concentrandoci sul tempo di risposta otteniamo 
$$Y(N)=\frac{N}{X(N)} \geq \frac{N}{1/V_bS_b} = NV_bS_b$$ 
di conseguenza l'asintoto del tempo di risposta è  $$R'(N)= N(V_bS_b) - Z$$



# Analisi Operazionale: Stati intermedi    

## Stato intermedio 
L'analisi a stato stabile del sistema non mostra tutti i comportamenti del sistema, è necessario analizzare anche cosa succede negli stati intermedi.
lo stato del sistema è rappresentabile come un vettore $\underline{n} = (n_1,n_2,...,n_m)$  $n_i \geq 0$  $i=1,2,...,M$  

- $S(M)$ => insieme di tutti gli stati possibili 

## Equilibrio di stato in una coda 
assumiamo 3 stati generici , definiti dal numero di clienti in coda a ciascuna stazione => k,m,n.

:LiAward: sia $C(m,n)$ => numero di transizioni dallo stato m allo stato n. 
:LiArrowRightCircle: allora l'equazione di bilanciamento tra stati è $$\sum_{k}C(k,n)= \sum_mC(n,m)$$
In generale , questa equazione è vera per tutti gli stati tranne il primo e l'ultimo. Ad eccezion fatta per i sistemi in equilibrio operazionale per cui **è vera per tutti gli stati**.

![[Pasted image 20231006125755.png]]


### Misure di equilibrio di stato
definiamo:
- :LiArrowRightCircle:  $r(n,m)=\frac{C(n,m)}{T(n)}$ => rateo di transizione da n a m.
- :LiArrowRightCircle:  $p(n)=\frac{T(n)}{T}$ => frazione di tempo spesa con n clienti in attesa

l'equazione di bilanciamento può essere riscritta come $$\sum_kp(k)r(k,n)=p(n)\sum_mr(n,m) \space |\forall n$$    
### Equazioni di bilanciamento
%%aggiungere anche i passaggi%%
$$
\begin{equation}
    \begin{cases}
      p(1)r(1,0)=p(0)r(0,1)\\
      \\
      p(n-1)r(n-1,n)+p(n+1)r(n+1,n)=p(n)[r(n,n+1)+r(n,n-1)]\ \ \ \ 0<n<N \\
      \\
      p(N-1)r(N-1,N)=p(N)r(N,N-1) \\
      \\
      \sum_np(n)=1
    \end{cases}\
\end{equation}
$$

#### Semplificare i ratei di bilanciamento 
usando 
- :LiArrowRightCircle: $C(n,n+1)= A(n)$ => # arrivi osservati quando il sistema è nello stato N; $A(N)=0$
- :LiArrowRightCircle: $C(n,n-1)=C(n)$ => # completamenti osservati allo stato n; $C(0)=0$

possiamo generalizzare a:
- :LiArrowRightCircle: $r(n,n+1)= \frac{A(n)}{T(n)}= \lambda(n)$
- :LiArrowRightCircle: $r(n,n-1)= \frac{C(n)}{T(n)}= \micro(n)$ 

#### Result
il sistema di equazioni può essere riscritto come 
$$
\begin{equation}
    \begin{cases}
    p(n)\micro(n)=p(n-1)\lambda(n-1) \ \ \ 0<n \leq N \\
    \\
    \sum_np(n)=1
    \end{cases}\
\end{equation}
$$

%%this is the final form, you can take the other system and perform the substitution to see the intermediate one%%
 

### Ratei dipendenti dal carico
nella precedente soluzione è presente un interessante relazione
$$
\begin{equation}
\begin{cases}
p(n) = p(0)\prod^{n}_{k=1}\frac{\lambda(k-1)}{\micro(k)} \ \ \ 0<n \leq N \\ 
\\
p(0)= (1+\sum^{N}_{n=1}[\prod^{n}_{k=1}\frac{\lambda(k-1)}{\micro(k)}])^{-1}
\end{cases}
\end{equation}
$$
e indici di performance

- $X= \sum^{N}_{n=1}p(n)\micro(n)$ 
- $\bar{n} = \sum^{N}_{n=1}np(n)$ 
- $\bar{W}=\frac{\bar{n}}{X}$ 

### Omogeneità
I ratei di arrivo sono indipendenti dallo stato del sistema 
    :LiAward: $\lambda(0)= \lambda(1)...=\lambda(N-1)=\lambda$
E lo sono anche i ratei di servizio 
    :LiAward: $\micro(1)=\micro(2)...=\micro(N)=\micro$

definiamo:
 :LiAward: $\rho=\frac{\lambda}{\micro}$ 
per concludere che  :LiArrowRightCircle: $$p(n)= \frac{1-\rho}{1-\rho^{N+1}}\rho^n \ \ \ 0\leq n \leq N$$  
#### Indici di performance asintotici e omogenei

Quando $\rho<1$ se si prende $\lim_{ N \to \infty }$ si può osservare che la quantità di tempo spesa dal sistema in un certo stato assume la **connotazione di una probabilità** 
    :LiAward: $p(n)= (1-\rho)\rho^n$ 

Da cui possiamo derivare 
- :LiArrowRightCircle: $X= \lambda$ => throughput
- :LiArrowRightCircle:  $\bar{n}=\frac{\rho}{1-\rho}$ => lunghezza media della coda 
- :LiArrowRightCircle:  $\bar{W} = \frac{1}{\micro(1-\rho)}$ => templo d'attesa medio 


## Generalizzazione 
Supponiamo che i valori dei ratei di servizio possano cambiare a seconda di un generico stato k. I risultati che si ottengono possono essere riassunti in questo modo:

- [Arrivi scoraggiati](###Arrivi scoraggiati)
- Coda con server multipli  
- Coda con infinite server 
- Coda con spazio d'attesa finito 
- Coda con popolazione fissa 

### Arrivi scoraggiati
- $\lambda(k)=\frac{\lambda}{k+1}$ 
- $\micro(k)=\micro \ \ k \geq 1$  

da questo risultato otteniamo 
$$p(n)= p(0)\prod^{n-1}_{k=0}\frac{\lambda/(k+1)}{\micro}=p(0)(\frac{\lambda}{\micro})^n \frac{1}{n!}$$  

p(0) si può ottenere mediante la sua espressione esplicita

$$
p(0)= [1+ \sum^{\infty}_{n=1}(\frac{\lambda}{\micro})^n \frac{1}{n!}]^{-1}=e^\frac{-\lambda}{\micro}
$$  
e quindi

$$
p(n)= \frac{(\lambda/\micro)^n}{n!}e^\frac{-\lambda}{\micro} 
$$



### Coda infinite server
- $\lambda(k) = \lambda$ 
- $\micro(k) = k \micro$ 

la distribuzione della lunghezza di coda è :LiArrowRightCircle: 
$$
p(n)=p(0) \prod^{n-1}_{k=0}\frac{\lambda}{(k+1)\micro} = p(0)(\frac{\lambda}{\micro})^n \frac{1}{n!} 
$$
un espressione semplice per  p(0) può essere ottenuta per $N \rightarrow \infty$ 
$$p(0) = [1+\sum^{\infty}_{n=1}(\frac{\lambda}{\micro})^n \frac{1}{n!}]^{-1} = e^{-\lambda/\micro}$$ 
Per cui l'espressione generale diventa :LiArrowRightCircle: 
$$
p(n) = \frac{(\lambda/\micro)^n}{n!}e^\frac{-\lambda}{\micro}
$$

### Coda con server multipli
- $\lambda(k) = \lambda$ 
- $\micro(k)= \begin{equation} \begin{cases}  k \micro \ \ \ 0 \leq k \leq m \\ m \micro \ \ m<k \end{cases} \end{equation}$   

La distribuzione del numero dei clienti diventa quindi 
$$
p(n) = 
\begin{equation}
\begin{cases}
p(0)\prod^{n-1}_{k=0} \frac{\lambda}{(k+1)\micro} = p(0)(\frac{\lambda}{\micro})^n \frac{1}{n!} \ \ \ 0 \leq n \leq m \\
\\
p(0) \prod^{m-1}_{k=0} \frac{\lambda}{(k+1)\micro} \prod^{n-1}_{k=m} \frac{\lambda}{m \micro} = p(0)(\frac{\lambda}{\micro})^n \frac{1}{m!m^{n-m}} \ \ \ m<n
\end{cases}
\end{equation}
$$
p(0) può essere derivato per normalizzazione o prendendo il limite $N \rightarrow \infty$ sotto l'assunzione che  $\frac{\lambda}{m \micro} < 1$ 

### Coda con sala d'attesa finita 

- $\lambda(k) = \begin{cases} \lambda \ \ \ 0 \leq k \leq B \\ 0 \ \ \ k>B\end{cases}$  
- $\micro(k)= \micro$

otteniamo 
$$
p(n) = \begin{cases}
p(0) \prod^{n-1}_{k=0} \frac{\lambda}{\micro} = p(0) (\frac{\lambda}{\micro})^n \ \ \ 0 \leq n \leq B 
\\
0
\end{cases}
$$
in questo caso :
$$p(0)= \frac{1-\lambda/\micro}{1-(\lambda/\micro)^{B+1}}$$
e l'espressione generale diventa
$$
p(n) = \begin{cases}
\frac{1-\lambda/\micro}{1-(\lambda/\micro)^{B+1}} \ \ \ 0 \leq n \leq B
\\0 \ \ \ n> B
\end{cases}
$$


### Single queue with fixed number of customers
- $\lambda(k)= \begin{cases}(N-k)\lambda \ \ \ 0 \leq k \leq N \\ 0 \ \ \ k > N\end{cases}$
- $\micro(k)= \micro$ 

  abbiamo: 
$$
p(n)= \begin{cases}
p(0) \prod^{n-1}_{k=0}\frac{(N-k)\lambda}{\micro} = p(0)(\frac{\lambda}{\micro})^n \frac{N!}{(N-n)!} \ \ \ 0 \leq n \leq N \\
0 \ \ \ n > N
\end{cases}
$$
da cui deriviamo 
$$p(0) = [1+\sum^{N}_{n=1}(\frac{\lambda}{\micro})^n \frac{N!}{(N-n)!}]^{-1}$$ 


## Comportamento un passo alla volta

![[Pasted image 20231006152829.png]]
siccome $\sum T(n) = T$  possiamo aggiungere la condizione di normalizzazione $\sum_np(n)=1$. In questo modo **lo stato può cambiare solo alla partenza o all'arrivo di un cliente.**

## State balance of a network of queues

:LiAward: $S(M) = \{\underline{n} =(n_1,n_2,...,n_M), n_i \geq 0 i=1,2,...,M\}$  => Insieme dei possibili stati 

:LiArrowRightCircle: $\underline{k}, \underline{m}$ e $\underline{n}$ => generici stati in S(M).

### Comportamento transitorio
:LiAward: $T(n)$ => tempo totale speso dal sistema in un generico stato $\underline{n}$ durante il periodo di osservazione, con $\sum T(n) = T$. \

Sia :LiArrowRightCircle:  $P(n)= T\frac{n}{T}$=> tempo totale speso dal sistema nello stato  $\underline{n}$. 

l'insieme delle frazioni di tempo spese dal sistema nei vari stati in $S(M)$ or $\{P(\underline{n}), \underline{n} \in S(M)\}$ è chiamata **distribuzione delle frazioni di tempo speso dal sistema nei suoi stati**. l'obiettivo è di derivare $P(\underline{n})$ senza misurarlo ma solo dai parametri del modello . 

Sia $C(\underline{n}, \underline{m})$ => # of direct transition made by the system from state $\underline{n}$ to state $\underline{m}$. In our measurement we can't observe transition within the same state so $C(\underline{n},\underline{n}) = 0$ for any n

### Equilibrio operazionale: stati a regime 
anche in questo caso si richiede $A=C$ per ogni stazione. il numero di partenze e di arrivi deve essere  $n_i(0)= n_i(T) \ \ \  i=1...M$.

**Questo significa che l'equilibrio operazionale è soddisfatto ogni volta che il sistema parte in uno stato e torna in quello stato**. Per un server singolo in isolamento:
$$
\sum_kC(\underline{k},\underline{n}) = \sum_mC(\underline{n},\underline{m}) \ \ \ \forall \underline{n}
$$

si può quindi affermare che: "**la condizione di bilanciamento tra clienti di un sistema è equivalente a bilanciare il numero di transizioni tra gli stati di un sistema**" 

:LiAward: $r(\underline{n},\underline{m})= \frac{C(\underline{n},\underline{m})}{T(\underline{n})}$ . 
:LiAward: $T(\underline{n})=0\implies C(\underline{n}, \underline{m})=0$. Variabili che possiamo introdurre nell equazione di bilanciamento 
$$
\sum_\underline{k} P(\underline{k})r(\underline{k},\underline{n}) = P(\underline{n}) \sum_\underline{m}r(\underline{n},\underline{m}) 
$$
La definizione di P(n) consente di introdurre la normalizzazione:
$\sum_\underline{n}P(\underline{n})=1$ 

### Comportamento a un passo: Misure derivate 
sia H => numero totale di equazioni del sistema, può avere valore:
- $H=(N_{max}+1)^M$  =>  in caso di **sistemi aperti** con al massimo Nmax clienti 
- $H = \binom{N+M-1}{M-1}$  => in caso di **sistemi chiusi** con N clienti

Stando all'ipotesi del comportamento a un passo, gli stati possono transire solo tra stati adiacenti tra di loro.  Introduciamo le seguenti definizioni:
- $\underline{n_{ij}} = (n_1,...,n_i+1,...,n_j-1,...,n_M)$ 
- $\underline{n_{i0}} = (n_1,...,n_i+1,...,n_j,...,n_M)$ 
- $\underline{n_{0j}} = (n_1,...,n_i,...,n_j-1,...,n_M)$ 
che possiamo usare per indicare gli stati adiacenti a:
- $\underline{n} = (n_1,...,n_i,...,n_j,...,n_M)$ 


### Omogeneità 
1) l'output di una stazione è **determinato dalla lunghezza della sua coda** ,ma è indipendente dalla lunghezza delle code delle altre stazioni.
2) i tassi di transizione da uno stato all'altro è invariante nel tempo e dipende al più dal carico del sistema 

### Simplify state transition balance equation (homogeneity)

La prima ipotesi permette di semplificare i ratei di transizione 
$$
r(\bar{n},\bar{n}_{ij})=\frac{C_{ij}(n_{j})}{T_{j}(n_{j})}
$$
La seconda implica che $C_{ji}(n_{j})=C_{j(n_{j})}q_{ji}$
per cui si ottiene
$$
r(\bar{n},\bar{n}_{ij})= 
\begin{cases}
\frac{q_{ji}}{S_{j(n_{j})}}  &  j \rightarrow i  \\
\frac{q_{j_{0}}}{S_{j}(n_{j})} & j \rightarrow 0 \\
\lambda_{0i}  &  0 \rightarrow i
\end{cases}
$$


sia:
- $\sigma(n)= \begin{cases}1 \ \ \ n>0 \\0 \ \ \ n=0\end{cases}$  una funzione indicatrice
 - $\lambda_{0j}$ => rateo di arrivo esterno verso la stazione di indice j
 
Con queste ipotesi le equazioni di bilanciamento assumono questa forma 
$$
\begin{aligned}
\sum^{M}_{i,j=1}P(\underline{n}_{ij}) \frac{q_{ij}}{S_i(n_i+1)}\sigma(n_j) + 
\\
\sum^{M}_{j=1}P(\underline{n}_{0j})\lambda_{0j}\sigma(n_j) + 
\\
\sum^{M}_{i=1}P(\underline{n}_{i0})\frac{q_{i0}}{S_i(n_i+1)}=
\\
P(\underline{n})[\sum^{M}_{i=1}\frac{\sigma(n_i)}{S_i(n_i)} +  \sum^{M}_{j=1}\lambda_{0j}]
\end{aligned}
$$

## Soluzione agli stati di transizione  
Assumiamo:
- che i $V_{i}$ siano calcolati
- $\lambda_i=\begin{cases}\lambda V_i \ \ \ open\ system \\ V_i \ \ \ closed\ system \end{cases}$ , dove $\lambda$ rappresenta il rateo totale di arrivo dall'esterno.  

Definiamo la funzione ⚠ 
$$
f_i(k)= \begin{cases}
1 \ \ \ k = 0 \\
\lambda_iS_i(k)f_i)k-1 \ \ \ k>0
\end{cases}
$$
è possibile mostrare che il tempo speso da ogni cliente nel sistema è pari a
>[!important] Soluzione forma prodotto
>$$P(\underline{n})= \frac{1}{G} \prod^{M}_{i=1}f_i(n_i)$$

Dove: G è una costante di normalizzazione definita nel modo seguente 
$$
1= \sum_{\underline{n}}P(\underline{n}) = \frac{1}{G}\sum_{\underline{n}}\prod^{M}_{i=1}f_i(n_i) \rightarrow G= \sum_{\underline{n}}\prod^{M}_{i=1}f_i(n_i)
$$
### Distribuzione della lunghezza della coda

usando l'espressione ricorsiva per $p(\underline{n})$ otteniamo 
%% ho saltato i passaggi intermedi %%
$$
\begin{cases}
P(\underline{n}_{i0}) = \lambda_iS_i(n_i+1)P(\underline{n}) \\
\\
P(\underline{n}_{0j}) = \frac{1}{\lambda_jS_j(n_j)}\\
\\
P(\underline{n}_{ij}) = \frac{\lambda_iS_i(n_i+1)}{\lambda_jS_j(n_j)}P(\underline{n})
\end{cases}
$$

definiamo la distribuzione dei clienti alla stazione i
$$
p_i(k) = \sum_{\underline{n_{n_i = k}}}P(\underline{n})
$$
sapendo che $F(k)= \lambda S(k)f(k-1)$ per k>0 e F(0)=1

>[!info] Caso 1: Coda a singolo server  
> $$p(n)=p(0)F(n);n>0$$    la costante di normalizzazione $p(0) \neq 0$ se la coda è stabile: $\lambda S(k)<1; \forall k>k_{0}$

>[!info] Caso 2: Singolo server integrato in un sistema aperto 
>$$P_M(n)=\frac{1}{G_M}F_M(n);n>0$$
>    la costante di normalizzazione $G_{m} \neq 0$ se la coda è stabile $\lambda_M*S_m(k)<1$ 

> [!warning] Caso 3: Singolo server integrato in sistema chiuso
>  $$P_M(n)=\frac{g(N-m,M-1)}{G(N,M)}F_M(n)    ;0 \leq n \leq N$$ il **fattore di normalizzazione non è costante**


Otteniamo quindi i seguenti indici di performance 

- $X_i=\sum^{n}_{k=1}p_i(k)\frac{1}{S_i(k)}$ 
- $U_i=1-P_i(0)$ 
- $\overline{n}_i=\sum_kkp_i(k)$ 
- $\overline{w_i} = \frac{n_i}{X_i}$ 

### Il teorema BCMP
una rete di code ha una soluzione forma prodotto se soddisfa i seguenti criteri :
- La rete ha un numero **finito** di stazioni  
- I clienti appartengono a un numero **finito** di classi chiuse o aperte e possono scambiarle.
- I tassi di transizione sono definiti da una **DTMC** per ogni classe 
- Ogni stazione può essere disciplinata da:
	- FCFS con distribuzione dei tempi di servizi **negativa esponenziale** 
	- LCFS con una distribuzione **razionale a trasformata di laplace** dei tempi di servizio 
	- Processor Sharing con una distribuzione **razionale a trasformata di laplace** 
	- Infinite server con una distribuzione **razionale a trasformata di laplace**

- FCFS è la policy standard first come first server, associata comunemente a una distribuzione negativa esponenziale
- LCFS pr (preemptive resume) ultimo arrivato primo servito: semplice approssimazione di un server in cui avvengono interruzioni ad alta priorità. Quando un cliente si unisce a una coda non vuota, il servizio del cliente corrente viene interrotto, aggiunto a uno stack e ripreso più tardi.
- PS Process sharing discipline: praticamente è il limite di una distribuzione round robin con quanto a 0
- IS infinte server discipline: Il server è equivalente a una stazione di delay.

## Calcolare la costante di normalizzazione nei sistemi aperti

Sia:
- $N_i,i=1,...,M$ =>  il massimo numero di clienti osservati alla stazione i durante l'osservazione (0,T].

In caso di sistemi aperti $N_i$ può crescere all'infinito. Che significa che non c'é dipendenza tra gli $N_i$ perciò la costante di normalizzazione diventa.
$$
G=\sum_\underline{n}\prod^{M}_{i=1}f_i(n_i) = \prod^{M}_{i=1}\sum^{N_i}_{i=1}f_i(n_i) = \prod^{M}_{i=1}G_i
$$
con soluzione forma prodotto
$$
P(\underline{n}) = \frac{1}{G} \prod^{M}_{i=1}f_i(n_i)=\prod^{M}_{i=1}\frac{f_i(n_i)}{G_i} = \prod^{M}_{i=1}p_i(n_i) 
$$
## Computing normalization constant in closed systems 

L'indipendenza di $N_i$ non è applicabile nei sistemi chiusi, poichè non vi sono nuovi arrivi in questi sistemi, l'unica possibilità sono clienti che si spostano da una stazione all'altra. 

Le equazioni di bilanciamento assumono una forma più semplice  
$$
\sum^{M}_{i,j=1}P(\underline{n_{ij}})\frac{q_{ij}\delta(n_j)}{S_i(n_i+1)}=P(\underline{n})\sum^{M}_{i=1}\frac{\delta(n_i)}{S_i(n_i)}
$$

La definizione formale rimane la stessa. 
 $$P(\underline{n}) = \frac{1}{G}\prod^{M}_{i=1}f_i(n_i)$$  dove: 
$$
f_i(k)= \begin{cases}
1 \ \ \ k=0 \\
V_iS_i(k)f_i(k-1) \ \ k>0
\end{cases}
$$
e $G = \sum_\underline{n}\prod^{M}_{i=1}f_i(n_i)$ 

### Il metodo convolutivo
in un sistema chiuso $\underline{n}$ è fattibile se:
- $n_i \geq 0,i=1\dots M$  
- $\sum^{M}_{i=1}n_i=N$ 

La seconda condizione introduce dipendenza tra le stazioni del sistema

Siano:
- $S(n,m)=\{(n_1 \dots n_M | n_i \geq 0, i=1 \dots m; \sum^{m}_{i=1}n_i=n \}$ =>  lo spazio degli stati con m stazioni e n clienti 
-  $g(n,m)= \sum_{\underline{n} \in S(n,m)} \prod^{m}_{i=1}f_i(n_i)$ => funzione ausiliaria dove:
    - $g(N,M)=G$  

con un pò di calcoli si può mostrare che 
$$
g(n,m) = \sum^{n}_{k=0}f_m(k)g(n-k,m-1) 
$$
la definizione g(n,m) può essere ricorsiva introducendo i seguenti casi base:
- $g(0,m) = 1(m=0 \dots )$
- $g(n,0) = 0 (n=1 \dots).$

Che è una somma convolutiva che calcola efficacemente la distribuzione nel modello.

### Schema di calcolo per  G
Per far si che questo schema funzioni **dobbiamo prima calcolare tutte le**:
- $f_m(k)$ 
- $g(k,m-1)$ 

Ogni riga della ricorsione di g corrisponde a un preciso carico del sistema e ogni colonna a una specifica stazione . La ricorsione è operata prima sul livello di carico (n) e poi sui componenti della rete(m) iniziando dal bordo sinistro superiore e finendo in quello inferiore destro.

La complessità dell'algoritmo è :
- $N^2*M$  nel caso generale 
- $N*M$ Se tutte le stazioni sono load indipendent, caso più semplice. 
```
//Input -> M: int,N: int,V[i]: Array<double>, S[i](k): Array<Array<double>>, ST[i]: Array<SType>
//Output -> G(k): Array<double>

G[0] = 1.0;
for k in 1...N{
	G[k]= 0.0;
}
for i in 1...M{
	if(ST[i] == LI){
		d = V[i] * S[i][1];
		for k in 1...N{
			G[k] = G[k] + d*G[k-1];
		}
	}

	else{
		f[0] = 1.0
		for k in 1...N{
			f[k] = f[k-1]*V[i]*S[i][k];
		}
		for n in N...1{
			sum = G[n];
			for k in 1...n{
				sum += f[k] * G[n-k];
			}
		}
	}
}
```
### Calcolo delle statistiche di performance 
usando l'espressione esplicita di $P(\underline{n})$ abbiamo  $$p_m(k)= f_m(k)\frac{g(n-k,m-1)}{g(n,m)}$$
>[!note]  
>per il resto dello schema $p_m(k,n)$ verrà semplificato in $p_m(k)$ omettendone la dipendenza esplicità con la dimensione della popolazione.

Di seguito il calcolo di alcuni indici di performance 

- $X_m= \sum^{n}_{k=1}p_m(k)\frac{1}{S_m(k)} = V_m \frac{g(n-1,m)}{g(n,m)}$ 
- $U_m=1-p_m(0)=1- \frac{g(n,m-1)}{g(n,m)}$ 
Si noti che U e X possono essere estratti direttamente dalla tabella di ricorsione risparmiando calcoli.

- $\overline{n}_m = \sum^{n}_{k=1}kp_m(k)$ 
- $\overline{w}_m = \frac{\overline{n}_m}{X_m}$ 

Nel caso di load independent station si può applicare il seguente:
- $U_m= X_m S_m = V_m S_m \frac{g(n-1,m)}{g(n,m)}$ (standard formula)
- $\overline{n}_m(n)= U_m(n)[1+\overline{n}_m(n-1)]$ 
- $\overline{w}_m(n)= S_m[1+\overline{n}_m(n-1)]$ 

### Teorema dell'arrivo
$$\overline{w}(n)= S_m[1+\overline{n}_m(n-1)$$conosciuta anche come teorema dell'arrivo (o PASTA): "Se un server ha una distribuzione **markovniana** degli arrivi allora i clienti che arrivano vedono il sistema come se fossero osservatori esterni non coinvolti nell'operazione".

Nel caso di sistemi chiusi che hanno una soluzione forma prodotto (BCMP):
quando il sistema ha N clienti, i clienti che arrivano vedono la coda i-esima come osservatori esterni **che monitorano la coda in equilibrio quando n-1 clienti sono presenti** 
## Analisi del valor medio
Raggruppando tutte le espressioni ricorrenti
-  $\overline{w}_i(n) = S_i[1+\overline{n}_i(n-1)]$
- $U_i(n)=X_i(n)S_i$ 
- $\overline{n}_i(n)= U_i(n)[1+\overline{n}_i(n-1)]$ 

l'equazione mancante per $X_i$ può essere derivata usando la [[#Formula di little ⚠]] 
- $X_{ref}(n)= \frac{n}{\sum^{M}_{j=1}V_j \overline{w_j}(n)}$ (derivato dalla definizione di $Y_k(n)$)   
- $X_i(n)= V_i X_{ref}(n)$ 
### MVA per stazioni Load Indipendent 
```
Input -> M: int, N: int, V[i] : Array<double>, S[i]: Array<double>
Output -> X[i][k]: Array<Array<double>>, U[i][k]:Array<Array<double>>, n[i][k]:Array<Array<int>>, w[i][k] : Array<Array<double>>

for k in 1...N{
	for i in 1...M{
		w[i][k] = S[i]*(1+n[i][k-1]);
	}
	sum = 0;
	for i in 1...M{
		sum += V[i]*w[i][k];
	}
	Xref = k/sum;
	for i in 1...M{
		X[i][k]= V[i]*Xref;
		U[i][k]=S[i]*X[i][k];
		n[i][k]=U[i][k]*(1+n[i][k-1]);
	}
}

```

### Analisi del valor medio con stazioni di ritardo
nel caso di stazioni di ritardo è sempre $\overline{w}_i(n)= Z$ . L'algoritmo può essere modificato osservando che
- $\overline{w}_i(n)= \begin{cases}Z_i \ \ \ delay\ station \\ S_i[1+\overline{n}_i(n-1)] \ \ \ LI \  station \end{cases}$  
- $\overline{n}_i(n)= \begin{cases}Z_iX_i(n) \ \ \ Delay \ Station \\ U_i(n)[1+\overline{n}_i(n-1)] \ \ \  LI \end{cases}$ 
- $U_i(n)= \begin{cases}\frac{\overline{n}_i(n)}{n} \ \ \ DI \\ X_i(n)S_i \ \ \ LI \end{cases}$ 
### MVA for LI&D stations 
```
Input -> M: int, N: int, V[i] : Array<double>, S[i]: Array<double>, ST[i]: Array<StationType>,Z[i] : Array<double>
Output -> X[i][k]: Array<Array<double>>, U[i][k]:Array<Array<double>>, n[i][k]:Array<Array<int>>, w[i][k] : Array<Array<double>>

for k in 1...N{
	for i in 1...M{
		if(ST[i] == "D){w[i][k] = Z[i]}
		else{w[i][k] = S[i]*(1+n[i][k-1]);}
	}
	sum = 0;
	for i in 1...M{
		sum += V[i]*w[i][k];
	}
	Xref = k/sum;
	for i in 1...M{
		X[i][k]= V[i]*Xref;
		if(ST[i] == "D){
			n[i][k] = Z[i]*X[i][k];
			U[i][k] = n[i][k]/k;
		}
		else{
		U[i][k]=S[i]*X[i][k];
		n[i][k]=U[i][k]*(1+n[i][k-1]);
		}
	}
}

```

### Mean value analysis with  Load dependent stations

considerando:
- l'espressione per la distribuzione della lunghezza di coda: $$p_m(k,n)= f_m(k)\frac{g(n-k,m-1)}{g(n,m)}$$
- l'espressione esplicità della funzione di servizio: $$f_m(k)=V_mS_m(k)f_m(k-1)$$
- del throughput: $X_m(n)= V_m \frac{g(n-1,m)}{g(n,m)}$  

sostituendo nella distribuzione della lunghezza di coda si ottiene: $$p_m(k,n)= X_m(n)S_m(k)p_m(k-1,n-1)$$ %%ho omesso i passaggi intermedi%% 
 siccome l'espressione di $X_m$ è vera per ogni i possiamo usarla per tutti gli indici. La nuova espressione ricorsiva ci permette di ottenere:

- $\overline{w}_i(n) = \frac{\overline{n}_i}{X_i(n)} = \frac{\sum^{n}_{k=1}kp_i(k,n)}{X_i(n)} = \sum^{n}_{k=1}kS_i(k)p_i(k-1,n-1)$ ultimo passaggio con la distribuzione  
- $X_{ref}(n)= \frac{n}{\sum^{M}_{j=1}V_j \overline{w}_j(n)}$ 
- $X_i(n)= V_iX_{ref}(n)$ 
- $\overline{n}_i(n)=\overline{w}_i(n) * X_i(n)$ 
- $p_i(k,n)= X_i(n)S_i(k)p_i(k-1,n-1)$
- $p_i(0,n)= 1- \sum^{n}_{k=1}p_i(k,n)$ 
- $U_i(n)= 1-p_i(0,n)= \sum^{n}_{k=1}p_i(k,n)$ 

ad ogni passo la coda può quindi essere calcolata con $p_i(0,n)=1.0-U_i(n)$  
inizializzata a $p(0,0)=1.0$ . A questo punto l'integrazione delle nuove espressioni è semplice.
### MVA for LD stations 
**non si può usare se il collo di bottiglia è dipendente dal carico**
```
Input -> M: int, N: int, V[i] : Array<double>, S[i]: Array<double>
Output -> X[i][k]: Array<Array<double>>, U[i][k]:Array<Array<double>>, n[i][k]:Array<Array<int>>, w[i][k] : Array<Array<double>>, p[i][k][n]: Array<Matrix<2,double>>

cum = 0.0;wait=0.0;y=0.0
for i in 1...M{
	p[i](0,0) = 1.0;
	for j in 1...N{p[i](j,0) = 0.0;}
}

for k in 1...N{
	for i in 1...M{
		for j in 1...k{
			wait += j * S[i][j]*p[i](j-1,k-1);
			w[i][k]=wait;
		}
	}
	for i in 1...M{
		Y+= V[i]*w[i][k];
	}
	Xref= k/Y;
	for i in 1...M{
		X[i][k] = V[i]*Xref;
		for j in 1...k{
			p[i](j,k)=X[i][k]*S[i][j]*p[i](j-1,k-1);
			cum += p[i](j,k);
		}
		p[i](0,k) = 1.0-cum;
		u[i][k]=cum;
		n[i][k]=X[i][k]*w[i][k];
	}
}


```