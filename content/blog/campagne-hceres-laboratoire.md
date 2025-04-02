---
date: '2025-04-01T14:45:33+02:00'
draft: false
title: 'Moulinette HAL pour une campagne HCERES'
author: Maximilien Petit
tags: ["HAL","LLM","HCERES"]
readingTime: true
toc: false
---
{{< toc >}}

<div style="background-color: #fff7f1; border: 1px solid #d22000; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
  {{< details summary="Pour information" >}}
  Cette bidouille est une synthèse d'une communication réalisée le jeudi 13 juin 2024 avec Henri Bretel (chargé de bibliométrie, Université Paris-Saclay) lors de la septième édition des journées CasuHAL. Cette communication était un retour d'expérience de la campagne HCERES et avait pour but d'expliquer comment l'on pouvait utiliser un LLM dans une chaîne de travail pour importer en lot plus de 1000 notices sur HAL.
  {{< /details >}}
</div>

# Le problème

**Assurer la campagne de dépôts de notices et/ou publications d'un laboratoire SHS**. L'objectif étant de déposer 100% des notices des enseignants-chercheurs et de disposer d'une base Zotero structurée des publications pour, à l'avenir, automatiser certaines tâches : dépôt des notices sur HAL, mise à jour des fiches CV des EC sur le site du laboratoire.

**Les obstacles sont légion** : les fiches CV des EC ne sont pas uniformisées (en termes de format, de norme bibliographique), pas actualisées, le fonctionnement des *LLM* pour la conversion est encore balbutiant (au moment du chantier), la moulinette fait gagner du temps mais n'élimine pas le temps de correction des métadonnées, le dépôt par lot sur HAL repose sur un outil de l'INRIA (X2HAL) précieux mais pas nécessairement à jour et qui pourrait disparaître subitement, les tâchées liées à la campagne HCERES sont chronophages et personne n'a la possibilité d'y consacrer 100% en termes de temps de travail.

**Et quand bien même la moulinette serait *parfaite*, elle est, sur le papier, un aveu d'échec** : le principe de HAL étant le dépôt des publications par les chercheurs (et non par les bibliothécaires, les documentalistes, les moulinettes), utiliser un telle chaîne de travail ne peut que se faire en soupirant et en étant insatisfait professionnellement. Mais il y a *le principe de réalité* : il faut déposer le dossier, et nous n'avons jamais le temps.

## Qui peut aider ?

**C'est un travail pour les personnels de la filière bibliothèque et pour les personnels ITRF de la BAP F** (et notamment celles et ceux qui font, tant bien que mal, de la documentation en laboratoire). Et comme il s'agit d'un chantier HCERES, les personnels ITRF de la BAP J (Valorisation de la recherche) interviennent ça et là en fonction des habitudes de votre université. Les campagnes HCERES sont cruelles pour les personnels dans le sens où elles permettent souvent de mettre au jour le manque de moyens humains, et donc l'aspect perfectible des collaborations.

## La bidouille

La démarche résumée dans la carte heuristique ci-dessous :

<img src="/MP/images/mindmap1.svg" alt="Diagramme de la démarche" style="width:100%; height:auto;">

### 1 Extraction des publications de l'EC

Laboratoire SHS, donc, nous pouvons oublier l'outil SCOPUS et toute forme de moissonnage efficace. Il faut partir avec ce que nous avons sous la main : des fiches CV qui sont des pages HTML non actualisées, des fichiers Word non actualisés, des PDF non actualisés. Il faut partir de tout cela et importer dans des fichiers TXT les références uniquement depuis la date d'intégration de l'EC au laboratoire.

### 2 Formatage des notices en BibTeX via l'usage d'un LLM

