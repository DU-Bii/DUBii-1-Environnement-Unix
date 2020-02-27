# Tutoriel 2 : Les bases d'Unix


## Prérequis : téléchargement des jeux de données sur votre poste de travail 

Sur votre station de travail, dans un *shell* :

- déplacez-vous dans votre répertoire personnel,
- créez le répertoire `dubii`,
- déplacez-vous dans ce répertoire.

> **Aide :**:
> > ```bash
> > $ cd ~
> > $ mkdir dubii
> > $ cd dubii
> > ```
{:.answer}


Téléchargez les fichiers des jeux de données du DUBii avec la commande :

```bash
$ git clone https://github.com/DU-Bii/study-cases.git
```

Remarques :

- L'instruction `git` vous sera expliquée un peu plus tard.
- La commande à exécuter est assez longue et complexe. Pour éviter de faire des erreurs et aller plus vite, utilisez le copier/coller. Voici deux méthodes :
    1. Sélectionnez la commande en la surlignant avec le clic gauche de votre souris. Puis dans votre shell, cliquez sur le bouton du milieu de votre souris.
    2. Sélectionnez la commande en la surlignant avec le clic gauche de votre souris. Appuyez ensuite sur les touches `Ctrl` + `C` (c'est-à-dire les touches *Control* et *C* pressées en même temps). Dans votre shell, appuyez sur les touches `Ctrl` + `Maj` + `V` (c'est-à-dire les touches *Control*, *Majuscule* et *V* pressées en même temps).


Patientez quelques instants que les données soient téléchargées.

Déplacez-vous ensuite dans le répertoire `study-cases` nouvellement créé.

## Partie 2.1 : Espace disque

### Connaître le taux d'occupation des espaces disques d'un poste de travail

La commande `df` (pour *disk free*) permet de connaître les quantités d'espace occupé et disponible pour tous les disques du système. L'option `-h` permet d'utiliser les multiples "human readable" (ko, Mo, Go, To, ...).

```{bash}
$ df- h
```

### Connaître la quantité d'espace disque occupé par un fichier/dossier.

La commande pour connaître la taille des fichiers présents dans un dossier est `ls -lh`.

<blockquote>
Exemple: Déterminer la quantité d'espace disque occupée par chacun des fichiers présents dans le répertoire `/home/sdv/dubii` et trier les fichiers du plus volumineux au moins volumineux :

```{bash}
$ cd /home/sdv/dubii
$ ls -lh
# Afficher la taille des fichiers du dossier courant
```
</blockquote>

Pour connaître la quantité d'espace disque occupée par un dossier, utiliser la commande `du` (disk usage), encore une fois avec l'option `-h`. On peut affichier la version résumé avec `-s`.

<blockquote>
Exemple: Afficher la taille des sous-dossiers du dossier `/home/sdv/dubii`.

```{bash}
$ du -sh /home/sdv/dubii
```
</blockquote>

## Partie 2.2 : Afficher le contenu d'un fichier

Sous Linux on dispose de plusieurs commandes permettant d'afficher le contenu de fichiers texte de différentes manières.

### cat

