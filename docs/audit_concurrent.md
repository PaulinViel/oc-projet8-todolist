# **Audit de performance du site todolistme.net**

[1. Organisation du site](#organisation-du-site)  
[2. Performance du site](#performance-du-site)  
[3. Audit du site](#audit-du-site)  
[4. Organisation du site](#organisation-du-site)  



## Technologies externes

****

Grâce à WhatsRun, on peut connaitre les différentes technologies utilisés par le site :  

<br>

![alt text](../img/Capture.PNG "Technologies utilisées sur todolistme.net")  

<br>

**Request Map**
***

Le mapping du concurrent permet aussi de connaitre l'ensemble des Thirds Parties chargées. Cela permet de 
se rendre compte de la chaîne de chargement non maitrisée ainsi que des possibles fuites de données.

<br>

![alt text](../images/request_map.png "Request Map de totolistme")  
<br> 

## Performance du site

**Temps d'affichage**
****

Le temps d'affichage d'un site est un bon indicateur de la performance du site. 
Sur ce site, il pourrait être amélioré:  
A 1,28 secondes, le site commence à s'afficher mais il faut attendre 2.46 secondes 
afin que le site s'affiche complètement

<br>

![alt text](../images/1,28.png)  

<br>

![alt text](../images/2,46.png)  

<br>

On peut voir que le background est très long à charger (cf. image suivante)

<br>

![alt text](../images/imagelongue.png)

<br>

Pour réduire le temps d'affichage, la bonne technique serait de réduire l'image au minimum puis de la compresser
 et ensuite d'utiliser le background-repeat en CSS. Ceci permettra d'avoir une image avec un poids
 plus négligeable et d'accelerer le chargement de la page .  
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







