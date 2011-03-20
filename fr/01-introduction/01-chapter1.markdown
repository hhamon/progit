# Premiers Pas #

Ce chapitre aborde les concepts de base pour bien démarrer avec Git. Nous
commencerons par expliquer les bases de la gestion de version, puis nous
parlerons de l'installation de Git sur votre système et enfin nous étudierons
comment paramétrer Git afin de l'utiliser. À la fin de ce chapitre vous devriez
en savoir assez pour comprendre ce qu'est Git, pourquoi vous devriez l'utiliser
et vous devriez enfin avoir une configuration prête à l'emploi pour bien
démarrer.

## À Propos du Contrôle De Version ##

Qu'est-ce que le contrôle de version et pourquoi devriez-vous vous en soucier ?
Un gestionnaire de version est un système qui enregistre l'évolution d'un
fichier ou d'un ensemble de fichiers au cours du temps de manière à ce qu'on
puisse récupérer une version antérieure d'un fichier à tout moment. Dans cet
ouvrage, nous prendrons pour exemple des fichiers de code source de logiciel
comme fichiers sous contrôle de version, bien qu'en réalité nous puissions
l'utiliser avec presque n'importe quel fichier d'ordinateur.

Si vous êtes un dessinateur ou un développeur web, et que vous désirez conserver
toutes les versions d'une image ou d'une mise en page (ce que vous souhaiteriez
assurément), un système de gestion de version (VCS en anglais pour Version
Control System) est un outil qu'il convient d'utiliser. Il vous offre par
exemple la possibilité de récupérer un fichier ou tout un projet à une version
antérieure. De plus, il vous permet de comparer les modifications au fil du
temps ou bien de savoir quelle est la personne qui a modifié quelque chose en
dernier et qui aurait pu causer un problème. Il est également possible de
déterminer qui a introduit un problème et quand, et bien plus encore. Utiliser
un VCS signifie aussi que si vous vous trompez ou que vous perdez des fichiers,
vous serez en mesure de les récupérer sans nécessiter le moindre effort.

### Les Systèmes De Contrôle De Version Locaux ###

La méthode traditionnelle pour versionner des documents consiste à recopier les
fichiers dans un autre répertoire (avec un nom incluant la date du jour par
exemple). Cette méthode est aussi la plus commune car il s'agit à la fois de la
plus simple à mettre en oeuvre et de la moins fiable. Il est en effet très
facile d'oublier le répertoire dans lequel vous êtes et d'écrire
accidentellement dans le mauvais fichier ou bien d'écraser des fichiers que vous
vouliez conserver.

Pour palier à ce problème, les programmeurs ont développé il y a longtemps des
VCSs locaux qui avaient recours à une simple base de données pour conserver les
modifications d'un fichier (voir figure 1-1).

Insert 18333fig0101.png 
Figure 1-1. Diagramme des systèmes de gestion de version locaux.

