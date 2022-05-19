# Développeur.se front

## Le “Front”, c’est quoi ?

Le “front” c’est ce qui fait référence à l’ensemble des éléments visibles et accessibles à un utilisateur sur une application ou un site web. Il s’occupe de mettre en forme l’affichage (couleurs, taille des textes, images, animations, etc) et charge les différents scripts utiles au fonctionnement des applications. C’est en quelque sorte la partie visible de l’iceberg, en tant que principal vecteur sur lequel une développeuse ou un développeur peut agir pour le développement responsable.

En général, c’est le front qui consomme le plus de ressources : le CPU, la mémoire vive et le stockage. C’est sur ces parties qu’il faudra travailler en priorité d’un point de vu éco-conceptuel. D’autres aspects ne sont pas à négliger, le front peut avoir un impact important sur l’accessibilité numérique et la sécurité des données.

Nous allons voir ensemble comment agir pour rendre l’applicatif le plus responsable possible en respectant les normes d’éco-conception, de performance informatique, d’accessibilité et de sécurité.

## Éco-concevoir son Front-end

L’éco-conception du front-end est importante, et il existe une multitude de pratiques permettant de réduire les impacts de nos applications au quotidien, essentiellement en agissant avec sobriété (réduire les appels réseaux, le nombre de ressources, stocker intelligemment nos assets…). Les bonnes pratiques d’éco-conception web se basent, en général, sur de bonnes pratiques de performance web.

Ce n’est cependant pas vrai pour toutes les bonnes pratiques de webPerf : certaines peuvent en effet améliorer la rapidité de ton site internet, en ayant beaucoup plus d’impact que si tu ne les avais pas appliquées, mais d’autres ne sont pas vraiment bénéfiques. C’est par exemple le cas de la mise en place de la balise <link rel="prerender" href="ton_autre_page">.

Ajouter cette balise pointant sur une autre page sur ton site internet va demander à ton navigateur de pré-télécharger les ressources de cette autre page, dans le cas où l’utilisateur s’y rend.

Si c’est le cas, vu que le navigateur aura pré-rendu la page, elle s’affichera très rapidement : c’est une bonne pratique de performance. Néanmoins, si l’utilisateur ne s’y rend pas, tu auras demandé à ton navigateur de pré-télécharger des tas de ressources inutiles : c’est donc aussi une mauvaise pratique en terme d’éco-conception numérique. Il faut bien faire attention à comprendre ce que font les tips (ou astuces) de performance web avant de les appliquer. Voici une liste de bonnes pratiques que tu peux utiliser sans crainte :

