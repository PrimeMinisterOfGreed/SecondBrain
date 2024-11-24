un segnale può essere generato da:
- Una sorgente => **Segnale Scalare**
- Più sorgenti => **Segnale Vettoriale**
se un segnale è rappresentato da valori reali allora è reale, altrimenti è complesso.

Un segnale è caratterizzato da:
- **Ampiezza** => il suo valore numerico 
- Variazione di Ampiezza => forma d'onda

Un segnale può essere in base alla discretizzazione:
- Continuo => Segnale analogico => $u(t) \rightarrow u(t,y,z)$ (banalmente un video in questo caso)
- Discreto => Segnale digitale $v[n] \rightarrow v[x,y,z]$ (per esempio nel caso di un immagine) 

I valori dei segnali possono essere:
- Deterministici => seguono una legge matematica
- Aleatori => provengono da una fonte aleatoria (rumore)

# Operazioni di processamento
## Operazioni sul dominio del tempo 
- Scaling => moltiplicazione per costante 
- Delay  => $x(t) \rightarrow y(t)=x(t-t_{0})$ => ritardo su $t_{0}$ , se $t_{0} < 0$  allora è anticipo 
- Addizione => $y_{1}(t)= x_{1}(t)+x_{2}(t)\dots$ 
- Moltiplicazione => $y_{1}(t)=x_{1}(t)*x_{2}(t)\dots$
- 
