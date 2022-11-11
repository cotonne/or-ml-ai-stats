 * Feature extraction
 * Data augmentation
 * Missing data (mean/avg/MissMDA/MissForest/)
 * Données aberrantes (outliers), boxplot
 * Malédiction des dimensions (méthodes basées sur la densité inutile, toutes les données finissent par être à la même distance, volume utile)

 https://www.math.univ-toulouse.fr/~besse/Wikistat/pdf/st-m-app-idm.pdf

# Données manquantes

## Types de données manquantes

  - Données manquantes de façon complètement aléatoire (**MCAR** : Missing completly At Random)
  - Données manquantes de façon aléatoire (**MAR** : Missing At Random). Exemple: les notes de rattrapage n'existent pas selon la réussite à l'examen principal.
  - Données manquantes de façon non aléatoires (**MNAR** : Missing Not At Random). Exemple: refus de répondre. Relier à des données non observées.

## Traitement

### Solution 1: Supprimer les données

 - MCAR: ne biaise pas le résultat. Mais perte d'information pour le modèle
 - MAR: biaise le résultat. Imputer les données manquante
 - MNAR: biaise le résultat. Imputation difficile à justifier

 On peut peut pas savoir si on est dans le cas MAR ou MNAR

###  Solution 2: Imputer les données

 - Valeur unique: moyenne, médiane, valeur la plus fréquente.... => baisse de la variance
 - Centre de groupes
    - Détecter les groupes / Classification
    - Imputer les groupes en utilisant une distance partielle
 - k plus proches voisins
 - SVD

Outils: 
 - [sklearn](https://scikit-learn.org/stable/modules/impute.html)
 - MissForest, MissMDA