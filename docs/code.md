<a href="https://cffdrs.github.io/website_en/code/" target="_self" style="float: right;"> English </a>

# Code

## Référentiel

Le [référentiel GitHub cffdrs-ng](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main) (en anglais) contient le code à jour des modules MCEDIF2025 dans trois langages de programmation : *R*, *Python* et *C* (**tout le code C est encore en cours de développement**). Ces trois versions sont écrites pour produire les mêmes résultats, de sorte que les utilisateurs peuvent choisir la version qui correspond à leurs propres systèmes logiciels.

Voir le [README du référentiel](https://github.com/nrcan-cfs-fire/cffdrs-ng?tab=readme-ov-file#readme) (en anglais) pour plus d'informations sur la façon de fournir des rapports de bogues, la structure du référentiel, et notre processus de mise à jour. Pour les notifications par courriel concernant les mises à jour du code, tu peux spécifier le type de mises à jour à recevoir lorsque tu <a href="../ressources/#inscription" target="_self">joins notre liste de diffusion</a>.

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

## Capacités
- Calculer les codes et indices IFM toutes les heures
- Calcule les résumés quotidiens des paramètres IFM au moment du pic de brûlage
- Calculer le code et les indices des prairies toutes les heures
- Calculer le lever et le coucher du soleil à partir de la date et du lieu, ainsi que le rayonnement solaire supplémentaire à partir des données météorologiques locales
- Convertir les données météorologiques quotidiennes traditionnelles de midi en données météorologiques quotidiennes minimales/maximales
- Convertir les données météorologiques quotidiennes minimales/maximales en données météorologiques horaires

## IFM2025

<div class="text-center">
	<button disabled class="btn btn-dark"">IFM2025 <br> C <br> en cours de construction</button>
	&emsp;
    <button class="btn btn-dark" onclick="location.href='../code/IFM2025_Python'">IFM2025 <br> Python</button>
	&emsp;
	<button class="btn btn-dark" onclick="location.href='../code/IFM2025_R'">IFM2025 <br> R</button>
</div>

## Licence

Les [scripts NG-CFFDRS](https://github.com/nrcan-cfs-fire/cffdrs-ng) sont sous licence GNU General Public License version 2 (GPL-2.0). Une copie de la licence est disponible sur le [référentiel GitHub](https://github.com/nrcan-cfs-fire/cffdrs-ng/tree/main?tab=GPL-2.0-1-ov-file#readme) (en anglais).
