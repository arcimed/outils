 # Développeur.se back

 ## Le “Back”, c’est quoi ?

 Le “backend” c’est ce que l’on appelle aussi “le cloud”, c’est en général là ou l’on effectue des traitements qui sont invisibles aux utilisateurs.

C’est l’endroit où l’on va pouvoir stoker toute sorte de données, de fichiers, de ressources qui seront téléchargées par nos utilisateurs et utilisatrices.

C’est ici que l’on aura nos bases de données, que l’on va définir nos APIs et générer des réponses aux formats HTML, JSON ou Xml.

Enfin, c’est ici que l’on aura des données qui seront stockées, agrégées, traitées, renvoyées.

## Prérequis à l’éco-conception du backend

### Sélectionner le bon hébergement

Avoir un espace disque sur le “cloud”, ce n’est pas très compliqué.

Avoir un espace sur internet, le plus vertueux possible, c’est déjà plus difficile. Pour faire au mieux, il faut aussi choisir l’hébergement qui sera le plus exigent sur son implication envers la planète.

Il y a là plusieurs questions à se poser :

* D’où vient l’électricité produite ?
* Provient-t-elle d’une source bas carbone ?
* Comment sont refroidies les salles de serveurs ?
* Comment sont gérés les composants obsolètes de l’hébergeur ?
* Ont-ils une seconde vie ?
* La chaleur générée par les serveurs a t-elle une autre utilité ?
* Quelle est la politique environnementale de mon hébergeur ?
  
Dans tous les cas, il ne faut pas oublier qu’un “hébergeur green” n’existe pas : chaque hébergeur consommera quand même des ressources et de l’énergie finale.


### Choisir son type de serveur, par rapport à son besoin
Avoir un espace vertueux sur le “cloud” est déjà moins compliqué.

Mais l’idéal reste d’avoir un espace vertueux ET bien dimensionné !

Il est inutile d’avoir un espace de plusieurs centaines de gigaoctet, si ce n’est que pour stoker un site statique de quelques mégaoctets.

Tout comme il est inutile d’avoir un site avec 32 Go de RAM, si tu n’as pas un trafic gigantesque, ou que tu n’exécutes pas de tâches de fond très lourdes.

Il faut agir avec sobriété lors de chaque étape de la conception d’un produit, c’est aussi le cas pour le choix de son infrastructure.



## Éco-concevoir son Backend

Tu as choisi le framework et le langage que tu utiliseras, ton projet back est déployable sur ton hébergement, c’est bon, tu peux commencer à coder \o/ . Mais tout en sobriété, en pensant à toutes les personnes qui téléchargeront tes ressources. Pour cela, il existe des tas de choses à mettre en place :

### Utilise un protocole HTTP récent

Le protocole HTTP/1 existe depuis les années 90.

Même s’il gère très bien la transmission d’informations, il y a eu des mises à jour qui rendent ce protocole obsolète. HTTP/2 et HTTP/3 (QUIC) sont opérationnels et améliorent (beaucoup) le temps de transfert des ressources entre le serveur et le client.

### Réduise les temps de traitements.

#### Encore du cache

Une ressource doit être téléchargée rapidement, elle doit prendre le moins de temps possible pour être générée. Il est possible d’optimiser nos traitements lourds en les mettant en cache, eux aussi. Au lieu de réeffectuer un traitement qui dure plusieurs minutes, tu stockes le résultat après le premier appel, que tu récupères pendant “x” temps (le temps de validité du traitement) pour les appels suivants.

#### Asynchronisme

Les temps de traitement peuvent également être réduits en effectuant des appels asynchrones et des traitements asynchrones. Il est conseillé de monitorer correctement ce type d’appel, vu que cela peut être à double tranchant : la vitesse du traitement initial peut drastiquement être réduite, mais les charges mémoires/CPU de la machine seront beaucoup plus sollicitées, au vu de l’exécution des traitements en parallèle.

### Utilise le stockage temporaire et les agrégats

Non, le stockage temporaire, ce n’est pas juste un fichier que l’on supprime après telle ou telle durée. De nos jours, de nombreuses bases de données gèrent ce que l’on appelle le “TTL” (Time to Live : la durée de vie).

Une donnée peut elle aussi avoir une durée de vie, il est même possible de l’agréger à une table d’agrégation lorsque celle-ci s’apprête à être détruite : il existe de nombreuses solutions pour optimiser nos bases de données et éviter qu’elles ne grossissent continuellement le long de la durée de vie de notre application.

