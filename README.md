# TP Algorithmique : Recherche de Plus Court Chemin

Ce projet a pour objectif d’implémenter et de comparer deux algorithmes majeurs de recherche de chemin (pathfinding) sur une grille pondérée : **Dijkstra** et **A***.

L’application lit une carte, construit un graphe connexe et permet à l’utilisateur de visualiser le chemin optimal entre un point de départ et une arrivée, tout en analysant les performances de l’algorithme choisi.

---

## Fonctionnalités principales

### Lecture de fichier de configuration

Importation des données depuis un fichier **graph.txt** : dimensions, types de terrains, définition de la grille, coordonnées de départ et d’arrivée.

### Graphe pondéré

Gestion d’une carte sous forme de grille avec une connexité de **8 voisins** (déplacements horizontaux, verticaux et diagonaux).

### Poids dynamiques

Calcul du coût de déplacement prenant en compte la nature du terrain et la distance physique.

### Comparaison d’algorithmes

* **Dijkstra** : recherche exhaustive garantissant le chemin optimal.
* **A*** : recherche heuristique optimisée pour réduire le nombre de nœuds explorés.

### Métriques

Affichage du temps de calcul et du nombre total de nœuds visités.

---

## Détails d’implémentation

### 1. Calcul des poids des arêtes

Le poids d’une arête entre deux cases A et B est donné par :

```
Poids = ((Cout_A + Cout_B) / 2) * Facteur_Distance
```

* **Cout_A / Cout_B** : coût de traversée selon le type de terrain (ex : Herbe = 1, Eau = 1000).
* **Facteur_Distance** :

  * `1.0` pour un déplacement cardinal
  * `1.414` (racine de 2) pour un déplacement diagonal

### 2. Heuristique A*

Les déplacements diagonaux étant autorisés, A* utilise la **Distance de Chebyshev** :

```
h(v) = max(|x_fin - x_actuel|, |y_fin - y_actuel|)
```

Cette heuristique est admissible et permet à A* de rester optimal tout en ciblant la destination de manière efficace.

---

## Utilisation

1. Placer le fichier **graph.txt** à la racine du projet Java.
2. Exécuter la classe contenant la méthode `main`.
3. Choisir l’algorithme via la console :

   * Entrer `1` pour Dijkstra
   * Entrer `2` pour A*

Le programme affiche :

* La progression graphique dans une fenêtre
* Le temps d’exécution
* Le nombre de nœuds explorés

Le chemin final (suite d'indices) est sauvegardé dans **out.txt**.

---

## Résultats

Les tests montrent que **A*** trouve un chemin de coût identique à celui de Dijkstra (optimalité), tout en explorant généralement moins de nœuds, ce qui le rend plus efficace sur les cartes de grande taille.

