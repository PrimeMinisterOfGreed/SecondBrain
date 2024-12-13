1. Descrivi il processo di nascita e morte e la sua rilevanza nella teoria delle code. Un processo di nascita e morte è un processo stocastico che modella l'evoluzione di un sistema in cui gli unici cambiamenti possibili sono l'arrivo di nuovi elementi ("nascite") o la partenza di elementi esistenti ("morti"). Nella teoria delle code, i processi di nascita e morte sono ampiamente utilizzati per descrivere l'evoluzione della lunghezza di una coda, dove le "nascite" corrispondono agli arrivi dei clienti e le "morti" corrispondono ai completimenti dei servizi.

2. Quali sono le assunzioni fondamentali del modello di coda M/M/1? Il modello M/M/1 assume che gli arrivi dei clienti seguano un processo di Poisson, che i tempi di servizio siano distribuiti in modo esponenziale, che ci sia un solo server e che la disciplina di servizio sia First-Come, First-Served (FCFS).

3. Come si calcola l'utilizzo di un sistema di accodamento e cosa rappresenta? L'utilizzo, denotato come ρ, rappresenta la frazione di tempo in cui il server è occupato. In un sistema M/M/1, l'utilizzo è dato dal rapporto tra il tasso di arrivo λ e il tasso di servizio μ: ρ = λ/μ.

4. Spiega il concetto di arrivi scoraggiati e come influenza il comportamento di un sistema di accodamento. Gli arrivi scoraggiati si verificano quando il tasso di arrivo dei clienti diminuisce all'aumentare della lunghezza della coda. Questo comportamento modella situazioni in cui i clienti potenziali sono scoraggiati dall'attesa eccessiva e decidono di non unirsi alla coda.

5. Quali sono le principali caratteristiche di un sistema di accodamento M/M/∞ e come si differenzia da altri modelli, come M/M/1? Il modello M/M/∞ rappresenta un sistema con un numero infinito di server. Questo significa che ogni cliente che arriva viene servito immediatamente, senza dover aspettare in coda. A differenza del modello M/M/1, dove l'utilizzo è un fattore limitante, in un sistema M/M/∞ l'utilizzo è sempre minore di 1, indipendentemente dal tasso di arrivo.

6. Descrivi il modello di coda M/M/m e i suoi parametri. Il modello M/M/m rappresenta un sistema con m server identici che lavorano in parallelo. I clienti si accodano solo se tutti i server sono occupati. Come in M/M/1, gli arrivi seguono un processo di Poisson e i tempi di servizio sono distribuiti in modo esponenziale.

7. Quali sono le implicazioni di un buffer finito in un sistema di accodamento? Illustra il modello M/M/1/B. Un buffer finito limita il numero di clienti che possono essere in coda. Nel modello M/M/1/B, se un cliente arriva quando la coda è piena (cioè contiene B clienti), viene respinto e abbandona il sistema.

8. Cosa distingue un sistema di accodamento a popolazione finita da un sistema a popolazione infinita? In un sistema a popolazione finita, il numero di clienti che possono richiedere un servizio è limitato. Nel modello M/M/1//N, ad esempio, c'è un numero fisso N di clienti che circolano tra la coda e il server. Man mano che i clienti entrano nella coda, il tasso di arrivo diminuisce, riflettendo la popolazione finita.

9. Spiega il metodo degli stadi e come può essere applicato per analizzare sistemi di accodamento non markoviani. Il metodo degli stadi consente di rappresentare distribuzioni di tempi di servizio non esponenziali, come la distribuzione Erlang, scomponendole in una serie di stadi esponenziali. Questo permette di utilizzare l'analisi basata su catene di Markov per sistemi con distribuzioni di servizio più generali.

10. Quali sono i principali vantaggi e svantaggi dell'utilizzo della trasformata Z nell'analisi di sistemi di accodamento? La trasformata Z è uno strumento matematico che può semplificare la derivazione di indici di performance come la lunghezza media della coda. Tuttavia, la sua applicazione può richiedere la risoluzione di equazioni algebriche complesse e l'inversione della trasformata per ottenere la distribuzione di probabilità desiderata.


1.
Il processo di nascita e morte a tempo continuo è la base per trovare gli indici di performance stazionari delle stazioni considerate, tipicamente si inserisce all'interno della soluzione il modello proposto , si verificano le condizioni di ergodicità e si calcolano i vari indici di performance 

2.
la coda M/M/1 assume tempi di inter-arrivo e di servizio markovniani, per cui assumendo tempi costanti e  inserendoli dentro alla soluzione dei processi di nascita e morte , otteniamo $\pi_{k}=\pi_{0}\rho^k$ e $\pi_{0}=1-\rho$ . A questo punto possiamo verificare le condizioni di ergodicità secondo $S_{1}=$