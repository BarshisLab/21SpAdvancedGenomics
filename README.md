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
## Day02 Exercises 2021-Jan-22
``` sh
#Exercise day02:
#1- Logon to the cluster @turing.hpc.odu.edu
[dbarshis@turing1 dan]$ ls
db_exercise1.txt  groundrules.txt  scripts

#2- Make a directory in your course workspace called data
[dbarshis@turing1 dan]$ mkdir data

#3- Make a directory called exercises in your data directory
[dbarshis@turing1 dan]$ mkdir exercises

#4- execute a pwd command and start a log of your commands with a header for today's date in your README.md github logfile in your workspace
[dbarshis@turing1 exercises]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/exercises

#5- cp the Exercise2.fasta.gz and Exercise2.fastq.tar.gz files into your exercises directory from the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02 directory
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

#6- unzip and untar the files
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

#7- add these commands to your notebook file
You\'re looking at it buddy!

#8- calculate how many sequences are in each file and add these results to your notebook file
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

#9- cp the avg_cov_len_fasta_advbioinf.py from the /cm/shared/courses/dbarshis/21AdvGenomics/scripts directory into your class scripts directory
[dbarshis@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py ../scripts/

#10- start an interactive compute session and re-navigate to your exercises directory
[dbarshis@turing1 exercises]$ salloc
salloc: Pending job allocation 9268620
salloc: job 9268620 queued and waiting for resources
salloc: job 9268620 has been allocated resources
salloc: Granted job allocation 9268620
[dbarshis@coreV1-22-005 exercises]$ 

#11- run the avg_cov_len_fasta_DJB.py script on your Exercise2.fasta file by typing the path to the script followed by the Exercise2.fasta file name
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

#12- did you add all these entries to your notebook file, including the results of the script?
Yup!

#13- push your notebook file to your github page
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
```sh
#1- Write an sbatch script to cp the files /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/ into your own data directory
[dbarshis@coreV1-22-005 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@coreV1-22-005 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data
[dbarshis@coreV1-22-005 data]$ nano DansFQCp.sh

#2- Add the content of your sbatch script to your logfile
[dbarshis@coreV1-22-005 data]$ cat DansFQCp.sh 
#!/bin/bash -l

#SBATCH -o dansfastqcopy.txt
#SBATCH -n 1
#SBATCH --mail-user=dbarshis@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=DansFastqCp

cp /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/*.fastq.gz /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/dan/data/

#3- submit the slurm script (sbatch scripname.sh) and verify that it's working (by squeue -u yourusername multiple times and checking the destination directory to make sure the files are being created)
[dbarshis@coreV1-22-005 data]$ sbatch DansFQCp.sh 
Submitted batch job 9268621
[dbarshis@coreV1-22-005 data]$ squeue -u dbarshis
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9268621      main DansFast dbarshis  R       0:18      1 coreV1-22-005 
[dbarshis@coreV1-22-005 data]$ ls
dansfastqcopy.txt                  HADB01-B_S18_L002_R1_001.fastq.gz  HADB01-E_S21_L002_R1_001.fastq.gz
DansFQCp.sh                        HADB01-C_S19_L002_R1_001.fastq.gz  HADB01-F_S22_L002_R1_001.fastq.gz
HADB01-A_S17_L002_R1_001.fastq.gz  HADB01-D_S20_L002_R1_001.fastq.gz

#4- Make sure this is all documented on your github notebook
Yup

#5- Write a sbatch script to gunzip all the fastq.gz files

#6- Push your notebook file to your github page (document everything on your github notebook, drink a beer, and realize that all that work was just to get the data organized to start looking at it!)
```
