# GLACIAL

Glacial est une extension qui ajoute certaines fonctionnalités à gel.usherbrooke.ca.

## Navigateurs supportés

### Firefox

Prendre la dernière version dans les [releases](https://github.com/antoineMoPa/glacial/releases)

Fichier .xpi 

Télécharger et effectuer un «drag and drop» dans n'importe quelle fenêtre firefox.

### Chrome/Chromium

Prendre la dernière version dans les [releases](https://github.com/antoineMoPa/glacial/releases)

Fichier .crx

Télécharger et effectuer un «drag and drop» dans la fenêtre «extensions» de chrome.

#### Safari (via le code source)

Voir les instructions pour safari plus bas dans «Développer pour Safari»

## Fonctionnalités

* Affichage des notes en pourcentage (Il faut appuyer le bouton)
* Surlignement en jaune des nouvelles notes
* Affichage de toutes les pondérations dans l'infobulle<br>
   Lorsqu'on survole les évaluations dont la note n'a pas encore été entrée.
* Recalcul de la moyenne du groupe dans les cellules de notes finales.<br>
   (Sans l'extension, votre note accumulée est affichée et la moyenne du groupe est affichée)
* Téléchargement de tous les fichiers (Intégration du code de @frederik-labbe: https://github.com/frederik-labbe/GelDocuments)

## Structure de fichiers

Les fichiers dans le dossier `common/` sont faits pour être placés automatiquement dans le répertoire `firefox/`, `chrome/` et `safari/`.

Sous linux, il suffit de faire `make`, car un makefile est présent pour faire exactement ça. Sous windows, vous pouvez toujours copier/coder manuellement et ramener ça dans `common/` après. Le mieux reste d'installer `make` sur votre plateforme.

### Dossier common:

Le js et le css que l'on insère dans les deux extensions.

### Dossier chrome:

Tout ce qui est propre à chrome

Les fichiers du dossier `common/` sont copiés ici même.

### Dossier firefox:

Tout ce qui est propre à firefox. 

Les fichiers du dossier `common/` sont copiés dans le sous dossier `data/`.

### Dossier Safari:

Tout ce qui est propre à Safari. 

# Notre workflow

## Conventions

Lire les conventions et les respecter: [conventions](conventions.md)

## Développer pour Chrome/Chromium

Allez voir [ici](https://developer.chrome.com/extensions/getstarted), dans la section intitulée «load the extension».

Faites «reload» dans le gestionnaire d'extensions lorsque vous faites des changements.

## Développer pour Firefox

Il faut downloader nodejs et jpm. Ensuite, c'est facile.

Pour savoir comment installer jpm:

    https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/jpm

Ensuite, on peut aller dans le dossier /firefox et rouler:

    jpm run

`Jpm` part alors firefox avec l'extension activée, suffit d'aller sur notre site favori (à part Wikipédia et [Hacker news](http://news.ycombinator.com)).

Il est pertinent d'installer l'extension [autoinstaller](https://addons.mozilla.org/en-US/firefox/addon/autoinstaller/) qui évite de restarter firefox et de se reconnecter à chaque fois.

Suffit alors d'entrer la commande suivante pour rafraichir l'extension:

    jpm watchpost --post-url http://localhost:8888

Ainsi lorsqu'un changement est fait dans le dossier de firefox, l'extension va actualisé dans firefox. (ne marche pas dans le dossier commun)

Depuis Firefox 43 (Décembre 2015), il est nécessaire de désactiver `xpinstall.signatures.required` dans `about:config` pour que ceci fonctionne.

## Développer pour Safari

Ajouter manuellement de la façon suivante :

Safari —> Développement —> Afficher extension Builder —> + —> Ajouter une extension —> Sélectionner le répertoire contenant ".safariextension" comme extension —>  contenu injecté —> script de fin —> main.js —> feuille de style —> style.css —> Installer

Pour coder	 : Xcode 

Pour débogguer	 : L’inspecteur Web

## Github

Voici le processus pour que votre code se retrouve dans l'extension

1. Discuter dans un «Issue» d'une fonctionnalité ou d'un bug
2. S'entendre sur une manière de faire dans l'Issue
3. Coder
4. Faire un `git push` vers votre clone du repo sur github
5. Faire une pull request avec une description claire qui explique le code changé et ce qu'il fait

## Building

Le Makefile permet de copier les fichiers qui sont communs à la version firefox et chrome dans les bon répertoires.

Pour builder (sous linux/quelquechose qui a bash)

    make build

## Test

Tester dans chrome et firefox, les instructions sont plus haut.
