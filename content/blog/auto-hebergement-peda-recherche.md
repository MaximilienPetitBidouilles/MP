---
date: '2025-04-09T10:37:51+02:00'
draft: false
title: 'Auto-héberger pour la pédagogie et la recherche'
author: Maximilien Petit
tags: ["YunoHost"]
readingTime: true
---
{{< toc >}}

<div style="background-color: #fff7f1; border: 1px solid #d22000; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
  {{< details summary="Pour information" >}}
Ne pratiquez pas cette bidouille chez vous si vous n'avez pas quelques bases en informatique. Mais en même temps, c'est un bon moyen d'apprendre par la pratique...
{{< /details >}}
</div>

# Le problème

**On souhaite doter une unité de recherche SHS d'un serveur abordable, rapide et sécurisé**. Et ce, pour plusieurs raisons : se "libérer" des contraintes et du coût du *cloud* propriétaire (Google Drive, Dropbox), pouvoir tester aisément des applications en ligne sans entraves. La solution d'auto-hébergement doit également avoir un "potentiel pédagogique" pour les formations et UE d'humanités-numériques. C'est un bon moyen de sensibiliser les étudiants, doctorants et enseignants-chercheurs sur la souveraineté des données.

**Cet auto-hébergement doit pouvoir offrir également la possibilité d'héberger une instance Omeka S** afin de tester des bases de données et projets SHS. Cette instance est utilisée comme une *sandbox*/un bac à sable, le déploiement en ligne s'effectue ensuite par d'autres biais (principalement, les services d'Huma-Num).

## Qui peut aider ? 

**Personne !** Enfin, si, c'est évidemment de l'informatique donc cela relève des personnels ITRF de la BAP E. Néanmoins, autant prévenir : **l'auto-hébergement n'est pas une pratique réalisable au sein d'une université car, bien entendu, cela va a l'encontre des règles de sécurité et des procédures**. Il faut donc pratiquer cela chez soi, et avec parcimonie. On le verra plus loin, l'auto-hébergement est selon moi une pratique sécurisée, et offre toutes les possibilités de gestion et d'administration d'un serveur classique mais c'est un usage *exotique* donc il est tout à fait normal de ne pas prendre de risques. 

J'ajoute que les unités de recherche SHS peuvent, en complément d'un auto-hébergement hors les murs, installer dans leurs locaux des serveurs domestiques (NAS) qui, là, seront sécurisés par les services informatiques. Et les plus chanceux dans les universités les plus dotées pourront utiliser des *data center*/centres de données. 

**Mais, selon moi (conviction personnelle), toutes ces solutions sont complémentaires**. J'estime que les pratiques pédagogiques et de recherche en SHS ne nécessitent pas nécessairement l'achat de serveurs rutilants, onéreux. D'autant plus quand vous manquez de personnels pour gérer au quotidien ce matériel rutilant, onéreux. 

## La bidouille

On s'oriente vers l'installation de YunoHost sur un Raspberry Pi 4 Model B.

**YunoHost est une application qui va vous permettre de gérer et administrer votre serveur**. Il y a toute une communauté pour faire évoluer ce système d'exploitation et il est simple à prendre en main. C'est l'une des solutions les plus pertinentes pour la pratique de l'auto-hébergement. Yunohost repose sur Debian, est doté d'une interface web bien pensée et permet de **déployer un catalogue d'applications en quelques clics** : <a href="https://apps.yunohost.org/" target="_blank">la liste est ici</a>

Pour les unités de recherche, ce catalogue est précieux. Vous pouvez installer et essayer, sans entraves, Nextcloud, FreshRSS, Collabora Online, Penpot, Joplin, Paperless-ngx, Dokuwiki, Mastodon, WordPress, HedgeDoc, Kanboard, Lufi, GitLab, Castopod, Weblate, Moodle, Overleaf, JupyterLab, eLabFTW, OJS, Omeka S, etc.  

**Un Raspberry Pi est un "nano-ordinateur monocarte à processeur ARM"**. Imaginez un ordinateur de la taille d'une carte de crédit, qui coûte moins de 100 euros. Ces machines sont pensées en amont par des chercheurs de Cambridge et une fondation. L'idée étant d'avoir du matériel flexible et à bas coût afin de démocratiser la pratique de l'informatique. **Il y a une communauté internationale (de la recherche à la simple bidouille) pour déployer des projets, des méthodes, et des pratiques où le Raspberry Pi est au centre.**

### L'installation

Pour installer Yunohost sur Raspberry Pi 4, je recommande d'avoir **le logiciel SD Card Formater** pour formater une carte micro SD et **Etcher** pour "flasher" les images. Les liens en fin d'article.

- Télécharger l'image sur le site de Yunohost : <a href="https://repo.yunohost.org/images/yunohost-bookworm-12.0-rpi-stable.img.zip " target="_blank">ici</a>

- Flashez l'image sur la carte micro SD en utilisant Etcher ; 

- Insérer la carte dans votre Raspberry Pi et allumez-le, sans oublier de le relier via ethernet à votre routeur/box à la maison et via hdmi à un écran pour vérifier le bon fonctionnement de l'installation ; 

- Notez dans un coin l'IP de votre Raspberry ; 

