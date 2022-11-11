# K-Means

## Objectif

Répartir N données en k groupes disjoints, avec k inconnu a priori, en minimisant la somme des inerties intra-classes.

$$
\left.\begin{matrix}
inertie & = & \frac {1} {n} \sum d^2(e_i, g) \\
        & = & \underbrace{\frac {1} {n} \sum_{i=1}^k n_i d^2(g_i, g)}_{intertie\ interclasse} 
            + \underbrace{\frac {1} {n} \sum_{i=1}^k \sum_{e \in G_i} d^2(e, g_i)}_{intertie\ intraclasse} \\
\end{matrix}\right.
$$

## Algorithmes

### Centres mobiles

 0. Initialisation des k centres (positions aléatoires)
 1. Affectation des données au groupe du centre le plus proche
 2. Recalcul et replacement du centre 
 3. Reprendre à l'étape 1 jusquà dépassement de la condition (nombre d'itérations max atteinte, variations de l'inertie inter/intra faible ($\le \epsilon$)

### K-Means

 - Variante stochastique, online
 - A chaque itération, choisir une seule donnée aléatoirement. Si elle change de groupe, on recalcule les centres

### K-Means++

Lors de l'initialisation des centres, il est possible d'avoir des centres proches.

Pour éviter cela, à l'intialisation, K-Means++ positionne les centres les uns après les autres suivant une loi uniforme qui privilégie les candidats éloignés des centres déjà existants.

Cette méthode permet de créer des centres éloignés les uns des autres tout en les plaçant proches des données denses.

### K-Medoïd

Traiter des données quelconques (non vectorielles) pour lesquelles une métrique existe

## TODO

 - Avantages/Incovénients (complexité/explicabilité)

 - Simple à comprendre, à expliquer
 - Fragile face au
 - 