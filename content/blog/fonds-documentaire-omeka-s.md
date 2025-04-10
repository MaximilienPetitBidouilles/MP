---
date: '2025-04-10T10:29:41+02:00'
draft: false
title: 'Valoriser un fonds documentaire de laboratoire avec Omeka S'
author: Maximilien Petit
tags: ["Omeka S"]
readingTime: true
---
{{< toc >}}

# Le problème

**Certains laboratoires (de moins en moins...) disposent de bibliothèques qui sont le plus souvent "exotiques" en termes de documentation**. Ces fonds possèdent parfois plusieurs "strates" d'indexation et de catalogage car, de fait, ces unités de recherche n'ont pas de personnel pour s'en charger, ou du personnel qui ne dispose pas d'une formation en documentation, ou du personnel qui n'a tout simplmenent pas le temps de s'en préoccuper. Il y a même des laboratoires où ce sont les enseignants-chercheurs et les doctorants qui font évoluer les fonds, et qui s'en occupent au quotidien. **Donc vous avez des bibliothèques qui sont très particulières car, évidemment, tout est à faire** : beaucoup de documents ne sont pas dans le Sudoc, il n'y a jamais eu véritablement un "désherbage" et il est donc difficile d'en assurer une valorisation. Les services communs de la documentation associent, ou non, ces bibliothèques (par convention). Et, quoi qu'il en soit, **le soutien de la filière bibliothèque est toujours précieux** pour les unités (par le catalogue central, par l'aide apportée sur la création de notices, par l'appui professionnel).

**Même avec ces problèmes, il importe selon moi de garder ces fonds, notamment car il y a très souvent des documents, et une littérature grise, que l'on trouve difficilement ailleurs (ou nulle part)**. D'autant plus que ces fonds sont parfois le reflet et l'histoire d'une unité de recherche et cela me semble pertinent d'avoir une stratégie de valorisation. À la fois pour les publics, pour l'unité (ses enseignants-chercheurs, les disciplines et les méthodologies).

**En réalité, même quand un fonds de laboratoire est identifié sur le SUDOC, il est presque invisible pour les usagers**. Les SIGB (Système de gestion de bibliothèque) modernes dans les universités agrègent des dizaines de bibliothèques et "moissonnent" des bases de données documentaires. Une notice se retrouve perdue dans "une masse" et **il y a une tendance professionnelle à vouloir "simplifier" à outrance les interfaces de recherche**. Donc il est de plus en plus difficile, et même parfois impossible dans certaines universités, d'aller précisément faire des recherche de documents ciblées par fonds de laboratoire/localisation.

**Face à cela il me semble important, dans certains cas, de pouvoir doter les fonds de laboratoires de catalogues indépendants**. Avec cette idée de ne pas doubler le travail de catalogage et de toujours privilégier quoi qu'il arrive le "circuit classique" SUDOC/catalogue bibliothèque centrale.

## Qui peut aider ?

Les personnels de la filière bibliothèque et les personnels de la BAP F (documentation).

## La bidouille

**Le résultat est visible ici : <a href="https://bibliohisto.org/s/bibliohisto/page/welcome" target="_blank">Bibliohisto</a>**

**Bibliohisto, donc, est un catalogue de notices bibliographiques de littérature grise (mémoires, thèses, HDR, etc.) des collections de la bibliothèque du laboratoire**. Les sujets qui structurent les fonds : l'histoire de l'édition, du livre, de la lecture et des archives, l'histoire des médias (presse, radio, tv, cinéma, internet, image, propagande), les arts du spectacle (théâtre, musique, danse) et loisirs (photos, sport), le patrimoine et la ville (urbanisation, architecture), les relations culturelles internationales, les rapports sociaux de sexe dans le champ culturel. Les documents couvrent une période chronologique précise : fin XVIIIe siècle à nos jours. 

Comme indiqué plus haut, il s'agit essentiellement d'une bibliothèque constituée, durant plus de 30 ans, par des dons d'enseignants-chercheurs, et quelques rares achats (moins de 2000 euros par an). **Ce catalogue donne ainsi une visibilité à 2994 notices du fonds**.

**Ce catalogue se base sur Omeka S**. C'est l'outil le plus pertinent car il est pensé pour la pratique des SHS et il sépare utilement la gestion documentaire des notices et l'exposition/valorisation des contenus. J'ajoute qu'**Omeka S n'a pas de problème de pérennité** : il dispose d'une communauté internationale et il est utilisé par beaucoup d'institutions culturelles et patrimoniales (archives, bibliothèques, musées). 

