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
- Integrazione => $y(1)= \int^{-\infty}_{t}x(\tau)d\tau$
- Differenziazione => $y(1)= \frac{dx(t)}{dt}$ 

Alcune operazioni sono meglio eseguibili nel dominio delle frequenze, a cui si passa usando la trasformata di fourier
$$
X(j\Omega) = \int^{t}_{-\infty}x(t)e^{-j\Omega t}dt
$$
definito anche **spettro di** $x(t)$ l'operazione di passaggio serve per eseguire il filtraggio del segnale. Il range di frequenze che può passare da un filtro è detto **banda passante** mentre quella che non passa è la **banda filtrata**.
In molti casi la **funzione filtrante** è lineare tempo invariante =>
Sia $h(t)$ => impulso di risposta => il segnale è $y(t)=\int^{\infty}_{-\infty}h(t-\tau)x(\tau)dt$. 

Assumendo che il filtro non abbia precondizioni allora si può riscrivere come $Y(j\Omega)=H(j\Omega)x(j\Omega)$ dove Y,X e H sono le trasformazioni di fourier di y,x,e h. 

Un **filtro passa basso** => blocca tutte le frequenze $>f_{s}$ 
Un **filtro passa alto** => blocca tutte le frequenze $<f_{s}$ 
Un **filtro a banda passante** => fa passare le frequenze in $f_{s_{1}}<f<f_{s_{2}}$ 

