# Fiche de cours : charge des condensateurs, temps de charge et oscillateurs

Niveau : Terminale à L2 / BUT GEII – Durée conseillée : 2 séances de 2 h (cours + TD)

---

## Objectifs

- Établir et résoudre l'équation différentielle de la charge et de la décharge d'un condensateur.
- Calculer une constante de temps, un temps de charge, un temps pour atteindre un seuil.
- Comprendre comment la charge entre deux seuils produit un oscillateur à relaxation (NE555, AOP).
- Connaître l'oscillateur LC / RLC : période propre, énergie, régimes d'amortissement.

---

## Partie 1 – Le condensateur

| Grandeur | Formule | Unités |
|---|---|---|
| Charge | $q = C u_C$ | C (coulomb), F, V |
| Intensité (convention récepteur) | $i = \dfrac{dq}{dt} = C \dfrac{du_C}{dt}$ | A |
| Énergie stockée | $E_{el} = \dfrac{1}{2} C u_C^2 = \dfrac{q^2}{2C}$ | J |
| Association série | $\dfrac{1}{C_{eq}} = \sum \dfrac{1}{C_k}$ | F |
| Association parallèle | $C_{eq} = \sum C_k$ | F |

À retenir : la tension aux bornes d'un condensateur est **continue** (elle ne peut pas changer brusquement), car l'énergie ne peut pas varier instantanément.

---

## Partie 2 – Charge et décharge dans un circuit RC série

### 2.1 Charge sous un échelon de tension E

Loi des mailles : $E = R i + u_C$, donc

$$
\boxed{RC \frac{du_C}{dt} + u_C = E}
$$

Avec $u_C(0) = 0$ :

$$
\boxed{u_C(t) = E\left(1 - e^{-t/\tau}\right)} \qquad \boxed{i(t) = \frac{E}{R} e^{-t/\tau}} \qquad \boxed{\tau = RC}
$$

### 2.2 Décharge (condensateur initialement à $U_0$)

$$
RC \frac{du_C}{dt} + u_C = 0 \quad\Rightarrow\quad \boxed{u_C(t) = U_0 e^{-t/\tau}} \qquad i(t) = -\frac{U_0}{R} e^{-t/\tau}
$$

### 2.3 Valeurs remarquables (charge)

| $t$ | $\tau$ | $2\tau$ | $3\tau$ | $4\tau$ | $5\tau$ |
|---|---|---|---|---|---|
| $u_C / E$ | 63 % | 86 % | 95 % | 98 % | 99,3 % |

- **Durée du régime transitoire** : $\Delta t \approx 5\tau$ (charge ou décharge quasi complète).
- **Détermination graphique de τ** : (1) abscisse où la tangente à l'origine coupe l'asymptote $u_C = E$ ; (2) date où $u_C = 0{,}63 E$ (charge) ou $0{,}37 U_0$ (décharge).

### 2.4 Temps pour atteindre une tension donnée

Pour la charge, le temps pour atteindre $u_C = U$ est :

$$
\boxed{t = \tau \ln\left(\frac{E}{E-U}\right)}
$$

**Forme générale (charge vers une tension cible $V_\infty$, de $U_1$ à $U_2$)** – formule clé pour les oscillateurs :

$$
\boxed{\Delta t = \tau \ln\left(\frac{V_\infty - U_1}{V_\infty - U_2}\right)}
$$

### 2.5 Bilan énergétique de la charge complète

- Énergie fournie par le générateur : $C E^2$
- Énergie stockée dans le condensateur : $\frac{1}{2} C E^2$
- Énergie dissipée par effet Joule dans R : $\frac{1}{2} C E^2$ (indépendante de R).

---

## Partie 3 – Oscillateurs à relaxation (multivibrateurs astables)

Principe : un condensateur se charge et se décharge **entre deux seuils** ; un comparateur bascule à chaque seuil. La période se calcule avec la formule 2.4.

### 3.1 Astable à NE555

Le condensateur oscille entre $V_{CC}/3$ et $2V_{CC}/3$. Il se charge à travers $R_1 + R_2$ (sortie à l'état haut), puis se décharge à travers $R_2$ via la broche 7 (sortie à l'état bas).

Charge de $V_{CC}/3$ à $2V_{CC}/3$ vers $V_{CC}$ : $\ln \dfrac{V_{CC} - V_{CC}/3}{V_{CC} - 2V_{CC}/3} = \ln 2$

$$
\boxed{t_H = \ln 2 \, (R_1+R_2) C \approx 0{,}693 (R_1+R_2) C} \qquad \boxed{t_L = \ln 2 \cdot R_2 C}
$$

