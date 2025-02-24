## Dépôt de code 

Le [dépôt GitHub de la PG-MCEDIF](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main) (en anglais) contient le code actualisé des modules MCEDIF2025 dans trois langages de programmation : R, C et Python. Les trois langues contiennent les mêmes équations et exécutent les mêmes tâches. Le choix dépend des exigences de votre système. 

## Documentation 

Code et documentation technique relatifs au dépôt de code de la PG-MCEDIF. L’information comprend des précisions concernant les fichiers nécessaires à l’exécution de chaque langage de programmation. 

Remarque : bien que certains liens vers la MCEDIF actuelle et la MCEDIF2025 se trouvent ici et dans la section sur le transfert de technologie, de nombreuses autres sources d’information et de publications concernant l’utilisation de la MCEDIF et la documentation historique se trouvent sur le dépôt ouvert de la [S et T de RNCan (DOST)](https://ostrnrcan-dostrncan.canada.ca/accueil). 

## Informations sur le code IFM2025 

La ressource suivante décrit les fichiers et les exigences nécessaires pour générer des sorties pour la prochaine génération du système d’IFM (ci-après dénommé IFM2025). 

L’IFM2025 fait partie d’un programme plus vaste visant à mettre à jour la méthode canadienne d’évaluation des dangers d’incendie de forêt (MCEDIF). Trois langages de programmation différents sont disponibles : R, Python et C. Ces trois langages produisent les mêmes résultats, vous pouvez donc choisir celui qui répond à vos besoins. 

Les fichiers, les entrées, les formats et les sorties sont décrits ci-dessous de manière générale pour les trois langues. Tout écart par rapport à un langage spécifique est indiqué. 

Le code IFM2025 a été écrit et testé à l’origine en utilisant des tableaux de données et des fichiers .csv comme entrées. Ainsi, la sortie génère des tableaux de données simples qui peuvent ensuite être exportés. Les utilisateurs peuvent configurer les types de fichiers d’entrée et de sortie en fonction de leurs propres flux de données. 

Un ensemble de données de test est disponible en ligne ici:

[https://github.com/nrcan-cfs-fire/cffdrs-ng/blob/main/data/wx_prf.csv](https://github.com/nrcan-cfs-fire/cffdrs-ng/blob/main/data/wx_prf.csv) (en anglais) 

Remarque sur les termes : 

Les calculs du système d’IFM ont été conçus à l’origine pour être effectués à partir des données enregistrées par les stations météorologiques locales. Par conséquent, les descriptions ci-dessous font référence aux données des stations météorologiques. En réalité, toutes les données météorologiques qui présentent une estimation représentative du temps selon les paramètres standard requis pour l’entrée du système IFM peuvent être utilisées (p. ex. données maillées et données de prévision). Voir le guide météo afin d’obtenir une description des normes d’entrée des données météorologiques, pour le système IFM. 

### Exécuter l’IFM2025 

Page principale où se trouve tout le code relatif au développement de la PG-MCEDIF: 

[https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main) (en anglais)

Pour chaque langage de programmation, deux scripts sont nécessaires afin de générer des sorties d’IFM2025 : 

1. IFM de PG : Contient les fonctions et les équations permettant de générer des sorties d’IFM2025.

    R : **NG_FWI.r**  
    Python : **NG_FWI.py**  
    C : **NG_FWI.c**

2. util : Inclut des fonctions de base qui ne font pas partie des équations de l’IFM2025, mais qui génèrent de l’information intermédiaire pour le calcul des composantes de l’IFM2025 (p. ex. heure du lever et du coucher du soleil et nombre d’heures d’ensoleillement). Ce script comprend également le processus de génération du résumé quotidien.

    R : **util.r**  
    Python : **util.py**  
    C : **util.c**, **util.h**

### Progiciels
Chaque langage est associé à des dépendances de bibliothèque ou de progiciel. Il doit être installé avant l’exécution de NG_FWI.

R : lubridate et data.table  
Python : datetime, logging, math, numpy, pandas, os.path, sys  
C : stdlib.h, stdbool.h, string.h 

### INTRANTS 

Les intrants de l’IFM2025 comprennent des variables météorologiques horaires et une estimation du traitement. Pour en savoir plus sur les intrants du système d’IFM, cliquez ici. 

En-têtes de colonnes et structure des données d’entrée : 

| Colonne | Description |
| --- | --- |
| `id` | Identifiant de la station météorologique; numéro unique pour la station, texte ou numéro |
| `lat` | Latitude. Emplacement de la station météorologique, en degrés décimaux (double précision) |
| `long` | Longitude. Emplacement de la station météorologique, en degrés décimaux (double précision) |
| `yr` | Année de relevé de la station météorologique (AAAA) |
| `mon` | Mois du relevé de la station météorologique; M ou MM (doit être cohérent dans l’ensemble du jeu de données) |
| `day` | Jour du relevé de la station météorologique, DD ou D (doit être cohérent dans l’ensemble du jeu de données) |
| `hr` | Heure de la lecture de la station météorologique, nombre en heure militaire (0-23) |
| `temp` | Température en °Celsius, en chiffre |
| `rh` | Humidité relative en pourcentage, en chiffre (0-100) |
| `ws` | Vitesse du vent en km/h, en chiffre |
| `prec` | Précipitations (pluie) mesurées en millimètres (mm), en chiffre |
| `solrad` | Rayonnement solaire mesuré en kW/m2 (kilowatts par mètre carré) pour les codes des herbacés, en chiffre. Entrée OPTIONNELLE, l’IFM2025 génère la méthode par défaut. (en savoir plus sur les capteurs de rayonnement solaire et les exigences minimales) |
| `percent_cured` | Pourcentage d’herbacés fanés dans les prairies ouvertes, mesuré en pourcentage pour les codes d’herbacés, en chiffre (0-100). Entrée OPTIONNELLE, l’IFM2025 génère la méthode par défaut | 

En plus des variables météorologiques, la fonction permettant de générer des sorties d’IFM2025 horaires nécessite le fuseau horaire où la station météorologique est située et la valeur de démarrage pour les codes d’humidité (p. ex. ICL de 85, IH [indice de l’humus] de 6 et IS [indice de sécheresse] de 15). Voir la section suivante pour savoir où ils sont utilisés. 

Les en-têtes de colonne peuvent être en minuscules ou en majuscules, tandis que le format de sortie est paramétré en majuscules. 

### Calcul des composants du système d’IFM et fichier de synthèse 

La fonction du fichier NG_FWI est conçue pour générer des sorties du système d’IFM pour une station à la fois, mais peut s’adapter à une entrée correctement formatée pour plusieurs stations, dans les versions R et Python. Exception : la version C nécessite la saisie d’une seule année pour une station donnée. 

La fonction permettant de générer des sorties d’IFM2025 se trouve dans le fichier NG_FWI et se présente comme suit : 

R : 
```r
hFWI(df_wx, timezone, ffmc_old, dmc_old, dc_old)
```

| Paramètres | Description |
| --- | --- |
| `df_wx` | cadre de données ou tableau formaté (peut avoir plusieurs années et stations, doit être séquentiel dans le temps au cours d’une année donnée) |
| `timezone` | fuseau horaire dans lequel se trouve la station météorologique, exprimé en nombre d’heures de décalage par rapport à UTC (p. ex., pour les stations situées à l’heure normale du Centre, le fuseau horaire est fixé à -6) |
| `ffmc_old` | la valeur initiale du code d’humidité fine des combustibles (p. ex. 85, valeur par défaut) |
| `dmc_old` | la valeur initiale de l’indice de l’humus (IH) (p. ex. 6, valeur par défaut) |
| `dc_old` | la valeur initiale de l’indice de sécheresse (IS) (p. ex. 15, valeur par défaut) |

Python :
```python
hFWI(df_wx, timezone, ffmc_old=85, dmc_old=6, dc_old=15, silent=False)
```

| Paramètre | Description |
| --- | --- |
| `df_wx` | cadre de données ou tableau formaté (peut avoir plusieurs années et stations, doit être séquentiel dans le temps au cours d’une année donnée) |
| `timezone` | fuseau horaire dans lequel se trouve la station météorologique, exprimé en nombre d’heures de décalage par rapport à UTC (p. ex., pour les stations situées à l’heure normale du Centre, le fuseau horaire est fixé à -6) |
| `ffmc_old` | la valeur initiale du code d’humidité fine des combustibles (p. ex. 85, valeur par défaut) |
| `dmc_old` | la valeur initiale de l’indice de l’humus (IH) (p. ex. 6, valeur par défaut) |
| `dc_old` | la valeur initiale de l’indice de sécheresse (IS) (p. ex. 15, valeur par défaut) |
| `silent` | imprimer les messages de progression afin de surveiller le script. Vrai ou Faux; Faux par défaut |

C :  

La version C peut être exécutée à partir de la ligne de commande avec les arguments suivants, dans l’ordre : 

| Code | Description |
| --- | --- |
| `local GMToffset` |  |
| `starting FFMC` |  |
| `starting DMC` |  |
| `starting DC` |  |
| `input file` | nom du fichier .csv contenant les données d’une seule station au cours d’une année |
| `output file` | nom du fichier dans lequel les résultats doivent être enregistrés |

### Résultats 

Des colonnes sont ajoutées au tableau des données d’entrée et un deuxième tableau de données récapitulatives est généré.

Colonnes de sortie qui sont ajoutées au tableau des données météorologiques horaires: 

| Colonne | Description |
| --- | --- |
| `timestamp` | date et heure des variables météorologiques et d’IFM. Format : AAAA-MM-JJ HH:MM:SS. (pas en langage C) |
| `date` | AAAA-MM-JJ Type de date (sans hh:mm:ss). (pas en langage C) |
| `sunrise` | Heure du lever du soleil en fonction de la latitude, de la longitude et de la date (heure décimale). (pas en langage C) |
| `sunset` | Heure du coucher du soleil en fonction de la latitude, de la longitude et de la date (heure décimale). (pas en langage C) |
| `sunlight_hours` | Nombre d’heures entre le lever et le coucher du soleil (heure décimale). (pas en langage C) |
| `solrad` | Rayonnement solaire mesuré en kW/m2 (kilowatts par mètre carré) pour les codes d’herbacés, généré automatiquement s’il n’est pas indiqué dans l’entrée (en chiffre). (doit être calculé à l’aide de make_inputs.c s’il n’est pas donné) |
| `percent_cured` | pourcentage de combustibles fanés (morts) dans les prairies, généré automatiquement s’il n’est pas indiqué dans l’entrée. Utilisé exclusivement dans les calculs relatifs aux prairies. Pourcentage sous forme de nombre (0-100). (doit être calculé à l’aide de make_inputs.c s’il n’est pas donné) |
| `grass_fuel_load` | La quantité de combustible herbacé standard est intégrée aux codes Python et R, soit 0,35 kg/m2. (doit être calculée à l’aide de make_inputs.c si elle n’est pas donnée, elle génère une colonne associée à la valeur standard) |
| `ffmc` |  |
| `dmc` |  |
| `dc` |  |
| `isi` |  |
| `bui` |  |
| `fwi` |  |
| `dsr` |  |
| `gfmc` |  |
| `gsi` |  |
| `gfwi` |  |

Les résultats horaires d’IFM2025 peuvent être résumés de différentes manières, et pour inciter les utilisateurs à réfléchir aux résumés qui seraient pertinents dans leur situation, une fonction du fichier « util » résume la journée en quelques mesures de base. 

Fonction permettant de générer des résumés quotidiens : 

R (trouvé dans util.r) : 

```r
generate_daily_summaries <- function(hourly_data) {} 
```

Lorsque : hourly_data = le cadre de données de sortie généré par NG_FWI 

Python (trouvé dans util.py) : 

```python
def generate_daily_summaries(hourly_data): 
```

Lorsque : hourly_data = les données de sortie générées par NG_FWI 

C (trouvé dans util.h) :

```c
hourly_data = le cadre de données de sortie généré par NG_FWI
```

Résumé quotidien des sorties : 

| Colonne | Description |
| --- | --- |
| `wstnid` | identifiant de la station météorologique, ou identifiant unique de la station météorologique |
| `year` | année, AAAA, en chiffre (p. ex. 2024) |
| `mon` | mois, M, en chiffre (p. ex. 3) |
| `day` | jour, J, en chiffre (p. ex. 8) |
| `sunrise` | Heure du lever du soleil. Format de l’horodatage HH:MM:SS, en heure militaire (p. ex. 06:30:55) |
| `sunset` | Heure du coucher du soleil. Format de l’horodatage HH:MM:SS, en heure militaire (p. ex. 19:45:05) |
| `peak_time` | Heure, H, en heure militaire (0-23), en format numérique. Heure à laquelle on peut s’attendre à un comportement maximal du feu, exprimé par un indice de propagation initiale (IPI) modifié (voir les définitions de wind_speed_smoothed et peak_isi_smoothed cidessous). Si l’IPI de pointe (du champ peak_isi_smoothed) est inférieur à cinq, l’heure de pointe est fixée à 17 heures |
| `duration` | nombre d’heures, en format numérique. Peut également être appelé durée d’une fenêtre de combustion. Il s’agit du nombre d’heures dans la journée où l’on peut s’attendre à un incendie actif (lorsque l’IPI modifié est égal ou supérieur à cinq). Si l’IPI n’a pas atteint 5 ou plus, la valeur de la durée de la fenêtre de coombustion est de zéro |
| `wind_speed_smoothed` |  Vitesse du vent (km/h), double précision. La vitesse horaire du vent enregistrée en fonction d’une moyenne de 10 minutes peut être erronée d’une heure à l’autre, ce qui rend difficile l’estimation de la durée d’une fenêtre de brûlage. Pour estimer la durée d’une fenêtre de brûlage et l’heure de pointe, la vitesse du vent horaire est ajustée et l’PSI est recalculé en fonction de la vitesse du vent ajustée et de l’ICLitesse du vent (km/h), double précision. La vitesse horaire du vent enregistrée en fonction d’une moyenne de 10 minutes peut être erronée d’une heure à l’autre, ce qui rend difficile l’estimation de la durée d’une fenêtre de brûlage. Pour estimer la durée d’une fenêtre de brûlage et l’heure de pointe, la vitesse du vent horaire est ajustée et l’PSI est recalculé en fonction de la vitesse du vent ajustée et de l’ICL |
| `peak_isi_smoothed` | Indice de propagation initiale (IPI) maximal recalculé en fonction de l’ICL et de la vitesse du vent ajustée à partir de wind_speed_smoothed; en chiffre pour une double précision. En chiffre, double précision |
| `ffmc` | Indice du combustible léger correspondant l’ICL à l’heure de pointe. En chiffre, double précision |
| `dmc` |  |
| `dc` |  |
| `isi` |  |
| `bui` |  |
| `fwi` |  |
| `dsr` |  |
| `gfmc` |  |
| `gsi` |  |
| `gfwi` |  |

## Licence

[GPL-2.0 Licence](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main?tab=GPL-2.0-1-ov-file#readme) (en anglais)