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