$$
\boxed{T = 0{,}693 (R_1 + 2R_2) C} \qquad f \approx \frac{1{,}44}{(R_1+2R_2) C} \qquad \alpha = \frac{t_H}{T} = \frac{R_1+R_2}{R_1+2R_2}
$$

Remarque : avec ce montage de base, $\alpha > 50$ % (une diode en parallèle sur $R_2$ permet de descendre en dessous).

### 3.2 Astable à AOP (comparateur à hystérésis + RC)

Sortie $\pm V_{sat}$, seuils $\pm\beta V_{sat}$ avec $\beta = \dfrac{R_2}{R_1+R_2}$. Le condensateur se charge à travers R entre $-\beta V_{sat}$ et $+\beta V_{sat}$ :

$$
\boxed{T = 2RC \ln\left(\frac{1+\beta}{1-\beta}\right)}
$$

Cas particulier $R_1 = R_2$ ($\beta = 0{,}5$) : $T = 2RC\ln 3 \approx 2{,}2 RC$.

---

## Partie 4 – Oscillateurs harmoniques LC et RLC

### 4.1 Circuit LC idéal (oscillations libres non amorties)

$$
\frac{d^2q}{dt^2} + \omega_0^2 q = 0 \qquad \boxed{\omega_0 = \frac{1}{\sqrt{LC}}} \qquad \boxed{T_0 = 2\pi\sqrt{LC}}
$$

Solution (condensateur chargé sous E, $i(0)=0$) : $q(t) = Q_0\cos(\omega_0 t)$ avec $Q_0 = CE$, $I_{max} = Q_0 \omega_0$.

Conservation de l'énergie : $E_{tot} = \dfrac{q^2}{2C} + \dfrac{1}{2} L i^2 = \dfrac{Q_0^2}{2C} = \dfrac{1}{2} L I_{max}^2 = \text{cte}$

### 4.2 Circuit RLC série libre (oscillations amorties)

$$
\frac{d^2q}{dt^2} + \frac{R}{L}\frac{dq}{dt} + \omega_0^2 q = 0
$$

| Paramètre | Formule |
|---|---|
| Résistance critique | $R_c = 2\sqrt{L/C}$ |
| Facteur de qualité | $Q = \dfrac{1}{R}\sqrt{\dfrac{L}{C}} = \dfrac{L\omega_0}{R}$ |
| Pseudo-période | $T = \dfrac{T_0}{\sqrt{1 - \frac{1}{4Q^2}}} \approx T_0$ si $Q \gg 1$ |

- $R < R_c$ : régime **pseudo-périodique** (oscillations amorties)
- $R = R_c$ : régime **critique** (retour à zéro le plus rapide sans oscillation)
- $R > R_c$ : régime **apériodique**

L'énergie diminue par effet Joule. Pour **entretenir** les oscillations, il faut compenser les pertes (montage à résistance négative, oscillateurs Colpitts, Hartley, pont de Wien).

---

## Exercices

### Exercice 1 – Charge d'un condensateur (application directe)

Un condensateur $C = 100~\mu\mathrm{F}$, initialement déchargé, est chargé à travers $R = 10~\mathrm{k\Omega}$ par un générateur $E = 12~\mathrm{V}$.

1. Calculer τ et la durée de la charge.
2. Calculer $u_C$ à $t = 2~\mathrm{s}$.
3. À quelle date $u_C = 9~\mathrm{V}$ ?
4. Calculer l'intensité à $t = 0$ et l'énergie stockée en fin de charge.

### Exercice 2 – Décharge

Un condensateur $C = 470~\mu\mathrm{F}$ chargé sous $5~\mathrm{V}$ se décharge dans $R = 2{,}2~\mathrm{k\Omega}$.

1. Calculer τ.
2. Au bout de combien de temps $u_C = 1~\mathrm{V}$ ?
3. Quelle fraction de l'énergie initiale reste stockée à ce moment ?

### Exercice 3 – Lecture graphique

Lors de la charge d'un condensateur sous $E = 6{,}0~\mathrm{V}$ à travers $R = 1{,}0~\mathrm{k\Omega}$, on mesure à l'oscilloscope $u_C = 3{,}78~\mathrm{V}$ à $t = 2{,}0~\mathrm{ms}$.

1. Montrer que cette date correspond à τ.
2. En déduire C.

### Exercice 4 – Minuterie (temporisation)

Une minuterie déclenche l'extinction d'une lampe lorsque la tension d'un condensateur, en charge sous E, atteint le seuil $\frac{2}{3} E$. On dispose de $C = 1000~\mu\mathrm{F}$.

Quelle résistance R faut-il pour une temporisation de 30 s ?

### Exercice 5 – Astable NE555