Affiche et concatène le contenu du ou des fichiers donnés en arguments
(ou de l'entrée standard) sur la sortie standard.

**Exemple 1**: afficher le contenu du fichier `cutadapt_bwa_featureCounts_all.tsv`
dans le répertoire `RNA-seq`

> **Solution**:
> > ```bash
> > $ cat RNA-seq/cutadapt_bwa_featureCounts_all.tsv
> > Geneid  WT1 WT2 dFNR1   dFNR2
> > b0001   70  98  72  63
> > b0002   23421   33092   32156   20749
> > b0003   7538    10350   9596    6490
> > b0004   8263    11927   11042   7145
> > b0005   121 156 104 62
> > b0006   177 224 287 209
> > b0007   138 116 68  50
> > b0008   2964    3971    4211    2823
> > b0009   213 205 196 128
> > [...]
> > b4400   82  42  37  35
> > b4401   3349    4692    2619    1609
> > b4402   201 318 224 128
> > b4403   82  116 87  68
> > ```
{:.answer}


**Exemple 2** : concaténer le contenu des fichiers `FNR1_vs_input1_cutadapt_bowtie2_homer.bed`
et `FNR1_vs_input1_cutadapt_bowtie2_macs2.bed` dans le répertoire `ChIP-seq`.

> **Solution**:
> > ```bash
> > $ cat ChIP-seq/FNR1_vs_input1_cutadapt_bowtie2_homer.bed ChIP-seq/FNR1_vs_input1_cutadapt_bowtie2_macs2.bed
> > # HOMER Peaks
> > # Peak finding parameters:
> > # tag directory = ChIP-seq/results/peaks/FNR1_vs_input1/homer/FNR1_tag
> > #
> > # total peaks = 161
> > # peak size = 177
> > # peaks found using tags on both strands
> > # minimum distance between peaks = 354
> > # fragment length = 176
> > # genome size = 4639221
> > [...]
> > Chromosome  4628694 4628894 FNR1_vs_input1_cutadapt_bowtie2_macs2_peak_409  255 .   1.64016 27.14359    25.51793    45
> > Chromosome  4633063 4633362 FNR1_vs_input1_cutadapt_bowtie2_macs2_peak_410  374 .   1.87671 39.12086    37.41762    131
> > Chromosome  4640075 4640748 FNR1_vs_input1_cutadapt_bowtie2_macs2_peak_411  6432    .   4.90760 645.83362   643.22699   454
> > ```
{:.answer}


**Question 1** : quel inconvénient majeur voyez-vous à la commande `cat`?  

> **Réponse**:
> > La commande `cat` affiche la totalité des fichiers ce qui rend la sortie
> > de la commande souvent illisible.
{:.answer}


### less

_less does more or less the same as more, but less does more than more_

La commande `less` permet d'afficher le contenu d'un ou plusieurs fichiers
page par page, ce qui est très utile lorsqu'on manipule des fichiers de taille
importante.

Quelques fonctionnalités utiles :

- `barre d'espace` : faire défiler le contenu page par page  
- `g`: affiche le debut du fichier
- `G`: affiche la fin du fichier
- `/`: recherche les occurences d'un motif
- `n`: passe à l'occurence suivante du motif recherché
- `N`: passe à l'occurence précédente du motif recherché
- `:n` : passe au fichier suivant ('next file', si plusieurs fichiers en arguments)  
- `:p` : passe au fichier précédent ('previous file', si plusieurs fichiers en arguments)
- `q` : quitte less  

**Question 2** : afficher le contenu du fichier
`cutadapt_bwa_featureCounts_all.tsv` avec `less`
> > ```bash
> > less RNA-seq/cutadapt_bwa_featureCounts_all.tsv
> > ```
{:.answer}
### head
La commande `head` permet d'afficher uniquement le début du ou des fichier(s)
passé(s) en argument.
Par défaut, `head` affiche les 10 premières lignes d'un fichier.  
Utiliser l'option `-n <N>` pour afficher les `N` premières lignes d'un fichier.

**Question 3** : afficher les 20 premières lignes du fichier `RNA-seq/cutadapt_bwa_featureCounts_all.tsv`.

> **Réponse**:
> > ```bash
> > $ head -n 20 RNA-seq/cutadapt_bwa_featureCounts_all.tsv
> > Geneid	WT1	WT2	dFNR1	dFNR2
> > b0001	70	98	72	63
> > b0002	23421	33092	32156	20749
> > b0003	7538	10350	9596	6490
> > b0004	8263	11927	11042	7145
> > b0005	121	156	104	62
> > b0006	177	224	287	209
> > b0007	138	116	68	50
> > b0008	2964	3971	4211	2823
> > b0009	213	205	196	128
> > b0010	184	193	130	74
> > b0011	44	13	13	10
> > b0013	18	6	7	3
> > b0014	10758	14747	15432	10243
> > b0015	1343	1667	1549	1045
> > b0016	261	326	252	141
> > b4412	0	0	0	0
> > b0018	7	0	2	1
> > b4413	1	0	1	1
> > b0019	714	944	1093	704
> > ```
{:.answer}

### tail

La commande `tail` permet d'afficher uniquement la fin du ou des fichier(s)
passé(s) en argument.
Par défaut `tail` affiche les 10 dernières lignes d'un fichier.
Utiliser l'option `-n N` pour afficher les `N` dernières lignes d'un fichier.

**Question 4** : afficher les 20 dernières lignes du fichier `RNA-seq/cutadapt_bwa_featureCounts_all.tsv`.

> **Réponse**:
> > ```bash
> > $ tail -n 20 RNA-seq/cutadapt_bwa_featureCounts_all.tsv
> > b4384	846	1241	1173	751
> > b4385	205	224	145	84
> > b4386	243	233	192	106
> > b4387	164	197	142	98
> > b4388	409	489	404	264
> > b4389	712	785	615	350
> > b4390	421	535	471	316
> > b4391	2341	2740	2888	1913
> > b4392	538	601	717	464
> > b4393	203	258	202	137
> > b4394	256	292	243	167
> > b4395	404	591	422	309
> > b4396	903	1161	1055	709
> > b4397	235	280	242	143
> > b4398	210	251	178	122
> > b4399	166	115	122	101
> > b4400	82	42	37	35
> > b4401	3349	4692	2619	1609
> > b4402	201	318	224	128
> > b4403	82	116	87	68
> >
> >
{:.answer}


## Partie 2.3 : L'éditeur de texte nano

Il existe beaucoup d'éditeurs de fichiers textes sour Linux.


[![Un bon éditeur](img/un-bon-editeur.png)](img/un-bon-editeur.png)

Parmi les plus connus on trouve : `vi`, `emacs` et `nano`.  
___Nano___ est l'éditeur le plus simple à utiliser.

**Question 5** : qu'est-ce qu'un un éditeur de texte ? Quelle différence avec un traitement de texte ?

> **Réponse**
> > éditeur = programme permettant de modifier des fichiers texte sans mise en forme
> > traitement de texte = logiciel le plus souvent avec une interface graphique pour mettre en forme des documents
{:.answer}

Pour lancer l'éditeur de texte nano : il vous suffit de taper `nano`
éventuellement suivi d'un nom de fichier à éditer.

Toutes les commandes sont résumées dans le bandeau en bas de l'écran
Le symbole `^` signifie <kbd>CTRL</kbd> (la touche Contrôle de votre clavier).

Voici les raccourcis les plus importants :
- `Ctrl-G` : afficher l'aide
- `Ctrl-K` : couper la ligne de texte (et la mettre dans le presse-papier)
- `Ctrl-U` : coller la ligne de texte que vous venez de couper
- `Ctrl-C` : afficher à quel endroit du fichier votre curseur est positionné (numéro de ligne)
- `Ctrl-W` : rechercher une chaine de caractères dans le fichier
- `Ctrl-O` : enregistrer le fichier (écrire)
- `Ctrl-X` : quitter Nano.

Vous pouvez vous déplacer dans le fichier avec les flèches du clavier ainsi
qu'avec les touches <kbd>PageUp</kbd> et <kbd>PageDown</kbd> pour avancer
de page en page (les raccourcis <kbd>CTRL-Y</kbd> et <kbd>CTRL-V</kbd> fonctionnent aussi).

**Question 6** : ouvrir avec l'éditeur `nano` le fichier `Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3`  
**Recommandations :**  
- Créer un répertoire ~/DUBii/study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/Annotations  
- Télécharger depuis le site https://du-bii.github.io/study-cases/Escherichia_coli/bacterial-regulons_myers_2013/ le fichier `Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3`

- Rechercher les lignes contenant le nom de gène `oriC` et afficher le numéro de ces lignes
- Supprimer ces lignes
- Enregistrer le fichier sous le nom `Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome_wo_oriC.gff`

Remarques :

- pour rechercher un mot plusieurs fois sans le réécrire, tapez juste `Ctrl-W ENTER`
- si vous voulez sortir du mode recherche, tapez `CTRL-C`

> **Réponse**  
> > Utiliser successivement les commandes :  
> > - `Ctrl-W` pour rechercher `oriC`
> > - `Ctrl-C` pour connaitre le numéro de ligne courante  
> > - `Ctrl-K` pour supprimer la ligne courante  
> > Au moment de sauvergarder le fichier avec la commande `Ctrl-O` penser à modifier le nom du fichier  
> > Les 4 occurences de `oriC` sont aux lignes 4859, 8256, 18950 et 22228 dans le fichier original (4859, 8255, 18948 et 22225 si vous supprimez les lignes au fur et à mesure)
> >
> >
{:.answer}


## Partie 2.4 : Avoir de l'aide sur une commande

Sous Linux toutes les commandes sont documentées de manière standardisée.

Il y a deux moyens d'accèder à l'aide d'une commande :

- via la commande `man <nom_commande>` qui permet d'accéder au manuel
(description complète) de la commande page par page avec les facilités de
recherche d'un éditeur de texte,

- via l'option `<nom_commande> --help`: on affiche un résumé de la
documentation et des options à l'écran.

**Question 7** : Quelle signifie l'option `-N` de la commande less ?

> **Réponse**:
> > ```bash
> > $ man less
> > [...]
> >   -n  -N  ....  --line-numbers  --LINE-NUMBERS
> >                   Don't use line numbers.
> > [...]
> > ```
> L'option `-N` sert à afficher les numéros des lignes à gauche de chaque ligne.
{:.answer}
