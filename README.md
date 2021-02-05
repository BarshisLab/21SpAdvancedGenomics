2021_Spring_Dan's Advanced Genomics Notebook
================
# How to make a notebook file on git
[Here's an epic example on markdown syntax](https://github.com/eriqande/thompson-et-al-2020-chinook-salmon-migration-timing/blob/master/README.md) and reproducible research from Eric Anderson at NOAA. Click on the "raw" box to see the raw text file
1. Create a new repository on the github website under your user account
2. make a new local directory with the same name as your repository online

``` sh
(base) danbarshis@BIOLLBB0 21-01_Sp_AdvancedGenomicsDataAnalysis % mkdir 21SpDansAdvancedGenomicsLog
```

3. cd into that local directory

``` sh
(base) danbarshis@BIOLLBB0 21-01_Sp_AdvancedGenomicsDataAnalysis % cd 21SpDansAdvancedGenomicsLog
```

4. create a README.md file in your text editor using the [markdown syntax](https://www.markdownguide.org/basic-syntax). This will be your log/notebook file and will be what you update and push to git each session
* use \# for main headers
# main headers
* use \## for sub headers
## sub headers
5. save your README.md and follow the following steps to push it to your git repository **NOTE** change the web address to your specific git repo

``` sh
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git init
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git add README.md 
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git commit -m 'first commit'
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git branch -M main
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git remote add origin https://github.com/BarshisLab/21SpDansAdvancedGenomicsLog.git
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git push -u origin main
```

* below is the output I got when I went through the process

``` sh
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git init
Initialized empty Git repository in /Users/danbarshis/dansstuff/Projeks/ODU/CoursesTaught_Taken/21-01_Sp_AdvancedGenomicsDataAnalysis/DemoFolder/21SpDansAdvancedGenomicsLog/.git/
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git add README.md 
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git commit -m 'first commit'
[master (root-commit) 32f7384] first commit
 1 file changed, 17 insertions(+)
 create mode 100644 README.md
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git branch -M main
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git remote add origin https://github.com/BarshisLab/21SpDansAdvancedGenomicsLog.git
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git push -u origin main
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 569 bytes | 569.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/BarshisLab/21SpDansAdvancedGenomicsLog.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

6. Then, to update your notebook/log each session, just edit your README.md file locally in your text editor and push any updates to your github page like so

``` sh
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git add README.md 
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git commit -m 'updating readme'
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git push -u origin main
```

7. To then enable a github pages version of your notebook, follow the instructions [here](https://nicolas-van.github.io/easy-markdown-to-github-pages/) after [creating/signing up for/enabling](https://pages.github.com/) a github pages account

## Day02 Exercises 2021-Jan-22

Exercise day02:
1. Logon to the cluster @turing.hpc.odu.edu

``` sh
[dbarshis@turing1 dan]$ ls
db_exercise1.txt  groundrules.txt  scripts
```

2. Make a directory in your course workspace called data
``` sh
[dbarshis@turing1 dan]$ mkdir data
```

3. Make a directory called exercises in your data directory
``` sh
[dbarshis@turing1 dan]$ mkdir exercises
```

4. execute a pwd command and start a log of your commands with a header for today's date in your README.md github logfile in your workspace

``` sh
[dbarshis@turing1 exercises]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/exercises
```

5. cp the Exercise2.fasta.gz and Exercise2.fastq.tar.gz files into your exercises directory from the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02 directory

``` sh
[dbarshis@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02/Exercise2.fast* ./
[dbarshis@turing1 exercises]$ ls
db_exercise1.txt  Exercise2.fasta.gz  Exercise2.fastq.tar.gz
[dbarshis@turing1 exercises]$ ls -alh
total 13M
drwxrwxrwx 2 dbarshis users  110 Jan 21 23:55 .
drwxrwxrwx 5 dbarshis users  107 Jan 21 23:51 ..
-rwxrwxrwx 1 dbarshis users   75 Jan 20 15:05 db_exercise1.txt
-rwxr-xr-x 1 dbarshis users 4.3M Jan 21 23:55 Exercise2.fasta.gz
-rwxr-xr-x 1 dbarshis users 4.3M Jan 21 23:55 Exercise2.fastq.tar.gz
```

6. unzip and untar the files
``` sh
[dbarshis@turing1 exercises]$ gunzip -c Exercise2.fasta.gz > Exercise2.fasta
[dbarshis@turing1 exercises]$ ls
db_exercise1.txt  Exercise2.fasta  Exercise2.fasta.gz  Exercise2.fastq.tar.gz
[dbarshis@turing1 exercises]$ ls -alh
total 37M
drwxrwxrwx 2 dbarshis users  143 Jan 21 23:56 .
drwxrwxrwx 5 dbarshis users  107 Jan 21 23:51 ..
-rwxrwxrwx 1 dbarshis users   75 Jan 20 15:05 db_exercise1.txt
-rwxrwxrwx 1 dbarshis users  17M Jan 21 23:56 Exercise2.fasta
-rwxr-xr-x 1 dbarshis users 4.3M Jan 21 23:55 Exercise2.fasta.gz
-rwxr-xr-x 1 dbarshis users 4.3M Jan 21 23:55 Exercise2.fastq.tar.gz
[dbarshis@turing1 exercises]$ tar -zxvf Exercise2.fastq.tar.gz 
Exercise2.fastq
[dbarshis@turing1 exercises]$ ls -alh
total 63M
drwxrwxrwx 2 dbarshis users  176 Jan 21 23:59 .
drwxrwxrwx 5 dbarshis users  107 Jan 21 23:51 ..
-rwxrwxrwx 1 dbarshis users   75 Jan 20 15:05 db_exercise1.txt
-rwxrwxrwx 1 dbarshis users  17M Jan 21 23:56 Exercise2.fasta
-rwxr-xr-x 1 dbarshis users 4.3M Jan 21 23:55 Exercise2.fasta.gz
-rw-r--r-- 1 dbarshis users  18M Sep  2  2015 Exercise2.fastq
-rwxr-xr-x 1 dbarshis users 4.3M Jan 21 23:55 Exercise2.fastq.tar.gz
```

7. add these commands to your notebook file
  * You\'re looking at it buddy!

8. calculate how many sequences are in each file and add these results to your notebook file
``` sh
[dbarshis@turing1 exercises]$ head -1 Exercise2.fasta
>scaffold10078|size20675
[dbarshis@turing1 exercises]$ grep -c '>' Exercise2.fasta
138
[dbarshis@turing1 exercises]$ head -1 Exercise2.fastq
@HS3:541:HAYTUADXX:1:1101:1297:1938 1:N:0:AGTTCC
[dbarshis@turing1 exercises]$ grep -c '@HS3' Exercise2.fastq
61304
[dbarshis@turing1 exercises]$ wc -l Exercise2.fastq
245216 Exercise2.fastq
[dbarshis@turing1 exercises]$ echo 245216/4 | bc -l
61304.00000000000000000000
```

9. cp the avg_cov_len_fasta_advbioinf.py from the /cm/shared/courses/dbarshis/21AdvGenomics/scripts directory into your class scripts directory

``` sh
[dbarshis@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py ../scripts/
```

10. start an interactive compute session and re-navigate to your exercises directory

``` sh
[dbarshis@turing1 exercises]$ salloc
salloc: Pending job allocation 9268620
salloc: job 9268620 queued and waiting for resources
salloc: job 9268620 has been allocated resources
salloc: Granted job allocation 9268620
[dbarshis@coreV1-22-005 exercises]$ 
```

11. run the avg_cov_len_fasta_DJB.py script on your Exercise2.fasta file by typing the path to the script followed by the Exercise2.fasta file name

``` sh
[dbarshis@coreV1-22-005 exercises]$ ../scripts/avg_cov_len_fasta_advbioinf.py Exercise2.fasta
The total number of sequences is 138
The average sequence length is 126640
The total number of bases is 17476447
The minimum sequence length is 1122
The maximum sequence length is 562680
The N50 is 187037
Median Length = 92612
contigs < 150bp = 0
contigs >= 500bp = 138
contigs >= 1000bp = 138
contigs >= 2000bp = 135
```

12. did you add all these entries to your notebook file, including the results of the script?
  * **Yup!**

13. push your notebook file to your github page

``` sh
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git add README.md 
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git commit -m 'updating readme with day02 exercises'
[main 21e0267] updating readme with day02 exercises
 1 file changed, 101 insertions(+), 1 deletion(-)
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git push -u origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 2.53 KiB | 2.53 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/BarshisLab/21SpDansAdvancedGenomicsLog.git
   e7b36c3..21e0267  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

## Day02 Homework 2021-Jan-22

1. Write an sbatch script to cp the files /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/ into your own data directory

``` sh
[dbarshis@coreV1-22-005 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@coreV1-22-005 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@coreV1-22-005 data]$ nano DansFQCp.sh
```

2. Add the content of your sbatch script to your logfile
``` sh
[dbarshis@coreV1-22-005 data]$ cat DansFQCp.sh 
#!/bin/bash -l

#SBATCH -o dansfastqcopy.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=DansFastqCp

cp /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/*.fastq.gz /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/
```

3. submit the slurm script (sbatch scripname.sh) and verify that it's working (by squeue -u yourusername multiple times and checking the destination directory to make sure the files are being created)

``` sh
[dbarshis@coreV1-22-005 data]$ sbatch DansFQCp.sh 
Submitted batch job 9268621
[dbarshis@coreV1-22-005 data]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9268621      main DansFast dbarshis  R       0:18      1 coreV1-22-005 
[dbarshis@coreV1-22-005 data]$ ls
dansfastqcopy.txt                  HADB01-B_S18_L002_R1_001.fastq.gz  HADB01-E_S21_L002_R1_001.fastq.gz
DansFQCp.sh                        HADB01-C_S19_L002_R1_001.fastq.gz  HADB01-F_S22_L002_R1_001.fastq.gz
HADB01-A_S17_L002_R1_001.fastq.gz  HADB01-D_S20_L002_R1_001.fastq.gz
```

4. Make sure this is all documented on your github notebook
  * Yup

5. Write a sbatch script to gunzip all the fastq.gz files

``` sh
[dbarshis@turing1 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@turing1 data]$ cat DansFQGunzip.sh 
#!/bin/bash -l

#SBATCH -o dansfastqgunzip.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=Fastqgunzip

gunzip ./*.fastq.gz

[dbarshis@turing1 data]$ sbatch ./DansFQGunzip.sh 
Submitted batch job 9268704
[dbarshis@turing1 data]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9268704      main Fastqgun dbarshis  R       0:10      1 coreV3-23-024 
[dbarshis@turing1 data]$ ls
dansfastqcopy.txt                  HADB02-N_S46_L003_R1_001.fastq.gz  HADB04-P_S80_L005_R1_001.fastq.gz
dansfastqgunzip.txt                HADB02-O_S47_L003_R1_001.fastq.gz  HADB05-A_S81_L006_R1_001.fastq.gz
DansFQCp.sh                        HADB02-P_S48_L003_R1_001.fastq.gz  HADB05-B_S82_L006_R1_001.fastq.gz
DansFQGunzip.sh                    HADB03-A_S49_L004_R1_001.fastq.gz  HADB05-C_S83_L006_R1_001.fastq.gz
HADB01-A_S17_L002_R1_001.fastq     HADB03-B_S50_L004_R1_001.fastq.gz  HADB05-D_S84_L006_R1_001.fastq.gz
```

6. Push your notebook file to your github page (document everything on your github notebook, drink a beer, and realize that all that work was just to get the data organized to start looking at it!)

  * Done, except the beer, too early
  
## Day 03 Homework 27-Jan-2021
* day 03 homework
``` sh
[dbarshis@turing1 dan]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan
```
1. cp the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03 directory (and files) to your sandbox
``` sh
[dbarshis@turing1 dan]$ cp -r /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/ ./
```
2. mkdir a fastq directory in your data directory and mv all the .fastq files into this directory
``` sh
[dbarshis@turing1 dan]$ cd data
[dbarshis@turing1 data]$ mkdir fastq
[dbarshis@turing1 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@turing1 data]$ mv *.fastq ./fastq/
```
3. cp the renamingtable_complete.txt from the day03 directory into your fastq directory and the /cm/shared/courses/dbarshis/21AdvGenomics/scripts/renamer_advbioinf.py script into your sandbox scripts folder and less the new script and check out the usage statement
``` sh
[dbarshis@turing1 data]$ cp ../day03/renamingtable_complete.txt ./fastq/
[dbarshis@turing1 data]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/renamer_advbioinf.py ../scripts/
[dbarshis@turing1 data]$ head ../scripts/renamer_advbioinf.py 
#!/usr/bin/env python
####usage renamer.py renamingtable
#### this script take the entries in the first column of table and renames (mv's) them to files with the names in the second column
```
4. run the renamer_advbioinf.py script in your fastq folder using the renamingtable_complete.txt as practice and verify the output to the screen by hand
``` sh
[dbarshis@turing1 data]$ cd fastq/
[dbarshis@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq
[dbarshis@turing1 fastq]$ ../../scripts/renamer_advbioinf.py renamingtable_complete.txt 
mv HADB01-A_S17_L002_R1_001.fastq VA_W_01_14.fastq
mv HADB01-B_S18_L002_R1_001.fastq VA_B_01_14.fastq
mv HADB01-C_S19_L002_R1_001.fastq RI_W_01_14.fastq
mv HADB01-D_S20_L002_R1_001.fastq RI_B_01_14.fastq
mv HADB01-E_S21_L002_R1_001.fastq VA_W_01_22.fastq
mv HADB01-F_S22_L002_R1_001.fastq VA_B_01_22.fastq
mv HADB01-G_S23_L002_R1_001.fastq RI_W_01_22.fastq
mv HADB01-H_S24_L002_R1_001.fastq RI_B_01_22.fastq
mv HADB01-I_S25_L002_R1_001.fastq VA_W_01_18.fastq
mv HADB01-J_S26_L002_R1_001.fastq VA_B_01_18.fastq
mv HADB01-K_S27_L002_R1_001.fastq RI_W_01_18.fastq
mv HADB01-L_S28_L002_R1_001.fastq RI_B_01_18.fastq
mv HADB01-M_S29_L002_R1_001.fastq VA_W_08_SNP.fastq
mv HADB01-N_S30_L002_R1_001.fastq VA_B_09_SNP.fastq
mv HADB01-O_S31_L002_R1_001.fastq RI_W_08_SNP.fastq
mv HADB01-P_S32_L002_R1_001.fastq RI_B_08_SNP.fastq
mv HADB02-A_S33_L003_R1_001.fastq VA_W_02_14.fastq
mv HADB02-B_S34_L003_R1_001.fastq VA_B_02_14.fastq
mv HADB02-C_S35_L003_R1_001.fastq RI_W_02_14.fastq
mv HADB02-D_S36_L003_R1_001.fastq RI_B_02_14.fastq
mv HADB02-E_S37_L003_R1_001.fastq VA_W_02_22.fastq
mv HADB02-F_S38_L003_R1_001.fastq VA_B_02_22.fastq
mv HADB02-G_S39_L003_R1_001.fastq RI_W_02_22.fastq
mv HADB02-H_S40_L003_R1_001.fastq RI_B_02_22.fastq
mv HADB02-I_S41_L003_R1_001.fastq VA_W_02_18.fastq
mv HADB02-J_S42_L003_R1_001.fastq VA_B_02_18.fastq
mv HADB02-K_S43_L003_R1_001.fastq RI_W_02_18.fastq
mv HADB02-L_S44_L003_R1_001.fastq RI_B_02_18.fastq
mv HADB02-M_S45_L003_R1_001.fastq VA_W_09_SNP.fastq
mv HADB02-N_S46_L003_R1_001.fastq VA_B_08_SNP.fastq
mv HADB02-O_S47_L003_R1_001.fastq RI_W_09_SNP.fastq
mv HADB02-P_S48_L003_R1_001.fastq RI_B_09_SNP.fastq
mv HADB03-A_S49_L004_R1_001.fastq VA_W_03_14.fastq
mv HADB03-B_S50_L004_R1_001.fastq VA_B_03_14.fastq
mv HADB03-C_S51_L004_R1_001.fastq RI_W_03_14.fastq
mv HADB03-D_S52_L004_R1_001.fastq RI_B_03_14.fastq
mv HADB03-E_S53_L004_R1_001.fastq VA_W_03_22.fastq
mv HADB03-F_S54_L004_R1_001.fastq VA_B_03_22.fastq
mv HADB03-G_S55_L004_R1_001.fastq RI_W_03_22.fastq
mv HADB03-H_S56_L004_R1_001.fastq RI_B_03_22.fastq
mv HADB03-I_S57_L004_R1_001.fastq VA_W_03_18.fastq
mv HADB03-J_S58_L004_R1_001.fastq VA_B_03_18.fastq
mv HADB03-K_S59_L004_R1_001.fastq RI_W_03_18.fastq
mv HADB03-L_S60_L004_R1_001.fastq RI_B_03_18.fastq
mv HADB03-M_S61_L004_R1_001.fastq VA_W_10_SNP.fastq
mv HADB03-N_S62_L004_R1_001.fastq VA_B_10_SNP.fastq
mv HADB03-O_S63_L004_R1_001.fastq RI_W_10_SNP.fastq
mv HADB03-P_S64_L004_R1_001.fastq RI_B_10_SNP.fastq
mv HADB04-A_S65_L005_R1_001.fastq VA_W_04_14.fastq
mv HADB04-B_S66_L005_R1_001.fastq VA_B_04_14.fastq
mv HADB04-C_S67_L005_R1_001.fastq RI_W_04_14.fastq
mv HADB04-D_S68_L005_R1_001.fastq RI_B_04_14.fastq
mv HADB04-E_S69_L005_R1_001.fastq VA_W_04_22.fastq
mv HADB04-F_S70_L005_R1_001.fastq VA_B_04_22.fastq
mv HADB04-G_S71_L005_R1_001.fastq RI_W_04_22.fastq
mv HADB04-H_S72_L005_R1_001.fastq RI_B_04_22.fastq
mv HADB04-I_S73_L005_R1_001.fastq VA_W_04_18.fastq
mv HADB04-J_S74_L005_R1_001.fastq VA_B_04_18.fastq
mv HADB04-K_S75_L005_R1_001.fastq RI_W_04_18.fastq
mv HADB04-L_S76_L005_R1_001.fastq RI_B_04_18.fastq
mv HADB04-M_S77_L005_R1_001.fastq VA_W_05_14.fastq
mv HADB04-N_S78_L005_R1_001.fastq VA_B_05_14.fastq
mv HADB04-O_S79_L005_R1_001.fastq RI_W_05_14.fastq
mv HADB04-P_S80_L005_R1_001.fastq RI_B_05_14.fastq
mv HADB05-A_S81_L006_R1_001.fastq VA_W_05_22.fastq
mv HADB05-B_S82_L006_R1_001.fastq VA_B_05_22.fastq
mv HADB05-C_S83_L006_R1_001.fastq RI_W_05_22.fastq
mv HADB05-D_S84_L006_R1_001.fastq RI_B_05_22.fastq
mv HADB05-E_S85_L006_R1_001.fastq VA_W_05_18.fastq
mv HADB05-F_S86_L006_R1_001.fastq VA_B_05_18.fastq
mv HADB05-G_S87_L006_R1_001.fastq RI_W_05_18.fastq
mv HADB05-H_S88_L006_R1_001.fastq RI_B_05_18.fastq
mv HADB05-I_S89_L006_R1_001.fastq VA_W_06_14.fastq
mv HADB05-J_S90_L006_R1_001.fastq VA_B_06_14.fastq
mv HADB05-K_S91_L006_R1_001.fastq RI_W_06_14.fastq
mv HADB05-L_S92_L006_R1_001.fastq RI_B_06_14.fastq
mv HADB05-M_S93_L006_R1_001.fastq VA_W_06_22.fastq
mv HADB05-N_S94_L006_R1_001.fastq VA_B_06_22.fastq
mv HADB05-O_S95_L006_R1_001.fastq RI_W_06_22.fastq
mv HADB05-P_S96_L006_R1_001.fastq RI_B_06_22.fastq
mv HADB06-A_S97_L007_R1_001.fastq VA_W_06_18.fastq
mv HADB06-B_S98_L007_R1_001.fastq VA_B_06_18.fastq
mv HADB06-C_S99_L007_R1_001.fastq RI_W_06_18.fastq
mv HADB06-D_S100_L007_R1_001.fastq RI_B_06_18.fastq
mv HADB06-E_S101_L007_R1_001.fastq VA_W_07_14.fastq
mv HADB06-F_S102_L007_R1_001.fastq VA_B_07_14.fastq
mv HADB06-G_S103_L007_R1_001.fastq RI_W_07_14.fastq
mv HADB06-H_S104_L007_R1_001.fastq RI_B_07_14.fastq
mv HADB06-I_S105_L007_R1_001.fastq VA_W_07_22.fastq
mv HADB06-J_S106_L007_R1_001.fastq VA_B_07_22.fastq
mv HADB06-K_S107_L007_R1_001.fastq RI_W_07_22.fastq
mv HADB06-L_S108_L007_R1_001.fastq RI_B_07_22.fastq
mv HADB06-M_S109_L007_R1_001.fastq VA_W_07_18.fastq
mv HADB06-N_S110_L007_R1_001.fastq VA_B_07_18.fastq
mv HADB06-O_S111_L007_R1_001.fastq RI_W_07_18.fastq
mv HADB06-P_S112_L007_R1_001.fastq RI_B_07_18.fastq
```
5. Uncomment the last line of the renaming script in your scripts folder that starts with os.popen and comment out the next to last line that starts with print
``` sh
[dbarshis@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq
[dbarshis@turing1 fastq]$ nano ../../scripts/renamer_advbioinf.py 
```
6. write a sbatch script and submit it to rename all the .fastq files according to the renaming table using your renamer_advbioinf.py script
``` sh
[dbarshis@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq
[dbarshis@turing1 fastq]$ cat DansRenamer.sh 
#!/bin/bash -l

#SBATCH -o dansrenamer.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=FastqRename

../../scripts/renamer_advbioinf.py renamingtable_complete.txt
[dbarshis@turing1 fastq]$ sbatch ./DansRenamer.sh 
Submitted batch job 9270345
[dbarshis@turing1 fastq]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270345      main FastqRen dbarshis PD       0:00      1 (Priority) 
[dbarshis@turing1 fastq]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270345      main FastqRen dbarshis PD       0:00      1 (Priority) 
[dbarshis@turing1 fastq]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270345      main FastqRen dbarshis  R       0:01      1 coreV2-25-047 

```
7. Make sure this is all documented on your github page
``` sh
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % pwd
/Users/danbarshis/dansstuff/Projeks/ODU/CoursesTaught_Taken/21-01_Sp_AdvancedGenomicsDataAnalysis/DemoFolder/21SpDansAdvancedGenomicsLog
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git add README.md
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git commit -m 'updating day03 homework'
[main 81bbb64] updating day03 homework
 1 file changed, 21 insertions(+)
(base) danbarshis@BIOLLBB0 21SpDansAdvancedGenomicsLog % git push -u origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 405 bytes | 405.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/BarshisLab/21SpDansAdvancedGenomicsLog.git
   8f5c8ef..81bbb64  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```
8. The naming convention for the files is as follows:
  * SOURCEPOPULATION_SYMBIOTICSTATE_GENOTYPE_TEMPERATURE.fastq
  * There are 2 sources: Virginia and Rhode Island
  * There are 2 symbiotic states: Brown and White
  
9. Next, you're going to start the process of adapter clipping and quality trimming all the renamed .fastq files in batches, by lane
10. cp the script /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Trimclipfilterstatsbatch_advbioinf.py into your scripts directory

``` sh
[dbarshis@coreV2-25-047 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@coreV2-25-047 data]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Trimclipfilterstatsbatch_advbioinf.py ../scripts/
```
11. Less/head the new script and check out the usage statement
``` sh
[dbarshis@coreV2-25-047 data]$ head -14 ../scripts/Trimclipfilterstatsbatch_advbioinf.py
#!/usr/bin/env python
# Written by Dan Barshis

import sys, os

########### Usage #############
# Trimclipfilterstatsbatch.py barcodefile.txt anynumberoffastqfiles
# This should be run from within the folder with all of your original .fastqstrim
# Will quality trim multiple SINGLE-END fastq files
# Things to customize for your particular platform:
# qualoffset = 33 Quality score offset
# -t option in qualitytrim (the lower threshold quality score for trimming)
# -l option in qualitytrim and adapterclip (the length threshold for throwing out short reads)
```
12. cp the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/adapterlist_advbioinf.txt into the working directory with your fastq files
``` sh
[dbarshis@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq
[dbarshis@turing1 fastq]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/adapterlist_advbioinf.txt ./
```
13. Make a sbatch script for the Trimclipfilter... script and run it on your fastq files
``` sh

[dbarshis@coreV2-25-047 Testing]$ pwd 
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/Testing
[dbarshis@coreV2-25-047 Testing]$ cat TestTrimClip.sh 
#!/bin/bash -l

#SBATCH -o djbtestTrimclip.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=djbTrimTest

../../../scripts/Trimclipfilterstatsbatch_advbioinf.py adapterlist_advbioinf.txt *.fastq


[dbarshis@coreV2-25-047 Testing]$ sbatch TestTrimClip.sh 
Submitted batch job 9270351

[dbarshis@coreV2-25-047 Testing]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270351      main djbTrimT dbarshis  R       0:52      1 coreV2-25-005 
[dbarshis@coreV2-25-047 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq
[dbarshis@coreV2-25-047 fastq]$ cat FullTrimClip.sh 
#!/bin/bash -l

#SBATCH -o djbFullTrimclip.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=djbTrimFull

../../scripts/Trimclipfilterstatsbatch_advbioinf.py adapterlist_advbioinf.txt *.fastq

[dbarshis@coreV2-25-047 fastq]$ sbatch FullTrimClip.sh 
Submitted batch job 9270353
[dbarshis@coreV2-25-047 fastq]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270353      main djbTrimF dbarshis  R       0:34      1 coreV2-25-005 
           9270351      main djbTrimT dbarshis  R       7:04      1 coreV2-25-005 
```
14. This will take a while (like days)
15. Now might be a good time to update everything on your github
   * Jeez, i'm working on it

## Homework day04 29-Jan-2021
Homework day04 (document all this in your notebook, don't forget to pwd before each entry to remind yourself where you were working):
1. Add your trimclipstats.txt output to the full class datafile /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt using the following steps

1a. run `/cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py -h` to examine usage

``` sh
[dbarshis@turing1 RI_B_14]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq
[dbarshis@turing1 RI_B_14]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py -h
Written by Peter Schafran pscha005@odu.edu 5-Oct-2015

This script takes a stats output file from fastx_clipper and converts it into a table.

Usage: Schafran_trimstatstable.py [-c, -v, -h] inputfile.txt outputfile.txt

Options (-c and -v must be listed separately to run together):
-h	Display this help message
-c	Use comma delimiter instead of tabs
-v	Verbose mode (print steps to stdout)
```
1b. Run the script on your data with the outputfilename YOURNAME_trimclipstatsout.txt

``` sh
[dbarshis@turing1 fastq]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py trimclipstats.txt DAN_trimclipstatsout.txt
```

1c. Add YOURNAME_trimclipstatsout.txt to the class file by running tail -n +2 YOURNAME_trimclipstatsout.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt

``` sh
[dbarshis@turing1 fastq]$ tail -n +2 DAN_trimclipstatsout.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt
```

2. Now we're going to map our reads back to our assembly using the bowtie2 alignment algorithm (starting to follow this pipeline https://github.com/bethsheets/SNPcalling_tutorial)

3. write a sbatch script to do the following commands in sequence on your _clippedtrimmedfilterd.fastq datafiles from your lane of data

``` sh
module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmed.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/18AdvBioinf/classdata/Astrangia_poculata/refassembly/ast_hostsym -U $i \
> ${i%_clippedtrimmed.fastq}.sam; done
```

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
> ${i%_clippedtrimmed.fastq}.sam --no-unal -k 5; done

[dbarshis@turing1 RI_B_14]$ sbatch bowtiealn.sh 
Submitted batch job 9271002
```

4. Submit and add everything to your logfile

## Homework day05 3-Feb-2021


## Homework day06 5-Feb-2021
1. start an interactive session via salloc and run the /cm/shared/apps/trinity/2.0.6/util/TrinityStats.pl script on your Trinity.fasta output from your assembly
``` sh
[dbarshis@turing1 dan]$ salloc
salloc: Pending job allocation 9272731
salloc: job 9272731 queued and waiting for resources
salloc: job 9272731 has been allocated resources
salloc: Granted job allocation 9272731
[dbarshis@coreV3-23-036 21sampleassembly_trinity_out_dir]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/QCFastqs/21sampleassembly_trinity_out_dir
[dbarshis@coreV3-23-036 21sampleassembly_trinity_out_dir]$ /cm/shared/apps/trinity/2.0.6/util/TrinityStats.pl Trinity.fasta


################################
## Counts of transcripts, etc.
################################
Total trinity 'genes':	20980
Total trinity transcripts:	21992
Percent GC: 46.21

########################################
Stats based on ALL transcript contigs:
########################################

	Contig N10: 1178
	Contig N20: 694
	Contig N30: 514
	Contig N40: 414
	Contig N50: 347

	Median contig length: 273
	Average contig: 356.95
	Total assembled bases: 7850006


#####################################################
## Stats based on ONLY LONGEST ISOFORM per 'GENE':
#####################################################

	Contig N10: 1027
	Contig N20: 643
	Contig N30: 486
	Contig N40: 397
	Contig N50: 336

	Median contig length: 271
	Average contig: 347.72
	Total assembled bases: 7295061
```
2. compare this with the output from avg_cov_len_fasta_advbioinf.py on our class reference assembly (/cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta) and add both to your logfile

``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta
The total number of sequences is 15079
The average sequence length is 876
The total number of bases is 13210470
The minimum sequence length is 500
The maximum sequence length is 10795
The N50 is 881
Median Length = 578
contigs < 150bp = 0
contigs >= 500bp = 15079
contigs >= 1000bp = 3660
contigs >= 2000bp = 536
```
3. less or head your bowtie2 job output file to look at your alignment statistics and calculate the following from the information:
  * a-the mean percent "overall alignment rate"

``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/RI_B_14
[dbarshis@coreV3-23-036 RI_B_14]$ grep "overall alignment rate" djbowtie2.txt 
3.22% overall alignment rate
1.91% overall alignment rate
1.61% overall alignment rate
2.48% overall alignment rate
2.32% overall alignment rate
4.40% overall alignment rate
1.53% overall alignment rate

### compared to full ref alignment
[dbarshis@coreV3-23-036 RI_B_14]$ grep "overall alignment rate" djbowtie2fullref.txt 
90.54% overall alignment rate
87.77% overall alignment rate
94.95% overall alignment rate
91.75% overall alignment rate
94.39% overall alignment rate
96.40% overall alignment rate
96.08% overall alignment rate

### fancy with pipes to cut
[dbarshis@coreV3-23-036 RI_B_14]$ grep "overall alignment rate" djbowtie2fullref.txt | cut -d " " -f 1 | cut -d "%" -f 1
90.54
87.77
94.95
91.75
94.39
96.40
96.08
```
  * b-the mean percent reads "aligned exactly 1 time"
``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned exactly 1 time" djbowtie2.txt 
    117712 (1.63%) aligned exactly 1 time
    50875 (0.86%) aligned exactly 1 time
    199136 (1.11%) aligned exactly 1 time
    370715 (1.41%) aligned exactly 1 time
    677289 (1.66%) aligned exactly 1 time
    38261 (0.99%) aligned exactly 1 time
    279609 (1.10%) aligned exactly 1 time

### compared to full ref alignment
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned exactly 1 time" djbowtie2fullref.txt 
    3896116 (53.92%) aligned exactly 1 time
    2745106 (46.21%) aligned exactly 1 time
    9095833 (50.59%) aligned exactly 1 time
    14477971 (55.13%) aligned exactly 1 time
    20493151 (50.18%) aligned exactly 1 time
    1893541 (48.83%) aligned exactly 1 time
    13498376 (53.00%) aligned exactly 1 time

### fancy with pipes to cut
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned exactly 1 time" djbowtie2fullref.txt | cut -d "(" -f 2 | cut -d "%" -f 1
53.92
46.21
50.59
55.13
50.18
48.83
53.00

```
  * c-the mean number of reads "aligned exactly 1 time"
``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned exactly 1 time" djbowtie2.txt 
    117712 (1.63%) aligned exactly 1 time
    50875 (0.86%) aligned exactly 1 time
    199136 (1.11%) aligned exactly 1 time
    370715 (1.41%) aligned exactly 1 time
    677289 (1.66%) aligned exactly 1 time
    38261 (0.99%) aligned exactly 1 time
    279609 (1.10%) aligned exactly 1 time
    
### compared to full ref alignment
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned exactly 1 time" djbowtie2fullref.txt 
    3896116 (53.92%) aligned exactly 1 time
    2745106 (46.21%) aligned exactly 1 time
    9095833 (50.59%) aligned exactly 1 time
    14477971 (55.13%) aligned exactly 1 time
    20493151 (50.18%) aligned exactly 1 time
    1893541 (48.83%) aligned exactly 1 time
    13498376 (53.00%) aligned exactly 1 time

### fancy with pipes to cut
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned exactly 1 time" djbowtie2fullref.txt | cut -d " " -f 5
3896116
2745106
9095833
14477971
20493151
1893541
13498376
```
  * d-the mean percent reads "aligned >1 times"
``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned >1 times" djbowtie2.txt 
    114820 (1.59%) aligned >1 times
    62532 (1.05%) aligned >1 times
    90147 (0.50%) aligned >1 times
    281407 (1.07%) aligned >1 times
    272001 (0.67%) aligned >1 times
    132422 (3.42%) aligned >1 times
    109989 (0.43%) aligned >1 times
    
### compared to full ref alignment
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned >1 times" djbowtie2fullref.txt 
    2646216 (36.62%) aligned >1 times
    2469596 (41.57%) aligned >1 times
    7976744 (44.36%) aligned >1 times
    9619647 (36.63%) aligned >1 times
    18053294 (44.21%) aligned >1 times
    1844254 (47.56%) aligned >1 times
    10974446 (43.09%) aligned >1 times

### fancy with pipes to cut
[dbarshis@coreV3-23-036 RI_B_14]$ grep "aligned >1 times" djbowtie2fullref.txt | cut -d "(" -f 2 | cut -d "%" -f 1
36.62
41.57
44.36
36.63
44.21
47.56
43.09

```	
  * **hint** use grep and paste into excel or get fancy with **cut** and paste into excel

4. add your statistics as single rows to the shared table /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt as tab-delimited text in the following order:
LaneX_yourinitials	b-the mean percent "overall alignment rate"	c-the mean percent reads "aligned exactly 1 time"	d-the mean number of reads "aligned exactly 1 time"	e-the mean percent reads "aligned >1 times"

``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/RI_B_14
[dbarshis@coreV3-23-036 RI_B_14]$ nano alignstats.txt
[dbarshis@coreV3-23-036 RI_B_14]$ cat alignstats.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt
```
5. Data cleanup and archiving:
  * a-mv your Trinity.fasta file from your trinity_out_dir to a folder called testassembly in your data directory

``` sh
[dbarshis@coreV3-23-036 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/QCFastqs
[dbarshis@coreV3-23-036 QCFastqs]$ mkdir /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/testassembly
[dbarshis@coreV3-23-036 QCFastqs]$ mv 21sampleassembly_trinity_out_dir/Trinity.fasta /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/testassembly
```
  * b-set up a sbatch script to:
    * rm -r YOURtrinity_out_dir
    * rm -r YOURoriginalfastqs
    * rm -r YOURfilteringstats # as long as you've already appended your filteringstats output to the class table as part of homework_day04.txt

``` sh
#!/bin/bash -l

#SBATCH -o OUTFILENAME.txt
#SBATCH -n NUMTHREADS(1 if not multi-threaded)
#SBATCH --mail-user=YOUREMAIL@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

rm -r /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/QCFastqs/21sampleassembly_trinity_out_dir
rm -r /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/originalfastqs
rm -r /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/filteringstats
```

6. submit a blast against sprot from your testassembly folder using the following command

``` sh
#!/bin/bash -l

#SBATCH -o OUTFILENAME.txt
#SBATCH -n 6         
#SBATCH --mail-user=EMAIL
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

enable_lmod
module load container_env blast
blastx -query Trinity.fasta -db /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018 -out blastx.outfmt6 \
        -evalue 1e-20 -num_threads 6 -max_target_seqs 1 -outfmt 6

### my workflow
[dbarshis@coreV3-23-036 testassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/testassembly
[dbarshis@coreV3-23-036 testassembly]$ cat blast2sprot.sh 
#!/bin/bash -l

#SBATCH -o blastx2sprot.txt
#SBATCH -n 6         
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=djbblastx2sprot

enable_lmod
module load container_env blast
blastx -query Trinity.fasta -db /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018 -out djbblastx.outfmt6 \
        -evalue 1e-20 -num_threads 6 -max_target_seqs 1 -outfmt 6
[dbarshis@coreV3-23-036 testassembly]$ sbatch blast2sprot.sh 
Submitted batch job 9272733
```

\###Exploring our SAM files, check out http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#sam-output for bowtie2 specific output and http://bio-bwa.sourceforge.net/bwa.shtml#4 for general SAM output

7. head one of your .sam files to look at the header

``` sh
[dbarshis@coreV3-23-036 RI_B_14]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/fastq/RI_B_14
[dbarshis@coreV3-23-036 RI_B_14]$ head RI_B_01_14_clippedtrimmed.fastq.sam 
@HD	VN:1.0	SO:unsorted
@SQ	SN:TR78|c0_g1_i1_coral	LN:1109
@SQ	SN:TR78|c0_g2_i1_coral	LN:1109
@SQ	SN:TR79|c0_g1_i1_coral	LN:610
@SQ	SN:TR79|c0_g2_i1_coral	LN:1549
@SQ	SN:TR87|c0_g1_i1_coral	LN:732
@SQ	SN:TR93|c0_g1_i1_coral	LN:550
@SQ	SN:TR101|c0_g1_i1_coral	LN:673
@SQ	SN:TR104|c0_g1_i1_coral	LN:607
@SQ	SN:TR105|c0_g1_i1_coral	LN:587

```
8. grep -v '@' your.sam | head to look at the sequence read lines, why does this work to exclude the header lines?
```
```
9. in an interactive session run /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py on 2-3 of your .sam files using * to select 2-3 at the same time.
```
```
10. for expression counting, we need to run bowtie2 a little different, so if you have time, set up and run the following script on your filtered fastq files to finish before Wednesday, this will also perform the read sorting step required for SNP calling:

``` sh
#!/bin/bash -l

#SBATCH -o OUTFILENAME.txt
#SBATCH -n 1         
#SBATCH --mail-user=EMAIL
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

module load samtools/1.1
module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmedfilterd.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/18AdvBioinf/classdata/Astrangia_poculata/refassembly/ast_hostsym -U $i \
> ${i%_clippedtrimmed.fastq}_v2.sam --no-unal -k 5; done

for i in *.sam; do `samtools view -bS $i > ${i%.sam}_UNSORTED.bam`; done

for i in *UNSORTED.bam; do samtools sort $i > ${i%_UNSORTED.bam}.bam
samtools index ${i%_UNSORTED.bam}.bam
done
```
