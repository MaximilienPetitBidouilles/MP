---
date: '2025-04-08T10:25:03+02:00'
draft: false
title: 'Collection HAL et template HTML-CSS'
author: Maximilien Petit
tags: ["HAL"]
readingTime: true
---
{{< toc >}}

# Le problème

On souhaite **modifier le *template* (modèle) HTML et CSS de la collection HAL d'une unité de recherche SHS**. HAL met à disposition des outils qui évoluent et qui s'améliorent mais il n'est pas toujours simple de prendre en main les fonctionnalités de gestion/administration des collections. Il y a un système de "widget" et un éditeur *WYSIWYG* (What You See Is What You Get pour "ce que vous voyez est ce que vous obtenez") mais, de fait, ce n'est pas évident d'avoir quelque chose qui nous convient précisément.

## Qui peut aider ?

**La gestion/administration de HAL, à l'échelle d'une université, dépend des personnels de la filière bibliothèque**. Et, en fonction des procédures de l'université, la gestion des collections est déléguée en laboratoire à un personnel de l'unité (si le personnel existe...). Parfois l'université impose un *template* commun aux unités, parfois non.

## La bidouille

**Le résultat est visible ici : <a href="https://hal.science/CHCSC" target="_blank">Collection HAL</a>**

**On s'inspire comme souvent de l'Inria** qui met à disposition des feuilles de style qu'il convient de modifier en fonction de vos attentes. De plus la démarche est documentée dans un tutoriel que j'ajoute en fin d'article.

On rappelle, si vous avez les droits de gestion de la collection, qu'il faut modifier les contenus en étant connecté directement sur la page d'accueil de votre collection en cliquant sur le bouton orange en bas intitulé "Modifier le contenu de la page". 

<img src="/MP/images/hal_1.PNG" alt="HAL HTML CSS 1" style="width:100%; height:auto;">

Ensuite, dans l'éditeur, il faut passer par le bouton "code source" pour modifier les informations. Copiez et collez les informations de votre *template* dans l'éditeur puis sauvegardez. 

<img src="/MP/images/hal_2.PNG" alt="HAL HTML CSS 2" style="width:100%; height:auto;">

Dans le cas présent, pour ma collection, voici ce que cela donne : 

{{< code language="html" title="Template page d'accueil collection HAL" open="false" >}}

<div class="row">
<div class="Gauche col-md-8">
<h1 class="titre-h1">La collection HAL du CHCSC</h1>
<p></p>
<p style="text-align: center;"><iframe src="https://www.youtube.com/embed/KvNFOVob9Kc" width="560" height="315"></iframe></p>
<p></p>
<p class="paragraphes">Le Centre d&rsquo;histoire culturelle des soci&eacute;t&eacute;s contemporaines (CHCSC) a &eacute;t&eacute; cr&eacute;&eacute; comme jeune &eacute;quipe en 1992 et a obtenu en 1994 le statut &eacute;quipe d&rsquo;accueil (EA 2448).<br /><br />Seul laboratoire d&rsquo;histoire en France ayant pour mission exclusive la recherche en histoire culturelle du contemporain (de la fin du XVIIIe si&egrave;cle &agrave; nos jours), il entend la culture comme &laquo; l&rsquo;ensemble des repr&eacute;sentations collectives propres &agrave; une soci&eacute;t&eacute; &raquo; et l&rsquo;histoire culturelle comme &laquo; l&rsquo;histoire sociale des repr&eacute;sentations &raquo;.<br /><br />Pluridisciplinaire, il f&eacute;d&egrave;re tous ses membres autour du concept d&rsquo;histoire culturelle et entend continuer &agrave; jouer un r&ocirc;le majeur dans l&rsquo;&eacute;tude et la mise en pratique de ce concept, tant &agrave; l&rsquo;&eacute;chelle de l&rsquo;Universit&eacute; Paris-Saclay que sur un plan national et international.</p>
<p class="paragraphes"></p>
<p class="paragraphes"><strong>R&eacute;f&eacute;rent publications</strong> : Maximilien Petit (<a href="mailto:maximilien.petit@uvsq.fr">maximilien.petit@uvsq.fr</a> - 01 39 25 56 32)</p>
<p class="paragraphes"></p>
<widget>{"type":"last","title":"Derni\u00e8res publications","limit":"7"}</widget></div>
<div class="Droite col-md-4">
<p>&nbsp;</p>
<widget>{"type":"cloud","title":"Mots cl\u00e9s","limit":"4"}</widget></div>
</div>


