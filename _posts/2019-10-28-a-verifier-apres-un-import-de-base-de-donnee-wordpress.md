---
layout: post
title: "Vérifier l'URL après avoir importé une base de données Wordpress"
---

Je me suis retrouvée avec des erreurs de type `Ivalid ssl request` après avoir importé une base de données  et lancé le serveur en local sur des projets Wordpress. Ce genre d'erreur apparaît parce que Wordpress a déjà été configuré sur l'ancien URL qui utilise par exemple un certificat SSL . Alors que localement , vous avez une URL en http.

Pour éviter de vous retrouver dans la même situation, la première chose que vous devez faire est de changer l'URL de votre site. Pour cela, vous avez deux options : 

* Option 1 : Changer l 'URL directement dans votre base de données  
Pour  mon cas, j'utilise [mysql Workbench](https://www.mysql.com/fr/products/workbench/). 
Une fois connecté sur Mysql Workbench : 
     * sélectionner la base de données de votre projet dans le panneau à gauche.  
     * Cliquer sur `Tables` . Cliquer ensuite sur `wp_options`
     * répérez les lignes `siteurl` et `home`  
     * Double cliquer sur chaque ligne pour l'éditer  
     * modifier l'URL en saisissant la nouvelle. Par exemple `http://localhost:8080` 
     * Cliquer sur `Apply` en bas à droite . Effectuer la même chose pour `siteurl` et `homeurl`    
     
     Vous pouvez maintenant relancer votre serveur et vous connecter à vous connecter sur `/wp-login.php`  

* Option 2 :  Changer l'URL dans le fichier `wp-config.php` de votre projet.  
Ouvrir le fichier wp-config.php et ajouter les lignes de codes suivantes :   
`define('WP_HOME', 'http://exemple.com');`  
`define('WP_SITEURL', 'http://exemple.com');`  
   
