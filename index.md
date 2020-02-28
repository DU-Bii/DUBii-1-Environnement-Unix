## Synopsis

L'objectif de ce module est de vous familiariser avec l'environnement Unix et ses principales commandes.

Lien court vers cette page : <https://huit.re/dubii-m1>

Rappel des prérequis : <https://du-bii.github.io/accueil/activites_preparatoires/>


## Intervenants

- Hélène Chiapello, INRAE, `helene.chiapello@inra.fr`, [@HeleneChiapello](https://twitter.com/HeleneChiapello)
- Pierre Poulain, Université de Paris, `pierre.poulain@univ-paris-diderot.fr`, [@pierrepo](https://twitter.com/pierrepo)
- Benoist Laurent, IPBC, `benoist.laurent@ibpc.fr`
- Julien Seiler, IGBMC, `seilerj@igbmc.fr`
- Jacques van Helden, Institut Français de Bioinformatique et Univ. Aix-Marseille, `Jacques.van-Helden@univ-amu.fr`
- Sandra Dérozier, INRAE, `sandra.derozier@inra.fr`
- Hubert Santuz, CNRS, `hubert.santuz@ibpc.fr`


## Séance 1 - Premiers pas

- Lundi 02/03/2020 14:30 - 17:30
- Instructeurs : Hélène Chiapello & Pierre Poulain
- helpers : Benoist Laurent & Hubert Santuz

[Présentation](seance1/slides_intro/index.html) - [Tutoriel 1](seance1/tutorial1/README.md) - [Tutoriel 2](seance1/tutoriel2/README.md)


## Séance 2 - Gestion de flux et extraction de données

- Mardi 03/03/2020 14:30 - 17:30
- Instructeurs : Hélène Chiapello & Benoist Laurent
- Helpers : Sandra Derozier & Pierre Poulain

<!--
[Présentation + TP](seance2/slides/index.html)
-->

## Séance 3 - Gestion et utilisation des ressources IFB

- Jeudi 05/03/2020 9:00 - 12:00
- Instructeurs : Julein Seiler & Pierre Poulain
- Helpers : Hélène Chiapello, Benoist Laurent & Jacques van Helden

<!--
[Tutoriel](seance3/tutorial/README.md)

[Changer son prompt](seance3/slides/index.html)
-->

## Séance 4 - Automatisation

- Mardi 10/03/2020 9:30 - 12:30
- Instructeurs : Benoist Laurent & Hélène Chiapello
- Helper : Pierre Poulain

<!--
[Tutoriel](seance4/tutorial/README.md)

[Présentation](seance4/slides/index.html)
-->


## Installer un *shell* Linux sur sa machine

### Linux et Mac OS X

Si vous travaillez avec les systèmes d'exploitations Linux (Ubuntu, Mint, Debian...) ou Mac OS X, vous avez déjà un *shell* installé sur votre machine.

### Windows

Si vous travaillez avec Windows :

- Pour Windows 7. Nous vous conseillons d'installer [Git pour Windows](https://git-for-windows.github.io/) qui en plus du gestionnaire de versions git installera un *shell* Linux.
- Pour Windows 10. Vous pouvez installer très rapidement un *shell* Linux. Voici quelques liens pour y arriver :
    + <https://www.windowscentral.com/how-install-bash-shell-command-line-windows-10>
    + <https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/>
    + <https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/>

    Depuis un *shell* Linux, votre répertoire utilisateur de Windows est accessible via le chemin `/mnt/c/Users/<login-windows>` ou `<login-windows>` est votre *login* sous Windows. Nous vous conseillons de travailler depuis ce répertoire afin que vos fichiers puissent également être visibles depuis Windows.

Ces recommandations sont tirées du site de [Software Carpentry](https://carpentries.org/) dédié au [*Shell*](http://swcarpentry.github.io/shell-novice/setup.html).

Si vous souhaitez simplement un logiciel sous Windows pour vous connecter au cluster du NNCR en SSH. Nous vous conseillons [MobaXterm](https://mobaxterm.mobatek.net/). La version [*Free*](https://mobaxterm.mobatek.net/download.html) est suffisante. Vous trouverez quelques vidéos de démo [ici](https://mobaxterm.mobatek.net/demo.html).

Pour copier / coller entre Windows et le *shell* Linux :

- Pour copier depuis Windows (<kbd>Ctrl</kbd>+<kbd>C</kbd>) puis coller dans le *shell* : clic droit de la souris.
- Pour copier depuis le *shell* (<kbd>Ctrl</kbd>+<kbd>Maj</kbd>+<kbd>C</kbd>) puis coller dans Windows (<kbd>Ctrl</kbd>+<kbd>V</kbd>)


## Bibliographie / webographie

Livre :

- [Bioinformatics Data Skills](http://shop.oreilly.com/product/0636920030157.do), Vince Buffalo, O'Reilly Media, 2015.

Sites internet :

- [The UNIX Shell](http://swcarpentry.github.io/shell-novice/), cours en ligne de *Software Carpentry*.
- [Unix Fondamentals](https://edu.sib.swiss/pluginfile.php/2878/mod_resource/content/4/couselab-html/content.html), du *Swiss Institute of Bioinformatics*.
- [IFB SLURM cluster user guide](http://taskforce-nncr.gitlab.cluster.france-bioinformatique.fr/doc/slurm_user_guide/), guide d'utilisation du *cluster SLURM de l'Institut Français de Bioinformatique*.


## Licence

![](img/CC-BY-SA.png)

Ce contenu est mis à disposition selon les termes de la licence [Creative Commons Attribution - Partage dans les Mêmes Conditions 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/deed.fr) (CC BY-SA 4.0). Consultez le fichier [LICENSE](LICENSE) pour plus de détails.
