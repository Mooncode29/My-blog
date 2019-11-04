---
layout: post
title: "Invalider le cache du navigateur"
---

Vous êtes en train de développer un site, vous avez fait les enièmes modifications CSS demandées par le chef de projet. Vous avez bien testé en local, ça marche bien.
Seulement, une fois que vous avez dis au chef de projet de tester à son tour, bim! Il vous dit qu'il ne vois pas de changement. 
Et là vous lui dites : "As-tu vidé le cache ?".  
Il est en effet de la responsabilité du developpeur d'épargner cette tâche à son chef de projet.

Avant de vous dire ce qu'il faut faire dans ce cas, une définition de ce qu'est le cache du navigateur me paraît utile.

Le cache du navigateur est tout simplement ce qui lui permet de sauvegarder les données et ressources nécessaires à l'affichage des pages web (images, feuilles de style, Javascript) de sorte qu'elles ne soient chargées qu'une seule fois . Cela lui permet d'économiser la bande passante. Ainsi, lorsque vous consultez à nouveau la page web, elle se charge plus rapidement.   

Voici comment vous pouvez contourner ce comportement du navigateur et impacter ainsi vos modifications sur votre site :   
- soit  versionner le nom de votre fichier. Par exemple `style-v2.css`  
- soit versionner le chemin du fichier. Par exemple `/v2/style.css`

Grâce à ces numéros de versions uniques, le navigateur comprendra qu'il s'agit d'une nouvelle version de vos fichiers . Par conséquent, au lieu de récupérer les anciens fichiers du cache, le navigateur va faire une requête sur le serveur d'origine pour les nouveaux fichiers. 
