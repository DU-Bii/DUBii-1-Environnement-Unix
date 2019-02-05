# Exemple de mise en pratique pour sur de l'analyse de données RNAseq
# Lancement des analyses sur le cluster NNCR en utilisant des scripts bash

## Connnection au cluster NNCR IFB et chargement des environnements nécessaires

> > ```bash
> > $ ssh <username>@core.cluster.france-bioinformatique.fr
> > ```

> > ```bash
> > module load conda
> > source activate eba_rnaseq_ref-2018
> >```

## Le jeu de données

On dispose de 2 échantillons de reads pairés de E. coli : WT (Wild Type) et dFNR (mutant du gène FNR).  
Il y a 2 répliques par échantillons (soient 4 échantillons et 8 fichiers, les paires de reads étant stockées dans 2 fichiers séparés) :

> > ```bash
> > $ ls  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/*.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/dFNR1_1.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/dFNR1_2.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/dFNR2_1.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/dFNR2_2.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/WT1_1.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/WT1_2.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/WT2_1.fastq
> >  /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq/WT2_2.fastq
> > 
> >```

## Première exemple : contrôle qualité

Nous allons utiliser un premier script bash pour lancer sur le cluster de l'IFB 8 calculs fastqc correspondant aux 8 fichiers à analyser

> > ```bash
> >  $ cat fastqc_myfiles.sh  
> >  #! /bin/bash  

> >  data=$(ls $1/*.fastq)   

> >  for fastqc_file in ${data[@]}   
> >  do  
          echo "srun srun fastqc --quiet  $fastqc_file -o ./fastqc-results/ 2>> fastqc.err "
> >       srun fastqc --quiet  $fastqc_file -o ./fastqc-results/ 2>> fastqc.err  &   
> >  done  
> >```

Pour lancer ce script on utilise la commande suivante :

> > ```bash  
> >     ./fastqc_myfiles.sh /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/RNA-seq/fastq
> >  
> >```

**Questions** :   
- Combien de jobs sont lancés sur le cluster ?  
- Comment suivre l'éxécution des jobs ?  
- Où seront produits les fichiers résulats de la commande `fastqc`?  
- Que veut dire "2>> fastqc.err" ?  

## Deuxième exemple : mapping des reads sur le génome de E. coli

Nous allons utiliser le logiciel **STAR** pour aligner les reads RNAseq sur le génome de E. coli.  

Pour pouvoir utiliser STAR il faut d'abord indexer le génome de référence.  

Regarder la documentaion de STAR  
> > ```bash  
> > $ STAR --help | less
> >```

L'usage est :  
 `Usage: STAR  [options]... --genomeDir REFERENCE   --readFilesIn R1.fq R2.fq 
  Spliced Transcripts Alignment to a Reference (c) Alexander Dobin, 2009-2015`

Nous allons commencer par créer un répertoire pour le génome de référence indexé :  
> > ```bash  
> >  mkdir ./Ecoli_star
> >```

Puis nous lancons la commande d'indexation du génome sur le cluster :  

> > ```bash  
> >  srun STAR --runMode genomeGenerate --genomeDir ./Ecoli_star --genomeFastaFiles /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/genome/Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.dna.chromosome.Chromosome.fa  --runThreadN 4 --sjdbGTFfile /shared/projects/du_bii_2019/data/study_cases/Escherichia_coli/bacterial-regulons_myers_2013/genome/Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.gtf
> >```



