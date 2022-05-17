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

Virtual watts a besoin des deux sensor un pour la machine hôte hwpc et l’autre pour la VM profcs.  
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

Ratio base = tapper “lscpu” trouver le modèle de cpu aller sur la doc trouver la fréquence de base X10  
Ratio min = tapper “lscpu” trouver le ration diviser par 100  
Ratio max = tapper “lscpu” trouver le ration diviser par 100  

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

Scaphandre est un agent de monitoring de consommation énergétique plus générale, en effet Scaphandre est disponible pour toutes les distributions et est facilement implémentable dans docker.

<https://github.com/hubblo-org/scaphandre/>

### installation rapide

>docker run -v /sys/class/powercap:/sys/class/powercap -v /proc:/proc -ti hubblo/scaphandre stdout -t 15

### Installation docker

>git clone https://github.com/hubblo-org/scaphandre.git  
>cd scaphandre/docker-compose  
>docker-compose up -d  

Cela va permettre de lancer scaphandre facilement et d'avoir graphana et prometheus opérationnel en même temps. Graphana sera disponible à l'adresse suivante <http://localhost:3000>  avec les identifiants suivant :
- login : admin
- password : secret

<center>
<img src="images\scaphandre.PNG" style="width : 600px ">
</center>
____

## EcoCode

EcoCode utilise SonarQube pour tester le code de l'application sous différents languages tel que :
- Java
- PHP
- Python
- Android

EcoCode va permettre de donner une note globale au code sur son eco conception, mais aussi les points possbiles améliorer à l'aide des retours de SonarQube.

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

Cloud carbon footprint est une application rapide a installer sur toutes distribution, elle permet de mesurer les émissions de CO2 par les différents clouds providers :  
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

EcoDiag est un site internet qui permet de mesurer la consommation éléctrique des appareil éléctronique (ordinateurs, serveurs, portables, ...) d'une entreprise ainsi que leur coût de fabrication en CO2.

<https://ecoinfo.cnrs.fr/ecodiag-calcul/>

<center>
<img src="images\ecoDiag.PNG" style="width : 600px ">
</center>

____

## Carbonalyser

Carbonalyser est un add-on firefox permettant de faire un audit basic de la navigation réalisée par l'utilisateur sur le moteur de recherche, il va ainsi donnée une idée de la consommation éléctrique et de CO2 mais aussi la bande passante utilisé.

<https://theshiftproject.org/carbonalyser-extension-navigateur/>

<center>
<img src="images\carbonalyser.PNG" style="width : 500px;height : 600px">
</center>

____

## PageSpeed Insight

PageSpeed Insight est un outil de mesure des performance d'une page internet, cela permet notamment d'évaluer la rapiditer d'affichage, les différentes étapes d'affichages, le temps avant de pouvoir intéragir, ect.  
De plus cet outils fournit des opportunités et des conseil possibles pour améliorer la page du site internet. Ces indicateurs sont primordiaux pour l'ecoconception d'un site qui se base sur la durée de vie de celui-ci ainsi que sur son utilisation, son chargement, etc.

<https://developers.google.com/speed/pagespeed/insights/>

<center>
<img src="images\pageSpeed1.PNG" style="width : 600px">
<img src="images\pageSpeed2.PNG" style="width : 600px">
</center>

____

## GreenIT-analysis

GreenIT-analysis est une extensions chrome permettant de réaliser un audit d'une page web, cela donne plusieurs indicateurs :  
- EcoIndex  
- Eau  
- CO2
- Nombre de requête
- Taille de la page
- Taille du DOM

De plus l'extensions permet de données des conseils et bonnes pratique a réalisées pour améliorer l'empreinte carbon de la page.

<https://github.com/cnumr/GreenIT-Analysis>

<center>
<img src="images\GreenIT.PNG" style="width : 600px">
</center>

____

## Estimator

Estimator est un site internet permettant de mesure les améliorations possibles d'une page si le javascript de celle-ci est mise a jour. Cela permet notamment de donnée plusieur indicateur des calculs et une ordre d'idée de la vitesse gagnée.

<https://estimator.dev/>

<center>
<img src="images\estimator.PNG" style="width : 600px">
</center>

____

## Joulemeter