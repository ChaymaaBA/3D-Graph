Pseudo-code : **Modélisation du Graphe et Recherche du Chemin Optimal**

**Entrées :**
- **Waypoints** : Liste de points **(x, y, z)** formant une grille régulière.
- **Thermaux** : Liste de points **(x, y, z)** avec des altitudes variables.
- **Start** : Point de départ **(x, y, z)**.
- **End** : Point d’arrivée **(x, y, z)**.

**Sorties :**
- **Chemin optimal** : Séquence de nœuds **(x, y, z)**.
- **Coût total du trajet**.

---

### **1. Initialisation du Graphe**
- **Créer un graphe dirigé G.**
- **Ajouter tous les waypoints et thermaux comme nœuds dans G.**
- **Pour chaque waypoint w, ajouter w à G.**
- **Pour chaque thermique t, ajouter t à G.**

---

### **2. Création des Connexions entre les Nœuds**
**Pour chaque nœud i dans G :**
   - **Pour chaque nœud j dans G :**
       - **Si i ≠ j :**
           - **Calculer la distance Euclidienne** `dist(i, j)`.
           - **Calculer la différence d’altitude** `altitude_diff = zi - zj`.
           - **Définir le poids de l’arc :**
               - **Si altitude_diff > 0** → `coût = dist * 0.5` (**descente avantageuse**).
               - **Sinon** → `coût = dist * 2` (**montée coûteuse**).
           - **Ajouter un arc dirigé** `(i → j)` avec le poids.

---

### **3. Algorithme de Recherche du Chemin Optimal (Dijkstra)**
1. **Initialiser une file de priorité P contenant** `(coût = 0, start)`.
2. **Créer un dictionnaire `dist`** avec tous les nœuds mis à **∞** sauf **start = 0**.
3. **Créer un dictionnaire `prédécesseur`** pour stocker le chemin optimal.

4. **Tant que P n’est pas vide :**
   - **Extraire le nœud u avec le plus petit coût.**
   - **Si u == end**, alors **reconstruire et retourner le chemin**.
   - **Pour chaque voisin v de u :**
       - **Calculer le coût total** `c = coût(u) + poids(u, v)`.
       - **Si c < dist[v] :**
           - **Mettre à jour** `dist[v] = c`.
           - **Mettre à jour** `prédécesseur[v] = u`.
           - **Ajouter v à la file de priorité P**.

**Si aucun chemin trouvé, retourner** `"Pas de chemin disponible"`.

---

### **4. Reconstruction du Chemin Optimal**
1. **Initialiser une liste** `chemin = [end]`.
2. **Tant que prédécesseur[end] existe :**
   - **Ajouter prédécesseur[end] au chemin.**
   - **Mettre à jour** `end = prédécesseur[end]`.
3. **Inverser `chemin` et le retourner**.

---

### **Conclusion**
- **Ce pseudo-code modélise un graphe** où chaque **waypoint** est connecté aux **voisins proches** et où chaque **thermique est relié aux waypoints les plus proches**.
- **L’algorithme utilisé est Dijkstra**, qui **garantit le chemin le moins coûteux en énergie**.
- **Il est possible d’améliorer cette approche en :**
  - **Priorisant les waypoints et utilisant les thermaux uniquement si cela réduit le coût.**

