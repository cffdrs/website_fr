<a href="https://cffdrs.github.io/website_en/home/" target="_self" style="float: right;"> English </a>

# Accueil

## À propos

La [Méthode canadienne d’évaluation des dangers d’incendie de forêt (MCEDIF)](https://ressources-naturelles.canada.ca/forets-foresterie/feux-vegetation/methode-canadienne-evaluation-dangers-incendie-foret) est la principale source d’information sur les incendies à la disposition de toutes les [agences de gestion des incendies de forêt](https://www.canada.ca/fr/securite-publique-canada/campagnes/feux-de-foret/prov.html) au Canada. Elle est largement utilisée comme outil de sécurité et de sensibilisation, tant à l’échelle régionale qu’en bordure de feu. La MCEDIF fait l’objet de révisions approfondies sous le nom de [MCEDIF de prochaine génération (PG-MCEDIF)](https://ostrnrcan-dostrncan.canada.ca/handle/1845/245410). Le déploiement auprès des praticiens se passe présentement.  L'objectif principal est de mettre à jour le système pour permettre l'utilisation de technologies et de sources de données modernes tout en conservant sa simplicité et son efficacité initiales.  

Ce site web est destiné à :

- informer les utilisateurs des changements apportés à la MCEDIF 
- centraliser l’accès au code et à la documentation
- héberger des tutoriels pour les nouveaux utilisateurs

Rejoignez notre <a href="../ressources/#inscription" target="_self">liste de diffusion</a> des mises à jour par e-mail sur les derniers développements de MCEDIF2025.

Pour ceux qui ne connaissent pas la MCEDIF ou pour obtenir des informations officielles sur les incendies forestiers au Canada, consultez les pages officielles du gouvernement du Canada sous la rubrique <a href="../ressources/#liens-web" target="_self">Ressources#Liens Web</a>. 

---

## Annonces

### Juin 2026
Nous avons le plaisir de vous informer que des fichiers Excel contenant une calculatrice d'IFM2025 sont désormais à votre disposition. Ces fichiers constituent une méthode alternative aux calculs utilisant le code C, Python ou R. Ils offrent une interface visuelle simple pour l'entrée des données météorologiques d'une seule station. Veuillez vous référer à la page <a href="../ressources/#les-calculatrices-excel" target="_self">Ressources</a> pour y trouver le manuel d'utilisateur ainsi que les capsules video explicatives.

### Annonces précédentes

#### Fevrier 2026
Au cours des six dernières semaines, le Groupe sur le danger d'incendie a organisé trois ateliers en personne sur l'IFM2025 à travers le pays. Chaque session s'est concentrée sur la présentation des mises à jour de la Méthode, l'introduction des nouvelles composantes du danger d'incendie de la prairie et le partage d'une proposition de méthode de classification nationale du danger d'incendie.

Une mise à jour du code a été publiée afin de mettre à jour les méthodes de conversion des données météorologiques quotidiennes en données horaires. Un nouveau tutoriel est disponible <a href="../tutoriels/#daily-to-hourly" target="_self">ici</a> (en anglais). Plus de détails sur la mise à jour peuvent être trouvés sur le [changelog GitHub](https://github.com/nrcan-cfs-fire/cffdrs-ng/blob/main/CHANGELOG.md#2026-02-27) (en anglais).

#### Archive
- <a href="../accueil/annonces_2025" target="_self">2025</a>

---

<h3 style="text-align: center; font-style: italic;"> Traduction en cours </h3>
## FAQ

- <a href="#can-fwi2025-be-used-with-the-current-fbp-system" target="_self">Can FWI2025 be used with the current FBP system?</a>
- <a href="#why-is-timezone-required-and-how-do-i-determine-it" target="_self">Why is timezone required and how do I determine it?</a>

<br>

#### Can FWI2025 be used with the current FBP system?

*As of February 2026:*

Feedback from users is crucial, and to that effect – we have heard valuable feedback on the compatibility between the Fire Weather Index 2025 (FWI2025) System and the current Fire Behaviour Prediction (FBP) System that needs to be addressed. FWI2025 is related to a new danger-rating system. It has not yet been linked to absolute (rather than relative) quantities of fire behaviour prediction and therefore should not be used with FBP1992 at this time. Linking of FWI2025 and fire behaviour prediction will come with (interim) iFBP2025. As for what agencies can do, they can implement FWI2025 in parallel with FWI1987 to take advantage of its new capabilities and help us with ongoing testing. Some of those new capabilities include:

- Tracking moisture in fast drying fine fuels like the Fine Fuel Moisture Code
- Provide indication of overnight burning
- Better indicators for ignition, spread and intensity with the Grassland FWI System components (Grassland Fuel Moisture Code, Grassland Spread Index, Grassland Fire Weather Index)
- Better indicator of peak fire danger with calculations of the FWI System components in near-real time

For FBP inputs, they should continue to use FWI1987 for operational decisions, though testing FWI2025 with FBP1992 and providing feedback would be valuable. Work is ongoing to quantify the differences between FWI2025 and FWI1987 in relation to the effect on fire behaviour using the current FBP System (FBP1992). We will communicate our findings this spring via our communication channels.  But, at this time, **FWI2025 should not be used as an input to the FBP System**.  

<br>

#### Why is timezone required and how do I determine it?
`timezone` is one of the required parameters to run FWI2025. More specifically, it is the UTC offset corresponding to the times in a dataset, and should be given in units of hours. It is required because it is an essential piece of information to be able to calculate sunrise and sunset times, along with latitude and longitude.  

If you know your weather data was collected in Local Standard Time (LST), the `timezone` parameter is simply the [UTC offset of the LST](https://en.wikipedia.org/wiki/List_of_UTC_offsets). This is true for any dataset that followed the [old CFFDRS standard](https://ostrnrcan-dostrncan.canada.ca/handle/1845/219568) of collecting daily weather data at noon LST. For example, [Eastern Standard Time](https://en.wikipedia.org/wiki/Eastern_Time_Zone) is 5 hours behind Coordinated Universal Time (UTC), which corresponds to a `timezone` input of -5. To find the UTC offset of a date and location programmatically, see the corresponding FWI2025 tutorial appendices for <a href="../tutoriels/IFM_horaire_Python/#appendix-timezone" target="_self">Python</a> and <a href="../tutoriels/IFM_horaire_R/#appendix-timezone" target="_self">R</a>.  

The other common practise for weather data is to collect it in UTC. In this case, `timezone` should be set to 0. If you know a dataset was collected in Local Daylight Time (LDT), this should be one hour ahead of LST, so add 1 to the UTC offset of the LST.  

If you do not know the UTC offset used for a dataset, the only thing you can do is guess what it is based on the diurnal fluctuations of the weather variables. Feel free to <a href="../contact" target = "_self">contact us</a> for more information or guidance.
