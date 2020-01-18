# Rendu MOSH/KICAD DJEBAR-TISSOT
## KICAD

Dans l'optique d'avoir un circuit optimal entre le module LoRa et le capteur de gaz présentés dans la partie MOSH ci-dessus, nous avons réalisé un shield qui dans l'idéal permettrait de pouvoir directement connecter notre capteur et notre émetteur de manière simplifiée.

Pour le schéma électrique, nous avons crée un composant représentant notre capteur de gaz et nous nous sommes basé sur ce que nous avons vu en cours avec Mr Nouillet :

![alt text](https://github.com/MOSH-Insa-Toulouse/2019_MOSH_B2_DJEBAR_TISSOT/blob/master/ImagesPCB/schema.png "Figure 1: Schéma du circuit électrique du shield")

Une fois le schéma électrique réalisé, il faut placer les différents composant sur le shield et les relier entre eux avec des pistes. C'est une partie complexe car il y'a beaucoup de contraintes à prendre en compte comme l'agencement des composants ou le fait que l'on puisse créer nos vias des deux cotés du shield.

![alt text](https://github.com/MOSH-Insa-Toulouse/2019_MOSH_B2_DJEBAR_TISSOT/blob/master/ImagesPCB/Pcb.PNG "Figure 2: Positionnement des pistes")

Une fois ces deux parties réalisées (schéma électrique et agencement), on peut visualiser notre modèle 3D final.

![alt text](https://github.com/MOSH-Insa-Toulouse/2019_MOSH_B2_DJEBAR_TISSOT/blob/master/ImagesPCB/3dVisu1.PNG "Figure 3: Vue 3D de coté")

![alt text](https://github.com/MOSH-Insa-Toulouse/2019_MOSH_B2_DJEBAR_TISSOT/blob/master/ImagesPCB/3dVisu2.PNG "Figure 4: Vue 3D de dessus")

![alt text](https://github.com/MOSH-Insa-Toulouse/2019_MOSH_B2_DJEBAR_TISSOT/blob/master/ImagesPCB/3dVisu2.PNG "Figure 5: Vue 3D de dessous")

## MOSH

#### I/ Les TPs

Après la présentation du cours par l’enseignant, nous avons décidé de commencer les Tps. Nous avons donc réalisé les activités des Tp 1 et 2 qui consistent surtout à réaliser le montage électrique nécessaire puis à téléverser le code fourni sur le moodle dans l’Arduino.
C’est un bon moyen de comprendre le fonctionnement de la carte Arduino à la fois au niveau du software mais aussi du hardware. 
De plus, certains montages peuvent nous pousser à être très créatifs comme celui du “Buzzer Melody” qui permet à tout le monde de créer sa propre mélodie. L’enseignant qui était également présent nous a aussi bien aidé

A partir du moment ou nous pensions maîtriser la carte, nous avons décidé de passer sur le mini projet.

#### II/ Le mini Projet

##### 1ère étape : Fabrication de l’émetteur/récepteur

La première étape fut de fabriquer l'émetteur/récepteur LoRa qui nous permettra par la suite de transmettre les données collectées par le capteur de gaz. Nous avions à notre disposition une puce RN 2483 permettant la communication LoRa et un support, sur lequel nous devions souder la puce. Afin de réaliser ce soudage, la lecture de la datasheet nous fut très utile et en particulier ce schéma :

![alt text](https://github.com/mystofake/MOSH_GazSensor/blob/master/MOSH/Images/pins.jpg "Figure 1: Pins de la puce RN 2483")

A partir de ce schéma nous avons pu limiter le travail de soudage puisqu’il nous a permis de savoir de quels pins nous avions besoin. Il a également fallu souder l’antenne afin que le dispositif puisse fonctionner. 


Le résultat obtenu est le suivant :

![alt text](https://github.com/mystofake/MOSH_GazSensor/blob/master/MOSH/Images/module.JPG "Figure 2 : Emetteur/Récepteur LoRa")

##### 2ème étape : La mise en place

Une fois le module LoRa fabriqué, nous avons pu commencer à le faire fonctionner avec les branchements suivants :

 * RN2xx3 -- Arduino
 * Uart TX -- 10
 * Uart RX -- 11
 * Reset -- 12
 * Vcc -- 3.3V
 * Gnd -- Gnd

Nous avons d’abord communiqué en Serial chaque commande pour bien s’assurer que tout fonctionne, comme par exemple :  sys get hweui qui retourne l’adresse MAC du module.

Vous pourrez trouver le code utilisé en annexe.


##### 3ème étape : The Things Network

Afin de faire communiquer notre module LoRa précédemment validé, nous avons suivi le tutoriel présenté sur moodle afin de créer une application pour le capteur de gaz sur The Thing Networks. Nous avons donc utilisé le code joint en annexe, en utilisant une authentification ABP, puisque c’était la seule fonctionnelle.

Nous l’avons ensuite testé en générant des valeurs aléatoires afin de vérifier la bonne réception des données. 
On constate un petit délai ainsi que le besoin de réaliser l’affichage pour éviter un blocage au bout d’un certain nombre de données reçues.
  
![alt text](https://github.com/mystofake/MOSH_GazSensor/blob/master/MOSH/Images/figure3.png "Figure 3 : Réception des données sur The Things Network")



##### 4ème étape : Réalisation d’un dashboard avec NodeRed

Afin de récupérer les données reçues sur The Things Network, il a fallu importer une bibliothèque pour avoir accès aux blocs permettant de récupérer ces valeurs.
Ensuite pour récupérer et traiter les données, il suffit de mettre en place ce type de graphes.

 
Inline-style: 
![alt text](https://github.com/mystofake/MOSH_GazSensor/blob/master/MOSH/Images/figure4.png
 "Figure 4 : Récupération des données sur NodeRed")


Les données ainsi récupérées peuvent ensuite être affichée sur sous forme de graphique, et on obtient ainsi le dashboard demandé.

![alt text](https://github.com/mystofake/MOSH_GazSensor/blob/master/MOSH/Images/figure5.png "Figure 5 : Visualisation des données du capteur") 

