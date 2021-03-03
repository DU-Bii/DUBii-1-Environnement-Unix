# Exploration de données COVID-19 avec bash
T. Denecker et H. Chiapello

## Informations générales

### Objectif

L'objectif de ce TP est de télécharger et vérifier un ensembme de fichiers de données de séquençage du SARS-CoV-2 à l'aide de scripts bash. Les fichiers proviennent de l'European National Archive (ENA) qui est la plateforme européenne chargée de la gestion, du partage, de l’intégration, de l’archivage et de la diffusion des données de séquences [Pour en savoir plus](https://www.ebi.ac.uk/ena/browser/about).

Une page de documention est proposée par l'ENA pour télécharger les séquences qui y sont hébergées : [ici](https://ena-docs.readthedocs.io/en/latest/retrieval/file-download.html).

### Étapes

Plusieurs étapes seront réalisées lors de ce TP :

1) Créer un dossier pour organiser les fichiers télécharges
2) Téléchargement des fichiers avec la commande `wget`
3) Exploration des fichiers :
    - pour chaque fichier fastq, nous allons compter le nombre de séquences. Si le nombre de séquences est en dessous d’une certaine valeur, nous allons afficher un message (dans le cas par exemple où on voudrait un nombre minimal de reads par fichiers).

Pour compter le nombre de reads, il y aura 2 stratégies :

- Soit compter le nombre de lignes et diviser cette valeur par 4 (sachant qu’un reads c’est 4 lignes);
- Soit compter le nombre de lignes qui ne contiennent que + (la 3e ligne pour des reads récents séquencés par illumina).

### La commande `wget`

> Wget est un programme en ligne de commande non interactif de téléchargement de fichiers depuis le Web. Il supporte les protocoles HTTP, HTTPS et FTP ainsi que le téléchargement au travers des proxies HTTP. Il est disponible sur presque tous les environnements Unix.

