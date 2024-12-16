
## Monte carlo simulation
è una tecnica computerizzata che permette di generare valori con distribuzioni affidabili utili alla simulazione 

## Processo di poisson  (negative exponential)
gli eventi sono rari è occorrono in maniera completamente aleatoria. Assumendo che p sia un evento che capita in un intervallo di tempo  $\Delta$ la frequenza è $\lambda \Delta+ o(\Delta)$ 
dividendo l'intervallo  T in m parti di lunghezza $\Delta$ e contando gli eventi otteniamo
![[Pasted image 20231101180122.png]]
$$P(k,T|\Delta) = \binom{m}{k} (\lambda \Delta)^k(1-\lambda \Delta) ^{(m-k)} + o(\Delta)$$ 
il limite di questa probabilità per  $m \rightarrow \infty$ 
$$P(k,T) = \frac{(\lambda T)^k}{k!}e^{-\lambda T}$$ dove:
- $\tau$ distanza tra arrivi successivi 
- 
$P(\tau > T) = P(0,T)= \frac{(\lambda T)^0}{0!}e^{-\lambda T} = e^{-\lambda T}$  per cui $P(\tau < t) = 1- e^{-\lambda T}$ 

- CDF = $F_X(x)=Pr[X \leq x] = 1-e^{-\lambda x}$ 
- PDF= $f_X(x)=\frac{dF_X(x)}{dx}= \lambda e^{-\lambda x}$ 
- $E[X] = \sigma = \frac{1}{\lambda}$ 
- $VAR[X]= \sigma^2 = \frac{1}{\lambda^2}$
- $CV[X]=\frac{Std[X]}{E[X]}= \frac{\sqrt{VAR[X]}}{E[X]}= 1$ 
## Generazione di numeri casuali
un generatore di numeri casuali **ideale** produce sequenze $0<u<1$ tali che queste siano equamente distribuite 

un buon generatore di numeri casuale produce sequenze statisticamente indistinguibili da un generatore di numeri casuale ideale

### Modello concettuale  
- scegli un intero positivo molto grande m, questo definisce l'insieme  $\chi_m =1...m-1$.
- riempi un urna con gli elementi di $\chi_m$ , ogni volta che abbiamo bisogno di un numero u estrailo e applica $u=x/m$ 

Ogni estrazione simula un campione da una variabile aleatoria Uniforme(0,1) , è importante che m sia grande così che i valori siano densamente distribuiti nell'intervallo.

### Algoritmo di Lehmer 
il generatore congruente lineare prende due parametri : 
- modulo => m (large prime) 
- moltiplicatore =>  a ($I \in \chi_m)$ 
la sequenza di interi $x_0,x_1,...$ è definita dall'equazione iterativa 
$x_{i+1}=g(x_i)$  dove:
- $g(x)=ax \mod{m}$ 
- $x_0 \in \chi_m$ è chiamato seme.

a causa dell'operatore modulo  $0 \leq g(x) < m$ . 
0 non occorre siccome $g(0)=0$ 
m , poichè è primo, $g(x) \neq 0$ se $x \in \chi_m$ . 
Se $x_0 \in \chi_m$ allora $x_i \in \chi_m$  per tutti gli $i \geq 0$.

Non c'é nulla di casuale in questo generatore, per questo motivo è chiamato pseudo casuale 

## Periodo pieno  
la scelta di m è caratterizzata in parte dalle caratteristiche del sistema, a seconda che sia a 64/32/16 bit . Per cui questa scelta va fatta molto accuratamente. 
Dato un modulo m , un **periodo pieno** contiene tutti i valori nell'intervallo (1,m-1) prima di ripetersi. 

## Test per generatori casuali

### statistica del chi quadro 
Sia:
- x una variabile aleatoria, assumiamo che prenda valori in $\chi=(0,m)$

Supponiamo di dividere il suo insieme di valori possibili in k intervalli adiacenti 
$(a_{0},a_{1}],(a_{1},a_{2}]\dots(a_{k-1},a_{k})$ per formare un nuova variabile aleatoria discreta che assume valori nell'insieme $Y_{k}=\{0,1,\dots,k-1\}$ 

