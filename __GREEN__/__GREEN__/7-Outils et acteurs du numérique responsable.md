# Outils et acteurs du numérique responsable

## Les outils

Il existe une multitude d’outils utiles pour rendre le numérique beaucoup plus responsable. Des analyseurs statiques, pour analyser la structure de ton DOM, aux profileurs, qui peuvent entièrement profiler tes applications et éviter de surconsommer des ressources inutiles.

### Les outils utiles à l’éco-conception 

#### EcoIndex (https://www.ecoindex.fr)

EcoIndex est un outil communautaire, gratuit et transparent qui, pour une URL donnée, permet d’évaluer :

* sa performance environnementale absolue à l’aide d’un score sur 100 (higher is better) ;
* sa performance environnementale relative à l’aide d’une note de A à G ;
* l’empreinte technique de la page (poids, complexité, etc) ;
* l’empreinte environnementale associée (gaz à effet de serre et eau).
  
L’objectif d’EcoIndex est d’aider le plus grand nombre à prendre conscience de l’impact environnemental de l’internet et de proposer des solutions concrètes pour réduire cet impact. EcoIndex te propose donc une analyse automatique de premier niveau pour t’aider à identifier rapidement et gratuitement des sites web / services en ligne à ausculter en priorité.


### Les outils d’analyse de qualité et de performance
#### Dareboost (https://www.dareboost.com/fr)

Du test de performance au monitoring synthétique de pages comme de parcours utilisateurs, Dareboost est un outil tout-en-un dédié à la performance web. C’est un outil conçu pour faciliter la collaboration entre professionnels du Web, et renforcer leur capacité d’action sur les problématiques de performance web.

Les rapports générés par Dareboost sont sûrement les plus complets que tu pourras trouver à travers la multitude d’outils sur le web. À partir de l’analyse statique d’une URL, le rapport est capable de retrouver une multitude de composants, de plugins ou de modules utilisés, et de t’orienter vers de bonnes pratiques te permettant de mieux les utiliser. Il est aussi intéressant de voir que cet outil te spécifie les ressources qu’il serait utile d’améliorer et pourquoi ! Les explications sont complètes, et en français. Si une page française n’existe pas, une ressource en anglais sera présentée. Dans tous les cas, tu auras accès à beaucoup de documentation, d’explications, et d’exemples d’amélioration.

#### Lighthouse (https://web.dev/)

Lightouse est un outil d’analyse statique développé par Google permettant d’obtenir des bonnes pratiques et des conseils sur les pages de ton site internet à partir de son URL. Ces conseils sont séparés en cinq parties distinctes :

* La performance
* Les bonnes pratiques
* l’accessibilité
* le SEO
* la partie PWA.

Un grade allant de 0 à 100 est décerné aux pages internet pour chacune des catégories et de nombreux conseils sont proposés pour améliorer les points faibles de ces pages.

Lightouse est aussi disponible dans la console “d’outils de développeur” sur tous les navigateurs ayant une base “chromium” (Google Chrome, Brave, Microsoft Edge). Les rapports peuvent donc être effectués localement sur une machine de développement, mais il faut prendre en compte que les performances analysées peuvent êtres perturbées par les modules que tu utilises quotidiennement sur ta machine. Malgré ce soucis, les tests via les outils de développement restent très intéressants pour analyser les URLs qui ne sont pas publiques (comme les intranets).


#### GTMetrix (https://gtmetrix.com/)

GTMetrix est un outil d’analyse statique utilisant une partie des données de Lighthouse pour générer son rapport. Le site donne également un grade aux pages testées, mais permet de garder un historique avec l’espace de connexion. Il est également possible d’avoir des conseils différents et complémentaires à ceux de Lightouse et de Dareboost pour améliorer l’état des pages testées.

Cet outil est intéressant puisqu’il permet (gratuitement) de brider la connexion (en 2G/3G) et/ou de tester via différents CDN pour voir comment se comporte nos pages internet sur des connexions bas-débit, ou à travers le monde.

#### WebPageTest (https://www.webpagetest.org/)

