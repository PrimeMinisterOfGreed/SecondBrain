## Trigonometria
![[rectangle.png]]
>[!danger] identità fondamentale
>  $$\sin^{2}(\alpha) + \cos^2(\alpha)=1$$
>  $$\frac{a}{\sin(a)}=\frac{b}{\sin(b)}=\frac{c}{\sin(c)}$$

>[!important]  teorema del coseno 
> $a^2=b^2+c^2-2bc*\cos(\alpha)$
> $b^2=a^2+c^2-2ac*\cos(\beta)$
> $c^2=a^2+b^2+2ab*\cos(\gamma)$

>[!important] Definizioni 
> $\sin(\alpha)=\frac{a}{c}$
> $\cos (\alpha)=\frac{b}{c}$
> $\tan(\alpha)=\frac{a}{b}$ => $\tan(\alpha)=\frac{\sin(\alpha)}{\cos(\alpha)}$



## Cinematica

>[!danger] Equazione generale 
> $$x=x_{0}+v_{0}t+\frac{1}{2}at^2$$ 
> 

>[!important] Derivazioni molto usate 
> $v^2=v_{0}+2a\Delta x = v_{0}+2a(x_{1}-x_{0})$ 
> $v=v_{0}+at$
> $x=vt$

### Moto del proiettile 
>[!important] Gittata 
> $$ r= \begin{cases} x=x_{0}+v_{0,x}t \\ y=y_{0}+v_{0,y}t+\frac{1}{2}gt^2 \end{cases} $$

scegliendo $x_{0}=y_{0}=0$ e exploitando $v_{0x}=|v_{0}|\cos \theta$ e $v_{0,y}=|v_{0}|\sin \theta$ e $y=y_{0}+\left( \frac{v_{0,x}}{v_{0,y}} \right)x+\frac{1}{2} \frac{g}{v^2_{0,x}}x^2$

>[!danger] Gittata
> $$ y= y_{0}+ x \tan \theta+\left( \frac{g}{2v^2_{0}\cos^2 \theta} \right)x^2 $$
> $$ R=-\frac{\sin_{2}\theta}{g}v^2_{0} $$




## Dinamica 
>[!important]  2,3 legge di newton 
> $F=ma$ -> forza peso $P=mg$
> $F_{ab}=-F_{ba}$
> nel caso della forza centripeta 
> $F_{c}=ma_{c}=m \frac{v^{2}}{r}$ (ref 1)

>[!important]  Forza gravitazionale 
> $$F_{12}=- \frac{Gm_{1}m_{2}}{|r_{12}|^2}\hat{u}_{r}$$
> $G=6.67*10^{-11}$

### Forza elastica 
>[!important] Legge di hooke 
> $$F=-k(x-x_{0})$$

### Forze vincolari 
>[!important] Attrito 
> Statico :$F_{fr}\leq \mu _sF_{n}$ => $\sum F=0$ 
> dinamico : $F_{fr}=\mu_{d}F_{N}$ => $\sum F \neq 0$ => $\mu_{d}<\mu_{s}$
> massimo angolo: $\theta=\arctan u_{s}$
> 

>[!important] Modello per la forza centrifuga 
> $\sum F_{y}=ma_{y}=F_{N}-mg=0$
> $\sum F_{x}=F_{fr}=ma_{y}=m \frac{v^2_{r}}{r}$ => $v_{R,max}=\sqrt{ \mu_{s}g*r }$
> $F_{fr}\leq \mu_{s}F_{N}=\mu_{s}mg=m \frac{v^2_{R}}{r}$
> angolo con 0 attrito necessario: $\theta=\arctan\left( \frac{v^{2}}{rg} \right)$

>[!important] Terza legge di keplero
> $T^2 \propto R^3 \implies T^2=\left( \frac{4\pi^2}{GM} \right)R^3$ dove M è la massa del sole

## Lavoro ed energia

>[!important] Definizione di lavoro  e energia cinetica
> $$W=F*d = m*a*d= \frac{1}{2}mv_{2}^2 - \frac{1}{2}mv_{1}^2 =K_{2}-K_{1}$$ usando $a=\frac{v_{2}-v_{1}}{2d}$ per cui 
> $$K=\frac{1}{2} mv^2$$

teorema delle forze vive $W=K_{2}-K_{1}=\Delta K$ => forze conservative 

>[!important] Potenziale gravitazionale
> $$U(h)= mgh+U_{0} $$ => $W=-\Delta U$

>[!important] Energia potenziale elastica 
> $$U(x)=\frac{1}{2} kx^2+U_{0}$$ 

