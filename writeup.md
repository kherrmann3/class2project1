NOTES: I've setup the following git aliases:
git l = git log --oneline
git s = git status
git co = git checkout

#######
STEP 1: Create first commit on the master branch, and then create branches for Integration and HotFix.:
###########

tful@tfuls-MacBook-Pro class2project1 % git init
Initialized empty Git repository in /Users/tful/Documents/Caltech CTME PGP DevOps/PG_DO_gitandgithubtraining/class2project1/.git/
tful@tfuls-MacBook-Pro class2project1 % clear

tful@tfuls-MacBook-Pro class2project1 % vi baseapp.txt
tful@tfuls-MacBook-Pro class2project1 % git add .
tful@tfuls-MacBook-Pro class2project1 % git commit -m "first commit of the base app"
[master (root-commit) fad45f4] first commit of the base app
 1 file changed, 1 insertion(+)
 create mode 100644 baseapp.txt
tful@tfuls-MacBook-Pro class2project1 % git branch HotFix
tful@tfuls-MacBook-Pro class2project1 % git branch Integration
tful@tfuls-MacBook-Pro class2project1 % git branch
  HotFix
  Integration
* master


#######
STEP 2: Create Feature 1 and Feature 2 branches off of the Integration branch
############

tful@tfuls-MacBook-Pro class2project1 % git branch
  HotFix
  Integration
* master
tful@tfuls-MacBook-Pro class2project1 % git co Integration
Switched to branch 'Integration'
tful@tfuls-MacBook-Pro class2project1 % git branch
  HotFix
* Integration
  master
tful@tfuls-MacBook-Pro class2project1 % git branch Feature1
tful@tfuls-MacBook-Pro class2project1 % git branch Feature2
tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
  Feature2
  HotFix
* Integration
  master

#######
STEP 3: Commit changes to Feature 2 branch and merge it into Integration branch
############
tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
  Feature2
  HotFix
* Integration
  master
tful@tfuls-MacBook-Pro class2project1 % git co Feature2
Switched to branch 'Feature2'
tful@tfuls-MacBook-Pro class2project1 % mkdir feature2
tful@tfuls-MacBook-Pro class2project1 % vi feature2/feature2.txt
tful@tfuls-MacBook-Pro class2project1 % git add .
tful@tfuls-MacBook-Pro class2project1 % git commit -m "added feature2/feature2.txt as first version of feature2"
[Feature2 f328500] added feature2/feature2.txt as first version of feature2
 2 files changed, 1 insertion(+)
 create mode 100644 feature2/feature2.txt
 create mode 100644 writeup.md
tful@tfuls-MacBook-Pro class2project1 % vi feature2/feature2.txt 
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 2.1"
[Feature2 cfb8c22] added feature 2.1
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % vi feature2/feature2.txt 
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 2.2"
[Feature2 2199146] added feature 2.2
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % cat feature2/feature2.txt 
first release of feature2
adding feature 2.1
adding feature 2.2
tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
* Feature2
  HotFix
  Integration
  master
tful@tfuls-MacBook-Pro class2project1 % git co Integration
Switched to branch 'Integration'
tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
  Feature2
  HotFix
* Integration
  master
tful@tfuls-MacBook-Pro class2project1 % ls                
baseapp.txt
tful@tfuls-MacBook-Pro class2project1 % git l             
fad45f4 (HEAD -> Integration, master, HotFix, Feature1) first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git merge Feature2
Updating fad45f4..2199146
Fast-forward
 feature2/feature2.txt | 3 +++
 writeup.md            | 0
 2 files changed, 3 insertions(+)
 create mode 100644 feature2/feature2.txt
 create mode 100644 writeup.md
tful@tfuls-MacBook-Pro class2project1 % git l
2199146 (HEAD -> Integration, Feature2) added feature 2.2
cfb8c22 added feature 2.1
f328500 added feature2/feature2.txt as first version of feature2
fad45f4 (master, HotFix, Feature1) first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
  Feature2
  HotFix
* Integration
  master