**Certaines "bidouilles" à venir seront centrées sur la formation des publics et Omeka S.**

En attente d'une reprise par Huma-Num, ce catalogue est hebergé par Reclaim Hosting. Une entreprise anglo-saxonne qui permet d'installer et gérer très facilement une instance Omeka S et qui travaille avec de nombreuses universités et écoles à l'internationale. J'ajoute que le support de Reclaim Hosting est extrêmement efficace.

**La gestion des thèmes sous Omeka S est relativement hasardeuse**, c'est le point faible de l'outil. **On fait donc le choix d'utiliser le thème "Foundation"** car il est flexible, embarque plusieurs feuilles de style et est *responsive* (il s'adapte à tous les écrans, y compris les smartphones). On modifie toutefois le thème (et le *stylesheet* *Sea Foam* du thème) avec notre propre CSS et en utilisant le module CSSEditor. Le CSS ci-dessous : 



{{< code language="css" title="CSS Bibliohisto" open="false" >}}

.site-title img {
    max-height: 200px;
    width: auto;
}

.button:hover, :hover[type="submit"], :hover[type="button"], .site-page-pagination > a:hover, [class^="numeric-"] label.numeric-toggle-time.button:hover, [class*="numeric-"] label.numeric-toggle-time.button:hover, .button:focus, :focus[type="submit"], :focus[type="button"], .site-page-pagination > a:focus, [class^="numeric-"] label.numeric-toggle-time.button:focus, [class*="numeric-"] label.numeric-toggle-time.button:focus {
    background-color:#007198;
    color: #003C57;
}
.resource-list .resource {
    margin: 1rem 0;
    border-bottom: 1px solid #007198;
    padding-bottom: 1rem;
}

.button, [type="submit"], [type="button"], .site-page-pagination>a, [class^="numeric-"] label.numeric-toggle-time.button, [class*="numeric-"] label.numeric-toggle-time.button, .button.disabled, .disabled[type="submit"], .disabled[type="button"], .site-page-pagination>a.disabled, [class^="numeric-"] label.disabled.numeric-toggle-time.button, [class*="numeric-"] label.disabled.numeric-toggle-time.button, .button[disabled], [disabled][type="submit"], [disabled][type="button"], .site-page-pagination>a[disabled], [class^="numeric-"] label.numeric-toggle-time.button[disabled], [class*="numeric-"] label.numeric-toggle-time.button[disabled], .button.disabled:hover, .disabled:hover[type="submit"], .disabled:hover[type="button"], .site-page-pagination>a.disabled:hover, [class^="numeric-"] label.disabled.numeric-toggle-time.button:hover, [class*="numeric-"] label.disabled.numeric-toggle-time.button:hover, .button[disabled]:hover, [disabled]:hover[type="submit"], [disabled]:hover[type="button"], .site-page-pagination>a[disabled]:hover, [class^="numeric-"] label.numeric-toggle-time.button[disabled]:hover, [class*="numeric-"] label.numeric-toggle-time.button[disabled]:hover, .button.disabled:focus, .disabled:focus[type="submit"], .disabled:focus[type="button"], .site-page-pagination>a.disabled:focus, [class^="numeric-"] label.disabled.numeric-toggle-time.button:focus, [class*="numeric-"] label.disabled.numeric-toggle-time.button:focus, .button[disabled]:focus, [disabled]:focus[type="submit"], [disabled]:focus[type="button"], .site-page-pagination>a[disabled]:focus, [class^="numeric-"] label.numeric-toggle-time.button[disabled]:focus, [class*="numeric-"] label.numeric-toggle-time.button[disabled]:focus {
    background-color:#007198;
    color: #003C57;
}


.top-bar {
    background-color: #007198;
}

.top-bar ul {
    background-color: #007198;
}

