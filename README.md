# Matériel associé à l'article « La recherche reproductible : une communication scientifique explicite. »

## L'exemple et ses déclinaisons

Nous illustrons de façon très élémentaire une courte mise en œuvre concrète de recherche reproductible générant à nouveau un [graphe](http://fr.wikipedia.org/wiki/William_Playfair#mediaviewer/File:Chart_Showing_at_One_View_the_Price_of_the_Quarter_of_Wheat,_and_Wages_of_Labour_by_the_Week,_from_1565_to_1821.png) publié par [William Playfair](http://fr.wikipedia.org/wiki/William_Playfair) dans son livre _Letter on our Agricultural Distresses, Their Causes and Remedies_. Notre tâche est ici de récupérer les données au format `csv` à partir du dépôt GitHub
[Rdatasets](https://github.com/vincentarelbundock/Rdatasets). Après les avoir chargées dans notre logiciel d'analyse, [R](http://www.r-project.org/) ou [Python](https://www.python.org/) pour l'instant, nous vérifions que notre lecture des données s'est déroulée correctement avant de générer la figure.

### `Markdown` et `Pandoc Markdown`
Les trois premières « déclinaisons » que nous présentons emploient l'extension [`Pandoc Markdown`](http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown) du [langage de balisage léger](http://fr.wikipedia.org/wiki/Langage_de_balisage_l%C3%A9ger) [`Markdown`](http://daringfireball.net/projects/markdown/). Un excellent [didacticiel en français](http://enacit1.epfl.ch/markdown-pandoc/) de Jean-Daniel Bonjour permettra à tout lecteur de lire _et d'écrire_ en `Markdown` et `Pandoc Markdown` en une petite heure. Le lecteur pressé pourra toujours ouvrir les fichiers du dépôt se terminant par `.md`, `.Rmd` ou `.mdw` avec son éditeur de texte préféré ; il constatera alors que la lecture de ceux-ci est aisée, même sans « mode d'emploi ».

### Utilisation de `R` et `R Markdown`
Le fichier [`ExemplePlayfair_RMarkdown.Rmd`](https://github.com/khinsen/article-statistique-et-societe/raw/master/ExemplePlayfair_RMarkdown.Rmd) contient le « document actif » utilisable avec le paquet [R Markdown](http://rmarkdown.rstudio.com/) du logiciel `R`. Il y a plusieurs façons de générer le document « final » `ExemplePlayfair_RMarkdown.html`. La plus simple est d'ouvrir ce fichier avec l'éditeur de fichiers de [RStudio](http://www.rstudio.com/) puis de cliquer sur l'icône `knit HTML`. Le lecteur n'utilisant pas `RStudio` pourra lancer `R` comme d'habitude et après avoir installé le paquet [rmarkdown](http://cran.at.r-project.org/web/packages/rmarkdown/index.html) disponible sur le [CRAN](http://cran.at.r-project.org/), taper en ligne de commande les instructions suivantes :

```{r}
library(rmarkdown)
rmarkdown::render("Playfair_RMarkdown.Rmd")
```

pour générer une sortie au format `PDF` il suffit de remplacer la seconde commande par :

```{r}
rmarkdown::render("Playfair_RMarkdown.Rmd","pdf_document")
```

où le deuxième paramètre formel contrôle le format du fichier de sortie qui s'appellera ici `Playfair.pdf`.

### Utilisation du carnet de notes `IPython`
Le fichier [`ExemplePlayfair_IPython.ipynb`](https://github.com/khinsen/article-statistique-et-societe/raw/master/ExemplePlayfair_IPython.ipynb) contient le « document actif » utilisable avec le [« carnet de notes »](http://ipython.org/notebook.html) (_notebook_) [IPython](http://ipython.org/). Ce document n'est pas fait pour être visualisé directement - c'est bien du texte, plus précisement en notation [JSON](http://json.org/), mais c'est plutôt une notation à l'usage d'un ordinateur. Le service gratuit [Notebook Viewer](http://nbviewer.jupyter.org/) l'affiche joliment, ce que vous pouvez vérifier en cliquant [ici](http://nbviewer.jupyter.org/github/khinsen/article-statistique-et-societe/blob/master/ExemplePlayfair_IPython.ipynb) pour voir notre exemple.

Pour travailler avec ce fichier sur votre propre ordinateur, vous devez installer [Python](http://www.python.org/) et [IPython](http://ipython.org/), mais aussi [NumPy](http://www.numpy.org/), [Pandas](http://pandas.pydata.org/)
et [matplotlib](http://matplotlib.org/) parce que notre exemple utilise ces trois libraries. Vous pouvez vous faciliter la vie en intallation [Anaconda](https://store.continuum.io/cshop/anaconda/), une distribution Python faite spécialement pour le calcul scientifique, qui contient tous les éléments dans la liste ci-dessus et encore bien plus.

Enfin, il existe des services "cloud computing" qui permettent de travailler, seul ou en collaboration, avec des carnets de notes de ce type. Par exemple, en cliquant [ici](https://wakari.io/sharing/bundle/khinsen/ExemplePlayfair_IPython) vous accédez à notre exemple par le site [Wakari.io](https://wakari.io/).

### Utilisation du module `Pweave` de `Python`
Le fichier `ExemplePlayfair_Pweave.mdw` contient le « document actif » utilisable avec le module [Pweave](http://mpastell.com/pweave/) de [Python](https://www.python.org/). Le document final `ExemplePlayfair_Pweave.html` est généré en tapant en [interface système](http://fr.wikipedia.org/wiki/Interface_système) (_shell_) et _pas en ligne de commande Python_ les commandes suivantes :

```{.bash}
Pweave -f pandoc ExemplePlayfair_Pweave.mdw
pandoc -s --mathjax ExemplePlayfair_Pweave.md -o ExemplePlayfair_Pweave.html
``````````

Cela suppose évidemment que [pandoc](http://johnmacfarlane.net/pandoc/) est installé sur le système.

### Utilisation d'[`ActivePapers pour Python`](http://www.activepapers.org/python-edition/)
L'approche [ActivePapers](http://www.activepapers.org/) est faite pour des applications bien plus complexes que notre petite exemple. Son point fort est la gestion de grands jeux de données, et la gestion automatique de dépendence entre différentes publications. Néanmoins, nous proposons une [version ActivePapers](https://github.com/khinsen/article-statistique-et-societe/raw/master/ExemplePlayfair.ap) de notre exemple. C'est un fichier [HDF5](http://www.hdfgroup.org/HDF5/), donc un fichier binaire, qu'on ne peut pas simplement afficher à l'écran. On peut inspecter les données à l'intérieur avec [HDFView](http://www.hdfgroup.org/products/java/hdfview/) ou d'autres logiciels qui gèrent le format HDF5.

Pour pleinement exploiter un ActivePaper, il faut [installer le gestionnaire `aptool`](http://www.activepapers.org/python-edition/installation.html). Téléchargez [`ExemplePlayfair.ap`](https://github.com/khinsen/article-statistique-et-societe/raw/master/ExemplePlayfair.ap), puis dans le repertoire ou vous avez copié ce fichier, entrez les commandes suivantes:

 - `aptool ls -l` pour voir le contenu
 - `aptool checkout documentation` pour extraire une description et les résultats des calculs, notamment le graphe
 - `aptool checkout code` pour extraire les trois scripts Python

Pour approfondir, suivez le [tutoriel](http://www.activepapers.org/python-edition/tutorial.html).

## Quelques liens utiles

Nous ne donnons ici que des liens vers des logiciels « libres » :

* [moteurs de production](http://fr.wikipedia.org/wiki/Moteur_de_production) :
	+ [GNU make](<https://www.gnu.org/software/make/>), le moteur le plus employé ;
	+ [SCons](<http://www.scons.org/>), une version « modernisée » écrite en [Python](https://www.python.org/) et utilisée par le projet [Madagascar](http://www.ahay.org/wiki/Main_Page).
* Quelques outils de [programmation lettrée](http://fr.wikipedia.org/wiki/Programmation_lettr%C3%A9e) :
	+ [Noweb](<http://www.cs.tufts.edu/~nr/noweb/>), l'outil le plus courant, neutre vis-à-vis du langage de programmation utilisé ;
	+ [pyWeb](<http://pywebtool.sourceforge.net/>), une version écrite en [Python](https://www.python.org/) ;
	+ [Org mode](<http://orgmode.org/fr/index.html>), un mode de l'éditeur [emacs](http://www.gnu.org/software/emacs/emacs.html) ;
* [langages de balisage léger](http://fr.wikipedia.org/wiki/Langage_de_balisage_l%C3%A9ger) :
	+ [Markdown](<http://daringfireball.net/projects/markdown/>), le langage utilisé pour rédiger cet article avec son extension [pandoc de Markdown](<http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown>) ;
	+ [reStructuredText](<http://docutils.sourceforge.net/rst.html>), le langage de documentation Python ;
	+ [Org mode](<http://orgmode.org/fr/index.html>), voir ci-dessus ;
* Logiciels de [gestion de version](http://fr.wikipedia.org/wiki/Gestion_de_versions) :
	+ [RCS](http://www.gnu.org/software/rcs/) le plus ancien (ou presque) logiciel de ce type, simple a utiliser mais limité aux petits projets (un seul fichier) ; les logiciels qui suivent sont dicutés dans l'article ;
	+ [Git](<http://git-scm.com/>) ;
	+ [Mercurial](<http://mercurial.selenic.com/>) ;
	+ [Bazaar](<http://bazaar.canonical.com/en/>) ;
* Dépôts sous gestion de version :
	+ [GitHub](<https://github.com/>) ;
	+ [Bitbucket](<https://bitbucket.org/>) ;
	+ [GitLab](<https://about.gitlab.com/>) ;
* Dépôts de données, articles, etc., orientés vers la recherche reproductible :
	+ [RunMyCode](<http://www.runmycode.org>) ; 
	+ [Zenodo](<https://zenodo.org>) ;
	+ L'[Open Science Framework](<https://osf.io>) ;
	+ [Figshare](<http://figshare.com>) ;
	+ [DRYAD](<http://datadryad.org/>) ;
	+ [Research Compendia](<http://researchcompendia.org>) ; 
    + [Exec&Share](<http://www.execandshare.org>).

