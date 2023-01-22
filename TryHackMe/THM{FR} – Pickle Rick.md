<h2>Phase d'exploration :</h2>
Une fois sur le site, on inspecte le code html et on y trouve un commentaire intéressant en bas de l’inspecteur :
![Image1](https://user-images.githubusercontent.com/112400062/213931165-bd79d9c5-f512-4d41-9e4c-eaba1edbfcbc.png)

On note l’username : R1ckRul3s

<hr>

Dans la balise  <head> du code, on y retrouve des liens :
 ![image](https://user-images.githubusercontent.com/112400062/213931217-6863806e-48d0-4010-a434-9926b6eb044b.png)

 
Ces liens mènent à une page précise qui est /assets. On rentre donc le répertoire dans l’url pour tester si l’on peut accéder à la page et on atterrit ici :
 ![image](https://user-images.githubusercontent.com/112400062/213931290-69695576-adf8-4351-9a2f-a17366eb8ae6.png)

 
Parfait, nous avons donc l’accès au répertoire contenant des fichiers intéressant. 
On y retrouve fail.gif, picklerick.gif et portal.jpg qui n’était pas disponible avant.
Après inspection du code source des trois images, aucune ne semble donner suite à quelque chose d’intéressant.




On teste maintenant d’accéder à la page robots.txt comme suis :
 
 ![image](https://user-images.githubusercontent.com/112400062/213932424-e92276c2-c90f-4483-8f5a-cfc01864624f.png)

 
On atterrit sur une page nous donnant juste :

 ![image](https://user-images.githubusercontent.com/112400062/213932870-6fff4840-b424-4d0e-8618-7ff0e40aa133.png)

 
On tente alors d’accéder au fichier qui pourrait être nommé ainsi :

 ![image](https://user-images.githubusercontent.com/112400062/213932874-c7da660e-6f1f-48a4-b888-15ad33c8aaf4.png)

Mais on ne trouve rien.

On passe maintenant à la manière forte avec gobuster, en rajoutant dans notre wordlist le mot que l’on a trouvé dans la page robots.txt :
 
Le résultat nous retourne :
 
La page d’accueil ne contient donc pas plus de répertoire que ceux que nous avons déjà découvert.
On recommence gobuster, mais cette fois-ci dans le répertoire /assets :
 
Aucun résultat




Revenons-en à nos moutons, la page principale du site web nous demande de se connecter à l’ordinateur de Rick. On suit donc son conseil à la lettre et pour ce faire, on scan le serveur web pour y trouver ssh un port ssh :
 
Bingo, le port 22 soit ssh est ouvert !
Sachant que l’on a trouvé un nom d’utilisateur (R1ckRul3s) et un potentiel mot de passe (Wubbalubbadubdub), on tente de s’y connecter :
 
Impossible de passer par le port…

On continue en scannant le serveur web avec Nikto :
 
Le scan nous retourne quelque chose de très intéressant -> une page /login.php
On tente donc de l’afficher dans le navigateur :
 

First Flag !
La page nous affiche donc :
 
Ce qui est parfait, même pas besoin de se connecter en ssh.
On rentre donc le nom d’utilisateur et le mot de passe ce qui nous amènes ici :
 
En rentrant la commande « ls » on trouve :
 



On ouvre donc le premier fichier .txt :
 
La commande semble désactiver. On utilise alors l’alternative « less » :
 
Le premier flag est donc mr. meeseek hair !

Deuxième flag :
On continue en affichant le fichier clue.txt qui nous donne un indice :
 
On continue donc en regardant dans les fichiers système disponible (30 minutes plus tard), dans le fichier home à la racine, on trouve un répertoire intéressant : 
 
Qui contient lui-même le second ingrédient :
 
On affiche le contenue du fichier :
 
Ce qui nous donne notre deuxième flag : 
1 jerry tear

3ème flag
Comme nous n’avons pas d’indice pour le troisième flag, on recommence nos recherches comme au début, en inspectant le code source, nous trouvons ce commentaire :
 
Vm1wR1UxTnRWa2RUV0d4VFlrZFNjRlV3V2t0alJsWnlWbXQwVkUxV1duaFZNakExVkcxS1NHVkliRmhoTVhCb1ZsWmFWMVpWTVVWaGVqQT0==
Ça forme est tout de suite identifiable, ce message est encodé en base64. On le décode en ligne avec le site -> dcode base64 et le résultat nous retourne encore un message coder, en continuant comme ça 7 fois le résultat est « rabbit hole » … On s’est fait avoir.

Après plusieurs recherche rien n’est concluant donc on continue de chercher dans les fichiers de l’ordinateur de Rick, on utilise la commande sudo -l pour savoir quels sont les commandes que l’on peut utiliser :
 
Visiblement toute les commandes sont autorisées. On liste donc les fichiers du répertoire root : 
 
Parfait, on a trouvé le 3ème flag. On affiche son contenu :
 
Le 3ème ingrédient est : fleeb juice 
