**Branching and merging:**

Magic lies in git branching.Wanna see? Follow along with the demo.

![](./images/media/image1.png){width="5.383721566054243in"
height="3.589148075240595in"}

![](./images/media/image2.png){width="5.453488626421697in"
height="3.8230653980752405in"}

**Merge conflicts**

Merge conflicts happen whenever two branches have 'line-level' content
conflict. It means if a file has been changed at the same line in two
branches after a common commit, then there will be a merge conflict if
one tries to merge the two branches. Git cannot decide which branch has
correct code, so it leaves marks inside the conflicting regions for the
programmer to solve.

To see a merge conflict yourself, make a new branch and commit something
in an existing file. Now go back to the main branch, edit the same line
in that file and commit it. At this point the main branch commit and the
other branch commit are a divergence of the same previous commit,
basically two different histories of the same file. Now merging the
other branch into master will result in a merge conflict.

![](./images/media/image3.png){width="4.122093175853018in"
height="2.945891294838145in"}

![](./images/media/image4.png){width="4.002987751531059in"
height="2.770255905511811in"}

Merge conflict marks in a file look like the following (the cat command
just lets us view the file):

1.  Line 1 says the current location which is HEAD (trying to merge
    another branch (newBranch) into the current branch (main), which is
    also the location of the HEAD pointer).

2.  Line 2 lists the contents present inside HEAD.

3.  Line 5 mentions the location (newBranch) that you're trying to merge
    into the current location (here I am trying to merge newBranch into
    the master branch using git merge newBranch while being present in
    the master branch).

4.  Line 4 lists the contents present in the newBranch branch.

5.  Line 3 is a separator between the two conflicting contents in both
    the branches.

Programmers have to manually solve this conflict by editing the messy
file itself. After removing the merge conflict disarrangement, my file
looks like this:

![](./images/media/image5.png){width="6.268055555555556in"
height="0.401162510936133in"}

Now staging the clean file using git add myFile.txt and committing it
using git commit \--message "Merge conflicts resolved", the merge
conflict has been resolved.

![](./images/media/image6.png){width="6.268055555555556in"
height="0.17248468941382328in"}

![](./images/media/image7.png){width="6.268055555555556in"
height="0.29791666666666666in"}

**Where can you get merge conflicts?**

Merge conflicts can be found during conflicting combinations, either
branch-branch combinations, branch-remote combinations, rebasing
different branches, or any new weird experiment you pull out yourself.\
The most common of these conflicting combinations is branch-remote
combination, which happens when your local computer's changes are
different from remote GitHub's changes (in the same file at the same
line of course) and vice versa.

Follow along to see merge conflicts in action

1.  Push your local repository on GitHub.

2.  Edit a line in a file in your local repository.

3.  Edit the same file on the same line on GitHub.

4.  Run git pull origin main locally to merge your GitHub repository
    into your local repository.

Here you have a new merge conflict right in front of you. Solve this as
a fun exercise and push it to your remote GitHub repository.

**Tip**

The command git pull origin main does two things in the background:

1\. git fetch origin main\
2. git merge

It is always suggested to manually run the git fetch origin main command
first, then git diff main..origin/main, followed by the git merge
command.

1.  The git fetch origin main command downloads the new changes from
    GitHub but doesn't merge it locally yet.

2.  The git diff main..origin/main command lists the new changes on the
    remote that is fetched above from the GitHub repository. This diff
    tool is used to diagnose any potential merge conflicts.

3.  Finally the git merge command actually merges the newly downloaded
    remote main branch into the local main branch.

**[Submodules]{.underline}**

Oftentimes one needs to use someone else's work from within their own
repository. A common issue arises in these scenarios: you want to be
able to treat the two projects as separate yet still be able to use one
from within the other.

The way you add another repository into your repository is by doing

git submodule add
[[https://github.com/userName/repoName.git]{.underline}](https://github.com/userName/repoName.git)

Anything you do outside of the submodule folder doesn't affect the
submodule folder, but every time you do anything in your submodule, you
need to 

1.  Commit the submodule repository, 

2.  Go out of the submodule repository while being inside the parent
    repository, and 

3.  Commit in the parent repository.

See carefully the following demo

![](./images/media/image8.png){width="5.238371609798775in"
height="3.623611111111111in"}

![](./images/media/image9.png){width="5.81053258967629in"
height="1.7561636045494313in"}

Whenever a repository having a submodule is pushed on GitHub, it shows
the submodule not as a regular folder but as a link to the submodule
repository.

![](./images/media/image10.png){width="5.231802274715661in"
height="2.4999737532808397in"}

Sometimes one needs to delete the submodule. Deleting a submodule
involves 3 steps

1.  Deleting the submodule folder itself

2.  Deleting the folder .git/modules/submoduleName (mind the 'dot')

3.  Editing the .gitmodules file and removing the lines for the
    submodule

Now staging and committing the repository again will have the submodule
removed completely. If you push the repo, the link to the submodule is
gone.

**[Task]{.underline}**

This is to see if you have understood using git from **terminal** in
conjunction with GitHub. Create a repository, and try out as many of
these commands as you can - create multiple branches, commits; try to
merge them. 

*Surf online (Pro Git book is the second best resource after
StackOverflow) how you can undo a commit (for those oopsies and spelling
mistakes, go back to a different commit to view older files, perhaps
even create a branch from an old point in history and merge it ;)*

You **must** be able to use the commands **add, commit, push, pull and
branch** as these are used very frequently. However, use this
opportunity to try out the rest as well, because they can get
challenging when you actually have to use them. To view how much you've
understood, we'd like you to share the history of your repo. 

For this type the commands:

1.  git log \--graph \--pretty=\"%C(bold blue)%h\" \--decorate \--all

2.  git log \--graph \--pretty=\"%C(yellow) Hash: %h %C(blue)Date: %ad
    %C(red) Message: %s \" \--date=human

3.  git log \--all \--decorate \--oneline \--graph

You can submit the outputs of these commands to us, preferably as text
file (.txt). Screenshots are also welcome.

**[Tip]{.underline}**

To put output of any command into a text file, use the following trick:

your command \>\> myNewFile.txt

This will put the entire output of the command in the newly generated
myNewFile.txt. Moreover, if you try to put content of a new command in
this file while this file is non-empty, it inserts the new output at the
end of the file without removing the old output already present.

Example:

dir \>\> myNewFile.txt

dir \| wc \>\> myNewFile.txt

any third command of your wish \>\> myNewFile.txt

Above chain of commands will insert the command outputs into the
myNewFile.txt file in order.
