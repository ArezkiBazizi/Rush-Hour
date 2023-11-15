Le problème : 
Le plateau de jeu est une grille de taille N × M représentant un parking. On y trouve plusieurs types de véhicules de différentes longueurs, mais tous larges d'une case. Le parking n'a qu'une seule sortie large d'une case et qui se situe sur l’une des parois du plateau. Le but du jeu est de faire sortir une voiture particulière : le voiture GOAL. Chaque véhicule est orienté dans une des deux directions (horizontale ou verticale) et ne peut se déplacer qu'en ligne droite (en marche avant ou en marche arrière). Chaque véhicule reste donc toujours sur une même ligne si sa direction est horizontale ou sur une même colonne si sa direction est verticale. Le véhicule goal est donc placé sur la ligne de la sortie mais il est bloqué par d'autres véhicules qu'il faut déplacer.

Résolution :
Pour Implémentez le problème, plusieurs méthodes s’offrait à nous, on a finalement choisi la méthode qui nous paraissait réalisable avec la contrainte de temps, celle de l’algorithme de parcours en largeur, on est conscient que ce n’est pas la plus optimale qui existe, mais c’est celle qu’on a mieux réussit à implémenter.

Le code : le code se compose de trois classes essentielles :

•	Main : il s’agit de la classe principale, dans cette dernière on commence par lire l’état initial du parking à partir d’un fichier représenté par un objet Parking avec la fonction parseFileToParking(), ensuite on vérifie si une solution est possible. Si c’est le cas, on génère la meilleure solution en parcourant l’arborescence des déplacements de stationnement possibles à l’aide de la méthode solveParking(), qui renvoie l’objet Parking final (une feuille de l’arbre) comme solution. Le programme utilise ensuite la méthode printSteps() pour afficher les mouvements qui mènent à la solution. Si aucune solution n’est trouvée, le programme imprimera qu’il n’y a pas de solution.


•	Move : Cette classe représente le déplacement d'une voiture dans un parking. Elle contient deux variables d'instance : _carIndex, qui représente l'index de la voiture qui est déplacée, et _parentParking, qui représente le parking d'où le déplacement a été effectué. La classe a également deux méthodes : getMovedCar(), qui retourne l'index de la voiture déplacée, et getParentParking(), qui retourne le parking d'où le déplacement a été effectué. La méthode constructeur Move(Parking parentParking, Parking childParking, int carIndex) permet de construire un objet Move en spécifiant le parking parent, le parking enfant et l'index de la voiture qui est déplacée.

•	Parking : La classe Parking représente un état possible du parking. Il contient des membres statiques qui décrivent les caractéristiques générales du parking (taille, sortie, etc.) et des membres propres à chaque instance qui décrivent l'état actuel du parking (positions des voitures, etc.). Il contient également une référence à l'objet Move qui l'a généré, ce qui permet de retracer les déplacements effectués pour arriver à cet état. Les membres statiques de la classe comprennent une matrice indiquant l'état des emplacements de parking (occupé ou non), un ensemble de hashage contenant tous les parkings générés, les dimensions du parking, la position de la sortie, le nombre d'emplacements bloqués entre la voiture cible (goal car) et la sortie, et un indicateur indiquant si la sortie est située à l'avant ou à l'arrière de la voiture cible. Il y a également des compteurs pour le nombre de voitures, l'orientation des voitures, la plage d'index des voitures et la taille des voitures. Les membres de chaque instance de la classe comprennent la position des voitures dans leurs rangées (définissant le parking) et un déplacement reliant cette situation à la précédente. Il y a également des méthodes pour vérifier si le parking est résolu ou s'il est impossible de résoudre le parking en raison de la situation de la voiture cible.


Remarque : on s’est inspiré de travaux trouvés sur internet sur des jeux similaires pour la l’implémentation de la méthode de hachage car elle permet d’optimiser la recherche d'une solution, en évitant de retomber sur des états déjà explorés, et en permettant de comparer rapidement des états.

Exemple : 
Parking: 5 fois 5
+---+---+---+---+---+
|     1   1         |
+   +   +   +   +   +
|         2         |
+   +   +   +   +   +
| G   G   2   3   3 
+   +   +   +   +   +
|                   |
+   +   +   +   +   +
|                   |
+---+---+---+---+---+
Elements du Parking:
		 voiture Goal: 1
		 autre voitures: 3
Emplacements:
		 voiture Goal: [(2,0), (2,1)]
		 voiture 1: [(0,1), (0,2)]
		 voiture 2: [(1,2), (2,2)]
		 voiture 3: [(2,3), (2,4)]
