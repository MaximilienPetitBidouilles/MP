---
date: '2025-04-03T13:29:30+02:00'
draft: false
title: 'API Zotero et tableau de bord'
author: Maximilien Petit
tags: ["HAL","Zotero","HCERES"]
readingTime: true
---
{{< toc >}}

# Le problème

On souhaite utiliser **un tableau de bord pour suivre l'évolution d'un chantier documentaire**, en l'occurrence le dépôt des notices HAL d'un laboratoire SHS pour la dernière campagne HCERES. Ce chantier repose, entre autres, sur l'utilisation d'une bibliothèque Zotero pour la validation des métadonnées des notices qui sont importées ensuite sur HAL par le biais de X2HAL.

Ce tableau de bord doit se coder rapidement et se mettre à jour en fonction des données qui sont contenues dans la bibliothèque Zotero.

Ce tableau de bord doit pouvoir utiliser sommairement **la visualisation de données** : un nuage de mots-clés (qui puise dans les titres des publications), un graphique des publications par type.

## Qui peut aider ?

C'est un travail qui relève de l'informatique, donc, les personnels ITRF de la BAP E. Et celles et ceux qui bidouillent dans les laboratoires (BAP D, BAP F). Il y a toujours également un ou deux bidouilleurs chevronnés dans les bibliothèques. On peut penser également aux réseaux des MSH qui, de plus en plus, bénéficient d'une ou deux personnes en appui aux structures pour les "humanités numériques".

## La bidouille

**On fait le choix de tout coder dans un seul fichier (HTML, CSS, JavaScript)** car l'usage sera avant tout personnel et situationnel (la campagne HCERES). Pour le graphique et le nuage de mots-clés, c'est **la bibliothèque Highcharts** qui est utilisée, avec Highcharts Word Cloud et Highcharts Boost Module. Tout repose également sur le paramétrage de l'API Zotero.

Le code partagé ici est largement améliorable (à votre bon coeur !) mais, en l'état, il fonctionne et pourrait être utile pour les laboratoires. **Le code est un peu "lourd"** (des duplications), la pagination dans les tableaux n'est pas satisfaisante. Le nuage de mots-clés et le graphique, de fait, alourdissent le fichier.

Ci-dessous, le code + le résultat dans une visionneuse HTML. Cliquez sur un auteur et patientez un peu pour l'affichage des données. Le nuage de mots-clés et le graphique son utilisés pour "Toutes les publications".

L'idée étant d'avoir, pour chaque chercheur, son nom + prénom, sa date d'arrivée dans l'unité, des identifiants utiles (scopus, scanR, idRef) et la liste de ses publications. C'est-à-dire, les publications qui sont dans la bibliothèque Zotero au coeur du chantier, et donc, qui sont déposées sur HAL.

Vous pouvez consulter le tableau de bord interactif ci-dessous :

<div style="border: 1px solid #ddd; border-radius: 8px; overflow: hidden;">
  <iframe src="/MP/html/10_code_fonctionnel_tableau_de_bord_37.html" width="100%" height="600" style="border: none;"></iframe>
</div>

Et le code à la suite : 

{{< code language="html" title="Code tableau de bord" open="false" >}}
<!DOCTYPE html>
<html>
<head>
<title></title>
<style type="text/css">
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
  }

  h2 {
    margin-top: 20px;
    text-align: center;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin: 20px 0;
    text-align: center;
  }

  ul li {
    display: inline-block;
    margin: 0 10px;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }

  th, td {
    padding: 10px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }

  th {
    background-color: #f2f2f2;
    font-weight: bold;
  }

  a {
    color: #007bff;
    text-decoration: none;
  }

  a:hover {
    text-decoration: underline;
  }

  #researcherInfoContainer {
    background-color: #f9f9f9;
    padding: 20px;
    margin-bottom: 20px;
  }

  #wordcloudContainer {
    margin-top: 20px;
    text-align: center;
  }

  #wordcloud {
    max-width: 600px;
    margin: 0 auto;
  }

  #publicationChartContainer {
    margin-top: 20px;
    text-align: center;
  }

  /* Ajouts CSS pour une meilleure ergonomie */
  #researcherInfoContainer h3 {
    margin-top: 0;
  }

  #publicationTable {
    border-collapse: collapse;
    margin-top: 20px;
  }

  #publicationTable th,
  #publicationTable td {
    padding: 10px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }

  #publicationTable th {
    background-color: #f2f2f2;
    font-weight: bold;
  }

  #publicationChartContainer {
    margin-top: 40px;
  }