{{< /code >}}

Vous devez ensuite **adapter la feuille de style CSS** de l'Inria et l'ajouter pour votre collection. Ceci vous permet de paramétrer des éléments de mise en forme (les couleurs de chaque menu, par exemple). 

Toujours en étant connecté, et avec les droits, cliquez sur "Administrer dans HAL" puis sur "Site Web" et enfin sur "Apparence".

<img src="/MP/images/hal_3.PNG" alt="HAL HTML CSS 3" style="width:100%; height:auto;">

Il faut choisir le type de personnalisation "Avancé" puis copier et coller dans l'éditeur les informations de votre CSS. le code à la suite pour ma collection, toujours basé sur l'excellent travail de l'Inria : 

{{< code language="CSS" title="CSS Collection HAL" open="false" >}}

@CHARSET "UTF-8";

/*==========================================================================================*/
/*===================================== ROOT [VARIABLE]  ==================================*/
/*=========================================================================================*/

:root {

/* Variable qui agit sur les couleurs le background des widgets ---------------------------------------------------------------------------------------------------------------------------*/
    --widget: #6f6f6e; 

/* Variable qui agit sur les couleurs des bordures des widgets ---------------------------------------------------------------------------------------------------------------------------*/
    --boxwidget: #f8f9fa;

/* Variable qui agit sur les couleurs du texte URL "lien" ---------------------------------------------------------------------------------------------------------------------------*/
    --texte-url: #7C1272; 

/* Variable qui agit sur les couleurs du texte ---------------------------------------------------------------------------------------------------------------------------*/
    --texte: #444a52; 

 /* Variable qui agit sur les couleurs des labels des widgets tels que le nombre de text intÃ©gral ---------------------------------------------------------------------------------------------------------------------------*/
    --label:#88cac9;

/* Variable qui agit sur les couleurs des menu et des menu dÃ©roulants ---------------------------------------------------------------------------------------------------------------------------*/
    --menu:#6f6f6e;

/* Variable qui agit sur les couleurs des boutons et les mots clÃ©s du widget mots clÃ©s ---------------------------------------------------------------------------------------------------------------------------*/
    --bouton:#6c6980; 

/* Variable qui agit sur les couleurs des boutons et les mots clÃ©s du widget mots clÃ©s ---------------------------------------------------------------------------------------------------------------------------*/
    --motcles:#6d2065; 

/* Variable qui agit sur les couleurs des boutons du menu ---------------------------------------------------------------------------------------------------------------------------*/
    --bouton-menu:#7C1272; 

/* Variable qui agit sur les couleurs au passage du curseurs sur les Ã©lÃ©ments tels que les boutons et les mots clÃ©s  ---------------------------------------------------------------------------------------------------------------------------*/
    --hover: ##7C1272; 

/* Variable qui agit sur les couleurs au passage du curseurs sur le menu ----------------------------------------------------------------------------------------------------------------*/
    --hover-menu: #7C1272; 

/* Variable qui agit sur les couleurs des boutons et les mots clÃ©s du widget mots clÃ©s ---------------------------------------------------------------------------------------------------------------------------*/
    --hover-motcles:#cd0b23; 

/* Variable qui permet une animation de transition au passage du curseur ---------------------------------------------------------------------------------------------------------------------------*/
    --transition: .3s cubic-bezier(.25,.8,.5,1); 

}

/*=======================================================================================*/
/*============================ CONTENUS MODIFIABLE (Mode Rapide) =========================*/
/*======================================================================================*/

/* ================================== PAGE ================================== */

/* Couleur du fond de la page ------------------------------------------------------------------------------------ */
main {
background-color: #FFFFFF;
}

/* ============================== FONT (POLICE) ============================== */

/* Couleur des liens ( URL-HTML) ------------------------------------------------------------------------------------ */
a { 
    color: var(--texte-url);
}

