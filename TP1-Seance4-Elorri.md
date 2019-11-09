# TP1 - Séance 4

## Manipulation 1 : Manipulation de fichiers

**En utilisant l'éditeur vi, modifier les fichiers nécessaires afin d'ajouter deux groupes : auditeurs, enseignants.**

Dans etc/groups on ajoute les lignes suivantes : 

```
auditeurs:x:1005:
enseignants:x:1006:
```
Chaque ligne contient dans l’ordre :

```
	nom de groupe
	mdp
	GID
	Liste des utilisateurs autorisés à se connecter au groupe (util[,util ... ])
```		
ici il n'y aucun membre dans les 2 groupes.
le GID est choisi en prenant soin que celui-ci n'existe pas déjà

**Une méthode naïve pour l'ajout des utilisateurs consiste à éditer les fichiers /etc/passwd et /etc/shadow. Selon cette méthode l'ajout d'un utilisateur passe par les étapes suivantes :**
1. Ajout d'une entrée (ligne) correspondant à l'utilisateur dans le fichier /etc/passwd. et une autre dans /etc/shadow
2. Positionnement du mot de passe initial
3. Création du répertoire personnel de l'utilisateur
4. Changement de propriétaire pour ce répertoire
5. Copie des fichiers d'environnement (les fichiers contenus dans /etc/skel).