</style>
<script src="https://code.highcharts.com/highcharts.js"></script>
<script src="https://code.highcharts.com/modules/wordcloud.js"></script>
<script src="https://code.highcharts.com/modules/boost.js"></script>
</head>
<body>
<!-- rest of your code -->
</body>
</html>

</style>
<script src="https://code.highcharts.com/highcharts.js"></script>
<script src="https://code.highcharts.com/modules/wordcloud.js"></script>
<script src="https://code.highcharts.com/modules/boost.js"></script>
</head>
<body>
<h2>Liste des chercheurs</h2>

<ul>
  <li><a href="#" onclick="showResearcherInfo('ambroise-rendu'); return false;">Anne-Claude Ambroise-Rendu</a></li>
  <li><a href="#" onclick="showResearcherInfo('moine'); return false;">Caroline Moine</a></li>
  <li><a href="#" onclick="showResearcherInfo('barjonet'); return false;">Aurélie Barjonet</a></li>
  <li><a href="#" onclick="showResearcherInfo('jollin'); return false;">Sophie Bertocchi-Jollin</a></li>
  <li><a href="#" onclick="showResearcherInfo('boudet'); return false;">Alexandra Boudet-Brugal</a></li>
  <li><a href="#" onclick="showResearcherInfo('guilhamon'); return false;">Lise Guilhamon</a></li>
  <li><a href="#" onclick="showResearcherInfo('geslot'); return false;">Jean-Charles Geslot</a></li>
  <li><a href="#" onclick="showResearcherInfo('dawes'); return false;">Simon Dawes</a></li>
  <li><a href="#" onclick="showResearcherInfo('bouffartigue'); return false;">Sylvie Bouffartigue</a></li>
  <li><a href="#" onclick="showResearcherInfo('mollier'); return false;">Jean-Yves Mollier</a></li>
  <li><a href="#" onclick="showResearcherInfo('dallet'); return false;">Sylvie Dallet</a></li>
  <li><a href="#" onclick="showResearcherInfo('stead'); return false;">Evanghelia Stead</a></li>
  <li><a href="#" onclick="showResearcherInfo('croisy'); return false;">Sophie Croisy</a></li>
   <li><a href="#" onclick="showResearcherInfo('flechet'); return false;">Anaïs Fléchet</a></li>
   <li><a href="#" onclick="showResearcherInfo('coquet'); return false;">Cécile Coquet-Mokoko</a></li>
   <li><a href="#" onclick="showResearcherInfo('olivesi'); return false;">Stéphane Olivesi</a></li>
   <li><a href="#" onclick="showResearcherInfo('kahan'); return false;">Alan Kahan</a></li>
   <li><a href="#" onclick="showResearcherInfo('cyna'); return false;">Esther Cyna</a></li>
   <li><a href="#" onclick="showResearcherInfo('guena'); return false;">Béatrice Guéna</a></li>
   <li><a href="#" onclick="showResearcherInfo('bazin'); return false;">Laurent Bazin</a></li>
   <li><a href="#" onclick="showResearcherInfo('giardino'); return false;">Gianni Giardino</a></li>
   <li><a href="#" onclick="showResearcherInfo('malandain'); return false;">Gilles Malandain</a></li>
   <li><a href="#" onclick="showResearcherInfo('ferre'); return false;">Sandrine Ferré-Rode</a></li>
   <li><a href="#" onclick="showResearcherInfo('hache'); return false;">Françoise Hache-Bissette</a></li>
   <li><a href="#" onclick="showResearcherInfo('hagimont'); return false;">Steve Hagimont</a></li>
   <li><a href="#" onclick="showResearcherInfo('hautbois'); return false;">Xavier Hautbois</a></li>
   <li><a href="#" onclick="showResearcherInfo('henneton'); return false;">Lauric Henneton</a></li>
   <li><a href="#" onclick="showResearcherInfo('levy'); return false;">Paule Levy</a></li>
   <li><a href="#" onclick="showResearcherInfo('mougin'); return false;">Pascal Mougin</a></li>
   <li><a href="#" onclick="showResearcherInfo('pauly'); return false;">Véronique Pauly</a></li>
   <li><a href="#" onclick="showResearcherInfo('pothier'); return false;">Jacques Pothier</a></li>
   <li><a href="#" onclick="showResearcherInfo('quenet'); return false;">Grégory Quenet </a></li>
   <li><a href="#" onclick="showResearcherInfo('rodd'); return false;">Adrien Rodd </a></li>
   <li><a href="#" onclick="showResearcherInfo('sourdeval'); return false;">Matthieu Sourdeval </a></li>
   <li><a href="#" onclick="showResearcherInfo('robinet'); return false;">François Robinet</a></li>
   <li><a href="#" onclick="showResearcherInfo('rialland'); return false;">Ivanne Rialland</a></li>
   <li><a href="#" onclick="showResearcherInfo('delporte'); return false;">Christian Delporte</a></li>
   <li><a href="#" onclick="showResearcherInfo('doc'); return false;">Les doctorants du CHCSC</a></li>
  <!-- Ajoutez autant de liens pour les chercheurs supplémentaires -->
  <li><a href="#" onclick="showAllPublications(); return false;">Toutes les publications</a></li>
