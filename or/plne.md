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
\max Z = 44 - \dfrac{1}{2} u_1 - 3 u_3 \\
s.t. \left|\begin{matrix}
x_1 & = & 8 &  & & - u_1 & & \\
u_2 & = & 2 &  & & - \dfrac{1}{2} u_1 & + u_3 & \\
x_2 & = & 4 &  & & + \dfrac{1}{2} u_1 & - u_3 & \\
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
\max Z = \alpha * (8 - u_1) + 3 * (4 + \dfrac{1}{2} u_1 - u_3) \\
s.t. \left|\begin{matrix}
x_1 & = & 8 &  & & - u_1 & & \\
u_2 & = & 2 &  & & - \dfrac{1}{2} u_1 & + u_3 & \\
x_2 & = & 4 &  & & + \dfrac{1}{2} u_1 & - u_3 & \\
\end{matrix}\right.
\end{matrix}

\Rightarrow

\begin{matrix}
\max Z = (\alpha * 8 + 12) + (-\alpha + 3/2) * u_1 - 3 * u_3 \\
s.t. \left|\begin{matrix}
x_1 & = & 8 &  & & - u_1 & & \\
u_2 & = & 2 &  & & - \dfrac{1}{2} u_1 & + u_3 & \\
x_2 & = & 4 &  & & + \dfrac{1}{2} u_1 & - u_3 & \\
\end{matrix}\right.
\end{matrix}
$$ 

Le PL reste stable tant que $(-\alpha + 3/2) \le 0 => 3/2 <= \alpha$.
Pour chaque augmentation d'alpha, l'objectif augmente de 8.

## Second membre

$$
Z = x_1 + 3 x2 \\
s.t. \left|\begin{matrix}
x_1 &   &      & \le & 8 + \alpha\\
    &   &  x_2 & \le & 6 \\
x_1 & + & 2x_2 & \le & 16 \\
\end{matrix}\right.
$$

En passant en forme standard: 

$$
Z = \ x_1 + 3 x2 \\
s.t. \left|\begin{matrix}
u_1 - \alpha & = & 8   & - & x_1 \\
u_2 & = & 6   &   &     & - &  x_2 \\
u_3 & = & 16  & - & x_1 & + & 2x_2 \\
\end{matrix}\right.
$$

En posant $\hat{U_1} = u_1 - \alpha$, le PL reste le même.
On a donc:

$$
\begin{matrix}
\max Z = 44 - \dfrac{1}{2} \hat{U_1} - 3 u_3 \\
s.t. \left|\begin{matrix}
x_1 & = & 8 & - & \hat{U_1} \\
u_2 & = & 2 & - & \dfrac{1}{2} \hat{U_1} & + u_3 \\
x_2 & = & 4 & + & \dfrac{1}{2} \hat{U_1} & - u_3 \\
\end{matrix}\right.
\end{matrix}

\Rightarrow

\begin{matrix}
\max Z = 44 - \dfrac{1}{2} (u_1 - \alpha) - 3 u_3 = (44 + \dfrac{1}{2} \alpha) - \dfrac{1}{2} u_1 - 3 u_3 \\
s.t. \left|\begin{matrix}
x_1 & = & 8 & - & (u_1 - \alpha)\\
u_2 & = & 2 & - & \dfrac{1}{2} (u_1 - \alpha) & + u_3 \\
x_2 & = & 4 & + & \dfrac{1}{2} (u_1 - \alpha) & - u_3 \\
\end{matrix}\right.
\end{matrix}
$$

Quand $\alpha$ augmente de 1, l'objectif augmente de 0.5. Le domaine de $\alpha$ se trouve avec les contraintes et en mettant les variables hors base à 0 :

$$
\begin{matrix}
\left|\begin{matrix}
8 & + \alpha & \ge & 0 \\
2 & + & \dfrac{1}{2} \alpha & \ge & 0 \\
4 & - & \dfrac{1}{2} \alpha & \ge & 0 \\
\end{matrix}\right.
\end{matrix}

\Rightarrow

-4 \le \alpha \le 8
$$

# Formulation problèmes courants

