### **Manage files with Git**

```shell
My Git Machine $ echo "Happy New Year" > NewYearFile.txt
My Git Machine $ ls
NewYearFile.txt
My Git Machine $ cat NewYearFile.txt
Happy New Year
My Git Machine $
My Git Machine $
My Git Machine $ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        NewYearFile.txt

nothing added to commit but untracked files present (use "git add" to track)
 My Git Machine $
```



As we can see that your new NewYearFile.txt file is untracked, because it’s under the “Untracked files” heading in your status output. 


**What is the Untracked means:** Untracked basically means that Git sees a file you didn’t have in the previous snapshot (commit), and which hasn’t yet been staged. Git won’t start including it in your commit snapshots until you explicitly tell it to do so. 



**Why Git behave like this:** It does this so you don’t accidentally begin including generated binary files or other files that you did not mean to include. You do want to start including NewYearFile.txt, so let’s start tracking the file.

**How to Track the New Files**: In order to begin tracking a new file, you use the command git add. To begin tracking the NewYearFile.txt file, you can run this:

```shell
My Git Machine $
My Git Machine $ git add NewYearFile.txt
```

If you run your status command again, you can see that your NewYearFile.txt file is now tracked and staged to be committed:

```shell
My Git Machine $  git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   NewYearFile.txt

My Git Machine $
```

As we can see that NewYearFile.txt file is staged because it’s under the “Changes to be committed” heading. 

**Committing Your Changes**: The stage area is set up, now we can commit our changes. 

**NOTE**: If at this point you have any thing that is unstaged, I'm talking about any file that you've created or modified and you haven’t run git add on since you edited them  won’t go into this commit. 

```shell
My Git Machine $ git commit -m "New File Added"
[master (root-commit) 8d83d5a] New File Added
 1 file changed, 1 insertion(+)
 create mode 100644 NewYearFile.txt
My Git Machine $
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $

Now you’ve created your first commit! 

```

You can see that the commit has given you some output about itself: which branch you committed to (master), what SHA-1 checksum the commit has (**8d83d5a**), how many files were changed, and statistics about lines added and removed in the commit.

**What commit does:** Commit records the snapshot you set up in your staging area. Anything you didn’t stage is still sitting there modified.

**Removing Files:** In order to remove a file from git, First you have  to remove it from your tracked files i.e. remove it from your staging area and then commit.  The **git rm** command does that, and also removes the file from your working directory  so you don’t see it as an untracked file the next time around.

```shell
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $
My Git Machine $ ls
a.py
My Git Machine $ rm a.py
My Git Machine $
My Git Machine $ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    a.py

no changes added to commit (use "git add" and/or "git commit -a")
My Git Machine $ git rm a.py
rm 'a.py'
My Git Machine $
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    a.py

My Git Machine $ git commit -m "Deleted a.py file"
[master 2818f4b] Deleted a.py file
 1 file changed, 1 deletion(-)
 delete mode 100644 a.py
My Git Machine $

My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $

My Git Machine $ ls
My Git Machine $
```



Here as you can see that file also got deleted from the Drive I.E. OS level as well. What about if you may want to keep the file on your hard drive but not have Git track it anymore.  Something like a large log file, that you forgot to your .gitignore file and accidentally staged it. You use the below command:

```shell
$ git rm --cached <File_Name>
```

**What is the difference between :** "git rm --cached <file_name>" vs "git reset head -- <file_Name>"?

git rm will remove entries from the staging area.  This is a bit different from git reset HEAD which "unstages" files.  By "unstage" I mean it reverts the staging area to what was there before we started modifying things. However the  git rm on the other hand just kicks the file off the stage entirely, so that it's not included  in the next commit snapshot, thereby effectively deleting it.



**Moving Files** If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file. 

```shell
$ git mv file_from file_to

My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $
My Git Machine $ git ls-tree -r master --name-only
.gitignore
old_file
My Git Machine $
My Git Machine $ git mv old_file New_file
My Git Machine $
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    old_file -> New_file

My Git Machine $ git commit -m "Rename the file"
[master 816d68d] Rename the file
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename old_file => New_file (100%)
My Git Machine $
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $
```

**However, this is equivalent to running something like this:**

```shell
$ mv old_file New_file

$ git rm old_file

$ git add New_file
```



**Undoing Things:** How to undo the changes in Git.  we’ll do this by using undo  tools, however be little careful,  because you can’t always undo some of these undos.  If you want to redo that commit, make the additional changes you forgot, stage them, and commit again using the --amend option:

**$ git commit --amend**

```shell
My Git Machine $ ls
App.log  New_file
My Git Machine $ echo "Add more data" > New_file
My Git Machine $ git stau
git: 'stau' is not a git command. See 'git --help'.

The most similar command is
        status
My Git Machine $ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   New_file

no changes added to commit (use "git add" and/or "git commit -a")
My Git Machine $ git add New_file
warning: in the working copy of 'New_file', LF will be replaced by CRLF the next time Git touches it
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   New_file

My Git Machine $ touch One_more_new_file
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   New_file

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        One_more_new_file

My Git Machine $ git commit -m "NewFile"
[master e864a92] NewFile
 1 file changed, 1 insertion(+)
My Git Machine $ git sttau
git: 'sttau' is not a git command. See 'git --help'.

The most similar command is
        status
My Git Machine $ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        One_more_new_file

nothing added to commit but untracked files present (use "git add" to track)
My Git Machine $ git log -1
commit e864a9217f324d6beb000a3a3c8815916c80c627 (HEAD -> master)
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 15:26:33 2023 +0530

    NewFile
My Git Machine $ git add One_more_new_file
My Git Machine $ git commit --amend
[master fee4be3] NewFile
 Date: Mon Jan 2 15:26:33 2023 +0530
 2 files changed, 1 insertion(+)
 create mode 100644 One_more_new_file
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $ git log -1
commit fee4be34cd4bba275552b72faaa25ebe322f0b9b (HEAD -> master)
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 15:26:33 2023 +0530

    NewFile
My Git Machine $

```

