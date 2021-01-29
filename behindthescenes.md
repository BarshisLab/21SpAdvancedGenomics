# behind the scenes
## 29-Jan-2021
 1. Finding and uploading Hannah's published reference assembly

```sh
(base) danbarshis@BIOLLBB0 final_annotated_assembly % pwd
/Users/danbarshis/dansstuff/MyPapers/2020_Aichelman_and_Barshis_2020_PeerJ/Astrangia_PopGen/2-BuildAnnotateReferenceTranscriptome/final_annotated_assembly
(base) danbarshis@BIOLLBB0 final_annotated_assembly % ls
Assembly_GoodCoralSymbiont_suffixed.fasta
Assembly_GoodCoralSymbiont_suffixed_totalannotated.txt
```
2. building updated bowtie reference assembly from Hannah's published assembly

``` sh
[dbarshis@coreV1-22-016 refassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly
[dbarshis@coreV1-22-016 refassembly]$ sbatch bowtiebuild.sh
Submitted batch job 9270998
```
3. testing bowtie2 alignment against published reference assembly

``` sh
[dbarshis@turing1 RI_B_14]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/RI_B_14
[dbarshis@turing1 RI_B_14]$ cat bowtiealn.sh 
#!/bin/bash -l

#SBATCH -o djbowtie2.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=newbowtie

module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmed.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/Apoc_hostsym -U $i \
> ${i%_clippedtrimmedfilterd.fastq}.sam --no-unal -k 5; done

[dbarshis@turing1 RI_B_14]$ sbatch bowtiealn.sh 
Submitted batch job 9271002
    ```