>[!important] Conversione 
> $E_{tot}=K+U=const$
> $E_{tot}=U_{g}+U_{e}+K$

>[!important] Potenza 
> $$P=\frac{W}{\Delta t}= F*v$$

>[!important] Quantità di moto 
> $$p=mv\implies \sum F = \frac{d}{dt}p$$ e quindi $\sum F = \frac{dm}{dt}v + m \frac{dv}{dt}= \frac{dm}{dt}v+ma$

con p costante allora si ha la legge di inerzia ($\sum F=0$)
>[!important] Impulso 
> $$I=\Delta p = F = \frac{dp}{dt}\implies dp = F dt \implies \Delta p=\int_{t_{0}}^{t_{1}} F \, dt \equiv I \implies I_{m}=F_{m}\Delta t $$

## Oscillatore armonico 

>[!important] Energia dell'oscillatore armonico 
> $$E_{tot}=K+U_{el}= \frac{1}{2}mv^2+\frac{1}{2}kx^2=const $$
> usando l'ampiezza $E_{tot}=\frac{1}{2}kA^2$ da questo deriva 
> velocità massima $v= \pm v_{0}\sqrt{ 1-\frac{x^2}{A^2} }$

>[!important] Periodo del moto armonico
> periodo $$T=\frac{2\pi a}{v_{0}}=2\pi \sqrt{ \frac{m}{k} }$$ 
>  conservazione dell'energia meccanica $$\frac{A}{v_{0}}=\sqrt{ \frac{m}{k} }$$ 
>  frequenza $f=\frac{1}{T}=\frac{1}{2\pi}\sqrt{ \frac{k}{m} }$
>  pulsazione $\omega=2\pi f= \sqrt{ \frac{k}{m} }$

>[!danger] Legge oraria del moto armonico 
> $$x(t)=A\cos \theta = A\cos(\omega t + \phi)$$ con $\theta=\frac{2\pi t}{T}=\omega t$

>[!important] derivazioni 
> - posizione: $x(t)=A\cos(\omega t)=A \cos\left( \frac{2\pi t}{T} \right)$ 
> - velocità : $v(t)=\frac{dx}{dt}=-\omega A\sin(\omega t)=-v_{0}\sin(\omega t)$
> - accelerazione $a(t)=\frac{dv}{dt}=-\omega^2 A\cos(\omega t)=-\omega^2x(t)$
> - conservazione: $v_{0}^2=\omega^2A^2=\frac{k}{m}A^2$

### Moto armonico forzato e smorzato 
>[!important] forzato 
> 2 legge di newton e equilibrio: $\sum F=mg - kx_{0}=0 \implies x_{0}=\frac{mg}{k}$ 

>[!important] smorzato 
> $F_{fr}=-bv$ dove b è un termine di smorzamento
> $\sum F=-kx-b \frac{dx}{dt}=ma=m \frac{d^2x}{dt^2}$
> $x(t)=A \cos(\omega t+\phi)e^{t(b/2m)}$

### Pendolo semplice 
>[!important] 
> Componente normale alla traiettoria s 
> $$ \sum F_{n}=T -mg\cos \theta = 0 $$
> componente tangenziale 
> $$\sum F_{t} = -mg \sin \theta$$
> derivazioni 
> $\theta(t)=\theta_{0}\cos(\omega t)$ 
> $\omega=\sqrt{ \frac{g}{L} }$



## Meccanica dei sistemi : moti traslatori 
>[!important] Centro di massa 
> $$ x_{CM}= \frac{1}{M} \sum_{i}m_{i}x_{i}$$
> $$ v_{CM}= dx_{CM}/dt= \frac{d}{dt}\left( \frac{1}{M} \right) \sum_{i} m_{i}x_{i}=\frac{1}{M} \sum_{i}m_{i}v_{i}$$ l'ultimo passaggio è valido a massa costante.
> Per cui si ottiene che 
> $$ Mv_{CM}=p_{CM}=\sum_{i}p_{i}$$
> $$ a_{CM}=1/M \sum_{i}m_{i}a_{i}$$

>[!important] Estensione della 2 legge della dinamica 
> $$ F_{i}+\sum_{j\neq i}=m_{i}a_{i}$$
> $$ F_{ris}=\sum_{i}F_{i}+0=\sum_{i}m_{i}a_{i}=Ma_{CM}$$

### Sistemi a massa variabile 

