javaee-poitiers-2014
======================

L'énonce du TP est disponible ici : https://github.com/mathieuancelin/javaee-poitiers-2014/wiki/Todo-App

Le squelette du code est disponible ici : https://github.com/mathieuancelin/javaee-poitiers-2014/raw/master/todo-tp.zip

Pour déployer votre TP sur le cloud, allez faire un tour du côté de chez CleverCloud : http://doc.clever-cloud.com/java/java-war/

Les slides de cours sont directement téléchargeable sur cette page :

* https://github.com/mathieuancelin/javaee-poitiers-2014/raw/master/01-Web.pdf
* https://github.com/mathieuancelin/javaee-poitiers-2014/raw/master/JavaEE7.pdf


Todo
========

L'objectif est de coder une application de type TODO list en utilisant le framework Play!

Les URLs
------------------------

* http://localhost:9000/ : affiche la page principale de l'application. Cette page est consituée d'un formulaire simple permettant de renseigner le nom d'une tâche à accomplir et du bouton pour créer la tâche ainsi que de la liste des tâches enregistrées dans la base de données. Chaque tâche possède une checkbox permettant de signaler si une tâche a été effectuée. Si c'est la cas, la tâche sera alors barrée. Un bouton permettra d'effacer les tâches faites.

* http://localhost:9000/tasks : URL accessible en POST, permet d'ajouter une nouvelle tâche à l'application. Cette URL sera utilisée via un appel ajax

* http://localhost:9000/tasks/{id} : URL accessible en POST, permet de mettre à jour une tâche (via un appel ajax) afin de changer son statut.

* http://localhost:9000/tasks : URL accessible en delete, efface toutes les tâches faite en base

* http://localhost:9000/tasks/{id}/delete : URL accessible en delete, efface une tache donnée

Composition de l'application
----------------------------

* 1 vue sous forme de fichier html
* 1 entité JPA représentant les tâches. Cette entité est très simple, elle comporte simplement un champ pour le nom de la tâche et un boolean pour son statut, ainsi qu'un id représentant la version raccourcie (automatiquement ajouté par Play)
* 1 contrôleur Play contenant les diverses méthodes executant la logique métier de l'application.

Guide de survie
------------------

installation de Play! Framework :

http://www.playframework.org/documentation/1.2.7install

configuration de l'IDE : 

http://www.playframework.org/documentation/1.2.7/ide

utilisation de la ligne de commande :

http://www.playframework.org/documentation/1.2.7cheatsheet/commandLine

utilisation des contrôleurs :

http://www.playframework.org/documentation/1.2.7/cheatsheet/controllers

utilisation des templates :

http://www.playframework.org/documentation/1.2.7/cheatsheet/templates

http://www.playframework.org/documentation/1.2.7/index : section built-in tags

utilisation des modèles :

http://www.playframework.org/documentation/1.2.7/cheatsheet/model

documentation complète : 

http://www.playframework.org/documentation/1.2.7/home


