# Utilisation des différents outils d'éco conception

## Argos

<https://github.com/marmelab/argos>

### Environnement

Docker  
Docker-compose  
Make : sudo apt install make  

### Installation

>git clone https://github.com/marmelab/argos.git  
>make install

### Lancement

>make start

### Arrêt

>make stop

____

## Power API

<https://powerapi-ng.github.io/>

### Jouleit
#### **Installation**

>git clone https://github.com/powerapi-ng/jouleit.git  
>cd jouleit/  
 
#### **Lancement**

>./jouleit.sh cmd

<center>
<img src="images\jouleit.PNG" style="width : 600px ">
</center>

### virtual Watts
#### **Sensor**

Virtual watt a besoin des deux sensors un pour la machine hôte hwpc et l’autre pour la VM profcs.
<https://powerapi-ng.github.io/hwpc-sensor.html>  
<https://powerapi-ng.github.io/procfs-sensor.html>  

#### **Environnement**

Installation de Smart Watts sur la machine hôte linux :
<https://powerapi-ng.github.io/smartwatts.html>  

config :   
>{
  "verbose": true,  
  "stream": true,  
  "input": {  
    "puller": {  
      "model": "HWPCReport",  
      "type": "mongodb",  
      "uri": "mongodb://127.0.0.1",  
      "db": "test",  
      "collection": "prep"  
    }  
  },  
  "output": {  
    "pusher_power": {  
      "type": "mongodb",  
      "uri": "mongodb://127.0.0.1",  
      "db": "test",  
      "collection": "prep"  
    }  
  },  
  "cpu-frequency-base": Ratio Base,  
  "cpu-frequency-min": Ratio min,  
  "cpu-frequency-max": Ratio max,  
  "cpu-error-threshold": 2.0,  
  "disable-dram-formula": true,  
  "sensor-report-sampling-interval": 1000  
>}

Ratio base = tapper “lscpu” trouver le modèle de cpu aller sur la documentation trouver la fréquence de base X10  
Ratio min = tapper “lscpu” trouver le ratio divisée par 100  
Ratio max = tapper “lscpu” trouver le ratio divisée par 100  

#### **Installation**

>docker pull powerapi/virtualwatts-formula

Configuration
>{  
    'verbose': True,  
    "stream":True,  
    "input": {  
        "puller_filedb": {  
            "type": "filedb",  
            "model": "PowerReport",  
            "filename": "SW_output"  
            },  
        "puller_tcpdb": {  
            "type" : "socket",  
            "model": "ProcfsReport",  
            "uri": "127.0.0.1",  
            "port": self.port  
        }  
    },  
    "output": {  
        "power_pusher": {  
        "type": "influxdb",  
        "model": "PowerReport",  
        "uri": "127.0.0.1",  
        "port": 8086,  
        "db": "test",  
        "collection": "prep"  
        }  
    },  
    "delay-threshold": 500,  
    "sensor-reports-sampling-interval": datetime.timedelta(500)  
>}  

#### **Lancement**
>docker run -t --net=host -v $(pwd)/config_file.json:/config_file.json powerapi/virtualwatts --config-file /config_file.json

____

## Scaphandre

Scaphandre est un agent de monitoring de consommation énergique plus générale, en effet scaphandre est disponible pour toutes les distributions et est facilement implémentable dans docker.

<https://github.com/hubblo-org/scaphandre/>

### installation rapide

>docker run -v /sys/class/powercap:/sys/class/powercap -v /proc:/proc -ti hubblo/scaphandre stdout -t 15

### Installation docker

>git clone https://github.com/hubblo-org/scaphandre.git  
>cd scaphandre/docker-compose  
>docker-compose up -d  

Cela va permettre de lancer scaphandre facilement et d'avoir graphana et prometheus opérationnel en même temps. Graphana sera disponible à l'adresse suivante <http://localhost:3000>  avec les identifiants suivants :
- login : admin
- password : secret

<center>
<img src="images\scaphandre.PNG" style="width : 600px ">
</center>

____

## EcoCode

EcoCode utilise SonarQube pour tester le code de l'application sous différents languages tels que :
- Java
- PHP
- Python
- Android

EcoCode va permettre de donner une note globale au code sur son Eco conception, mais aussi les points possibles améliorer à l'aide des retours de SonarQube.

