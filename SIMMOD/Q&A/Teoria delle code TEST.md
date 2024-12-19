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
la coda M/M/1 assume tempi di inter-arrivo e di servizio markovniani, per cui assumendo tempi costanti e  inserendoli dentro alla soluzione dei processi di nascita e morte , otteniamo $\pi_{k}=\pi_{0}\rho^k$ e $\pi_{0}=1-\rho$ . A questo punto possiamo verificare le condizioni di ergodicità secondo $S_{1}=\sum_{k=0}^{\infty}\left( \frac{\lambda}{k} \right)^k<\infty$ e $S_{2}=\sum_{k=0}^{\infty} \frac{1}{\lambda}\left( \frac{\micro}{\lambda} \right)^{k}= \infty$  che sono soddisfatte solo se $\frac{\lambda}{\micro}<1$ . Per cui questo porta $\pi_{k}=\pi_{0}\rho^k$ e $\pi_{0}=1-\rho$. Da queste due soluzioni è possibile calcolare vari indici di performance, come il numero atteso di client $\frac{\rho}{1-\rho}$ e il secondo momento di questa misura $2\left( \frac{\rho}{1-\rho} \right)+\frac{\rho}{1-\rho}^2$ e la varianza. Usando la formula di little è possibile calcolare l'attesa media e anche la probabilità che la coda ecceda una certa soglia. 

4.
In una coda con arrivi scoraggiati invece otteniamo l'effetto della decrescita degli arrivi man mano che la coda aumenta. La soluzione diventa quindi $\pi_{0}=e^{-\lambda/\micro}$  e $\pi_{k}=\frac{\left( \frac{\lambda}{\micro}^k \right)}{k!}e^{-\lambda/\micro}$ . L'ergodicità è soddisfatta per $\frac{\lambda}{\micro}<1$ . Anche qui è possibile stimare diversi indici di performance come l'utilizzo 

11. Spiega come si calcolano i tempi di soggiorno in una coda M/M/1

Per spiegare come si calcolano i tempi di soggiorno dobbiamo partire dalla pasta property, che ci dice , grazie alla proprietà di assenza di memoria, che un cliente che arriva vede il sistema come se fosse arrivato in un momento casuale, non connesso cioè allo stato della catena. Sia W la variabile che rappresenta il tempo di soggiorno in questa coda, sia $W_{n}[a]=\sigma+\omega_{1}+\omega_{2}+\omega_{3}\dots+\omega_{n-1}+R$ la variabile che rappresenta il tempo d'attesa dell'n-esimo cliente dati n clienti in coda , R  il tempo di servizio rimanente per il cliente che era in servizio  ,$\sigma$ il tempo di servizio del cliente appena entrato. 
Siccome tutti i clienti sono statisticamente equivalenti allora $W_{n}^{[a]}$ è la somma di n+1 variabili aleatorie tutte negative esponenziali, quindi applicando la trasformata di laplace e eseguendo vari passaggi otteniamo che $F_{W}(t)=Pr\{X\leq t\}=1-e^{-ut}$ 


5.
In un sistema M/M/inf il rateo di partenze cresce linearmente con l'arrivo dei clienti, ed è quindi un sistema duale a quello degli arrivi scoraggiati. In questo sistema le soluzioni sono $\pi_{0}=e^{-\lambda/\micro}$ e $\pi_{k}= \frac{(\lambda/\micro)^k}{k!}e^{-\lambda/\micro}$ l'ergodicità è soddisfatta per $\frac{\lambda}{\micro}<1$ . I risultati sono i medesimi degli arrivi scoraggiati, per cui $E[n]=\frac{\lambda}{\micro}$ il tempo di soggiorno invece dipende solo dal tempo di servizio $E[w]=\frac{1}{\micro}$ 