**Appliquer la méthode naïve décrite ci-dessus pour créer le compte 'tintin'. Essayer d'accéder à la machine en fournissant le login de l'utilisateur après chaque étape (donc essayer 5 fois) et noter les messages rendus par le système. Préciser dans votre compte-rendu les modifications apportées aux fichiers de configuration.**

	Dans /etc/passwd, les lignes contiennent dans l’ordre : 
	
		1.nom de connexion
		2.mdp crypté
		3.UID
		4.GID par défaut
		5.Commentaire
		6.Répertoire de connexion
		7.Champ de commande

	On ajoute la ligne suivante. Càd un utilisateur nommé toto, n’ayant pas de mot de passe, pas d’id, n’appartenant pas à un groupe

		tintin:::::

	Puis on essai de se logger : 

		root@Vivo-AIO-27-V272UA:/home/elorri# login tintin
		Identifiant de connexion incorrect

	On ajoute le UID
		
		tintin::1001:::

	Puis on essai de se logger : 

		root@Vivo-AIO-27-V272UA:/home/elorri# login tintin
		Identifiant de connexion incorrect
		
	Ne marche toujours pas. Ajoutons un mot de passe crypté. Pour cela créons uin mot de passe crypté.
	
		root@Vivo-AIO-27-V272UA:/home/elorri# mkpasswd UnMdpCrypte
		EBcF/zCvA/EZY

	Modifions la ligne tintin du fichier /etc/passwd
	
		tintin:x:1001:::
				
	Ajoutons le mot de passe crypté dans le fichier shadow
	
		tintin:EBcF/zCvA/EZY:18206:0:99999:7:::
		
	C'est à dire dans l'ordre : 
	
		1 : nom de l’utilisateur tintin
		2 : mot de passe crypté
		3 : nombre de jours écoulés entre le 01/01/1970 et la dernière modification du mot de passe. Aujourd’hui le 6 novembre 2019. Sous excel 01/01/1970 – 06/11/2019  = 18206
		4 : nombre minimum de jours requis entre deux modifications du mot de passe. Ici  on a choisi 0.
		5 : Nombre maximum de jours au bout duquel une modification est obligatoire. Si ce champ est inférieur à la valeur du champ précédent, l’utilisateur ne peut modifier le mot de passe . Ici on a mis le maximum, ça fait 273 ans.
		6 : Nombre de jours avant lequel l’utilisateur doit être averti de l’expiration prochaine du mot de passe. On a mis 7 cad 1 semaine.
		7 : Nombre de jours avant que le compte soit verrouillé (mdp expiré). On a rien mis, le compte ne sera pas verrouillé.
		8 : Date d’expiration du mot de passe (en jours écoulés depuis 01/01:1970). On a rien mis, pas d’expiration du mot de passe.
		9 : champ réservé. Rien non plus, le système ajoutera quelque chose si nécessaire.	
	
	Puis on essai de se logger : 

		root@Vivo-AIO-27-V272UA:/home/elorri# login tintin
		Identifiant de connexion incorrect

	Pour que cela fonctionne il faut spécifier égamlement le groupe auquel appartient tintin, ici on va mettre tintin et le fichier de commande shell qu'il va utiliser. Donc dans /etc/passwd on met
	
		tintin:x:1003:1003:/bin/bash
		
	Dans /etc/group
	
		tintin:x:1003
		
	On essaie de se connecter : 
	
		root@Vivo-AIO-27-V272UA:/home/elorri# login tintin
		
	Cela marche mais on voit le message 
	
		Pas de répertoire, connexion avec HOME=/

	Essayons de nous connecter par l'interface graphique.
	
		Ctrl+alt+suppr pour fermer la session en cours
		
	L'utilisateur apparait bien dans la liste, cependant lorsque l'on tente de se connecter en entrant le mot de passe, cela est impossible. Problablement parce qu'il n'y a pas de répertoire /home dédié pour pierre. Creons en un. 
	
		root@Vivo-AIO-27-V272UA:/home# mkdir tintin

	Le répertoire tintin existe bien, pouvons nous nous connecter ?
		
			Ctrl+alt+suppr pour fermer la session en cours
			
		Toujours pas. Peut-être parce qu'il n'a pas les droits d'acces à son répertoire home/tintin, donnons lui les droits.
		
			root@Vivo-AIO-27-V272UA:/home/elorri# chown tintin /home/tintin
			root@Vivo-AIO-27-V272UA:/home/elorri#		
		
		Essayons à nouveau
		
			Ctrl+alt+suppr pour fermer la session en cours
			On entre le mot de passe de tintin
			
		Ca marche.
		
	Il nous reste à copier les répertoires et fichiers définis par l'admistrateur comme étant les répertoire et fichiers que devrons contenir par défaut tous les nouveaux comptes
	
		cp -r /etc/skel/* /home/tintin
		
	Note : Les répertoires ajoutés par la commandes useradd ne sont pas ceux présents dans /etc/skel mais ceux définis dans le fichier
	
		cat .config/user-dirs.dirs


Manipulation 2 : Commandes de base

Cherchez le(s) rôle(s) et testez les différentes commandes suivantes : useradd, usermod, userdel, groupadd, groupmod, groupdel, pwck, grpck, finger, chfn, chsh, passwd, su, id, groups, vipw, vigr.

	Pour connaitre le rôle de chaque commandes le plus simple est de faire 
	
		man commande
		exple : man useradd
		
	Roles des commendes : 
	
		useradd - créer un nouvel utilisateur ou modifier les informations par défaut appliquées aux nouveaux utilisateurs
		adduser, addgroup - Ajouter un utilisateur ou un groupe au système
		usermod - Modifier un compte utilisateur
		userdel - supprimer un compte utilisateur et les fichiers associés
		groupadd - Créer un nouveau groupe
		groupmod - Modifier la définition d'un groupe du système
		groupdel - Supprimer un groupe
		pwck - Vérifier l'intégrité des fichiers de mots de passe
		grpck - Vérifier l'intégrité des fichiers d'administration des groupes
		finger - affiche des informations sur un utilisateur.  
			- cette commande n'existe plus car considérée trop explicite et pouvant entrainer des failles de sécurité.
			- l'alternative est pinky
		pinky - commande finger moins exhaustive
		chfn - Modifier le nom complet et les informations associées à un utilisateur
		chsh - Changer l'interpréteur de commandes initial cad le shell. Par exemple utiliser /bin/bash plutot que /bin/sh
		passwd - Modifier le mot de passe d'un utilisateur
		su - Changer d'identifiant d'utilisateur ou devenir superutilisateur
		id - print real and effective user and group IDs
		groups - print the groups a user is in
		vipw, vigr - Éditer les fichiers passwd, group, shadow ou gshadow	

A quoi sert la commande adduser qu'elle est la différence avec useradd ?

	useradd est une commande binaire.
	adduser est un script perl faisant appel à useradd. 
	adduser est plus large que useradd, il ajoute le répertoire de travail de l'utilisateur et y copie les donnée présentes dans /etc/skel



Manipulation 3 : Collecte des informations

Est-ce que l’utilisateur « bin » existe ?

	Oui, on retrouve la ligne suivante ... dans /etc/passwd
	
		bin:x:2:2:bin:/bin:/usr/sbin/nologin
		
A quels groupes appartient l’utilisateur « bin » ?

	Pour le savoir il suffit de taper la commande :
	
		elorri@Vivo-AIO-27-V272UA:~$ groups bin
		bin : bin

	L'utilisateur bin appartient au seul et unique groupe du meme nom bin.  Note: l'utilisateur bin est utilisé pour éxécuter des fichier binaires notamment toutes les commandes du /bin/bash cad cd, cat, ls…
		
Existe-t-il d’autres comptes utilisateurs possédant les mêmes droits que « root » ?

	Oui c'est seul sur la machine virtuelle présentée. Cependant, il est possible de créer des utilisateur ayant les mêmes droits que root, il suffit pour cela du lui donner le même UID à savoir 0. Ceci se fait dans le fichier /etc/passwd



Manipulation 4 : Création et gestion d’un utilisateur

Créer avec useradd en gardant les caractéristiques par défaut, l’utilisateur pierre. Quel est le groupe de pierre ? Son shell ? Son répertoire de travail ?

	useradd Pierre

	cat /etc/passwd

	Pierre:x:1002:1002::/home/Pierre:/bin/sh

	L’utilisateur Pierre créé
		a un mot de passe crypté noté ici x
		a le UID 1002
		appartient au groupe de GID 1002
		pas de commentaires 
		a comme répertoire de travail /home/Pierre
		a pour interpreteur de commande le shell sh (note ceci est différent de l’interpreteur donné à l’utilisateur administrateur qui est un bash (bash est un interpreteur plus complet)).

	Pour connaître le nom du groupe à partir du GID : 

	cat /etc/group

	Le groupe ayant le GID 1002 est 

	Pierre:x:1002:

	Donc, le système a crée un groupe ayant le même nom que le nom utilisateur.

	Vérifions que le système a bien crée un répertoire de travail home/Pierre

	ls /home/Pierre

	Réponse :  ls: impossible d'accéder à '/home/Pierre': Aucun fichier ou dossier de ce type

	Visiblement le répertoire n’a pas été crée.

	Regardons si le mot de passe crypté de Pierre est bien stocké dans /etc/shadow

	cat /etc/shadow

	Réponse : Pierre:!:18206:0:99999:7:::

	Oui, il y a bien un mot de passe crypté mais il est très court, c’est le « ! ». Ceci indique qu’aucun mot de passe n’a été définit pour l’utilisateur.


Ajoutez un groupe staff. Enregistrez pierre dans ce groupe, tout en gardant ses autres groupes.

	elorri@Vivo-AIO-27-V272UA:~$ groupadd staff
	groupadd : le groupe « staff » existe déjà

	
	Apparement ce groupe existe déjà, donc pas besoin de le créer. Voyons si d'autres utisateurs sont associés à ce groupe
	
	cat /etc/group
	Parmi les lignes, il y a : 
	staff:x:50:

	Donc pour le moment personne n'a été affecté.
	
	Affectons Pierre à ce groupe : 
	
	sudo usermod -G staff Pierre
	
	Voyons si ça a marché en regardant la liste des groupes
	
	cat /etc/group
	Parmi les lignes, il y a : 
	staff:x:50:Pierre

	Oui Pierre est bien dans le groupe.


Affichez les groupes de pierre.

	elorri@Vivo-AIO-27-V272UA:~$ groups Pierre
	Pierre : Pierre staff
	
	staff fait bien partie des groupes de Pierre


Connectez-vous au compte de pierre de deux façons différentes : à la connexion classique, et avec la commande su. 

	Essayons de se connecter à ce compte en ligne de commande

	login Pierre
	
	ou
	
	su Pierre

	puis mettons "Enter" comme mot de passe.

	Identifiant de connexion incorrect

	La documentation indique "Prenez note qu'un compte d'utilisateur sans mot de passe est inactif : aucun usager ne peut ouvrir de session avec ce compte tant qu'un mot de passe ne lui a pas été attribué. Pour ce faire, utilisez la commande passwd pour attribuer un mot de passe après la création du compte."

	Allons dans Paramètre/Détails/Utilisateurs

	Un utilisateur Pierre a bien été ajouté

	Fermons la session, pour essayer de se connecter par l'interface graphique (connexion classique)

	Il n'y a qu'un seul utilisateur proposé Pierre n'y est pas.

Expliquez les différences. 

	La commande login se fait dans le terminal, la façon classique consiste à passer par une interface graphique.

Que faut-il faire pour pouvoir se connecter normalement au compte pierre ? 

	Ajouter un mot de passe.

Faites le nécessaire.

	root@Vivo-AIO-27-V272UA:/home/elorri# passwd Pierre
	Entrez le nouveau mot de passe UNIX : 
	Retapez le nouveau mot de passe UNIX : 
	passwd : le mot de passe a été mis à jour avec succès
	
	Essayons à nouveau de nous connecter en ligne de commande
	
		root@Vivo-AIO-27-V272UA:/home/elorri# login
		Vivo-AIO-27-V272UA login : Pierre
		Mot de passe : 
		Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 5.0.0-32-generic x86_64)

		 * Documentation:  https://help.ubuntu.com
		 * Management:     https://landscape.canonical.com
		 * Support:        https://ubuntu.com/advantage

		 * Kata Containers are now fully integrated in Charmed Kubernetes 1.16!
		   Yes, charms take the Krazy out of K8s Kata Kluster Konstruction.

		     https://ubuntu.com/kubernetes/docs/release-notes

		 * Canonical Livepatch is available for installation.
		   - Reduce system reboots and improve kernel security. Activate at:
		     https://ubuntu.com/livepatch

		1 paquet peut être mis à jour.
		0 mise à jour de sécurité.

		Your Hardware Enablement Stack (HWE) is supported until April 2023.

		The programs included with the Ubuntu system are free software;
		the exact distribution terms for each program are described in the
		individual files in /usr/share/doc/*/copyright.

		Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
		applicable law.


		The programs included with the Ubuntu system are free software;
		the exact distribution terms for each program are described in the
		individual files in /usr/share/doc/*/copyright.

		Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
		applicable law.

		Pas de répertoire, connexion avec HOME=/
		$ 
		
	Ca marche. Notons qu'il est indiqué qu'il manque le répertoire /home. 
	Essayons de nous connecter par l'interface graphique.
	
		Ctrl+alt+suppr pour fermer la session en cours
		
	L'utilisateur apparait bien dans la liste, cependant lorsque l'on tente de se connecter en entrant le mot de passe, cela est impossible. Problablement parce qu'il n'y a pas de répertoire /home dédié pour pierre. Creons en un. 
	
		root@Vivo-AIO-27-V272UA:/home# mkdir Pierre
		root@Vivo-AIO-27-V272UA:/home# ls
		elorri  Pierre

	Le répertoire Pierre existe bien, pouvons nous nous connecter ?
	
		Ctrl+alt+suppr pour fermer la session en cours
		
	Toujours pas. Peut-être parce qu'il n'a pas les droits d'acces à son répertoire home/Pierre, donnons lui les droits.
	
		root@Vivo-AIO-27-V272UA:/home/elorri# chown Pierre /home/Pierre
		root@Vivo-AIO-27-V272UA:/home/elorri#		
	
	Essayons à nouveau
	
		Ctrl+alt+suppr pour fermer la session en cours
		On entre le mot de passe de Pierre
		
	Ca marche.
		
Changez le champ commentaire de pierre en utilisant la commande vipw. Renseignez le champ avec le texte suivant : « Pierre Cerf – Lannion ».

	Ligne de pierre dans /etc/passwrd
	
		Pierre:x:1002:1002::/home/Pierre:/bin/sh	
		
	Ajoutons un comentaire, cad modifions la ligne par : 
		
		Pierre:x:1001:1001:Pierre Cerf – Lannion:/home/Pierre:/bin/sh
		
	Verifions dans
		
		Paramètres/Détails/Utilisateurs
		
	Le nom a changé, "Pierre Cerf – Lannion" apparait à la place de Pierre, idem lorsqu'on ferme la session.

Verrouillez le compte de pierre. 

	usermod --expiredate 1 Pierre
	
Essayez de vous connecter au compte pierre et notez les messages.

	root@Vivo-AIO-27-V272UA:/home/elorri# login
	Vivo-AIO-27-V272UA login : Pierre
	Mot de passe : 
	Votre compte a expiré. Contactez votre administrateur système
	Échec d'authentification
	
	Le même message apparait si l'on tente de se connecter en mode graphique.

Déverrouillez ensuite ce compte et essayez de vous reconnecter à pierre.

	usermod --expiredate "" Pierre
	login Pierre

	Ca marche.

Créez un compte avec l’outil d’administration (linuxconf, users-admin...). Créez un compte «admin » d’UID 0.  Hérite t'il automatiquement de tous les droits?

		/Paramètres/Détails/Utilisateurs/Ajouter un utilisateur
		
	Regardons quels droits il a , en regardant à quels groupe il appartient
	
		elorri@Vivo-AIO-27-V272UA:~$ sudo groups unadmin
		unadmin : unadmin sudo
		
	Il n'a donc pas tous les droits, puis que le groupe "root " n'est pas dans la liste. Cependant, il peut agir comme un super-utilisateur car il y a le groupe sudo.
	
Testez et à défaut donnez lui. Il peut servir si, par exemple, on oublie le mot de passe de root.	

	Regadons /etc/passwd
	
		unadmin:x:1002:1002:UnAdmin,,,:/home/unadmin:/bin/bash
		
	Donnons lui les droits root, en mettant un UID de 0.
	
		unadmin:x:0:1002:UnAdmin,,,:/home/unadmin:/bin/bash
		
	Regardons les droits
	
		elorri@Vivo-AIO-27-V272UA:~$ sudo groups unadmin
		unadmin : unadmin root sudo
		
	Maintenant il a tous les droits. "root" est présent dans la liste. Verifions.
	
		root@Vivo-AIO-27-V272UA:/home/elorri# login unadmin
		Identifiant de connexion incorrect

	Bizarre je n'ai pas trouvé pourquoi. Cependant ça marche quand j'utilise la méthode graphique.
	
		Ctrl+alt+suppr pour fermer la session en cours
		
	En ouvrant le terminal le prompt finit bien par # comme ceci
	
		root@Vivo-AIO-27-V272UA:/home/unadmin#
		
Manipulation 5 : Gestion des utilisateurs suite...

Que fait la commande id ?

	Elle donne les id des groupes auxquel l'utilisateur appartient.
	Exple : uid=1000(elorri) gid=1000(elorri) groupes=1000(elorri),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare),127(kvm),129(wireshark),130(vboxusers)

Donner les étapes nécessaires pour fermer le compte d'un utilisateur en prenant soin de sauvegarder ses données.

	Savegarder les donnée du repertoir home
	
		cp /home/Pierre /home/Pierre_backup
		
	Garder dans un fichier texte les 4 lignes suivantes 
		
		Pierre:x:1001:1001:Pierre Cerf – Lannion:/home/Pierre:/bin/sh
		Pierre:$6$O83UpXB7$nnjBKewiSOlQGEHUrCmUBLrko23MQcXr.L5vzN3yfDBxbwvY2srOJmaCwjWAEdi6oGuyfK6MDRyaM/f1SBrhr0:18207:0:99999:7:::
		Pierre:x:1001:
		uid=1001(Pierre) gid=1001(Pierre) groupes=1001(Pierre),50(staff)

	Qui correspondent
	
		la ligne de l'utilisateur Pierre dans le fichier /etc/passwd
		la ligne de l'utilisateur Pierre dans le fichier /etc/shadow
		la ligne du groupe Pierre dans le fichier /etc/group  (normalement la suppression de Pierre ne supprime pas ce groupe mais au cas où)
		le résultat de la commande : id Pierre
		
	Fermer le compte
	
		deluser Pierre
		delgroup Pierre
		rmdir /home/Pierre
		
	Pour le restaurer
	
		mv /home/Pierre_backup  /home/Pierre
		adduser Pierre
		
	Puis remettre Pierre dans tous les groupes où il était affecté
	
		usermod -G staff Pierre	
	

Manipulation 6 : Gestion des groupes

Rappel : à la connexion, un utilisateur est identifié par son UID et le GID de son groupe principal qui devient le groupe actif durant la session. Tester la commande newgrp. A quoi sert elle ? 

	Pour savoir ce que fait newgrp on peut taper dans le terminal
	
		man newgrp

	man pour manuel. On obtient : 
	
		NOM
		       newgrp - se connecter avec un nouveau groupe

		DESCRIPTION
		       La commande newgrp permet de changer l'identifiant de groupe de l'utilisateur au cours d'une session...L'accès sera refusé si le mot de passe du groupe est vide et que l'utilisateur ne fait pas partie de ses membres.
		       
	On en déduit que la commande newgrp permet à l'utilisateur courant de s'ajouter à un groupe (s'il n'y ait pas déjà). Cela lui permet de bénéficier des droits de ce groupe.
	
Cette commande est elle durable ? 

	Elle dure la durée de la session. Pour vérifier cela ajoutons l'utilisateur courant pierre au groupe pierregroup avec cette commande. D'abord créons le groupe pierregroup avec le compte administrateur.
	
		elorri@Vivo-AIO-27-V272UA:#  addgroup pierregroup
		
	Ajoutons un mot de passe au groupe, car comme indiqué dans la doc l'accès sera refusé (cf plus haut)
	
		elorri@Vivo-AIO-27-V272UA:#  gpasswd pierregroup
		
	Ensuite créons un répertoire "pierregroupe" accéssible uniquement au membres de ce groupe "pierregroup", ainsi qu'un fichier à l'interieur

		mkdir /home/pierregroupe
		chgrp pierregroup /home/pierregroupe/
		touch unFichierDuGroup
		echo "Me vois ?" > unFichierDuGroup 
		chgrp pierregroup unFichierDuGroup
				
	Puis restreignons les permissions uniquement aux membres du groupe
	
		elorri@Vivo-AIO-27-V272UA:/home$ cd /home
		elorri@Vivo-AIO-27-V272UA:/home$ ll
		drwxr-xr-x 19 pierre       pierre       4096 nov.   7 21:25 pierre/
		drwxr-xr-x  2 root         pierregroup         4096 nov.   7 21:39 pierregroupe/

	On voit que tous les utilisateurs ont la permission d'ecriture. Changeons cela.
	
		chmod 770 pierregroupe
		chmod 770 unFichierDuGroup
		
	Ce qui correspond à 
	
		-R pour récurssif, cad valable pour les sous dossiers aussi
		7 on donne tous les droits au propriétaire
		7 on donne tous les droits au groupe auquel appartient le fichier
		0 on donne aucun droits au reste du monde.
		Plus d'infos : https://doc.ubuntu-fr.org/permissions		
	
	Maintenant connectons nous sur le compte pierre et essayons de travailler sur le fichier unFichierDuGroup
	
		pierre@Vivo-AIO-27-V272UA:/home$ cd /home/pierregroupe
		bash: cd: /home/pierregroupe: Permission non accordée		
	
	Nous n'avons pas les droits car nous n'appartenons pas au group pierregroup, faisons un newgrp
	
		pierre@Vivo-AIO-27-V272UA:~$ groups
		pierre
		pierre@Vivo-AIO-27-V272UA:~$ newgrp pierregroup
		Mot de passe : 
		pierre@Vivo-AIO-27-V272UA:~$ groups
		pierregroup pierre
		
	Réessayons
	
		pierre@Vivo-AIO-27-V272UA:~$ cd /home/pierregroupe/
		pierre@Vivo-AIO-27-V272UA:/home/pierregroupe$ cat unFichierDuGroup 
		Me vois tu ?
		pierre@Vivo-AIO-27-V272UA:/home/pierregroupe$ echo "Oui, je te vois" >> unFichierDuGroup 
		pierre@Vivo-AIO-27-V272UA:/home/pierregroupe$ cat unFichierDuGroup 
		Me vois tu
		Oui, je te vois
		pierre@Vivo-AIO-27-V272UA:/home/pierregroupe$ 	
	
	Ca marche, on n'arrive a modifier le fichier.
	
Les droits de l’utilisateur sont ils impactés ? 

	Il ne sont pas impactés, après déconnection de la session, la commande groups revient aux valeurs par défaut.
	Les fichiers /etc/passwd, /etc/shadows, /etc/group restent inchangés.

Qu’en est il lors de la création d’un nouveau fichier ?

	La création d'un nouveau fichier ne posse pas problème après l'utilisation de newgrp.


Manipulation 7 : Gestion des mots de passe

L'administrateur peut-il connaître le mot de passe d'un utilisateur ? 

	Il ne peut pas. La seule chose qu'il puisse voir c'est la version chiffrée du mot de passe dans le fichier /etc/shadow. Exemple de ligne de shadow : 
	
		pierre:$6$teOnMj/y2Tk9GlAq$gux6nlKoGIbLIR.pdpb9KwoYWle1NR.7vM0.pv4.YJqa.1sgLTEIH/KIgEMxHKylxpupOXZRtP1kooHq2qqbl1:18207:0:99999:7:::

Peut-il le changer ? Si oui comment ?

	administrateur@ordinateur:# passwd pierre
	Entrez le nouveau mot de passe UNIX : (nouveau mot de passe)
	Retapez le nouveau mot de passe UNIX : (mot de passe répété)
	passwd : le mot de passe a été mis à jour avec succès
	
Optionnel : Test de robustesse des mots de passe, avant que ce ne soit fait par un pirate, il est indispensable de tester si un utilisateur n’a pas un mot de passe trop facile par rapport à une attaque par dictionnaire.
Pour ce faire il convient à un administrateur de faire tourner régulièrement un outil du style crack, L0phtCrack ou John the Ripper et de bloquer les comptes qui ont été cassés. Ces comptes ne seront ré-activés qu’après changement de mot de passe sérieux.
L’intérêt de John the Ripper est qu’il peut être rajouté directement au système de PAM du système (pam_passwdqc) afin de refuser à un utilisateur la possibilité de mettre un mot de passe craquable facilement par n’importe qui. C’est aussi un logiciel portable, optimisé et pouvant casser des mots de passe Windows, etc.

Installation de John the Ripper
	Tapez la commande apt-get install john pour récupérer et installer le paquet deb correspondant.  
	A défaut récupérer sur http://www.openwall.com/john/ une version récente. Décompresser avec un tar zxvf et lire le README. Compiler suivant le mode d’emploi. http://dawal.chrysalice.org/article.php3?id_article=48
	Récupérer le fichier source de mot de passe et tester la commande
	
		john /etc/shadow
		
	cela prend du temps alors passer à la suite pendant que l’ordinateur travaille.

Réfféchir aux méthodes de communication positives permettant d’éviter que de pareils cas se reproduisent. 
Évidemment cela n’empêche pas de faire tourner régulièrement un logiciel de craquage afin d’éviter ce genre d’étourderies. La bonne nouvelle est que ce logiciel possède un mode qui envoie un courriel à une personne dont le mot de passe est trouvé afin de la prévenir de la faiblesse trouvée. 
Les plus curieux regarderont le fichier de configuration john.ini en conjonction avec le fichier explicatif doc/RULES. 
Par défaut le système utilise les noms des utilisateurs comme source de mot de passe, puis des combinaisons du petit dictionnaire password.lst avant de se lancer dans une recherche par force brute.
Pour une mise en production dans la vraie vie il faudrait utiliser un dictionnaire de mots plus important.


Manipulation 8 : Mise en place de Quota
	
Commandes de base : Cherchez le(s) rôle(s) des différentes commandes suivantes : edquota, quota, repquota, quoaton, quotaoff, quotacheck.

	edquota : édite les quotas utilisateurs
	quota : affiche l'utilisation des disques et les limites définies
	repquota : récapitule les quotas d'un système de fichier. Indique si l'utilisateur a dépassé les limites ou s'en approche.
	quotaon, quotaoff  : allume ou éteint les statisques de quota faites sur le système de fichier.
	quotacheck : scanne le système de fichier et met à jour ses statistiques de quota.

Mise en place de quotas pour un utilisateur. Instaurez un quota « soft » et « hard » pour un utilisateur que vous aurez créé au préalable.





Mettez en place ce quota après avoir vérifié que l’utilisateur ne dépasse pas le quota. Remplissez le compte de l’utilisateur et observez ce qui se passe.

Refaites la manipulation en remplissant le compte avant d’instaurer le quota. 

Que se passe-t-il à la connexion de l’utilisateur après la mise en place du quota ? 

Peut-il encore se connecter ?

Peut-il détruire des fichiers pour libérer l’espace ?

Mise en place de quotas pour un groupe. Quelle est la signification d’un quota sur un groupe ?


Manipulation 9 : ACL

Vérifier que le noyau est bien configuré pour supporter les ACL (être root pour effectuer les commandes) :
Exécuter la commande suivante : grep ACL /boot/config-*
Vérifiez que la ligne CONFIG_FS_POSIX_ACL=y est bien présente et que celle lié au système de fichier également.


	/boot/config-5.0.0-31-generic:CONFIG_FS_POSIX_ACL=y
	/boot/config-5.0.0-31-generic:CONFIG_EXT4_FS_POSIX_ACL=y


Installer le paquet ACL : 

		apt-get install acl
	
	Fait.
	

Créer un utilisateur Tintin, créer un fichier article donner les droits de lecture et d’écriture à Tintin sur ce fichier test avec ACL (utiliser la commande setfactl).

	On crée l'utilisateur tintin
	
		root@Vivo-AIO-27-V272UA:/home/elorri# adduser tintin
		Ajout de l'utilisateur « tintin » ...
		Ajout du nouveau groupe « tintin » (1006) ...
		Ajout du nouvel utilisateur « tintin » (1004) avec le groupe « tintin » ...
		Création du répertoire personnel « /home/tintin »...
		Copie des fichiers depuis « /etc/skel »...
		Entrez le nouveau mot de passe UNIX : 
		Retapez le nouveau mot de passe UNIX : 
		passwd : le mot de passe a été mis à jour avec succès
		Modification des informations relatives à l'utilisateur tintin
		Entrez la nouvelle valeur ou « Entrée » pour conserver la valeur proposée
			Nom complet []: Tintin
			N° de bureau []: 3
			Téléphone professionnel []: 
			Téléphone personnel []: 
			Autre []: 
		Ces informations sont-elles correctes ? [O/n] o
		root@Vivo-AIO-27-V272UA:/home/elorri# 

	On crée un document "article" par exemple dans le home de l'administrateur
	
		root@Vivo-AIO-27-V272UA:/home/elorri# touch article
		root@Vivo-AIO-27-V272UA:/home/elorri# echo "Tintin, peux tu me modifier ?" > article
		root@Vivo-AIO-27-V272UA:/home/elorri# 
		
	On regarde les droits
	
		root@Vivo-AIO-27-V272UA:/home/elorri# ll
		-rw-r--r--  1 root   root       37 nov.   8 20:50  article
		
	On voit que l'article est 
		- lisible et modifiable par l'utilisateur root
		- uniquement lisible par les utilisateur du groupe root, et le reste du monde.
	Donc pierre ne devrait pas pouvoir écrire dans le fichier. Connectons nous avec pierre et essayons d'écrire dans le fichier
	
		tintin@Vivo-AIO-27-V272UA:~$ echo "Oui, je peux" >> /home/elorri/article 
		-bash: /home/elorri/article: Permission non accordée
		
	En effet on ne peut pas. Repassons en mode admistrateur et ajoutons le droit a tintin
	
		root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -m u:tintin:rw article
		root@Vivo-AIO-27-V272UA:/home/elorri# ll
		-rw-rw-r--+  1 root   root       37 nov.   8 20:50  article
	
	le "+" à coté des droits de base indique que des droits ACL ont étés ajoutés. Pour vérifier les droits ACL ajoutés
	
Tapez la commande getfacl afin de vérifier les droits nouvellement créé. Quels sont les droits de Tintin ?	
	
		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article
		# file: article
		# owner: root
		# group: root
		user::rw-
		user:tintin:rw-
		group::r--
		mask::rw-
		other::r--
		
	Il y a bien tintin. Essayons à nouveau de modifier le fichier à partir du compte tintin.
	
		tintin@Vivo-AIO-27-V272UA:~$ echo "Oui, je peux" >> /home/elorri/article 
		tintin@Vivo-AIO-27-V272UA:~$ cat /home/elorri/article 
		Tintin, peux tu me modifier ?
		Oui, je peux
		tintin@Vivo-AIO-27-V272UA:~$ 		
		
	Tintin a bien pu modifier le fichier.
		
Créer un masque par défaut de lecture seule pour les autres utilisateurs.

	root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -m m:r-- article
	root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article
	# file: article
	# owner: root
	# group: root
	user::rw-
	user:tintin:rw-			#effective:r--
	group::r--
	mask::r--
	other::r--
	
Le masque l'emporte sur les droits de tintin. Tintin ne devrait plus pourvoir modifier le fichier.

	tintin@Vivo-AIO-27-V272UA:~$ echo "Oui, je peux" >> /home/elorri/article 
	-bash: /home/elorri/article: Permission non accordée
	
Créer le repertoire PetitReporter et appliquer les droits de lecture écriture sur tout le repertoire pour Tintin.

		root@Vivo-AIO-27-V272UA:/home/elorri# mkdir PetitReporter
		root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -Rm u:tintin:rw- PetitReporter/
		root@Vivo-AIO-27-V272UA:/home/elorri# ll
		drwxrwxr-x+  2 root   root     4096 nov.   8 21:23  PetitReporter/
		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl PetitReporter/
		# file: PetitReporter/
		# owner: root
		# group: root
		user::rwx
		user:tintin:rw-
		group::r-x
		mask::rwx
		other::r-x
	
	Notes sur la commande setfacl -Rm u:tintin:rw- PetitReporter/
	
		-R pour récurssif, cela veut dire que pour les sous répertoire tintin aura également les droits donnés à celui-ci.
		-m pour modifier
		
	Voyons si tintin peut accéder à PetitReporter et y créer un répertoire
	
		tintin@Vivo-AIO-27-V272UA:~$ mkdir /home/elorri/PetitReporter/UnRepCreeParTintin
		mkdir: impossible de créer le répertoire «/home/elorri/PetitReporter/UnRepCreeParTintin»: Permission non accordée
		tintin@Vivo-AIO-27-V272UA:~$ 
	
	Ca aurait du marcher, je ne comprends pas pourquoi. 

Quelle commande utiliser pour l’héritage afin que chaque fichier nouvellement créés aient bien les droits lectures écriture pour l’utilisateur Tintin et aucun droits pour les autres ?

	Il faut ajouter un masque sur "o" cad "others"
	
		setfacl -dm u:Tintin:rw,o:--- PetitReporter/
		
Tester la commande setfacl avec l’option b sur le fichier article, à quoi sert elle ?

		-rw-r--r--+ 1 root root 50 nov.   8 21:03 article
		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article 
		# file: article
		# owner: root
		# group: root
		user::rw-
		user:tintin:rw-			#effective:r--
		group::r--
		mask::r--
		other::r--

		root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -b article 
		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article 
		# file: article
		# owner: root
		# group: root
		user::rw-
		group::r--
		other::r--
		root@Vivo-AIO-27-V272UA:/home/elorri# 
		
	setfacl -b a supprimé  toutes les valeurs d'ACL données à savoir ici
	
		les droits d'écriture de tintin
		le masque
	
Quelle est la commande pour supprimer uniquement l’ACL d’un utilisateur ?

	Remettons des droit a tintin avant de tester la commande

		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article 
		# file: article
		# owner: root
		# group: root
		user::rw-
		group::r--
		other::r--

		root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -m u:tintin:rw article
		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article 
		# file: article
		# owner: root
		# group: root
		user::rw-
		user:tintin:rw-
		group::r--
		mask::rw-
		other::r--
		
	Supprimmons les droits de tintin

		root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -x u:tintin
		Utilisation : setfacl [-bkndRLP] { -m|-M|-x|-X ... } file ...
		Essayer « setfacl --help » pour plus d'informations.
		root@Vivo-AIO-27-V272UA:/home/elorri# setfacl -x u:tintin article 
		root@Vivo-AIO-27-V272UA:/home/elorri# getfacl article 
		# file: article
		# owner: root
		# group: root
		user::rw-
		group::r--
		mask::r--
		other::r--
	