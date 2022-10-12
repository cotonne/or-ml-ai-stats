# Programmation Linéaire

## Problème

### Définitions

 * z: fonction de coût que l'on cherche à minimiser/maximiser
 * 

### Forme canonique

$$
max z = \sum_{i = 1}^{n} c_i x_i \\
subject\ to : \mathit{A}x \le b
$$

Avec $\mathit{A} \in \mathbb{R}^{m \times n}$ et $b \in \mathbb{R}^n$

### Forme standard

Introduction des variables d'écart de m varia $u$

$$
max z = \sum_{i = 1}^{n} c_i x_i \\
subject\ to : \mathit{A}x + u = b
$$

Avec $u_j \ge 0$

### Variables en Base/Hors Base

 * n varibles hors base (VHB) = 0
 * m variables en base (VB) $\ne$ 0

$$
\max z = \boxed{4x_1 + 3x_2} VHB \\
s.t. \\
\boxed{
\left|\begin{matrix}
u_1 \\
u_2 \\
u_3 \\
VB \\
\end{matrix}\right.
}
\left.\begin{matrix}
 = &  8 & - & x_1 &   &     \\
 = &  6 &   &     & - & x_2 \\
 = & 15 & - & x_1 & - & x_2 \\
\end{matrix}\right.\\
x_1, x_2 \ge 0
$$

## Résolution avec le Simplexe

### Phase 1: Choix d'une base de départ / Solution initiale

#### Phase 1.1: Trouver une base de départ

Si pas de base évidente (exemple $\overrightarrow{0}$), on transforme/ré-écrit le problème pour en trouver une:

Exemple:
$$
\max z = 4x_1 + 2x_2 \\
s.t. \\
\left|\begin{matrix}
3x_1 & + & 2x_2 & \le & 12 \\
 x_1 &   &      & \ge &  3 \\
 x_1 & + & 2x_2 &  =  &  4 \\
\end{matrix}\right.\\
x_1, x_2 \ge 0
$$

 * Introduction des variables d'écarts
 * Introduction des variables artificielles
 * Nouvel objectif

$$
\min\ \psi = a_2 + a_3 \\
s.t. \\
\left|\begin{matrix}
3x_1 & + & 2x_2 & + & u_1 & = & 12 \\
 x_1 & - & u_2  & + & a_2 & = &  3 \\
 x_1 & + & 2x_2 & + & a_3 &=  &  4 \\
\end{matrix}\right.\\
x_1, x_2, u_1, u_2, a_2, a_3 \ge 0
$$

Objectif: $\psi = 0$ sinon, pas de base de départ/pas de solution.
Le résultat de ce PL est la base initiale.

#### Phase 1.2: ré-écriture du PL dans la nouvelle base

### Phase 2: Choix de la variable qui entre en base

 * Variable qui entre

$$\max z = 4 \boxed{x_1} + 3 x_2$$

x_1 est la variable la plus intéressante. Elle fait augmenter le plus la fonction objective.

 * Variable qui sort

$$
\left.\begin{matrix}
u_1 & = &  8 & - & x_1 & \ge & 0 & (1) \\
u_2 & = &  6 &   &     & \ge & 0 & (2) \\
u_3 & = & 15 & - & x_1 & \ge & 0 & (3) \\
\end{matrix}\right.\\
$$

L'équation (1) est la plus contraignante. $u_1$ entre en base.
On remplace $x_1$ par sa valeur issue de (1): $8 - u_1$.

$$
\max z = 4 * (8 - u_1) + 3 x_2 \\
\left.\begin{matrix}
x_1 & = &  8 & - & u_1 & \ge & 0 & (1) \\
u_2 & = &  6 &   &     & \ge & 0 & (2) \\
u_3 & = & 15 & - & x_1 & \ge & 0 & (3) \\
\end{matrix}\right.\\
$$

### Phase 3: arrêt?

Conditions d'arrêts:

 * Paramètres de la fonction objectif négatif
 * Boucle sur les variables entrant en base

### Phase 4: solution

Les variables hors base sont égales à 0. 
La fonction objective et les variables en base sont égales à la constante de leur équation.

# Dualité

## Formulation

A tout problème de maximisation P correspond un problème de minimisation D:

$$
max (P) = min (D) \\
Primal\ \ Dual \\
Var Primal = Contraintes Dual \\
Contraintes Primal = Var Dual
$$