### Sois sobre avec le HTML, le CSS et le Javascript
#### Le HTML
On parle souvent de sobriété de ressources, de suppression d’images, de vidéos, mais pas assez de la sobriété de code. En effet, réduire son HTML, c’est la base, et une bonne pratique qui permet une augmentation de la rapidité de rendu de ta page. Le HTML est composé de balises différentes comportant plusieurs niveaux de nœuds et d’arborescence. Google recommande (https://web.dev/dom-size/) de ne pas avoir plus de 1400 éléments HTML dans ta page et de ne pas dépasser 32 niveaux de profondeur. Plus ton HTML sera lourd et complexe, plus le navigateur mettra du temps à interpréter la page que tu souhaites afficher à tes utilisateurs. Pour vérifier le respect de cette règle, il est possible d’effectuer une analyse statique de ton site via l’outil https://web.dev/measure/ .

Le HTML est aussi critique car l’organisation des ressources peut bloquer le rendu utilisateur, rendre la page inactive et inutilisable le temps que les scripts s’exécutent ou que les ressources se téléchargent. Il faut bien comprendre et apprendre à utiliser le HTML du mieux que l’on puisse, utiliser les bonnes balises et les bons attributs à bon escient. En effet, si tu rends tous tes scripts asynchrones, et que tu précharges toutes les ressources de ta page, la performance de cette dernière risque d’en pâtir et de ne pas être optimale, bien que dans une majorité de cas, utiliser de l’asynchronisme et du pré-chargement peuvent être de bonnes idées.

#### Les CSS
Le CSS, c’est pareil : on ne télécharge pas des bibliothèques entières pour afficher un style spécifique pour deux boutons !

On essaye d’avoir les styles utiles à l’affichage de la page, très rapidement, même s’ils sont inlines dans la page HTML entre les balises <style></style>

On ne les inclue pas dans des fichiers trop gros mettant beaucoup de temps à se télécharger. C’est la base pour avoir un rendu rapide à l’utilisateur. Comme pour le reste on agit avec sobriété et on évite de doublonner les sélecteurs dans de multiples fichiers pour éviter d’effectuer des “repaint” incessants, qui, comme pour le JS, peuvent consommer beaucoup de CPU.

Beaucoup de développeurs et de développeuses utilisent Bootstrap pour sa grille ou ses styles alors qu’aujourd’hui, avec les CSS 3, natifs sur la plupart des navigateurs, il est possible d’utiliser les grids ou les flexboxs.

Trop de CSS, c’est un rendu de page plus lent car la génération du CSSTree va prendre plus de temps qu’une page ayant un CSS réduit. Il faut éviter au maximum les effets et les animations pour améliorer l’expérience utilisateur, le fonctionnement similaire entre navigateurs, et la surconsommation de ressources sur le périphérique.

#### Le JavaScript
En premier lieu, il faut savoir que le javascript n’est pas utile au fonctionnement d’un site internet. Oui, il est utilisé à travers de nombreux frameworks qui le rendent indispensable, mais ce n’est pas un cas absolu. De nombreuses personnes (entre 3 et 6% de la population) naviguent sur internet en désactivant le JavaScript : c’est faisable… et même agréable.

Les principaux navigateurs de recherche le permettent, tout comme une multitude de sites. L’expérience utilisateur peut même s’en trouver améliorée vu que le Javascript ne fera rien : les animations, traqueurs, et autres scripts généralement trop lourds ne vont ni se parser, ni s’exécuter. La page s’affichera vite, sans avoir à attendre l’exécution d’une multitude de scripts avant de pouvoir enfin interagir avec la page.

Bien que la désactivation du Javascript reste “marginale”, il faut idéalement que ton site réponde lorsque le javascript est désactivé. Le mieux étant qu’il reste fonctionnel sans javascript, le moins pire étant d’avertir tes utilisateurs de réactiver le JS pour naviguer de manière optimale sur ton site. C’est à cela que peut servir la balise <noscript></noscript> :

    ``
    <noscript>Pour une experience optimale, veuillez réactiver JavaScript!</noscript>
    ``
Comme quoi, on peut être extrêmement sobre avec le Javascript, vu qu’on peut très bien avoir un site internet qui n’en utilise pas du tout.

Contrairement aux idées reçues, les animations que l’on peut avoir sur une page internet peuvent très bien être faites en CSS sans Javascript (surtout depuis HTML5 et CSS3). Ainsi, faire un “accordéon”, un “indicateur de scroll”, une “lightbox” ou un système de tabulation peut être intégralement conçu avec du CSS. De nombreux exemples sont présents sur le site http://youmightnotneedjs.com/ .

### Javascript allégé et vanilla.js
Dans une bonne partie des cas, il est possible de ne pas utiliser Javascript. Pour faire des animations, tu n’es pas obligé de télécharger tout jQuery pour afficher un carrousel qui peut être fait en CSS ! Mais c’est aussi le cas pour de nombreuses choses bien particulières. Utiliser des sélecteurs jQuery est bien moins performant que d’utiliser les sélecteurs natifs du JavaScript, et ce avec tous les navigateurs existants (même Internet Explorer 5…). Avant de télécharger n’importe quelle librairie, ou n’importe quel framework, il faut se poser les bonnes questions :

* Est-ce que j’en ai vraiment besoin ?
* Puis-je faire autrement ? en natif ? plus simplement ?
* N’ai-je pas déjà téléchargé une librairie ou un module qui fait ce dont j’ai besoin ?
  
Cela a l’air simple, mais on te garantie qu’il y a de nombreux sites sur lesquels on peut voir des choses encore plus hallucinantes que ça !!

Pire que de télécharger des librairies différentes, il y a des sites qui téléchargent en même temps des librairies identiques, dans des versions différentes.

Le téléchargement de librairies et de modules supplémentaires rajoutent, dans la majeur partie des cas, une couche de javascript supplémentaire à ta page qui alourdira le poids total du site. Le navigateur utilisera également plus de CPU, et de bande passante, vu qu’il devra télécharger, analyser et exécuter plus de scripts.

D’où l’intérêt de se poser les bonnes questions avant d’utiliser une <N>ième librairie dans son projet web.

Dans le cas où tu es sur un projet legacy, ou que tu veux simplement tenter de te passer de jQuery, d’Axios ou de moment.Js, tu peux consulter le super site https://youmightnotneed.com/ qui explique comment se passer de ces différentes librairies en utilisant du code natif 🙂.

### Javascript et performance
Comme toutes les ressources que tu peux télécharger à partir de son site internet, le Javascript peut causer de sérieux problèmes de performance. Tout d’abord en matière d’interactivité utilisateur car lorsque ton code est analysé puis exécuté, le main-thread peut-être bloqué.

Le Javascript, en général, n’est pas directement dans la page, bien qu’on puisse placer du code dans le HTML directement entre les balises `` <script></script>``. 
Il est plutôt utilisé en téléchargeant des fichiers javascript en rajoutant des attributs
``<script src="monfichier.js">``.

Comme le reste des ressources web, plus on a à télécharger de fichiers, plus le site peut sembler lent, et mettre du temps à s’afficher. Tout dépend d’une multitude de paramètres tels que le débit du réseau de l’utilisateur, mais aussi la taille de tes fichiers, le nombre de domaines appelés pour télécharger tes ressources, le temps de connexion au domaine, le temps de résolution du SSL, le temps de téléchargement du fichier. Il est recommandé d’éviter de télécharger une multitude de fichiers javascript, et si possible de les télécharger de manière asynchrone. Cela permet d’éviter de bloquer le rendu, pour afficher au plus tôt la page à l’utilisateur avec le HTML et les CSS prioritaires. Il existe deux moyens d’améliorer le rendu utilisateur par rapport à ce que l’on veut faire en javascript, juste sur le téléchargement des fichiers : on peut télécharger nos JS en async ou en defer .

Télécharger une ressource JavaScript avec l’attribut async (ex : ``<script async src="monfichier.js">``) libérera le main-thread durant le temps de téléchargement du fichier, mais celui-ci le bloquera dès que son téléchargement sera fini pour être interprété et analysé. (Alors qu’il te restera peut-être des CSS à télécharger ou des ressources plus critiques).

Télécharger un fichier Javascript avec l’attribut defer (ex ``<script defer src="monfichier.js">``) va déférer tout le traitement du script. Il sera téléchargé de manière asynchrone, mais analysé et exécuté après le rendu de la page.

Ces bonnes pratiques de performance web peuvent tout de même causer des problèmes. Même si l’affichage de la page est rendu plus rapidement, si tu as une multitude de requêtes trop longues à cause d’un débit trop lent, ou que ton serveur met trop de temps à répondre, ou que tu as tout simplement trop de fichiers à appeler, l’utilisateur se retrouvera bloqué par l’ensemble des scripts qui s’exécuteront après leur téléchargement…

Agir avec sobriété sur le nombre de ressources JavaScript, et sur le code présent sur ton front est essentiel pour éviter le TBT (Total Blocking Time) déclenché dès qu’une ressource met plus 60ms à s’exécuter, et le TTI (Time To Interactive) mesurant le temps nécessaire à ta page pour être interactive pour tes utilisateurs.

Une fois que tu as compris l’intérêt de jouer avec le téléchargement asynchrone des ressources JavaScript, tu trouveras peut-être une nouvelle balise HTML censée t’aider pour améliorer le téléchargement des ressources, et le rendre plus rapide. Il s’agit de la balise ``<link rel="preload" href="Mytyle.css" as="style">`` utilisable pour toutes les ressources (JS, CSS, Fonts…). Cette balise peut être intéressante quand tu as trop de ressources et que l’ordre de celles-ci n’est pas respecté par défaut dans ta page, mais il faut faire attention avec le preload ! Comme on le dit souvent : “un grand pouvoir nécessite de grandes responsabilités” et ici, c’est clairement le cas. Ton navigateur est suffisamment intelligent pour donner un niveau d’importance à chaque ressource téléchargée dans ta page, si tu lui donnes des ressources en preload. La file de téléchargement des ressources critiques va être bouleversée, et tu risques de télécharger des ressources inutiles au rendu utilisateur au lieu de celles qui sont réellement importantes, ce qui pourrait perturber le rendu initial de ta page et ralentir son apparition.

### Javascript et rétrocompatibilité
Tout coder en vanilla.js c’est bien beau, mais ça possède quand même quelques soucis… Prenons un cas extrême, celui du fetch. Fetch est un nouveau standard du web remplaçant XMLHttpRequest, il permet d’effectuer des requêtes bien plus simplement qu’à l’époque, sans utiliser ni XMLHttpRequest qui reste compliqué d’utilisation, ni un $.get() ou un $.post() via la librairie jQuery, ni un axios.get() en utilisant la librairie Axios. Sur le papier tout est parfait. On exécute des requêtes plus simplement qu’avant, sans avoir à télécharger de dépendances.

Sauf que cette fonctionnalité, même si elle n’est plus si “nouvelle” que ça, n’est pas compatible avec toutes les versions de navigateurs. Si ton entreprise doit encore (et malheureusement) supporter d’ancien navigateurs comme Internet Explorer, tu ne peux pas utiliser Fetch, qui n’est disponible que depuis les versions de navigateurs relativement récentes.

Lorsque tu es dans cette situation, tu peux te poser pas mal de questions :

* Dois-je rester sur fetch, sachant qu’une partie des navigateurs n’y ont pas accès ?
* Dois-je télécharger une librairie spécifique pour palier l’absence de fetch sur les anciennes versions ? ou utiliser un polyfill qui te permettra de l’utiliser ?
  
En matière d’éco-conception, on évitera de rendre nos applicatifs non fonctionnels sur les anciens périphériques. En effet, l’aspect le plus polluant du numérique est le renouvellement des périphériques utilisateur. Ainsi, en rendant une application obsolète sur une ancienne version, on peut indirectement forcer notre utilisateur à renouveler son périphérique s’il est dans l’incapacité de télécharger une nouvelle version, ou un autre navigateur.

Il faudra donc, dans ce genre de cas, favoriser la solution technique la moins impactante pour ton utilisateur : soit l’utilisation d’un polyfill, qui ne gérera que ce dont tu as besoin, ou l’utilisation d’une librairie qui pourrait importer des éléments inutiles à ton utilisation.

### Les Frameworks JavaScript
React.js, Vue.js, Angular, Svelte… Le monde du Javascript est en perpétuel changement : de nombreux frameworks existent, évoluent et s’adaptent pour tenter de rendre le code toujours plus simple, plus performant, et plus qualitatif.

Ces frameworks nous permettent de gagner du temps, d’être plus efficace en tant que développeur, de sécuriser le code que l’on produit, et de faciliter la maintenance de nos pages. Ce sont des boîtes à outils formidables permettant de gérer beaucoup de choses plus simplement que si nous le faisions nous, d’avoir une hiérarchisation du projet qui doit être respectée. Que ça soit dans la gestion du shadowDom, des customs Elements ou de la gestion des templates HTML, ils gèrent bien plus simplement les web components que ce que nous pouvons faire manuellement.

Cependant, bien que l’utilité d’un framework soit avéré, ils embarquent généralement beaucoup de choses qui ne sont peut-être pas essentielles à tes besoins. Avant de commencer à utiliser un framework JavaScript, demande toi s’il te sera nécessaire, si tu en auras l’utilité et s’il va combler correctement les besoins que tu as.

Si tu n’as qu’un besoin spécifique, demande toi aussi s’il ne vaut pas mieux télécharger une librairie ou un package plus petit que de télécharger tout le code d’un Framework pour n’en utiliser qu’une petite partie.

#### Minife ton HTML, ton JS tes CSS et tes SVGs

Tous les fichiers que nous codons possèdent des éléments qui ne sont pas utiles à l’interpréteur ou au compilateur du langage. Que ça soit les sauts de ligne, les espaces et tabulations inutiles, les attributs obsolètes ou les commentaires dans le code, ce sont autant de choses que l’utilisateur n’a pas à télécharger et qui peuvent réduire le poids de ton site internet et la bande passante consommée pour son téléchargement.

Il existe de nombreux moyens de minifier tes ressources : pour les JS et les CSS, tu peux utiliser des plugins JavaScript, comme [<https://webpack.js.org/plugins/css-minimizer-webpack-plugin/>](<https://webpack.js.org/plugins/css-minimizer-webpack-plugin/>) qui minifient tes CSS lors du build de l’application.

Pour les SVGs, qui sont généralement trop lourds, et blindés d’attributs inutiles, tu as une liste non exhaustive d’outils de minification disponible ici ⇒ https://css-tricks.com/tools-for-optimizing-svg/ Pour le HTML, il est possible de minifier la sortie HTML via le module https://developers.google.com/speed/pagespeed/module (de Google) disponible sur Apache et Nginx. Ce module fait beaucoup d’autres choses, mais il est aussi utile à la minification 😉

#### Split tes CSS par requête de média

Minifier les CSS est une bonne chose, mais il faut aussi éviter au maximum de charger des CSS inutiles. Pour ce faire, il est possible d’utiliser l’attribut media pour spécifier explicitement quand télécharger les CSS. Un utilisateur mobile ne téléchargera pas les CSS utiles au desktop et vice-versa, un utilisateur sur desktop, ne téléchargera pas les CSS spécifiques au mobile. On se retrouve donc avec plus de lignes de fichiers de CSS dans le code, mais avec moins de CSS téléchargé, vu qu’ils sera adapté à la condition de l’attribut media:

    ``
    <!-- Split des CSS en deux fichiers pour mobile et desktop -->
    <link rel="stylesheet" media="screen and (max-width: 768px)" href="mobile.css">
    <link rel="stylesheet" media="screen and (min-width: 768px)" href="desktop.css">
    ``
Pour ce faire, il existe des plugins permettant de splitter les CSS automatiquement, comme https://github.com/SassNinja/postcss-extract-media-query ou encore https://github.com/mike-diamond/media-query-splitting-plugin.

### Réduis le nombre de tes ressources

Toutes les ressources doivent être téléchargées avec parcimonie. Les designers t’ont fourni une maquette avec des vidéos ? Est-ce qu’elle est utile ? Ne peut-on pas la remplacer par une image ? Si ce n’est pas le cas, dois-tu la télécharger, et la lire directement ? Peux-tu la lazy-loader, lorsque l’utilisateur demande à la voir ?

Un nouveau third-part ? En as-tu réellement l’utilité, l’équipe qui l’a demandé est-elle au courant des autres services disponibles sur le site ? N’y en a-t-il pas un autre, déjà téléchargé, qui fait la même chose ?

Une galerie d’images ? Pourquoi pas juste une ou deux images maximum ?

Une image d’illustration ? A-t-on jugé son utilité ? Ne peut-on pas faire sans ? ou peut-être différemment, avec un pictogramme, ou une forme de font téléchargée sur la page ?

Dans le cas ou les ressources téléchargées doivent réellement l’être, qu’il n’y a pas moyen de s’en passer, il existe des méthodes pour les optimiser, réduire leur poids, ou le nombre de requêtes effectuées en fusionnant certains fichiers, certaines images. Ainsi, si tu utilises des pictogrammes, et que tu les as au format SVG, tu peux les intégrer directement dans la page HTML, pour éviter toutes les requêtes faites pour leur utilisation… Mais s’ils sont aussi appellés sur d’autres pages, autant les laisser en tant que fichier, que les autres pages les téléchargeant puissent profiter du cache si elles ont déjà été téléchargées ailleurs.

Si tu as un header/footer avec des dizaines d’images ou de pictos, tu peux également utiliser la technique des sprites, pour éviter de télécharger une multitudes d’images, lorsque le cache expire. (https://css-tricks.com/snippets/css/perfect-css-sprite-sliding-doors-button/).

Le but étant de réduire le nombre de ressources à télécharger, d’éviter au maximum les requêtes HTTP faites par ton applicatif, d’optimiser celles qui doivent l’être, d’éviter à tes utilisateurs d’utiliser trop de bande passante, et à leur navigateur de consommer trop de ressources pour afficher tes pages. Un super site internet existe pour analyser ce que l’on appelle le “waterfall” : la cascade des ressources que ton site télécharge, il s’agit de https://www.webpagetvest.org/. En analysant tes Waterfall, tu verras que toute ressource téléchargée prend du temps lors de sa connexion, de son téléchargement et/ou de son exécution. Par conséquent, les réduire te permet d’optimiser naturellement ta page.

### Désactive (ou n’active pas) la lecture automatique des vidéos

Dans le cas ou tu dois intégrer une vidéo, désactiver la lecture automatique de celle-ci est le minimum à faire. Premièrement, c’est une bonne pratique de qualité web. En effet, un utilisateur doit pouvoir visionner une vidéo s’il le décide, on ne doit pas lui imposer le visionnage ou l’écoute de quelque chose ou il n’y a pas eut la moindre interaction.

En éco-conception, c’est également une pratique intéressante : en ne lisant pas la vidéo lorsque l’utilisateur n’en a pas fait la demande, on ne tente pas de télécharger toute la vidéo. Ce qui réduira la bande passante utilisée, et permettra à tes autres ressources de s’afficher plus rapidement. Dans aucun cas, nous ne devons télécharger de données qui peuvent être inutiles au bon fonctionnement du site ou à tes utilisateurs. C’est la base pour réduire l’impact environnemental de nos sites internet.

En HTML5 la balise vidéo n’active pas l’autoplay par défaut, il faut l’activer, cependant, l’attribut autoplay, est un attribut boolean : pour désactiver l’autoplay, il faut bien supprimer totalement l’attribut et non pas écrire un autoplay = false :

    `` 
    <!-- Vidéos avec Autoplay -->
    <video src="maVideo.webm" autoplay poster="poster.jpg"></video>
    <video src="maVideo.webm" autoplay="false" poster="poster.jpg"></video>

    <!-- Vidéo sans Autoplay -->
    <video src="maVideo.webm" poster="poster.jpg"></video>
    ``

### Evite le pré-chargement des vidéos

Nous l’avons vu, désactiver la lecture automatique des vidéos est une solution qui permet de réduire l’impact environnemental de nos pages web, mais même avec cette bonne pratique, les navigateurs peuvent télécharger des données supplémentaires qui sont inutiles dans le cas où l’utilisateur ne lance pas la vidéo. Idéalement, il faut non seulement ne pas activer la lecture automatique, mais aussi désactiver le téléchargement des métadonnées des vidéos, vu que dans le cas où tes utilisateurs ne lancent jamais la vidéo, ces métadonnées sont inutiles.

L’attribut preload="none" permet de demander explicitement au navigateur de ne rien télécharger en plus. Il faut faire attention car dans l’ordre de priorité, l’attribut autoplay est devant l’attribut preload . Si les deux attributs sont présents, l’attribut preload ne servira à rien et ne sera pas pris en compte.

    ``
    <!-- Vidéo ne préchargeant aucunes données -->
    <video controls preload="none">
    <source src="maVideo.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>

    <!-- Vidéo chargeant quand même les données, vu que `autoplay` est présent -->
    <video controls autoplay preload="none">
    <source src="maVideo.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    ``

### Charge les données présentes sous la ligne de flottaison de manière paresseuse
La ligne de flottaison, c’est la ligne “invisible” qui sépare la partie visible de ta page de sa partie invisible pour l’utilisateur (celle ou l’utilisateur est obligé de scroller pour la rendre visible). Cette ligne est très importante : toutes les données visibles (qui sont au dessus de la ligne de flottaison) doivent s’afficher le plus rapidement possible pour que l’utilisateur puisse interagir avec la page le plus vite possible.

C’est une des raisons pour lesquelles il faut charger les éléments en-dessous de la ligne de flottaison de manière paresseuse. La partie invisible n’est pas essentielle à la première visualisation de la page.

Pour charger les données invisibles seulement lorsque l’on en a besoin, on peut utiliser l’attribut loading="lazy", qui est disponible (mais pas encore sur tous les navigateurs) sur les éléments ``<img></img>`` et ``<iframe></iframe>`` . Il existe néanmoins des libraires (très légères) permettant de faire le travail de lazyLoading sur plus d’éléments (avec les ``<video></video>`` …) comme https://github.com/verlok/vanilla-lazyload ce qui peut réduire de beaucoup le nombre d’éléments chargés sur ta page lors du premier rendu.

    `` 
    <!-- Image chargée de manière paresseuse, en différé. -->
    <img src="monImage.jpg" alt="description de mon image" loading="lazy">
    ``

Pour garder la compatibilité avec le plus de navigateurs différents, il est possible d’utiliser un polyfill : https://github.com/mfranzke/loading-attribute-polyfill qui va te permettre d’utiliser l’attribut loading="lazy" même si ton navigateur ne le prend pas en compte nativement.

 ### Utilise les polices d’écriture par défaut

 Les polices d’écriture sont aussi des ressources que l’on télécharge, comme le sont les images, les vidéos les CSS ou les scripts. Par contre, celles-ci peuvent avoir un impact important sur le chargement de la page. Non seulement elles peuvent bloquer le rendu lors de leur téléchargement, mais elles peuvent aussi augmenter, de beaucoup, l’apparition du texte sur ta page. Tout dépend des valeurs que tu as configurées dans tes CSS.

La criticité des polices d’écriture est le fait qu’elles se téléchargent avec une haute priorité, et qu’elles peuvent donc ralentir tout le reste dans le cas où leur téléchargement prend du temps. Certaines peuvent également provoquer du CLS (Cumulative Layout shift: un indicateur de #webPerf issu des coreVitals de Google), ce qui n’est pas non plus une bonne idée.

Pour améliorer le rendu, Google préconise même de précharger ses fonts pour éviter d’avoir un site qui s’affiche en différé.

    ``
    <head>
    <!-- préchargement de la font Pacifico-Bold.woff2 -->
    <link rel="preload" href="/assets/Pacifico-Bold.woff2" as="font" type="font/woff2" crossorigin>
    </head>
    ``

Si, dans le pire des cas, il est nécessaire d’utiliser une police d’écriture customisée, veille à utiliser le format woff2 et à la télécharger sur ton propre domaine, voire sur un sous-domaine statique, pour éviter de télécharger des métadonnées inutiles avec ta police d’écriture 🙂

### Charge les images dans les bonnes dimensions

Les images sont, avec les vidéos, les ressources les plus lourdes que l’on télécharge sur un site internet. Pour éviter de télécharger des images trop lourdes, il faut que celles-ci soit adaptées à l’emplacement qui leur est réservé dans la page.

Par exemple, si tu as un emplacement unique qui s’affiche dans les dimensions 30*30px, on ne va pas télécharger une image de 300*300px. Non seulement l’image sera beaucoup plus lourde, elle se téléchargera moins vite, mais utilisera en plus la mémoire et le CPU du périphérique pour redimensionner cette image trop grande.

Dans le cas où l’image a une taille unique sur tous les périphériques, il n’y a pas trop de problèmes : il suffit de définir une seule image de la taille affichée.

C’est un tout petit peu plus complexe lorsqu’une même image peut s’afficher dans plusieurs dimensions. Par exemple, une même image, peut avoir une taille de 80*80 sur desktop, de 60*60 sur tablette et de 40*40 sur mobile. C’est une très mauvaise pratique de n’afficher que l’image la plus grande (80*80 dans cet exemple) dans toutes les dimensions. Oui, l’image va être redimensionnée pour être affichée dans les dimensions inférieures (en 60*60 et en 40*40) mais tu vas télécharger une image trop lourde dans deux cas sur trois et forcer le périphérique à redimensionner l’image.

Heureusement, il est possible d’utiliser des techniques d’image adaptive, en définissant plusieurs tailles d’image grâce aux attributs srcset et sizes de la balise ``<img></img>``:

Il existe de nombreuses spécificités à l’attribut srcset pour optimiser au mieux tes images, que tu peux retrouver sur le site de la MDN ici : https://developer.mozilla.org/fr/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images

### Charge les images dans le bon format

Une fois que l’image est adaptive, que tu l’as bien affichée dans la bonne dimension, qu’importe sa zone d’affichage, il y a toujours moyen d’optimiser l’image, notamment en jouant sur le format d’encodage. Une même image peut avoir plusieurs formats différents, et de nouveaux formats, adaptés au web, ont été créés pour réduire le poids des images d’origine.

Traditionnellement, les format .png et .jpg sont favorisés, mais il en existe beaucoup d’autres : le .webp, le .avif sont des formats beaucoup plus récents et bien mieux optimisés; qui réduisent la taille des ressources très significativement. Convertir l’image dans un de ces formats récents peut permettre de l’alléger jusqu’à 95% de son poids.

Comme pour le reste des bonnes pratiques, l’idéal n’est pas de perdre du temps à le faire à la main, mais d’automatiser ces optimisations. Sachant qu’en plus, ces nouveaux formats ne sont pas pris en compte par tous les navigateurs. Si tu convertis à la main ces images, et que tu les imposes à chaque navigateur, tes images n’apparaîtront pas partout ! Il existe des modules, comme le module pagespeed de google disponible pour apache et nginx https://developers.google.com/speed/pagespeed/module, qui permet de convertir tes images par rapport aux headers des requêtes sur ton serveur. L’intérêt est double : non seulement le module peut convertir l’image dans le meilleur format possible (convertir du .gif en .png, ou du .jpg en .webp) mais en plus, le support du format est intégré. Ainsi, une image convertie en .webp ne sera envoyée que si le navigateur qui la demande supporte ce format 😉

    ``
    <!-- Image .gif non optimisée dans le code source original -->
    <img src="images/monImage.gif"/>

    <!-- Image .png optimisant l'image .gif originale dans le code source retourné -->
    <img src="images/xMonImage.gif.pagespeed.ic.GSLMcHP-fl.png"/>
    ``

### Optimise l’utilisation de ton framework

#### Angular : Évite les re-render inutiles

Avec Angular, par défaut, un composant est rendu de nouveau à chaque fois qu’un évènement asynchrone est déclenché comme un clic, une requêtre XHR, un setTimeout ou autre. Cela pose problème puisque ce comportement par défaut cause de nombreux re-render inutiles. Une des solutions est de changer la stratégie de détection des changements.

Dans cet exemple on applique la stratégie OnPush.

La détection des modifications OnPush ne restitue un modèle que si :

* L’une de ses propriétés d’entrée a obtenu une nouvelle référence.
* Un évènement du composant ou de l’un de ses enfants est déclenché. Par exemple cliquer sur un bouton dans le composant.
* À la détection d’une exécution explicite de changement.

    ``
    @Component({
    selector: 'app-todo-list',
    templateUrl: './todo-list.component.html',
    styleUrls: ['./todo-list.component.scss'],
    changeDetection: ChangeDetectionStrategy.OnPush
    })
    export class TodoListComponent implements OnInit {
    ``

#### React : Évite la réconciliation en utilisant la méthode

shouldComponenUpdate()
Il arrive parfois que React décide de mettre à jour un composant en exécutant la fonction render() de ce dernier, alors que cela n’est pas nécessaire. C’est un peu dommage, surtout si le composant en question est complexe. Heureusement, les créateurs de React proposent la méthode shouldComponentUpdate() pour palier à ce problème. Tu pourras utiliser cette méthode afin de t’assurer que ton composant est rechargé uniquement si nécessaire.

Voici un exemple repris de la documentation de React :

Si la seule façon de changer ton composant provient d’une modification de props.color ou state.count, alors tu dois vérifier ces valeurs dans shouldComponentUpdate :


    ``
    class CounterButton extends React.Component {
    constructor(props) {
        super(props);
        this.state = {count: 1};
    }

    shouldComponentUpdate(nextProps, nextState) {
        if (this.props.color !== nextProps.color) {
        return true;
        }
        if (this.state.count !== nextState.count) {
        return true;
        }
        return false;
    }

    render() {
        return (
        <button
            color={this.props.color}
            onClick={() => this.setState(state => ({count: state.count + 1}))}>
            Compteur : {this.state.count}
        </button>
        );
    }
    }
    ``

https://fr.reactjs.org/docs/optimizing-performance.html#avoid-reconciliation


## Sécuriser son applicatif

En tant que développeur ou développeuse côté Front, tu es aussi en charge de la sécurisation de ton applicatif. Il est essentiel de prendre en compte cet aspect lorsque l’on met en ligne une application pour de nombreuses raisons plus ou moins évidentes :

* Sécuriser la transmission des informations utilisateurs.
* Sécuriser les informations de l’entreprise.
* Augmenter le seuil de confiance du site internet auprès de vos utilisateurs et utilisatrices
* Augmenter la qualité de votre produit, et indirectement, votre SEO.

Aucun de ces points n’est à négliger, il est très important de prendre en compte le fait que tu es garant de la sécurité des données qui transitent sur ton site. Pour prévenir ces risques, il existe de bonnes pratiques à mettre en place :

### Réfléchis VRAIMENT avant d’ajouter des services tiers

On a vu que l’ajout de scripts tiers peut impacter la performance, mais ils peuvent aussi impacter la sécurité de ton applicatif. Un script qui traine sur ton applicatif peut potentiellement récupérer une quantité d’informations colossales sur tes utilisatrices et utilisateurs. Il est aussi probable que ces scripts n’utilisent pas la même politique de sécurité que celle de ton projet. Ils peuvent utiliser des librairies dépréciées et importer des failles de sécurité. Pour se prémunir contre ces problématiques, il est possible d’effectuer des analyses via des outils d’analyse de vulnérabilité comme Snyck .

L’analyse des vulnérabilités est automatiquement lancée avec un test d’analyse statique de Webpagetest.org.

### Mets à jour tes dépendances

Mettre à jour ses dépendances, ça devrait être évident pour tout le monde. Bien sûr, lorsque l’on parle de mises à jour, on parle de mises à jour de version stable. Tu ne vas pas mettre à jour tes packages en version alpha ou bêta car elles sont plus récentes que les versions stables. Non, les versions alpha et béta ne doivent en aucun cas arriver sur un service disponible en production.

Néanmoins, la mise à jour de dépendances est intéressante à de nombreux niveaux : la performance peut avoir été améliorée, l’architecture du bundle a pu être modifiée pour palier à certains problèmes et des failles de sécurité ont pu être corrigées.

On te conseille sincèrement de mettre à jour régulièrement tes dépendances, pour ne pas avoir à subir de mises à jour forcées, qui pourrait te faire perdre énormément de temps. Mieux vaut fixer les méthodes dépréciées, et les évolutions au fur et à mesure que de tout modifier d’un coup, et de risquer d’avoir un nombre incalculable de problèmes.

### Vérifie la dernière date de modification de tes dépendances

Mettre à jour ses dépendances ne suffit pas. On peut très bien avoir des dépendances à jour qui sont… obsolètes. Et une dépendance obsolète peut aussi causer de sérieux problèmes à ton applicatif. Un bundle obsolète peut causer des soucis sur les navigateurs récents, en utilisant des fonctions dépréciées. Il peut aussi causer des soucis en embarquant des failles de sécurité qui n’auraient jamais été corrigées.

### Utilise l’intégrité des ressources des scripts que tu ajoutes

    ``
    <script src="<https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js>" 
integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" 
crossorigin="anonymous"></script>
    ``

Cela permet de ne pas autoriser l’exécution de scripts non conforme à leur intégrité et d’éviter une manipulation malveillante de tes sources. Une documentation plus complète est disponible ici : https://developer.mozilla.org/fr/docs/Web/Security/Subresource_Integrity

### Vérifie les en-têtes HTTP de sécurité

Lorsque l’on crée une application Web, il y a un nombre incalculable d’échanges entre le front (coté client) et le serveur (coté back). Pour éviter et contrer les menaces informatiques, l’OWASP (pour Open Web Application Security Project®) recommande de spécifier correctement une dizaine d’en-têtes de réponse. Heureusement pour toi, il est possible d’analyser tous les headers transmis via le site https://securityheaders.com/ qui te donnera un grade suivant le niveau de sécurité de ton site.

La majorité des headers et des règles ne sont définissables que coté serveur (le back) via une configuration Apache ou NGINX, ou NodeJS

Voici la configuration Apache pour la mise en place du HSTS (HTTP Strict Transport Security) :


    ``

    <IfModule mod_headers.c>
     Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
    </IfModule>
    ``

Et la mise en place de l’HSTS via NGINX:

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

Coté front, ce n’est pas évident (voir impossible) de spécifier ces règles de headers, mais il peut être possible, grâce à certaines balises meta, de surcharger les règles des headers. Par exemple, pour le CSP (Content Security Policy), si aucun header n’a été mis en place, tu peux tester tes propres règles en spécifiant la balise ``<meta http-equiv="Content-Security-Policy" content="...">``

Voici un exemple de CSP ayant une règle default-src https: définissant que le navigateur n’exécutera pas les scripts inline, et forcera les ressources à se charger en HTTPS :

    ``
    <meta http-equiv="Content-Security-Policy" content="default-src https:">
    ``

La gestion des headers est très importante pour sécuriser ton site ! Attention à ne pas tester des règles de headers en production ! La modification d’un header peut empêcher le chargement de ressources, l’exécution de tes scripts, ou forcer le chargement https de tes pages. Cela peut mettre en péril l’affichage du site pour l’ensemble de tes utilisatrices et utilisateurs.

## Rendre son front accessible

Pour information, lorsque l’on parle d’accessibilité, on utilise très souvent l’abréviation #A11Y. Cette abréviation est la contraction de accessibility avec la première lettre a, le nombre de lettres entre celles-ci et la dernière lettre y.

Une des étapes obligatoires (oui) lors de la mise en ligne d’une page internet est de vérifier que celle-ci soit accessible à tout le monde. Si les choses sont bien faites, tu as dû passer des tests d’accessibilité tout au long de la livraison de ton produit.

Pourquoi c’est essentiel ? Tout d’abord, parce que cet aspect fait partie des principes fondamentaux du web : il doit être accessible à l’ensemble de la population et le plus inclusif possible.

L’OMS (Organisation Mondiale de la santé) estime que 15% de la population mondiale vit avec un handicap. Rendre le Web Accessible, c’est aussi et surtout ne laisser personne de côté.

Contrairement à ce que l’on peut croire, il n’y a pas de surcoût à la mise en place de l’accessibilité sur un site. On peut naturellement rendre n’importe quel site web accessible, et c’est beaucoup plus simple si on s’y prend tôt (un peu comme la performance et la sobriété…)

Il existe deux référentiels majeurs connus auxquels se référer lorsque l’on parle d’accessibilité :

* le WCAG (Web Content Accessibility Guidelines) maintenu par le W3C (The World Wide Web Consortium) et qui est garant des bonnes pratiques du web, des évolutions du HTML et du CSS.
* Le RGAA (Référentiel général d’amélioration de l’accessibilité), qui est le référentiel d’accessibilité du gouvernement Français et qui se base sur le WCAG. Tous les sites institutionnels sont censés respecter le RGAA.

De nombreux sites existants te permettent de faire des audits d’accessibilité, mais ils n’effleurent que la surface du WCAG. En effet, on estime que seulement 30 à 50% des bonnes pratiques d’accessibilité sont auditionnées par les outils existants (cf https://marcysutton.com/evinced-automated-accessibility-testing). Ils ne permettent donc pas d’effectuer des analyses pointilleuses de l’ensemble des points essentiels à l’accessibilité. On peut citer web.dev (de Google) qui permet de tester un peu l’accessibilité des sites, le validateur officiel du W3C https://validator.w3.org/, le site https://wave.webaim.org/ et https://tenon.io/ qui est le plus complet des quatre.

Voici une liste non exhaustive de bonnes pratiques à mettre en place pour rendre son site un minimum accessible :

#### Vérifie l’arborescence de ton DOM

Le code HTML du DOM que tu crées est très important pour les lecteurs d’écran. Lorsque l’ accessibilityTree se génère (à partir du DOM), il va utiliser l’arborescence que tu as définie sans prendre en compte le visuel (oui, un lecteur d’écran se moque que tu aies ajouté un margin-top: 300px pour faire apparaître un élément sous un autre. C’est une très mauvaise pratique de placer un ordre d’affichage visuel différent de l’ordre des éléments que tu as dans le DOM).

#### Utilise les bonnes balises HTML

Les balises HTML ont toutes un intérêt spécifique d’utilisation : elles intègrent nativement un comportement à adapter lors de la création de l’arbre d’accessibilité. Ainsi, pour éviter d’utiliser des attributs aria et role (les attributs HTML utiles à la description des éléments accessibles) à outrance et de la mauvaise manière, autant utiliser les bonnes balises HTML directement.

Voici un exemple de ce qu’il ne faut pas faire :

    ``
    <!-- Bouton pas accessible -->
    <span>Enregister la vidéo</span>
    <!-- Bouton accessible, mais HTML mal utilisé -->
    <span role="button" aria-pressed="false">Enregister la vidéo</span>
    ``

Voici la solution à privilégier:

    ``
    <!-- Bouton accessible avec une bonne utilisation du HTML -->
    <button>Enregister la vidéo</button>
    ``
#### Spécifie correctement tes étiquettes

Spécifier correctement l’étiquetage des balises est primordial pour que lors d’une lecture d’écran le lien puisse être associé correctement à une description. C’est le cas pour tous les éléments spécifiques que tu as.

Exemple de ce qu’il faut éviter :

    ``
    <!-- Texte de lien mal spécifié 'ici' -->
    <p>Le cours de TheGreenCompagnon est disponible <a href="super_cours.html">ici</a> depuis des semaines</p>
    ``
Bonne pratique à adopter :

    ``
    <!-- Texte de lien bien spécifié 'Le cours de TheGreenCompagnon est disponible' -->
    <p><a href="super_cours.html">Le cours de TheGreenCompagnon est disponible</a> depuis des semaines</p>
    ``

#### Vérifie tes contrastes !

Un des points centraux de l’accessibilité, qui doit être défini avant même de commencer un projet, est celui de la définition des contrastes. Les contrastes de ta page (couleur d’arrière-plan par rapport à la couleur du texte) doivent avoir un ratio assez prononcé pour que toutes les personnes puissent lire le texte facilement. Il est très facile, avec les CSS, de fournir un contraste trop faible qui perturbera la lecture de la page par tes utilisateurs et utilisatrices. Le WCAG spécifie 2 “grades” pour qualifier le niveau de contraste de tes couleurs. ,Pour être valide au niveau “AA” il faut que tous les contrastes de tes pages soient au moins au ratio de : 4.5:1 dans le cas où le texte a une taille normale (qu’il n’est pas agrandi). Si tu souhaites avoir le grade maximum “A”, il faudra que tes pages aient un ratio minimum de 7:1.

Beaucoup d’outils d’analyse sont capables de vérifier tes contrastes : la console des outils de développement du navigateur Mozilla Firefox le fait naturellement. Il y a aussi l’outil “Contrast Finder” (https://contrast-finder.tanaguru.com/) qui permet d’analyser tes contrastes et de te proposer des couleurs similaires aux tiennes dans le cas où elles ne sont pas suffisamment contrastées.

#### Pense à utiliser un CSS ``<noscript>``

En règle générale, il faut que l’on puisse accéder au contenu du site sans avoir à activer JavaScript. Sauf qu’aujourd’hui, ne pas activer JavaScript, ce n’est pas évident. Dans le cas où des utilisateurs n’utilisent pas JavaScript, il est possible de leur afficher un style particulier, ou de faire apparaitre un message expliquant qu’il est préférable d’activer JavaScript pour naviguer sur le site. Pour cela, on utilisera la balise ``<noscript></noscript>`` qui permet d’exécuter le code présent seulement si Javascript est désactivé.

Voici un cas d’utilisation avec l’affichage d’un message en haut de la page si Javascript est désactivé :

    ``
    <!-- Afficher un message lorsque JavaScript est désactivé -->
    <body>
        <noscript>
            <p>Attention, ce site n'est fonctionnel que si Javascript est activé</p>
        </noscript>
        <!-- ... -->
    </body>
    ``

Et un autre exemple pour charger des styles spécifiques seulement si Javascript est désactivé :

    ``
    <!-- Charger un style spécifique si JavaScript est désactivé -->
    <head>
        <noscript>
            <link href="/css/no-js.css" rel="stylesheet">
        </noscript>
        <!-- ... -->
    </head>
    ``