</ul>

<div id="researcherInfoContainer"><!-- L'information sur les chercheurs sera affichée ici --></div>

<div id="wordcloudContainer"><!-- Le nuage de mots-clés sera affiché ici --></div>

<div id="publicationChartContainer"><!-- Le graphique des publications par type sera affiché ici --></div>

<table id="publicationTable" style="display: none;">
  <thead>
    <tr>
      <th>#</th>
      <th>Titre</th>
      <th>Auteur(s)</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
<script>
  var researchers = {
    'ambroise-rendu': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'VBNTR69L',
      arrivalDate: 'sept 2016',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=26665321600',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref056736029',
      idrefUrl: 'https://www.idref.fr/056736029'
    },
    'moine': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'A36SU8KS',
      arrivalDate: 'sept 2006',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=26536457700',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref08775116X',
      idrefUrl: 'https://www.idref.fr/08775116X'
    },
    'barjonet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '3A9SYXVH',
      arrivalDate: 'sept 2008',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=52963171600',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref111587042',
      idrefUrl: 'https://www.idref.fr/111587042'
    },
	'jollin': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '5Z7CRV9E',
      arrivalDate: 'sept 2007',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57189004468',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref055391001',
      idrefUrl: 'https://www.idref.fr/055391001'
    },
    'boudet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'MBCBNNBK',
      arrivalDate: 'fév 2013',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57346200300&origin=recordPage',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref099069016',
      idrefUrl: 'https://www.idref.fr/099069016'
    },
    'guilhamon': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'CP4ID5PH',
      arrivalDate: 'fév 2013',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57204576181&origin=recordPage',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref119706105',
      idrefUrl: 'https://www.idref.fr/119706105'
    },
    'geslot': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'ABZLT2WW',
      arrivalDate: 'sept 2013',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=37080651600',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref078786827',
      idrefUrl: 'https://www.idref.fr/078786827'
    },
    'dawes': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'Y7SKJBT9',
      arrivalDate: 'sept 2016',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=37661269400',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref220246416',
      idrefUrl: 'https://www.idref.fr/220246416'
    },
    'bouffartigue': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'CEK68ANV',
      arrivalDate: 'sept 2015',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57170860700&origin=recordPage',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref059581980',
      idrefUrl: 'https://www.idref.fr/059581980'
    },
    'mollier': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '3SE7MHIR',
      arrivalDate: '1992',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=26034079700',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref027033732',
      idrefUrl: 'https://www.idref.fr/027033732'
    },
    'dallet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'WB7DGG5C',
      arrivalDate: 'sept 2006',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=55458449300',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref028295250',
      idrefUrl: 'https://www.idref.fr/028295250'
    },
    'stead': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '3PMM4DH3',
      arrivalDate: 'sept 2010',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=28168057900',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref060786450',
      idrefUrl: 'https://www.idref.fr/060786450'
    },
    'croisy': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '474DZQUE',
      arrivalDate: 'fév 2013',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=55303832900',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref176586741',
      idrefUrl: 'https://www.idref.fr/176586741'
    },
    'flechet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'B9JDFTKP',
      arrivalDate: 'sept 2010',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=56330152900',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref084278390',
      idrefUrl: 'https://www.idref.fr/084278390'
    },
    'coquet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '3E2BNAS3',
      arrivalDate: 'sept 2019',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57189262943',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref050729772',
      idrefUrl: 'https://www.idref.fr/050729772'
    },
    'olivesi': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'L8XQRBJH',
      arrivalDate: 'oct 2015',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=26655991800',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref035701854',
      idrefUrl: 'https://www.idref.fr/035701854#'
    },
    'kahan': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '62NXYUGN',
      arrivalDate: 'février 2013',
      scopusUrl: 'https://www-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=55100055900',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref032503822',
      idrefUrl: 'https://www.idref.fr/032503822'
    },
    'cyna': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'WYR9Z3BE',
      arrivalDate: 'sept 2022',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57205657174',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref255092431',
      idrefUrl: 'https://www.idref.fr/255092431'
    },
    'guena': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'X9Z6QPA8',
      arrivalDate: 'sept 2018',
      scopusUrl: '',
      scanrUrl: '',
      idrefUrl: ''
    },
    'bazin': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'R32DNC7C',
      arrivalDate: 'oct 2016',
      scopusUrl: '',
      scanrUrl: '',
      idrefUrl: ''
    },
    'giardino': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '9YKHSE6X',
      arrivalDate: 'janv 2006',
      scopusUrl: '',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref068720416',
      idrefUrl: 'https://www.idref.fr/068720416'
    },
    'malandain': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'SIFQ3EZ3',
      arrivalDate: 'sept 2021',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=38261620200',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref094994005',
      idrefUrl: 'https://www.idref.fr/094994005'
    },
    'ferre': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '3RUZFJYF',
      arrivalDate: 'juin 2012',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=56184514100',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref135612438',
      idrefUrl: 'https://www.idref.fr/135612438'
    },
    'hache': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '65MLPE7C',
      arrivalDate: 'janv 2006',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=36453808800',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref113369573',
      idrefUrl: 'https://www.idref.fr/113369573'
    },
    'hagimont': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'K2L8FUSX',
      arrivalDate: 'sept 2019',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57170863800',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref224151614',
      idrefUrl: 'https://www.idref.fr/224151614'
    },
    'hautbois': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'FE8JU9X4',
      arrivalDate: 'janv 2009',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=36166925000',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref069045070',
      idrefUrl: 'https://www.idref.fr/069045070'
    },
    'henneton': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'QJR79XZR',
      arrivalDate: 'sept 2022',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=37114378600',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref078718902',
      idrefUrl: 'https://www.idref.fr/078718902'
    },
    'levy': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'H4MFSSV9',
      arrivalDate: 'sept 1994',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=56225587600',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref074694995',
      idrefUrl: 'https://www.idref.fr/074694995'
    },
    'mougin': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'JHXTUGWN',
      arrivalDate: 'sept 2020',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57908784900',
      scanrUrl: '',
      idrefUrl: ''
    },
    'pauly': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'HE22VCFF',
      arrivalDate: 'sept 1998',
      scopusUrl: '',
      scanrUrl: '',
      idrefUrl: ''
    },
    'pothier': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '9LGSUERH',
      arrivalDate: 'février 1996',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57031606600',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref085708801',
      idrefUrl: 'https://www.idref.fr/085708801'
    },
    'quenet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'XY9C23BL',
      arrivalDate: 'sept 2012',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=6508124393',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref059444487',
      idrefUrl: 'https://www.idref.fr/059444487'
    },
    'rodd': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '2R4B5KGH',
      arrivalDate: 'février 2013',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=57191869300',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref15230214X',
      idrefUrl: 'https://www.idref.fr/15230214X'
    },
    'sourdeval': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '93XGDS8T',
      arrivalDate: 'sept 2007',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=8592497700',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref118656716',
      idrefUrl: 'https://www.idref.fr/118656716'
    },
    'robinet': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'PEU8K333',
      arrivalDate: 'sept 2013',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=55831292700',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref176478663',
      idrefUrl: 'https://www.idref.fr/176478663'
    },
    'rialland': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '5G2VCIIS',
      arrivalDate: 'sept 2016',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=56047650900',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref127126228',
      idrefUrl: 'https://www.idref.fr/127126228'
    },
    'delporte': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: '5N265FGE',
      arrivalDate: 'janvier 2006',
      scopusUrl: 'https://www2-scopus-com.ezproxy.universite-paris-saclay.fr/authid/detail.uri?authorId=26656499500',
      scanrUrl: 'https://scanr.enseignementsup-recherche.gouv.fr/person/idref032103875',
      idrefUrl: 'https://www.idref.fr/032103875'
    },
    'doc': {
      userId: '5996232',
      apiKey: 'VRMvU5FwD33qp0MUPyxT9bUZ',
      collectionKey: 'LPJ29TYR',
    }
    // Ajoutez les chercheurs supplémentaires avec leurs informations
  };

  var allPublications = [];

 function showResearcherInfo(researcherKey) {
    var researcher = researchers[researcherKey];
    var researcherInfoContainer = document.querySelector('#researcherInfoContainer');
    researcherInfoContainer.innerHTML = '';

    var researcherInfo = document.createElement('div');
    researcherInfo.innerHTML = '<h3>' + researcherKey.charAt(0).toUpperCase() + researcherKey.slice(1) + '</h3>' +
      '<p>Date d\'arrivée dans l\'unité: ' + researcher.arrivalDate + '</p>' +
      '<p>SCOPUS: <a href="' + researcher.scopusUrl + '" target="_blank">' + researcher.scopusUrl + '</a></p>' +
      '<p>scanR: <a href="' + researcher.scanrUrl + '" target="_blank">' + researcher.scanrUrl + '</a></p>' +
      '<p>idRef: <a href="' + researcher.idrefUrl + '" target="_blank">' + researcher.idrefUrl + '</a></p>';

    researcherInfoContainer.appendChild(researcherInfo);

    var publicationTable = document.querySelector('#publicationTable');
    publicationTable.style.display = 'table';

    getResearcherPublications(researcherKey)
      .then(function(researcherPublications) {
        populatePublicationTable(researcherPublications);

        var wordcloudContainer = document.querySelector('#wordcloudContainer');
        wordcloudContainer.innerHTML = '';

        var publicationChartContainer = document.querySelector('#publicationChartContainer');
        publicationChartContainer.innerHTML = '';
      })
      .catch(function(error) {
        console.log('Une erreur est survenue:', error);
      });
  }

  function showAllPublications() {
    var allPublicationsTable = document.querySelector('#publicationTable');
    allPublicationsTable.style.display = 'table';

    var researcherInfoContainer = document.querySelector('#researcherInfoContainer');
    researcherInfoContainer.innerHTML = '';

    var wordcloudContainer = document.querySelector('#wordcloudContainer');
    wordcloudContainer.innerHTML = '';

    var publicationChartContainer = document.querySelector('#publicationChartContainer');
    publicationChartContainer.innerHTML = '';

    getPublicationsForAllResearchers()
      .then(function(publications) {
        allPublications = publications;
        populatePublicationTable(allPublications);

        var wordcloudTitle = document.createElement('h3');
        wordcloudTitle.textContent = 'Nuage de mots-clés';

        var wordcloudDiv = document.createElement('div');
        wordcloudDiv.id = 'wordcloud';

        wordcloudContainer.appendChild(wordcloudTitle);
        wordcloudContainer.appendChild(wordcloudDiv);

        generateWordCloud(allPublications);
        generatePublicationChart(allPublications);
      })
      .catch(function(error) {
        console.log('Une erreur est survenue:', error);
      });
  }

  function getResearcherPublications(researcherKey) {
  var researcher = researchers[researcherKey];
  var publications = [];
  var limit = 100; // Limite par requête
  var start = 0; // Point de départ pour la pagination

  function fetchBatch() {
    var apiUrl = `https://api.zotero.org/users/${researcher.userId}/collections/${researcher.collectionKey}/items?format=json&limit=${limit}&start=${start}&key=${researcher.apiKey}`;

    return fetch(apiUrl)
      .then(function(response) {
        // Extraction du nombre total de résultats à partir de l'en-tête 'Total-Results'
        var totalResults = parseInt(response.headers.get('Total-Results'), 10);
        start += limit;
        return response.json().then(data => ({ data, totalResults })); // Passer les données et totalResults
      })
      .then(function({ data, totalResults }) {
        publications = publications.concat(data);
        if (start < totalResults) {
          return fetchBatch(); // Récupérer le prochain lot de données
        } else {
          return publications; // Toutes les données ont été récupérées
        }
      });
  }

  return fetchBatch().catch(function(error) {
    console.log('Une erreur est survenue:', error);
    return publications;
  });
}




  function getPublicationsForAllResearchers() {
    var researcherPromises = Object.keys(researchers).map(function(researcherKey) {
      return getResearcherPublications(researcherKey);
    });

    return Promise.all(researcherPromises)
      .then(function(publicationsArray) {
        var allPublications = [];
        publicationsArray.forEach(function(publications) {
          allPublications = allPublications.concat(publications);
        });
        return allPublications;
      })
      .catch(function(error) {
        console.log('Une erreur est survenue:', error);
        return [];
      });
  }

  function populatePublicationTable(publications) {
    var tableBody = document.querySelector('#publicationTable tbody');
    tableBody.innerHTML = '';

    var filledRowCount = 0; // Initialisation du compteur de lignes remplies

publications.forEach(function(publication, index) {
  var title = publication.data.title ? publication.data.title : '';
  var authors = publication.data.creators ? publication.data.creators.map(function(creator) {
    return creator.firstName + ' ' + creator.lastName;
  }).join(', ') : '';
  var date = publication.data.date ? publication.data.date : '';

  // Ignore les lignes avec des données vides
  if (title !== '' && authors !== '' && date !== '') {
    filledRowCount++; // Incrémenter le compteur de lignes remplies
    var row = document.createElement('tr');
    var numberCell = document.createElement('td');
    var titleCell = document.createElement('td');
    var authorsCell = document.createElement('td');
    var dateCell = document.createElement('td');

    numberCell.textContent = filledRowCount; // Utiliser le compteur de lignes remplies pour le numéro de la ligne
    titleCell.textContent = title;
    authorsCell.textContent = authors;
    dateCell.textContent = date;

    row.appendChild(numberCell);
    row.appendChild(titleCell);
    row.appendChild(authorsCell);
    row.appendChild(dateCell);

    tableBody.appendChild(row);
  }
});

  }


   function generateWordCloud(publications) {
  var wordData = {};

  // Liste des mots à exclure étendue pour inclure également les mots très courts et courants qui n'apportent pas de valeur significative au nuage de mots
  var excludedWords = ['de', 'siècle', 'dune', 'dun', 'cr', 'et', 'du', 'der', 'au', 'le', 'les', 'la', 'un', 'une', 'in', 'en', 'the', 'and', 'dans', '?', 'of', 'des', 'à', 'est', 'ou', 'von', '(dir.)', 'compte-rendu', 'und', 'die', 'sur', 'pour', ':', 'a', '"', ',', '.', ';', '!', '-', '(', ')', '[', ']', '{', '}', '=', '+', '#', '*', '/', '|', '\\', '"', "'", '`', '“', '”', '‘', '’'];

  publications.forEach(function(publication) {
    var title = publication.data.title ? publication.data.title : '';
    // Suppression de tous les caractères spéciaux, y compris les guillemets et conversion en minuscules
    var words = title.replace(/[^a-zA-Z0-9éèêëàâäôöûüçîïÉÈÊËÀÂÄÔÖÛÜÇÎÏ\s]/g, "").toLowerCase().split(/\s+/);

    words.forEach(function(word) {
      if (!excludedWords.includes(word) && word.length > 1) { // Exclut également les mots d'un seul caractère
        wordData[word] = (wordData[word] || 0) + 1;
      }
    });
  });

  var wordcloudData = Object.keys(wordData).map(function(word) {
    return { name: word, weight: wordData[word] };
  }).sort(function(a, b) {
    return b.weight - a.weight;
  }).slice(0, 25); // Sélection des 25 mots les plus fréquents

  Highcharts.chart('wordcloud', {
    series: [{
      type: 'wordcloud',
      data: wordcloudData,
      name: 'Occurrences'
    }],
    title: { text: '' },
    credits: { enabled: false }
  });
}




  function generatePublicationChart(publications) {
    var publicationTypes = {};

    publications.forEach(function(publication) {
      var type = publication.data.itemType ? publication.data.itemType : 'Autre';

      if (publicationTypes[type]) {
        publicationTypes[type]++;
      } else {
        publicationTypes[type] = 1;
      }
    });

    var chartData = Object.keys(publicationTypes).map(function(type) {
      return {
        name: type,
        y: publicationTypes[type]
      };
    });

    Highcharts.chart('publicationChartContainer', {
      chart: {
        type: 'column'
      },
      title: {
        text: 'Les publications par type'
      },
      xAxis: {
        type: 'category'
      },
      yAxis: {
        title: {
          text: 'Nombre de publications'
        }
      },
      series: [{
        name: 'Nombre de publications',
        data: chartData
      }],
      credits: {
        enabled: false
      }
    });
  }