1. Avec $R_1 = 1~\mathrm{k\Omega}$, $R_2 = 10~\mathrm{k\Omega}$ et $C = 10~\mu\mathrm{F}$, calculer $t_H$, $t_L$, T, f et α. Une LED en sortie clignote-t-elle de façon visible ?
2. **Dimensionnement** : on veut $f = 1~\mathrm{kHz}$ et $\alpha = 60$ % avec $C = 100~\mathrm{nF}$. Calculer $R_1$ et $R_2$.

### Exercice 6 – Astable à AOP

Un astable à AOP utilise $R = 10~\mathrm{k\Omega}$, $C = 100~\mathrm{nF}$ et un pont de réaction $R_1 = R_2$. Calculer la période et la fréquence.

### Exercice 7 – Oscillateur LC idéal

Un condensateur $C = 0{,}50~\mu\mathrm{F}$ chargé sous $E = 6{,}0~\mathrm{V}$ est relié à $t = 0$ à une bobine idéale $L = 0{,}50~\mathrm{H}$.

1. Calculer $\omega_0$, $T_0$ et $f_0$.
2. Calculer la charge maximale $Q_0$ et l'intensité maximale $I_{max}$.
3. Vérifier la conservation de l'énergie.

### Exercice 8 – Circuit RLC amorti

Un circuit RLC série comporte $L = 1{,}0~\mathrm{H}$, $C = 15~\mu\mathrm{F}$ et $R = 50~\Omega$.

1. Calculer la résistance critique. Quel est le régime ?
2. Calculer le facteur de qualité et estimer la pseudo-période.

### Exercice 9 – Simulation Python (méthode d'Euler)

Écrire un script qui résout $\dfrac{du_C}{dt} = \dfrac{E - u_C}{RC}$ par la méthode d'Euler (données de l'exercice 1), puis comparer $u_C(\tau)$ à la solution exacte.

---

## Corrigés

### Corrigé 1

1. $\tau = RC = 10\times10^3 \times 100\times10^{-6} = 1{,}0~\mathrm{s}$ ; charge quasi complète au bout de $5\tau = 5{,}0~\mathrm{s}$.
2. $u_C(2) = 12 (1 - e^{-2}) = 12 \times 0{,}865 \approx 10{,}4~\mathrm{V}$.
3. $t = \tau\ln\dfrac{E}{E-U} = 1{,}0 \times \ln\dfrac{12}{3} = \ln 4 \approx 1{,}39~\mathrm{s}$.
4. $i(0) = E/R = 12 / 10^4 = 1{,}2~\mathrm{mA}$ ; $E_{el} = \frac{1}{2} C E^2 = 0{,}5 \times 10^{-4} \times 144 = 7{,}2~\mathrm{mJ}$.

### Corrigé 2

1. $\tau = 2{,}2\times10^3 \times 470\times10^{-6} \approx 1{,}03~\mathrm{s}$.
2. $1 = 5 e^{-t/\tau} \Rightarrow t = \tau \ln 5 \approx 1{,}03 \times 1{,}609 \approx 1{,}66~\mathrm{s}$.
3. L'énergie varie comme $u_C^2$ : $\left(\frac{1}{5}\right)^2 = 0{,}04$, soit 4 % (0,235 mJ restants sur 5,88 mJ).

### Corrigé 3

1. $3{,}78 / 6{,}0 = 0{,}63$ : c'est la valeur atteinte à $t = \tau$, donc $\tau = 2{,}0~\mathrm{ms}$.
2. $C = \dfrac{\tau}{R} = \dfrac{2{,}0\times10^{-3}}{1{,}0\times10^3} = 2{,}0~\mu\mathrm{F}$.

### Corrigé 4

$\frac{2}{3} E = E(1 - e^{-t/\tau}) \Rightarrow e^{-t/\tau} = \frac{1}{3} \Rightarrow t = \tau\ln 3 \approx 1{,}10 \tau$.

$R = \dfrac{t}{C\ln 3} = \dfrac{30}{10^{-3} \times 1{,}099} \approx 27~\mathrm{k\Omega}$ (valeur normalisée : 27 kΩ).

### Corrigé 5

1. $t_H = 0{,}693 \times 11\times10^3 \times 10\times10^{-6} \approx 76~\mathrm{ms}$ ; $t_L = 0{,}693 \times 10^4 \times 10^{-5} \approx 69~\mathrm{ms}$.
   $T \approx 146~\mathrm{ms}$, $f \approx 6{,}9~\mathrm{Hz}$, $\alpha = 11/21 \approx 0{,}52$ soit 52 %. Oui, environ 7 clignotements par seconde sont visibles à l'œil.
