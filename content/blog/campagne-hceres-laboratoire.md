---
date: '2025-04-01T14:45:33+02:00'
draft: false
title: 'Moulinette HAL pour une campagne HCERES'
author: Maximilien Petit
tags: ["HAL","LLM"]
---

## Le problème

Assurer la campagne de dépôts de notices et/ou publications d'un laboratoire SHS. L'objectif étant de déposer 100% des notices des enseignants-chercheurs et de disposer d'une base Zotero structurée des publications pour, à l'avenir, automatiser certaines tâches : dépôt des notices sur HAL, mise à jour des fiches CV des EC sur le site du laboratoire.

**Les obstacles sont légions** : les fiches CV des EC ne sont pas uniformisées (en termes de format, de norme bibliographique), pas actualisées, le fonctionnement des *LLM* pour la conversion est encore balbutiante, la moulinette fait gagner du temps mais n'élimine pas le temps de correction des métadonnées, le dépôt par lot sur HAL repose sur un outil de l'INRIA (X2HAL) précieux mais pas nécessairement à jour et qui pourrait disparaître du jour au lendemain, les tâchées liées à la campagne HCERES sont chronophages et personne n'a la possibilité d'y consacrer 100% en termes de temps de travail.

Et quand bien même la moulinette serait *parfaite*, elle est, sur le papier, l'aveu d'un échec : le principe de HAL étant le dépôt des publications par les chercheurs (et non par les bilbiothécaires, les documentalistes, les moulinettes), utiliser un telle chaîne de travail ne peut que se faire en soupirant et en étant insatisfait professionnellement. Mais il y a le principe de réalité : il faut déposer le dossier, et nous n'avons jamais le temps.

## Qui peut aider ?

C'est un travail pour les personnels de la filière bibliothèque et pour les personnels ITRF de la BAP F (et notamment celles et ceux qui font, tant bien que mal, de la documentation). Et comme il s'agit d'un chantier HCERES, les personnels ITRF de la BAP J (Valorisation de la recherche) interviennent ça et là en fonction des habitudes de votre université. Les campagnes HCERES sont cruelles pour les personnels dans le sens où elles permettent souvent de mettre au jour le manque de moyens humains, et l'aspect perfectible (ou performant !) des collaborations.

## La bidouille

La démarche résumée dans le Markmap ci-dessous : 

<img src="/MP/images/mindmap1.svg" alt="Diagramme de la démarche" style="width:100%; height:auto;">


**1 Extraction des publications de l'EC**

Laboratoire SHS, donc, nous pouvons oublier l'outil SCOPUS et toute forme de moissonnage efficace. Il faut partir avec ce que nous avons sous la main : des fiches CV qui sont des pages HTML non actualisées, des fichiers Word non actualisés, des PDF non actualisés. Il faut partir de tout cela, importer les références uniquement depuis la date d'intégration de l'EC au laboratoire.

**2 Formatage des notices en BibTeX via l'usage d'un LLM**

Il faut uniformiser les données bibliographiques car, en SHS, les pratiques sont très multiples, ce qui est un obstacle pour notre chanteir documentaire. Il y a plus de 1000 références, donc impossible dans le temps donné de tout faire ça à la main. Donc nous utilisons un LLM, avec regret, pour effectuer une tâche de conversion vers le format BibTeX. Avant les LLM, cela pouvait se faire difficilement avec, par exemple, Reference Extractor (https://rintze.zelle.me/ref-extractor/) ou AnyStyle https://anystyle.io/). Mais dorénavant cela peut se faire avec beaucoup plus d'efficacité avec un prompt travaillé et un LLM. 

**3 Import des notices dans un Zotero structuré et validation des métadonnées**

Le fichier BibTeX du LLM est importé dans une bibliothèque Zotero qui permet de contrôler "à la main" les métadonnées des notices. Il faut également préparer les notices aux particularités de X2HAL. Par exemple, les x-audience, x-language, qui se retrouveront, dans Zotero, dans le champ "Extra". Il faut aussi bien prendre en compte les équivalences entre les gabarits des notices sur Zotero et les gabarits des notices sur HAL/X2HAL. C'est une étape complexe, je recommande d'avancer par tâtonnement et de consigner les problèmes (et leurs solutions) dans une documentation.

**4 Usage de X2HAL et import par lot sur HAL**

On exporte avec Zotero le fichier BibTex retravaillé et on l'importe sur X2HAL. Je recommande de travailler dans Zotero avec le plugin Better BibTeX (https://retorque.re/zotero-better-bibtex/). Et ensuite, X2HAL vous permet de vérifier à nouveau les métadonnées, de gérer les affiliations, les champs obligatoires. Pour bien prendre en main l'outil, vous avez un bac à sable à disposition (https://cas-preprod.ccsd.cnrs.fr/cas/login?service=http%3A%2F%2Fqlf-x2hal.inria.fr%2F). Quelques limites : parfois des problèmes techniques pour les imports (vérifiez bien vos métadonnées et caractères spéciaux), et ne tentez pas de dépasser 50 notices en une seule action.

**5 Prise de contact avec l'EC**

Jusqu'ici, vous travaillez "dans le dos" de l'EC. Avec l'accord de votre laboratoire bien entendu ! Mais il est important de bien prendre en compte le fait que l'EC doit pouvoir contrôler aisément, même s'il ne s'agit que des notices bibliographiques. 