/* ============================== Titre & Paragraphes ============================== */

/* Style du Titre h1 ------------------------------------------------------------------------------------ */
.titre-h1 { 
    padding-left: 0px;
    border-bottom: 1px solid var(--texte);
    color: var(--texte);
    padding-top: 15px;
    text-align: center;
}

/* Style du paragraphe de prÃ©sentation ------------------------------------------------------------------------------------ */
.paragraphes { 
    font-size: 16px;
    line-height: 30px;
    color: var(--texte);
    padding: 10px 10px 10px 10px;
}
/* Taille des listes Ã  puce Li ------------------------------------------------------------------------------------ */
li {
    font-size: 16px;
}

/* =============================== BanniÃ¨re ===============================*/

/* Style de la banniÃ¨re [En-tÃªte] ------------------------------------------------------------------------------------ */
.logo {
    background-color: #ffffff;
    margin-top: 15px;
}


/* ========================== Widgets -> Commun Ã  tous ==========================*/

/* Marge interne et couleur de l'entÃªte des widgets ------------------------------------------------------------------------------------ */
.section-corps .widget .widget-header { 
    background-color: var(--widget);
    padding-top: 15px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}

/* Marge interne et couleur des bordures des widgets ------------------------------------------------------------------------------------ */
 .section-corps .widget {
    margin-bottom: 25px;
    box-shadow: 0 3px 4px #00000029;
    border-radius: 7px;
    background-color: var(--boxwidget);
}

/* ========================== Label (chiffres qui s'affichent dans le widget) ==========================*/

/* Bloc avec chiffres dans les des widgets ------------------------------------------------------------------------------------ */
.label.label-contrast {
    background-color: var(--label);
    color: #395554;
    padding: 11px 20px 8px;
    border-radius: 4px;
    font-size: 16px;
    border: 2px solid #588483;
}

/* ========================== Widget -> derniÃ¨re publication ========================== */

/* Style des Ã©lÃ©ments dans le widget derniÃ¨re publication ------------------------------------------------------------------------------------ */
.list-deposit .media { 
    margin-top: 0px;
    transition: var(--transition);
    border-left: 2px solid transparent;
    border-bottom: 0px solid #cacaca;
    padding: 10px;
}

/* Style du widget derniÃ¨re publication hover -> (au passage de la souris) ------------------------------------------------------------------------------------ */
.list-deposit .media:hover {  
    border-color: var(--widget);
    background-color: #cdd0d3;
    transform: translatey(-5px);
}

/* Marge interne des Ã©lÃ©ments du widget derniÃ¨re publication ------------------------------------------------------------------------------------ */
.list-deposit { 
    padding: 10px 10px;
}

/* Marge externe du texte du widget derniÃ¨re publication ------------------------------------------------------------------------------------ */
.media-body { 
    margin-left: 10px;
}


/* --------------------------------------------- Widget avec Graphique --------------------------------------------- */

rect { /* Pas de fond blanc sur les graphiques pour des raisons de responsive */
    fill: transparent;
}

/* ================================ Mots-clÃ©s (Widget) ================================ */

/* Marge interne du widget Mots clÃ©s ------------------------------------------------------------------------------ */
.widget-cloud { 
    padding: 20px;
}

/* Style des mots clÃ©s du widget Mots clÃ©s ------------------------------------------------------------------------------ */
.widget-cloud .keyword {
    background-color: var(--motcles);
    color: #fff;
    padding: 0px 12px 0px 12px;
    font-size: 16px;
    border-radius: 0px 7px 0px 7px;
    display: inline-block;
    margin-top: 5px;
    transition: var(--transition);
}

/* Fond du mots clÃ©s widget Mots clÃ©s Hover (au passage du curseur) -------------------------------------- */
.widget-cloud .keyword:hover { 
    background-color: var(--hover-motcles);
}


/*=================================================================================*/
/*========================= CONTENUS MODIFIABLE (Mode avancÃ©) =====================*/
/*================================================================================*/

/* ============================ Bouton ============================ */

/* Bouton +DÃ©poser aux couleurs de l'Inria --------------------------------------------- */
.btn-primary-orange { 
    background: var(--bouton);
    border: 1px solid var(--bouton);
}

