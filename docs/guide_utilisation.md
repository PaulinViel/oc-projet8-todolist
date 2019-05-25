# **Guide d'utilisation du projet todolis**

[1. Installation](#installation)  
[2. Fonctionnalités](#fonctionnalités)  
[3. Fonctionnement interne](#fonctionnement-interne)  
[4. Audits comparatifs](#audit-comparatifs)  


L'application Todolist permet de créer et maintenir une liste de "todos", les marquer en tant que complet, et les filtrer. L'application est réalisée en Vanilla Javascript et n'a pas de dépendency, à part todomvc-common utilisé comme base (https://github.com/tastejs/todomvc-common).

Les tests sont réalisé à l'aide du standalone [Jasmine](https://jasmine.github.io/). Tout les tests peuvent être trouvés dans `/test/ControlloerSpec.js`. Pour utiliser les tests, vous devrez ouvrir `/test/SpecRunner.html` dans votre navigateur.

<br>

## Installation:

<br>

Téléchargez ou copiez ce projet sur votre ordinateur.

Cliquez sur le bouton "Clone or download" en haut à droite du projet. Puis cliquez sur l'icone "copy to clipboard". Enfin, ouvrez votre terminal et utilisez la commande git : 

`git clone https://github.com/PaulinViel/oc-projet8-todolist.git`

Vous pouvez aussi directement télécharger le fichier ZIP depuis le bouton "Download ZIP".

ici vous copiez le contenu du projet Github "oc-projet8-todolist" sur votre machine dans un dossier appelé comme le projet (oc-projet8-todolist).

Vous devriez pouvoir dès maintenant ouvrir le fichier `index.html` qui s'ouvrira dans votre navigateur et vous permettra d'utiliser l'application. Si jamais un problème se présente, il sera peut être nécessaire lancer `npm install` pour se mettre à jour. 

<br>

****

## Fonctionnalités: 

<br>

Cette application permet de gérer une liste de tâches (todo-list) sans devoir enregistrer de compte. Il est cenpendant nécessaire d'utiliser le même navigateur pour récupérer les données précédemment utilisées.

Il est possible de créer des todos, les éditer, les supprimer, les terminer, les réactiver et les filtrer par statut.

<br>

Nous allons voir dans le détail toutes les actions possible sur notre application :

<br>

### Page d'accueil

<br>

Voici la page d'accueil de l'application Todo. C'est une page très simple où l'on peut voir un champ texte (input) servant à ajouter de nouveaux todos.

<br>

![alt text](../img/todoAccueil.png "Accueil todo")  

<br>

### Création d'une liste

<br>

Ajouter un nouveau todo dans la liste est très simple. Il suffit d'écrire le titre du todo dans le champs texte ('What needs to be done?'), puis, soit appuyer sur la touche "Entrée", soit cliquer en dehors du champs sélectionné afin de valider l'entrée.

<br>

![alt text](../img/todoListItems.png "Liste todo")  

<br>

### Modifier un todo

<br>

Pour modifier un todo, double-cliquez sur son titre, vous passerez en mode "édition", le todo sélectionné aura une bordure grise et votre curseur se trouvera dans le champs de titre, comme vu ci-dessous. A partir de là vous pouvez modifier le titre de votre todo en validant de la même façon que vu précédemment ("Entrée" ou "Click" en dehors du champs). Dans le cas ou vous souhaiteriez  annuler votre modification avant d'avoir validation, appuyer sur "Echap", l'ancien titre sera restauré. 

<br>

![alt text](../img/todoEdit.png "Edit todo")  

<br>

### Terminer un todo

<br>

Pour terminer un todo (le marquer complété), il suffit de cliquer sur l'icône à gauche du titre de celui-ci, représenté par un cercle gris. Si vous avez cliqué au bon endroit, la bordure du cercle deviendra plus foncée, une flèche verte apparaîtra au centre de ce dernier, et le titre du todo complété sera barré et rendu plus clair. Vous pouvez annulé la complétion d'un todo en cliquant une fois de plus sur le cercle. 

<br>

![alt text](../img/todoComplete.png "Todo complété")  

<br>

Cliquer sur le lien "Completed" se situant en bas de la fenêtre, entre "Active" et "Clear completed" (quand celui-ci est visible) permet d'aller sur une page montrant tout les todos marqués comme complétés.
Lorsqu'un ou plusieurs todo sont complétés, un lien "Clear completed" apparait en bas à droite de la fenêtre. Cliquer sur ce lien supprimera tout les todos marqués comme "complétés" de toutes les pages ("All", "Completed") et ce de manière manière définitive.

<br>

![alt text](../img/totoCmpleted.png "Todo complété")  

<br>

Cliquer sur le lien "Active", situé entre "All" et "Completed", permet de voir tout vos todos actifs (non marqués comme "complété")

<br>

![alt text](../img/todoActive.png "Active todo")  

<br>

### Complétion de tout les todos

<br>

Cliquer sur la flèche se situant à gauche du champs d'ajout de titre de todo "What needs to be done?" permet de marqué tout les todos comme marqués, que ceux-ci soient déjà marqués ou non. 

<br>

![alt text](../img/todoCompleteAll.png "Todo all complétés")  

<br>

### Supprimer un todo 

<br>

Il y a deux façons de supprimer un/des todos.

Si le/les todos ont été marqués comme "complétés", cliquer sur "Clear completed" les supprimera définitivement.
Dans le cas ou vous souhaiteriez supprimer un seul todo, complété ou non, vous pouvez cliquer sur la croix marron qui apparaît au survol d'un todo. Cette action supprimera définitivement le todo et il ne sera pas récupérable, il est préférable de ne supprimer des todos avec cette fonction qu'en cas d'erreur.

<br>

![alt text](../img/todoDelete.png "Surrpime todo")  

<br>

## Fonctionnement interne: 

<br>

### Vue d'ensemble

<br>

L'arborescence suivante présente l'architecture des dossiers principaux du projet.
``OpenClassrooms-Projet-8-To-do-List-Javascript
|
│ index.html
│
├─── js
│       app.js
│       controller.js
│       helpers.js
│       model.js
│       store.js
│       template.js
│       view.js
│
├─── node_modules
│
└─── test
        ControllerSpec.js
        SpecRunner.html``

L’application est organisée selon une architecture MVC (Modèle - Vue - Contrôleur).

MVC
L’objectif de ce patron est de séparer la logique du code en trois parties distinctes :
• Le modèle: Il contient la logique métier mais aussi il contient les données à afficher. (sql)
• La vue: Elle contient la présentation graphique de l'application. (html)
• Le contrôleur: Il contient la logique concernant les actions effectuées par l'utilisateur.
De plus, il assure le lien entre le modèle et la vue. (javascript)

App.js
App.js permet d'instancier l'application grâce à la classe Todo.

setView(): En fonction de l'adresse actuelle, cela permet de changer la vue.

Controller.js
Controller.js permet en fonction des actions réalisées par l'utilisateur de modifier la vue et le modèle.

setView(): Permet de charger et initialise la vue.

showAll(): Permet de récupèrer les tâches et les affiche dans la liste. Au départ, elle est décochée.

showActive(): Permet de montrer toutes les tâches actives.

showCompleted(): Permet de montrer toutes les tâches complètes.

addItem(): Permet d'ajouter une tâche (donc utilisé chaque fois). Cela permettra de changer le DOM et de sauvegarder la nouvelle tâche.

editItem(): Permet d'éditer la tâche.

editItemSave(): Permet de confirmer l'édition de la tâche.

editItemCancel(): Permet d'annuler l'édition de la tâche.

removeItem(): Permet de supprimer la tâche grâce à son ID dans le DOM mais aussi le storage.

removeCompletedItems(): Permet de supprimer toutes les tâches finis du DOM et du storage.

toggleComplete(): Permet de modifier le statut d’une tâche dont l’id est passé en paramètre.

toggleAll(): Permet de modifier le statut de toutes les checkboxes (on ou off). Il suffit de les passer dans l'objet voulu.

_updateCount(): Permet de mettre à jour en fonction du nombre de tâches à effectuer les différents endroits de la page.

_filter(): Permet de filtrer la liste des tâches.

_updateFilterState(): Permet de mettre à jour le filtre.

Helper.js
Helper.js permet d'avoir une aide pour la manipulation du DOM. Cela permet donc de ne pas utiliser des librairies.

window.qs: Query Selector, il permet de récuperer les différents éléments grâce à son sélecteur CSS.

window.qsa: Query selector all, il permet de récupèrer tous les éléments grâce aux selecteurs CSS.

window.$on: Il permet de lier à addEventListener un élément voulu.

window.$delegate: Il permet de lier pour tous les éléments correspondant au sélecteur un gestionnaire d'événement.

window.$parent: Il permet à partir d'un tag de trouver l'élément parent d'un élément.

Model.js
Model.js permet de créer un nouvel objet appellé Model et de manipuler les informations dans le local storage.

create(): Permet de créer le nouveau modèle.

read(): Permet de trouver et de retourner un modèle dans l'espace de stockage. Si jamais aucune reqûete n'est spécifiée, cela ne retourne rien.

update(): Cela permet de mettre à jour une tâche.

remove(): Cela permet d'enlever une tâche.

removeAll(): Permet d'enlever toutes les tâches.

getCount(): permet d'avoir le nombre de tâche.

Store.js
Le store.js permet de créer une base de donnée avec la classe Store qui sera stockée dans le local storage.

find(): Permet de trouver les tâches à partir d'une requête comme un objet JS.

findAll(): Permet de trouver toutes les tâches de l'espace de stockage.

save(): Permet de sauvegarder une tâche dans la BDD soit en l'updatant soit en la créant.

remove(): Permet de supprimer une tâche de la BDD grâce à son ID.

drop(): Permet de supprimer la BDD actuelle et crée une nouvelle.

Template.js
Permet de créer le modèle par défaut avec la classe Template.

show(): Permet de créer les balises

de chaque tâche et de les retourner dans l'application.
itemCounter(): Permet de connaitre le nombre de tâches restantes grâce à un compteur.

clearCompletedButton(): Permet de mettre à jour avec le texte suivant "Clear completed" si le nombre de tâche complété est supérieur à 0.

View.js
View.js permet de manipuler le DOM et fait la liaison entre le model et le controller. On va utiliser dans les différentes méthodes les sélecteurs de helper.js

_removeItem: Permet de supprimer une tâche.

_clearCompletedButton: Permet d'afficher le bouton 'Clear completed'.

_setFilter(): Permet de filtrer suivant la page les résultats voulus.

elementComplete(): Permet de définir si une tâche a bien été effectué.

_editItem(): Permet lors de l'édiion d'une tâche de l'afficher.

_editItemDone(): Permet d'afficher la tâche après son édition.

render(): Permet de gérer l'affichage grâce aux fonctions suivantes:

showEntries: Permet d'afficher les tâches.

removeItem: Permet de supprimer une tâche.

updateElementCount: Permet de mettre à jour le nombre de tâches.

clearCompletedButton: Permet de mettre à jour l'affichage du 'Clear completed'.

contentBlockVisibility: Permet de choisir si on veut l'affichage du footer.

toggleAll: Permet de basculer toutes les tâches.

setFilter: Permet d'afficher le filtre demandé.

clearNewTodo: Permet de supprimer les informations dans le champs de saisie.

elementComplete: Permet d'afficher une tâche terminée.

editItem: Permet de choisir une tâche pour l'éditer.

editItemDone: Permet de fermer la tâche en cours d'édition.

_itemId(): Permet de retourner l'ID de la tâche.

_bindItemEditDone(): Permet de gérer l'arrêt de l'édition de la tâche.

_bindItemEditCancel(): Permet de gérer l'annulation de l'édition de la tâche.

bind(): Permet de gérer l'utilisationd de Javascript suivant l'événement retourné.

****

## Audits comparatifs: 

****

<br>

![alt text](../img/auditv1.png "Audit v1")  

<br>
<br>

![alt text](../img/auditv2.png "Audit v2")  

<br>