#######
STEP 4: Commit changes to Feature 1 branch and rebase it to the integration branches
#############

tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
  Feature2
  HotFix
* Integration
  master
tful@tfuls-MacBook-Pro class2project1 % git co Feature1
Switched to branch 'Feature1'
tful@tfuls-MacBook-Pro class2project1 % mkdir feature1
tful@tfuls-MacBook-Pro class2project1 % vi feature1/feature1.txt
tful@tfuls-MacBook-Pro class2project1 % git add .
tful@tfuls-MacBook-Pro class2project1 % git commit -m "added feature1 1.0"
[Feature1 b2960aa] added feature1 1.0
 1 file changed, 1 insertion(+)
 create mode 100644 feature1/feature1.txt
tful@tfuls-MacBook-Pro class2project1 % vi feature1/feature1.txt 
tful@tfuls-MacBook-Pro class2project1 % ls  
baseapp.txt	feature1
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 1.1"
[Feature1 df5e29a] added feature 1.1
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % git l
df5e29a (HEAD -> Feature1) added feature 1.1
b2960aa added feature1 1.0
fad45f4 (master, HotFix) first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git branch Integration
fatal: A branch named 'Integration' already exists.
tful@tfuls-MacBook-Pro class2project1 % git co Integration
Switched to branch 'Integration'
tful@tfuls-MacBook-Pro class2project1 % git l 
2199146 (HEAD -> Integration, Feature2) added feature 2.2
cfb8c22 added feature 2.1
f328500 added feature2/feature2.txt as first version of feature2
fad45f4 (master, HotFix) first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git rebase feature1
First, rewinding head to replay your work on top of it...
Applying: added feature2/feature2.txt as first version of feature2
Applying: added feature 2.1
Applying: added feature 2.2
tful@tfuls-MacBook-Pro class2project1 % git l
3c491f0 (HEAD -> Integration) added feature 2.2
19def3e added feature 2.1
28fd132 added feature2/feature2.txt as first version of feature2
df5e29a (Feature1) added feature 1.1
b2960aa added feature1 1.0
fad45f4 (master, HotFix) first commit of the base app


#######
STEP 5: Merge Integration branch into HotFix and Production branches
############

tful@tfuls-MacBook-Pro class2project1 % git branch
  Feature1
  Feature2
  HotFix
* Integration
  master
tful@tfuls-MacBook-Pro class2project1 % git l --graph
* 3c491f0 (HEAD -> Integration) added feature 2.2
* 19def3e added feature 2.1
* 28fd132 added feature2/feature2.txt as first version of feature2
* df5e29a (Feature1) added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 (master, HotFix) first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git co HotFix    
Switched to branch 'HotFix'
tful@tfuls-MacBook-Pro class2project1 % git merge Integration
Updating fad45f4..3c491f0
Fast-forward
 feature1/feature1.txt | 2 ++
 feature2/feature2.txt | 3 +++
 writeup.md            | 0
 3 files changed, 5 insertions(+)
 create mode 100644 feature1/feature1.txt
 create mode 100644 feature2/feature2.txt
 create mode 100644 writeup.md
tful@tfuls-MacBook-Pro class2project1 % git co master
Switched to branch 'master'
tful@tfuls-MacBook-Pro class2project1 % git merge Integration
Updating fad45f4..3c491f0
Fast-forward
 feature1/feature1.txt | 2 ++
 feature2/feature2.txt | 3 +++
 writeup.md            | 0
 3 files changed, 5 insertions(+)
 create mode 100644 feature1/feature1.txt
 create mode 100644 feature2/feature2.txt
 create mode 100644 writeup.md
tful@tfuls-MacBook-Pro class2project1 % git l --graph
* 3c491f0 (HEAD -> master, Integration, HotFix) added feature 2.2
* 19def3e added feature 2.1
* 28fd132 added feature2/feature2.txt as first version of feature2
* df5e29a (Feature1) added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 first commit of the base app