Basandosi su un campione di osservazioni n molto grande e indipendente di y, per ogni valore $y_{j}$ possibile sia:
- $N_{j}$ => il numero di volte che $y_{j}$ occorre 
- $\eta_{j} = np_{j}$ => il numero atteso di volte che occorra $y_{j}$ , dove :
    - $p_{j}$ => probabilità di osservarla in $(a_{j-1},a_{k}]$ 

Allora la risultante quantità **non negativa** $$V=\frac{\sum^{k}_{j=1}(N_{j}-\eta_{j})^2}{\eta_{j}}$$
è conosciuta anche come **statistica del chi quadro*** 

### Test del chi quadro 
Se il campione di variabili aleatorie x, rappresentato dal campione $X=\{x_{1},x_{2},\dots,x_{n}\}$ è davvero un campione identicamente e indipendentemente distribuito della distribuzione che volgiamo ottenere e se $\frac{n}{k}$ è sufficientemente grande (>10).

Allora la statistica V è approssimativamente una variabile aleatoria $\chi^2$ con k-1 gradi di libertà 

In queste condizioni siccome la distribuzione del $\chi^2$ non è simmetrica, sia:
- $v_{1}^*=\chi^2\left( k-1,\frac{\alpha}{2} \right)$ => il percentile definito come $Pr\{\chi^2(k-1)\leq v_{1}^*\}=\frac{\alpha}{2}$
-  $v_{2}^*=\chi^2\left( k-1,1-\frac{\alpha}{2} \right)$ => il percentile definito come $Pr\{\chi^2(k-1)\leq v_{2}^*\}=\frac{\alpha}{2}$

allora la $Pr\{v_{1}^*<V\leq v_{2}^*\}=1-\alpha$ cioè la statistica del chi quadro apparterrà all'intervallo $(v_{1}^*,v_{2}^*)$ con livello di confidenza $1-\alpha$ 

#### interpretazione del test del chi quadro 
con l'aiuto della tabella dei percentili del test del chi quadro è possibile accettare l'ipotesi del test basandosi su questi criteri: 
- Un valore V è considerato **accettabile** con 95% confidenza se cade tra le colonne .025 e .975 della tabella 
- **rifiutato** prima di 0.005 o dopo .995
- **dubbioso** tra .005 e .01 o tra .99 e .995 
- **quasi-dubbioso** tra 0.1 e 0.25 o .975 e .99 

un test di questo tipo è chiamato **test delle due code** 

### Test di uniformità 
Dividere l'intervallo (0,1) in k sottointervalli di uguale lunghezza generando $U_{1},U_{2},\dots,U_{n}$ , si raccomanda di scegliere $k\geq 100$ e $\frac{n}{k}\geq 5$.

Sia:
- $N_{j}$ => numero di $U_{i}$ che occorrono nel j-esimo sotto intervallo. 

Allora:  $$V=\frac{k}{n}*\sum^{k}_{j=1}\left( N_{j}-\frac{n}{k}^2 \right)$$
è approssimativamente una variabile distribuita come un $\chi^2(k-1)$

### Test seriale 
versione 2-d del test di uniformità per accertare l'indipendenza tra osservazioni successive

dividere l'intervallo (0.,1) in k sotto intervalli di lunghezza uguale 
generare $U_{1},U_{2},\dots,U_{2n}$ , se le $U_{i}$ sono davvero IID allora le coppie non sovrapposte $(U_{1},U_{2}),(U_{3},U_{4})\dots(U_{2n-1}U_{2n})$ sono vettori di IID uniformemente distribuiti nel quadrato $(0,1)^2$ 

- Contare il numero di risultati che cadono in ogni sotto quadrato ($N_{ij}$ => numero di paia che cadono nel (i,j) sotto quadrato)

allora $$V=\frac{K^2}{n}\sum^{k}_{i=1}\sum^{k}_{j=1}\left( N_{ij}-\frac{n}{k^2} \right)^2$$ è approssimativamente una $\chi^2(k-1)$ 
**questo test è generalizzabile per più dimensioni** 

### Test del gap
il test del gap controlla l'aleatorietà del generatore con una visione non locale.

Sia:
- $\alpha,\beta \in(0,1)$  con $\alpha<\beta$
- $q=\beta-\alpha$ => probabilità che un numero U sia nell'intervallo $(\alpha,\beta)$

Generare $U_{1},U_{2},\dots,U_{n}$ -> trasformare la sequenza $\{U_{i}\}$ in $\{I_{i}\}$ mediante 
$$
I_{i}= \begin{cases}
1 &&if&U_{i}\in(\alpha,\beta)\\ \\
0
\end{cases}
$$

