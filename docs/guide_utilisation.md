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

****

## Audits comparatifs: 

****

<br>

![alt text](../img/auditv1.png "Audit v1")  

<br>
<br>

![alt text](../img/auditv2.png "Audit v2")  

<br>
