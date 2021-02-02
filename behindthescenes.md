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

## 1-Feb-2021
1. Testing trinity assembly
``` sh
[dbarshis@coreV2-25-019 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/QCFastqs
[dbarshis@coreV2-25-019 QCFastqs]$ cat TrinityTest21Files.sh 
#!/bin/bash -l

#SBATCH -o djb21fileTrinityTest.txt
#SBATCH -n 32
#SBATCH -p himem
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=djb21fileTrinityTest

enable_lmod
module load container_env trinity

crun Trinity --seqType fq --max_memory 768G --normalize_reads --single RI_B_01_14_clippedtrimmed.fastq,RI_B_01_18_clippedtrimmed.fastq,RI_B_01_22_clippedtrimmed.fastq,RI_B_02_14_clippedtrimmed.fastq,RI_B_02_18_clippedtrimmed.fastq,RI_B_02_22_clippedtrimmed.fastq,RI_B_03_14_clippedtrimmed.fastq,RI_B_03_18_clippedtrimmed.fastq,RI_B_03_22_clippedtrimmed.fastq,RI_B_04_14_clippedtrimmed.fastq,RI_B_04_18_clippedtrimmed.fastq,RI_B_04_22_clippedtrimmed.fastq,RI_B_05_14_clippedtrimmed.fastq,RI_B_05_18_clippedtrimmed.fastq,RI_B_05_22_clippedtrimmed.fastq,RI_B_06_14_clippedtrimmed.fastq,RI_B_06_18_clippedtrimmed.fastq,RI_B_06_22_clippedtrimmed.fastq,RI_B_07_14_clippedtrimmed.fastq,RI_B_07_18_clippedtrimmed.fastq,RI_B_07_22_clippedtrimmed.fastq --CPU 32
[dbarshis@coreV2-25-019 QCFastqs]$ sbatch TrinityTest21Files.sh 
Submitted batch job 9271931
```
2. Testing num mapped reads to full ref for my RI_B_14 test set
``` sh
[dbarshis@coreV2-25-019 RI_B_14]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/RI_B_14
[dbarshis@coreV2-25-019 RI_B_14]$ cat bowtiealn_fullref.sh 
#!/bin/bash -l

#SBATCH -o djbowtie2fullref.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=newbowtie

module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmed.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/barshislab/Hannah/2018-Feb_Berkeley/sandbox/Barshis/trinity_out_dir/HEA_AstrangiaAssembly -U $i \
> ${i%_clippedtrimmed.fastq}_2fullref.sam --no-unal -k 5; done

[dbarshis@coreV2-25-019 RI_B_14]$ sbatch bowtiealn_fullref.sh 
Submitted batch job 9271936
```