Identificare sotto sequenze successive $I_{j},I_{j+1},\dots,I_{j+r},I_{j+r+1}$ così che il primo e l'ultimo elemento di questa sequenza siano 1 e gli altri 0. Il gap diventa quindi un **gap di lunghezza r**.

Sia:
- N => numero totale di gap generati durante l'applicazione del test 
- $\eta_{j} = Nq(1-q)^j$ => numero atteso di gap di lunghezza j che dovrebbero apparire nella sequenza 
- $N_{j}$=> numero di gap di lunghezza j osservati nella sequenza 

$$V=\sum^{k}_{i=0}\left( \frac{(N_{j}-\eta_{j})^2}{\eta_{j}} \right)$$

eseguire un test del chi quadro usando lunghezze differenti di gap come categorie e probabilità in questo modo $p_{r}=q(1-q)^r$

la dimensione di un gap potrebbe crescere all'infinito, così consolidiamo il gap, scegliendo un k arbitrario che faccia da tetto e contando insieme tutti i gap di lunghezza (k-1) o più grandi. La probabilità di questo evento consolidato è 

$$Pr\{r\geq k-1\}=(1-q)^{k-1}$$ siccome i gap hanno distribuzione geometrica con parametro (1-q), la lunghezza del gap attesa è 
$$
E[r]=\frac{1-q}{q}
 $$
valori bassi di q portano a gap di grandezza maggiore.

La scelta di k e q hanno un grande impatto sulla lunghezza della sequenza di valori aleatori che vogliamo usare per il test. Più grande il valore di k meno sarà locale l'aleatorietà del test. Valori grandi di k fanno si che la probabilità di avere gap di lunghezza maggiore di k-2 più piccola. Valori piccoli di q rendono il test più concentrato. La lunghezza della sequenza di numeri aleatori n può essere stimata in questo modo: 
$$n\geq E[r]  \frac{m}{Pr\{r\geq k-1\}}=\frac{m}{q(1-q)^{k-2}}$$

dove m è il numero minimo di gap con lunghezza $\geq 10$ attesi. Di solito si sceglie $m\geq 10$
## Probabilità base 
Probabilità empirica => dato un evento $A$ si esegua un esperimento per vedere quante volte si ripete:
- frequenza relativa : $n_a/n$ , converge a $Pr(A)=\lim_{n \rightarrow \infty}\frac{n_a}{n}$ 

Probabilità assiomatica: costruiamo matematicamente lo spazio dei campioni 

## Variabili aleatorie discrete 
una variabile aleatoria X è discreta se l'insieme dei suoi possibili valori  $\chi$ è finito. 
è unicamente caratterizzata dalla sua distribuzione di probabilità che è una funzione reale determinata per ogni valore in $\chi$  

PDF: $f(x)=Pr(X=x)$ 
per definizione : $\sum_xf(x)=1$ 

### Distribuzione Cumulata 
la distribuzione cumulata di una variabile aleatoria X è specificata come 
$F(x)= Pr(X \leq x)= \sum_{t \leq x} f(t)$ 

Si può generare una CDF da una PDF tramite ricorsione
$\chi=\{x|x=a,a+1,...b\}$ --> $F(a)=f(a) \ \ \ \ F(x)=F(x-1)+f(x)$ 

Viceversa è possibile tramite differenziazione:
$f(a)=F(a) \ \ \ \ \ f(x)=F(x)-F(x-1)$ 

una cdf è strettamente monotona crescente 
- se $x_1<x_2$ allora $F(x_1)<F(x_2)$ 
- CDF values are $\in (0.0,1.0)$ , Monotonicity of F(x) is the basis to generate discrete RVs

## Variabili aleatorie continue
Una variabile aleatoria X è continua se i suoi valori possibili $\chi$ sono un insieme continuo definito da :
 - PDF:  $\int^{b}_{a}f(x)dx= Pr(a \leq X \leq b)$ 

per definizione  $\int_\chi f(x)dx =1$ 


### CDF 
- CDF => $F(x)=Pr(X \leq x) = \int_{t \leq x} f(t)dt$ 
strettamente monotona crescente entro i valori (0.0,1.0)