a:link { color: #051C24 }          /* Liens non visités */
a:visited { color: #051C24 }     /* Liens visités */
a:hover { background: #007198 }  /* Liens survolés */
a:active { color: #007198 }         /* Liens actifs */

p:active { background: #eee; }

span.title {
    color: #051C24;
}

a.nav-header {
    color: #fefefe;
   border-radius: 10%;
}


.menu .active>a, .toc-block>ul .active>a, .toc-block ul ul .active>a {
    background: #003C57;
    color: #fefefe;
}

.button {
    background-color:#007198;
    color: #003C57;
    
}

.button:hover {
    background-color:#007198;
    color: #003C57;
    
}



.label, .filter-label, .filter-value {
    display: inline-block;
    padding: 0.33333rem 0.5rem;
    border-radius: 0;
    font-size: .8rem;
    line-height: 1;
    white-space: nowrap;
    cursor: default;
    background: #007198;
    color: #fefefe;
}

{{< /code >}}

**Le catalogue est pensé pour être le plus simple possible en termes d'utilisation**. On installe et on configure plusieurs modules pour y arriver (les liens en fin de bidouille) : Advanced Search, Block Plus, Blocks Disposition, Collecting, Common, CSV Import, Easy Admin, EU Cookie Bar, Export, Generic module, Log, Mapping, Metadata Browse, Sharing, Shortcode, Timeline, Zotero Import.

**Chaque notice doit être très simple en termes de métadonnées** (Dublin Core) pour faciliter et accélérer le projet car il y a des imports de notices mais aussi des créations (en partant d'un inventaire sur Zotero). Par exemple, pour une notice de mémoire, voici ce qui est envisagé : Titre du mémoire, Auteur du mémoire, Jury de soutenance, Département, Date de soutenance, Mention du mémoire, Niveau du mémoire, Notation.

**Idem, il faut simplifier autant que possible la navigation**. Le site contient 6 pages visibles. Chaque page doit être centrée sur un ensemble cohérent de notices : une page pour les notices en Histoire, une page pour les notices en Histoire des médias, une page pour les notices en Histoire du livre, une page pour les notices Architecture et Patrimoine, une page pour présenter le projet. On ajoute également une page "Monographies" pour les notices qui, par ailleurs, se trouvent déjà dans le catalogue de la BU centrale et qui sont les documents que le laboratoire achète ou intègre à ses collections après un don.

**Dans l'instance Omeka S de notre catalogue, chaque page doit suivre le même modèle** : un titre de page, un "bloc HTML" pour indiquer la démarche, un "bloc Aperçu des ressources" pour mettre en valeur 12 notices du lot, un "bloc Frise chronologique" qui interroge les notices par date de publication.

**Les 2994 notices sont regroupées, via Omeka S, dans 15 collections**. La plupart du temps, les alimentations de la base se font par le biais de l'import d'un fichier CSV structuré ou l'import de notices depuis Zotero ou la création de notices directement dans le *back-office* du logiciel.

**Les métadonnées "Créateur" et "Contributeur" de chaque notice sont interrogeables (cliquables)**. On peut ainsi, par exemple, consulter toutes les notices d'un même auteur en cliquant dessus. Cette opération s'effectue grâce au module *Metadata Browse*.

Une bidouille à venir détaillera comment ce simple catalogue de notices est également au centre d'une stratégie de sauvegarde des mémoires de M1 et M2 d'une formation.

## Pour aller plus loin

* <a href="https://omeka.org/s/" target="_blank">Omeka S</a>
* <a href="https://omeka.org/s/themes/foundation/" target="_blank">Thème Foundation</a>
* <a href="https://omeka.org/s/modules/CSSEditor/" target="_blank">CSSEditor</a>
* <a href="https://omeka.org/s/modules/AdvancedSearch/" target="_blank">Advanced Search</a>
* <a href="https://omeka.org/s/modules/BlockPlus/" target="_blank">Block Plus</a>
* <a href="https://omeka.org/s/modules/BlocksDisposition/" target="_blank">Blocks Disposition</a>
* <a href="https://omeka.org/s/modules/Collecting/" target="_blank">Collecting</a>
* <a href="https://omeka.org/s/modules/Common/" target="_blank">Common</a>
* <a href="https://omeka.org/s/modules/CSVImport/" target="_blank">CSV Import</a>
* <a href="https://omeka.org/s/modules/EasyAdmin/" target="_blank">Easy Admin</a>
* <a href="https://omeka.org/s/modules/EUCookieBar/" target="_blank">EU Cookie Bar</a>
* <a href="https://omeka.org/s/modules/Export/" target="_blank">Export</a>
* <a href="https://github.com/Daniel-KM/Omeka-S-module-Generic" target="_blank">Generic module</a>
* <a href="https://omeka.org/s/modules/Log/" target="_blank">Log</a>
* <a href="https://omeka.org/s/modules/Mapping/" target="_blank">Mapping</a>
* <a href="https://omeka.org/s/modules/MetadataBrowse/" target="_blank">Metadata Browse</a>
* <a href="https://omeka.org/s/modules/Sharing/" target="_blank">Sharing</a>
* <a href="https://omeka.org/s/modules/Shortcode/" target="_blank">Shortcode</a>
* <a href="https://omeka.org/s/modules/Timeline/" target="_blank">Timeline</a>
* <a href="https://omeka.org/s/modules/ZoteroImport/" target="_blank">Zotero Import</a>