Mongo DB, AWS Dynamo DB, REDIS, Oracle et Azure Document DB gèrent très bien le TTL.

### Ne requête que ce qui est utile

Cela semble évident, mais on constate encore trop d’appels, de jointures, de données récupérées qui ne servent… à rien!

Commencer par éviter le fameux Select * From myTable est une bonne chose, comme le fait d’éviter de faire des sous-requêtes, des jointures qui ne vont pas récupérer de données essentielles à votre traitement.

### Utilise le bon format d’API


REST ? SOAP ? GraphQL ? c’est à toi de choisir !

Cependant, il est judicieux de choisir un format qui puisse te renvoyer des données en effectuant le moins de requêtes possibles et en renvoyant des réponses les plus légères possibles.

On favorisera une sortie JSON à une sortie XML, qui restera beaucoup plus lourde, en intégrant un format de balisage qui n’est plus forcément utile aujourd’hui.


### Utilise les bons codes “HTTP”

Retourner une réponse ayant un code HTTP 200 au lieu d’un code HTTP 204 peut avoir un impact sur les personnes qui vont utiliser tes services : chaque code HTTP a une utilité, et doit être utilisé comme il se doit.

Si tu authentifies tes utilisateurs, ou que tu as différentes couches de caches, peut-être que de renvoyer juste un code HTTP 204 à tes appelants et une réponse vide peut suffire, vu que la réponse n’aura pas changée et aura déjà été envoyée (et sauvegardée) précédemment.

Cela n’évitera pas les appels à outrance à tes APIs, mais réduira drastiquement le poids des réponses envoyées : tant que ta réponse n’aura pas reçue de mise à jour, tu ne renverras qu’une page vide avec un code HTTP 204.

### Tout cacher !

Une fois que ton code est en place sur ton hébergement, des données seront à disposition par le biais d’une URL. Avant toute autre chose, il faut vérifier que tu aies une bonne politique de cache sur toutes les ressources qui sont exposées. Une politique de cache optimale va empêcher à tes utilisateurs de retélécharger une ressource qui n’a pas d’intérêt à l’être.

Il n’est en principe pas cohérent d’avoir une politique de cache similaire à toutes tes ressources ; une police d’écriture qui ne changera jamais n’aura pas la même politique de cache qu’une image, qui peut changer un peu plus fréquemment, qui n’aura pas non plus la même politique de cache que ta page HTML, que tes JS ou CSS qui changeront plus régulièrement.

La mise en cache doit être optimale pour que tes clients ne saturent pas ta bande passante en téléchargeant des ressources qui leur sont inutiles. Il est aussi possible de mettre en cache certains traitements, pour éviter de les recalculer à l’avenir.

### Compresse les données à bon escient

Après avoir défini la bonne “durée de vie” d’une ressource avant son prochain téléchargement, il faut maintenant l’optimiser, pour transférer le moins de données possibles sur le réseau. Pour cela, on peut utiliser la compression des ressources ( gzip ou brotli).

#### Activation du mod_deflate sous APACHE, qui gzip les ressources

    ``
    <IfModule mod_deflate.c>
    SetOutputFilter DEFLATE
    DeflateCompressionLevel 9
    </IfModule>

    <Location />
    AddOutputFilterByType DEFLATE text/plain
    AddOutputFilterByType DEFLATE text/html
    AddOutputFilterByType DEFLATE text/xml
    AddOutputFilterByType DEFLATE text/css
    AddOutputFilterByType DEFLATE image/svg+xml
    AddOutputFilterByType DEFLATE application/xml
    AddOutputFilterByType DEFLATE application/rss+xml
    AddOutputFilterByType DEFLATE application/x-javascript
    </Location>

    ``

La compression des données est idéale pour quasiment toutes les ressources, mais peut aussi perdre de son efficacité avec certains formats, comme le PNG qui est une ressource déjà compressée.

### Et alors, c’est tout ?

Pas du tout.

Tu viens de faire le minimum vital pour déployer un backend sobre, efficace et résilient, mais tu peux sûrement faire encore mieux en appliquant plusieurs autres bonnes pratiques “responsables” relatives à la sécurité ou à l’accessibilité.

## Ethique et sécurité