$$
(P) \left\{\begin{matrix}
\max z = c x \\
s.t. : \mathit{A}x \le b
\end{matrix}\right.
\Leftrightarrow 
(D) \left\{\begin{matrix}
\min w = y \  b \\
s.t. : y \mathit{A} \ge c
\end{matrix}\right.
$$

## Cas général

$$
\begin{matrix}
min & max \\
Fonction\ objective & Second\ membre \\
Matrice\ de\ contraintes\ A & Matrice\ de\ contraintes\ A^t \\
x_i \ge 0 & Contrainte\ i\ de\ type\ \le \\
x_i \le 0 & Contrainte\ i\ de\ type\ \ge \\
x_i \in \mathbb{R} & Contrainte\ i\ de\ type\ = \\
Contrainte\ i\ \le, \ge ou = & y_i \ge 0, \le 0\ ou \in \mathbb{R} \\
x_i\ en\ base & y_{\hat{j}}\ hors\ base \\
\end{matrix}
$$

## Ecarts complémentaires

Si $\hat{x}$ est une solution admissible de (P) et $\hat{y}$, une solution de (D), alors:

$$
\left|
\begin{matrix}
\hat{x_i} & \times & (\sum \hat{y_j} a_{ij} - c_j) & = & 0 \\
\hat{y_j} & \times & (b_i - \sum a_{ij} \hat{x_i}) & = & 0
\end{matrix}
\right.
$$

On retrouve les solutions du primal à partir du dual.

# Analyse en sensibilité

L'analyse en sensibilité a pour but d'étudier l'évolution de la solution lorsque l'on fait varier la solution optimale.

## Définitions

###  Coût marginal

> Augmentation minimale de dépenses, par rapport à la solution optimale, qui résulterait de l’utilisation d’une unité supplémentaire de ce bien, lorsque le problème posé consiste à produire des biens au moindre coût [source](https://www.cours-et-exercices.com/2016/03/dualite-et-analyse-de-sensibilite-cours.html#Heading3)

## PL exemple

$$
\begin{matrix}
\max Z = 4 x_1 + 3 x_2 \\
s.t. \left|\begin{matrix}
x_1 &   &      & \le & 8 \\
    &   &  x_2 & \le & 6 \\
x_1 & + & 2x_2 & \le & 16 \\
\end{matrix}\right.
\end{matrix}

\Rightarrow


\begin{matrix}
\max Z = 44 - 1/2 u_1 - 3 u_3 \\
s.t. \left|\begin{matrix}
x_1 & = & 8 &  & & - u_1 & & \\
u_2 & = & 2 &  & & - 1/2 u_1 & + u_3 & \\
x_2 & = & 4 &  & & + 1/2 u_1 & - u_3 & \\
\end{matrix}\right.
\end{matrix}
$$ 


## Fonction Objective

On rremplace le paramètre C pour la variable $x_1$ par $\alpha$ : 
$$
Z_\alpha = \alpha\ x_1 + 3 x2 \\
s.t. \left|\begin{matrix}
x_1 &   &      & \le & 8 \\
    &   &  x_2 & \le & 6 \\
x_1 & + & 2x_2 & \le & 16 \\
\end{matrix}\right.
$$
avec $\alpha \in \mathbb{R}$

Comme le résultat du PL ne doit pas changer, on a les mêmes variables hors base et en base. On remplace donc $x_1$ par sa valeur: 

$$
\begin{matrix}
\max Z = \alpha * (8 - u_1) + 3 * (4 + 1/2 u_1 - u_3) \\
s.t. \left|\begin{matrix}
x_1 & = & 8 &  & & - u_1 & & \\
u_2 & = & 2 &  & & - 1/2 u_1 & + u_3 & \\
x_2 & = & 4 &  & & + 1/2 u_1 & - u_3 & \\
\end{matrix}\right.
\end{matrix}

\Rightarrow

\begin{matrix}
\max Z = (\alpha * 8 + 12) + (-\alpha + 3/2) * u_1 - 3 * u_3 \\
s.t. \left|\begin{matrix}
x_1 & = & 8 &  & & - u_1 & & \\
u_2 & = & 2 &  & & - 1/2 u_1 & + u_3 & \\
x_2 & = & 4 &  & & + 1/2 u_1 & - u_3 & \\
\end{matrix}\right.
\end{matrix}
$$ 

Le PL reste stable tant que $(-\alpha + 3/2) \le 0 => 3/2 <= \alpha$.
Pour chaque augmentation d'alpha, l'objectif augmente de 8.

## Second membre

# Divers

## Résoudre le problème

```python
import pyomo.environ as pyo 

m    = pyo.ConcreteModel()
m.x  = pyo.Var([1,2], domain=pyo.NonNegativeReals)
m.z  = pyo.Objective(expr = 4 * m.x[1] + 3 * m.x[2], sense=pyo.maximize)
m.c1 = pyo.Constraint(expr = m.x[1] <= 8)
m.c2 = pyo.Constraint(expr = m.x[2] <= 6)
m.c3 = pyo.Constraint(expr = m.x[1] + 2 * m.x[2] <= 16)

opt = pyo.SolverFactory('cbc')
results = opt.solve(m)

from pyomo.opt import SolverStatus, TerminationCondition
if results.solver.status == SolverStatus.ok and results.solver.termination_condition == SolverStatus.OK:
    print(f"x1 = {m.x[1].value}, x2 = {m.x[2].value}")
```

## TODO

 * Branch-and-cut
 * Branch-and-bound
 * Branch-and-price
 * Lagrangien + gradient ou coupe de khelley
 * Génération de colonne
 * Formulation problèmes
 * Linéarisation
 * Fonctions quadratiques

## Démonstration

L'ensemble admissible du problème est un polyèdre convexe.

 _Chaque itération consiste à passer d'un sommet du polyèdre convexe à un sommet adjacent en suivant une arête de manière à faire décroître la fonction-coût._[wikipedia][wikipedia-simplex]

 [wikipedia-simplex]: https://fr.wikipedia.org/wiki/Algorithme_du_simplexe

# Bibliographie

 * Livre Alain Billionet
 * Theorie des graphes