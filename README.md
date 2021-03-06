# Projet 8 Openclassrooms - Todo List // Reprenez un projet existant

[Lien vers le guide d'utilisation](docs/guide_utilisation.md)

# Etape 1 : Corrigez les bugs

- Première erreur : faute de frappe dans le fichier [controller.js](js/controller.js) :  

`	Controller.prototype.adddItem = function (title) 	`

Après correction :  

`	Controller.prototype.addItem = function (title) 	`

<br>

- Deuxième erreur : pas d'Id sur l'input "toggle-all", le "for" du label ne reconnaissait donc pas sa cible, et par conséquent la flèche "Toggle all" ne fonctionnait pas. Dans le fichier [index.html](index.html) :

`<input class="toggle-all" type="checkbox">` après correction : `<input id="toggle-all" type="checkbox">`

<br>

- Troisième erreur : conflit potentiel entre deux IDs (il est possible d'avoir des doublons) dans le fichier [store.js](js/store.js) :

		Store.prototype.save = function (updateData, callback, id) {
		var data = JSON.parse(localStorage[this._dbName]);
		var todos = data.todos;

		callback = callback || function () {};

		// Generate an ID
	    var newId = ""; 
	    var charset = "0123456789";

        for (var i = 0; i < 6; i++) {
     		newId += charset.charAt(Math.floor(Math.random() * charset.length));
		}

		// If an ID was actually given, find the item and update each property
		if (id) {
			for (var i = 0; i < todos.length; i++) {
				if (todos[i].id === id) {
					for (var key in updateData) {
						todos[i][key] = updateData[key];
					}
					break;
				}
			}

			localStorage[this._dbName] = JSON.stringify(data);
			callback.call(this, todos);
		} else {

    		// Assign an ID
			updateData.id = parseInt(newId);
    

			todos.push(updateData);
			localStorage[this._dbName] = JSON.stringify(data);
			callback.call(this, [updateData]);
		}
		};

Après correction :

    Store.prototype.save = function (updateData, callback, id) {
        const data = JSON.parse(localStorage[this._dbName]);
        const todos = data.todos;

        callback = callback || function () {
        };

        // If an ID was actually given, find the item and update each property
        if (id) {
            for (let i = 0; i < todos.length; i++) {
                if (todos[i].id === id) {
                    for (const key in updateData) {
                        todos[i][key] = updateData[key];
                    }
                    break;
                }
            }

            localStorage[this._dbName] = JSON.stringify(data);
            callback.call(this, todos);
        } else {

            // Generate an ID, changed the previous function since it was possible to get the same ID twice, using Date.now() prevents this issue.
            // Assign an ID
            updateData.id = Date.now();

            todos.push(updateData);
            localStorage[this._dbName] = JSON.stringify(data);
            callback.call(this, [updateData]);
        }
    };


- Suppression complète de la logique avec les var newId et charset, à la place, nous utilisons Date.now() qui générera un Id unique en fonctionne de la date/heure actuelle (à la milliseconde près).

<br>

- En cas de scaling de l'application (utilisations par plusieurs dizaines de personnes sur un même compte par exemple), pour assurer -autant que possible- un Id unique dans le cas ou deux personnes générerait un nouveau todo à la même milliseconde, il est possible d'utiliser par exemple l'algorithme de Fisher–Yates, qui demande bien plus de ressources mais est l'une des solutions les plus adaptées pour générer un iD unique. On peut aussi envisager d'ajouter d'utiliser Date.now() avec en plus une variable similaire à celle utilisée à l'orogine. Ou encore en fonction de la base de données un simple Id auto-incrémental.

<br>

<br>

D'autres améliorations ont été réalisées :

<br>

Dans le fichier [controller.js](js/controller.js), deux boucles while sont inutiles :
       
        while (title[0] === " ") {
            title = title.slice(1);
        }
        
et
        
         while (title[title.length-1] === " ") {
            title = title.slice(0, -1);
        }
        
- Le check sur title[0] et title[title.length-1] se faisant sur une string vide, il n'y a donc aucune raison de slice()

Dans le fichier [store.js](js/store.js), une boucle for est inutile :

    Store.prototype.remove = function (id, callback) {
		    var data = JSON.parse(localStorage[this._dbName]);
		    var todos = data.todos;
		    var todoId;
		
		    for (var i = 0; i < todos.length; i++) {
		    	if (todos[i].id == id) {
			    	todoId = todos[i].id;
		    	}
		    }

		    for (var i = 0; i < todos.length; i++) {
		    	if (todos[i].id == todoId) {
			    	todos.splice(i, 1);
		    	}
		    }

	    	localStorage[this._dbName] = JSON.stringify(data);
		    callback.call(this, todos);
	    };
      
Après correction : 

    Store.prototype.remove = function (id, callback) {
            const data = JSON.parse(localStorage[this._dbName]);
            const todos = data.todos;

            for (let i = 0; i < todos.length; i++) {
                if (todos[i].id === id) {
                   todos.splice(i, 1);
               }
            }
    
           localStorage[this._dbName] = JSON.stringify(data);
           callback.call(this, todos);
       };

- La première boucle for servant simplement à attribuer à todoId la valeur de todos[i].id, celle-ci n'est pas nécessaire vu que la seconde boucle permet d'obtenir le même résultat en utilisant directement l'argument id reçu.

<br>
        
## Etape 2 : Où sont les tests ?!

Les tests ont été ajoutés directement dans le fichier [ControllerSpec](test/ControllerSpec.js).

Les différents tests modifiés sont trouvables aux lignes :  

| Numero de la Ligne |                        Nom du Test                              |   
| :------------      |             :-------------:                                     |     
| l.62               | 'should show entries on start-up'                               | 
| l.92               | 'should show active entries'                                    | 
| l.103              | 'should show completed entries'                                 | 
| l.156              | 'should highlight "All" filter by default'                      | 
| l.168              | 'should highlight "Active" filter when switching to active view'| 
| l.180              | 'should toggle all todos to completed'                          | 
| l.194              | 'should update the view'                                        | 
| l.209              | 'should add a new todo to the model'                            | 
| l.256              | 'should remove an entry from the model'                         | 

<br>

## Etape 3 : Optimisez la performance

Réalisation d'un audit de performance sur site concurrent -300 à 500 mots-.  

L'audit complet est disponible [ici](docs/audit_concurrent.md).

<br>

## Etape 4 : Améliorez le projet

Documentation complète de l'application réalisée.  

Disponible [ici](docs/guide_utilisation.md).
