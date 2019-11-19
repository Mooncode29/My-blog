---
layout: post  
title: Tutoriel récupérer des images aléatoires sur Lorem picsum et les mettre en fond d'écran avec Node.js
---

Dans ce tutoriel, nous allons écrire un petit programme avec Node.js qui consiste à récupérer une image sur internet et le mettre en tant que fond d'écran. A titre personnel,la dernière où fois j'ai fais du Node.js remonte à l'époque où j'étais encore en formation développeur Web en 2016. Depuis, je n'ai pas vraiment eu d'occasions pour le pratiquer davantage. A travers ce tuto et , j'ai donc décidé de remettre le nez dedans. Et tenez-vous bien, ça ne sera que le début de probablement d'autres tutos que je vais réaliser sur cette techno et dont je me ferai le plaisir de vous les partager au fur et à mésure. Trève de bavardage, rentrons dans le vif du sujet ! 

##  Les Prérequis :   
- Connaissance en Javascript
- ES6 

## Première étape : Mise en place de l'environnement de travail 
- Installer npm

- [Installer Node.js](https://nodejs.org/fr/) . La version que j'ai à l'heure où j'écris ce blog est la `v12.13.0`. Mon OS est Linux Ubuntu 18.04.1

- Créer le dossier : donner un petit nom à votre projet .
- Créer le fichier qui va contenir nos codes sources . Pour ma part, je l'ai nommé `app.js`.
- Pour le versionning avec git, créer un fichier `.gitignore` pour mettre les dosiers ou fichiers qu'il n'est pas souhaitable de vérsionner, notamment le dossier `node modules`  
- Initialiser npm en tapant sur votre terminal `npm init` . Npm est le gestionnaire officiel de paquets pour Node.js. Il est indispensable pour installer les dépendances dont on aura besoin sur ce projet.   
Après cette étape, vous remarquerez qu'un dossier `node_modules` s'est ajouté à la racine de votre projet , ainsi qu'un fichier `package.json`.  


## Deuxième étape : Installation des dépendances  

Dans ce projet, nous allons utiliser trois modules : `fs`, `request` et `child_process` .  
- Les modules `fs` (File System) et `child_process` sont déjà inclus dans le core de Node.js et pourront donc être utilisé directement via la fonction `require` qu'on verra plus en détails un peu plus tard dans ce tutuo.  
- `npm i request --save ` pour installer le module `request` et l'ajouter dans le package.json  
- Nous allons également installer Nodemon, un outil en ligne de commande qui vous évite de devoir relancer votre application à chaque changement. Il surveille le moindre changement sur votre système de fichier et relance automatiquement le process.
Vous  pouvez l'installer :
    - soit globalement en tapant `npm install nodemon -g` . Ce que j'ai fais pour ce tuto et que je vous conseille de faire. Pour le lancer une fois que vous avez commencé à coder, tapez `nodemon <nom_de_votre_fichier>`
    - soit en local en tapant `npm install nodemon --save-dev`. 
    
A ce stade, nous avons tout ce dont avons besoin pour passer à la prochaine étape : commencer à coder !   

## Troisième étape : Ecrire notre programme  

Tous nos codes vont être écris dans le fichier `app.js`.

Vous vous rappelez, un peu plus haut je vous ai parlé de modules . La première chose qu'on va faire est d'appeler nos modules au début de notre fichier :  
- `fs` ce module fournit plusieurs fonctionnalités très utiles pour interagir avec le système de fichier . Il n'a pas besoin d'être installé comme je vous l'ai dis précédemment. Il suffit tout simplement d'utiliser require pour l'utiliser.
- `child_process` fait également partie du core de Node.js donc pas besoin de l'installer. 


![image-title-here](/assets/images/appel-modules.png){:class="img-responsive"}

Voyons maintenant dans les détails le contenu de la fonction `downloadImage` :   

![image-title-here](/assets/images/fonction-downloadImage.png){:class="img-responsive"}    
Elle prend 3 paramètres :   


- url : l'url de la ressource où on veut faire la requête,  
 - filePath : le fichier de destination, 
  - cb : un callback 

On crée un stream de nature Writable. Ce dernier permet  d'écrire un contenu sous forme de flux et de recevoir les informations sous forme de petits blocs plus digetste pour la mémoire.
![image-title-here](/assets/images/createWritestream.png){:class="img-responsive"} 

 On fait la requête pour lancer le téléchargement.   

![image-title-here](/assets/images/myreq.png){:class="img-responsive"}     

Nous vérifions la validité du code de réponse Http réçu.

![image-title-here](/assets/images/myreq-check-response.png){:class="img-responsive"} 

 Nous  faisons appel à l'évènement `error` pour gérer le cas où notre requête rencontre une erreur. Nous effaçons le fichier partiellement écrit avec `fs.unslik()`. Nous passons ensuite l'erreur au callback.    

![image-title-here](/assets/images/myreq-error.png){:class="img-responsive"} 

La methode `pipe()` nous permet d'écrire  le fichier directement téléchargé.  
![image-title-here](/assets/images/pipe-req.png){:class="img-responsive"} 

Lorsque le téléchargement est terminé , nous appellons le callback. 
![image-title-here](/assets/images/file-finish.png){:class="img-responsive"} 

Une fois que le le fichier est complètement téléchargé, nous pouvons lancer la commande qui permet de mettre le l'image télécharé en tant qu'image de fond de notre écran.
![image-title-here](/assets/images/file-finish.png){:class="img-responsive"} 

Si une erreur survient lors de l'écriture du fichier , nous l'effaçons puis nous passons l'erreur au callback  
![image-title-here](/assets/images/file-on-error.png){:class="img-responsive"} 

Voilà, nous pouvons maintenant utiliser cette fonction comme ceci : 

![image-title-here](/assets/images/utilisation-fonction.png){:class="img-responsive"} 

Nous passons donc à cette fonction une URL. Vous remarquerez dans l'URL le query string `?random` qui permet de récupérer des images aléatoires sur le site de [lorem picsum](https://picsum.photos/) , en second paramètre l'emplacement du fichier une fois téléchargé. J'ai crée une variable path pour le stocker et en dernier un callback pour savoir quand c'est terminé et si des erreurs ont survenu.

