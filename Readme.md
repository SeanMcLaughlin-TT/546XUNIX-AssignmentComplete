> +#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes.txt`

```
wc fang_et_al_genotypes.txt
du -h fang_et_al_genotypes.txt
awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt
```

By inspecting this file I learned that:

1. The file contains 2,783 lines with a total of 2,744,038 words after using wc command
2. File size is 6.1M after using du -h command
3. Has 986 columns in the file using an awk script

###Attributes of `snp_position.txt`

```
wc snp_position.txt
du -h snp_position.txt
grep -v "^#" snp_position.txt | awk -F "\t" '{print NF; exit}'
```

By inspecting this file I learned that:

1. The file contains 984 lines with a total of 13,198 words after using wc command
2. The files size is 38K after using du -h command
3. After accounting for headers using grep, the number of columns is 15 using an awk script

##Data Processing

###Maize Data
Formatting Data
```
Head -n 1 fang_et_al_genotypes.txt > FangHeaderFile
grep "ZMM" fang_et_al_genotypes.txt | cut -f 1-3 > MaizeIndv
cat FangHeaderFile MaizeIndv > CatMaizeFile
awk -f transpose.awk CatMaizeFile > transposed_Maize_Genotypes.txt
sort -k1,1 transposed_Maize_Genotypes.txt > Sorted_MaizeGT
Sort -k1,1 snp_position.txt > SortedSNPs.txt
join -1 1 -1 1 Sorted_MaizeGT.txt SortedSNPs.txt > CombinedMaizedata.txt
```
Chromosome Outputs
```
cut -f 2 CombinedMaizedata.txt |sed 's/ /?/g' CombinedMaizedata.txt | grep "1" CombinedMaizedata.txt | sort -k1,2n CombinedMaizedata.txt > M_Chr_1_Inc
```
Repeat for each Chromosome 1-10
```
cut -f 2 CombinedMaizedata.txt | sed 's/ /-/g' CombinedMaizedata.txt | grep "1" CombinedMaizedata.txt | sort -r -k1,2n CombinedMaizedata.txt > M_Chr_1_Dec
```
Repeat for each Chromosome 1-10
```
cut -f 3 CombinedMaizedata.txt | grep "unknown" CombinedMaizedata.txt > UnknMaizeSNPs.txt
cut -f 2 CombinedMaizedata.txt | grep "Multiple" CombinedMaizedata.txt > MultiMaizeSNPs.txt
```
My Code first sets up the data by formatting the Fang data to be able to be joined together with the SNP data, I did not pipe the commands to create intermediate files that I could check for accuracy and start over at any intermediate point. Then I created piped command line which produces a file that can be input for each chromosome and to the specifications of the assignment. Lastly, two different piped command lines that extract both the unknown and multiple SNP data.


###Teosinte Data

```
Head -n 1 fang_et_al_genotypes.txt > FangHeaderFile
grep "ZMP" fang_et_al_genotypes.txt | cut -f 1-3 > TeosinteIndv 
Cat FangHeaderFile TeosinteIndv > CatTeosinteFile
awk -f transpose.awk CatTeosinteFile > transposed_Teosinte_Genotypes.txt
sort -k1,1 transposed_Teosinte_Genotypes.txt > Sorted_TeosinteGT
Sort -k1,1 snp_position.txt > SortedSNPs.txt
join -1 1 -1 1 Sorted_TeosinteGT.txt SortedSNPs.txt > CombinedTeosintedata.txt
```
Chromosome Outputs
```
cut -f 2 CombinedTeosintedata.txt |sed 's/ /?/g' CombinedTeosintedata.txt | grep "1" CombinedTeosintedata.txt | sort -k1,2n CombinedTeosintedata.txt > T_Chr_1_Inc
```
Repeat for each Chromosome 1-10
```
cut -f 2 CombinedTeosintedata.txt | sed 's/ /-/g' CombinedTeosintedata.txt | grep "1" CombinedTeosintedata.txt | sort -r -k1,2n CombinedTeosintedata.txt > T_Chr_1_Dec
```
Repeat for each Chromosome 1-10
```
cut -f 3 CombinedTeosintedata.txt | grep "unknown" CombinedTeosintedata.txt > UnknTeosinteSNPs.txt
cut -f 2 CombinedTeosintedata.txt | grep "Multiple" CombinedTeosintedata.txt > MultiTeosinteSNPs.txt
```
This code is set up exactly the same as the Maize individuals but with a different grep command to separate the Teosinte individuals which is then combined the same with the SNP data. It is then put through the same programs since the same data processing is required for Teosinte individuals as well which has been done here.
> 