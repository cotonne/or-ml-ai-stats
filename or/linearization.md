## Linéarisation

### min d'une fonction max:

$min max {x_i}$ devient:

$$
min w \\
s.t. w \ge x_i \forall i
$$

**Exemple**: minimisrer la distance de Manhattan $min \sum ([x - x_i| + -|y - y_i|)$
devient:

$$
min \sum (u_i + v_i) \\
s.t.\\
u_i \ge x - x_i \\
u_i \ge x_i - x \\
v_i \ge y - y_i \\
v_i \ge y_i - y \\
$$

### Produit de deux variables binaires

Un objectif de type $max xy$ peut peut être linéarisé en introduisant une variable $z = xy$

$$
max z
z \le x \\
z \le y \\
$$

L'objectif va forcer z à être maximal.

Une contrainte xy peut être linéarisé en introduisant une variable $z = xy$:

$$
z \le x \\
z \le y \\
x + y - 1 \le z \ (1) \\
$$

La contrainte (1) peut être ignoré si on a une contrainte du type $a \le xy$.

### Abs dans une contrainte

Une contrainte $x \ge |A|$ peut être linéarisé par:

$$
x \ge A \\
x \ge -A
$$

Une valeur absolue peut être écrire sous la forme : |A| = max{-A, A}

### Abs dans un objectif

Un objectif $min |A|$ devient:

$$
min w \\
s.t. w \ge |A|
$$

### Max / Min

Une contrainte $x \ge max(A, B)$ peut être linéarisé par:

$$
x \ge A \\
x \ge B
$$

Une contrainte $x \le max(A, B)$ peut être linéarisé en écrivant $x \le min(A, B) + |A - B|$:

$$
x \le A + S^- + S^+ \\
x \le B + S^- + S^+ \\
S^- \ge B - A \\
S^+ \ge A - B \\
x \ge B
$$

Only one of the $S^-/S^+$ will be different from 0.

Inverse for min

### References

 - https://www.leandro-coelho.com/how-to-linearize-max-min-and-abs-functions/
 - https://yetanothermathprogrammingconsultant.blogspot.com/2016/02/xor-as-linear-inequalities.html

### Deux contraintes à satisfaire

Soit deux contraintes:

 * f(x) <= b1 (1)
 * g(x) <= b2 (2)

On veut satisfaire une des deux contraintes uniquements.

On définit une variable binaire z qui vaut 0 si la contrainte 1 est sélectionné, 1 si c'est la contrainte 2 qui est choisie.

On choisit un grand M et on remplace les contraintes par:

 * f(x) - b1 <= M * z
 * g(x) - b2 <= M * (1 - z)

### Deux contraintes parmi 3 à satisfaire

Soit trois contraintes de la forme f_i(x) <= b_i

On veut satisfaire une des deux contraintes uniquements.

On définit une variable binaire z_i qui vaut 0 si la contrainte i est sélectionné, 0 sinon

On choisit un grand M et on remplace les contraintes par:

 * f_i(x) - b_i <= M * z_i pour chaque i
 * z_1 + z_2 + Z_3 >= 2