>[!important] 2 legge di newton per s a massa var 
> $p_{i}=Mv$, $p_{f}=(M-\Delta M)(v+\Delta v)+Mu$
> $$\Delta p=p_{f}-p_{i}=M \Delta v-\Delta Mv-\Delta M\Delta v+\Delta Mu$$
> $$F_{ext}=\lim_{ \Delta t \to 0 } \frac{\Delta p}{\Delta t}= M \frac{dv}{dt}+(u-v) \frac{dM}{dt} $$ => $v_{rel}=v-u$ 

>[!danger] Thrust
> $$M \frac{dv}{dt}=-v_{rel} \frac{dM}{dt} \implies m*a=-v_{rel} \frac{dM}{dt}$$
> 
> $$ M_{f}/M_{0}=e^{-vf/v_{rel}}$$

## Meccanica dei sistemi: moti rotazionali 

>[!important] Accelerazione radiale e tangenziale 
> $$ a_{R}=\frac{v^2}{r}=\omega^2r$$
> $$ a_{T}= \frac{dv}{dt}= r \frac{d\omega}{dt}  $$
> $$ a = a_{R}+a_{T}= -\frac{v^2}{r}u_{r}+r \ddot{\theta}u_{\theta}$$
> $r \ddot{\theta} = r \frac{d^2\theta}{dt^2}$

>[!important] corrispondenza con leggi cinematiche 
> $\ddot{\theta} = \alpha$
> $\omega=\omega_{0}+\alpha t \implies v=v_{0}+at$
> $\theta=\omega_{0}t+\frac{1}{2}\alpha t^{2}\implies s=v_{0}t+\frac{1}{2}at^{2}$
> $\omega^{2}=\omega_{0}^{2}+2\alpha \theta \implies v^{2}=v_{0}^{2}+2as$
> $\bar{\omega}=\frac{\omega+\omega_{0}}{2}\implies  \bar{v}=\frac{v+v_{0}}{2}$

>[!derivazioni usate]
> $$ v = \omega r$$
> $$ a= \alpha r $$
 
>[!danger]  Momento Torcente 
> $\tau=r\perp F$
> $$\tau=rF\perp$$
> $$\tau=rF\sin \theta$$

>[!danger] Momento di inerzia 
> $$I=\sum_{i}m_{i}d^{2}_{i}$$
> $$ \sum \tau = I \alpha $$

c'é una tabella che li riporta 

>[!danger] Energia cinetica rotazionale 
> $$K_{rot}= \sum_{i} \left( \frac{1}{2} m_{i}v_{i}^{2} \right) =\frac{1}{2}I \omega_{2}$$
> $$ K_{tot}=K_{tr}+K_{rot}= \frac{1}{2}m_{i}v_{CM}^{2}+\frac{1}{2}I_{CM}\omega^{2}_{CM} $$

>[!important] Lavoro e potenza del momento torcente 
> $$W=F \Delta l=F r \Delta \theta = \tau \Delta \theta$$
> $$p=\frac{dW}{dt}=t \frac{d\theta}{dt}=\tau * \omega$$

>[!important] Momento angolare 
> $$L=I \omega$$
> $$\sum \tau = \frac{dL}{dt} = I \alpha$$
> $$ \sum \tau = 0 \implies L = const$$
> $$ K_{tot}= K_{tr}+ k_{rot} = \frac{1}{2} mv^{2} + \frac{1}{2} I \omega^{2} $$
> $$m r_{1} \omega_{1} = m r_{2} \omega_{2} $$

## Equilibrio in presenza di rotazioni 

>[!danger] Condizioni di equilibrio 
> prima condizione (traslazione): $$R=\sum F = 0$$
> seconda condizione (rotazione): $$T=\sum \tau = 0 \implies \sum$$

vale in ogni direzione , quindi sono 6 equazioni (2x3 direzioni) 

>[!important] Forza applicata alla leva 
> $$\frac{r}{R}= \frac{F_{p}}{mg}$$


>[!important] Modulo di young , sforzo e deformazione 
> allungamento $$\Delta L = \frac{1}{E} \frac{F}{A} L_{0}$$
> deformazione = $\Delta L / L_{0}$ , modulo di young = sforzo/deformazione = E

>[!important] Sforzo di taglio 
> $$\Delta L= \frac{1}{G} \frac{F}{A} L_{0}$$
G = modulo di taglio

>[!important] Modulo di compressione 
> $$\frac{\Delta V}{V_{0}}=-\frac{1}{B} \Delta P$$
V= volume, B modulo di compressione 

## Onde Meccaniche 

