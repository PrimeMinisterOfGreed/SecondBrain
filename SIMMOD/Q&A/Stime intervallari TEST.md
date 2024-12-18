
1. Descrivi il concetto di stimatore puntuale e stima intervallare. Cosa li differenzia e perché la stima intervallare è spesso preferita?

2. Cos'è la disuguaglianza di Chebychev e come si applica alle stime intervallari? Cosa ci dice sulla proporzione di punti del campione che si trovano entro un certo intervallo dalla media campionaria?

3. Spiega il concetto di parametro di confidenza (1-α). Cosa rappresenta e come influenza l'ampiezza dell'intervallo di confidenza?

4. Dato un campione di grandi dimensioni, come si può utilizzare la distribuzione t di Student per costruire un intervallo di confidenza per la media della popolazione? Quali sono le ipotesi necessarie per l'applicazione di questo metodo?


1 
Uno stimatore puntuale è una stima polarizzata di un certo parametro, un buono stimatore puntuale ha distribuzione centrata sul parametro teorico, la sua differenza rispetto al parametro teorico è la minore possibile e la distribuzione e le informazioni sullo stimatore possono essere ottenuti dai valori osservati, in particolare dalla dimensione del campione, la polarizzazione di uno stimatore è la sua differenza rispetto al valore reale del parametro che vogliamo stimare. La stima intervallare è spesso preferita perchè ci fornisce un intervallo di valori entro cui il valore vero del parametro che vogliamo stimare è contenuto con una certa sicurezza (data dal parametro di fiducia $\alpha$) e precisione del risultato. Inoltre la stima intervallare tiene conto della variabilità del campione fornendo anche una misura dell'incertezza relativa alla stima che stiamo conducendo.

2 
La diseguaglianza di chebichev è :

$q_{k}\geq 1-\frac{\left( \frac{p-1}{p} \right)}{k^2}\geq 1-\frac{1}{k^2}$ dove:
qk è la proporzione degli elementi che rientrano nell'intervallo circoscritto da k deviazioni standard dalla media, mentre k è il numero di deviazioni standard rispetto alla media , per k =2 è molto conservativo e dice che almeno il 95% dei punti rientra nell'intervallo += ks mentre per k = 3 otteniamo che il 95% dei punti è entro questo intervallo. Inoltre questa stima è indipendente dalla distribuzione del parametro che stiamo stimando. La disuguaglianza ci dice anche che maggiore è la sicurezza che vogliamo maggiore sarà l'ampiezza dell'intervallo, ma anche più campioni si raccolgono più stretto quest'ultimo sarà.

3 
l'intervallo di confidenza si definisce a partire da un campione la cui media è sconosciuta, la sua dimensione è grande e abbiamo calcolato media e varianza campionaria. In queste condizioni il parametro di confidenza è una costante $\alpha \in(0.0,1.0)$ associata a un numero positivo t* tale per cui la probabilità che la media vera e propria sia in un intervallo compreso tra i confini $\bar{x}\pm\left( \frac{\hat{s}t^*}{\sqrt{ p }} \right)$ è circa $(1-\alpha)$, a patto che t approssimi una student con p-1 gradi di libertà

4
Per un campione la cui media è sconosciuta possiamo costruire un intervallo di fiducia partendo dalla definizione usata per gli istogrammi , associamo quindi a $t_{j}=\left( \frac{\bar{x}_{j}-\bar{x}}{\hat{s}_{j}/\sqrt{ p }} \right)$ , quando il campione è sufficientemente grande t approssima una student normalizzata con p-1 gradi di libertà , più p è grande più questa student approssimerà una normale. Questo approccio permette di usare gli stessi metodi di indagine utilizzati conoscendo media e varianza. Per calcolare l'intervallo di confidenza di una sequenza quindi basterà:
- Scegliere un valore di confidenza 
- calcolare media e deviazione standard campionaria 
- determinare il valore critico di t dalla distribuzione t di student con p-1 gradi di libertà (student(p-1,1-$\alpha$/2), se il campione è più grande di 40 possiamo prendere $t_{\infty}$ 
- calcolare i confini dell'intervallo $\bar{x}\pm \frac{t^*\hat{s}}{\sqrt{ p }}$ 
dopodichè , specificata una certa larghezza dell'intervallo richiesta (spesso parametrizzata in termini della deviazione standard tipo 10% di essa), bisogna tenere a mente che w si può usare come parametro per la precisione solo dopo aver raccolto almeno 40 campioni, a questo punto se si ha una ragionevole stima per la deviazione standard possiamo calcolare quanti campioni dovremmo ancora raccogliere per ottenere un intervallo stretto abbastanza. se una ragionevole stima per la deviazione standard non è presente allora si può implementare una sequential stopping rule , calcolando quindi un primo valore per media e deviazione standard e controllando se la precisione richiesta è stata raggiunta. In caso affermativo ci si ferma, altrimenti si va avanti raccogliendo  $\left\lfloor  \left( \frac{t_{\infty}^*\hat{s}}{\bar{x}\epsilon} \right)^2  \right\rfloor$  campioni e verificando se la precisione richiesta non sia stata raggiunta.