## Plus court chemin

## Max flow

## TSP

## pb du sac à dos

## bin packing

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

# Résolutions de problèmes difficiles

## Branch-and-bound / Branch-and-cut

L'algorithme "Branch-and-bound" est basée sur une stratégie "diviser pour régner" (divide and conquer). L'idée est de partitionner l'espace des solutions en sous-ensembles que l'on cherche à résoudre.

Considérons un problème de maximisation avec des variables entières.

On trouve une solution optimale en relachant les contraintes d'intégrité sur les variables
 * Si le PL n'a pas de solution alors on arrête l'évaluation de cette branche
 * Si la solution est entière => on peut s'arrêter. Il s'agit de la meilleure solution sur cette branche. Cela donne aussi une borne minimale au problème.
 * Si la valeur de la objective issue de la relaxation est inférieure à une solution acceptable du problème (respectant les contraintes d'intégrité), on arrête. On ne pourra pas trouver une solution encore meilleure que la solution acceptable.
 * Sinon, on choisit une variable et on subdivise l'espace en deux: x_i <= |x| et |x| >= x_i et on recommence. On peut remarque qu'en ajoutant ces contraintes, on exclue la solution trouvée précédemment.

Soit le PL suivant issu de https://web.mit.edu/15.053/www/AMP-Chapter-09.pdf: 

$$
\begin{matrix}
\max Z = 5 x_1 + 8 x_2 \\
s.t. \left|\begin{matrix}
x_1 & + x_2 & \le & 6 & (1)\\
5 x_1 & + 9 x_2 & \le & 45 & (2)\\
x_1 , & x_2 & \in & \mathbb{N} & (3)
\end{matrix}\right.
\end{matrix}
$$

* **Etape 0**: On relaxe les contraintes d'intégrité (3), on résoud le PL ce qui nous donne une valeur objective  $z_0 = 41.25$. La valeur de la fonction objective de la  meilleure solution faisable de ce PL est forcément inférieur à 41.
* **Etape 1**: On partitionne l'arbre en deux. On choisit d'évaluer L1.
* **Etape 2**: On partitionne l'arbre en deux. 
* **Etape 2.1**: On choisit d'évaluer L2. L2 n'est pas faisable, on arrête l'évaluation de la branche L2.
* **Etape 2.2**: On évalue L4. On partionnne, on évalue L5. La solution est entière, on a donc une borne minimale de notre fonction objective: $37 \le z \le 41$. On évalut L6. On trouve une solution entière et une nouvelle borne meilleure que la précédente:  $40 \le z \le 41$
* **Etape 3**: On évalue L2. La valeur de la solution optimale est inférieue à la borne précédente:  $39 \le 40 \le z \le 41$. On peut arrêter l'évaluation de L2.

Ce qui donne l'arbre suivant:

 ![Arbre d'exploration des solutions](branch-bound-tree.png)

## Génération de colonnes / Branch-and-price

## Relaxation Lagrangienne + gradient ou coupe de khelley

## Linéarisation

## 
 * Matrice totalement unimodulaire => Relaxation car meilleur solution forcément entière

# Divers

## TODO

 * Fonctions quadratiques (objectif)

## Démonstration

L'ensemble admissible du problème est un polyèdre convexe.

 _Chaque itération consiste à passer d'un sommet du polyèdre convexe à un sommet adjacent en suivant une arête de manière à faire décroître la fonction-coût._[wikipedia][wikipedia-simplex]

 [wikipedia-simplex]: https://fr.wikipedia.org/wiki/Algorithme_du_simplexe

Solution optimale du problème <=> point du polyèdre convexe

## Bibliographie et références

 * [RCP101](https://formation.cnam.fr/rechercher-par-discipline/recherche-operationnelle-et-aide-a-la-decision-208739.kjsp) du CNAM
 * [RPC104](https://formation.cnam.fr/rechercher-par-discipline/optimisation-en-informatique-208741.kjsp) du CNAM
 * Alain Billionnet : Optimisation discrète (Dunod)
 * Theorie des graphes
 * https://moodle.caseine.org/