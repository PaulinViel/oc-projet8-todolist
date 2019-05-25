# **Guide d'utilisation du projet todolis**

[1. Installation](#installation)  
[2. Fonctionnalités](#fonctionnalites)  
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

Nous allons voir dans le détail toutes les actions possible sur notre application.

![alt text](../img/todoAccueil.png "Accueil todo")  
![alt text](../img/todoActive.png "Active todo")  
![alt text](../img/todoComplete.png "Todo complété")  
![alt text](../img/todoCompleteAll.png "Todo all complétés")  
![alt text](../img/todoDelete.png "Surrpime todo")  
![alt text](../img/todoEdit.png "Edit todo")  
![alt text](../img/todoListItems.png "Liste todo")  
![alt text](../img/totoCmpleted.png "Todo complété")  

<br>
****

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
