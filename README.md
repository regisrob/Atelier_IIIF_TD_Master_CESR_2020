# Cours IIIF - TD Master Humanités Numériques (CESR)

Support du cours de travaux dirigés "Visualisation et fouille de données" dans le cadre du Master "Mediation Numérique de la Culture et des Patrimoines", École Supérieure en Intelligence des Patrimoines (ESI-Pat), Centre d'Études Supérieures de la Renaissance (CESR), Université de Tours.

Conçu et animé par **Régis Robineau** (coordinateur technique de Biblissima).	

## Recommandations et pré-requis techniques

- Utiliser de préférence les dernières versions des navigateurs **Firefox** ou **Chrome**
- Installer une extension à votre navigateur permettant d'afficher de façon lisible des documents JSON : **JSONView** (pour [Chrome](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) ou pour [Firefox](https://addons.mozilla.org/fr/firefox/addon/jsonview/)).
- Disposer d'un **éditeur de code** (même si dans l'absolu un simple éditeur de texte suffit) : par exemple Sublime Text, Visual Studio Code, NotePad++
- Installer les outils de développements suivants :
	- **Node.js** version v12.18.0 ou plus ([Télécharger Node.js](https://nodejs.org/fr/download/)) + **npm** version v6.14.4 ou plus (inclus dans node.js)
	- **Git** ([Télécharger](https://git-scm.com/downloads))

------

## Exercice 1 : API Image

### Rappels

#### Requête d'image

Dans l'API Image, une URL de requête d'image se conforme au modèle suivant :

```none
{scheme}://{server}{/prefix}/{identifier}/{region}/{size}/{rotation}/{quality}.{format}
```

Les paramètres d'URL spécifiées par l'API Image sont :

- [region](https://iiif.io/api/image/3.0/#41-region)
- [size](https://iiif.io/api/image/3.0/#42-size)
- [rotation](https://iiif.io/api/image/3.0/#43-rotation)
- [quality](https://iiif.io/api/image/3.0/#quality)
- [format](https://iiif.io/api/image/3.0/#45-format)

#### Requête d'information sur l'image (`info.json`)

Une URL de requête d'information sur l'image se conforme au modèle suivant :

```
{scheme}://{server}{/prefix}/{identifier}/info.json
```

### Questions

Soit l'URL d'image IIIF suivante : 
https://iiif.lib.ncsu.edu/iiif/mc00198-008-ff0051-000-001_0001/full/512,/0/default.jpg

1. quelle est l'URL du fichier information de cette image (`info.json`) ?
2. quelle est la largeur et la hauteur de la version pleine taille de cette image (dimension maximale) ?
3. Construire les URL IIIF correspondantes :
	- image pleine taille pivotée sur l'axe horizontal (miroir)
	- image pleine taille retournée à l'envers (180°)
	- image redimensionnée avec une hauteur de 250 pixels
	- image au format PNG et en niveau de gris

------

## Exercice 2 : API Présentation

### Rappels

#### Principe de base de l'annotation (Web Annotation Data Model)

![https://www.w3.org/TR/annotation-model/images/intro_model.png](https://www.w3.org/TR/annotation-model/images/intro_model.png)

#### Structure de base d'un Manifeste

```
Manifest

​	|__  Sequence

​		|__  Canvas

​			|__  Content
```

#### Structure complète

- API Présentation v2 : https://iiif.io/api/presentation/2.1/img/objects-all.png
- API Présentation v3 : ![https://iiif.io/api/assets/images/data-model.png](https://iiif.io/api/assets/images/data-model.png)

### Dissection d'un Manifeste

Inspectons ensemble la structure et les différentes composantes d'un Manifeste IIIF :

- Ouvrir le lien suivant dans votre navigateur (Firefox ou Chrome avec l'extension JSONView activée) : https://purl.stanford.edu/hg676jb4964/iiif3/manifest

	


------

## Exercice 3 : Identifier et sélectionner des ressources IIIF

Vous trouverez ci-dessous une liste non-exhaustive de sites qui proposent des objets numérisés compatibles avec IIIF (bibliothèques, archives, musées, agrégateurs). Les sites affichant clairement leur compatibilité et donnant accès aux Manifests ont été privilégiés.

**Consignes de l'exercice** : 

- Parcourir quelques sites ci-dessous et conserver dans des onglets séparés les différentes pages que vous avez ouvertes
	- essayer de sélectionner des objets de diverses natures (livre, tableau, carte, objet archéologique etc.) depuis différents types de collections.
- Copier à partir de ces sites quelques URL de Manifests dans un fichier texte sur votre ordinateur 
	- *Astuce* : l'URL du Manifest est parfois présente dans les métadonnées de l'objet, parfois située ailleurs dans l'interface (souvent "cachées" derrière le logo IIIF)
- Enregistrer le fichier
- Vous pouvez lancer les recherches qui vous intéressent sur plusieurs de ces sites, ou pour aller plus vite vous pouvez aussi cliquer sur les liens donnés en exemple dans la liste ci-dessous.

### Liste d'entrepôts IIIF

Pour une liste plus riche, voir https://iiif.io/guides/finding_resources/

#### Agrégateurs, portails, banques d'images

- [Biblissima IIIF-Collections](https://iiif.biblissima.fr/collections/) (manuscrits et imprimés anciens avant 1800) (exemple : https://iiif.biblissima.fr/collections/manifest/044a300f19837f83a3cf4c04f2641ace6b61641b)
- [Portail Biblissima](https://portail.biblissima.fr) (exemple : https://portail.biblissima.fr/fr/ark:/43093/desc0e5c216fbb094b28d21da14ddcf6f510f211fbc7)
- [HeidICON](https://heidicon.ub.uni-heidelberg.de/search) (exemple : https://heidicon.ub.uni-heidelberg.de/detail/762656)
- [Qatar Digital Library](https://www.qdl.qa/en/search/site/?f%255B0%255D=document_source%3Aarchive_source) (exemple : https://www.qdl.qa/en/archive/81055/vdc_100027090276.0x000004)
- [OCLC IIIF Explorer](https://researchworks.oclc.org/iiif-explorer/) (exemple : https://researchworks.oclc.org/iiif-explorer/manifest?url=https%3A%2F%2Fcdm16013.contentdm.oclc.org%2Fdigital%2Fiiif-info%2Fp16013coll27%2F4225%2Fmanifest.json) 

#### Bibliothèques

- [Biblioteca Apostolica Vaticana](https://digi.vatlib.it) (exemple : https://digi.vatlib.it/view/MSS_Vat.lat.3225)
- [Bayerische StaatsBibliothek, Munich](https://app.digitale-sammlungen.de/bookshelf/) (exemple : https://app.digitale-sammlungen.de/bookshelf/bsb00003881/view)
- [Bodleian Libraries, Oxford](https://digital.bodleian.ox.ac.uk) (exemple : https://digital.bodleian.ox.ac.uk/objects/faeff7fb-f8a7-44b5-95ed-cff9a9ffd198)
- [e-codices - Virtual Manuscript Library of Switzerland](https://e-codices.ch) (exemple : https://e-codices.ch/en/searchresult/list/one/fmb/cb-0007)
- [Cambridge University Library](https://cudl.lib.cam.ac.uk) (exemple : https://cudl.lib.cam.ac.uk/view/MS-ADD-00269/13)
- [Durham University and Cathedral Library](https://collections.durham.ac.uk) (exemple : https://iiif.durham.ac.uk/index.html?manifest=t1mk930bx00d)
- [Harvard University](https://library.harvard.edu/digital-collections) (exemple : https://id.lib.harvard.edu/curiosity/immigration-to-the-united-states-1789-1930/39-HUAM11324soc_urn-3:HUAM:OCP14752_dynmc)
- [Bibliotheca Hertziana, Max-Planck-Institut für Kunstgeschichte, Rom · Fotothek](https://foto.biblhertz.it/exist/foto/search.html) (exemple : https://foto.biblhertz.it/exist/foto/object.xql?id=08051840,T,001)

#### Musées

- [Art Gallery of Ontario](https://ago.ca/collection/browse) (exemple : https://ago.ca/mirador/compare?objects=5997,6275)
- [Belvedere](https://sammlung.belvedere.at/) (exemple : https://sammlung.belvedere.at/objects/6289/der-koch-le-pere-paul)
- [Germanisches Nationalmuseum - GMN](https://www.gnm.de/en/collections/collections/) (exemple : https://tafelmalerei.gnm.de/wisski/navigate/161/view)
- [Harvard Art Museums](https://www.harvardartmuseums.org/collections) (exemple : https://hvrd.art/o/296313)
- [J. Paul Getty Museum](http://www.getty.edu/art/collection/) (exemple : https://www.getty.edu/art/collection/objects/144/vincent-van-gogh-portrait-of-joseph-roulin-dutch-1888/)
- [National Gallery of Art - USA](https://www.nga.gov/collection.html) (exemple : https://www.nga.gov/collection/art-object-page.95419.html)
- [Princeton Art Museum](https://artmuseum.princeton.edu/collections/explore) (exemple : https://artmuseum.princeton.edu/collections/objects/22783)
- [Smithsonian Institution](https://collections.si.edu/search/results.htm?q=&iiif.enabled=true) (exemple : http://n2t.net/ark:/65665/sm489c1c193-694a-4012-8517-03ae07c89191)
- [SMK](https://open.smk.dk/en/) (exemple : https://open.smk.dk/en/artwork/image/KMSsp292)
- [The Royal Collection Trust](https://albert.rct.uk) (exemple : https://albert.rct.uk/collections/raphael-collection/vatican-frescoes/raphael-collection-portfolio-26)
- [The Frick Collection](https://www.frick.org/art) (exemple : https://collections.frick.org/objects/265/antwerp-van-goyen-looking-out-for-a-subject)
- [The Huntington](https://emuseum.huntington.org/collections) (exemple : https://emuseum.huntington.org/objects/12176/santuarioleon)
- [The Leiden Collection](https://www.theleidencollection.com/) (exemple : https://www.theleidencollection.com/viewer/satyrs-nymphs-putti-and-leopards-in-a-landscape/)
- [Yale Center for British Art](https://collections.britishart.yale.edu/) (exemple : https://collections.britishart.yale.edu/catalog/tms:1153)

#### **Exemples d'URL de Manifestes IIIF**

```
https://data.artmuseum.princeton.edu/iiif/objects/22783
https://www.theleidencollection.com/iiif/presentation/v2/2372/manifest/
https://www.nga.gov/api/v1/iiif/presentation/manifest.json?cultObj:id=95419
https://api.smk.dk/api/v1/iiif/manifest/?id=KMSsp292
https://foto.biblhertz.it/exist/foto/bhpd43644/manifest.json
https://manifests.britishart.yale.edu/manifest/7237
https://iiif.harvardartmuseums.org/manifests/object/296313
https://iiif.harvardartmuseums.org/manifests/object/170874
https://data.getty.edu/museum/api/iiif/144/manifest.json
https://data.getty.edu/museum/api/iiif/9421/manifest.json
https://www.nga.gov/api/v1/iiif/presentation/manifest.json?cultObj:id=52450
https://heidicon.ub.uni-heidelberg.de/manifest/iiif/1139791/manifest.json
https://iiif.bodleian.ox.ac.uk/iiif/manifest/faeff7fb-f8a7-44b5-95ed-cff9a9ffd198.json
https://www.e-codices.unifr.ch/metadata/iiif/bbb-0318/manifest.json
https://portail.biblissima.fr/iiif/manifest/ark:/43093/desc57cb76cd3739a24a9277b6669d95b5f3a590e771
https://digi.vatlib.it/iiif/MSS_Vat.lat.3225/manifest.json
https://cudl.lib.cam.ac.uk/iiif/MS-ADD-00269
```

## Exercice 4 : installer en local et prendre en main Mirador

Mirador est un visualiseur d'images configurable, extensible et facile à intégrer, qui permet d'annoter et de comparer des images provenant de différents entrepôts IIIF. Plus d'informations sur [projectmirador.org](https://projectmirador.org/).

### Installation de Mirador 3 en local

Ouvrir un terminal et taper les commandes suivantes l'une après l'autre :

```
$ git clone https://github.com/ProjectMirador/mirador.git
$ cd mirador
$ npm install
$ npm start
```

Ouvrir votre navigateur à l'adresse [http://127.0.0.1:4444](http://127.0.0.1:4444/)

#### Instance Mirador de secours !

Instance Mirador 3 sur Biblissima (Mirador vide par défaut) : https://iiif.biblissima.fr/mirador3/?theme=light

*Astuce* : charger directement une ressource IIIF via l'URL :

- un Manifeste :
	- `https://iiif.biblissima.fr/mirador3/?iiif-content={URL_MANIFESTE_IIIF}`
	- [Exemple](https://iiif.biblissima.fr/mirador3/?iiif-content=https://media.nga.gov/public/manifests/nga_highlights.json&theme=light) (National Gallery of Art Collection Highlights)
- une Collection : 
	- `https://iiif.biblissima.fr/mirador3/?iiif-content={URL_COLLECTION_IIIF}`
	- [Exemple](https://iiif.biblissima.fr/mirador3/?theme=light&iiif-content=https://portail.biblissima.fr/iiif/collection/ark:/43093/coldata5151005ea5833e5a05e2639cbb210946cb7e0609) (collection de livres numérisés de la Bibliothèque de l'abbaye Saint-Benoît de Fleury à Saint-Benoît-sur-Loire)

### Étapes de l'exercice

1. **Importer au moins 2 ou 3 Manifests** de votre choix parmi ceux sélectionnés lors de l'exercice précédent. A défaut, piocher dans la liste "Exemples d'URL de Manifestes IIIF" ci-dessus
3. **Configurer un environnement multi-fenêtres :**
  - expérimenter les deux types d'espaces d'espace de travail : "Elastique" et "Mosaïque"
  - explorer les différents panneaux disponibles (informations, index, droits) et options de fenêtre (modes d'affichage)
4. **Modifier les réglages d'une image** (luminosité, contraste, saturation, rotation etc.)
5. **Télécharger une image entière et un détail au sein d'une image** (région zoomée), en cliquant sur l'icône en forme de trois petits points verticaux au niveau d'une fenêtre
6. **Importer d'autres ressources IIIF** dans votre espace de travail à partir des sites donnés en exemple (cf. *"Liste d'entrepôts IIIF"*) :
  - importer via l'URL d'un Manifest  : copier l'URL et la coller dans le champ `Ajouter une ressource` dans Mirador
  - importer par glisser-déposer ("drag and drop") :
    - d'une image de votre ordinateur (glisser l'image dans l'interface de Mirador)
    - d'un logo IIIF depuis l'un des sites suivants : Getty, NGA, Princeton Art Museum, Harvard Art Museums, Yale Center for British Art
7. **Importer/exporter une session Mirador** :
  - dans la barre de menu principal (à gauche), cliquer sur l'icône avec les trois petits points horizontaux
  - cliquer sur `Exporter l'espace de travail` puis `Copier`
  - recharger la page, ou bien ouvrir un Mirador vide dans un nouvel onglet ou un autre navigateur
  - cliquer sur `Importer un espace de travail` puis `Coller` et `Importer`
	

------

## Exercice 5 : Annoter un objet avec SimpleAnnotationServer (SAS)

L'oeuvre utilisée dans cet exercice est la suivante : *Picture Gallery with Views of Modern Rome* (1757), Giovanni Paolo Pannini (1691–1765). Museum of Fine Arts, Boston. https://collections.mfa.org/objects/34215 (Consulté le 11/11/2020).

Ressources Wikimedia sur ce tableau :

- Commons : https://commons.wikimedia.org/wiki/File:Giovanni_Paolo_Pannini_-_Picture_Gallery_with_Views_of_Modern_Rome_-_Google_Art_Project.jpg
- Wikidata : https://www.wikidata.org/wiki/Q28796135
- IIIF Manifest : https://wd-image-positions.toolforge.org/iiif/Q28796135/P18/manifest.json

Cet exemple est inspiré de la démo réalisée à partir de l'oeuvre *Galerie de vues de la Rome antique* (Giovanni Paolo Panini, Musée du Louvre) sur Wikimedia Commons :

- Wikidata : http://www.wikidata.org/entity/Q14619165 => voir l'utilisation de la propriété `depicts` (P180) conjointement avec le qualifieur `relative position within image` (P2677) : ces données sont utilisées pour les annotations IIIF.
- Mirador sur Toolforge, avec les annotations IIIF visibles sur l'image : https://mirador.toolforge.org/?manifest=https://wd-image-positions.toolforge.org/iiif/Q14619165/P18/manifest.json (Manifeste IIIF : https://wd-image-positions.toolforge.org/iiif/Q14619165/P18/manifest.json)

### Démo introductive

Un autre exemple d'exploitation dans une interface dédiée des annotations IIIF créées via Mirador et stockées dans SAS :

- *Ovide moralisé ou La Bible des poètes en images. Comparaison de deux cycles iconographiques avec IIIF et Mirador*. Démos Biblissima. https://demos.biblissima.fr/ovide-moralise/

### Étapes de l'exercice

1. **Ouvrir l'interface d'administration de SAS :** https://demos-dev.biblissima.fr/simpleAnnotationStore/index.html

	```
	- URL Manifeste source : https://wd-image-positions.toolforge.org/iiif/Q28796135/P18/manifest.json
	- IIIF Search API endpoint : https://demos-dev.biblissima.fr/simpleAnnotationStore/search-api/P18/search
	- Manifeste dérivé : https://api.npoint.io/4b814fdc63a68e61da04
	```

2. **Ouvrir un objet à annoter :**
  - cliquer sur `View annotations` dans le menu supérieur
  - La page liste les Manifestes qui ont été importés et indexés dans SAS : cliquer sur l'entrée `Picture Gallery with Views of Modern Rome` 
  - ouvrir le lien `Annotate` dans un nouvel onglet : l'objet devrait s'ouvrir dans Mirador

3. **Annoter l'image dans Mirador :**

  - cliquer sur l'icône en forme de bulles en haut à gauche
  - sélectionner une forme de tracé (rectangle, ovale, tracé libre, polygone, marqueur)
  - délimiter la zone (ou le point) de l'image à annoter ; une fenêtre devrait apparaître au-dessus de l'image
  - saisir votre annotation dans l'éditeur (un formatage html de base est possible) ; un champ "Tags" est aussi disponible
  - cliquer sur `Enregistrer` pour sauvegarder l'annotation : celle-ci est désormais stockée de manière persistente dans SAS (backend utilisé : Jena)

4. **Voir dans le back-office le détail des annotations créées  :**

  - cliquer sur `View annotations` dans le menu supérieur, puis sur le lien `Picture Gallery with Views of Modern Rome`
  - cliquer sur `Download annotations`, puis sur le lien `Picture Gallery with Views of Modern Rome - n annotations` : un document JSON s'ouvre, il contient la liste des annotations qui ont été saisies (ce document JSON est une `AnnotationList` conforme à l'[API Presentation 2.1](https://iiif.io/api/presentation/2.1/))

5. **Visualiser dans Mirador les annotations** créées par les autres participants :

	- Retourner à la page `View annotations` > `Picture Gallery with Views of Modern Rome` : https://demos-dev.biblissima.fr/simpleAnnotationStore/manifest.xhtml?manifest=P18
	- Ouvrir Mirador en cliquant sur `Annotate` : https://demos-dev.biblissima.fr/simpleAnnotationStore/index.html?iiif-content=https://wd-image-positions.toolforge.org/iiif/Q28796135/P18/manifest.json.
	- Afficher toutes les annotations créées (icône en forme de bulles).

6. **Activer et tester la recherche sur ces annotations** (API *Content Search* de IIIF) :

	- Retourner à la page `View annotations` > `Picture Gallery with Views of Modern Rome` : https://demos-dev.biblissima.fr/simpleAnnotationStore/manifest.xhtml?manifest=P18
	- Enregistrer le Manifeste IIIF source sur votre ordinateur (clic-droit "Copier l'adresse du lien") : https://wd-image-positions.toolforge.org/iiif/Q28796135/P18/manifest.json
	- Ouvrir le fichier dans votre éditeur favori
	- Sur la page `Picture Gallery with Views of Modern Rome` de SAS, copier le bloc dans la section `IIIF Search Service` (dupliqué ci-dessous) :

	```
	"service": {
	    "profile": "http://iiif.io/api/search/0/search",
	    "@id": "https://demos-dev.biblissima.fr/simpleAnnotationStore/search-api/P18/search",
	    "@context": "http://iiif.io/api/search/0/context.json"
	},
	```

	- Coller ce morceau de JSON dans le Manifeste que vous avez téléchargé à l'étape précédente : l'insérer juste avant ou après le champ `label` par exemple.

	- Copier la totalité du contenu JSON du fichier (Ctrl+A, Ctrl+C)

	- Ouvrir le site https://www.npoint.io, puis coller le JSON dans le champ situé au centre de la page (après avoir supprimé son contenu). Cliquer ensuite sur `Create JSON Bin`.

	- Une fois le JSON importé, cliquer sur le bouton `Share` en haut à droite : dans la fenêtre qui s'ouvre ensuite, copier le premier lien (en dessous du paragraphe `Access this bin via the API at:`).

	- Cette URL pointe désormais vers notre Manifest modifié, que l'on va pouvoir tester sur divers outils de visualisation :

		- Mirador 2 : https://demos-dev.biblissima.fr/simpleAnnotationStore/
		- Mirador 3 : [https://iiif.biblissima.fr/mirador3/?iiif-content=](https://iiif.biblissima.fr/mirador3/?iiif-content=){URL_Manifeste}
		- Universal Viewer : https://uv-v3.netlify.app/#?c=&m=&s=&cv=&manifest={URL_Manifeste}

		

------

## Exercice 6 : créer/éditer un Manifeste avec le Manifest Editor

Le IIIF Manifest Editor est un éditeur de Manifestes développées par Bodleian Libraries (Oxford) et *text & bytes LLC*.

### Exemple

L'exemple donné est une sélection d'images représentant le *Groupe du Laocoon* (Musée Pio-Clementino, Vatican), issues de différentes collections (NGA, INHA, Bibliothèque Vaticane, Smithsonian, Bibliotheca Hertziana), et de différents types (manuscrit enluminé, estampe, sculpture, peinture, dessin, gemme) :

  - Ouvrir dans Mirador : https://iiif.biblissima.fr/mirador3/?iiif-content=https://jsonstorage.net/api/items/7ba0b03e-f171-44ef-a58e-2992145441db
  - Manifeste IIIF : https://jsonstorage.net/api/items/7ba0b03e-f171-44ef-a58e-2992145441db

### Étapes de l'exercice

1. **Choisir 2 ou 3 Manifestes**, en piochant dans la liste "Exemples d'URL de Manifestes IIIF" ci-dessus, ou en parcourant les sites compatibles IIIF donnés en exemple

2. **Ouvrir le *Manifest Editor*** : https://digital.bodleian.ox.ac.uk/manifest-editor

3. **Créer un nouveau Manifeste et importer des images :**

	- Cliquer sur `New Manifest`, puis dans le panneau à droite aller sur `Manifest Actions` > `Import Canvases` 
	- Cliquer sur le bouton `Open Sequence`, copier-coller une URL de Manifest dans le champ "Enter a remote Manifest URL", puis cliquer sur `Open`. Une vue zoomable de l'objet devrait s'ouvrir dans une fenêtre.
	- Répéter les points suivants pour chacun des Manifestes que vous avez préalablement choisis.

4. **Composer/éditer la séquence de votre Manifeste :**

  - Une fois vos Manifestes chargés dans l'éditeur, vous pouvez glisser-déposer une à une les images de votre choix dans la partie inférieure (dans l'espace horizontal blanc avec l'indication `+ Add Canvas`) :
	  - en survolant la partie inférieure d'une image, un bandeau avec une ou plusieurs vignettes devrait apparaître.
		- glisser-déposer la vignette de votre choix sur la zone `+ Add Canvas`
		- répéter l'opération pour chaque image que vous souhaitez incorporer à votre Manifeste.
  - vous pouvez réordonner la séquence d'images en faisant glisser chaque *Canvas*, vous pouvez aussi dupliquer ou supprimer un *Canvas*

5. **Éditer les métadonnées de votre Manifeste :**

  - Une fois votre sélection faite, cliquer sur `Return to Edit Manifest` dans le panneau de droite
  - Dans ce même panneau latéral, vous pouvez :
	  - éditer les métadonnées associées à votre Manifeste dans la section `Manifest Metadata` : éditer les champs pré-existants du Manifeste d'origine, ou ajouter un nouveau champ en cliquant sur `Add metadata field`
    - éditer les métadonnées associées à chaque Canvas dans la section `Canvas Metadata`

6. **Sauvegarder votre Manifeste :**

  - Dans le panneau latéral, cliquer sur l'icône en forme de roue dentée en haut à droite de l'écran (paramètres). Une fenêtre `Server Endpoint Settings` s'affiche.
  - Cliquer sur le lien `click here to use JsonStorage.net ` dans le paragraphe de texte. Les 2 champs de formulaire situés en dessous se remplissent automatiquement. Cliquer ensuite sur `Save Settings`, puis `Close`.
  - Cliquer sur le bouton `Save Manifest`, à partir de là vous pouvez :
	  - télécharger votre Manifeste (JSON) sur votre ordinateur, pour pouvoir ensuite le publier sur votre propre serveur (`Download manifest`)
  - publier directement votre Manifeste sur le service en ligne *JsonStorage.net* : cela présente l'avantage de le rendre immédiatement accessible en ligne à travers une URL, mais sans garantie de pérennité. Après avoir cliqué sur `Store Manifets on Server`, un message de confirmation apparaît et l'URL de votre Manifeste est indiquée en dessous (sous la forme `https://jsonstorage.net/api/items/abc123...`).

------

## Exercice 7 : générer un Manifeste IIIF simple en local

### Installation et configuration de Biiif

  - Ouvrir un terminal et entrer les commandes suivantes :

```shell
$ git clone https://github.com/edsilv/biiif.git
$ cd biiif
```

  - Ouvrir le dossier `biiif` dans votre éditeur de code.

  - Ouvrir le fichier `package.json` puis éditer le comme indiqué ci-dessous :

	1. Ajouter la ligne `"http-server": "^0.12.3"` dans la partie `devDependencies`. 
		Vous devriez avoir :

		```json
		"devDependencies": {
		    "@types/node": "^11.13.8",
		    "mocha": "4.0.1",
		    "mock-fs": "4.9.0",
		    "typescript": "3.4.5",
		    "http-server": "^0.12.3"
		 }
		```

	2. Ajouter la ligne `"serve": "node_modules/.bin/http-server --cors",` dans la partie `scripts`.
		Vous devriez avoir :

		```json
		"scripts": {
		    "serve": "node_modules/.bin/http-server --cors",
		    "test": "tsc && mocha",
		    "testbuild": "node --nolazy --inspect-brk=5858 -e \"require('./index').build('collection', 'http://test.com/collection')\""
		},
		```

  - Ensuite, revenir dans le terminal puis entrer la commande suivante :


```shell
$ npm install
```

  - Ouvrir une nouvelle fenêtre ou un nouvel onglet de votre terminal, puis entrer :

```shell
$ npm run serve
```

Un mini serveur web devrait maintenant tourner à l'adresse http://127.0.0.1:8080.

  - Télécharger le dossier d'exemple à cette adresse : https://partages.campus-condorcet.fr/f/ac6c6c9a2b96423d8390/?dl=1
    - dézipper l'archive dans votre répertoire `biiif`
	  - vous devriez avoir à la racine un nouveau répertoire nommé `collection` 
  - Revenir ensuite dans le premier terminal ouvert dans le dossier `biiif`, puis taper la commande :

```shell
$ node_modules/.bin/biiif collection -u http://localhost:8080/collection -g
```

  - Les fichiers d'exemple suivants devraient désormais être accessibles via votre mini serveur web :
	  - URL de la Collection IIIF : http://localhost:8080/collection/index.json
	  - URL du Manifest IIIF : http://localhost:8080/collection/gallica_ark_12148_bpt6k1526005v/index.json

### Principes de fonctionnement de Biiif

Observons ensemble la structure du répertoire `collection` et tâchons de comprendre la convention de nommage des répertoires et fichiers supportée par Biiif :

  - Lire les explications données ici : https://github.com/edsilv/biiif/#conventions
  - Voir un exemple d'arborescence : https://github.com/edsilv/biiif/#examples

Le répertoire `collection` représente une **Collection IIIF**, intitulée  ici"Ma collection d'objets IIIF" (cf. fichier `info.yml`).

Le sous-répertoire `gallica_ark_12148_bpt6k1526005v` représente quant à lui un **Manifest IIIF** intitulée "BnF, département Réserve des livres rares, RES M-Y2-227" (cf. fichier `info.yml`).

Les sous-répertoires, dont le nom commence par un underscore (ex. `_f19`), correspondent aux différents **Canvas**, c'est-à-dire aux différentes pages ou vues de l'objet représenté par le Manifest en question (ici il s'agit de quelques pages d'un livre imprimé conservé à la BnF et numérisé sur Gallica).

#### Nota bene

La commande qui permet de générer la Collection dans son ensemble (Collection + Manifestes IIIF enfants) est :

```bash
$ node_modules/.bin/biiif collection -u http://localhost:8080/collection -g
```

- le 1er paramètre désigne le répertoire cible, ici `collection`
- le 2e paramètre `-u` désigne l'URL de publication de la Collection IIIF (par laquelle on va accéder au document JSON de la Collection)
- le 3e paramètre `-g` indique que l'on va générer des vignettes `thumb.jpg` pour toutes les images présentes dans les différents dossiers

### Exercice

Le but de l'exercice consiste à ajouter un nouveau Manifest à notre Collection. Il s'agit donc de créer un nouveau répertoire à l'intérieur de notre dossier `collection` organisé sur le même modèle que l'exemple vu ci-dessus (`gallica_ark_12148_bpt6k1526005v`).

  - Télécharger l'archive suivante sur puis dézipper-la sur votre ordinateur : https://partages.campus-condorcet.fr/f/2a9fd9527db941b3b5a7/?dl=1
	  - le dossier `laocoon` contient 4 images JPG, chacune accompagnée d'un petit fichier texte avec quelques métadonnées basiques
  - Déplacer ce répertoire `laocoon` dans le répertoire `biiif/collection`
  - Puis l'organiser selon les conventions de Biiif vues ci-dessus, afin de pouvoir générer un nouveau Manifest pour nos 4 images du Laocoon.
	  - créer des fichiers `info.yml` pour renseigner quelques métadonnées de base, au niveau du Manifest et au niveau de chaque image
  - Une fois cela fait, tester la génération du Manifest avec la commande vue précémment (`node_modules/.bin/biiif collection -u http://localhost:8080/collection -g`)
  - Puis ouvrir la Collection ou le Manifest individuel dans votre Mirador local :
	  - URL de la Collection IIIF : http://localhost:8080/collection/index.json


------

## Bonus

### Bonus 1 : Créer une mini-exposition virtuelle avec Exhibit.co

**Exemple préparé pour l'atelier** : "exhibit" créé à partir de la série de tableaux *The Voyage of Life*, par Thomas Cole (National Gallery of Art, Washington D.C.). Source : [nga.gov](https://www.nga.gov/collection-search-result.html?artist=Cole%2C%20Thomas&title=voyage%20of%20life&artobj_imagesonly=Images_online). 

Voir l'exposition : https://exhibit.so/exhibits/t153UkCxJXovu1jeuLV3

Autres exemples : https://exhibit.so/#showcase

### Bonus 2 : Créer une "curation" de contenus avec le IIIF Curation Viewer

**Exemple préparé pour l'atelier** : "curation" de ressources IIIF de monnaies grecques de Panticapée (Royaume du Bosphore Cimmérien). Sources : Harvard Art Museums, Gallica.

Voir la démo : http://codh.rois.ac.jp/software/iiif-curation-viewer/demo/?curation=https://mp.ex.nii.ac.jp/api/curation/json/962dc427-6241-4200-82ad-69a0821b573c&lang=en

Curation (JSON) : https://mp.ex.nii.ac.jp/api/curation/json/962dc427-6241-4200-82ad-69a0821b573c 

