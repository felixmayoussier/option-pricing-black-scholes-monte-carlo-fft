# Pricing d'options européennes : Black–Scholes, Monte Carlo et FFT de Carr–Madan

## Présentation

Ce projet compare plusieurs méthodes de valorisation d'options européennes dans le cadre du modèle de Black–Scholes :

1. Formule analytique de Black–Scholes
2. Simulation de Monte Carlo
3. Méthode de Carr–Madan utilisant la Transformée de Fourier Rapide (FFT)

L'objectif est d'étudier à la fois la précision numérique et la complexité algorithmique de ces différentes approches.

---

## Contexte mathématique

Sous la mesure risque-neutre, le prix d'un call européen s'écrit :

\[
C_0 = e^{-rT}\mathbb{E}\left[(S_T-K)^+\right]
\]

où :

- \(S_T\) est le prix du sous-jacent à maturité ;
- \(K\) est le prix d'exercice (strike) ;
- \(r\) est le taux sans risque ;
- \(T\) est la maturité ;
- \(\sigma\) est la volatilité.

Dans le modèle de Black–Scholes, le sous-jacent suit l'équation différentielle stochastique :

\[
dS_t = rS_tdt + \sigma S_t dW_t
\]

ce qui permet d'obtenir une formule fermée pour le prix de l'option.

---

## Méthodes implémentées

### 1. Formule analytique de Black–Scholes

Cette méthode fournit la valeur exacte de référence dans le cadre du modèle de Black–Scholes.

**Avantages :**
- Calcul instantané ;
- Solution exacte.

**Limites :**
- Applicable uniquement lorsque l'on dispose d'une formule fermée.

---

### 2. Méthode de Monte Carlo

Le prix de l'option est estimé à partir d'un grand nombre de trajectoires simulées :

\[
C_0 \approx e^{-rT}\frac{1}{N}
\sum_{i=1}^{N}
(S_T^{(i)}-K)^+
\]

**Avantages :**
- Très flexible ;
- Applicable aux produits complexes et aux modèles multidimensionnels.

**Limites :**
- Temps de calcul élevé ;
- Convergence relativement lente.

---

### 3. Méthode de Carr–Madan (FFT)

La méthode de Carr–Madan exploite la fonction caractéristique du logarithme du sous-jacent et la Transformée de Fourier Rapide (FFT) afin de calculer efficacement les prix d'options sur une grille de strikes.

**Avantages :**
- Très rapide pour le calcul simultané d'un grand nombre de prix ;
- Excellente efficacité numérique.

**Limites :**
- Principalement adaptée aux options européennes ;
- Extension multidimensionnelle coûteuse.

---

## Expériences numériques

Le notebook réalise plusieurs expériences.

### Comparaison des prix

Les prix obtenus par :

- Black–Scholes ;
- Monte Carlo ;
- Carr–Madan (FFT)

sont comparés sur une large plage de strikes.

### Comparaison des temps de calcul

Les temps d'exécution sont étudiés en fonction du nombre de strikes.

Les résultats observés montrent :

| Méthode | Complexité observée |
|----------|----------|
| Monte Carlo | \(O(N^2)\) |
| Carr–Madan FFT | \(O(N\log N)\) |

La méthode de Carr–Madan devient rapidement beaucoup plus performante lorsque le nombre de strikes augmente.

---

## Extension à plusieurs sous-jacents

Une section complémentaire étudie le comportement des méthodes lorsque l'option dépend de plusieurs actifs.

### Complexité de Carr–Madan

\[
O(N^d \log N)
\]

où \(d\) représente le nombre de sous-jacents.

### Complexité de Monte Carlo

\[
O(N_{sim}\times d)
\]

Les résultats montrent que :

- La FFT est extrêmement efficace en dimension 1 ;
- Son coût explose lorsque la dimension augmente ;
- Monte Carlo reste la méthode de référence en grande dimension.

Cette expérience illustre la malédiction de la dimension dans les méthodes basées sur la FFT multidimensionnelle.

---

## Principaux résultats

Pour une option européenne sur un seul sous-jacent :

- La formule de Black–Scholes fournit la référence exacte ;
- La méthode de Carr–Madan est significativement plus rapide que Monte Carlo ;
- La complexité observée est proche de \(O(N\log N)\) ;
- Monte Carlo présente une croissance beaucoup plus rapide du temps de calcul.

Pour plusieurs sous-jacents :

- La FFT multidimensionnelle devient rapidement impraticable ;
- Monte Carlo demeure l'approche privilégiée.

---

## Technologies utilisées

- Python
- NumPy
- SciPy
- Matplotlib
- Jupyter Notebook

---

## Structure du projet

```text
.
├── pricing_options.ipynb
└── README.md
```

---

## Références

- Black, F. & Scholes, M. (1973),
  *The Pricing of Options and Corporate Liabilities*

- Merton, R. (1973),
  *Theory of Rational Option Pricing*

- Carr, P. & Madan, D. (1999),
  *Option Valuation Using the Fast Fourier Transform*