2. $T = 1~\mathrm{ms}$ donc $t_H = 0{,}6~\mathrm{ms}$ et $t_L = 0{,}4~\mathrm{ms}$.
   $R_2 = \dfrac{t_L}{0{,}693 C} = \dfrac{0{,}4\times10^{-3}}{0{,}693\times10^{-7}} \approx 5{,}77~\mathrm{k\Omega}$
   $R_1 + R_2 = \dfrac{t_H}{0{,}693 C} \approx 8{,}66~\mathrm{k\Omega} \Rightarrow R_1 \approx 2{,}89~\mathrm{k\Omega}$

### Corrigé 6

$\beta = 0{,}5 \Rightarrow T = 2RC\ln 3 = 2 \times 10^4 \times 10^{-7} \times 1{,}099 \approx 2{,}20~\mathrm{ms}$ ; $f \approx 455~\mathrm{Hz}$.

### Corrigé 7

1. $LC = 0{,}25\times10^{-6}~\mathrm{s^2} \Rightarrow \omega_0 = 1/\sqrt{LC} = 2000~\mathrm{rad/s}$ ; $T_0 = 2\pi\sqrt{LC} \approx 3{,}14~\mathrm{ms}$ ; $f_0 \approx 318~\mathrm{Hz}$.
2. $Q_0 = CE = 3{,}0~\mu\mathrm{C}$ ; $I_{max} = Q_0 \omega_0 = 6{,}0~\mathrm{mA}$.
3. $\frac{1}{2} CE^2 = 0{,}5 \times 0{,}5\times10^{-6} \times 36 = 9{,}0~\mu\mathrm{J}$ et $\frac{1}{2} L I_{max}^2 = 0{,}5 \times 0{,}5 \times (6\times10^{-3})^2 = 9{,}0~\mu\mathrm{J}$. L'énergie est bien conservée.

### Corrigé 8

1. $R_c = 2\sqrt{L/C} = 2\sqrt{1/(15\times10^{-6})} \approx 516~\Omega$. Comme $R = 50~\Omega < R_c$, le régime est pseudo-périodique.
2. $Q = \dfrac{1}{R}\sqrt{\dfrac{L}{C}} \approx \dfrac{258}{50} \approx 5{,}2$. Comme $Q \gg 1$, $T \approx T_0 = 2\pi\sqrt{LC} \approx 24~\mathrm{ms}$ (on compte environ Q ≈ 5 oscillations visibles avant extinction).

### Corrigé 9

```python
import numpy as np
import matplotlib.pyplot as plt

R, C, E = 10e3, 100e-6, 12.0
tau = R * C
dt = tau / 100                       # pas de calcul
t = np.arange(0, 5 * tau, dt)
u = np.zeros_like(t)
for k in range(len(t) - 1):
    u[k + 1] = u[k] + dt * (E - u[k]) / tau   # schéma d'Euler explicite

u_exact = E * (1 - np.exp(-t / tau))
print(f"Euler : u(tau) = {u[100]:.3f} V  |  exact : {u_exact[100]:.3f} V")

plt.plot(t, u, label="Euler")
plt.plot(t, u_exact, "--", label="Exacte")
plt.axhline(0.63 * E, color="gray", lw=0.8)
plt.axvline(tau, color="gray", lw=0.8)
plt.xlabel("t (s)"); plt.ylabel("u_C (V)"); plt.legend(); plt.grid()
plt.show()
```

Résultat : Euler donne $u_C(\tau) \approx 7{,}61~\mathrm{V}$ contre $7{,}59~\mathrm{V}$ pour la solution exacte (écart d'environ 0,3 %). Diviser le pas par 10 réduit l'écart d'un facteur 10 environ (méthode d'ordre 1).

Prolongement possible : simuler l'astable NE555 en inversant la cible de charge ($V_{CC}$ ou 0) à chaque franchissement des seuils $V_{CC}/3$ et $2V_{CC}/3$.

---

## Ressources pour aller plus loin

- Charge RC et τ : [Kartable](https://www.kartable.fr/ressources/physique-chimie/cours/la-dynamique-dun-systeme-electrique-capacitif/52467), [CPGE Parriat (PDF)](http://cpge-parriat.fr/wp-content/uploads/2024/05/P11_regime_transitoire_circuit_RC_cours.pdf), [Physagreg](https://www.physagreg.fr/electrocinetique-2-condensateur-bobine.php)
- Oscillations RLC : [Physagreg – Oscillations électriques (PDF)](https://www.physagreg.fr/CoursTS/Physique/Cours/Physique-C-chap8-oscillations_electriques.pdf)
- Oscillateurs à relaxation : [Étienne Thibierge – Oscillateurs auto-entretenus (PDF)](https://www.etienne-thibierge.fr/cours_2025/06_oscillateurs_poly-prof.pdf)
- NE555 : [Électronique Mixte](https://www.electronique-mixte.fr/logiciels/ne-555/), [Electronics Tutorials](https://www.electronics-tutorials.ws/sequential/seq_3.html)
