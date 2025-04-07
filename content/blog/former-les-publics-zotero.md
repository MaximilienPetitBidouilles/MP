---
date: '2025-04-07T13:39:57+02:00'
draft: false
title: 'Former les publics : Zotero'
author: Maximilien Petit
tags: ["Pédagogie","Zotero"]
readingTime: true
---
{{< toc >}}

# Le problème

Il n'est pas rare, en laboratoire SHS, d'être amené à devoir former des publics sur des outils. Le plus souvent, il s'agit d'étudiants de L3, M1, M2, et des doctorants. Le logiciel Zotero est par exemple incontournable pour aborder la gestion des références bibliographiques. Parfois, il est abordé dans des UE de méthodologie, ou alors, dans des formations dispensées par des personnels de l'Information Scientifique et Technique (I.S.T.) en bibliothèque. C'est un outil très complet et simple à prendre en main et les contenus pédagogiques en ligne ne manquent pas.

Toutefois, ces supports et formations sont très souvent de type "clique-bouton" et ce n'est pas nécessairement une approche qui fonctionne avec tout le monde. De plus, on se contente de l'usage premier de Zotero (gestion des notes de bas de page, des bibliographie) et on oublie d'aborder le fait que c'est un véritable outil "couteau-suisse" qui est interopérable avec, entre autres, Tropy et Omeka S.

Nous souhaitons donc déployer, en ligne, des contenus pédagogiques adaptés, malléables et pertinents pour la prise en main de Zotero. Ce contenu doit pouvoir être utilisable dans plusieurs situations pédagogiques : formation en laboratoire, formation doctorale, UE de méthodo, apprentissage auto-didacte.

# Qui peut aider ? 

Les personnels de la filière bibliothèque, les EC qui abordent l'outil dans des UE de méthodo, les personnels de la BAP F (documentation).

## La bidouille

Le résultat est visible ici : <a href="https://pasletempspourladoc.netlify.app/zotero/presentation/" target="_blank">tutoriel "Pas le temps pour Zotero"</a>

On s'oriente encore vers l'usage des générateurs de sites statiques, et en particulier Hugo, car, comme d'habitude, il s'agit de concevoir une interface rapide et sécurisée avec une mise en place flexible et sans coûts. Comme souvent, on regarde encore du côté des thèmes d'Hugo Blox (anciennement *Wowchemy Hugo Modules*) et le déploiement en ligne se fait par le biais de Netlify. Le thème en question est adapté en particulier pour conserver l'ergonomie d'une documentation qui se prête facilement aux tutoriels et cours. Cette ergonomie supporte la présence d'une arborescence visible dans une colonne à gauche et une navigation linéaire. L'utilisateur doit progresser étape par étape dans les contenus pédagogiques, page par page. Cet ensemble de pages fixes doit pouvoir se mettre à jour facilement (via Netlify CMS ou directement sur le dépôt Github).

L'approche pédagogique : il faut pouvoir présenter la quasi intégralité des fonctionnalités du logiciel Zotero. La progression doit être linéaire et se baser sur un "livrable". Aborder Zotero, c'est toujours questionner les méthodologies de recherche documentaire, la gestion des notices bibliographiques, l'intéropérablité des métadonnées. Il faut pouvoir donner "du sens" à tout cela, notamment car, le plus souvent, les étudiants (L3, M1) abordent le logiciel avec une approche superficielle en début d'année, laissent tomber après quelques semaines, puis "se réveillent" en fin d'année universitaire (rendu d'un dossier, d'un mémoire). Il faut donc apprendre à utiliser Zotero, certes, mais montrer très concrètement aux utilisateurs ce que l'on peut faire avec *en situation*. On s'inspirera utilement des contenus de Pascal Martinolli, bibliothécaire à l'Université de Montréal, et excellent pédagogque sur toutes ces questions.

Si le tutoriel est utilisé en cours, la progression des contenus se fait en groupe. Chaque groupe doit choisir un sujet de recherche documentaire, progresser dans le tutoriel, tenir un "carnet de recherche", produire une bibliothèque partagée de références bibliographiques et générer avec le logiciel une bibliographie. Dans chaque groupe, on encourage (sans obliger) la distribution de rôles afin d'achever les tâches et les 36 étapes du tutoriel. L'enseignant, ou le formateur, accompagne les groupes. De courtes présentations générales sont réalisées pour des "focus" sur des points annexes (usage de l'API de Zotero, interopérabilité avec Omeka S, etc.). 

Le plus souvent, chaque page du tutoriel contient des explications, une vidéo de manipulations, des exercices.

## Pour aller plus loin

* <a href="https://tropy.org/" target="_blank">Tropy</a>
* <a href="https://omeka.org/s/" target="_blank">Omeka S</a>
* <a href="https://omeka.org/s/" target="_blank">Site personnel de Pascal Martinolli</a>








