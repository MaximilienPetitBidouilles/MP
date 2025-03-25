---
date: '2025-03-25T22:35:15+01:00'
author: Maximilien Petit
draft: false
title: "Générer un PDF exploitable depuis un CV HTML/CSS avec Weasyprint"
tags: ["Hugo","Python"]
---

## Le problème

Les générateurs de sites statiques permettent de déployer rapidement des sites utiles pour les communautés universitaires. Notamment pour la gestion d'événements scientifiques, la valorisation de projets de médiation/vulgarisation. Ils sont en cela une alternative utile à <a href="https://www.sciencesconf.org/" target="_blank">Sciencesconf</a> ou toutes les usines à gaz sous WordPress.

Dans le cas présent, on souhaite partir d'un CV déployé dans un site statique sous Hugo et utilisant un *layout* adapté et des *shortcodes*.

On souhaite ensuite transformer ce CV HTML/CSS en un fichier PDF exploitable. C'est-à-dire, un PDF que l'on peut partager facilement, imprimer facilement et qui respecte les normes de mise en page.

## La bidouille

On utilise un environnement virtuel (Jupyter Notebook, Google Colab) et Python pour installer Weasyprint. Et c'est cette librairie, précisément, qui permet de transformer un fichier HTML en un PDF très propre. Le code à la suite, avec une simple modification, en l'occurrence une commande pour insérer le numéro de page dans le fichier.