Côté back, tu es amené à gérer beaucoup de choses.

Il y transite un tas d’informations qu’il faut sécuriser. Mais avant de les sécuriser, il faut aussi se poser les bonnes questions : Est-ce que cette information est essentielle à mon application ? Dois-je réellement récupérer des events utilisateurs et les tracker toutes les 4 secondes ?

Il faut bien comprendre que moins tu auras à récupérer de données de tes utilisatrices et utilisateurs, moins tu auras à les sécuriser et à les traiter.

Néanmoins, que tu doives ou non récupérer des données confidentielles, il y a des choses à faire “coté Back” pour éviter les intrusions, les tentatives de récupération malveillantes, et pour être un peu plus conforme au RGPD (https://www.cnil.fr/fr/rgpd-par-ou-commencer).

### Chiffre ta connexion avec le client avec un certificat

C’est une des premières choses à faire pour sécuriser les échanges que l’on a entre front et back : l’ajout d’un certificat TSL (appelé plus communément “SSL”) permet de chiffrer la connexion, ce qui rend les échanges privés. Un utilisateur qui intercepte le trafic ne peut pas lire “en clair” ce qui se passe entre ton serveur et ton client.

Il est bon de savoir qu’un certificat n’est pas forcément payant : il est tout à fait possible d’utiliser https://letsencrypt.org/fr/ pour générer ces certificats et chiffrer la connexion de son application.

### Configure les bonnes en-têtes HTTP

Lorsque l’on crée une application Web, il y a un nombre incalculable d’échanges entre le front (coté client) et le serveur (coté back). Pour éviter et contrer les menaces attaquantes, l’OWASP (pour Open Web Application Security Project®) recommande de spécifier correctement une dizaine d’en-têtes de réponse. Heureusement pour nous, il est possible d’analyser tous les headers transmis via le site https://securityheaders.com/ qui te donnera un grade suivant le niveau de sécurité de ton site.

La majorité des headers et des règles sont définissables coté serveur via une configuration Apache ou NGINX, ou NodeJS, c’est à toi de mettre en place une bonne politique de sécurité pour tous les headers essentiels à la sécurité des données.

### Le HSTS (HTTP Strict Transport Security)

Une fois que le certificat SSL est en place, on peut forcer le navigateur à utiliser une connexion HTTPS pour toutes les ressources que l’on fournit sur notre domaine et sur nos sous-domaine. (Il faut faire attention à bien vérifier que le SSL est valable partout). La configuration du HSTS n’est pas très compliquée :

Voici la configuration Apache pour la mise en place du HSTS (HTTP Strict Transport Security) :


    ``
    <IfModule mod_headers.c>
        Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
    </IfModule>
    ``

### Et la mise en place de l’HSTS via NGINX:

    ``
    add_header Strict-Transport-Security max-age=31536000;
    ``

Ou sur NodeJS en utilisant la librairie helmet https://www.npmjs.com/package/helmet

    `` 
    const express = require("express");
    const helmet = require("helmet");

    const app = express();

    app.use(helmet());
    app.use(helmet.hsts());
    ``

### Le CSP (Content Security Policy)

La mise en place du CSP permet d’améliorer sa sécurité, notamment en détectant et réduisant certains types d’attaques, dont les attaques de Cross Site Scripting (XSS) et les injections de contenu. Sa mise en place est relativement simple une fois que l’on comprend les règles de gestion du CSP. Il faut prendre conscience qu’une mauvaise configuration du CSP peut empêcher le navigateur de télécharger ou d’exécuter le contenu de certains types de ressources !

Voici la mise en place d’une règle CSP default-src https: définissant que le navigateur n’exécutera pas les scripts inline, et forcera les ressources à se charger en HTTPS sous apache :

    `` 
    Header always set Content-Security-Policy "default-src https:"
    ``

Pour éviter de casser tout ton site, il y a deux moyens de tester la règle CSP appliquée :

On peut utiliser le header Content-Security-Policy-Report-Only ! Celui-ci à été conçu spécifiquement pour tester les règles CSP, il permet d’avertir que la règle ne passe pas, mais ne l’applique pas :
    
    ``
    Header always set Content-Security-Policy-Report-Only "default-src https:"
    ``
On peut aussi demander au client de tester la règle avec une balise méta : (Attention à ne pas la pousser en production 🙂)

### X-Content-Type-Options

Les ressources ont toutes un type spécifique, par exemple, une image sera sûrement de type image/jpeg pour le fichier minImage.jpg ou de type image/png pour le fichier monImage.png, une vidéo maVideo.mp4 aura surement un type video/mp4 et un fichier HTML un type text/html.

Pour éviter la manipulation des fichiers via le changement de type MIME (de faire qu’un fichier .php ou .js ne se cache pas derrière le type mime d’une image, et qu’on puisse parvenir à l’exécuter en changeant son type) on peut spécifier le header X-Content-Type-Options qui empêche la manipulation des type mime.

La configuration Apache :

    ``
    Header always set X-Content-Type-Options "nosniff"
    ``

La configuration NGINX :

    `` 
    add_header X-Content-Type-Options "nosniff" always;
    ``

### X-Frame-Options

Il est facilement possible d’intégrer du contenu d’un site sur un autre par le biais des balises <iframe></iframe> , <embed></embed> , <object></object> . Pour éviter qu’un site malveillant puisse intégrer ton contenu, tu peux définir une politique d’options de frame dans tes headers :

La configuration Apache :

    ``
    Header set X-Frame-Options "sameorigin" 
    ``

La configuration NGINX :

    `` 
    add_header X-Frame-Options sameorigin always;
    ``

### Supprime (ou change) ton header “server”

Par défaut, le header server retourne le type de serveur utilisé par ton infrastructure, si tu es sous Apache, la variable server renverra donc Apache. Ce header est indicatif, il n’est pas utile au bon fonctionnement de ton application. Pour éviter de faciliter la tâche à un utilisateur malveillant, mieux vaut le supprimer pour qu’il ne puisse pas profiter des failles potentielles de ton serveur.

### Crypte les données sensibles

Dans tous les cas, tu dois te dire que tout le monde pourra accéder à ta base de données, même si évidemment, ça ne sera pas le cas. Mais si ça l’était ? Quelles sont toutes les données qui sont sensibles dans ta base ? Qu’est-ce qui ne doit pas être lu par toutes les personnes ayant réussi à s’infiltrer ? Il faut penser à tout ça et utiliser des algorithmes de cryptage pour sécuriser au maximum les informations qu’il y a en base de données. Il existe des méthodes de cryptage dans chaque langage informatique (ou presque) et de nombreux bundles, qui sont beaucoup plus performants existent.

Avec le langage PHP, il est possible d’utiliser https://github.com/defuse/php-encryption par exemple.

### Prépare toi aux injections SQL

Qui dit requêtes SQL dit injection SQL. Toutes les requêtes que tu exécutes sur ta base de données peuvent potentiellement permettre à un utilisateur maîtrisant le SQL (et les injections) de s’y infiltrer. Il faut donc veiller à bien préparer les requêtes que tu exécutes et de sécuriser un maximum les informations que tu vas insérer en base pour éviter les injections.

En général, les ORMs que l’on utilise permettent déjà d’éviter les risques d’injection SQL.

Mais, on le sait : tout le monde n’utilise pas un ORM :

* d’un point de vue éco conceptuel, il n’est pas forcément utile d’utiliser un ORM s’il l’on fait juste une ou deux requêtes sur une base de données.
* d’un point de vue performance, utiliser un ORM sera aussi moins performant que d’exécuter son SQL avec les fonctions natives de nos langages.
  
Il faut donc bien faire la part des choses, et éviter au maximum les infiltrations et les problèmes de sécurité : La sécurité sera toujours à prendre en compte avant l’éco-conception et la performance.

Pour éviter les injections, tu peux commencer par “échapper” les caractères spéciaux, pour qu’ils s’enregistrent avec un format différent en base de données. Par exemple, en PHP, il est possible d’utiliser https://www.php.net/manual/fr/mysqli.real-escape-string.php .


### Limite les accès aux données


Limiter les accès est une très bonne pratique de manière générale. Est-ce que cet utilisateur a le droit de lire cette table en base de données ? A-t-il possibilité d’écrire dans celle-ci ? Est-ce que mon application doit avoir accès en écriture à l’intégralité du serveur ? Puis-je restreindre certaines permissions à un dossier ?

Toutes ces questions sont à se poser pour limiter au maximum les accès à tes données : pour un accès SSH au serveur ou un accès à la base de données, il est possible de créer plusieurs utilisateurs avec des restrictions et droits différents.