########
STEP 6: Commit changes to Feature 1 branch and merge into Integration, Hotfix and Production.
############
tful@tfuls-MacBook-Pro class2project1 % git co Feature1
Switched to branch 'Feature1'
tful@tfuls-MacBook-Pro class2project1 % ls 
baseapp.txt	feature1
tful@tfuls-MacBook-Pro class2project1 % vi feature1/feature1.txt 
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 1.2"
[Feature1 11b3371] added feature 1.2
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % vi feature1/feature1.txt 
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 1.3"
[Feature1 4e34763] added feature 1.3
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % git l
4e34763 (HEAD -> Feature1) added feature 1.3
11b3371 added feature 1.2
df5e29a added feature 1.1
b2960aa added feature1 1.0
fad45f4 first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git co Integration 
Switched to branch 'Integration'
tful@tfuls-MacBook-Pro class2project1 % git merge Feature1
Merge made by the 'recursive' strategy.
 feature1/feature1.txt | 2 ++
 1 file changed, 2 insertions(+)
tful@tfuls-MacBook-Pro class2project1 % git co HotFix
Switched to branch 'HotFix'
tful@tfuls-MacBook-Pro class2project1 % git merge Feature1
Merge made by the 'recursive' strategy.
 feature1/feature1.txt | 2 ++
 1 file changed, 2 insertions(+)
tful@tfuls-MacBook-Pro class2project1 % git co master
Switched to branch 'master'
tful@tfuls-MacBook-Pro class2project1 % git merge Feature1
Merge made by the 'recursive' strategy.
 feature1/feature1.txt | 2 ++
 1 file changed, 2 insertions(+)
tful@tfuls-MacBook-Pro class2project1 % git l --graph
*   14a349c (HEAD -> master) Merge branch 'Feature1'
|\  
| * 4e34763 (Feature1) added feature 1.3
| * 11b3371 added feature 1.2
* | 3c491f0 added feature 2.2
* | 19def3e added feature 2.1
* | 28fd132 added feature2/feature2.txt as first version of feature2
|/  
* df5e29a added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 first commit of the base app

########
STEP 7: Commit changes to Hotfix branch and merge into Integration and Master branches
#############

tful@tfuls-MacBook-Pro class2project1 % git co HotFix
Switched to branch 'HotFix'
tful@tfuls-MacBook-Pro class2project1 % ls
baseapp.txt	feature1	feature2	writeup.md
tful@tfuls-MacBook-Pro class2project1 % vi feature1/feature1.txt 
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 1.3.1"
[HotFix f31dcb3] added feature 1.3.1
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % vi feature2/feature2.txt 
tful@tfuls-MacBook-Pro class2project1 % git commit -am "added feature 2.2.1"
[HotFix 1b41921] added feature 2.2.1
 1 file changed, 1 insertion(+)
tful@tfuls-MacBook-Pro class2project1 % git l --graph
* 1b41921 (HEAD -> HotFix) added feature 2.2.1
* f31dcb3 added feature 1.3.1
*   c3e4d6f Merge branch 'Feature1' into HotFix
|\  
| * 4e34763 (Feature1) added feature 1.3
| * 11b3371 added feature 1.2
* | 3c491f0 added feature 2.2
* | 19def3e added feature 2.1
* | 28fd132 added feature2/feature2.txt as first version of feature2
|/  
* df5e29a added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git co Integration 
Switched to branch 'Integration'
tful@tfuls-MacBook-Pro class2project1 % git merge HotFix
Merge made by the 'recursive' strategy.
 feature1/feature1.txt | 1 +
 feature2/feature2.txt | 1 +
 2 files changed, 2 insertions(+)
