# Matériel associé à l'article « La recherche reproductible : une communication scientifique explicite. »

## L'exemple et ses déclinaisons

Nous illustrons de façon très élémentaire une courte mise en œuvre concrète de recherche reproductible en régénérant un [graphe](http://fr.wikipedia.org/wiki/William_Playfair#mediaviewer/File:Chart_Showing_at_One_View_the_Price_of_the_Quarter_of_Wheat,_and_Wages_of_Labour_by_the_Week,_from_1565_to_1821.png) publié par [William Playfair](http://fr.wikipedia.org/wiki/William_Playfair) dans son livre « _Letter on our Agricultural Distresses, Their Causes and Remedies._ ». Notre tâche consiste en récupérer les données au format `csv` à partir du dépôt GitHub
[Rdatasets](https://github.com/vincentarelbundock/Rdatasets). Après les avoir chargées dans notre logiciel d'analyse, [R](http://www.r-project.org/) ou [Python](https://www.python.org/) pour l'instant, nous vérifions que notre lecture des données s'est déroulée correctement avant de générer la figure.

### `Markdown` et `Pandoc Markdown`
Les trois premières « déclinaisons » que nous présentons emploient l'extension [`Pandoc Markdown`](http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown) du [langage de balisage léger](http://fr.wikipedia.org/wiki/Langage_de_balisage_l%C3%A9ger) [`Markdown`](http://daringfireball.net/projects/markdown/). Un excellent [didacticiel en français](http://enacit1.epfl.ch/markdown-pandoc/) de Jean-Daniel Bonjour permettra à tout lecteur de lire _et d'écrire_ en `Markdown` et `Pandoc Markdown` en une petite heure. Le lecteur pressé pourra toujours ouvrir les fichiers du dépôt se terminant par `.md`, `.Rmd` ou `.mdw` avec son éditeur de texte préféré ; il constatera alors que la lecture de ceux-ci est aisée, même sans « mode d'emploi ».

### Utilisation de `R` et `R Markdown`
Le fichier `ExemplePlayfair_RMarkdown.Rmd` contient le « document actif » utlisable avec le paquet [R Markdown](http://rmarkdown.rstudio.com/) du logiciel `R`. Il y a plusieurs façons de générer le document « final » `ExemplePlayfair_RMarkdown.html`. La plus simple est d'ouvrir ce fichier avec l'éditeur de fichiers de [RStudio](http://www.rstudio.com/) puis de cliquer sur l'icône `knit HTML`. Le lecteur n'utilisant par `RStudio` pourra lancer `R` comme d'habitude et après avoir installé le paquet [rmarkdown](http://cran.at.r-project.org/web/packages/rmarkdown/index.html) disponible sur le [CRAN](http://cran.at.r-project.org/), taper en ligne de commande les instructions suivantes :

```{r}
library(rmarkdown)
rmarkdown::render("Playfair_RMarkdown.Rmd")
```

pour générer une sortie au format `PDF` il suffit de remplacer la seconde commande par :

```{r}
rmarkdown::render("Playfair.Rmd","pdf_document")
```

### Utilisation du carnet de notes `IPython`
Le fichier `ExemplePlayfair_IPython.ipynb` contient le « document actif » utlisable avec le [« carnet de notes »](http://ipython.org/notebook.html) (_notebook_) [IPython](http://ipython.org/).

### Utilisation du module `Pweave` de `Python`
Le fichier `ExemplePlayfair_Pweave.mdw` contient le « document actif » utlisable avec le module [Pweave](http://mpastell.com/pweave/) de [Python](https://www.python.org/). Le document final `ExemplePlayfair_Pweave.html` est générer en tapant en [interface système](http://fr.wikipedia.org/wiki/Interface_système) (_shell_) et _pas en ligne de commande Python_ les commandes suivantes :

```{.bash}
Pweave -f pandoc ExemplePlayfair_Pweave.mdw
pandoc -s --mathjax ExemplePlayfair_Pweave.md -o ExemplePlayfair_Pweave.html
``````````

Cela suppose évidemment que [pandoc](http://johnmacfarlane.net/pandoc/) est installé sur le système.

## Quelques liens utiles

Nous ne donnont ici que des liens vers des logiciels « libres » :

* [moteurs de production](http://fr.wikipedia.org/wiki/Moteur_de_production) :
	+ [GNU make](<https://www.gnu.org/software/make/>), le moteur le plus employé ;
	+ [SCons](<http://www.scons.org/>), une version « modernisée » écrite en [Python](https://www.python.org/) et utilisée par le projet [Madagscar](http://www.ahay.org/wiki/Main_Page).
* Quelques outils de [programmtion lettrée](http://fr.wikipedia.org/wiki/Programmation_lettr%C3%A9e) :
	+ [Noweb](<http://www.cs.tufts.edu/~nr/noweb/>), l'outil le plus courant, neutre vis-à-vis du langage de programmation utilisé, écrit par Norman Ramsay ;
	+ [pyWeb](<http://pywebtool.sourceforge.net/>), une version écrite en [Python](https://www.python.org/) ;
	+ [Org mode](<http://orgmode.org/fr/index.html>), un mode de l'éditeur [emacs](http://www.gnu.org/software/emacs/emacs.html) ;
* [langages de balisage léger](http://fr.wikipedia.org/wiki/Langage_de_balisage_l%C3%A9ger) :
	+ [Markdown](<http://daringfireball.net/projects/markdown/>), le langage utilisé pour rédiger cet article avec son extension [pandoc de Markdown](<http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown>) ;
	+ [reStructuredText](<http://docutils.sourceforge.net/rst.html>), le langage de documentation Python ;
	+ [Org mode](<http://orgmode.org/fr/index.html>), voir ci-dessus ;
* Logiciels de [gestion de version](http://fr.wikipedia.org/wiki/Gestion_de_versions) :
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