L'un des systèmes les plus populaires était RCS et il est aujourd'hui encore
distribué avec de nombreux systèmes d'exploitation. Même le système
d'exploitation populaire Mac OS X inclut le programme rcs lorsqu'on installe les
outils de développement logiciel. Cet outil fonctionne en conservant des
ensembles de patches (c'est-à-dire les différences entre les fichiers) d'une
version à l'autre dans un format spécial stocké sur le disque. Il peut alors
restituer l'état de n'importe quel fichier à n'importe quel instant en
appliquant toutes ces différences aux fichiers.

### Les Systèmes De Contrôle De Version Centralisés ###

Le second problème que les utilisateurs rencontrent, c'est quand ils ont besoin
de collaborer ensemble avec des postes différents. Pour palier à ce problème,
les systèmes de contrôle de version centralisés (CVCS en anglais pour
*Centralized Version Control Systems*) furent développés. Ces systèmes tels que
CVS, Subversion, et Perforce, proposent un serveur central qui contient tous les
fichiers versionnés, et des clients qui peuvent extraire les fichiers de ce
dépôt central. Ce modèle fut le standard du contrôle de version pendant de
nombreuses années (voir figure 1-2).

Insert 18333fig0102.png 
Figure 1-2. Diagramme de la gestion de version centralisée.

Ce modèle offre de nombreux avantages par rapport à la gestion de version
locale. Par exemple, chacun sait jusqu'à un certain point ce que tous les autres
sont en train de faire sur le projet. Les administrateurs ont un contrôle plus
fin des permissions et il est par ailleurs plus aisé d'administrer un CVCS que
de gérer des bases de données locales.

Cependant ce modèle révèle aussi certains inconvénients. Le plus évident c'est
le point unique de panne que le serveur centralisé représente. Si ce serveur
tombe en panne pendant une heure, alors aucun des clients ne peut accéder ou
enregistrer des modifications issues de son travail pendant ce laps de temps. De
plus, si le disque dur du serveur central se corrompt et qu'aucune sauvegarde
n'a été réalisée, alors vous perdez absolument tout de l'historique d'un projet
en dehors des sauvegardes locales que les utilisateurs auraient pu réaliser sur
leur poste de travail. Les systèmes de contrôle de version locaux souffrent du
même problème - dès que l'on possède tout l'historique d'un projet sauvegardé à
un même endroit, on prend le risque de tout perdre.

### Les Systèmes De Gestion De Version Distribués ###

C'est à partir de cet instant que les systèmes de contrôle de version distribués
font leur apparition (DVCSs en anglais pour *Distributed Version Control
Systems*). Dans un DVCS (tels que Git, Mercurial, Bazaar ou Darcs), les clients
n'extraient plus seulement la dernière version d'un fichier, mais ils dupliquent
entièrement le dépôt. Par conséquent, si le serveur disparaît et que les clients
collaboraient avec ce dernier, alors n'importe quel dépôt de l'un des clients
peut servir à restaurer la copie du serveur principal. Chaque extraction est en
réalité une sauvegarde complète de toutes les données (voir figure 1-3).

Insert 18333fig0103.png 
Figure 1-3. Diagramme de gestionnaire de contrôle de version décentralisé.

De plus, un grand nombre de ces systèmes gère particulièrement bien le fait
d'avoir plusieurs dépôts avec lesquels travailler. Cela offre la possibilité de
collaborer avec des groupes de personnes et des manières différents
simultanément sur le même projet. Cette organisation permet la mise en place de
différentes chaînes de traitement qui ne sont pas réalisables avec les systèmes
centralisés, tels que les modèles hiérarchiques.

## Un Rapide Historique De Git ##

Comme de nombreuses choses extraordinaires de la vie, Git est né avec une dose
de destruction créative et de controverse houleuse. Le noyau Linux est un projet
libre de grande envergure. Pour la plus grande partie de sa vie (1991–2002), les
modifications étaient transmises sous forme de patches et d'archives de
fichiers. En 2002, le projet du noyau Linux a commencé à utiliser un DVCS
propriétaire appelé BitKeeper.

En 2005, les relations entre la communauté qui développait le noyau linux et la
société en charge du développement de BitKeeper furent rompues, et le statut de
gratuité de l'outil fut révoqué. Cet événement a poussé la communauté du
développement de Linux (et plus particulièrement Linus Torvalds, le créateur de
Linux) à développer leur propre outil en se basant sur les leçons apprises lors
de l'utilisation de BitKeeper. Certains des objectifs du nouveau système étaient
les suivants :

* Rapidité
* Architecture simple
* Support pour les développements non linéaires (milliers de branches 
  parallèles)
* Complètement distribué
* Capacité à gérer efficacement des projets d'envergure tels que le noyau Linux 
  (vitesse et compacité des données)

Depuis sa naissance en 2005, Git a évolué et mûri dans l'objectif d'être facile
à utiliser tout en conservant ses qualités initiales. Il est particulièrement
rapide, il est très efficace pour des projets d'envergure et il dispose d'un
incroyable système de branches pour les développements non linéaires (voir
chapitre 3).

## Rudiments De Git ##

En quelques mots, qu'est-ce que Git ? Il est fondamental de bien comprendre
cette section, parce que si l'on comprend ce qu'est Git et les concepts sur
lesquels il repose, alors utiliser Git efficacement devient plus facile. Au
cours de l'apprentissage de Git, essayez de libérer votre esprit de tout ce que
vous pourriez connaître au sujet des VCS, tels que Subversion et Perforce. De
cette manière, vous vous éviterez de petites confusions à l'utilisation de cet
outil. Bien que l'interface utilisateur paraisse similaire, Git enregistre et
gère l'information très différemment des autres systèmes ; Comprendre ces
différences vous évitera des confusions lors de son utilisation.

### Des Instantanés, Pas Des Différences ###

La différence majeure entre Git et les autres VCS (Subversion et autres) réside
dans la manière dont Git considère les données. Au niveau conceptuel, la plupart
des autres VCS gèrent l'information comme une liste de modifications de
fichiers. Ces systèmes (CVS, Subversion, Perforce, Bazaar et autres) considèrent
l'information qu'ils gèrent comme une liste de fichiers et les modifications
effectuées sur chaque fichier dans le temps, comme illustré en figure 1-4.

Insert 18333fig0104.png 
Figure 1-4. D'autres systèmes sauvent l'information comme des modifications sur
des fichiers.

Git ne gère pas et ne stocke pas les informations de cette manière. Au
contraire, Git perçoit davantage les données comme un instantané d'un mini
système de fichiers. A chaque fois que vous validez ou enregistrez l'état du
projet dans Git, ce dernier réalise un instantané du contenu de votre copie de
travail à ce moment et enregistre une référence à cet instantané. Afin d'être
plus efficace, si les fichiers n'ont pas changé, Git ne stocke pas le fichier à
nouveau. Il se contente juste d'une référence vers le fichier original qui n'a
pas été modifié. Git perçoit ses données comme le décrit le schéma de la figure
1-5.


Insert 18333fig0105.png 
Figure 1-5. Git stocke les données comme des instantanés du projet au cours du
temps

C'est une distinction importante entre Git et quasiment tous les autres VCSs.
Git a reconsidéré quasiment tous les aspects du contrôle de version que la
plupart des autres systèmes ont copié des générations précédentes. Cela fait
quasiment de Git un mini système de fichiers avec des outils incroyablement
puissants construits par dessus, plutôt qu'un simple VCS. Nous explorerons les
bénéfices qu'il y a à traiter les données de cette manière quand nous aborderons
la notion de branches au chapitre 3.

### Presque Toutes Les Opérations Sont Locales ###

La plupart des opérations de Git ne nécessitent que des fichiers et ressources
locales - généralement aucune information venant d'un autre ordinateur du réseau
n'est nécessaire. Si vous êtes habitué à un CVCS où toutes les opérations sont
ralenties par la latence des échanges réseau, cet aspect de Git vous fera penser
que les dieux de la vitesse ont octroyé leurs pouvoirs à Git. Comme vous
disposez de l'historique complet du projet localement sur votre disque dur, la
plupart des opérations semblent immédiates.

Par exemple, pour parcourir l'historique d'un projet, Git n'a pas besoin d'aller
la chercher sur un serveur pour vous la restituer. Il n'a qu'à simplement la
lire directement dans votre base de donnée locale. Cela signifie que vous avez
presque instantanément accès à l'historique du projet. Si vous souhaitez
connaître les modifications introduites entre la version actuelle d'un fichier
et son état un mois auparavant, Git peut le faire. Git est capable de rechercher
l'état du fichier un mois plus tôt et réaliser le calcul de la différence
localement. Celui lui évite de demander la différence à un serveur ou bien de
devoir récupérer cette ancienne version depuis ce dernier afin de calculer la
différence localement.

Cela signifie aussi qu'il y a très peu de choses que vous ne puissiez réaliser
si vous n'êtes pas connecté ou hors VPN. Si vous voyagez en train ou en avion et
que vous souhaitez avancer votre travail, vous pouvez continuer à gérer vos
versions sans soucis en attendant de pouvoir de nouveau vous connecter pour
partager votre travail. Si vous êtes chez vous et que vous ne pouvez disposer
d'une liaison VPN avec votre entreprise, vous pouvez toujours travailler. Pour
de nombreux autres systèmes, faire de même est impossible ou au mieux très
contraignant.

Avec Perforce par exemple, vous ne pouvez pas faire grand chose tant que vous
n'êtes pas connecté au serveur. Avec Subversion ou CVS, vous pouvez éditer les
fichiers, mais vous ne pourrez pas soumettre des modifications à votre base de
données (car celle-ci est sur le serveur inaccessible). Cela peut paraître
trivial au premier abord, mais vous seriez étonné de découvrir quelle grande
différence cela peut constituer à l'usage.


### Git Contrôle L'Intégrité ###

Dans Git, tout est vérifié par une somme de contrôles avant d'être stocké. Cette
suite de contrôles appliqués aux fichiers donne lieu a une signature unique qui
sert de référence. Par conséquent, cela signifie qu'il est impossible de
modifier le contenu d'un fichier ou d'un répertoire sans que Git ne s'en
aperçoive. Cette fonctionnalité est ancrée dans les fondations de Git et fait
partie intégrante de sa philosophie. Vous ne pouvez pas perdre des données en
cours de transfert ou corrompre un fichier sans que Git ne puisse le détecter.

Le mécanisme que Git utilise pour réaliser les sommes de contrôle est appelé empreinte SHA-1. C'est une chaîne composée de 40 caractères hexadécimaux (de '0' à '9' et de 'a' à 'f') calculée en fonction du contenu du fichier ou de la structure du répertoire considéré. Une empreinte SHA-1 ressemble à celle-ci :

    24b9da6552252987aa493b52f8696cd6d3b00373

Vous trouverez ces valeurs à peu près partout dans Git car il les utilise pour tout. En fait, Git stocke tout dans une base de données locale indexée par ces valeurs plutôt que des noms de fichiers.

### Généralement, Git N'Ajoute Que Des Données ###

Quand vous réalisez des actions dans Git, la quasi-totalité d'entre elles ne
font qu'ajouter des données dans la base de données de Git. Par conséquent, il
est très difficile de demander au système de réaliser des actions irréversibles
ou de lui faire effacer des données d'une quelconque manière. En revanche, comme
dans la plupart des systèmes de contrôle de version, vous pouvez perdre ou
corrompre des modifications qui n'ont pas encore été saisies en base de données.
Cependant, dès lors que vous avez validé un instantané dans Git, il est très
difficile de le perdre, en particulier si vous synchronisez votre base de
données locale avec un dépôt distant.

Tout cela fait de Git un vrai plaisir à utiliser, car on peut expérimenter sans
danger et sans risque de détériorer définitivement son projet. Si vous souhaitez
en savoir plus sur la manière dont Git stocke ses données et récupére des
données qui pourraient sembler perdues, référez-vous au chapitre 9 intitulé
"Sous Le Capot".

### Les Trois Etats ###

A partir d'ici, nous vous recommandons d'être attentif. Il est primordial de se
souvenir de ce qui suit si vous souhaitez que le reste de votre apprentissage
s'effectue sans difficulté. Git gère trois états dans lesquels les fichiers
peuvent résider : validé, modifié et indexé. Validé (ou "commité") signifie que
les données sont stockées en sécurité dans votre base de données locale. Modifié
signifie que vous avez modifié le fichier mais qu'il n'a pas encore été validé
en base de données. Enfin, le terme "indexé" signifie que vous avez marqué un
fichier modifié dans sa version actuelle pour qu'il fasse partie du prochain
instantané du projet.

Ceci nous mène aux trois sections principales d'un projet Git : le répertoire
Git, le répertoire de travail et la zone d'indexation.

Insert 18333fig0106.png 
Figure 1-6. Répertoire de travail, zone d'indexation et répertoire Git.

Le répertoire Git est l'endroit où Git stocke les méta-données et la base de
données des objets de votre projet. C'est la partie la plus importante de Git,
et c'est ce qui est copié lorsque vous clonez un dépôt depuis un autre
ordinateur.

Le répertoire de travail est une extraction unique d'une version du projet. Ces
fichiers sont extraits depuis la base de données compressée dans le répertoire
Git et placés sur le disque afin d'être manipulés ou modifiés.

La zone d'indexation est un simple fichier, généralement situé dans le
répertoire Git, qui stocke les informations référencées pour le tout prochain
instantané.

L'utilisation standard de Git se déroule de la manière suivante :

1.  Vous modifiez des fichiers dans votre répertoire de travail.
2.  Vous indexez les fichiers modifiés afin d'obtenir des instantanés de ces 
    documents dans la zone d'index
3.  Vous validez vos changements, ce qui a pour effet de transférer les 
    instantanés des fichiers de l'index vers la base de donnée du répertoire 
    Git.

Si une version particulière d'un fichier est dans le répertoire Git, il est
considéré comme validé. S'il est modifié mais qu'il n'a pas été ajouté dans la
zone d'indexation, il est indexé. S'il a été modifié depuis le dernier
instantané mais qu'il n'a pas été indexé, il est modifié. Dans le chapitre 2,
vous en apprendrez davantage sur ces états et comment vous pouvez en tirer parti
ou complètement les occulter.

## Installation De Git ##

Commençons donc à utiliser Git. La première étape consiste à l'installer. Vous
pouvez obtenir Git de différentes manières. Les deux principales consistent à
l'installer à partir des sources ou bien de télécharger et d'installer un paquet
existant sur votre plate-forme.

### Installation Depuis Les Sources ###

Si vous le pouvez, il est généralement conseillé d'installer Git à partir des
sources, car vous obtiendrez la version la plus récente. Chaque nouvelle version
de Git tend à inclure des améliorations utiles de l'interface utilisateur, donc
récupérer la toute dernière version est souvent la meilleure option si vous
savez compiler des logiciels à partir de leur code source. La plupart du temps,
les distributions contiennent des versions trop anciennes des logiciels. A moins
que vous ne travailliez sur une distribution très récente ou que vous utilisiez
des backports, une installation à partir des sources s'avère généralement être
la meilleure option.

L'installation de Git nécessite de disposer des bibliothèques suivantes : curl, zlib, openssl, expat, libiconv. Par exemple, si vous avez un système d'exploitation qui utilise yum (tel que Fedora) ou apt-get (tel qu'un système basé sur Debian), vous pouvez utiliser l'une des commandes suivantes pour installer ces dépendances :

    $ yum install curl-devel expat-devel gettext-devel \
      openssl-devel zlib-devel

    $ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \
      libz-dev libssl-dev

Quand vous disposez de toutes les dépendances nécessaires, vous pouvez poursuivre et télécharger la dernière version de Git depuis le site officiel :

    http://git-scm.com/download

Puis, compiler et installer :

    $ tar -zxf git-1.6.0.5.tar.gz
    $ cd git-1.6.0.5
    $ make prefix=/usr/local all
    $ sudo make prefix=/usr/local install

Après ceci, vous pouvez obtenir Git par Git lui-même pour les mises à jour :

    $ git clone git://git.kernel.org/pub/scm/git/git.git

### Installation Sur Linux ###

Si vous souhaitez installer Git sur Linux à partir d'un installateur
d'applications, vous pouvez généralement y parvenir grâce au système de gestion
de paquets de base fourni avec votre distribution. Si vous travaillez sur
Fedora, vous disposez de l'utilitaire yum :

    $ yum install git-core

Si vous êtes sur un système basé sur Debian, tel qu'Ubuntu, essayez apt-get :

    $ apt-get install git-core

### Installation Sur Mac ###

Il y a deux moyens simples d'installer Git sur Mac. Le plus simple est
d'utiliser l'installateur graphique de Git que vous pouvez télécharger depuis
les pages Google Code (voir figure 1-7) :

	http://code.google.com/p/git-osx-installer

Insert 18333fig0107.png 
Figure 1-7. Installateur OS X de Git.

L'autre méthode consiste à installer Git par les MacPorts
(`http://www.macports.org`). Si vous avez installé MacPorts, installez Git à
l'aide de la commande suivante :

    $ sudo port install git-core +svn +doc +bash_completion +gitweb

Vous n'avez pas à ajouter tous les extras, mais vous souhaiterez sûrement
inclure +svn si vous êtes amené à utiliser Git avec des dépôts Subversion (voir
chapitre 8).

### Installation Sur Windows ###

Installer Git sur Windows est très facile. Le projet msysGit fournit une des
procédures d'installation les plus simples. Téléchargez simplement le fichier
exécutable d'installation depuis la page Google Code, et lancez-le :

    http://code.google.com/p/msysgit

A l'issue de l'installation, vous bénéficiez à la fois de la version en ligne de
commande (avec un client SSH utile pour la suite) et de l'interface graphique
standard.

## Paramétrage Pour La Première Utilisation De Git ##

Maintenant que vous avez installé Git sur votre système, vous voudrez
personnaliser votre environnement Git. Vous ne devriez avoir à réaliser ces
réglages qu'une seule fois ; ils persisteront lors des mises à jour. Vous pouvez
aussi les changer à tout instant en réexécutant les mêmes commandes.

Git contient un outil appelé `git config` pour vous permettre de voir et de
modifier les variables de configuration qui contrôlent tous les aspects de
l'apparence et du comportement de Git. Ces variables peuvent être stockées à
trois endroits différents :

*   Fichier `/etc/gitconfig` : Contient les valeurs pour tous les utilisateurs 
    et tous les dépôts du système. Si vous passez l'option `--system` à `git 
    config`, il lit et écrit ce fichier spécifiquement.
*   Fichier `~/.gitconfig` : Spécifique à votre utilisateur. Vous pouvez forcer 
    Git à lire et écrire ce fichier en passant l'option `--global`.
*   Fichier `config` dans le répertoire Git (c'est à dire `.git/config`) du 
    dépôt en cours d'utilisation : spécifique au seul dépôt en cours.

Chaque niveau surcharge le niveau précédent, donc les valeurs dans `.git/config` 
surchargent celles de `/etc/gitconfig`.

Sur les systèmes Windows, Git recherche le fichier `.gitconfig` dans le
répertoire `$HOME` (`C:\Documents and Settings\$USER` la plupart du temps). Il
recherche tout de même `/etc/gitconfig`, bien qu'il soit relatif à la racine
MSys, qui se trouve où vous aurez décidé d'installer Git sur votre système
Windows.

### Votre Identité ###

La première chose à faire après l'installation de Git est de renseigner votre
nom et votre adresse e-mail. C'est important car tous les commits Git utilisent
cette information et elle est indélébile dans tous les commits que vous pourrez
manipuler :

    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com

Encore une fois, cette étape n'est nécessaire qu'une seule fois si vous passez
l'option `--global` car Git réutilisera toujours cette information pour chaque
action réalisée par l'utilisateur du système. Si vous souhaitez surcharger ces
valeurs avec un nom ou une adresse e-mail différents pour un projet spécifique,
vous pouvez lancer ces commandes sans option `--global` lorsque vous êtes dans
ce projet.

### Votre Editeur De Texte ###

À présent que votre identité est renseignée, il est temps de configurer l'éditeur de texte qui sera utilisé par défaut quand Git vous demandera de saisir un message. Par défaut, Git utilise l'éditeur par défaut configuré pour le système. Il s'agit généralement de Vi ou de Vim. Si vous souhaitez utiliser un éditeur de texte différent comme Emacs, il vous suffit d'exécuter la commande suivante :

    $ git config --global core.editor emacs

### Votre Outil De Différences ###

Une autre option utile concerne le paramétrage de l'outil de différences à
utiliser pour la résolution des conflits de fusion. Admettons que vous
souhaitiez utiliser vimdiff :

    $ git config --global merge.tool vimdiff

Git accepte kdiff3, tkdiff, meld, xxdiff, emerge, vimdiff, gvimdiff, ecmerge, et
opendiff comme outils valides de fusion. Vous pouvez aussi paramétrer un outil
personnalisé en vous référant au chapitre 7 pour plus d'informations la
procédure à suivre.

### Vérifier Vos Paramètres ###

Si vous souhaitez vérifier vos réglages, il convient d'utiliser la commande `git
config --list` afin de lister tous les réglages que Git a pu trouver jusqu'ici :

    $ git config --list
    user.name=Scott Chacon
    user.email=schacon@gmail.com
    color.status=auto
    color.branch=auto
    color.interactive=auto
    color.diff=auto
    ...

Vous pourrez voir certains paramètres apparaître plusieurs fois, car Git lit les
mêmes paramètres depuis plusieurs fichiers (`/etc/gitconfig` et `~/.gitconfig`,
par exemple). Git utilise la dernière valeur pour chaque paramètre.

Vous pouvez aussi vérifier la valeur effective d'un paramètre particulier en tapant `git config <paramètre>` :

    $ git config user.name
    Scott Chacon

## Obtenir De L'Aide ##

Si vous avez besoin d'aide pour utiliser Git, il existe trois moyens simples
d'obtenir les manuels d'utilisation de chacune des commandes de Git :

    $ git help <verbe>
    $ git <verbe> --help
    $ man git-<verbe>

Par exemple, vous pouvez obtenir la page de manuel pour la commande `config` en
exécutant la ligne suivante:

    $ git help config

Ces commandes sont particulièrement agréables car vous pouvez y accéder depuis
n'importe où, y compris hors connexion. Si les pages de manuel et ce livre ne
sont pas suffisants, vous pouvez toujours avoir recours aux canaux `#git` ou
`#github` sur le serveur IRC Freenode (irc.freenode.net). Ces canaux sont
régulièrement peuplés de centaines de personnes dotés d'une bonne connaissance
de Git et prêtes à apporter leur aide.

## Résumé ##

Vous devriez avoir à présent une vue d'ensemble de ce qu'est Git et en quoi il
est différent des autres CVCS que vous pourriez avoir déjà utilisé. Vous devriez
aussi avoir une version de Git en état de fonctionnement sur votre système,
paramétrée avec votre identité. Il est temps désormais d'apprendre les bases de
l'utilisation de Git.