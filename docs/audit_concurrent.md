# **Audit de performance du site todolistme.net**

[1. Technologies externes](#technologies-externes)  
[2. Performance du site](#performance-du-site)  
[3. Audit du site](#audit-du-site)  
[4. Organisation du site](#organisation-du-site)  



## Technologies externes

****

L'utilisation de WhatsRun, nous a permit de pouvoir analyser les technologies utilisés par le site :  

<br>

![alt text](../img/Capture.PNG "Technologies utilisées sur todolistme.net")  

<br>

**Request Map**
***

La request map de todolist.net nous permet d'observer l'ensemble des interactions avec parties tiers.
Nous pouvons donc facilement constater d'ou viennent une partie des soucis de chargement et de ralentissement du site. 

<br>

![alt text](../img/requestmap.png "Request Map de totolistme")  
<br> 

## Performance du site

Plusieurs outils en ligne sont disponibles pour nous réaliser des audits et obtenir le condensé des informations nécessaire, ici nous avons utilisé Dareboost, en plus de l'inspecteur du navigateur Chrome et de Lighthouse.

**Temps d'affichage**
****

Tout d'abord nous allons nous intéresser au temps d'affichage, composante critique de l'expérience utilisateur et très bon indicateur de problèmes sous-jacents dans l'application.

<br>

Premier rapport (Dareboost):

<br>

![alt text](../img/concurrentspeed.PNG)  

<br>

Second rapport (LightHouse):

<br>

![alt text](../img/concurrentSpeed2.PNG)  

<br>
- Après observation de ces deux exemples nous constatons des différences, en particulier le début d'affichage, Dareboost se situe à 0.87sec alors que celui de LightHouse se situe à 1.6sec. Il est normal d'avoir des différences, y comprit en utilisant le même outil. Malgré ces différences, les deux sont d'accord sur un point : la fin de chargement est trop longue, 3.40 secs pour Dareboost et 5.4secs pour LightHouse. Une fois encore nous constatons des différences, mais même le meilleurs cas reste bien trop long pour une application relativement simple.

<br>

![alt text](../img/concurrentSpeed3.PNG)

<br>

Ici nous pouvons voir en partie d'ou vient ce temps de début d'affichage : les scripts et les images.

Dans la répartition du poids du ralentissement, le premier coupable est le script, il est clairement nécessaire de réduire sa taille et de l'optimiser autant que possible. Le second coupable est les images, il pourrait déjà etre utile de combiner les petites images dans une sprite CSS pour réduire le nombre de fichiers que le navigateur doit télécharger et donc accélèrer donc le chargement. On constate aussi que beaucoup d'images sont appelées par des requêtes externes, ce qui ralentis évidemment beaucoup le chargement du site. Si possible il vaudrait mieux les héberger dans le back-end si possible afin de limiter les calls externes. 



En outre, la mise en cache des différentes images permettra de gagner encore plus de temps 
(via un fichier en htaccess)

<br>

On peut voir que Jquery est chargé à chaque fois aussi (cf. image suivante)

<br>

![alt text](../images/jquery.png)

![alt text](../images/jquery_coverage.png)


<br>

Pour améliorer ce point ci, on peut :

| Améliorations                    |     Gain                                                                                         |
| :------------                    | :-------------:                                                                                  | 
|   Update la version de JQUERY    |   Correction de bugs divers, des problèmes de performance + Augmente la rapidité d'execution     |
|   Utiliser du javascript pur     |   Economie de temps --> Plus de chargement de Jquery à chaque fois                               |
|   Minifier Jquery-ui             |   Chargement plus rapide de la page car poids des fichiers moins importants                      |


En résumé pour améliorer la performance du site, il faudra faire :

| Améliorations                     |     Gain                                                                                         | Difficultés (sur 5) |
| :------------                     | :-------------:                                                                                  | :-------------:     | 
|   Update la version de JQUERY     |   Correction de bugs divers, des problèmes de performance + Augmente la rapidité d'execution     | :star:              |
|   Utiliser du javascript pur      |   Economie de temps --> Plus de chargement de Jquery à chaque fois                               | :star: :star: :star:|
|   Compression des images          | Economie de temps --> poids des images plus légers                                               | :star:              |
|   Utilisation du cache            | Economie de temps --> moins de chargement intempestif                                            | :star: :star:       |
|   Minifier Jquery-ui              |   Chargement plus rapide de la page car poids des fichiers moins importants                      | :star: :star:       |


## Audit du site

**Resumé**
***
![alt text](../images/performance.png)
<br>

On peut voir que d'après l'audit de la console Chrome, le site nécessite une amélioration au niveau de l'accesibilité mais aussi
au niveau de l'application web progressive (PWA = Application Web qui permet à un utilisateur d'avoir une
 expérience utilisateur similaire à celle d'une application mobile).  
 Il ne faudra pas négliger les autres parties qui peuvent être essentielles 
 pour être toujours plus performants  
<br>

**Performance**
***
![alt text](../images/performance2.png)  
<br>

La majorité des tests sont passés. En effet, on peut voir qu'il y a 75% des tests effectués qui sont validés.  
Les améliorations qui sont proposés par le site sont entre autre:
* Utiliser le cache du navigateur pour les fichiers qui sont long à charger (telle que les images),
* Enlever le CSS inutile,
* Utiliser des images au bon format et au bon poids.  
<br>

**Application Web Progressive**
***
![alt text](../images/pwa.png)  
<br>

Seulement 35% des tests sont passés. Notre concurrent n'as donc pas développé une Progressive Web App. 
Ceci pourra être une bonne chose de développer une Progressive Web app afin de se démarquer des concurrents.

<br>


**Accessibilité**
***
![alt text](../images/accessibility.png)  
<br>

L'accessibilité de notre concurrent n'est pas exceptionnelle. En effet, on peut voir que seulement 47% des 
tests passent. Il s'agit d'un des points importants à faire afin de se démarquer d'eux. 
Les points majeurs à améliorer sont:                
 - Ajouter un attribut langue dans la balise HTML pour que le lecteur d'écran puisse lire dans la bonne langue,
 - Ajouter des attributs alt (=texte alternatif) sur les différentes images pour permettre d'améliorer 
   le référencement du site mais aussi de retranscrire avec le lecteur d'acran le texte,
- Améliorer le contrast entre le background et les textes afin de permettre au plus grand nombre de lire 
  sans probleme,  
 Tous ses élèments s'ils sont améliorés vont permettre à notre application d'être plus accesible 
pour les personnes en situation d'handicap.   
<br>

**Bonne pratique**
***
![alt text](../images/best_pratices.png)  
<br>  

La majorité des tests sont passés sur cette catégorie (73%).  
Pourtant, pour améliorer les performances et la modernité du site,
il ne faudrait pas négliger l'update de la librairie Jquery qui contient une faille.  
En outre, l'utilisation de l'HTTPS permettra au site d'être plus sécurisé, 
d'être mieux référencé sur Google (et donc bénéficier d'un meilleur référencement) 
mais aussi d'être plus rapide à charger.  
<br> 
**SEO**

![alt text](../images/SEO.png)  
<br>

Un SEO (Search Engine Optimization) permet en utilisant un ensemble de technique 
d'améliorer le référencement naturel. Ici, le site possède 78% de tests réussis 
mais il y a toujours des axes d'améliorations comme:
- Utiliser une police dont la taille est supérieur à 12px afin que les utilisateurs 
sur mobiles ne soient pas obligés de zoomer,
- Ajouter un tag <meta name="viewport"> pour que le site soit optimisés sur les mobiles.