tful@tfuls-MacBook-Pro class2project1 % git l --graph
*   d9ac6ba (HEAD -> Integration) Merge branch 'HotFix' into Integration
|\  
| * 1b41921 (HotFix) added feature 2.2.1
| * f31dcb3 added feature 1.3.1
| *   c3e4d6f Merge branch 'Feature1' into HotFix
| |\  
* | \   af61feb Merge branch 'Feature1' into Integration
|\ \ \  
| |/ /  
|/| /   
| |/    
| * 4e34763 (Feature1) added feature 1.3
| * 11b3371 added feature 1.2
* | 3c491f0 added feature 2.2
* | 19def3e added feature 2.1
* | 28fd132 added feature2/feature2.txt as first version of feature2
|/  
* df5e29a added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 first commit of the base app
tful@tfuls-MacBook-Pro class2project1 % git co master
Switched to branch 'master'
tful@tfuls-MacBook-Pro class2project1 % git merge HotFix
Merge made by the 'recursive' strategy.
 feature1/feature1.txt | 1 +
 feature2/feature2.txt | 1 +
 2 files changed, 2 insertions(+)
tful@tfuls-MacBook-Pro class2project1 % git l --graph
*   55dd103 (HEAD -> master) Merge branch 'HotFix'
|\  
| * 1b41921 (HotFix) added feature 2.2.1
| * f31dcb3 added feature 1.3.1
| *   c3e4d6f Merge branch 'Feature1' into HotFix
| |\  
* | \   14a349c Merge branch 'Feature1'
|\ \ \  
| |/ /  
|/| /   
| |/    
| * 4e34763 (Feature1) added feature 1.3
| * 11b3371 added feature 1.2
* | 3c491f0 added feature 2.2
* | 19def3e added feature 2.1
* | 28fd132 added feature2/feature2.txt as first version of feature2
|/  
* df5e29a added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 first commit of the base app


########
STEP 8: delete feature branches
############

tful@tfuls-MacBook-Pro class2project1 % git branch 
  Feature1
  Feature2
  HotFix
  Integration
* master
tful@tfuls-MacBook-Pro class2project1 % git branch -d Feature1
Deleted branch Feature1 (was 4e34763).
tful@tfuls-MacBook-Pro class2project1 % git branch -d Feature2
error: The branch 'Feature2' is not fully merged.
If you are sure you want to delete it, run 'git branch -D Feature2'.
tful@tfuls-MacBook-Pro class2project1 % ls -l
total 40
-rw-r--r--  1 tful  staff     33 Oct 25 09:21 baseapp.txt
drwxr-xr-x  3 tful  staff     96 Oct 25 10:09 feature1
drwxr-xr-x  3 tful  staff     96 Oct 25 10:09 feature2
-rw-r--r--  1 tful  staff  12878 Oct 25 10:12 writeup.md
tful@tfuls-MacBook-Pro class2project1 % cat feature2/feature2.txt 
first release of feature2
adding feature 2.1
adding feature 2.2
adding feature 2.2.1
tful@tfuls-MacBook-Pro class2project1 % git remote add origin https://github.com/kherrmann3/class2project1.git
tful@tfuls-MacBook-Pro class2project1 % git push -u origin master
Enumerating objects: 44, done.
Counting objects: 100% (44/44), done.
Delta compression using up to 16 threads
Compressing objects: 100% (28/28), done.
Writing objects: 100% (44/44), 3.27 KiB | 1.64 MiB/s, done.
Total 44 (delta 13), reused 0 (delta 0)
remote: Resolving deltas: 100% (13/13), done.
To https://github.com/kherrmann3/class2project1.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
tful@tfuls-MacBook-Pro class2project1 % git branch -D Feature2
Deleted branch Feature2 (was 2199146).
tful@tfuls-MacBook-Pro class2project1 % git l --graph
*   55dd103 (HEAD -> master, origin/master) Merge branch 'HotFix'
|\  
| * 1b41921 (HotFix) added feature 2.2.1
| * f31dcb3 added feature 1.3.1
| *   c3e4d6f Merge branch 'Feature1' into HotFix
| |\  
* | \   14a349c Merge branch 'Feature1'
|\ \ \  
| |/ /  
|/| /   
| |/    
| * 4e34763 added feature 1.3
| * 11b3371 added feature 1.2
* | 3c491f0 added feature 2.2
* | 19def3e added feature 2.1
* | 28fd132 added feature2/feature2.txt as first version of feature2
|/  
* df5e29a added feature 1.1
* b2960aa added feature1 1.0
* fad45f4 first commit of the base app
