# Pricing d'options européennes : Black–Scholes, Monte Carlo et FFT de Carr–Madan

## Présentation

Ce projet compare plusieurs méthodes de valorisation d'options européennes dans le cadre du modèle de Black–Scholes :

1. Formule analytique de Black–Scholes
2. Simulation de Monte Carlo
3. Méthode de Carr–Madan utilisant la Transformée de Fourier Rapide (FFT)

L'objectif est d'étudier à la fois la précision numérique et la complexité algorithmique de ces différentes approches.

---

## Contexte mathématique

Sous la mesure risque-neutre, le prix d'un call européen est donné par :

$$
C_0 = e^{-rT}\mathbb{E}\left[(S_T-K)^+\right]
$$

où :

- $S_T$ : prix du sous-jacent à maturité ;
- $K$ : prix d'exercice (strike) ;
- $r$ : taux sans risque ;
- $T$ : maturité ;
- $\sigma$ : volatilité.

Dans le modèle de Black–Scholes, le sous-jacent suit :

$$
dS_t = rS_t\,dt + \sigma S_t\,dW_t.
$$

---

## Méthodes implémentées

### 1. Formule analytique de Black–Scholes

Cette méthode fournit la valeur exacte de référence dans le cadre du modèle de Black–Scholes.

**Avantages**

- Calcul instantané ;
- Solution exacte.

**Limites**

- Applicable uniquement lorsque l'on dispose d'une formule fermée.

---

### 2. Méthode de Monte Carlo

Le prix de l'option est estimé par :

$$
C_0 \approx e^{-rT}
\frac{1}{N}
\sum_{i=1}^{N}
\left(S_T^{(i)}-K\right)^+.
$$

**Avantages**

- Très flexible ;
- Applicable aux produits complexes ;
- Utilisable en grande dimension.

**Limites**

- Temps de calcul élevé ;
- Convergence lente.

---

### 3. Méthode de Carr–Madan (FFT)

La méthode de Carr–Madan exploite la fonction caractéristique du logarithme du sous-jacent ainsi que la Transformée de Fourier Rapide (FFT) afin de calculer efficacement une grille complète de prix d'options.

**Avantages**

- Très rapide pour un grand nombre de strikes ;
- Excellente efficacité numérique.

**Limites**

- Principalement adaptée aux options européennes ;
- Extension multidimensionnelle coûteuse.

---

## Expériences numériques

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
| Monte Carlo | $O(N^2)$ |
| Carr–Madan FFT | $O(N\log N)$ |

La méthode de Carr–Madan devient rapidement beaucoup plus performante lorsque le nombre de strikes augmente.

---

## Extension à plusieurs sous-jacents

Une section complémentaire étudie le comportement des méthodes lorsque l'option dépend de plusieurs actifs.

### Complexité de Carr–Madan

$$
O\!\left(N^d\log N\right)
$$

où $d$ représente le nombre de sous-jacents.

### Complexité de Monte Carlo

$$
O\!\left(N_{\text{sim}}\,d\right)
$$

Les résultats montrent que :

- la FFT est extrêmement efficace en dimension 1 ;
- son coût explose lorsque la dimension augmente ;
- Monte Carlo reste la méthode de référence en grande dimension.

Cette expérience illustre la **malédiction de la dimension** pour les méthodes basées sur la FFT multidimensionnelle.

---

## Principaux résultats

Pour une option européenne sur un seul sous-jacent :

- la formule de Black–Scholes fournit la référence exacte ;
- la méthode de Carr–Madan est significativement plus rapide que Monte Carlo ;
- la complexité observée est proche de $O(N\log N)$ ;
- Monte Carlo présente une croissance beaucoup plus rapide du temps de calcul.

Pour plusieurs sous-jacents :

- la FFT multidimensionnelle devient rapidement impraticable ;
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

1. Black, F. & Scholes, M. (1973),
   *The Pricing of Options and Corporate Liabilities*

2. Merton, R. (1973),
   *Theory of Rational Option Pricing*

3. Carr, P. & Madan, D. (1999),
   *Option Valuation Using the Fast Fourier Transform*

---

## Auteur

**Félix Mayoussier**

Étudiant en Licence de Mathématiques à Sorbonne Université.

Projet personnel réalisé dans le cadre de mon apprentissage de la finance quantitative, avec un intérêt particulier pour la valorisation numérique des produits dérivés, les probabilités et les méthodes de calcul scientifique.
