---
layout: post
author: Studiosus
title:  "Exploring Git"
date:   2023-10-15
tags: [git, terminal]
---

In my first article for this blog I’ll try to explore the possibilities of Git on Windows 10 using Visual Studio Code.

First, I need to download the Git distributive. In the address bar of my browser I type in `https://git-scm.com/` which brings me to the page where I can see the ["Download for Windows" link](https://git-scm.com/download/win "Download Git") which, in its turn, opens the page offering a set of links for portable editions and standalone installers. I choose 64-bit Git for Windows Setup and save it on my desktop.

Once I’ve downloaded a Git installer, it’s time to install it on my machine. I double click the file icon and follow the instructions in the installation window. At a certain point, I’m asked to choose the default editor used by Git, and I strike the line with the phrase “Use Visual Studio Code as Git’s default editor”.

As soon as Git is installed, I can launch Git Bash. From now on, I have a new Bash terminal, in addition to Command Prompt. I will mostly use it from inside my code editor.
So I start my VS Code and, from inside it, open the directory `D:\Git_Studies`, specially prepared for my practice in Git. It consists of an index file plus styles and scripts directories:
~~~~~~~
Git_Studies/
     |
     |--css/
     |
     |--scripts/
     |
     |--index.html
~~~~~~~

The key combination `Ctrl+`` opens Terminal in the VS Code window.

### Choosing Git Bash
Since I’m using Git with the support from VS Code for the very first time, I’ve got to change my Terminal from PowerShell to Git Bash. To do that, I push the **F1** key and, in the bar that appeared in the upper part of the VS Code window, write the following: `Select Default Profile`. A dropdown box appears, where I select the line that reads `Git Bash`.

By hitting the **+** button in the upper part of the Terminal I open another dropbox and strike the line that says `bash`.

### Global Configuration
When a user starts Git for the first time, he/she must specify some global settings, such as the user name, his/her email, etc. These are the necessary commands:

{% highlight bash %}
git config --global user.name 'Joshua Whizzarionetz'
git config --global user.email 'joshwhizz@outlook.com'
{% endhighlight %}

Of course, the name and email are fictional.

In order to avoid the CRLF conflict in Windows, one has to use the following command:
{% highlight bash %}
git config --global core.autocrlf  true
{% endhighlight %}

When the global configuration is finished, the user can have a look at all the settings by typing

{% highlight bash %}
git config --list
{% endhighlight %}

To get out of the list, just type in `Q`.

### Creating my first repository
The first step in making a repository is typing in `git init`, which is a command that creates a hidden folder **.git** where all the information concerning the current repo is stored:

{% highlight bash %}
$ git init
Initialized empty Git repository in D:/Git_Studies/.git/
{% endhighlight %}

Now, I can check the project’s status, and the command I need is

{% highlight bash %}
$ git status
On branch master

No commits yet  

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        css/
        index.html
        script/

nothing added to commit but untracked files present (use "git add" to track)
{% endhighlight %}

### The first commit ever
In general, the user’s modus operandi when dealing with Git is rather simple. First, you’ve got to add your file or files into staged, or tracked, area and then you make a commit.

So, let’s add the file **index.html** into staged area:

{% highlight bash %}
$ git add index.html
{% endhighlight %}

and check status after that:

{% highlight bash %}
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        css/
        script/
{% endhighlight %}

We can see that the folders **css** and **script** stay in the untracked condition whereas **index.html** became a tracked file. Let’s add all the files and folders to the staged area. To do that, we use the command

{% highlight bash %}
$ git add .
{% endhighlight %}

or

{% highlight bash %}
$ git add -A
{% endhighlight %}

Now, having checked the status, we get the following:

{% highlight bash %}
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   css/styles.css
        new file:   index.html
        new file:   script/script.js
{% endhighlight %}

And now, at last, we’re ready to make our first commit. And the command for that is `git commit -m 'DESCRIPTION'`. Let’s type it:

{% highlight bash %}
$ git commit -m 'initial commit'
[master (root-commit) b61eace] initial commit
 3 files changed, 41 insertions(+)
 create mode 100644 css/styles.css
 create mode 100644 index.html
 create mode 100644 script/script.js
 {% endhighlight %}

To make sure everything’s alright, I check the status:

{% highlight bash %}
$ git status
On branch master
nothing to commit, working tree clean
{% endhighlight %}

Nothing to commit. Perfect!

### New commits
It’s time to make changes in my files. I think my **index.html** file would do with a different heading, so I write a nicer one. I also change the background color for the page in the **styles.css** file. Once it’s done, I check the status.

{% highlight bash %}
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   css/styles.css
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
{% endhighlight %}

I can even trace the differences between earlier and later versions of the files by simply typing `git diff`.

{% highlight bash %}
$ git diff
diff --git a/css/styles.css b/css/styles.css
index 3310715..820021f 100644
--- a/css/styles.css
+++ b/css/styles.css
@@ -1,5 +1,5 @@
 html {
-    background-color: #F4E293;
+    background-color: #f1cae2;
 }

 h1 {
diff --git a/index.html b/index.html
index 2aa0659..4b689bc 100644
--- a/index.html
+++ b/index.html
{% endhighlight %}

The next step is adding both the files into staged area and checking status afterwards:

{% highlight bash %}
$ git add index.html css/styles.css
{% endhighlight %}

{% highlight bash %}
$ git status
On branch master        
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   css/styles.css
        modified:   index.html
{% endhighlight %}

And, of course, making a commit:

{% highlight bash %}
$ git commit -m 'changed H1, altered background color'
[master 88c1479] changed H1, altered background color
 2 files changed, 2 insertions(+), 2 deletions(-)
$ git status
On branch master
nothing to commit, working tree clean
{% endhighlight %}

What’s interesting and really useful about Git is the fact that you can trace all the history of your commits with the help of the command `git log --oneline`. (You can write simply `git log`,  but in this case the outcome tends to be too detailed which makes it more difficult to understand.)

{% highlight bash %}
$ git log --oneline
88c1479 (HEAD -> master) changed H1, altered background color
b61eace initial commit
{% endhighlight %}

Every commit has its unique, individual hash which you can use to check its content. For instance, let’s copy the hash of my first commit (b61eace) and paste it after the command `git show`:

{% highlight bash %}
$ git show b61eace
commit b61eace9e58ae87dba1bfd64632a374528b227ad
Author: Joshua Whizzarionetz < joshwhizz@outlook.com >
Date:   Fri Oct 13 07:22:18 2023 +0300

    initial commit

diff --git a/css/styles.css b/css/styles.css
new file mode 100644
index 0000000..3310715
--- /dev/null
+++ b/css/styles.css
@@ -0,0 +1,21 @@
+html {
+    background-color: #F4E293;
+}
+
+h1 {
+    font-size: 40px;
+}
+
{% endhighlight %}

### How to get back to any of the previous commits

And now I’m going to make three commits and then take a look at their history. My commits are:
1.	Return to the initial heading (H1) of the post.
2.	Change the font color of all the paragraphs.
3.	Change the background color of all the paragraphs.

I’ll make every commit immediately after I’ve done the necessary corrections, one after another, using the command `git commit -a -m` (the `-a` means that the command automatically adds all the changes from the files already listed in the index).

Having done all that, I check the log:

{% highlight bash %}
$ git log --oneline
cdc26cf (HEAD -> master) changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

Now, what’s the use of that? It’s in the fact that with the help of those hashes you can retrieve their corresponding commits in order to correct the things that were done wrongly.

### Retrieving former versions of files before any commits have been made

Let’s say it suddenly dawned upon me that I desperately need adding another paragraph into my **index.html**. I do that and then check the status.

{% highlight bash %}
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
{% endhighlight %}

But then I realize that adding that paragraph was wrong, that what I really needed there was, say, an unordered list of reasons why using Git is so good. To do that, I get back to the previous version of the **index.html** file using the command `git checkout index.html`. By mentioning the file name, I make it possible to regain only this very file the way it was prior to adding the paragraph; otherwise all the project would return to its previous stage.

{% highlight bash %}
$ git checkout index.html
Updated 1 path from the index
{% endhighlight %}

Now I look at the project home page and notice that the unnecessary paragraph is gone. If I choose to check the status, I’ll get the message:

{% highlight bash %}
$ git status
On branch master
nothing to commit, working tree clean
{% endhighlight %}

The command `git checkout` can also be used in case some file or folder has been unintentionally lost. For example, I removed my **styles.css** file by mistake. To get it back, I’ve got to type `git checkout css/styles.css`. If I was so inattentive that had wiped out the entire **css** directory, I should write just `git checkout css`.

### Returning to previously made commits

To roll back to any existing commit, I need to know its hash. First, I go ahead and have a look at my log, then copy the hash of the commit I want to get back to, and paste it right after the command `git checkout`, this way: `git checkout COMMITHASH`.

To regain only one of the files in its former condition, I must specify its name after the hash, e.g. `git checkout COMMITHASH css/styles.css`.

So, let’s roll the entire project back to a certain stage, but we’ve got to look at our log first. Here it is:

{% highlight bash %}
$ git log --oneline
cdc26cf (HEAD -> master) changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

I want to roll it back to the commit named “returned original H1”. So I type in the command

{% highlight bash %}
$ git checkout 1142e60
Note: switching to '1142e60'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 1142e60 returned original H1
{% endhighlight %}

Then check the status:

{% highlight bash %}
$ git status
HEAD detached at 1142e60
nothing to commit, working tree clean
{% endhighlight %}

The whole project has rolled back to where I wanted it to. Let’s check the log:

{% highlight bash %}
$ git log --oneline
1142e60 (HEAD) returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

There are only the commits here that had been made from the start of the project and on till the moment I decided to get the old title back. The ones that occurred after that are gone, and so their hashes. But what can I do if I feel I must regain the latest commit, the one where I changed the background color of my paraghaphs?

The thing about that commit that I happen to remember is it's still labeled **master**, and I can use it to roll the commit back. To do that, I type in the command `git checkout master`:

{% highlight bash %}
$ git checkout master
Previous HEAD position was 1142e60 returned original H1
Switched to branch 'master'
{% endhighlight %}

And the log now is exactly the way it used to be:

{% highlight bash %}
$ git log --oneline
cdc26cf (HEAD -> master) changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

Now it comes to my mind that the button on the home page is too big, and I’m going to downsize it by making the paddings smaller. So I make corresponding changes in my **styles.css** file. After that, I make a commit.

{% highlight bash %}
$ git commit -a -m 'downsized button'
[master df8f412] downsized button
 1 file changed, 1 insertion(+), 1 deletion(-)
{% endhighlight %}

And I check the status, just in case:

{% highlight bash %}
$ git status
On branch master
nothing to commit, working tree clean
{% endhighlight %}

### Exploring branches

Branches are much like savings in video games — different changes in branches lead to various kinds of development of your project. Making commits in those branches we can compare them to each other and choose the best ones.

Now, let’s take a glimpse at our log:

{% highlight bash %}
$ git log --oneline
df8f412 (HEAD -> master) downsized button
cdc26cf changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

The idea that has just come to my mind is to start a new branch based on the last commit (downsized button). I think the name **css_build** would suit the new branch perfectly, so the command I need to do that is `git checkout -b css_build`.

{% highlight bash %}
$ git checkout -b css_build
Switched to a new branch 'css_build'
{% endhighlight %}

Have a look at the log, again:

{% highlight bash %}
$ git log --oneline
df8f412 (HEAD -> css_build, master) downsized button
cdc26cf changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

Right now, branches **master** and **css_build** are at the same commit. Let’s check the status to understand which branch I’m at now.

{% highlight bash %}
$ git status
On branch css_build
nothing to commit, working tree clean
{% endhighlight %}

So, now I’m in the branch **css_build**, and before that, I was in the branch **master** — “On branch master,” Git kept reminding me when I was checking the status.

Next step I’m going to do is put an **<hr>** element between the first and the second paragraphs, and then I’ll make a commit.

{% highlight bash %}
$ git commit -a -m 'placed horizontal rule between first and second paragraphs'
[css_build 7ac75da] placed horizontal rule between first and second paragraphs
 1 file changed, 1 insertion(+)
{% endhighlight %}

And what does my log have to say?

{% highlight bash %}
$ git log --oneline
7ac75da (HEAD -> css_build) placed horizontal rule between first and second paragraphs
df8f412 (master) downsized button
cdc26cf changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

It says the branch master is no longer ahead, and the head now is at **css_build** branch — that’s where I’m at now.

For clarity’s sake, let’s make some changes in the **master** branch. But first I’ll move there.

{% highlight bash %}
$ git checkout master
Switched to branch 'master'
{% endhighlight %}

And now I want to wipe out the content of my `<title>` element in index.html and write there something completely different. And make a commit afterwards, of course.

{% highlight bash %}
$ git commit -a -m 'changed TITLE in HEAD'
[master bbccc80] changed TITLE in HEAD        
 1 file changed, 1 insertion(+), 1 deletion(-)
{% endhighlight %}

And what’s in the log?

{% highlight bash %}
$ git log --oneline
bbccc80 (HEAD -> master) changed TITLE in HEAD
df8f412 downsized button
cdc26cf changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

I’m in the **master** branch, and I can’t see the **css_build** branch at all. But if I add the `--all` flag to the same very command, I’ll get

{% highlight bash %}
$ git log --oneline --all
bbccc80 (HEAD -> master) changed TITLE in HEAD
7ac75da (css_build) placed horizontal rule between first and second paragraphs
df8f412 downsized button
cdc26cf changed background color of paragraphs
bc50655 changed font color of paragraphs
1142e60 returned original H1
88c1479 changed H1, altered background color
b61eace initial commit
{% endhighlight %}

I can see now all the commits. They are time-sequenced, starting from the bottom item (initial commit) to the upper one (the last commit). The **HEAD** label says where I’m at now — in the **master** branch.

And if I add the `--graph` flag to the `log` command, I’ll be able to see the spots where all the forks take place:

{% highlight bash %}
$ git log --oneline --all --graph
* bbccc80 (HEAD -> master) changed TITLE in HEAD
| * 7ac75da (css_build) placed horizontal rule between first and second paragraphs
|/
* df8f412 downsized button
* cdc26cf changed background color of paragraphs
* bc50655 changed font color of paragraphs
* 1142e60 returned original H1
* 88c1479 changed H1, altered background color
* b61eace initial commit
{% endhighlight %}

The commits in the **master** branch took their positions on the left side, and the only **css_build** commit moved a little to the right. Like the **master** branch, **css_build** starts at the initial commit but takes off to the left after the commit labeled “downsized button”.

Now I’ll try to make a fork at the commit “changed font color of paragraphs”. First, I must move there using the commit’s hash. My command will look like `git checkout -b html_css bc50655`, where


* -b — creates a new branch
* html_css — the name of the new branch
* bc50655 — the hash of the commit

{% highlight bash %}
$ git checkout -b html_css bc50655
Switched to a new branch 'html_css'
{% endhighlight %}

Back to the log in its graphic presentation:

{% highlight bash %}
$ git log --oneline --all --graph
* bbccc80 (master) changed TITLE in HEAD
| * 7ac75da (css_build) placed horizontal rule between first and second paragraphs
|/
* df8f412 downsized button
* cdc26cf changed background color of paragraphs
* bc50655 (HEAD -> html_css) changed font color of paragraphs
* 1142e60 returned original H1
* 88c1479 changed H1, altered background color
* b61eace initial commit
{% endhighlight %}

I’m now at the commit “changed font color of paragraphs”. I’m going to define there a different font size and its color for my button in the **styles.css** file. Then I want to make another commit.

{% highlight bash %}
$ git commit -a -m 'changed font size and color for button'
[html_css 8385594] changed font size and color for button
 1 file changed, 2 insertions(+), 2 deletions(-)
{% endhighlight %}

And now the log:

{% highlight bash %}
$ git log --oneline --all --graph
* 8385594 (HEAD -> html_css) changed font size and color for button
| * bbccc80 (master) changed TITLE in HEAD
| | * 7ac75da (css_build) placed horizontal rule between first and second paragraphs
| |/
| * df8f412 downsized button
| * cdc26cf changed background color of paragraphs
|/
* bc50655 changed font color of paragraphs
* 1142e60 returned original H1
* 88c1479 changed H1, altered background color
* b61eace initial commit
{% endhighlight %}

I’m moving into the **master** branch:

{% highlight bash %}
$ git checkout master
Switched to branch 'master'
{% endhighlight %}

And the log again:

{% highlight bash %}
$ git log --oneline --all --graph
* 8385594 (html_css) changed font size and color for button
| * bbccc80 (HEAD -> master) changed TITLE in HEAD
| | * 7ac75da (css_build) placed horizontal rule between first and second paragraphs
| |/
| * df8f412 downsized button
| * cdc26cf changed background color of paragraphs
|/
* bc50655 changed font color of paragraphs
* 1142e60 returned original H1
* 88c1479 changed H1, altered background color
* b61eace initial commit
{% endhighlight %}

The **HEAD** label is now at the **master** branch, and that’s where I’m at now.

### How to push your project to GitHub
Now, I’m in my account at GitHub. I start a new repository (the “New” green button in the left column, above the list of my repos). I give it a name (git_studies) and make the project public. I can add a README file and write a description, but that’s optional, and I feel no need to do it for a temporary project like that. I strike the button “Create repository” at the bottom of the page.

GitHub supplies me with the address of my `.git` file: `https://github.com/maxhomm/git_studies.git`.

Now, in my VS Code console, I type in the command

{% highlight bash %}
$ git remote add origin https://github.com/maxhomm/git_studies.git
{% endhighlight %}

It adds the remote repository named **origin** located at the given address. And now the next command:

{% highlight bash %}
$ git push -u origin master
Enumerating objects: 29, done.
Counting objects: 100% (29/29), done.
Delta compression using up to 4 threads
Compressing objects: 100% (23/23), done.
Writing objects: 100% (29/29), 3.46 KiB | 46.00 KiB/s, done.
Total 29 (delta 6), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (6/6), done.
To https://github.com/maxhomm/git_studies.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
{% endhighlight %}

The `-u` parameter here is the shortened flag `--set-upstream`, it configures the branch. This `-u` allows me not to define any additional parameters in future; my local branch from now on will be automatically connected with the remote one every time I use just `git push`.

If it’s my first push in the account, a sign in popup window appears where I have to fill in my credentials.

My repository is now live and on.

Now I’m going to change the name of my web page in the `<title>` element (again?!?!?!!!). Having done that, I make a commit and then push the project to GitHub.

{% highlight bash %}
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 369 bytes | 369.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0        
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/maxhomm/git_studies.git
   bbccc80..0989aaa  master -> master
{% endhighlight %}

### How to push another branch to GitHub
I’m still eager to explore the possibilities of Git, so I thought I would create a new branch on my computer and then move in there. Let’s assume I’m a student at some IT courses and, having finished my homework on Lesson 2, I’m going to start doing tasks of Lesson 3. Naturally, I need a new branch for it, so I’ll name the branch **lesson03**.

{% highlight bash %}
$ git checkout -b lesson03
Switched to a new branch 'lesson03'
{% endhighlight %}

Now I’ll create a new file **newfile.css** and fill it with some content. Then I’ll check the status.

{% highlight bash %}
$ git status
On branch lesson03
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        css/newfile.css

nothing added to commit but untracked files present (use "git add" to track)
{% endhighlight %}

I can see there’s a new untracked file. Let’s add it along with the entire project:

{% highlight bash %}
$ git add .
{% endhighlight %}

Then make a commit.

{% highlight bash %}
$ git commit -m 'newfile.css created'
[lesson03 258986e] newfile.css created
 1 file changed, 3 insertions(+)
 create mode 100644 css/newfile.css
{% endhighlight %}

Finally, I’m pushing the project into a new branch at GitHub.

{% highlight bash %}
$ git push origin lesson03
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 430 bytes | 143.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'lesson03' on GitHub by visiting:
remote:      https://github.com/maxhomm/git_studies/pull/new/lesson03
remote:
To https://github.com/maxhomm/git_studies.git
 * [new branch]      lesson03 -> lesson03
{% endhighlight %}

The two last lines of the message tell me there’s been created a new branch at GitHub, it’s called **lesson03**, and it’s filled with the content of my local branch **lesson03**.

At my GitHub page, I can see there are two branches now in my repository, **master** and **lesson03**. I find my **newfile.css** in the **lesson03** branch, but there’s no such file in the **master** branch.


### How to download, or pull, your project from Git to your local machine
Now my aim is to download the project into a certain folder on my computer. To begin with, I create it under the name of **git_pull**. But the truth is, it doesn’t matter what its name is, you can give it any name you choose.

Then I open this newly created directory and right-click any place inside it. I see a dropdown menu popup, and there I hit the line “GIT Bach here”, which causes a Terminal window to appear, where I type in the following command:

{% highlight bash %}
$ git clone https://github.com/maxhomm/git_studies.git
Cloning into 'git_studies'...
remote: Enumerating objects: 36, done.
remote: Counting objects: 100% (36/36), done.
remote: Compressing objects: 100% (22/22), done.
remote: Total 36 (delta 7), reused 36 (delta 7), pack-reused 0
Receiving objects: 100% (36/36), 4.16 KiB | 53.00 KiB/s, done.
Resolving deltas: 100% (7/7), done.
{% endhighlight %}

Now the project has been cloned to my local machine. But when I open its directory in Windows Explorer of VS Code, I don’t see my **newfile.css** there. That’s because only the **master** branch was downloaded, and **newfile.css** is in the branch **lesson03**. To download **lesson03**, I have to get back to my VS Code and open there the directory **git_studies**, which is now inside the folder **git_pull**, and type in the code editor’s Terminal the command

{% highlight bash %}
$ git pull origin lesson03
From https://github.com/maxhomm/git_studies  
 * branch            lesson03   -> FETCH_HEAD
Updating 0989aaa..258986e
Fast-forward
 css/newfile.css | 3 +++
 1 file changed, 3 insertions(+)   
 create mode 100644 css/newfile.css
{% endhighlight %}

The **lesson03** branch has been cloned to my desktop too.
