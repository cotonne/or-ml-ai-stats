# Lagrangian

## Description

$$
\max z = c^T x \\
s.t.\\
\quad Ax \leq b
$$

peut être écrit sous la forme:

$$
\max z^L = c^T x  + \lambda^T (b - Ax)\\
s.t.\\
\lambda \geq 0
$$

$\lambda$ est une pénalité de non-respect de la contrainte.
Les multiplicateurs de Lagrange sont les variables duales pour le NLP.

La fonction $z^L$ est convexe avec $\lambda \in \mathbb{R^+}$.
Un primal non-convexe deviendra convexe avec la Relaxation Lagrangienne.

## Dualité faible

> $z^* \leq z^L(\lambda)$

**Preuve**:

$$
\begin{matrix}
z^* & = & max_x \{f(x) / g_i(x) \leq b_i, \forall i\} & \\
    & = & max_x \{f(x) + \lambda_i [b_i - g_i(x)]/ g_i(x) \leq b_i, \forall i\} & (1) \\
    & = & max_x \{f(x) + \lambda_i [b_i - g_i(x)]\} & (2) 
\end{matrix}
$$

 - (1): $\lambda_i \geq 0$ et $b_i - g_i(x) \geq 0$ donc $\lambda_i [b_i - g_i(x)] \geq 0$
 - (2): On retire des contraintes, on relaxe le problème, on augmente la région faisable. La valeur optimale est donc meilleure

## Conditions KKT (Génération de la relaxation Lagrangienne)

Pour un Programme Non Linéaire "[normal](#constraint_qualification)":

$$
\max_x f(x)
s.t\\
g_i(x) \leq b
$$

Si $x^*$ est un maximum local, alors, il existe $\lambda$ tel que:

 - (1) **Primal feasibility** : $g_i(x^*) \leq b_i$
 - (2) **Dual feasibility** : $\lambda \geq 0\ \text{and}\ \nabla f(x^*) = \sum \lambda_i \nabla g_i(x^*)$

**First Order Condition of the Lagrangrian** $\mathcal{L}(x^*/\lambda)$:

Stationnarité: $\nabla \mathcal{L}(x^*/\lambda) = \nabla \{ f(x^*) + \sum \lambda_i (b_i - g_i(x^*))\} = 0$, définition d'un maximum

 - (3) Complementary Slackness: $\lambda_i [b_i - g_i(x^*)] = 0$

Les conditions KKT sont des conditions nécessaires (mais pas suffisantes) pour un maximum local.
En trouvant tous les minimums locaux, on trouve le maximum global

### Exemples KKT

#### Exemple 1

$$
\max_x f(x) = x_1 - x_2 \\
s.t\\
x_1^2 + x_2^2 \leq 4 \\
-x_1^2 - (x_2+2)^2 \leq -4 \\
$$

Condition KKT (2) $\lambda \geq 0\ \text{and}\ \nabla f(x^*) = \sum \lambda_i \nabla g_i(x^*)$ avec:

 - $\nabla f(x) = \begin{pmatrix} 1 \\ -1 \end{pmatrix}$
 - $\nabla \lambda [b - g(x)] = \lambda_1 \begin{pmatrix} 2 x_1 \\ 2x_2 \end{pmatrix} + \lambda_2 \begin{pmatrix} -2 x_1 \\ -2x_2 + 4 \end{pmatrix} $

Condition KKT (3): $\lambda_i [b_i - g_i(x^*)] = 0

 Ce qui donne:

$\begin{pmatrix} 
2 \lambda_1 x_1 - 2 \lambda_2 x_2  \\ 
2 \lambda_1 x_2 - 2 \lambda_2 x_2 + 4 \\
\lambda_1 [4 - x_1^2 - x_2^2] \\
\lambda_1 [-4 + x_1^2 + (x_2 + 2)^2]
\end{pmatrix} =  \begin{pmatrix} 1 \\ -1 \\ 0 \\ 0\end{pmatrix}$

## Dualité Lagrangienne vs. Dualité PL

La dualité PL est un cas spécial de la dualité Lagrangienne

Soit: 
$$
\max z = c^T x \\
s.t.\\
\quad Ax = b
$$

Le primal lagrangien est: 
$z^*(\lambda) = \max_x \underbrace{c^Tx}_{\text{Orignal objective}} + \lambda^T(b-Ax) = \lambda^T b + \max_x (c^T - \lambda^TA) x$

Le dual lagrangien est: 
$\min_\lambda z^L(\lambda) = \min_\lambda \{ \lambda^T b + \max_x \underbrace{(c^T - \lambda^TA)}_{(1)} x \}$

(1): Cela a du sens seulement si $c^T \leq \lambda^T A$. 
Si $c^T \geq \lambda^T A \Rightarrow c^T - \lambda^T A \geq 0$, on peut choisir x infini pour maximiser le primal.
La solution est alors non bornée.

Donc $c^T - \lambda^T A \leq 0 \Rightarrow \max_x (c^T - \lambda^T A)x = 0 \Rightarrow \min_\lambda z^L(\lambda) = \underbrace{\min_\lambda \lambda^T b,\ s.t.\ \lambda^T A \geq c^T}_{\text{Dual PL}}$

## Dualité forte

Pour un Programme Non Linéaire convexe "[normal][constraint_qualification]":

Références:

 - https://web.stanford.edu/~boyd/cvxbook/


[constraint_qualification]: Constraints qualification: https://en.wikipedia.org/wiki/Slater%27s_condition  sufficient condition for strong duality to hold for a convex optimization problem,

