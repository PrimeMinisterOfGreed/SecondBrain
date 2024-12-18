1. **Definire la proprietà di Markov**. Perché questa proprietà è fondamentale per l'analisi delle catene di Markov?

- La proprietà di Markov afferma che lo stato futuro di un processo stocastico dipende **solo** dallo stato presente e non dalla storia passata del processo.
- Questa proprietà semplifica notevolmente l'analisi, in quanto permette di studiare il comportamento del sistema **senza dover tenere traccia di tutta la sua storia**.

2. **Spiegare la differenza tra una catena di Markov a tempo discreto (DTMC) e una catena di Markov a tempo continuo (CTMC)**. Fornire esempi di sistemi che possono essere modellati con ciascuna di queste catene.

- In una **DTMC**, le transizioni di stato avvengono a istanti di tempo discreti. Esempi: un gioco d'azzardo in cui un giocatore effettua puntate a turni, oppure il clima in una città, analizzato giorno per giorno.
- In una **CTMC**, le transizioni di stato possono avvenire in **qualsiasi istante di tempo**. Esempi: il numero di clienti in un sistema di code, oppure il livello di scorte in un magazzino.

3. **Definire i concetti di stato "transitorio", "ricorrente" e "assorbente" in una catena di Markov**. Qual è l'importanza di classificare gli stati di una catena?

- Uno stato **transitorio** è uno stato che può essere visitato solo un numero finito di volte.
- Uno stato **ricorrente** è uno stato che può essere visitato un numero infinito di volte.
- Uno stato **assorbente** è uno stato che, una volta raggiunto, non può più essere lasciato.
- La classificazione degli stati è importante per comprendere il comportamento a lungo termine di una catena di Markov.

4. **Descrivere il metodo di calcolo della distribuzione stazionaria (o a regime) di una DTMC**. Quali sono le condizioni necessarie per l'esistenza di una distribuzione stazionaria?

- La distribuzione stazionaria di una DTMC rappresenta la probabilità di trovare la catena in ciascuno dei suoi stati a **lungo termine**.
- Per calcolare la distribuzione stazionaria, si risolve un sistema di equazioni lineari basato sulla matrice di transizione della catena.
- Le condizioni necessarie per l'esistenza di una distribuzione stazionaria sono:
- La catena deve essere **irriducibile**, ovvero ogni stato deve essere raggiungibile da qualsiasi altro stato.
- La catena deve essere **aperiodica**, ovvero non deve esistere un periodo fisso per le transizioni tra gli stati.
- Tutti gli stati devono essere **ricorrenti positivi**, ovvero il tempo medio di ritorno in uno stato deve essere finito.

5. **Spiegare come la Trasformata Z può essere utilizzata per l'analisi delle DTMC**. Quali sono i vantaggi di utilizzare questo strumento?

- La Trasformata Z è una tecnica matematica che permette di trasformare una sequenza di numeri in una funzione complessa.
- Nel contesto delle DTMC, la Trasformata Z può essere utilizzata per **semplificare il calcolo della distribuzione di probabilità** degli stati del sistema a un passo n.
- Invece di iterare la moltiplicazione della matrice di transizione per n volte, è possibile utilizzare la Trasformata Z per ottenere una soluzione in forma chiusa.

6. **Discutere l'utilizzo delle equazioni di Chapman-Kolmogorov per l'analisi delle CTMC**. Qual è il significato di queste equazioni?

- Le equazioni di Chapman-Kolmogorov esprimono la probabilità di transizione tra due stati di una CTMC **in funzione delle probabilità di transizione** tra stati intermedi.
- Queste equazioni sono fondamentali per l'analisi delle CTMC, in quanto permettono di calcolare la probabilità di transizione tra due stati **per qualsiasi intervallo di tempo**.

7. **Descrivere il processo di "pura nascita" in una CTMC**. Come si calcola la distribuzione di probabilità degli stati del sistema in questo caso?

- Un processo di "pura nascita" è una CTMC in cui sono possibili solo transizioni verso stati con un **numero maggiore di elementi**, ad esempio, arrivi in un sistema di code.
- Si assume che non ci siano "morti", ovvero transizioni verso stati con un numero minore di elementi.
- La distribuzione di probabilità degli stati del sistema può essere calcolata risolvendo un sistema di equazioni differenziali.

8. **Spiegare il concetto di "tempo di soggiorno" in una CTMC**. Perché il tempo di soggiorno in uno stato di una CTMC ha una distribuzione esponenziale?

- Il **tempo di soggiorno** in uno stato di una CTMC rappresenta l'intervallo di tempo che il sistema trascorre in quello stato prima di effettuare una transizione.
- A causa della **proprietà di assenza di memoria** delle CTMC, il tempo di soggiorno in uno stato ha una **distribuzione esponenziale**.
- Questo significa che la probabilità di lasciare uno stato **non dipende** da quanto tempo il sistema si trova già in quello stato.