</script>
</body>
</html>

{{< /code >}}

## Pour aller plus loin

* <a href="https://www.highcharts.com/integrations/javascript/?gad_source=1&gclid=CjwKCAjw47i_BhBTEiwAaJfPpgZI3HXrWjQkeu36H-l7Fo3ABLB2kIeGBqPNmh7SiTi0kUpCvbF0LBoCOEIQAvD_BwE" target="_blank">Bibliothèque Highcharts</a>
* <a href="https://www.highcharts.com/demo/highcharts/wordcloud?_gl=1*sst7yi*_up*MQ..*_gs*MQ..&gclid=CjwKCAjw47i_BhBTEiwAaJfPpgZI3HXrWjQkeu36H-l7Fo3ABLB2kIeGBqPNmh7SiTi0kUpCvbF0LBoCOEIQAvD_BwE" target="_blank">Highcharts Word cloud</a>
* <a href="https://www.highcharts.com/docs/advanced-chart-features/boost-module?_gl=1*1ijtyjn*_up*MQ..*_gs*MQ..&gclid=CjwKCAjw47i_BhBTEiwAaJfPpgZI3HXrWjQkeu36H-l7Fo3ABLB2kIeGBqPNmh7SiTi0kUpCvbF0LBoCOEIQAvD_BwE" target="_blank">Highcharts Boost module</a>
* <a href="https://www.zotero.org/support/dev/web_api/v3/start" target="_blank">API Zotero</a>