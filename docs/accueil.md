<a href="https://cffdrs.github.io/website_en/home/" target="_self" style="float: right;"> English </a>

# Accueil

## À propos

La [Méthode canadienne d’évaluation des dangers d’incendie de forêt (MCEDIF)](https://ressources-naturelles.canada.ca/forets-foresterie/feux-vegetation/methode-canadienne-evaluation-dangers-incendie-foret) est la principale source d’information sur les incendies à la disposition de toutes les [agences de gestion des incendies de forêt](https://ciffc.ca/mobilization-stats/member-agencies) (en anglais) au Canada. Elle est largement utilisée comme outil de sécurité et de sensibilisation, tant à l’échelle régionale qu’en bordure de feu. La MCEDIF fait l’objet de révisions approfondies sous le nom de [MCEDIF de prochaine génération (PG-MCEDIF)](https://ostrnrcan-dostrncan.canada.ca/handle/1845/245410). Le déploiement auprès des praticiens se passe présentement.  L'objectif principal est de mettre à jour le système pour permettre l'utilisation de technologies et de sources de données modernes tout en conservant sa simplicité et son efficacité initiales.  

Ce site web est destiné à :

- informer les utilisateurs des changements apportés à la MCEDIF 
- centraliser l’accès au code et à la documentation
- héberger des tutoriels pour les nouveaux utilisateurs

Rejoignez notre <a href="../ressources/#inscription" target="_self">liste de diffusion</a> des mises à jour par e-mail sur les derniers développements de MCEDIF2025.

Pour ceux qui ne connaissent pas la MCEDIF ou pour obtenir des informations officielles sur les incendies forestiers au Canada, consultez les pages officielles du gouvernement du Canada sous la rubrique <a href="../ressources/#apercu" target="_self">Ressources#Aperçu</a>. 

<img 
    style="display: block;
           width: 75px;
           padding: 4px;
           margin: 10px 25px 0px 0px;
           float: left;
           border-radius: 5px;
           background-color: #FFFFFF!important"
    src="../img/CFFDRS logoFRE.png" 
    alt="CFFDRS1992 logo">
</img>

L'ancien code MCEDIF1992 est toujours disponible sur le [GitHub de la MCEDIF](https://github.com/cffdrs) (en anglais), tandis que la documentation R se trouve sur la [page CRAN de la MCEDIF](https://cran.r-project.org/web/packages/cffdrs/) (en anglais).

## Annonces

### Septembre 2025
Une mise à jour majeure du code de IFM2025 a été publiée sur le [dépôt GitHub cffdrs-ng](https://github.com/nrcan-cfs-fire/cffdrs-ng) (en anglais). Elle inclut des changements dans les options lors de l'exécution de `hFWI()`, la structure des fichiers du dépôt, et la façon dont l'IH et le rayonnement solaire sont calculés. Plus de détails et le reste des changements peuvent être trouvés sur le [changelog GitHub](https://github.com/nrcan-cfs-fire/cffdrs-ng/blob/main/CHANGELOG.md#2025-09-10) (en anglais). Ce site web a également été mis à jour afin de disposer d'une documentation actualisée dans les sections <a href="../code" target="_self">Code</a> et <a href="../tutoriels" target="_self">Tutoriels</a>.

### Annonces précédentes

#### Août 2025
Une mise à jour mineure a été publiée dans le dépôt GitHub MCEDIF. Les changements spécifiques peuvent être trouvés dans le [changelog de GitHub](https://github.com/nrcan-cfs-fire/cffdrs-ng/blob/main/CHANGELOG.md#2025-08-22) (en anglais), qui comprend également des informations supplémentaires sur la prochaine mise à jour (à venir). Une <a href="../code/#capacites" target="_self">liste des habiletés</a> est maintenant disponible.

Natasha Jurko et Gabrielle Ayres ont animé le deuxième webinaire du Groupe sur le danger des incendies, discutant des nouvelles modifications de l'IFM2025 par rapport à la version IFM1987. L'enregistrement est disponible sur la <a href="../ressources/#serie-de-seminaires" target="_self">page Ressources</a>.

#### Juin 2025
Nous avons récemment mis à jour le référentiel GitHub cffdrs-ng [README](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main?tab=readme-ov-file#readme) (en anglais) et les [directives de contribution](https://github.com/nrcan-cfs-fire/cffdrs-ng/blob/main/CONTRIBUTING.md) (comment fournir des commentaires sur le code et signaler des bogues, en anglais). Nous publierons prochainement notre liste de fonctionnalités, une FAQ et une feuille de route détaillant notre processus de mise à jour du code pour MCEDIF2025. Comme toujours, vous pouvez nous contacter pour nous faire part de vos idées et questions générales à l'adresse courriel de notre équipe :  

[firedanger-dangerincendie@nrcan-rncan.gc.ca](mailto:firedanger-dangerincendie@nrcan-rncan.gc.ca)

#### Mai 2025
Natasha Jurko et Sam LaCarte ont animé un <a href="../ressources/#grasslands-in-the-fire-weather-index-system-mai-2025" target="_self">webinaire</a> présentant les composantes d'herbes de l'IFM (IFM2025) le 22 mai. Il s'agissait du premier d'une série de webinaires destinés à faciliter les discussions avec le groupe sur les risques d'incendie. L'enregistrement sera mis à la disposition du public sur ce site web au début du mois de juin. En attendant, veuillez nous <a href="../contact" target="_self">envoyer un courriel</a> si vous souhaitez avoir accès à l'enregistrement.

#### Mars 2025
Le <a href="../ressources/#bulletin" target="_self">premier bulletin</a>
est désormais disponible. Il présente les nouvelles fonctionnalités de l'indice Forêt-Météo (IFM2025), notamment l'utilisation de données horaires et les nouveaux intrants et indices pour le danger d'incendie dans les prairies.

#### Janvier 2025
Le module du système d’indice forêt-météo (IFM) écrit en Python et en R peut actuellement être testé par les utilisateurs (le travail sur le langage C est en cours). La publication des autres modules de la MCEDIF (p. ex. systèmes PCI, AHC, et FIF) est provisoirement prévue pour l’automne 2025. 