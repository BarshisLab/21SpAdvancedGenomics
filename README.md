2021_Spring_Dan's Advanced Genomics Notebook
================
# How to make a notebook file on git
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