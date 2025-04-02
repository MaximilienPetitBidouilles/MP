---
date: '2025-03-25T22:35:15+01:00'
author: Maximilien Petit
draft: false
title: "Générer un PDF exploitable depuis un CV HTML/CSS avec Weasyprint"
tags: ["Hugo","Python"]
readingTime: true
---
{{< toc >}}

# Le problème

Les générateurs de sites statiques permettent de déployer rapidement des sites utiles pour les communautés universitaires. Notamment pour la gestion d'événements scientifiques, la valorisation de projets de médiation/vulgarisation. Ils sont en cela une alternative utile à <a href="https://www.sciencesconf.org/" target="_blank">Sciencesconf</a> ou toutes les usines à gaz sous WordPress.

Dans le cas présent, on souhaite partir d'un CV déployé dans un site statique sous Hugo et utilisant un *layout* adapté et des *shortcodes*.

On souhaite ensuite transformer ce CV HTML/CSS en un fichier PDF exploitable. C'est-à-dire, un PDF que l'on peut partager facilement, imprimer facilement et qui respecte les normes de mise en page.

## Qui peut aider ? 

Les personnels BIATSS BAP E (informatique), les personnels BIATSS de laboratoire (espèces menacées d'extinction) BAP D (SHS) ou F (documentation, édition en particulier) et les bidouilleurs et bidouilleuses aux profils hybrides que l'on retrouve dans les humanités numériques.

## La bidouille

On utilise un environnement virtuel (Jupyter Notebook, Google Colab) et Python pour installer Weasyprint. Et c'est cette librairie, précisément, qui permet de transformer un fichier HTML en un PDF très propre. Le code à la suite, avec une simple modification, en l'occurrence une commande pour insérer le numéro de page dans le fichier.

```code
!python3 -m venv venv
!source venv/bin/activate
!pip install weasyprint
!weasyprint --info

# Use get_ipython().system to run 'weasyprint --info' command within the virtual environment
get_ipython().system('source venv/bin/activate && weasyprint --info') 
# This ensures the command is run in the correct environment.
```

```code
%%writefile style.css
@page {
    @bottom-right {
        content: counter(page); 
    }
}
```

```code
!weasyprint -s style.css https://maximilienpetitbidouilles.github.io/MP/cv/ /tmp/test.pdf
```
## Pour aller plus loin

* <a href="https://dev.to/bowmanjd/python-pdf-generation-from-html-with-weasyprint-538h " target="_blank">Python PDF Generation from HTML with WeasyPrint  </a>
* <a href="https://templated.io/blog/how-to-convert-html-to-pdf-with-python/" target="_blank">How To Convert HTML to PDF with Python (Best for 2024)  </a>
* <a href="https://doc.courtbouillon.org/weasyprint/stable/" target="_blank">La documentation de Weasyprint  </a>