Pour en savoir plus : [ici](https://doc.ubuntu-fr.org/wget)


### Les données

Les données utilisées ont été sélectionnées sur le site [COVID-19 Data Portal](https://www.covid19dataportal.org/sequences?db=embl-covid19).
Nous vous demandons de télécharger les fichiers de lectures des 11 échantillons des données de séquençage du Projet ENA : PRJNA07154, voir
https://www.ebi.ac.uk/ena/browser/view/PRJNA507154. 
A partir de ce lien nous avons téléchargé le fichier de metadonnées suivant:

``` bash
$ cat filereport_read_run_PRJNA507154.tsv
run_accession   sample_accession        tax_id  scientific_name instrument_platform     library_source  center_name     fastq_md5       fastq_ftp       sample_title
SRR8265746      SAMN10485239    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      2571ab5bc76da9605c4cfe6467d7b6b2;28806c5c96fecc5ce7be29953df0d3dc       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/006/SRR8265746/SRR8265746_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/006/SRR8265746/SRR8265746_2.fastq.gz        Human coronavirus OC43 - MDS6
SRR8265747      SAMN10485240    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      d767d7d7cbcc6487c1bd73b04a798e93;a568e39ebacd4e9f163bf92257925a26       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/007/SRR8265747/SRR8265747_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/007/SRR8265747/SRR8265747_2.fastq.gz        Human coronavirus OC43 - MDS11
SRR8265748      SAMN10485241    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      873e84c1bdf1d28de6d2f9f80355dd96;65689b188c451858806b5d48eb0063d0       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/008/SRR8265748/SRR8265748_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/008/SRR8265748/SRR8265748_2.fastq.gz        Human coronavirus OC43 - MDS12
SRR8265749      SAMN10485242    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      86c3a7a7816d9abac9430edb822990fe;a87ea8a2a2ea1da3f507bab1cf13ce1a       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/009/SRR8265749/SRR8265749_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/009/SRR8265749/SRR8265749_2.fastq.gz        Human coronavirus OC43 - MDS14
SRR8265750      SAMN10485235    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      4e75e0900474efc29d65c5c01134bba7;c8c3f11b9c3ae64f87fa929312e7ffea       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/000/SRR8265750/SRR8265750_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/000/SRR8265750/SRR8265750_2.fastq.gz        Human coronavirus OC43 - MDS1
SRR8265751      SAMN10485236    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      bb964c2b3e02fc9f9f056295637b42c1;be8f02dc2dc4e12baf0ed36730a448b1       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/001/SRR8265751/SRR8265751_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/001/SRR8265751/SRR8265751_2.fastq.gz        Human coronavirus OC43 - MDS2
SRR8265752      SAMN10485237    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      2ad85053c9816f2d481e4911e948682a;c71dd057ebaa98a3142923016424ed6e       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/002/SRR8265752/SRR8265752_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/002/SRR8265752/SRR8265752_2.fastq.gz        Human coronavirus OC43 - MDS4
SRR8265753      SAMN10485238    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      ff7e46fbdac8e2cb718ff7dd26bb21a9;f1c3bbc70683ebb8ac9ff68f51e2e695       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/003/SRR8265753/SRR8265753_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/003/SRR8265753/SRR8265753_2.fastq.gz        Human coronavirus OC43 - MDS5
SRR8265754      SAMN10485243    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      c4a6706cdaf80e12067588d48cd57ee1;f0841ddd122379ffabea8ce03480bb88       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/004/SRR8265754/SRR8265754_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/004/SRR8265754/SRR8265754_2.fastq.gz        Human coronavirus OC43 - MDS15
SRR8265755      SAMN10485244    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      4c9146e806ec8f16de8134b54377e86d;dd230409a654ffc48e308bcab8c820b0       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/005/SRR8265755/SRR8265755_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/005/SRR8265755/SRR8265755_2.fastq.gz        Human coronavirus OC43 - MDS16
SRR8265756      SAMN10485245    31631   Human coronavirus OC43  ILLUMINA        VIRAL RNA       SUB4830588      002d6244e103d6c7732e42a05e80a8e9;89c6697b47c84eb2db23dd2db30bb194       ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/006/SRR8265756/SRR8265756_1.fastq.gz;ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/006/SRR8265756/SRR8265756_2.fastq.gz        Human coronavirus OC43 - PR2
```

## Mise en pratique

Démarrer un serveur via JupyterHub (https://jupyterhub.cluster.france-bioinformatique.fr) en choisissant la configuration **medium** (4 cpu, 10 GB de RAM). Lancer ensuite un terminal.

### Script 1 - Téléchargement des données

Nous vous demandons d'écrire un script bash qui va réaliser les étapes suivantes :
- Création d'un dossier *COVID_FASTQ* pour stocker les fichiers de données FASTQ et d'un dossier *COVID19_META* pour stocker les métadonnées associées
- Extraire dans un tableau les URL de téléchargement contenues dans le fichier *filereport_read_run_PRJNA507154.tsv* 
   
    + téléchargement des deux fichiers de lectures à l'aide de la commande `wget`
Un paramètre intéressant de la commande wget est la possibilité de rediriger le fichier téléchargé dans un dossier spécifié : `-P DOSSIER_DESTINATION` :

``` bash
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR826/006/SRR8265756/SRR8265756_1.fastq.gz -P COVID19_FASTQ
```

Cette commande doit être à chaque fichier que vous souhaitez télécharger.

** Conseils**
- Utiliser la cheatsheet Bash: https://devhints.io/bash
- N'oublier pas de faire un `chmod +x NOM_SCRIPT` pour rendre votre script executable.


> **Solution :**:
> > ``` bash
> > #!/bin/bash
> > 
> > #------------------------------------------------------------------------------
> > #     - Télécharger un ensemble de fichiers de lectures de l’ENA
> > #     - Les stocker dans un répertoire dédié.
> > # Auteurs: Hélène Chiapello & Thomas Denecker
> > # Affiliation: IFB
> > # Organisme : SARS-CoV-2
> > # Date: Mars 2021
> > # Étapes :
> > # 1- Creation des dossiers de reception
> > # 2- Téléchagement des fichiers
> > #------------------------------------------------------------------------------
> >
> > echo "=============================================================="
> > echo "Creation du dossier COVID_FASTQ"
> > echo "=============================================================="
> >
> > mkdir -p COVID_FASTQ
> >
> > echo "--------------------------------------------------------------" 
> > echo "Téléchargement des séquences brutes du BioProjet PRJNA507154" 
> > echo "--------------------------------------------------------------" 
> >
> > ftp_url=($(tail -n +2 filereport_read_run_PRJNA507154.tsv | cut -f 9 | cut -d ';' -f 1))
> > ftp_url+=($(tail -n +2 filereport_read_run_PRJNA507154.tsv | cut -f 9 | cut -d ';' -f 2))
> >
> > for my_url in ${ftp_url[@]}
> > do
> >        echo "wget ${my_url} -P COVID_FASTQ\n"
> >        wget ${my_url} -P COVID_FASTQ
> > done

> > ```
{:.answer}


#### Architecture du projet

``` bash
$ tree 
.
├── FASTQ
│   ├── SRR8265752_1.fastq.gz
│   ├── SRR8265752_2.fastq.gz
│   ├── SRR8265754_1.fastq.gz
│   ├── SRR8265754_2.fastq.gz
│   ├── SRR8265756_1.fastq.gz
│   └── SRR8265756_2.fastq.gz
└── script1.sh
```

**Pour aller plus loin :**

- Donner le fichier contenant les données à télécharger en argument de la ligne de commande du script
- Vérifier l'intégrité des fichiers téléchargés avec par exemple la commande `md5sum`.


### Script 2 - Exploration

Nous souhaitons à présent explorer ces fichiers. Pour réaliser cette exploration, nous allons utiliser une boucle `for` qui va itérer sur tous les fichiers présents dans le dossier `COVID_FASTQ` et qui termine par `.fastq.gz`.

#### Stratégie 1

Nous allons compter le nombre de lignes et diviser cette valeur par 4 (sachant qu’un reads c’est 4 lignes). Pour le vérifier, nous avons par exemple la page [wikipedia](https://fr.wikipedia.org/wiki/FASTQ) ou encore une documentation proposée par [Illumina](https://emea.support.illumina.com/bulletins/2016/04/fastq-files-explained.html)

> ** Solution :**
> > ``` bash
> > #!/bin/bash
> > 
> > #------------------------------------------------------------------------------
> > # Objectifs du script :  
> > #     - Explorer les fichiers fastq.gz d'intérêt
> > # Auteurs: Hélène Chiapello & Thomas Denecker
> > # Affiliation: IFB
> > # Organisme : SARS-CoV-2
> > # Date: Mars 2021
> > # Étapes :
> > # 1- Compter le nombre de reads et alerter si le nombre est trop faible
> > #------------------------------------------------------------------------------
> > 
> > limit=2000000
> > 
> > for i in COVID_FASTQ/*.fastq.gz
> > do
> >    count=$(gunzip -c $i | echo $((`wc -l`/4)))
> > 
> >     echo "============================================================="
> >     echo "$i"
> >     echo "============================================================="
> >     
> >     echo "Nombre de reads du fichier :" "$count"
> > 
> >     if [ "$count" -lt "$limit" ]
> >     then
> >         echo "/!\\ Il y a moins de 2000000 de reads dans le fichier"
> >     fi
> > 
> > done
> > ```
{:.answer}

#### Stratégie 2

Nous allons compter cette fois le nombre de lignes qui ne contiennent que + . D'apèrs la documentation, la 3e ligne pour des reads récents séquencés par illumina ne contient que le signe `+`.

Nous allons donc utiser grep pour rechercher toutes les lignes commençant (`^`) par la signe `\+` (le \ permet d'échapper le signe + qui est un caractère spécial) et qui termine par un plus `$`. 

> ** Solution**
> > ``` bash
> > #!/bin/bash
> > 
> > #------------------------------------------------------------------------------
> > # Objectifs du script :  
> > #     - Explorer les fichiers fastq.gz d'intérêt
> > # Auteurs: Hélène Chiapello & Thomas Denecker
> > # Affiliation: IFB
> > # Organisme : SARS-CoV-2
> > # Date: Mars 2021
> > # Compter le nombre de reads et alerter si le nombre est trop faible afficher un message d'alerte
> > #------------------------------------------------------------------------------
> > 
> > limit=2000000
> > 
> > for i in COVID_FASTQ/*.fastq.gz
> > do
> >     count=$(gunzip -c $i | echo $((`grep -i "^\+$" | wc -l` )))
> > 
> >     echo "============================================================="
> >     echo "$i"
> >     echo "============================================================="
> >     
> >     echo "Nombre de reads du fichier :" "$count"
> > 
> >     if [ "$count" -lt "$limit" ]
> >     then
> >         echo "/!\\ Il y a moins de 2000000 de reads dans le fichier"
> >     fi
> > 
> > done
> > ```
{:.answer}

**Pour aller plus loin**

Nous vous proposons 
- de mettre en paramètre du script sur la ligne de commande le seuil (nombre de reads minimal) à obtenir par fichier
- d'écrire les résultats de cette analyse (seuil utilisé, puis avec 1 ligne par fichier : le nom du fichier fastq, nombre de lectures totales dans le fichier et warning si le seuil minimum n'est pas atteind dans ce fichier de sortie)

**Note : Pour les utilisateurs de Mac qui ne disposent pas de wget**

La commande n'est plus installée par défaut dans le terminal mac. Nous vous conseillons de l'installer à l'aide de [Homebrew](https://brew.sh/index_fr) :

``` bash
# Installation de Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Installation de wget 
brew install wget
```

