
# Partie 2.5: rsync

**Syntax**: `rsync [options] <SOURCE> <DESTINATION>`

`rsync` est un outil très puissant servant à faire notamment de la copie et 
du transfert de fichier.
Sa particularité est qu'il est capable de détecter des fichiers ou dossier
ajoutés/supprimés/modifiés dans la `SOURCE` et de ne copy que ceux-ci dans
le répertoire de `DESTINATION`.

Cette une différence majeure avec `cp` qui lui copie `SOURCE` vers `DESTINATION`
de manière brutale.

Cette capacité à ne transférer que la partie "utile" de la `SOURCE` permet
d'économiser un temps précieux lors de la copie de fichiers volumineux.

`rsync` a de nombreuses options, les plus utilisées étant :

- `-a, --archive` mode archive (typiquement ce qu'on veut 95% du temps)
- `-v, --verbose` mode verbeux  (afficher les éléments au fur et à mesure qu'il sont copiés)
- `-P, --progress` montre l'avancement, fichier par fichier
- `-h, --human-readable` montre les tailles au format humain (à utiliser avec `-P`)
- `-x, --exclude <MOTIF>` exclut des éléments de la copie.


- [Copie simple](#copie-simple)
- [Copie depuis/vers une machine distance](#copie-depuis-vers-une-machine-distante)
- [Copie de fichiers volumineux](#copie-de-fichiers-volumineux)

## Copie simple

```bash
$ rsync -av study-cases /data/
building file list ... done
study-cases/
study-cases/.gitignore
study-cases/LICENSE.txt
study-cases/README.md -> study-cases.md
study-cases/_config.yml
study-cases/study-cases.Rproj
study-cases/study-cases.html
study-cases/study-cases.md
study-cases/.git/
study-cases/.git/HEAD
study-cases/.git/config
study-cases/.git/description
study-cases/.git/index
study-cases/.git/packed-refs
study-cases/.git/branches/
study-cases/.git/hooks/
study-cases/.git/hooks/applypatch-msg.sample
study-cases/.git/hooks/commit-msg.sample
study-cases/.git/hooks/post-update.sample
study-cases/.git/hooks/pre-applypatch.sample
study-cases/.git/hooks/pre-commit.sample
study-cases/.git/hooks/pre-push.sample
study-cases/.git/hooks/pre-rebase.sample
study-cases/.git/hooks/prepare-commit-msg.sample
study-cases/.git/hooks/update.sample
study-cases/.git/info/
study-cases/.git/info/exclude
study-cases/.git/logs/
study-cases/.git/logs/HEAD
study-cases/.git/logs/refs/
study-cases/.git/logs/refs/heads/
study-cases/.git/logs/refs/heads/master
study-cases/.git/logs/refs/remotes/
study-cases/.git/logs/refs/remotes/origin/
study-cases/.git/logs/refs/remotes/origin/HEAD
study-cases/.git/objects/
study-cases/.git/objects/info/
study-cases/.git/objects/pack/
study-cases/.git/objects/pack/pack-f2c3e9935f7d62674c4ff06d5bad60551477f2ae.idx
study-cases/.git/objects/pack/pack-f2c3e9935f7d62674c4ff06d5bad60551477f2ae.pack
study-cases/.git/refs/
study-cases/.git/refs/heads/
study-cases/.git/refs/heads/master
study-cases/.git/refs/remotes/
study-cases/.git/refs/remotes/origin/
study-cases/.git/refs/remotes/origin/HEAD
study-cases/.git/refs/tags/
study-cases/Arabidopsis_thaliana/
study-cases/Arabidopsis_thaliana/README.md
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/data sheet 1.pdf
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised Suppl Table S1 Roots.xlsx
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised Suppl Table S2 Root Exudates JL140617.xlsx
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised Suppl Table S3 Analytical Characterization.xlsx
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised Suppl Table S4 Root exudate proteome.xlsx
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised_Suppl_Table_S1_Roots.txt
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised_Suppl_Table_S2_Root_Exudates_JL140617.txt
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised_Suppl_Table_S3_Analytical_Characterization.txt
study-cases/Arabidopsis_thaliana/metabo_proteo_Strehmel_2017/Strehmel revised suppl tables/Revised_Suppl_Table_S4_Root_exudate_proteome.txt
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM10_ESM.txt
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM10_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM12_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM13_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM14_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM15_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM16_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM17_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM18_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM19_ESM.txt
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM19_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM1_ESM.txt
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM1_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM2_ESM.txt
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM2_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM3_ESM.txt
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM3_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/12870_2016_726_MOESM4_ESM.xlsx
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/GSM1388555_WT_0.Gene.rpkm.txt.gz
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/GSM1388556_WT_1.Gene.rpkm.txt.gz
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/GSM1388557_WT_8.Gene.rpkm.txt.gz
study-cases/Arabidopsis_thaliana/transcripto_proteo_metabo_Liang_2016/README.md
study-cases/Escherichia_coli/
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/README.md -> bacterial-regulons_myers_2013.md
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/bacterial-regulons_myers_2013.html
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/bacterial-regulons_myers_2013.md
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq/
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq/FNR1_vs_input1_cutadapt_bowtie2_homer.bed
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq/FNR1_vs_input1_cutadapt_bowtie2_macs2.bed
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq/FNR_200bp.wig
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/ChIP-seq/input_200bp.wig
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/RNA-seq/
study-cases/Escherichia_coli/bacterial-regulons_myers_2013/data/RNA-seq/cutadapt_bwa_featureCounts_all.tsv
study-cases/Escherichia_coli/genome-metabolome_fuhrer_2017/
study-cases/Escherichia_coli/genome-metabolome_fuhrer_2017/.gitignore
study-cases/Escherichia_coli/genome-metabolome_fuhrer_2017/README.md -> genome-metabolome_fuhrer_2017.md
study-cases/Escherichia_coli/genome-metabolome_fuhrer_2017/genome-metabolome_fuhrer_2017.html
study-cases/Escherichia_coli/genome-metabolome_fuhrer_2017/genome-metabolome_fuhrer_2017.md
study-cases/Homo_sapiens/
study-cases/Homo_sapiens/TCGA_study-case/
study-cases/Homo_sapiens/TCGA_study-case/README.md -> TCGA_study-case.md
study-cases/Homo_sapiens/TCGA_study-case/SubAnnot.R
study-cases/Homo_sapiens/TCGA_study-case/TCGA_study-case.html
study-cases/Homo_sapiens/TCGA_study-case/TCGA_study-case.md
study-cases/Homo_sapiens/TCGA_study-case/subtypes_annotation.txt
study-cases/img/
study-cases/img/CC-BY-SA.png
```

Si seulement un fichier est modifié et qu'on relance la copie, seulement ledit
fichier est copié :

```bash
$ # Modifying README.md
$ echo "modifying README" >> study-cases/study-cases.md
$ # Making the copy again
$ rsync -av study-cases /data/
sending incremental file list
study-cases/study-cases.md

sent 8,153 bytes  received 67 bytes  16,440.00 bytes/sec
total size is 50,480,444  speedup is 6,141.17
```


## Copie depuis/vers une machine distance]

`rsync` peut être utilisé comme alternative (plus efficace) à `scp` :


**Copie depuis une machine distante**:

```bash
rsync -a login@server.domain:study-cases .
```

**Copie vers une machine distante**:

```bash
rsync -a study-cases login@server.domain:
```


## Copie de fichiers volumineux

Lorsqu'on copie des fichiers volumineux, il peut être intéressant d'utiliser
les options `-Ph` pour voir l'avancement du processus :

```bash
$ rsync -aPh my-big-file.tar.gz login@server.domain:
building file list ...
1 file to consider
my-big-file.tar.gz
     301.75M  22%   71.97MB/s    0:00:14
```