>[!important] Dal moto armonico  
> $E_{tot}=\frac{1}{2}kA^{2}$
> $T=2\pi \sqrt{ \frac{m}{k} }$
> $f=\frac{1}{T}$
> $\omega=2\pi f$

>[!important] velocità d'onda 
> $$v=\frac{\Delta s}{\Delta t}=\frac{\lambda}{T}=\lambda f$$ 
> $$v= \sqrt{ \frac{F_{T}}{u} }=\sqrt{ \frac{F_{T}}{\frac{M}{L}} }$$
>  con Ft => forza tensione corda, u= densità lineare della corda M = massa L=lunghezza
>  velocità di propagazione 
>  solidi $v=\sqrt{ \frac{E}{\rho} }$ , liquidi $v=\sqrt{ \frac{B}{\rho} }$
>  dove E e B sono young e compressione

>[!important] Intensità
> $$I=\frac{P}{A}=\frac{P}{4\pi r^{2}}$$
> $$ I_{1}d_{1}^{2} = I_{2}d_{2}^{2} $$
> $$\frac{I_{1}}{I_{2}}=\frac{r_{2}^{2}}{r_{1}}^{1}\implies \frac{A_{1}}{A_{2}}=\frac{r_{2}}{r_{1}}$$

>[!important] Problemi con interfaccia 
> $k= \frac{2\pi}{\lambda}$
>$$u_{tot}=A_{i}\cos(k_{I}x-\omega t)+A_{r}\cos(-k_{I}x-\omega t)+A_{T}\cos(k_{T}x - \omega t)$$
> con estremo fisso: $A_{I}=-A_{R}$
> con estremo libero: $A_{I}=A_{R}$

>[!important]  Condizioni al punto di giunzione 
> $u_{L}+u_{R}=u_{T} \implies A_{I}+A_{R}=A_{T}$
> $$-A_{I}k_{I}+A_{R}k_{I}=-A_{T}k_{T}\implies A_{T}= \frac{A_{I}k_{I}-A_{R}k_{I}}{k_{T}}$$
> mettendole a sistema si ottiene 
> $$A_{T}=A_{I} \frac{2k_{I}}{k_{I}+k_{T}}$$ 
> $$A_{R}=A_{I} \frac{k_{I}-k_{T}}{k_{I}+k_{T}}$$



>[!important] Onde stazionarie 
> $$u_{I}+u_{R}=2A \cos(kx)\cos(\omega t)$$
> $$E_{tot}=\frac{1}{4}mA_{n}^{2}\omega^{2}_{n}$$
> $$\lambda_{n}=\frac{2L}{n}, f_{n}=\frac{nv}{2L}$$
> dove n è l'n-esima armonica superiore, la fondamentale è a $\lambda=2L$


## Acustica 
>[!important] Velocità di propagazione
> $$ v= \sqrt{ \frac{B}{\rho} } $$
> in aria $$ v=(331+0.6T) $$

>[!important] Pressione 
> $$ P=\frac{F_{N}}{A} $$

>[!danger] Volume 
> $I_{0}=10^{-12}$
> $$ \beta(dB)=10 \log \frac{I}{I_{0}} $$
> $I \propto \frac{1}{r^{2}}$

temperamento equabile: $\sqrt{ 2 }^{12}$

### Strumenti a fiato 

Aperti da entrambi i lati 

prima armonica (fondamentale)  => $L=\frac{1}{2}\lambda_{1}$ , $f_{1}=\frac{v}{2L}$ 
seconda armonica => $L=\lambda_{2}$ , $f_{2}=\frac{v}{L}=2f_{1}$
terza armonica => $L= \frac{3}{2}\lambda_{3}, f_{3}= \frac{3v}{2L}=3f_{1}$

Chiusi da un lato

prima armonica (fondamentale)  => $L=\frac{1}{4}\lambda_{1}$ , $f_{1}=\frac{v}{4L}$ 
terza armonica => $L= \frac{3}{4}\lambda_{3}, f_{3}= \frac{3v}{4L}=3f_{1}$
quinta armonica => $L=\frac{5}{4} \lambda_{5}, f_{5}=\frac{5v}{4L}=5f_{1}$

>[!important] modulazione  
> battimenti: $f_{mod}=|f_{1}-f_{0}|$ 
> portante : $f_{ris}= \frac{f_{1}+f_{2}}{2}$


### Effetto doppler 
sorgente ferma , osservatore in moto 
>[!important] Avvicinamento e allontanamento 
> avvicinamento:
>  $$ f_{0}= \frac{v+v_{s}}{\lambda}= \frac{v+v_{s}}{v}f_{s} $$
>  allontanamento 
>  $$ f_{0}= \frac{v-v_{s}}{v}f_{s} $$

