<a href="https://cffdrs.github.io/website_en/code/" target="_self" style="float: right;"> English </a>

# Code

## Référentiel

Le [référentiel GitHub cffdrs-ng](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main) (en anglais) contient le code à jour des modules MCEDIF2025 dans trois langages de programmation : *R*, *Python* et *C* (**tout le code C est encore en cours de développement**). Ces trois versions sont écrites pour produire les mêmes résultats, de sorte que les utilisateurs peuvent choisir la version qui correspond à leurs propres systèmes logiciels.

Voir le [README du référentiel](https://github.com/nrcan-cfs-fire/cffdrs-ng?tab=readme-ov-file#readme) (en anglais) pour plus d'informations sur la façon de fournir des rapports de bogues, la structure du référentiel, et notre processus de mise à jour. Pour les notifications par courriel concernant les mises à jour du code, tu peux spécifier le type de mises à jour à recevoir lorsque tu <a href="../ressources/#inscription" target="_self">joins notre liste de diffusion</a>.

## Capacités
- Calculer les codes et indices IFM toutes les heures
- Calcule les résumés quotidiens des paramètres IFM au moment du pic de brûlage
- Calculer le code et les indices des prairies toutes les heures
- Calculer le lever et le coucher du soleil à partir de la date et du lieu, ainsi que le rayonnement solaire supplémentaire à partir des données météorologiques locales
- Convertir les données météorologiques quotidiennes traditionnelles de midi en données météorologiques quotidiennes minimales/maximales
- Convertir les données météorologiques quotidiennes minimales/maximales en données météorologiques horaires

## Indice forêt-météo 2025

[L'indice canadien de risque d'incendie de forêt (IFM)](https://cwfis.cfs.nrcan.gc.ca/renseignements/sommaire/fwi) est un sous-système important du MCEDIF. L'IFM2025 est la prochaine génération de la méthode IFM correspondant au MCEDIF2025. On décrit ci-après les fichiers, les intrants, les paramètres et les résultats de manière générale pour les trois langues, en soulignant les variations propres à chacune.

### Scripts

Chaque langage de programmation dispose de trois scripts nécessaires à la génération des résultats IFM2025 :

1. « NG_FWI » contient les fonctions et les équations permettant de générer les résultats IFM2025  

    R : **NG_FWI.r**  
    Python : **NG_FWI.py**  
    C : **NG_FWI.c**  

2. « util » comprend les fonctions de base qui ne font pas partie des équations FWI2025, mais qui génèrent des informations intermédiaires pour le calcul des composants FWI2025 (par ex. heure du lever et du coucher du soleil, nombre d'heures d'ensoleillement)  

    R : **util.r**  
    Python : **util.py**  
    C : **util.c**, **util.h**  

3. « daily_summaries » comprend le processus de génération du résumé quotidien des résultats  

    R : **daily_summaries.r**  
    Python : **daily_summaries.py**  
    C : (*en cours de développement*)  

### Packages

Les scripts IFM2025 nécessitent différents ensembles de bibliothèques ou de packages spécifiques à chaque langage. Ceux-ci doivent être installés avant d'exécuter « NG_FWI ».  

R : `lubridate`, `data.table`  
Python : `datetime`, `logging`, `math`, `numpy`, `pandas`, `os.path`, `sys`  
C : `stdlib.h`, `stdbool.h`, `string.h`

### Pour commencer

Le [référentiel GitHub cffdrs-ng](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main) (en anglais) comprend également un script tutoriel et des données de test. Consultez la section <a href="../tutoriels" target="_self">Tutoriels#IFM</a> horaire pour obtenir un aperçu étape par étape du flux de travail avec des données horaires. La documentation ci-dessous fournit des détails sur les fonctions spécifiques et les exigences en matière de données.

### Format

Le code IFM2025 est écrit et testé à l'aide de données d'intrant sous forme de tableau/matrice, généralement importées sous forme de fichiers CSV (valeurs séparées par des virgules, .csv). Les résultats sont également présentés sous la même forme de tableau/matrice. Les utilisateurs peuvent configurer les types de fichiers d'intrant et de résultat en fonction de leurs flux de données individuels.

### Documentation

#### Indice horaire de risque d'incendie

La fonction `hFWI()` du fichier « NG_FWI » est conçue pour générer les résultats de la méthode IFM pour une station à la fois. Les versions R et Python peuvent également fournir les résultats pour plusieurs stations avec des entrées correctement formatées. La version C ne peut traiter que les entrées d'une seule année pour une station donnée.

##### Données d'intrants

Le système d'indice de risque d'incendie a été initialement conçu pour être calculé à partir des données enregistrées par les *stations météorologiques* locales. Par conséquent, les descriptions ci-dessous font référence aux données des stations météorologiques comme intrants. En réalité, toutes les données météorologiques collectées ou calculées (par ex. données d'ensemble, données de prévision, etc.) qui comprennent les variables standard requises comme intrants pour la méthode IFM peuvent être utilisées. Voir le [Guide météorologique](https://ostrnrcan-dostrncan.canada.ca/handle/1845/219568) pour une description des normes d'entrée des données météorologiques pour la méthode IFM.  

Les lignes du cadre de données doivent correspondre à des données horaires consécutives. Les colonnes et les types de données du cadre de données d'entrée sont les suivants :  

| Colonne | Description |
| --- | --- |
| `id` | Identifiant de la station météorologique, numéro unique attribué à la station, texte ou chiffre |
| `lat` | Latitude de la station météorologique, en degrés décimaux (°) (double précision) |
| `long` | Longitude de la station météorologique, en degrés décimaux (°) (double précision) |
| `yr` | Année de la lecture de la station météorologique, nombre AAAA |
| `mon` | Mois de la lecture de la station météorologique, nombre M ou MM (doit être cohérent dans l'ensemble des données) |
| `day` | Jour de la lecture de la station météorologique, nombre DD ou D (doit être cohérent dans l'ensemble des données) |
| `hr` | Heure de la lecture de la station météorologique, nombre en heure militaire (0-23) |
| `temp` | Température en degrés Celsius (°C), nombre |
| `rh` | Humidité relative en pourcentage (%), nombre (0-100) |
| `ws` | Vitesse du vent en kilomètres par heure (km/h), nombre |
| `prec` | Précipitations (pluie) mesurées en millimètres (mm), nombre |
| `solrad` | Rayonnement solaire mesuré en kilowatts par mètre carré (kW/m^2) pour les codes de prairie, nombre. Entrée FACULTATIVE, IFM2025 la générera selon la méthode par défaut. ([MCEDIF rayonnement solaire IFM (draft)](../documents/MCEDIF2025_rayonnement-solaire-IFM.pdf)📥) |
| `percent_cured` | Pourcentage de fané des graminées dans les prairies ouvertes, mesuré en pourcentage pour les codes de prairies, nombre (0-100). Entrée FACULTATIVE, l'IFM2025 la générera selon la méthode par défaut | 

Les en-têtes de colonne peuvent être en minuscules ou en majuscules, le format des résultats est défini en majuscules.  

En plus des variables météorologiques, la fonction permettant de générer des résultats IFM2025 horaires nécessite le fuseau horaire dans lequel se trouve la station météo et la valeur de démarrage pour les codes d'humidité (par ex. ICL de 85, IH de 6 et IS de 15). Voir la section suivante pour savoir où cela est spécifié.  

##### Paramètres de la fonction

R :  
```r
hFWI(df_wx, timezone, ffmc_old = 85, dmc_old = 6, dc_old = 15)
```

| Paramètres | Description |
| --- | --- |
| `df_wx` | Cadre de données ou tableau formaté (peut comporter plusieurs années et stations, doit être séquentiel dans le temps au cours d'une année donnée) |
| `timezone` | Fuseau horaire dans lequel se trouve la station météorologique, exprimé en nombre d'heures de décalage par rapport à l'UTC (par ex. pour les stations situées dans le fuseau horaire Central Standard, le fuseau horaire est réglé sur -6) |
| `ffmc_old` | Valeur de démarrage de l'indice du combustible léger (p. ex. 85, valeur par défaut) |
| `dmc_old` | Valeur de démarrage de l'indice de l'humus (par ex. 6, valeur par défaut) |
| `dc_old` | Valeur de démarrage de l'indice de sécheresse (par ex. 15, valeur par défaut) |


Python:  
```python
hFWI(df_wx, ffmc_old = 85, dmc_old = 6, dc_old = 15, silent = False)
```

| Paramètre | Description |
| --- | --- |
| `df_wx` | Cadre de données ou tableau formaté (peut comporter plusieurs années et stations, doit être séquentiel dans le temps au cours d'une année donnée) |
| `timezone` | Fuseau horaire dans lequel se trouve la station météorologique |
| `ffmc_old` | Valeur de démarrage de l'indice du combustible léger (par ex. 85, valeur par défaut) |
| `dmc_old` | Valeur de démarrage de l'indice de l'humus (par ex. 6, valeur par défaut) |
| `dc_old` | Valeur de démarrage de l'indice de sécheresse (par ex. 15, valeur par défaut) |
| `silent` | Imprimer les messages de progression pour surveiller le script. Vrai ou faux, faux par défaut |

C:  
La version C peut être exécutée à partir de la ligne de commande avec les arguments suivants dans l'ordre :  

| Code | Description |
| --- | --- |
| `local GMToffset` | Fuseau horaire dans lequel se trouve la station météorologique |
| `starting FFMC` | Valeur de démarrage de l'indice du combustible léger (par ex. 85) |
| `starting DMC` | Valeur de démarrage de l'indice de l'humus (par ex. 6) |
| `starting DC` | Valeur de démarrage de l'indice de sécheresse (par ex. 15) |
| `input file` | Nom du fichier .csv contenant les données d'une seule station sur une année |
| `output file` | Nom du fichier dans lequel les résultats sont enregistrés |

##### Description des résultats

Les résultats sont également au même format que les données d'entrée, avec les colonnes suivantes ajoutées :  

| Colonne | Description |
| --- | --- |
| `timestamp` | Date et heure de la variable météorologique et IFM. Horodatage AAAA-MM-JJ HH:MM:SS. (pas en C) |
| `date` | AAAA-MM-JJ Type de date (sans hh:mm:ss). (pas en C) |
| `sunrise` | Heure du lever du soleil en fonction de la latitude, de la longitude et de la date en heure militaire (heure décimale). (pas en C) |
| `sunset` | Heure du coucher du soleil en fonction de la latitude, de la longitude et de la date en heure militaire (heure décimale). (pas en C) |
| `sunlight_hours` | Nombre d'heures (hr) entre le lever et le coucher du soleil (heure décimale). (pas en C) |
| `solrad` | Rayonnement solaire mesuré en kilowatts par mètre carré (kW/m^2) pour les codes de prairie, généré automatiquement s'il manque dans les intrants (nombre). (doit être calculé à l'aide de make_inputs.c s'il n'est pas fourni) |
| `percent_cured` | Pourcentage de combustibles végétaux fanés (morts) dans les prairies, généré automatiquement s'il manque dans les intrants. Utilisé exclusivement dans les calculs relatifs aux prairies. Pourcentage sous forme de nombre (0-100). (doit être calculé à l'aide de make_inputs.c s'il n'est pas fourni) |
| `grass_fuel_load` | La charge standard de combustible herbacé est intégrée dans le code Python et R, 0,35 kg/m^2. (doit être calculé à l'aide de make_inputs.c s'il n'est pas fourni, génère une colonne avec la valeur standard) |
| `ffmc` | Indice du combustible léger (ICL, nombre) |
| `dmc` | Indice de l'humus (IH, nombre) |
| `dc` | Indice de sécheresse (IS, nombre) |
| `isi` | Indice de propagation initiale (IPI, nombre) |
| `bui` | Indice du combustible disponible (ICD, nombre) |
| `fwi` | Indice forêt-météo (IFM, nombre) |
| `dsr` | Indice journalier de sévérité (DSR, nombre) |
| `gfmc` | Indice d'humidité de l'herbe, similaire à l'ICL (IHH, nombre 0-101) |
| `gsi` | Indice de propagation dans l'herbe (IPH, nombre) |
| `gfwi` | Indice du danger d'incendie pour l'herbe (IDIH, nombre) |

#### Résumés quotidiens

Les résultats horaires de l'IFM peuvent être résumés de différentes manières en fonction de l'utilisation et des besoins. Ces résumés se trouvent dans le script « daily_summaries ». `generate_daily_summaries()` résume les données horaires en quelques indicateurs quotidiens.  

##### Données d'intrant

Le seul intrant de `generate_daily_summaries()` est le résultat de `hFWI()`.

##### Paramètres de la fonction

R:  

```r
generate_daily_summaries <- function(hourly_data) {}
```

Python: 

```python
def generate_daily_summaries(hourly_data): 
```

C: 
```c
hourly_data = the output dataframe generated by NG_FWI
```

##### Description des résultats

| Colonne | Description |
| --- | --- |
| `wstnid` | Identifiant de la station météorologique ou identifiant unique de la station météorologique |
| `year` | Année, AAAA, nombre (par ex. 2024) |
| `mon` | Mois, M, nombre (par ex. 3) |
| `day` | Jour, J, nombre (par ex. 8) |
| `sunrise` | Heure du lever du soleil. Format d'horodatage HH:MM:SS en heure militaire (par ex. 06:30:55) |
| `sunset` | Heure du coucher du soleil. Format d'horodatage HH:MM:SS en heure militaire (par ex. 19:45:05) |
| `peak_time` | L'heure (hr) en format militaire (0-23), format numérique. L'heure à laquelle on peut s'attendre à un comportement maximal du feu, tel qu'exprimé par un IPI modifié (voir les définitions de wind_speed_smoothed et peak_isi_smoothed ci-dessous). Si l'IPI maximal (provenant du champ peak_isi_smoothed) est inférieur à cinq, le peak_time est fixé à 17 heures |
| `duration` | Nombre d'heures (hr), format numérique. Peut également être appelé durée d'une fenêtre de brûlage, nombre d'heures dans la journée où l'on peut s'attendre à un feu actif (où un IPI modifié est égal ou supérieur à cinq). Si l'IPI n'a pas atteint 5 ou plus, la durée est zéro |
| `wind_speed_smoothed` | Vitesse du vent en kilomètres par heure (km/h), double précision. La vitesse du vent enregistrée toutes les heures sur la base d'une moyenne de 10 minutes peut être bruyante d'une heure à l'autre, ce qui rend difficile l'estimation de la durée d'une fenêtre de brûlage. Pour estimer la durée d'une fenêtre de brûlage et l'heure de pointe, la vitesse du vent horaire est lissée et l'IPI est recalculé sur la base de la vitesse du vent lissée et de l'ICL |
| `peak_isi_smoothed` | Indice de propagation initiale maximale (IPI) recalculé à partir de l'ICL et de la vitesse du vent lissée à partir de « wind_speed_smoothed », nombre à double précision. Nombre, double précision |
| `ffmc` | Indice du combustible léger correspondant à l'ICL à l'heure du pic. Nombre, double précision |
| `dmc` | Indice d'humidité de l'humus correspondant à l'IH à l'heure du pic. Nombre, double précision |
| `dc` | Indice de sécheresse correspondant à l'IS à l'heure de pointe. Nombre, double précision |
| `isi` | Indice de propagation initiale correspondant à l'IPI à l'heure de pointe. Nombre, double précision |
| `bui` | Indice de combustible disponible correspondant à l'ICD à l'heure de pointe. Nombre, double précision |
| `fwi` | Indice forêt-météo correspondant à l'IFM à l'heure de pointe. Nombre, double précision |
| `dsr` | Indice journalier de sévérité correspondant au DSR à l'heure de pointe. Nombre, double précision |
| `gfmc` | Indice d'humidité de l'herbe correspondant au IHH à l'heure de pointe. Nombre, double précision |
| `gsi` | Indice de propagation dans l'herbe correspondant à l'IPH à l'heure de pointe. Nombre, double précision |
| `gfwi` | Indice du danger d'incendie pour l'herbe correspondant à l'IDIH à l'heure de pointe. Nombre, double précision |

## Licence

Les [scripts NG-CFFDRS](https://github.com/nrcan-cfs-fire/cffdrs-ng) sont sous licence GNU General Public License version 2 (GPL-2.0). Une copie de la licence est disponible sur le [référentiel GitHub](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main?tab=GPL-2.0-1-ov-file#readme) (en anglais).