<https://github.com/cnumr/SonarQube>

### Installation

>git clone https://github.com/cnumr/ecoCode.git  
>cd ecoCode/src  
>mvn clean install  
>cd ..  
>docker-compose up --build -d

Après avoir lancés EcoCode l'application sera disponible a cette adresse <http://localhost:9000> avec les identifiants suivant :
- login : admin
- password : admin


____

## Cloud Carbon Footprint

<https://www.cloudcarbonfootprint.org/>

Cloud carbon footprint est une application rapide à installer sur toutes distributions, elle permet de mesurer les émissions de CO2 par les différents clouds providers :  
- AWS  
- Azure  
- GCP  

<center>
<img src="images\cloud1.PNG" style="width : 600px ">
</center>

De plus, l'application propose des recommandations d'amélioration pour chaque Cloud provider montrant les gains financier et écologique possibles. Cet outils demande un accès au compte du cloud provider il ne sera donc pas utile au développeur mais uniquement au gestionnaires du cloud.

<center>
<img src="images\cloud2.PNG" style="width : 600px ">
</center>

### Environnement

Node > 11  
Yarn  

### Installation

>git clone --branch latest https://github.com/cloud-carbon-footprint/cloud-carbon-footprint.git  
>cd cloud-carbon-footprint  

### Lancement guidé  

>yarn install && yarn guided-install

### Lancement standard

>yarn install  
>yarn start  

____

## Impactomètre

Impactomètre est un site internet permettant d'évaluer la différence entre plusieurs réunion, cela sert plus a titre informatif et permet de définir des échelles a ne pas dépasser lors de réunions pour le respect de l'environnement.

<https://impactometre.fr/> 

<center>
<img src="images\impactometre.PNG" style="width : 600px ">
</center>

____

## EcoDiag

EcoDiag est un site internet qui permet de mesurer la consommation électrique des appareils électroniques (ordinateurs, serveurs, portables, ...) d'une entreprise ainsi que leur coût de fabrication en CO2.

<https://ecoinfo.cnrs.fr/ecodiag-calcul/>

<center>
<img src="images\ecoDiag.PNG" style="width : 600px ">
</center>

____

## Carbonalyser

Carbonalyser est un add-on Firefox permettant de faire un audit basique de la navigation réalisée par l'utilisateur sur le moteur de recherche, il va ainsi donner une idée de la consommation électrique et de CO2 mais aussi la bande passante utilisée.

<https://theshiftproject.org/carbonalyser-extension-navigateur/>

<center>
<img src="images\carbonalyser.PNG" style="width : 500px;height : 600px">
</center>

____

## PageSpeed Insight

PageSpeed Insight est un outil de mesure des performances d'une page internet, cela permet notamment d'évaluer la rapidité d'affichage, les différentes étapes d'affichages, le temps avant de pouvoir interagir, etc.  
De plus cet outils fournit des opportunités et des conseil possibles pour améliorer la page du site internet. Ces indicateurs sont primordiaux pour l'ecoconception d'un site qui se base sur la durée de vie de celui-ci ainsi que sur son utilisation, son chargement, etc.

<https://developers.google.com/speed/pagespeed/insights/>

<center>
<img src="images\pageSpeed1.PNG" style="width : 600px">
<img src="images\pageSpeed2.PNG" style="width : 600px">
</center>

____

## GreenIT-analysis

GreenIT-analysis et une extension chrome permettant de réaliser un audit d'une page web, cela donne plusieurs indicateurs :  
- EcoIndex  
- Eau  
- CO2
- Nombre de requête
- Taille de la page
- Taille du DOM

De plus l'extension permet des données des conseils et bonnes pratique à réaliser pour améliorer l'empreinte carbon de la page.

<https://github.com/cnumr/GreenIT-Analysis>

<center>
<img src="images\GreenIT.PNG" style="width : 600px">
</center>

____

## Estimator

Estimator est un site internet permettant de mesurer les améliorations possibles d'une page si le Javascript de celle-ci est mise à jour. Cela permet notamment de données plusieurs indicateurs des calculs et un ordre d'idées de la vitesse gagnée.

<https://estimator.dev/>

<center>
<img src="images\estimator.PNG" style="width : 600px">
</center>

____

## Ecograder