9. **Discutere come si calcola la distribuzione stazionaria (o a regime) di una CTMC**. Quali sono le analogie e le differenze rispetto al calcolo della distribuzione stazionaria di una DTMC?

- La distribuzione stazionaria di una CTMC, come per una DTMC, rappresenta la probabilità di trovare la catena in ciascuno dei suoi stati a lungo termine.
- Per calcolare la distribuzione stazionaria di una CTMC, si risolve un sistema di equazioni lineari basato sulla **matrice del generatore infinitesimale** della catena (matrice Q).
- Le condizioni necessarie per l'esistenza di una distribuzione stazionaria sono analoghe a quelle per le DTMC: irriducibilità, aperiodicità e ricorrenza positiva degli stati.


1.
la proprietà di markov ci dice che lo stato futuro del processo stocastico non dipende dal passato ma solo dal suo stato attuale, cosa dimostrabile tramite la fattorizzazione delle probabilità congiunte del processo stocastico. è importante perchè permette di conoscere il comportamento del processo senza conoscerne tutta la storia.   Per la proprietà di markov la funzione di transizione diventa $p_{ij}^{(m)}=\sum_{k}p_{ik}^{(m-1)}p_{kj}$ 

2.
In una DTMC l'indice di tempo è discreto, questo significa che la transizione da uno stato all'altro si può verificare solo in un determinato momento . Invece in una CTMC l'indice di tempo è un insieme continuo, pertanto la transizione può avvenire in qualunque momento della giornata.

3.
Uno stato transitorio è uno stato che può essere visitato solo un numero finito di volte, uno stato ricorrente è uno stato che può essere visitato un numero infinito di volte, uno stato assorbente è uno stato che una volta visitato non si può più lasciare. La classificazione degli stati è importante per comprendere bene il comportamento del sistema a regime

4.
per il calcolo della distribuzione stazionaria è necessario che tutti gli stati siano aperiodici , cioè che non abbiano un periodo fisso, ricorrenti positivi, cioè che il loro tempo medio di visita sia finito, la catena deve essere irriducibile, cioè non ci devono essere sottoinsieme di stati assorbenti e tutti gli stati devono poter raggiungere in un numero finito di passi gli altri stati, la catena deve quindi essere ergodica. Se lo è allora sappiamo che per definizione le probabilità stazionare al limite di n infinito esistono e sono indipendenti dallo stato iniziale, a questo punto per una DTMC omogenea possiamo calcolare la soluzione semplicemente sapendo la distribuzione iniziale $\pi=\pi^{(0)}P^\infty$, oppure conoscendo il vettore nello stato precedente calcolandolo al successivo, con la condizione $\sum_{i}\pi_{i}=1$.

5.
La trasformata Z semplifica il carico computazionale, trasformando la soluzione in una funzione complessa, concedendoci di calcolare la soluzione a partire dalla moltiplicazione con 3 kernel matriciali e poi antitrasformare per ottenere la forma chiusa.

11. Spiegare che cos'é una DTMC non omogenea e perchè ci interessa conoscere le equazioni di bilanciamento

Le equazioni di bilanciamento ci interessano perchè tramite loro si può spesso e volentieri calcolare la soluzione della DTMC. In una DTMC le probabilità di transizione non sono omogenee nel tempo e quindi non possiamo pensare che in N passi queste siano sempre le medesime, per altro la soluzione a regime di tali catene dipende dallo stato iniziale. Usando la definizione di probabilità condizionale possiamo calcolare la probabilità di transizione $p_{ij}(m,n)=\sum_{k}p_{ik}(m,q)p_{kj}(q,n)$ , in altre la probabilità dipende da uno stato intermedio q, da cui per forza la catena deve essere passata per arrivare allo stato m. per le omogenee ne è disponibile una forma semplificata. Questa volta la matrice di transizione è una funzione del tempo definiamo $H(m,n)=[p_{ij}(m,n)]$ e $H(n,n+1)=P(n)$ , da cui otteniamo l'equazione di chapman kolmogrov $H(m,n)=H(m,q)H(q,n)$ , la cui soluzione è $\pi^{n+1}=\pi^{(0)}H(0,n+1)$. L'equazione matriciale per la probabilità asintotiche degli stati prevede la risoluzione del sistema $\pi=\pi*P$ il cui j-esimo componente è $\pi_{j}=\sum_{i}p_{ij}\pi_{j}$ che si può anche scrivere come $(1-p_{jj})=\sum_{i\neq j}\pi_{i}p_{ij}$ che descrive l'equilibrio tra flussi uscenti e entranti, definita anche come equazione di bilanciamento globale, nel dettaglio per ogni stato vale $\pi_{i}p_{ij}=\pi_{j}p_{ji}$.

12. Spiegare cosa è una CTMC , come si definisce la sua probabilità di transizione