tutti in moto 

>[!important] Sorgente e osservatore in moto 
> $$ f_{0}= \frac{v+v_{0}}{v+v_{s}} f_{s} $$


## Ottica Geometrica 

>[!important] Fuoco 
> $$ f=\frac{r}{2} $$

>[!danger]  Equazione degli specchi 
> $$ \frac{1}{f}=\frac{1}{d_{i}}+\frac{1}{d_{o}} $$

>[!important] ingrandimento 
> $$ m=\frac{h_{i}}{h_{o}}=- \frac{d_{i}}{d_{o}} $$

>[!important] indice di rifrazione
>$$ n=\frac{c}{v} $$

>[!danger] Legge di snell 
> $$ n_{1}\sin \theta_{1}=n_{2} \sin \theta_{2} $$
> $$ \sin \theta_{c} = \frac{n_{2}}{n_{1}} $$

>[!important] Diottria o potenza della lente 
> $$ P=\frac{1}{f} $$

## Ottica ondulatoria 

>[!important] Principio di Huygens 
> $$ \frac{\sin \theta_{2}}{\sin \theta_{1}}=\frac{n_{1}}{n_{2}} $$
> $$ \frac{\lambda_{1}}{\lambda_{2}}=\frac{n_{2}}{n_{1}} $$

>[!important] Ordine della frangia di interferenza 
> massimo di interferenza: $$ m \lambda = D \sin \theta $$ 
> minimo di interferenza :
> $$ n \lambda = A \sin \theta $$

## Meccanica dei fluidi 

>[!important] Densità 
> densità : $$ \rho=\frac{m}{V} $$
> peso specifico: $$ \sigma= \frac{mg}{V}= \rho g $$

>[!important] Pressione 
> $$ p=\frac{F\perp}{S} $$
>

>[!important] Forze di volume e di superficie 
> volume : $$ dF^{(V)}=g dm = g \rho dV $$
> superficie: 
> $$dF \parallel = \tau dS, dF \perp= \rho dS $$
> 

>[!danger] Legge di stevino 
> per equilibrio idrostatico $\sum F = 0$ => $$ p = p_{0}+\rho gh $$
>  esercizio sulla diga:
> $$ F= p_{0}ld+\frac{1}{2}\rho g l d ^{2} $$

>[!important]  Legge di pascal 
> $$ F_{2}= \frac{S_{2}}{S_{1}} F_{1} $$
> per il lavoro compiuto dal pistone 
> $W_{1}=W_{2}\implies F_{1}d_{1}=F_{2}d_{2}$

>[!important] Principio di archimede
> per un liquido 
> $$ -M_{l}g + F_{p}= 0 $$
> $$ F_{p}=M_{l}g= \rho_{l}Vg \equiv B \implies B=\rho_{l} V g$$
> per un oggetto 
>  $$ \sum F_{y}= -M_{0}g+B = \rho_{l}V g- \rho_{0}V g= (\rho_{l}-\rho_{0})Vg $$

se un corpo galleggia allora 
$$ \sum F = -\rho_{0} V_{0} g + \rho_{f} V_{f}g = 0 \implies \rho_{0} V_{0} = \rho_{f}V_{f}$$


>[!summary] legge di stokes 
> $$ v=gV \frac{\rho_{l}-\rho_{0}}{6\pi \eta r} $$

### Continuità e portata 
>[!important] Conservazione della massa 
> $$ \Delta M_{1}=\rho A_{1}v_{1}\Delta t=\rho A_{1}\Delta x_{1}=\rho \Delta V_{1} $$ $$\Delta M_{2}=\rho A_{2}v_{2}\Delta t=\rho A_{2}\Delta x_{2}=\rho \Delta V_{2}$$ $$\implies \rho A_{i}\Delta x_{i} = const $$

>[!important] Portata 
> in volume: $$ Q_{v}= \frac{\Delta V}{\Delta t} = A*v $$
> in massa: $$ Q_{M}= \frac{\Delta M}{\Delta t} $$


>[!danger] Teorema di bernoulli 
> $$ p+\rho g y + \frac{1}{2}\rho v^{2} = const $$
> derivato da una considerazione sul lavoro svolto da un liquido con variazione cinetica 
> $$ \Delta K = \frac{1}{2}m (v_{2}^{2}- v_{1}^{2})= \frac{\rho v}{2}(v_{2}^{2}-v_{1}^{2}) $$ usando il teorema delle forze vive $L_{tot}=\Delta K$ 




