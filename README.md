# Matériel associé à l'article « La recherche reproductible : une communication scientifique explicite. »

## Une version « longue » de la section « Une brève histoire de la recherche reproductible et de ses outils »

La première tentative concrète de mise en œuvre d'« approches reproductibles », _au niveau des publications_, est apparue en économie au début des années quatre-vingt (Dewald et col., 1986). Le _Journal of Money, Credit and Banking_ a alors adopté une politique éditoriale demandant aux auteurs les programmes et données utilisés dans leurs articles « empiriques », ainsi que la mise à disposition de ceux-ci à tout chercheur sur simple demande. Cette mise à disposition s'est néanmoins faite de manière informelle par dépôt des codes et données dans un répertoire (d'ordinateur). Les approches reproductibles proposées par la suite peuvent être vues, en quelque sorte, comme le détournement (ou l'adaptation) d'outils créés dans un but assez différent. Ces outils sont ceux forgés par les informaticiens pour développer des logiciels fiables, bien documentés, faciles à faire évoluer et modifiables par d'autres personnes que leur auteur. Le premier outil est un [moteur de production](http://fr.wikipedia.org/wiki/Moteur_de_production) dont l'archétype dans le monde Unix est [`make`](http://fr.wikipedia.org/wiki/Make) : un logiciel, programmé par un [langage de script](https://fr.wikipedia.org/wiki/Langage_de_script), qui permet d'automatiser et d'ordonnancer la construction / compilation de logiciels « complexes » à partir de fichiers sources. Il est assez simple de remplacer le produit final, un logiciel complexe, par un article au format PDF (via LaTeX) et les compilations intermédiaires par des appels à des logiciels d'analyse de données en mode _batch_ (non-intéractif) -- le résultat de tels appels étant par exemple la génération des figures de l'article. C'est l'idée utilisée par les géophysiciens (Claerbout et Karrenbach, 1992) du _Stanford Exploration Project_ -- Le logiciel de recherche reproductible de ce groupe, [Madagscar](http://www.ahay.org/wiki/Main_Page), est maintenant basé sur le moteur de production [`scons`](http://www.scons.org/) (Fomel et Hennenfent, 2007). Au début des années 2000, des statisticiens, Friedrich Leisch et Tony Rossini (Leisch, 2002, 2002b, 2003; Rossini et Leisch, 2003), se sont inspirés de la « [programmation lettrée](http://fr.wikipedia.org/wiki/Programmation_lettr%C3%A9e) », proposée par Don Knuth (1984) lorsqu'il développait TeX. Ils ont ainsi créé la fonction `Sweave` du logiciel [`R`](http://www.r-project.org/) qui traite un fichier au format texte (ASCII ou UTF-8) où le texte d'un article, écrit avec LaTeX, est mélangé aux lignes de code `R` qui génèrent les figures et le tables de l'article^[`Sweave` recopie la partie texte du fichier d'entrée, telle quelle, dans un nouveau fichier LaTeX, exécute les lignes de codes puis inclut leurs résultats (figures et tables) dans le nouveau fichier.]. Si les moteurs de productions ou la programmation lettrée sont suffisants pour mettre en œuvre une recherche reproductible, ils sont insatisfaisants sous deux aspects : ils sont difficiles à utiliser « au quotidien » -- peu de gens tiennent leur cahier de laboratoire en LaTeX -- ; la recherche moderne se fait de plus en plus en collaboration ce qui nécessite des outils permettant _aux membres d'un groupe_ de pouvoir modifier, de préférence indépendemment, un ensemble de fichiers (données qui s'ajoutent à une étude, codes développés spécifiquement, textes d'articles, etc). Le premier « point faible » est éliminé en adoptant un [langage de balisage léger](http://fr.wikipedia.org/wiki/Langage_de_balisage_l%C3%A9ger) comme [`Markdown`](http://daringfireball.net/projects/markdown/), [`reStructuredText`](http://docutils.sourceforge.net/rst.html) ou [`Org mode`](http://orgmode.org/fr/index.html) pour n'en citer que quelques uns. Avec le logiciel [pandoc](http://johnmacfarlane.net/pandoc/), développé par le philosophe John MacFarlane, il est possible de passer quasi instantanément de l'un à l'autre et, grâce à l'extension [pandoc de Markdown](http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown), un débutant avec une heure de pratique peut générer un fichier LaTeX qui ferait envie à un expert^[Les utilisateurs de `R` peuvent combiner leurs lignes de code avec Markdown grâce au paquet [R Markdown](http://rmarkdown.rstudio.com/), qui remplace avantageusement `Sweave`, voir plus loin ; les utilisateurs de `Python` peuvent faire de même avec [`Pweave`](http://mpastell.com/pweave/).]. Le second point faible est éliminé en adoptant un logiciel de [gestion de version](http://fr.wikipedia.org/wiki/Gestion_de_versions) comme [`Git`](http://git-scm.com/), [`Mercurial`](http://mercurial.selenic.com/) ou [`Bazaar`](http://bazaar.canonical.com/en/) (Hinsen et col., 2009). Ces logiciels sauvent de façon incrémentielle les différences entre deux versions successives d'un même fichier -- on peut donc toujours revenir à n'importe quelle version antérieure d'un fichier -- et permettent de gérer efficacement les éventuels conflits créés par deux personnes modifiant indépendemment le même fichier. Pour des études impliquant de « fortes doses » de calculs scientifiques, comme des calculs de structures de protéines ou des simulations de réseaux neuronaux (Davison et col., 2014), la simple sauvegarde des codes sources et des paramètres de calcul / simulation s'avère souvent insuffisante ; il faut aller plus loin et enregistrer de façon précise les propriétés de l'environnement de calcul (versions des logiciels, compilateurs utilisés, propriétés physiques du ou des ordinateurs, etc.). Comme il est clairement impossible (ou terriblement chronophage !) de noter « à la main » l'ensemble de ces informations, des solutions logiciels ont été développées, allant de la capture automatique des données sur l'environnement comme le fait _Sumatra_ (Davison et col., 2014) à une [virtualisation](http://fr.wikipedia.org/wiki/Virtualisation) complète (Howe, 2014). Des solutions intermédiaires passant par l'usage de [machines virtuelles](http://fr.wikipedia.org/wiki/Machine_virtuelle), comme la machine virtuelle Java, ont été proposées accompagnées de démonstrations concrètes (Hinsen, 2011, 2014).

Il ne faut cependant pas penser qu'il est nécessaire d'être expert « de la ligne de commande » pour faire de la recherche reproductible. Il existe en effet plusieurs « moteurs de flux de travaux » (_workflows_) destinés aux chercheurs, comme : [`Taverna`](http://www.taverna.org.uk), [`VisTrails`](http://www.vistrails.org/) (Freire et col., 2014) et [`Galaxy`](http://galaxyproject.org). Ces logiciels permettent de créer, visualiser et exécuter une suite de tâches à partir d'une bibliothèque de composants ; l'ensemble étant géré par _une interface graphique_. Chaque exécution du flux de travaux est enregistrée, ce qui permet de revenir facilement à une analyse antérieure, de la relancer, ou de la modifier. Il est aussi possible d'intégrer des moteurs de flux de travaux avec les outils de programmation lettrée, en incluant, par exemple, un résultat, obtenu avec VisTrails dans un document LaTeX ; résultat associé à un lien hypertexte pointant vers un enregistrement du processus, hébergé sur la toile (Koop et col., 2011).

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

Pour travailler avec ce fichier sur votre propre ordinateur, vous devez installer [Python](http://www.python.org/) et [IPython](http://ipython.org/), ainsi que [NumPy](http://www.numpy.org/), [Pandas](http://pandas.pydata.org/)
et [matplotlib](http://matplotlib.org/) car notre exemple utilise ces trois libraries. Vous pouvez vous faciliter la vie en intallant [Anaconda](https://store.continuum.io/cshop/anaconda/), une distribution Python faite spécialement pour le calcul scientifique, qui contient tous les éléments dans la liste ci-dessus et encore bien plus.

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
	+ [RCS](http://www.gnu.org/software/rcs/) le plus ancien (ou presque) logiciel de ce type, simple a utiliser mais limité aux petits projets (un seul fichier) ; les logiciels qui suivent sont dicutés plus haut ;
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

## Les références

- Jon Claerbout and Martin Karrenbach (1992) [Electronic Documents Give Reproducible Research a New Meaning](http://sepwww.stanford.edu/doku.php?id=sep:research:reproducible:seg92). _Proceedings of the 62nd Annual Meeting of the Society of Exploration Geophysics_, 601-604. 
- Andrew P. Davison, Michele Mattioni, Dmitry Samarkanov and Bartosz Telenczuk (2014) [Sumatra: a toolkit for reproducible research](https://osf.io/rc5jf/) in _Implementing Reproducible Research_ édité par Victoria Stodden, Friedrich Leisch et Roger D. Peng, CRC Press.
- William G. Dewald, Jerry G. Thursby and Richard G. Anderson, 1986, Replication in Empirical Economics: The Journal of Money, Credit, and Banking Project. _American Economic Review_ __76(4)__, 587-603.
- Sergey Fomel and Gilles Hennenfent (2007) [Reproducible computational experiments using SCons](http://www.reproducibility.org/RSF/book/rsf/scons/paper_html/). _Proc. IEEE Int'l Conf. Acoustics, Speech and Signal Processing_ __4__, 1257-1260.
- Juliana Freire, David Koop, and Fernando Chirigati and Cláudio T Silva (2014) [Reproducibility Using VisTrails](https://osf.io/c3kv6/) in _Implementing Reproducible Research_ édité par Victoria Stodden, Friedrich Leisch et Roger D. Peng, CRC Press.
- Konrad Hinsen, Konstantin Laufer and George K. Thiruvathukal (2009) [Essential Tools: Version Control Systems](http://works.bepress.com/laufer/21/). _Computing in Science and Engineering_ __11(6)__, 84-91.
- Konrad Hinsen (2011) A data and code model for reproducible research and executable papers. _Procedia Computer Science_ __4__, 579-588.
- Konrad Hinsen (2014) [Platforms for publishing and archiving computer-aided research](http://dx.doi.org/10.12688/f1000research.5773.1). _F1000Research_ __3__, 289.
- Bill Howe (2014) [Reproducibility, Virtual Appliances, and Cloud Computing](https://osf.io/xrbqv/) in _Implementing Reproducible Research_ édité par Victoria Stodden, Friedrich Leisch et Roger D. Peng, CRC Press.
- Donald E. Knuth (1984) [Literate Programming](http://www.literateprogramming.com/knuthweb.pdf). _The Computer Journal_ __27(2)__, 97-111.
- David Koop, Emanuele Santos, Phillip Mates, Huy T. Vo, Philippe Bonnet, Bela Bauer, Brigitte Surer, Matthias Troyer, Dean N. Williams, Joel E. Tohline, Juliana Freire and Claudio T. Silva (2011) [A Provenance-Based Infrastructure to Support the Life Cycle of Executable Papers](http://www.sciencedirect.com/science/article/pii/S1877050911001268). _Procedia Computer Science_ __4__, 648-657.
- Friedrich Leisch (2002) [Sweave, Part I: Mixing R and LaTeX](http://www.r-project.org/doc/Rnews/Rnews_2002-3.pdf). _R News_ __2(3)__, 28-31.
- Friedrich Leisch (2002b) Sweave: Dynamic Generation of Statistical Reports Using Literate Data Analysis. _Compstat 2002 --- Proceedings in Computational Statistics_, 575-580.
- Friedrich Leisch (2003) [Sweave, Part II: Package Vignettes](http://www.r-project.org/doc/Rnews/Rnews_2003-2.pdf). _R News_ __3(2)__, 21-24.
- Anthony J. Rossini et Friedrich Leisch (2003) Literate statistical practice. _UW Biostatistics Working Paper Series 194_, University of Washington, WA, USA.
