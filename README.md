#The repository structure

Our central repository will hold two branches (their names are self-explanatory):

* production
* staging 
And in this new flow of development each developer | project domain gets its own repository.

#The Setup

How to set up your working environment:

Set up the special git subcommands by running (one time only and please mind the first period): 
````bash 
$> . /learn/scripts/git-aliases
```
Now set up your repository by running: 
```bash
$> git clone /learn/git/repositories/central-repository YOURUSERNAME-dev
```
Go into the newly created directory ( cd YOURUSERNAME-dev).
Now create your local staging branch by running: $> git branch staging origin/staging
If you run : 
```bash 
$> git branch ; then you should see listed two branches, production and staging.
```

# The git subcommands

This is how you will manage your self around:  

## git new <branch-name>

Creates a new branch. Everytime you want to start a new development: bug fix or new feauture. Don't mix logic work domains, if one branch is used for fixing a bug, stick to it and don't hack further, this will help you to keep the work organized and will avoid confusions later.

Conventions for your local branch-naming:

If you are fixing a bug then the name of the bug should follow the pattern bug-###; where the dashes should be substituted by the ticket number ( in case there is any ) or a relevant description of the bug. Examples: 
* bug-14456
* bug-ba_table_locking
In case you created a branch in order to develop a new feature, then the following pattern is encouraged: feature-###. In this case, dashes should be substituted by a relevant short-name that would help you to infeer what is being developed in that branch. Examples:
Since GIT encourages the usage of branches ( because they are inexpensive ) we are opting for branching as much as possible; this easy the control of our code in many ways, but most importantly will allow you to keep logically organize all of your work. It is worth mentioning that with this new flow, committing often is encouraged since you have your own space of development, your commits wont conflict or drag with it anyones changes ( by definition, you are only one changing files around ).  

```bash
git add < . | list-of-files >
git commit
```
For adding and committing your work into your local repository. Do this often. When committing give useful comments, why did you change what you changed? Comments like: "updating file1" are not useful at all.

## git log-commits

This subcommand will help you visualize how far you have developed your current branch by listing commit id and commit comment  of all those commits that are not merged into production. Also, on the list, those commits that are already merged into staging are marked ( those in staging already are marked with a (stag) label , otherwise empty. So you can have a clear view of what commits need to merged to which branches. 

## git sync

The sync subcommand automatically updates your production and staging branches, plus, it will incorporate into the current development branch all those new commits that were found in production. Running this command often ( once a day ) is encouraged as well.

## git squash

This command helps you to compress or group commits into one or more commits. Useful when commits are granular and extensive. IMPORTANT: This command is supposed to be used before merging any of your work into the staging or production branches. A detailed explanation on how it works can be found here: Git rebase interactive

## git staging

Staging subcommand will merge automatically all of your work into the staging branch.  

## git production

Production subcommand will merge automatically all of your work into the production branch.


## How to remove a branch? 
 In case one wants to get rid of a branch ( either because we are done or because we just want to throw away our work in that branch ) one has to follow the next commands: 

````bash
 $> git checkout production 

 $> git branch -d BRANCH-NAME 
```

 In case the deletion of the branch complains about not deleting the branch because there are some commits un-merged and you are sure that you want to delete the branch use -D instead of -d.

General GIT commit workflow (example)

(1) do your stuff commit properly on your branch / and sync

(2) Check your status
````bash $> git log-commits ```

(3) Push to staging
````bash $> git staging ```

(4) On Learn-E change to staging
```bash $> cd /learn/servers/staging ```

(5) Pull your commits (NOTE: sometimes commits from others are pulled as well - coordinate/communicate)
````bash $> git pull ```

(6) Test your stuff on staging!

(7) If everything is well continue and pussh to production
```bash $> cd /learn/serbers/your-dev/
$> git production
```

(8) Connect to Learn-D 
````bash
$> cd /learn/servers/production/
```

(9) $> git pull

... you are now productive!