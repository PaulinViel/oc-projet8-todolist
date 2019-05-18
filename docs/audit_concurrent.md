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

- Ici nous pouvons voir en partie d'ou vient ce temps de début d'affichage : les scripts et les images.

Dans la répartition du poids du ralentissement, le premier coupable est le script, il est clairement nécessaire de réduire sa taille et de l'optimiser autant que possible. Le second coupable est les images, il pourrait déjà etre utile de combiner les petites images dans une sprite CSS pour réduire le nombre de fichiers que le navigateur doit télécharger et donc accélèrer donc le chargement. On constate aussi que beaucoup d'images sont appelées par des requêtes externes, ce qui ralentis évidemment beaucoup le chargement du site. Si possible il vaudrait mieux les héberger dans le back-end si possible afin de limiter les calls externes. Pour les images non externes, il faudrait étudier la possibilité de les compresser, ou de changer leur format vers quelque chose de plus léger et optimiser

Il serait aussi très utile d'utiliser un système de mise en cache des différentes images permettra de gagner encore plus de temps. 

<br>

![alt text](../img/concurrentSpeed4.PNG)

<br>

- Dans ce tableau reprenant la répartition par domaines nous constatons plusieurs problèmes .

Premièrement, Jquery est chargé à chaque fois, plusieurs solutions sont possible : une mise à jour de Jquery -les version plus récentes sont bien plus performantes-, utiliser un fichier minifier -celui-ci étant moins lourd, le call sera plus rapide- ou utiliser du JavaScript ce qui éliminerait tout simplement le besoin de Jquery mais demanderait du temps de développemennt supplémentaire.

Deuxièmement, nous constatons qu'il y a beaucoup de calls externes dont l'utilité n'est pas assurée et qui ralentissent beaucoup le site pour un gain possiblement très faible. En particulier les calls automatiques vers les réseaux sociaux et tout les service Google. Si tout ces calls externes sont réellement essentiel, peut être pourrait-il être envisageable de déclencher certains d'entre eux grace a des évènements particulier et non systématiquement au chargement. Le mieux serait évidemment de réduire leur nombre.

<br>

Résumé des points à modifier pour améliorer la performance du site :

- Mettre à jour, minifier ou supprimer Jquery
- Optimiser le code JavaScript 
- Retravailler les images (réduire la taille, compresser, changer de format)
- Supprimer autant que possible les calls externes vers d'autres plateformes, ou au pire ne les déclencher que quand cela est nécessaire et non à chaque chargement.


## Audit du site

**Resumé**
***

Audit Lighthouse (extension Chrome) : 
<br>
![alt text](../img/auditresume.png)
<br>

**Performances**
***
<br>
Visiblement, des améliorations sont possibles ! 
<br>


Tout d'abord, attaquons-nous aux performances : 
<br>
<br>
![alt text](../img/concurrentperf.png)
<br>

Le soucis des render-blocking resources est assez problématique et parfois inévitable. En effet, dans notre cas, ces ressources bloquantes concernent le style (fonts google, css, et jquery css). Evidemment, il est possible de faire que le render se produise même si ces ressources ne sont pas chargées, mais dans ce cas il est problable que l'utilisateur expérience une page sans aucun style (aussi appelé FOUC ou 'Flash of Unstyled Content') ce qui est bien sûr à éviter. Il est généralement préférable de ne pas avoir ce FOUC visible, dans ce cas, le mieux est d'optimiser au possible les styles afin que leur chargement se apsse au plus vite (limite la taille et le nombre de fichier, réduire les calls sur des fonts externes ect).
Le format des images n'est pas otpimisé, des format plus récents de que le png permettent une meilleure compression et un téléchargement plus rapide des images. 

Grâce à cet audit, nous pouvons constater plusieurs problèmes majeurs :
Tout d'abord les performances générales peuvent être améliorées, cela est du aux soucis vus plus haut (calls externes, script non otpimiser, images trop lourdes ect).
<br>
Ensuite l'accessibilité laisse à désirer. Regarder l'audit plus en détail nous donne d'aurtes informations sur ce problème : 
- Le ratio de contrast en les couleurs en premier et second plan n'est pas assez élevé, c'est une mauvaise pratique, car un contraste trop faible peut rendre l'utilisation du site compliqué pour certains utilisateur (mal voyants, daltoniens ect), il est donc très important de régler ce problème. 
- Le résultat du test nous apprend aussi que certains Id ne sont pas uniques (en particulier dans des formulaires, tableaux ect), ce qui peut être problématique pour les bots en ligne par exemple, qui sauteront le 2nd id trouvé, seulement le premier sera "indexé". D'un point de vue code cela est aussi problématique et peut engendrer des dysfonctionnements.
- Il est aussi préférable d'attribuer un lang attribut au tag html, afin de référencer le langage principal utilisé.
- Nous constatons aussi que plusieurs images n'ont pas de alt attribut. Cet attribut permet par exemple d'aider à l'indexation dans les SEO (Search Engine Optimization), mais aussi de donner une description de l'image dans le cas ou celle-ci ne charge pas, ou encore pour les screen reader des non voyants. Même chose pour les formulaire et leur labels associés, ces labels ont le même intéret que les alt tags pour les images.
<br>

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







