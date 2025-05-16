**RL-DQN**
==========

Ce dépôt contient une implémentation de l'algorithme Deep Q-Learning (DQN) pour entraîner des agents à naviguer dans un labyrinthe en grille. Trois agents différents sont implémentés, chacun avec des comportements spécifiques.

**Structure du Dépôt**
----------------------

Le dépôt est structuré comme suit :

*   rl-dqn-game.ipynb : Ce fichier contient le code pour l'environnement du labyrinthe et l'implémentation des trois agents DQN.
    
*   rl-dqn-main.ipynb : Ce fichier est utilisé pour charger et exécuter des simulations avec plusieurs agents simultanément.
    

**Agents DQN**
--------------

Trois agents DQN distincts sont implémentés dans rl-dqn-game.py :

1.  **Agent destructeur de tours**: Cet agent est entraîné pour apprendre à casser les tours du labyrinthe afin d'atteindre plus facilement sa destination.
    
2.  **Agent éviteur de tours**: Cet agent est entraîné pour apprendre à éviter les tours et à trouver des chemins alternatifs pour naviguer dans le labyrinthe.
    
3.  **Agent standard** : Cet agent est un agent DQN standard sans comportement spécialisé. Il apprend simplement à naviguer dans le labyrinthe de la manière la plus efficace possible.
    

**Deep Q-Learning (DQN) : Un Aperçu Mathématique**
--------------------------------------------------

Deep Q-Learning (DQN) est un algorithme d'apprentissage par renforcement qui combine le Q-learning avec des réseaux de neurones profonds. Voici un bref rappel des concepts mathématiques clés :

### **Q-Learning**

En Q-learning, nous apprenons une fonction Q, Q(s,a), qui représente la récompense cumulative attendue en prenant l'action a dans l'état s, et en suivant ensuite une politique optimale. La fonction Q est mise à jour de manière itérative à l'aide de l'équation de Bellman :

Q(s,a)←Q(s,a)+α\[r+γmaxa′​Q(s′,a′)−Q(s,a)\]

où :

*   s est l'état actuel.
    
*   a est l'action prise dans l'état s.
    
*   r est la récompense reçue après avoir pris l'action a dans l'état s.
    
*   s′ est le nouvel état atteint après avoir pris l'action a dans l'état s.
    
*   α est le taux d'apprentissage, qui détermine dans quelle mesure les nouvelles informations l'emportent sur les anciennes.
    
*   γ est le facteur d'escompte, qui détermine l'importance des récompenses futures par rapport aux récompenses immédiates.
    
*   a′ est l'action qui maximise la fonction Q dans le nouvel état s′.
    

### **Réseaux de Neurones Profonds**

Dans les problèmes avec de grands espaces d'états, il est impossible de stocker la fonction Q dans un tableau. Au lieu de cela, DQN utilise un réseau de neurones profond pour approximer la fonction Q. Le réseau de neurones prend l'état s comme entrée et produit les valeurs Q pour toutes les actions possibles a comme sortie.

### **DQN**

DQN combine Q-learning avec des réseaux de neurones profonds en utilisant deux techniques clés :

1.  **Expérience Replay** : Au lieu de mettre à jour le réseau de neurones avec chaque transition (s,a,r,s′), nous stockons les transitions dans un tampon de relecture et échantillonnons un lot de transitions aléatoires à partir du tampon pour mettre à jour le réseau de neurones. Cela permet de briser les corrélations entre les transitions et d'améliorer la stabilité de l'entraînement.
    
2.  **Réseau Cible Fixe** : Pour améliorer encore la stabilité de l'entraînement, nous utilisons deux réseaux de neurones : un réseau Q et un réseau cible. Le réseau Q est utilisé pour prédire les valeurs Q pour l'état actuel, tandis que le réseau cible est utilisé pour calculer les valeurs Q cibles pour la mise à jour de l'équation de Bellman. Les paramètres du réseau cible sont mis à jour périodiquement avec les paramètres du réseau Q, mais restent fixes entre les mises à jour.
    

### **Algorithme DQN**

L'algorithme DQN peut être résumé comme suit :

1.  Initialiser le réseau Q et le réseau cible avec des poids aléatoires.
    
2.  Initialiser le tampon de relecture.
    
3.  Pour chaque épisode :
    

*   Initialiser l'état initial s.
    
*   Pour chaque pas de temps t :
    
*   Sélectionner une action a en utilisant une politique ϵ-greedy basée sur le réseau Q.
    
*   Exécuter l'action a et observer la récompense r et le nouvel état s′.
    
*   Stocker la transition (s,a,r,s′) dans le tampon de relecture.
    
*   Échantillonner un lot de transitions aléatoires (si​,ai​,ri​,si′​) à partir du tampon de relecture.
    
*   Pour chaque transition (si​,ai​,ri​,si′​) dans le lot :
    
*   Calculer la valeur Q cible : yi​={ri​​si s′i est un eˊtat terminal ri​+γmaxa′Q′(si′​,a′;θ−)​sinon​où Q′ est le réseau cible avec des paramètres θ−.
    
*   Effectuer une étape de descente de gradient pour minimiser la perte : L=N1​∑i=1N​(yi​−Q(si​,ai​;θ))2où Q est le réseau Q avec des paramètres θ.
    
*   Mettre à jour l'état s=s′.
    
*   Si s est un état terminal, terminer l'épisode.
    
*   Mettre à jour les paramètres du réseau cible θ− avec les paramètres du réseau Q θ toutes les C étapes.
    

**Utilisation**
---------------

Pour exécuter les simulations avec les agents DQN, exécutez le script rl-dqn-main.ipynb. Ce script chargera les agents entraînés et les exécutera dans l'environnement du labyrinthe.
