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
