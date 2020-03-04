# Partie 2.4 : connexion à un serveur distant, transfert de fichier

## Connexion à un serveur distant

Sous Unix, on utilise la commande `ssh` pour établir une communication sécurisée, 
sur un réseau informatique (Intranet ou Internet) entre une machine locale (le client) et une machine distante (le serveur).
La syntaxe de la commande est la suivante :

`ssh <nom_utilisateur>@<nom_serveur_distant>`

Exercice : Connectez-vous au serveur **core.cluster.france-bioinformatique.fr** en utilisant la commande `ssh`.

> **Solution :**:
> > ```bash
> > $ ssh hchiapello@core.cluster.france-bioinformatique.fr 
> > ```
{:.answer}

## Transfert - copie de fichiers - avec scp
Pour copier un fichier à partir d'un ordinateur sur un autre vous devrez utiliser la commande `scp`. 
La syntaxe est la suivante :

### Pour un fichier

`scp monfichier.txt <nom_utilisateur>@<nom_serveur_distant>:<répertoire_destination>`

Question : copier le fichier `Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3` dans votre  répertoire utilisateur ("home directory") du serveur core cluster de l'IFB :
> **Solution :**:
> > ```bash
> > $ scp Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3 hchiapello@core.cluster.france-bioinformatique.fr:~/ 
> > ```
{:.answer}

### Pour un répertoire :

`scp -r monrépertoire <nom_utilisateur>@<nom_serveur_distant>:<répertoire_destination>`


Question : Transférer le répertoire study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq de votre machine locale vers le serveur core.cluster.france-bioinformatique.fr dans votre répertoire utilisateur par défaut ("home directory")

> **Solution :**:
> > ```bash
> > $ scp -r study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq hchiapello@core.cluster.france-bioinformatique.fr:~/
> > ```
{:.answer}

## Si vous voulez aller plus loin

Exercice :  récupérer un génome Refseq de votre choix sur le site du NCBI avec la commande `rsync`
voir documentation ici : https://www.ncbi.nlm.nih.gov/genome/doc/ftpfaq/ 