<https://ecograder.com/>

Ecograder est un site internet permettant de calculer plusieurs facteurs d'une page internet :
- UX
- Page size
- Performance
- Hébergeur

Ce site internet permet aussi de données des conseils d'informations et de présenter les points les plus problématiques à corriger.
<center>
<img src="images\ecograder.PNG" style="width : 600px">
<img src="images\ecograder2.PNG" style="width : 600px">
</center>

____

## Wave

<https://wave.webaim.org/>

Wave est un site internet qui permet de vérifier l'accessibilité d'une page internet, cela donne des bonnes indications et les éléments pour améliorer chaque élément de la page.
<center>
<img src="images\wave.PNG" style="width : 600px">
</center>

____

## Greenspector

<https://greenspector.com/fr/accueil/>

Greespector est un site internet qui fait un audit d'un site internet et renvoie les données par mail, cet audit est plus axées sur la consommation énergétique du site sur un téléphone et permet de donner quelque idée d'amélioration possible.

<center>
<img src="images\greenspector.PNG" style="width : 600px">
</center>

____

## Website Carbon Badge

<https://www.websitecarbon.com/badge/>

Website Carbon Badge est un badge a rajouter sur les pages internet d'un site pour mesurer sa production de carbon par visites et pouvoir ainsi mettre en avant l'ecoconception de ce site internet.

<center>
<img src="images\badge.PNG" style="width : 600px">
</center>

____

## Gmetrix

<https://gtmetrix.com/>

Gmetrix est un site internet permettant de faire un audit d'un site internet sur ces performance majoritairement, mais cela peut être reporté pour de l'écoconception facilement, des rapport peuvent etre automatisé pour des site par un service de monitoring. Cet outil est intéressant puisqu’il permet (gratuitement) de brider la connexion (en 2G/3 G) et/ou de tester via différents CDN pour voir comment se comportent nos pages internet sur des connexions bas-débit, ou à travers le monde.

<center>
<img src="images\gmetrix.PNG" style="width : 600px">
</center>

____

## Pingdom

<https://tools.pingdom.com/>

Pingdom est un outil anglais d'audit de page il permet de mesurer les requêtes, le DNS, les éléments compresser, et les éléments de la page par taille.

<center>
<img src="images\pingdom.PNG" style="width : 600px">
</center>

____

## ShortPixel

<https://shortpixel.com/image-compression-test/#cruncher>

ShortPixel est un site permettant de faire un audit d'une page internet, ce site permet d'identifier les images trop lourde compressable et de les compresser.

<center>
<img src="images\shortPixel.PNG" style="width : 600px">
</center>

____

## WebPagetest

WebPagetest est un site internet qui permet de faire des audits extrêmement complets de performance, il permet ainsi d'analyser les points suivants :
- Chargement de la page
- Détails des requêtes
- Détails du contenu
- Domaine
- Analyse des images
- Mappage des requêtes
- Analyse de la sécurité

<https://webpagetest.org/>

<center>
<img src="images\webPageDetail.PNG" style="width : 600px">
<img src="images\webPageImage.PNG" style="width : 600px">
<img src="images\webPageSecurity.PNG" style="width : 600px">
</center>

## DareBoost

<https://www.dareboost.com/fr>

Du test de performance au monitoring synthétique de pages comme de parcours utilisateurs, Dareboost est un outil tout-en-un dédié à la performance web. C’est un outil conçu pour faciliter la collaboration entre professionnels du Web, et renforcer leur capacité d’action sur les problématiques de performance web.

Les rapports générés par Dareboost sont sûrement les plus complets que tu pourras trouver à travers la multitude d’outils sur le web. À partir de l’analyse statique d’une URL, le rapport est capable de retrouver une multitude de composants, de plugins ou de modules utilisés, et de t’orienter vers de bonnes pratiques te permettant de mieux les utiliser. Il est aussi intéressant de voir que cet outil te spécifie les ressources qu’il serait utile d’améliorer et pourquoi ! Les explications sont complètes, et en français. Si une page française n’existe pas, une ressource en anglais sera présentée. Dans tous les cas, tu auras accès à beaucoup de documentation, d’explications, et d’exemples d’amélioration.
<center>
<img src="images\DareBoost.PNG" style="width : 600px">
</center>