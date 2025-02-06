# 3D-Graph

1. **Initialiser le graphe G** comme un graphe orienté
2. **Ajouter tous les waypoints** en tant que noeuds avec des altitudes fixes
3. **Ajouter tous les thermals** en tant que noeuds avec des altitudes aléatoires plus basses
4. **Pour chaque noeud i dans le graphe** :
   a. **Pour chaque noeud j dans le graphe** :
      i. **Si i ≠ j** :
         - **Calculer la distance** entre i et j dans le plan (x, y)
         - **Calculer la différence d'altitude** (z)
         - **Déterminer le coût énergétique** :
           * **Si altitude(j) < altitude(i)** : coût réduit (**descente avantageuse**)
           * **Sinon** : coût augmenté (**montée énergivore**)
         - **Ajouter une arête dirigée entre i et j** avec le poids calculé
5. **Initialiser une liste `dist`** avec des valeurs infinies pour tous les noeuds sauf le point de départ `start` (distance 0)
6. **Initialiser une file de priorité `queue`** avec `(0, start)`
7. **Tant que la file `queue` n'est pas vide** :
   a. **Extraire le noeud `u` avec la plus petite distance**
   b. **Pour chaque voisin `v` de `u`** :
      i. **Calculer le coût temporaire `new_cost = dist[u] + poids(u, v)`**
      ii. **Si `new_cost < dist[v]`** :
         - **Mettre à jour `dist[v]`**
         - **Mettre à jour le prédécesseur de `v`**
         - **Ajouter `(new_cost, v)` dans la file `queue`**
8. **Construire `optimal_path` en retraçant les prédécesseurs** depuis `end` jusqu'à `start`
9. **Retourner `optimal_path` et `total_cost`**
