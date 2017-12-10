# Recap structures de donn�e Cnam here

En java : occupation memoire d'un tableau java : nb element x taille r�f�rence (en g�n�ral 4 octect).
On note n le nombre d'op�rations fondamentales d'un algorithme.
Calcul du nombre d'operations fondamentales
sequence : ajout nbOpFonda
condition : 
	au mieux : nbOpFonda + (nbOpFonda de la condition ayant le - nbOpFonda)
	au pire : nbOpFonda + (nbOpFonda de la condition ayant le + nbOpFonda)	
boucle : nbOpFonda * nb iterations
methode recursive = nbOpFonda * nb d'appel recursif

ca va encore : on peut les utiliser pour des nbOpFonda moyens
O(1) temps constant
O(log(n)) temps logarithmique
O(n) temps lin�aire
O(n.log(n))

ca montre tres vite, tres vite incontrollable  : on peut les utiliser pour des nbOpFonda petits
O(n2) temps quadratique
O(n3) temps cubique
O(2n) temps exponentiel




poll retrieves and remove the element at the end of the queue.
pop retrieves and remove the element at the top of the stack.

peek does not remove but return the head of the queue.
peek does not remove but return the top of the stack.

push(E item) Pushes an item onto the top of this stack.

AbreVide : permet de savoir si un arbre est vide
Racine : permet d�obtenir l��tiquette contenue dans la racine de l�arbre
IemeFils : sous-arbre dont la racine est le i�me fils de la racine de l�arbre
Cr�erArbre : � partir d�un �l�ment, cr�e un arbre compos� d�un seul noeud �tiquett� par l��l�ment
AjouterIemeFils : � partir de 2 arbres, rattache le deuxi�me comme i�me fils du premier
SupprimerIemeFils : supprime le i�me fils de l�arbre

Faire un joli tableau excel avec tout �a, puis le remettre sur .md, aller dans gist.

||doublonsallowed|nullelementallowed|sorted|
|---|---|---|---|
|List/Liste|yes|?|?|
|Stack|?|?|?|
|Set|no|yes|?|
|Map|no|no|?|
|SortedSet|?|?|yes|
|HashSet|no|||
|LinkedHashset|no|||
|TreeSet|yes||ascending|
|HashMap|no||no|
|TreeMap|no||ascending|
|LinkedHashMap|no|||


||canapplyCollection.sortonit|isEmptymethod||
|---|---|---|---|
|List|yes|yes||
|Stack|?|?|?|
|Set|no|||
|Map|no|||
|SortedSet|?|||
|HashSet|?|||
|LinkedHashset|?|||
|TreeSet|?|||
|HashMap|?|||
|TreeMap|?|||
|LinkedHashMap|?|||


||timecostforbasicoperation|||
|---|---|---|---|
|List|?|||
|Stack|?|?|?|
|Set|?|||
|Map|?|||
|SortedSet|?|||
|HashSet|constant|||
|LinkedHashset|constant|||
|TreeSet|logarithmtimecost|||
|HashMap|?|||
|TreeMap|?|||
|LinkedHashMap|?|||


||poll/sommet|pop/depiler|peak/sommet|push/empiler|
|---|---|---|---|---|
|List|?||||
|Stack|?|yes|yes|yes|
|Set|?||||
|Map|?||||
|SortedSet|?||||
|HashSet|constant||||
|LinkedHashset|constant||||
|TreeSet|logarithmtimecost||||
|HashMap|?||||
|TreeMap|?||||
|LinkedHashMap|?||||


Ajouter ces colones. Cf Big-O stealSheet for more infos.
||AbreVide|Racine|IemeFils|Cr�erArbre|AjouterIemeFils|SupprimerIemeFils|
|--|--|--|--|--|--|--|
||AbreVide|Racine|IemeFils|Cr�erArbre|AjouterIemeFils|SupprimerIemeFils|