---
date: '2025-04-06T12:36:59+02:00'
draft: false
title: 'Appuyer la médiation scientifique grâce aux sites statiques'
author: Maximilien Petit
tags: ["Hugo","Médiation scientifique"]
readingTime: true
---
{{< toc >}}

# Le problème

Des chercheurs souhaitent **valoriser des vidéos pédagogiques et de médiation scientifique** sur une thématique : *L'illustration en questions*, qui concerne la presse, les revues et le livre du XIXe au XXIe siècle et leur remédiation par la numérisation. Les vidéos sont visibles sur Youtube mais il est nécessaire de mettre en ligne un site permettant de présenter le projet (Histoires Vivantes) et lui donner une visibilité (pour les publics et d'éventuels financeurs à l'avenir). **Ce site doit être rapide à concevoir, facile à maintenir sur le temps long (les MAJ de contenus seront rares), rapide et sécurisé**.

## Qui peut aider ?

Déployer et mettre en ligne un site web pour un projet (recherche, médiation, vulgarisation) nécessitent, au besoin, d'avoir le support des **personnels BIATSS de la BAP E (informatique) et F (Médiation scientifique, culture et communication)**. D'autant plus si l'on souhaite déployer et mettre en ligne un site en dehors des outils internes de l'université (le plus souvent, un CMS de type K-SUP). Il faut pouvoir, au minimum, avoir les accords et respecter les procédures (chartes graphiques).

## La bidouille

**<a href="https://histoires-vivantes.netlify.app/" target="_blank">Le site en question</a>**

Les générateurs de sites statiques conviennent parfaitement à la demande car il ne s'agit, en l'état, que de **déployer des pages avec des contenus fixes** (ou l'usage d'*iframes* pour les contenus extérieurs : les vidéos).

Le site statique est une solution intéressante pour les projets SHS qui, le plus souvent, alimentent les sites et plateformes de médiation en fonction de **la réalité des financements**. Donc, de fait, il peut parfois y avoir plusieurs mois, années, avant l'ajout d'éventuels contenus. Il faut un site simple à maintenir sur le temps long et qui ne présente pas de failles de sécurité qui pourraient mettre fin à sa mise en ligne.

On s'oriente vers **Hugo** et, en particulier, les thèmes **Hugo Blox** (anciennement *Wowchemy Hugo Modules*) car ils sont pensés, à l'origine, pour un usage académique (déployer des sites pour des conférences, des portfolios pour les chercheurs).

Les thèmes Hugo Blox présentent également l'avantage d'être compatibles avec **Netlify pour la mise en ligne**, et **Netlify CMS (dorénavant Decap CMS) pour la gestion des contenus**. Ces deux possibilités améliorent encore la facilité pour prendre en main cette solution. L'usage de générateurs de sites statiques n'est pas complexe mais le fait de maintenir des fichiers sans CMS peut parfois rebuter des utilisateurs débutants. 

Le site du projet en question dispose certes d'une personne pour administrer (moi même !) mais il est important de **penser à des solutions simples et pérennes** si jamais les personnels en charge des plateformes changent de trajectoire professionnelle (il y a un véritable *cimetière* des sites et bases en SHS, et c'est malheureux). Il faut donc pouvoir se préoccuper de la pérennité des solutions que nous mettons en oeuvre, et pas seulement de la faisabilité ou de la communication à un instant "T".

**Une bidouille plus longue sera consacrée à la formation des publics pour prendre en main les générateurs de sites statiques.**

## Pour aller plus loin

* <a href="https://gohugo.io/documentation/" target="_blank">La documentation d'Hugo</a>
* <a href="https://hugoblox.com/templates/" target="_blank">Les templates d'Hugo Blox </a> et <a href="https://docs.hugoblox.com/" target="_blank">la documentation</a>
* <a href="https://www.netlify.com/" target="_blank">Netlify</a> 
