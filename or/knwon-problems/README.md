# Formulation problèmes courants

## Problème du sac à dos

L'objet i a les propriétés suivantes:

 - Un poids $w_i$
 - Un coût $c_i$
 - Un variable $x_i$ qui vaut 1 si l'objet est chargé.

On cherche à maximiser la coût d'objets chargés dans le sac à dos sans dépasser la capacité C du sca.

$$
\max z = \sum x_{i} c_{i} \\
s.t. 
\sum x_{i}  w_{i} \le c \\
$$

## Max flow

$$
\max z = \sum x_{ij} \times w_{ij} \\
s.t. 
\sum f_{ij} = \sum f_{ji}, \forall v \in \mathbb{V} - \{s, t\} \ (1)
$$

La contrainte (1) est la règle de conservation des flux.

## Plus court chemin

Plus court chemin pour aller du noeud s au noeud t

$$
\min z = \sum x_{ij} \times w_{ij} \\
s.t. 
 \left|\begin{matrix}
 \sum x_{ij} & - & \sum x_{ks} & = & 0 & (1)\\ 
 \sum x_{si} & - & \sum x_{is} & = & 1 \\ 
 \sum x_{ti} & - & \sum x_{it} & = & -1 \\ 
\end{matrix}\right.
$$

On modélise le plus court chemin comme un problème de flot max avec un flux égal à 1.

## Bin packing

**Objectif**: ranger les objets dans un minimum de boites

Soit les variables suivantes:
 
  - $x_i$ égal à 1 si la boite i est utilisé.
  - $y_{ij}$ égal à 1 si l'objet j est dans la boite i

Soit les paramètres suivants:

  - $c_j$, le coût de l'objet j
  - $C_i$, la capacité d'un boite i

$$
\min z = \sum x_i \\
s.t. 
 \left|\begin{matrix}
 \sum y_{ij} c_j & \le & C_i & \forall i & (1)\\ 
 \sum y_{ij} & \le & x_i & \forall i & (2) \\
 \sum y_{ij} & = & 1 & \forall j & (3) \\
\end{matrix}\right.
$$

Contraintes:

 - L'inégalité 1 assure qu'il n'y a pas plus d'objets que la boite peut contenir
 - L'inégalité 2 assure que, si la boite contient un objet, alors $x_i$ vaut 1
 - L'inégalité 3 assure que tous les objets sont bien placés dans une boite


## TSP

$$
\min z = \sum c_{ij} x_{ij} \\
s.t. 
 \left|\begin{matrix}
 \sum_{i=1}^N x_{ij} & = 1 & \forall j & (1)\\ 
 \sum_{j=1}^N x_{ij} & = 1 & \forall j & (2)\\ 

 t_1 = 1 (3) \\ 
 2 \le u_i \le n (3) \\
 t_i - B(1 - x_{ij}) & \le t_j & \forall i,j & (3)\\ 
 
 \sum_{(i,j) \in E} x_{ij} & \le |S| - 1 & \forall S \in V, V \ne S & (3')\\ 
\
end{matrix}\right.
$$

Contraintes:
 - Les contraintes (1) et (2) assurent que tous les neouds sont visités une fois (on utilise un arc pour entrée et un pour sortir)
  - Pour éliminer les sous-tours, on a le choix avec une des deux contraintes
    * (3) : Miller, Tucker, Zemlin: on ajoute une contrainte temporelle (B est une valeur très grande). Pareil que $u_i - u_j + 1 \le (n-1)(1-x_{ij})$? Si $x_{ij} = 0$, il n'y a pas de contrainte entre $u_i$ et $u_j$. Sinon $u_j$ doit être plus grand que $_ui$ d'au moins 1.
    * (3') : Dantzig, Fulkerson, Jhonson: Quel que soit un sous-graphe de G, les liens utilisés forment une chaîne.

Pour la contrainte (3') Cependant, on a $2^{|S|}$ parties possibles, rendant ce modèle non compact. Pour résoudre ce problème, on peut utiliser une approche itérative

 0. Créer le problème avec (1) et (2)
 1. Résoudre le problème
 1. Si le problème ne contient pas de des sous-tours, retourner le résultat
 2. Si le problème contient des des sous-tours, ajouter une contrainte (3') pour empêcher le sous-tour
 3. Retourner à 1

Réf:

 - [Exemple d'implémentation](https://medium.com/swlh/techniques-for-subtour-elimination-in-traveling-salesman-problem-theory-and-implementation-in-71942e0baf0c)
 - Capacitated Multitrip Vehicle-Routing Problem With Time Window
 - Multi-depot vehicle routing problem

## Location facility

Minimiser le coût d'installation des entrepôts

Paramètres:

 - $d_i$: coût d'installation de l'entrepôt sur le site i
 - $c_{ij}$: coût pour livrer le client j depuis le site i

Variables:

 - $x_i$: égale à 1 si l'entrepôt est placé sur le site i
 - $y_{ij}$: égale à 1 si l'u

$$
\min \sum_i \sum_j c_{ij} y_{ij} + \sum_j d_i x_i \\
s.t. \\
\sum_i y_{ij} = 1 \forall j (1) \\
\sum_j y_ij \lt x_i \forall i (2)
$$

Contraintes:

 - (1): assure que tous les clients sont servis
 - (2): si $y_{ij}$ alors $x_i$ - si le client j est servi par l'entrepôt i, alors l'entrepôt est installé en i

## Minimize makespan on parallel machines

On a j objets à produire sur i machines. Chaque objet prend p_j minutes à produire.

$x_{ij} = 1$ si l'objet j est associé à la machine j

On cherche à minimiser la fin du traitement w.

$$
\min w \\
s.t.\\
w >= \sum p_j x_{ij} \forall i \in I (1)\\
\sum x_{ij} = 1 \forall j \in J (2)\\
$$

La contrainte (1) contraint la durée w à être supérieure à la machine avec le plus long fonctionnement.
La contrainte (2) assure qu'un objet est produit une fois par une machine.


# TODO:
 - (U(C))-VRP
 - Knapsack
 - Lot-sizing