**Unstaging a Staged File:** Now let’s assume you’ve changed two files and want to commit them as two separate changes, but you accidentally type git add * and stage them both. How can you unstage one of the two? The git status command reminds you:



```shell
My Git Machine $ touch 1.txt 2.txt
My Git Machine $ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt
        2.txt

nothing added to commit but untracked files present (use "git add" to track)
My Git Machine $ git add *

My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   1.txt
        new file:   2.txt

My Git Machine $

Right below the “Changes to be committed” text, it says use git reset HEAD <file>…​ to unstage. 
So, let’s use that advice to unstage the 2.txt file:

My Git Machine $ git reset HEAD 2.txt
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        2.txt

My Git Machine $
```

**Unmodifying a Modified File:** Say for example, you have modified the file and you later reliaze that you don’t want to keep your changes to the CONTRIBUTING.md file?  How can you easily unmodify it — revert it back to what it looked like when you last committed:

```shell
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $ ls
1.txt  2.txt  App.log  New_file  One_more_new_file
My Git Machine $
My Git Machine $ cat 2.txt
My Git Machine $
My Git Machine $ echo " Modifying 2.txt" > 2.txt
My Git Machine $ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   2.txt

no changes added to commit (use "git add" and/or "git commit -a")
My Git Machine $

My Git Machine $
My Git Machine $ git checkout -- 2.txt
My Git Machine $
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $

```

Let's Assume that, you have modified the file, whe it was in staged area, how it will work:



```shell
My Git Machine $ ls 2.txt
2.txt
My Git Machine $ cat 2.txt
My Git Machine $ echo "Modifying 2.txt" > 2.txt
My Git Machine $
My Git Machine $ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   2.txt

no changes added to commit (use "git add" and/or "git commit -a")
My Git Machine $ git add 2.txt
warning: in the working copy of '2.txt', LF will be replaced by CRLF the next time Git touches it
My Git Machine $
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   2.txt

My Git Machine $ echo "Modifying after Staged" > 2.txt
My Git Machine $
My Git Machine $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   2.txt

My Git Machine $

```

So, the file is both Staged and modified area. 
Here 2 things can happen, depending upon your choice.

If you run the git commit, the first version will be store, if tiy run git add and then git commit the second version will store.

```shell
My Git Machine $ git add 2.txt
warning: in the working copy of '2.txt', LF will be replaced by CRLF the next time Git touches it
My Git Machine $ git commit -m "Second modification saved"
[master d15f942] Second modification saved
 1 file changed, 1 insertion(+)
My Git Machine $ git status
On branch master
nothing to commit, working tree clean
My Git Machine $ cat 2.txt
Modifying after Staged
My Git Machine $

```





**Viewing the Commit History** In order to see what you have commited so far, you can use gi log command.

```shell
My Git Machine $ git log
commit 816d68d7c16410fae05b7dbf57e5c7d87d96c45b (HEAD -> master)
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 14:06:05 2023 +0530

    Rename the file

commit efe521c855a1024fe932f6ee517c86c1561d7384
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 14:05:17 2023 +0530

    Addd olf fil

commit d9f376b3aabf55bc806e056322730134b5a22020
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 13:58:38 2023 +0530

    modified .gitignore

commit 3ff64933c6097c1602fca840bff8ef4559c23e16
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 13:57:47 2023 +0530

    Added .gitignore

commit a363eb531e2f59695e78a587e0be670a347036ed
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 13:56:28 2023 +0530

    the file asd is gone from the repository

commit 259702935bca44d7e55dc12060581cc12a167774
```

One of the more helpful options is -p or --patch, which shows the difference introduced in each commit.  You can also limit the number of log entries displayed, such as using -2 to show only the last two entries.

```shell
My Git Machine $ git log -p -2
commit 816d68d7c16410fae05b7dbf57e5c7d87d96c45b (HEAD -> master)
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 14:06:05 2023 +0530

    Rename the file

diff --git a/old_file b/New_file
similarity index 100%
rename from old_file
rename to New_file

commit efe521c855a1024fe932f6ee517c86c1561d7384
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 14:05:17 2023 +0530

    Addd olf fil

diff --git a/old_file b/old_file
new file mode 100644
index 0000000..e69de29
My Git Machine $

```

**This is very helpful for code review or to quickly browse what happened during a series of commits  that a collaborator has added.**

You can also use a series of summarizing options with git log. For example, if you want to see some  abbreviated stats for each commit, you can use the --stat option:

```
My Git Machine $ git log --stat
commit 816d68d7c16410fae05b7dbf57e5c7d87d96c45b (HEAD -> master)
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 14:06:05 2023 +0530

    Rename the file

 old_file => New_file | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

commit efe521c855a1024fe932f6ee517c86c1561d7384
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 14:05:17 2023 +0530

    Addd olf fil

 old_file | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

commit d9f376b3aabf55bc806e056322730134b5a22020
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 13:58:38 2023 +0530

    modified .gitignore

 .gitignore | 1 +
 1 file changed, 1 insertion(+)

commit 3ff64933c6097c1602fca840bff8ef4559c23e16
Author: Kumar Saurabh <my_email@gmail.com>
Date:   Mon Jan 2 13:57:47 2023 +0530
```

```shell
Some More log COmmands:
git log
git log
git log --stat
git log -n
git log --after
git log --oneline
git revert <commit_id>

```