la CDF si può ottenere dalla PDF usando l'integrazione 
la PDF si può ottenere dalla CDF tramite derivazione $f(x)= \frac{d}{dx}F(x)$ 

## Sommario delle distribuzioni 
### Discrete 

|Generator|Range (x)| Mean| Variance|
|---|----|---|---|
|Bernoulli (p)| x=0,1| p| p(1-p)|
|Binomial (n,p)|x=0,...,n|np|np(1-p)|
|Equilikely(a,b)|x=a,...,b|(a+b)/2|($(b-a+1)^2$-1)/12|
|Geometric(p)| $x=0,...$ | p/(1-p)| $np/(1-p)^2$
|Pascal(n,p)| $x=0,...$ |np/(1-p)| $np/(1-p)^2$ 
|Poisson(m)| $x=0,...$ |m|m


### Continuos 

|Generator|Range (x)| Mean| Variance|
|---|----|---|---|
|Uniform(a,b)| a < x < b| (a+b)/2| $(b-a)^2/12$ 
|Exponential(m)| x>0 | m| $m^2$
|Erlang (n,b)| x>0| nb| $nb^2$ 
|Normal(m,s)| $\forall x$ | m| $s^2$ 
|Lognormal(a,b)|x>0|$\exp(a+\frac{1}{2}b^2)$| $(\exp(b^2) -1) \exp(2a+b^2)$ 
|Chisquare(n)|x>0|n|2n
|Student(n)| $\forall x$ |0|n/(n-2)

## Generazione di distribuzioni aleatorie 
La generazione di variabili aleatorie non uniformi può essere fatta nei seguenti modi :
- Trasformazione inversa 
- Accettazione rigetto
- Composizione 

la trasformazione inversa si basa sulla conoscenza esplicita della CDF della distribuzione voluta . 

Acceptance rejection e composition assumono che le funzioni di distribuzione o la densità(nel caso continuo) siano conosciute.

## Generare una uniforme 

possiamo generare una uniforme(a,b) da una uniforme(0,1) semplicemente usando gli endpoint dell'intervallo a,b. Cosa possibile semplicemente scalando e shiftando usando a:
- Coefficiente di scaling $\alpha=(b-a)$ 
- Coefficiente di shifting $\beta=a$ . 
```C
double Uniform(double a, double b){return (a+(b-a)*Random());}
```

### Funzione di distribuzione inversa 
La funzione di distribuzione inversa (idf) di una variabile aleatoria X è una funzione definita in questo modo $F^{-1}:(0,1) \rightarrow \chi$ per ogni $u \in (0,1)$ come $F^{-1}(u)=x$ 
dove:
- $x \in \chi$ è l'unico valore possibile per $F(x)=u$ 

Esiste una corrispondenza ben precisa tra i valori possibili $x \in \chi$ e i valori della CDF $u=F(x) \in (0,1)$ 

segue una lista di distribuzioni inverse con media u e distribuzione inversa x.
>[!important] Uniform(a,b)
>$$u= F(x)= \frac{x-a}{b-a} ;\forall a<x<b$$ 
$$x= F^{-1}(u)=a+(b-a)u;  0  < u < 1$$ 


>[!important] Exponential($\eta$) 
>$$u = F(x)= 1-\exp\ \left( -\frac{x}{\eta} \right) ;x>0$$
>$$x= F^{-1}(u)= - \eta \ln(1-u);0<u<1$$

>[!important] Pareto($L,\alpha$)
$$u=F(x)=1-\left( \frac{L}{x} \right)^{\alpha};x \geq L$$


>[!important] Quadratica
>se X è una variabile aleatoria continua con valori $0<x<b$ 
>- PDF $f(x)=\frac{2x}{b^2}$ 
>- CDF  $u = F(x)=\left( \frac{x}{b} \right)^{2}$    
>$$x= F^{-1}(u)=b\sqrt{ u };0<u<1$$

## Metodo di composizione 
di solito usato per valori aleatorie la cui IDF non è facilmente calcolabile o è costosa. 
La distribuzione è la somma pesata di distribuzioni che sono più facili da calcolare .

Algoritmo per generare una distribuzione composita$f_{x}(X)=\sum^{n}_{i=1}\alpha_{i}g_{i}(x)$ 
```python
# Initialization
A = []
alpha = [] 
A[0] = alpha[0]
for i in range(1,n):
    A[i] = A[i-1]+alpha[i]


```
