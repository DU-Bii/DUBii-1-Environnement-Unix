# Partie 2.3 : Notions sur les expressions régulières

## Les expressions de bases  

Une expression régulière (en anglais *Regular Expression*) 
est une chaîne de caractères décrivant un ensemble de chaîne de
caractères.

On appelle également une expression regulière "regex" ou "motif"
(*pattern* en anglais).

De nombreux programmes utilisent les expressions régulières
(par exemple `sed`, `grep`, `vi`, ...) mais il est important 
de noter que leur syntaxe peut varier d'un programme à l'autre.

Le design d'expressions régulières peut rapidement s'avérer complexe et nécessite un savoir-faire certain.

Cette possibilité illustre cependant la puissance de l'environnement Unix 
pour spécifier des recherches et actions complexes en utilisant des lignes 
de commande concises.  

Les expressions régulières vont se baser sur des caractères spéciaux ou métacaractères :

- `.` correspond à n'importe quel caractère  
- `*` correspond à une répétition de 0 à n occurences (déconseillé) 
- `+` correspond à une répétition de 1 à n occurences 
- les caractères entre crochets (`[ ]`) correspondent à un ensemble de valeurs possibles (intervale ou explicites par exemple `[A-D]` est équivalent à [A,B,C,D]
- `^` indique une recherche d'un motif en début de ligne  
- `$` indique une recherche d'un motif en fin de ligne  

**Question :** Rechercher tous les noms de gènes nommés dnaA, dnaB, dnaC
et dnaD dans le fichier
`Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3`

> **Solution :**  
> > ```bash 
> > $ grep -e "dna[A-D]" Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3 
> > ```
{:.answer}


Pour aller plus loin :
- Tutorial sur les expressions régulières :  https://librarycarpentry.org/lc-data-intro/04-regular-expressions/  
- Site pour tester une expression régulère : https://regex101.com  

## sed  

`sed` (stream editor) est éditeur de texte non interactif permettant de filtrer et transformer les lignes du ou des fichier donnés en argument. La commande ne modifie pas le(s) fichier(s) traité(s)et écrit le résultat sur la sortie standard.  
La commande `sed` est très utile car elle permet de réaliser des commandes complexes sur des gros fichiers en utilisant des expressions régulières.  

**Syntaxe** : `sed -e [expression] <fichier-a-traiter>`

La partie `expression` peut contenir des fonctions de filtrage ou de transformation des lignes du fichier-a-traiter  
Nous ne verrons ici que quelques cas d'utilisation très courants en bioinformatique.  

### Exemple 1 : Remplacer toutes les occurences d'une chaine de caractères dans un fichier  
Remplaçons toutes les occurences de `Chromosome` par `chr` dans le fichier Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3   
Pour cela on utilise la fonction de subsitution *s*  
`sed 's/Chromosome/chr/g' Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3 > Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chr.gff3`

### Exemple 2 : Supprimer toutes les occurences d'une chaine de caractères dans un fichier  
Supprimons toutes les lignes contenant le nom `oriC` dans le fichier Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3  
Pour cela on utilise la fonction de suppression *d*  
`sed '/oriC/d' Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome.gff3  > Escherichia_coli_str_k_12_substr_mg1655.ASM584v2.37.chromosome.Chromosome_wo_oriC.gff`


Suite : [Espace de stockage, compression et archivage des données](05_tar.md)