**Il faut uniformiser les données bibliographiques** car, en SHS, les pratiques sont très multiples, ce qui est un obstacle pour notre chantier documentaire. Il y a plus de 1000 références à importer dans HAL, donc impossible à faire seul sur une courte période. Nous utilisons un LLM, avec regret, pour effectuer une tâche de conversion vers le format BibTeX. Avant les LLM, cela pouvait se faire difficilement avec, par exemple, <a href="https://rintze.zelle.me/ref-extractor/" target="_blank">Reference Extractor</a> ou <a href="https://anystyle.io/" target="_blank">AnyStyle</a>. Mais dorénavant cela peut se faire avec beaucoup plus d'efficacité avec un *prompt* travaillé et un LLM.

### 3 Import des notices dans un Zotero structuré et validation des métadonnées

**Le fichier BibTeX du LLM est importé dans une bibliothèque Zotero qui permet de contrôler "à la main" les métadonnées des notices**. Il faut également préparer les notices aux particularités de X2HAL. Par exemple, les x-audience, x-language, qui se retrouveront, dans Zotero, dans le champ "Extra". Il faut aussi bien prendre en compte les équivalences entre les gabarits des notices sur Zotero et les gabarits des notices sur HAL/X2HAL. C'est une étape complexe, **je recommande d'avancer par tâtonnement et de consigner les problèmes (et leurs solutions) dans une documentation**. Il faut aussi, si possible, avoir l'aide d'un ou une collègue qui fait de la documentation. Le chantier n'était par exemple pas possible, me concernant, sans un support (une collègue documentaliste, que je remercie grandement).

### 4 Usage de X2HAL et import par lot sur HAL

**On exporte avec Zotero le fichier BibTex retravaillé et on l'importe sur X2HAL**. Je recommande de travailler dans Zotero avec <a href="https://retorque.re/zotero-better-bibtex/" target="_blank">le plugin Better BibTeX</a>. Et ensuite, X2HAL vous permet de vérifier à nouveau les métadonnées, de gérer les affiliations, les champs obligatoires. Pour bien prendre en main l'outil, vous avez un <a href="https://cas-preprod.ccsd.cnrs.fr/cas/login?service=http%3A%2F%2Fqlf-x2hal.inria.fr%2F" target="_blank">bac à sable à disposition</a>. Quelques limites : parfois des problèmes techniques pour les imports (vérifiez bien vos métadonnées et caractères spéciaux), et ne tentez pas de dépasser 50 notices en une seule action.

### 5 Prise de contact avec l'EC

Jusqu'ici, vous travaillez "dans le dos" de l'EC. Avec l'accord de votre laboratoire bien entendu ! Mais il est important de bien prendre en compte le fait que **l'EC doit pouvoir contrôler aisément**, même s'il ne s'agit que des notices bibliographiques. Il y a plus de 60 personnes à contacter dans mon cas, donc on part d'un modèle de mail standard, mais que l'on adapte en fonction des connaissances que nous avons de ces personnes (profil, disciplines, aisance avec HAL/le numérique, etc.). L'EC doit prendre connaissance de ce qui est déposé sur HAL, vérifier les notices, valider ou demander des corrections ou des ajouts supplémentaires. Pour ce faire, on utilise l'option d'export des publications disponible sur HAL (qui...ne fonctionne pas toujours). X2HAL ne permet pas de partager aisément (sous forme de rapport ou de bibliographie) le résultat des imports par lot.

