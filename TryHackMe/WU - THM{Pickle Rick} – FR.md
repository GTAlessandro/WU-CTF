<h2>Phase d'exploration :</h2>

Une fois sur le site, on inspecte le code html et on y trouve un commentaire intéressant en bas de l’inspecteur :

![image](https://user-images.githubusercontent.com/112400062/213932974-904c6442-a511-4e59-a225-643fb3a94297.png)

On note l’username : R1ckRul3s


<hr>


Dans la balise  <head> du code, on y retrouve des liens :
 
 ![image](https://user-images.githubusercontent.com/112400062/213931217-6863806e-48d0-4010-a434-9926b6eb044b.png)

 
Ces liens mènent à une page précise qui est /assets. On rentre donc le répertoire dans l’url pour tester si l’on peut accéder à la page et on atterrit ici :
 
 ![image](https://user-images.githubusercontent.com/112400062/213931290-69695576-adf8-4351-9a2f-a17366eb8ae6.png)

 
Parfait, nous avons donc l’accès au répertoire contenant des fichiers intéressant. 
On y retrouve fail.gif, picklerick.gif et portal.jpg qui n’était pas disponible avant.
Après inspection du code source des trois images, aucune ne semble donner suite à quelque chose d’intéressant.

 
 <hr>
 
 
On teste maintenant d’accéder à la page robots.txt comme suis :
 
 ![image](https://user-images.githubusercontent.com/112400062/213932424-e92276c2-c90f-4483-8f5a-cfc01864624f.png)

 
On atterrit sur une page nous donnant juste:
 
 ![image](https://user-images.githubusercontent.com/112400062/213932870-6fff4840-b424-4d0e-8618-7ff0e40aa133.png)

 
On tente alors d’accéder au fichier qui pourrait être nommé ainsi :
 
 ![image](https://user-images.githubusercontent.com/112400062/213932874-c7da660e-6f1f-48a4-b888-15ad33c8aaf4.png)

Mais on ne trouve rien.
 
 
 <hr>

 
On passe maintenant à la manière forte avec gobuster, en rajoutant dans notre wordlist le mot que l’on a trouvé dans la page robots.txt :
 
 ![image](https://user-images.githubusercontent.com/112400062/213933322-e4bcb09f-90c7-4032-bda4-6e71ba6f4bc6.png)

 
Le résultat nous retourne :
 
 ![image](https://user-images.githubusercontent.com/112400062/213933325-f24341d1-436c-4055-9fa2-dbf69f8b7c33.png)

 
La page d’accueil ne contient donc pas plus de répertoire que ceux que nous avons déjà découvert.
On recommence gobuster, mais cette fois-ci dans le répertoire /assets :
 
 ![image](https://user-images.githubusercontent.com/112400062/213933334-2a7e049d-9dc6-42f9-851a-982bcc4bf7bf.png)

 
Aucun résultat

 
<hr>

 
Revenons-en à nos moutons, la page principale du site web nous demande de se connecter à l’ordinateur de Rick. On suit donc son conseil à la lettre et pour ce faire, on scan le serveur web pour y trouver un port ssh :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942368-70972b22-a0bf-4f66-b184-8bb75b46234d.png)

 
Bingo, le port 22 soit ssh est ouvert !
Sachant que l’on a trouvé un nom d’utilisateur (R1ckRul3s) et un potentiel mot de passe (Wubbalubbadubdub), on tente de s’y connecter :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942381-ea0793ab-3e6d-4d10-b6f3-6b529b7956d5.png)

 
Impossible de passer par le port…
 
 
 <hr>

 
On continue en scannant le serveur web avec Nikto :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942393-d961b09c-1a03-4a3f-b0e4-8b23b7180182.png)
 
 Le scan nous retourne quelque chose de très intéressant -> une page /login.php
 
 
 <hr>
 

 <h2>First Flag !</h2>
On tente donc de l’afficher dans le navigateur :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942397-57f866ae-631b-4bc8-bc25-0da9d7c63fdc.png)


 La page nous affiche donc :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942479-53581f69-b804-4734-abac-16dc34068a0a.png)

Ce qui est parfait, même pas besoin de se connecter en ssh.
On rentre donc le nom d’utilisateur et le mot de passe ce qui nous amènes ici :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942486-497e766b-2edd-462c-b9ba-1ae7a4ac2bb5.png)


 En rentrant la commande « ls » on trouve :
 
![image](https://user-images.githubusercontent.com/112400062/213942489-0dbf5449-f880-4772-ba45-caa161ff94c5.png)


 On ouvre donc le premier fichier .txt :
 
 ![image](https://user-images.githubusercontent.com/112400062/213942496-81a7b50a-fa55-49b9-8e6b-b469342d4444.png)

 
La commande semble désactiver. On utilise alors l’alternative « less »
Le premier flag est trouvé !

 
 <hr>
 
 
<h2>Deuxième flag !</h2>
On continue en affichant le fichier clue.txt qui nous donne un indice :
  
  ![image](https://user-images.githubusercontent.com/112400062/213942733-debddf0a-9957-44e0-af33-8d5ed0750a1c.png)

 
On continue donc en regardant dans les fichiers système disponible (30 minutes plus tard), dans le fichier home à la racine, on trouve un répertoire intéressant : 
  
  ![image](https://user-images.githubusercontent.com/112400062/213942753-cc6c8356-8e82-4171-bdf3-1a7099b470eb.png)

 
Qui contient lui-même le second ingrédient :
  
  ![image](https://user-images.githubusercontent.com/112400062/213942755-853f35d9-6359-43ec-ac8e-03ad1642a43a.png)

 
On affiche le contenue du fichier, ce qui nous donne notre deuxième flag
  
  
  <hr>

  
  <h2>Troisième flag</h2>
Comme nous n’avons pas d’indice pour le troisième flag, on recommence nos recherches comme au début, en inspectant le code source, nous trouvons ce commentaire :
  
  ![image](https://user-images.githubusercontent.com/112400062/213942807-ae9d44b7-a83f-4e46-a1af-f85f00de341e.png)

 
Vm1wR1UxTnRWa2RUV0d4VFlrZFNjRlV3V2t0alJsWnlWbXQwVkUxV1duaFZNakExVkcxS1NHVkliRmhoTVhCb1ZsWmFWMVpWTVVWaGVqQT0==
Ça forme est tout de suite identifiable, ce message est encodé en base64. On le décode en ligne avec le site -> dcode base64 et le résultat nous retourne encore un message coder, en continuant comme ça 7 fois le résultat est « rabbit hole » … On s’est fait avoir.

Après plusieurs recherche rien n’est concluant donc on continue de chercher dans les fichiers de l’ordinateur de Rick, on utilise la commande sudo -l pour savoir quels sont les commandes que l’on peut utiliser :
  ![image](https://user-images.githubusercontent.com/112400062/213942818-68df2b81-f67a-4396-be0e-225f823a73ce.png)

 
Visiblement toute les commandes sont autorisées. On liste donc les fichiers du répertoire root : 
  
  ![image](https://user-images.githubusercontent.com/112400062/213942826-f3770ffa-9b7a-42f9-a6b3-213dac20ddc0.png)

 
Parfait, on a trouvé le 3ème flag. On l'affiche comme ceci :
 ![image](https://user-images.githubusercontent.com/112400062/214363986-640b5de9-4d76-4406-8519-c475ecef7a46.png)

 