/* Bouton +DÃ©poser aux couleurs de l'Inria --------------------------------------------- */
.btn-primary-orange:hover { 
    background-color: var(--hover);
}

/* ============================ Zone & Barre de Recherche ============================ */

/* Correction d'un dÃ©calage de la barre de recherche Ã  droite --------------------------------------------- */
#searchHeaderList { 
    margin: auto !important;
}

/* Correction d'un bug permettant un dÃ©filement vertical non nÃ©cessaire --------------------------------------------- */
#ssheader-submit {  
    margin-left: 0;
    margin-right: 0;
}

/* Correction d'un bug de positionnement de la loupe dans la barre de recherche et mise en couleur (harmonisation) --------------------------------------------- */
.hal-main-search-button { 
    padding: 0 10px;
    color: var(--widget);
}

/* Mise en couleur de la ligne au clic dans la zone de recherche (harmonisation) (harmonisation) --------------------------------------------- */
.hal-main-search-input { 
    background-image: linear-gradient(0deg,var(--widget) 50%,#0000 0);
    color: var(--texte);
}

/* Plus grande taille du menu dÃ©roulant dans la zone de recherche avancÃ©e --------------------------------------------- */
.dropdown-menu.show { 
    max-height: 485px !important;
}

/* Correction de la hauteur des zones de recherches avancÃ©es ------------------------------------------------------------------------------------------------------------------------------------------------------ */
div.form-group.row input.input-flex, .input-group > .custom-file, .input-group > .custom-select, .input-group > .form-control, .input-group > .form-control-plaintext { 
    height: 35px;
}

/* Correction de la taille des boutons dans recherche avancÃ©e  ----------------------------------------------------------------------------------------------------------------------------------------- */
.input-group span.input-group-btn { 
width: 87px;
}

/* Correction de la marge des boutons dans recherche avancÃ©e ----------------------------------------------------------------------------------------------------------------------------------------- */
div.form-group.row .btn-group-sm > .btn-primary.btn, div.form-group.row .btn-primary.btn-sm {
margin-left: 0px;
}

/* Correction d'un bug sur le Hover (au passage de la souris) des boutons dans recherche avancÃ©e ---------------------------------------------------------------------------------------------------- */
.input-group span.input-group-btn button:hover { 
    background-color: transparent; 
}

 /* Harmonisation des couleurs sur le active des boutons dans recherche avancÃ©e --------------------------------------------------------------------------------------------------------------------- */
.btn-primary:not(:disabled):not(.disabled).active, .btn-primary:not(:disabled):not(.disabled):active, .show > .btn-primary.dropdown-toggle {
background-color: var(--hover);
border-color: var(--hover);
}

/* Uniformisation des couleurs et animations des boutons dans recherche avancÃ©e   ------------------------------------------------------------------------------------------------------------------------- */
div.form-group.row span.input-group-btn { 
    background-color: var(--bouton);
    transition: var(--transition);
    text-align: center;
}

/* Couleur du Bouton Ajouter dans zone de recherche hover (au passage de la souris) ---------------------------------------------------------------------------------------------------------- */
div.form-group.row span.input-group-btn:hover { 
    background-color: var(--hover);
}

/* Couleur du Bouton Lancer la recherche dans zone de recherche avancÃ©e ---------------------------------------------------------------------------------------------------------- */
.hal-visualize-button { 
    background-color: var(--bouton);
}

/* Couleur du Bouton Lancer la recherche dans zone de recherche hover (au passage de la souris) ---------------------------------------------------------------------------------------------------------- */
.hal-visualize-button:hover {
    background-color: var(--hover);
}
/* Texte Noir en Hover (au passage de la souris) sur les menus dÃ©roulant ---------------------------------------------------------------------------------------------------------- */
ul.dropdown-menu li:not(.not-white):hover a {
color: #000 !important;
}

/* ======================================================================================= */
/* ====================================== MENU ========================================== */
/* ===================================================================================== */

/* ============================ Zone du menu ============================ */

/* Style de la zone du menu principal ----------------------------------------------------------------------- */
.website-navigation { 
    background: var(--menu);
    min-height: 50px;
    padding-bottom: 0px;
    padding-top: 0px;
}

/* Taille des Ã©lÃ©ments du menu principal ----------------------------------------------------------------------- */
.nav-pills .nav-link { 
    border-radius: 0px;
    padding: 5px 15px 5px 15px !important;
}

/* Couleur des boutons du menu principal ----------------------------------------------------------------------- */
.nav-pills .nav-link.active, .nav-pills .show > .nav-link{
    background-color: var(--bouton-menu);
    color: #fff;
}

/* Couleur des boutons du menu principal en Hover (au passage de la souris) ----------------------------------------------------------------------- */
.website-navigation .nav-pills .nav-link:hover, .website-navigation .nav-pills .show > .nav-link { 
    background: var(--hover-menu);
}

{ /* Transition (survol du curseur) sur le menu --------------------------------------------------------------------------------------- */
.website-navigation .nav-pills .nav-link 
    transition: var(--transition);
}

/* ============================ Menu dÃ©roulant (principal) ============================ */

/* Style du menu dÃ©roulant (principal)  --------------------------------------------------------------------------------------- */
.website-navigation .nav-pills .dropdown-menu {
    background: var(--menu);
    border: 0px;
    border-radius:0px;
    margin: 0;
    transform: translate3d(-0px, 50px, 0px) !important;
}

/* Couleur du texte dans le menu dÃ©roulant (principal) & transition ----------------------------------------------------------------------- */
.website-navigation .dropdown-menu a { 
    color: #fff;
    transition: var(--transition);
}

/* Couleur dans le menu dÃ©roulant (principal) hover  (au passage de la souris) ----------------------------------------------------------------------- */
.website-navigation .dropdown-menu li.nav-item:hover a { 
    color: var(--hover) !important;
    background: #ecf0f4;
}

/* Correction bug du couleur sur les boutons du menu dÃ©roulant (principal) hover (au passage de la souris) ----------------------------------------------------------------------- */
ul.dropdown-menu li:not(.not-white):hover { 
    background-color: #ecf0f4!important;
}

/*==================================================================================*/
/*===================================== FOOTER =====================================*/
/*=================================================================================*/

/* Style et couleur du footer ----------------------------------------------------------------------- */
footer { 
    background-color: #272F3D !important;
    margin-top: 0px;
    padding-top: 50px;
}

/* Style et couleur du texte du footer ----------------------------------------------------------------------- */
footer li a { 
    color: #fff;
    background-image: linear-gradient(currentColor, currentColor);
    background-position: 0% 100%;
    background-repeat: no-repeat;
    background-size: 0% 1px;
    transition: background-size 0.3s;
}

/* Style et couleur du texte du footer hover ----------------------------------------------------------------------- */
footer li a:focus, footer li a:hover { 
    color: #fff;
    background-size: 100% 1px;
    font-weight: 500;
}

 /* SÃ©parateur du footer entre les Ã©lements  ----------------------------------------------------------------------- */
div.col-sm-4:nth-child(2), div.col-sm-4:nth-child(3), div.col-sm-4:nth-child(6) {
    border-left: 1px solid rgba(255, 255, 255, 0.25);
    height: 175px;
}
/* SÃ©parateur du footer entre les Ã©lements  ----------------------------------------------------------------------- */
div.col-sm-4:nth-child(4){ 
    border-left: 1px solid rgba(255, 255, 255, 0.25);
    border-right: 1px solid rgba(255, 255, 255, 0.25);
    height: 175px;
}

/*==================================================================================*/
/*==================================== RESPONSIVE ==================================*/
/*==================================================================================*/

/* Correction du chevauchement du bouton [+dÃ©poser dans HAL] avec la barre de rechercher ----------------------------------------------------------------------- */
@media (min-width: 992px) and (max-width: 1200px) { 
#searchHeaderList {
    width: 50%!important;
}
}

{{< /code >}}

## Pour aller plus loin

* <a href="https://inria.hal.science/page/creer-personnaliser-collection" target="_blank">Créer et modifier une collection en toute simplicité avec l'aide du Template HTML/CSS d'Inria</a>
* <a href="https://doc.hal.science/" target="_blank">La documentation HAL</a>