WebPageTest est sûrement un des outils de performance web les plus connus. Via une analyse statique de la page, sur trois itérations, il permet d’obtenir un nombre d’information phénoménal sur les différentes données du waterfall, et sur l’état du cache de chacune des ressources de la page. WebPageTest effectue également une multitude de tests sur des sites partenaires pour obtenir une note générale de l’état de ton site via différentes catégories (Sécurité, Taux de compression d’image, Cache statique…). Les notes sont généralement définies entre le grade “A+” (le meilleur) et “F” (le pire).

#### Snyk.io (https://snyk.io/)

WebPageTest exécute, conjointement à son propre test, un test de vulnérabilité web via la plateforme Snyk.io, C’est ce test qui te donne une note en matière de sécurité de 0 à 100, cette note est convertie d’un grade “A+” à “F”. Snyk permet de déceler les failles des packages que te utilises, et de t’avertir des problèmes existants.

#### Cloudinary Image Analysis

Un autre point fort de WebPageTest est de proposer, via un onglet dédié, d’effectuer un test d’analyse d’image via le site cloudinary. Ce site est très intéressant puisqu’il permet de vérifier l’état de compression de chaque image de la page, de les tester dans d’autres formats (PNG, SVG, WEBP, AVIF), et de te proposer de télécharger chacune des images générées, en te spécifiant quel est le meilleur choix pour chaque image. Il est facilement possible, via ce site, de réduire énormément le poids de tes pages, en particulier si les images ne sont pas encore dans des format modernes.

#### Blackfire ([blackfire.io](https://www.blackfire.io/))


Blackfire est un outil de profilage spécifique aux langages PHP / Go / Python. Cet outil est payant, mais est très efficace pour améliorer ces environnements si tu utilises un de ces langages. Le profiling d’une page te permettra de savoir exactement par où passe ta page pour obtenir le contenu attendu à travers les fonctions et méthodes de ton code et des différents frameworks/modules que tu utilises. Il est alors très simple de déceler les problèmes de ton applicatif, que cela soit dû à un trop grand nombre d’appel HTTP (vers une API, ou une base de données), un problème de surconsommation de mémoire vive, ou une trop grosse utilisation du CPU.

#### DotTrace (https://www.jetbrains.com/fr-fr/profiler/) / DotMemory

DotTrace et DotMemory sont également des outils de profilage très puissants, dédiés aux applications .NET.

Ces outils permettent le profilage et l’analyse des applications permettant de déceler toutes les problématiques qui pourraient surconsommer différentes ressources par ton application.

#### Les outils d’optimisation d’assets


Il existe une multitude d’outils sur Internet qui peuvent te permettre de changer la qualité de ressources originales ou leur format, pour réduire drastiquement la taille du contenu envoyé. Le but n’est pas d’avoir un visuel réduit au maximum, qui ne comble plus son besoin d’être sur ton site, mais d’avoir un visuel le plus léger possible, qui reste suffisamment qualitatif pour remplir son rôle.

#### Squoosh (https://squoosh.app/)

Squoosh est un outil en ligne te permettant d’optimiser tes images, en changeant leur format, ou leur qualité. La force de cet applicatif est de pouvoir visuellement constater les différences de tes changements avec l’image originale.

#### Optimizilla (https://imagecompressor.com/)
Optimizilla est un logiciel permettant de réduire énormément tes images de type JPEG, GIF et PNG en gardant la qualité originale de tes images.

#### Handbrake (https://handbrake.fr/)
Handbrake est un utilitaire installable sur tous les OS (Linux, Mac et Windows) permettant de changer les formats de tes fichiers vidéo et audio.

### Les outils utiles à la sécurité numérique

Bien qu’une analyse des vulnérabilité SNYK est effectuée lors d’un test WebPageTest, cela ne suffit pas. Il existe heureusement des sites dédiés à l’aspect “sécurité” de nos sites internet :

#### Observatory Mozilla
L’observatoire de Mozilla est un outil très complet qui va analyser plusieurs points de sécurité avec les headers renvoyés par tes applications web. Cet outil est très pratique pour connaitre l’état du chiffrement de ton certificat SSL, et pour voir si ton site est protégé contre certaines pratiques (CSP, XSS..)

### Les outils utiles à l’accessibilité numérique

### Wave ( https://wave.webaim.org/)
Wave est un outil d’analyse statique qui te permet d’avoir un retour visuel sur les problématiques d’accessibilité que tu as sur tes pages.











