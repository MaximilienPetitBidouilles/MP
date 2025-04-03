---
date: '2025-04-03T20:25:29+02:00'
draft: truefalse
title: 'Transcrire des entretiens avec Whisper'
author: Maximilien Petit
tags: ["LLM","Whisper"]
readingTime: true
---
{{< toc >}}

<div style="background-color: #fff7f1; border: 1px solid #d22000; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
  {{< details summary="Pour information" >}}
  Cette bidouille n'est pas obsolète mais, de fait, on peut aujourd'hui être plus rapide et plus efficace concernant l'usage de Whisper. Son aspect *open source* permet à beaucoup de développeurs indépendants (ou non) de travailler avec et de le modifier. Il y a des modèles "turbo" qui permettent un usage intéressant y compris avec des machines qui ne disposent pas de grosses cartes graphiques. Aujourd'hui, personnellement, je travaille toujours avec Whisper mais par le biais de l'application <a href="https://github.com/kaixxx/noScribe" target="_blank">noScribe</a> en particulier car cela permet de détecter les locuteurs et de travailler plus aisément l'horodatage.
  {{< /details >}}
</div>

# Le problème

On souhaite **transcrire rapidement et facilement des entretiens**. L'utilisation des *LLM* est envisagée car les résultats sont impressionnants depuis plusieurs mois. Il faut toutefois toujours corriger à la main et ne pas oublier que les outils ont leurs propres biais. Pour ce qui est des problématiques RGPD, la transcription ne doit pas se faire avec un outil en ligne. Il faut donc installer en local un *LLM*, le paramétrer et le faire tourner hors ligne sur une machine relativement puissante.

## Qui peut aider ?

En priorité, **les personnels de la BAP D** et notamment celles et ceux qui ont une expertise en "Production, traitement et analyse des données". Ne pas hésiter, donc, à travailler avec les collègues dans **les laboratoires de sociologie** par exemple.

## La bidouille

**Elle fonctionne avec Python 3.9.9, Pytorch 2.4.0 (stable, Windows, Pip, Python, CUDA 11.8), Chocolatey 2.3.0, ffmpeg 7.0.1, Whisper v20231117. La transcription est réalisée avec un ordinateur portable équipé d'une carte graphique Geforce RTX 4090.**

**On télécharge et on installe <a href="https://www.python.org/downloads/" target="_blank">Python</a> sur sa machine**. Whisper peut fonctionner avec les versions 3.8 à 3.11. Pour cette bidouille, nous installons la version 3.9.9.

- Avant l'installation, bien cocher la case « add python to path » ;
- Après l'installation, on vérifie : on ouvre l'invite de commande (cmd dans la barre de recherche de votre machine) puis on tape 

```code
python -V
```
- En cas de bon fonctionnement, l'invite de commande vous indique la version de Python installée.

**On télécharge et on installe en local <a href="https://pytorch.org/get-started/locally/" target="_blank">PyTorch</a> sur sa machine.**

- Pour cette bidouille, voici ce que l'on sélectionne pour PyTorch 2.4.0 : stable, Windows, Pip, Python, CUDA 11.8. Si vous n'avez pas une carte graphique puissante sur votre machine, ne sélectionnez pas CUDA mais CPU. Après sélection des choix, on copie la commande (« run this command ») ;
- On colle la commande dans l'invite de commande de sa machine lancée en mode administrateur (clic droit sur cmd puis « Exécuter en tant qu'administrateur »).

**On télécharge et on installe en local <a href="https://chocolatey.org/install" target="_blank">Chocolatey</a> sur sa machine.**

- On sélectionne « individual » pour le mode d'installation ;
- On copie la commande (« Now run the following command ») ;
- On colle la commande dans Powershell exécuté en administrateur.

**On télécharge et on installe en local ffmpeg sur sa machine.**

- Dans PowerShell exécuté en administrateur : 
```code
choco install ffmpeg 
```

- On vous demandera une fois « oui ou non » pour l'exécution du script, tapez « y » pour oui.

**On télécharge et on installe <a href="https://github.com/openai/whisper" target="_blank">Whisper</a> sur sa machine.**

- On ouvre l'invite de commande en administrateur puis : 
```code
pip install -U openai-whisper
```

**Après l'installation de Python, Pytorch, Chocolatey, ffmpeg et Whisper, vous pouvez maintenant travailler :)**

- Placez vos fichiers à transcrire dans un dossier sur votre machine (par exemple, sur le bureau) ;
- Ouvrez le dossier puis cliquez sur la barre de chemin d'accès aux fichiers, supprimez tout puis tapez "cmd". Cela ouvre l'invite de commande qui va pouvoir travailler dans le bon répertoire de fichiers ;
- Admettons, nous souhaitons transcrire un fichier intitulé « test » au format WAV. Ouvrez l’invite de commande puis tapez : 
```code
 whisper test.wav
```
- Nous souhaitons transcrire un fichier intitulé « test » au format WAV en utilisant le modèle « large » de Whisper : 
```code
whisper test.wav --model large
```
Plusieurs modèles à disposition, de plus en plus performants, de plus en plus gourmands en ressources **(c'est la VRAM de la carte graphique qui détermine votre choix de modèle)** : tiny, base, small, medium, large, large-v2, large-v3. Lorsque vous utilisez pour la première fois un modèle, l'invite de commande doit d'abord le télécharger. Par défaut, c'est le modèle « small » qui est utilisé ;
- Nous souhaitons transcrire un fichier intitulé « test » au format WAV en indiquant à Whisper la langue du fichier : 
```code
whisper test.wav --language French
```
- Nous souhaitons transcrire un fichier intitulé « test » au format WAV, spécifier la langue (fr) et ajouter une tâche de traduction (uk) : 
```code
whisper test.wav --language French --task translate
```
- Pour aller plus loin, tapez : 
```code
whisper --help
```
- Une fois la transcription terminée dans l'invite de commande, vous trouverez plusieurs fichiers dans votre dossier avec les données : un fichier json, un srt, un tsv, un txt, un vtt. Ils contiennent tous le texte de la transcription ;
- Je ne le recommande pas mais vous pouvez transcrire plusieurs fichiers à la fois. Par exemple, avec deux fichiers : 
```code
whisper test1.wav test2.wav
```

**Si cela ne fonctionne pas et que vous ne trouvez pas l'origine du problème, il convient de tout désinstaller afin de recommencer le tutoriel depuis le début.**
Pour désinstaller proprement :

- Whisper, dans l'invite de commande en administrateur : 
```code
pip uninstall openai-whisper
```
- FFMPEG, dans l'invite de commande en administrateur : 
```code
choco uninstall ffmpeg
```
- PyTorch, dans l'invite de commande en administrateur : 
```code
Pip3 uninstall torch torchvision torchaudio
```
- Python : vous pouvez le désinstaller dans Windows comme un logiciel.
