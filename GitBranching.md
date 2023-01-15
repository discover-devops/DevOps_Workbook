Git Branching 
=================
In order to understand how Git does branching, let's take a step back and examine how Git stores its data. Git doesn't store data as a series of changesets or differences, but instead as a series of snapshots.
When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author's name and email address, the message that you typed, and pointers to the commit.

Let's understand this with the help of diagram, let's assume that you have a directory containing three files, and you stage them all and commit.

$ git add file1.txt file2.txt file3.txt
$ git commit -m 'my commit'

What happens at the backend, actually when you create the commit by running git commit:

#1: Git checksums each subdirectory and stores them as a tree object in the Git repository.
#2: Git then creates a commit object that has the metadata and a pointer to the root project tree so it can re-create that snapshot when needed.


GIT BRANCHES
git branch 

git branch b1 master


git checkout b1
git branch
vi fileb1.txt
git status
git add fileb1.txt
git status
git commit -m "This sfor branch b1"
git status
git log --oneline

git checkout master
 git branch
git log --oneline

GIT Branch Merging
git merge src dest

git merge b1 master
ls 
git log --oneline

Branch Delete
git branch -d b1


Rename Branch
git branch -m <old branch name><new branch name>  

![image](https://user-images.githubusercontent.com/53135263/212557129-3e945177-ec40-4850-9373-796ce93374a6.png)