Cette prise de contact est également un moyen intéressant pour faire comprendre à l'EC qu'il y a derrière cela beaucoup de travail, des interlocuteurs (ne pas oublier d'associer les personnels de la filière bibliothèque). Cette prise de contact est également essentielle car, comme déjà évoqué plus haut, les fiches sont rarement à jour, donc il nous manque des références/publications. C'est donc suite à cette prise de contact que l'EC peut en profiter pour mettre à jour ce qui le concerne. C'est aussi par cette prise de contact que des questions seront remontées par l'EC. Des questions que nous connaissons bien car elles concernent les "verrous" habituels au dépôt sur HAL : est-ce que j'ai le droit de déposer ? est-ce que je peux ajouter un embargo ? est-ce que je suis obligé de déposer ? etc.

### 6 Import des données dans le tableau de bord

Je ne m'étends pas sur le sujet car **le tableau de bord sera l'objet d'une autre bidouille**. Mais, pour résumer, c'est une étape "bonus" supplémentaire, pas obligatoire donc, mais utile car elle permet de prendre connaissance de l'évolution du chantier documentaire et elle permet de faire remonter des données pertinentes. Ce tableau de bord codé basiquement (HTML, CSS, JavaScript) puise dans la bibliothèque Zotero au coeur de la moulinette.

## Remarques générales

* **L'usage des LLM est de plus en plus performant sur les conversions de formats**. C'est donc une tâche qui sera très certainement entièrement automatisée rapidement. Il est nécessaire de s'intéresser aux LLM *open-source* et à leurs usages en local (hors ligne) tant que certaines questions qui relèvent de l'éthique, de la souveraineté des données et de l'empreinte écologique des outils se posent.  **Toutefois, pour le moment, il est nécessaire de compléter l'usage des LLM par une correction "humaine" des métadonnées** car les erreurs sont non négligeables.
* **Le *prompt* est à travailler** pour limiter les "hallucinations" des LLM et pour bien prendre en compte les particularités des notices sur Zotero, X2HAL et HAL, mais également le formatage des caractères spéciaux et la capitalisation des titres des références. Les notices complexes sont à surveiller, en SHS il s'agira le plus souvent des actes de colloques et des communications dans des congrès.
* **X2HAL pourrait disparaître**. Et si cela arrive : il n'y aura plus un seul outil viable pour le dépôt par lot de notices sur HAL. Donc utilisez X2HAL, remerciez son développeur ( Kumar Guha - Archive-ouverte@inria.fr) et prévenez sa tutelle qu'il ne faut jamais, jamais (jamais) mettre hors ligne cet outil. Ou recrutez deux fois plus de bibliothécaires et documentalistes ! L'outil n'est pas parfait, il manque des gabarits, il y a des limites sur les imports et la reconnaissance des doublons et il faut sortir de l'outil pour exporter efficacement le résultat, mais il existe, et il fait gagner énormément de temps à toute une communauté. C'est précieux.
* Les moulinettes, les bidouilles et les moissonnages à la va-vite en période de campagne HCERES ne font pas progresser la science ouverte, à mon sens. Cette campagne incite fortement à un usage quantitatif (déposer le plus de notices bibliographiques) et non qualitatif (quid du texte intégral des notices ?). Le chantier est surdimensionné, les moyens humains et techniques sont faméliques. <a href="https://monevaluation.hceres.fr/hal" target="_blank">L'outil d'export des productions scientifiques du HCERES </a> était une aide, mais aussi, d'une certaine manière, un carcan. Et il s'agira un jour de trancher véritablement une question pourtant centrale : **déposer les notices sur HAL, finalement, c'est le travail de qui ?** Sur ce chantier documentaire, j'ai déposé avec ma collègue 1130 notices. Sur la même période, les EC du laboratoire n'ont eu le temps d'en déposer que 133. Comment font les laboratoires sans personnels ou avec un service commun de documentation ne pouvant pas appuyer ? Comment feront les unités de recherche SHS lorsqu'il s'agira de déposer à la fois les notices, les publications mais aussi les jeux de données ?

## Pour aller plus loin

* <a href="https://jan.ai/" target="_blank">Jan comme alternative open source à ChatGPT</a>
* <a href="https://doc.hal.science/x2hal/" target="_blank">La documentation de X2hal</a>
* <a href="https://casuhal2024.sciencesconf.org/data/Casuhal_atelier_X2hal_Inria_2024.pdf" target="_blank">Un support de Kumar Guha (INRIA) sur X2HAL</a>