- Avec un PC ou ordinateur portable sur le même réseau que le Raspberry, ouvrez le lien suivant : https://yunohost.local

- Suivez les indications qui s'affichent pour le paramétrage : choix du nom de domaine (votre propre nom de domaine ou un nom de domaine déjà paramétré pour Yunohost. Je recommande la dernière solution pour une première installation), du mot de passe administrateur (qui sera utile également pour le SSH et le SFTP). La "post-installation" peut s'avérer longue, c'est normal ; 

- Connectez-vous avec votre mot de passe admin et créez un premier utilisateur avec un mot de passe différent. En effet, l'admin se connecte à l'interface d'aministration mais pas sur le portail des utilisateurs. Cliquez sur "Comptes" et "Nouveau compte" pour l'ajout de cet utilisateur ; 

- Lancez un premier diagnostic de votre installation : cliquez sur "Diagnostic" ; 

- Certaines opérations à faire en fonction des résultats du diagnostic, le plus souvent : ouvrir les ports utiles à votre usage sur votre box FAI. Pour ce faire, la procédure diffère en fonction de votre FAI. Il s'agit d'activer le UPnP et de créer des règles NAT/PAT dans votre interface admin de box, tout en adaptant le pare-feu. N'ouvrez que ce qui est réellement nécessaire ; 

- Mettez à jour le système Yunohost avant d'installer des applications : "Mise à jour du système" ; 

- Ajoutez un certificat **Let's Encrypt** pour rassurer les utilisateurs de votre portail, en fonction de l'usage souhaité : cliquez sur "Domaines", puis votre domaine, et enfin "Certificate" ; 

- Je recommande d'installer un client mail en passant par le catalogue des applications car Yunohost vous permettra de recevoir des alertes par mail pour gérer votre serveur. L'application *Roundcube* est par exemple intéressante.

**Ensuite, c'est à vous de jouer ! Et d'apprendre à gérer votre serveur. C'est-à-dire, de réaliser régulièrement des diagnostics, de mettre à jour des applications, d'effectuer des sauvegardes. Progressez à tâtons, ne déployez les services que temporairement, ne sauvegardez pas  des données critiques et essentielles sans avoir d'autres solutions de sauvegarde (la règle 3-2-1).**

Ci-dessous, des captures d'écran de l'interface Yunohost. Vous pouvez ainsi réaliser que la solution offre des fonctionnalités pour faire des diagnostics de sécurité, des sauvegardes de vos installations, des mises à jour de votre système, une gestion de vos domaines et de vos utilisateurs. 

<img src="/MP/images/yuno_1.PNG" alt="YunoHost 1" style="width:100%; height:auto;">

<img src="/MP/images/yuno_2.PNG" alt="YunoHost 2" style="width:100%; height:auto;">

<img src="/MP/images/yuno_3.PNG" alt="YunoHost 3" style="width:100%; height:auto;">

## En bonus : les usages

Depuis que je pratique l'auto-hébergement (3 ans), je n'ai eu aucun problème de sécurité, aucun problème de plantage matériel et j'ai eu la possibilité de constater que les usages sont multiples pour la recherche et la pédagogie : 

* J'ai déployé des instances Omeka S utilisées dans des cours et en amont de certains projets de recherche ; 
* J'ai permis à des doctorants et des chercheurs de bénéficier d'espaces *cloud* temporaires (50Go sur Nextcloud, sur une période déterminée) pour gérer aisément des données ; 
* J'ai donné la possibilité à certains services, toujours temporairement, de déployer et tester des applications (par exemple un cahier de laboratoire électronique) ;
* J'ai initié des étudiants de M1 à la pratique de l'auto-hébergement et certains, désormais en thèse, continuent afin de sauvegarder leurs données. Aucune perte de fichiers à déplorer à ce jour ; 
* Le serveur est parfois utilisé comme un *bac à sable* temporaire pour des formations doctorales centrées sur un outil ; 

**L'idée étant toujours de déployer des solutions temporaires pour "débloquer" les pratiques.**

Au-delà de l'auto-hébergement, **l'intérêt également d'utiliser du matériel flexible comme le Raspbery Pi, c'est de pouvoir le détourner facilement et rapidement pour d'autres usages inattendus.** 

Par exemple, ci-dessous, la photo d'une "station d'écoute" permettant à des publics d'un colloque célébrant les 30 ans d'une unité de recherche d'écouter les créations sonores et podcasts du laboratoire. La station est basée sur un Raspberry Pi 4 Modèle B, un module de carte son, un écran tactile, et des logiciels libres (Raspberry Pi OS, Tenacity, VLC, Qmmp).

<img src="/MP/images/station_ecoute_colloque.png" alt="Station d'écoute" style="width:100%; height:auto;">

## Pour aller plus loin

* <a href="https://doc.yunohost.org/fr" target="_blank">Documentation de YunoHost</a>
* <a href="https://www.raspberrypi.com/" target="_blank">Site officiel de Raspberry Pi</a>
* <a href="https://www.cl.cam.ac.uk/projects/raspberrypi/" target="_blank">Raspberry Pi et University of Cambridge</a>
* <a href="https://www.sdcard.org/downloads/formatter/" target="_blank">SD Card Formater</a>
* <a href="https://etcher.balena.io/" target="_blank">Etcher</a>