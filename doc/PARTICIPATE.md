How to Participate as a Developer
===============================================================================

Contents
--------

1. [Code - Version Control](#code---version-control)
 - [Install git](#install-git)
 - [git](#git)
 - [git for svn users](#git-for-svn-users)
2. [GitHub Workflow](#github-workflow)
 - [How to Fork From Us](#how-to-fork-from-us)
 - [Keep Track of Updates](#keep-track-of-updates)
 - [Pull Requests or *Being Social*](#pull-requests-or-being-social)
 - [Maintainer Notes](#maintainer-notes)
3. [Coding Guide Lines](#coding-guide-lines)
4. [Commit Rules](#commit-rules)
5. [Test Suite Examples](#test-suite-examples)

*******************************************************************************

to do list:
- [ ] coding guide lines, styles/fileHeaders/...
- [x] commit rules
- [ ] compile suite movie -> COMMIT.md
- [x] git for svn users
- [x] explain pull requests

*******************************************************************************

Code - Version Control
----------------------

If you are familiar with git, feel free to jump to our [github workflow](#github-workflow) section.

### install git

**Debian/Ubuntu**:
- `sudo apt-get install git`

Optional *one* of these. There are nice GUI tools available to get an overview
on your repository.
- `gitk git-gui qgit gitg`

**Mac**:
- see [here](https://help.github.com/articles/set-up-git#platform-mac)
- you may like to visit http://mac.github.com/

**Windows**:
- see [here](http://lmgtfy.com/?q=debian+-+or+how+to+download+a+real+operating+system)
- just kidding, it's [this link](https://help.github.com/articles/set-up-git#platform-windows)
- please use UTF8 for your files and take care of
  [line endings](https://help.github.com/articles/dealing-with-line-endings#platform-windows)

**Configure** your global git settings:
- `git config --global user.name NAME`
- `git config --global user.email EMAIL@EXAMPLE.com`
- `git config --global color.ui "auto"` (if you like colors)
- `git config --global pack.threads "0"` (improved performance for multi cores)

You may even improve your level of awesomeness by:
- `git config --global branch.autosetuprebase always`
  (see how to [avoide merge commits](#keep-track-of-updates))
- `git config --global rerere.enable 1`
  (see [git rerere](http://git-scm.com/blog/2010/03/08/rerere.html))



### git

Git is a *distributed* **version control system**. It helps you to keep your software
development work organized, because it keeps track of *changes* in your project.
It also helps to come along in **teams**, crunching on
the *same project*. Examples:
- Arrr, dare you other guys! Why did you change my precious *main.cpp*, too!?
- Who introduced that awesome block of code? I would like to pay for a beer as a reward.
- Everything is wrong now, why did this happen and when?
- What parts of the code changed since I went on vacation
  (to a conference, phd seminar,
   [mate](http://en.wikipedia.org/wiki/Club-Mate) fridge, ...)?

If *version control* is totally **new** to you (that's good, because you are not
[spoiled](http://www.youtube.com/watch?v=4XpnKHJAok8)) - please refer to a
beginners guide first.
- [git - the simple guide](http://rogerdudler.github.io/git-guide/)
- 15 minutes guide at [try.github.io](http://try.github.io)

Since git is *distributed*, no one really needs a server or services like
github.com to *use git*. Actually, there are even very good reasons why one should
use git even for **local** data, e.g. a master thesis (or your collection of ascii art
dwarf hamster pictures).

Btw, **fun fact warning**: [Linus Torvalds](http://en.wikipedia.org/wiki/Linus_Torvalds),
yes the nice guy with the pinguin stuff and all that, developed git to maintain
the **Linux kernel**. So that's cool, by definition.

A nice overview about the *humongous* number of tutorials can be found at
[stackoverflow.com](http://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide)
... but we may like to start with a git **cheat sheet** (is there anyone out there who knows more
than 1% of all git commands available?)
- [git-tower.com](http://www.git-tower.com/files/cheatsheet/Git_Cheat_Sheet_grey.pdf) (print the 1st page)
- [github.com - "cheat git" gem](https://help.github.com/articles/git-cheatsheet) (a cheat sheet for the console)
- [kernel.org](https://www.kernel.org/pub/software/scm/git/docs/everyday.html) *Everyday GIT with 20 commands or so*
- [an other interactive, huge cheat sheet](http://ndpsoftware.com/git-cheatsheet.html)
  (nice overview about stash - workspace - index - local/remote repositories)

Please spend a minute to learn how to write **useful**
[git commit](https://github.com/blog/926-shiny-new-commit-styles)
**messages** (caption-style, maximum characters per line, use blank lines, present tense)
and read our [commit rules](#commit-rules).

If you like, you can **credit** someone else for your **next commit** with:
- `git credit "John Doe" john@example.com`
- `git commit --author "$1 <$2>"`

### git for svn users

If you already used version control systems before, you may enjoy the
[git for svn users crash course](http://git.or.cz/course/svn.html).

Anyway, please keep in mind to use git *not* like a centralized version control
system (e.g. *not* like svn). Imagine git as your *own private* svn server
waiting for your commits. For example *Github.com* is only **one out of many** *sources for updates*.
(But of course, we agree to share our *finished*, new features there.)

GitHub Workflow
---------------

Welcome to github! We will try to explain our coordination strategy (I am out
of here!) and our development workflow in this section.

### How to fork from us

To keep our development fast and conflict free, we recomment you to
[fork](https://help.github.com/articles/fork-a-repo) our **dev** (development)
branch into your private repository. Simply click the *Fork* button above to do so.

Afterwards, `git clone` **your** repository to your
[local machine](https://help.github.com/articles/fork-a-repo#step-2-clone-your-fork).
But that is not it! To keep track of the original **dev** repository, add
it as another [upstream](https://help.github.com/articles/fork-a-repo#step-3-configure-remotes).
- `git remote add upstream https://github.com/ComputationalRadiationPhysics/picongpu.git`

Well done so far! Just start developing. Just like this? No! As always in git,
start a fresh branch with `git branch <yourFeatureName>` and apply your changes there.

### Keep track of updates

We consider it a **best practice** *not to modify your master* branch branch at
all. Instead you can use it to `pull` new updates from the original
repository. Take care to **switch to dev** by `git checkout dev` to start
**new feature branches** from **dev**.

So, if you are really clever, you can even
[keep track](http://de.gitready.com/beginner/2009/03/09/remote-tracking-branches.html)
of the *original dev* branch that way. Just start your new branch with
`git branch --track <yourFeatureName> upstream/dev`
instead. This allows you to immediatly pull or fetch from **our dev** and avoids
typing (during `git pull`).

You should **add updates** from the original repository on a **regular basis**
or *at least* when you *finished your feature*.
- commit your local changes in your *feature branch*: `git commit`

Now you *could* do a normal *merge* of the latest `upstream/dev` changes into
your feature branch. That is indeed possible, but will create an ugly
[merge commit](http://kernowsoul.com/blog/2012/06/20/4-ways-to-avoid-merge-commits-in-git/).
Instead try to first update *the point where you branched from* and apply
your changes again. That is called a **rebase** and is indeed less harmful as
reading the sentence before:
- `git checkout <yourFeatureName>`
- `git pull --rebase`

Now solve your conflicts, if there are any, and you got it! Well done!

### Pull requests or *being social*

How to propose that **your awesome feature** (we know it will be awesome!) should be
included in the **mainline PIConGPU** version?

Due to the so called
[pull requests](https://help.github.com/articles/using-pull-requests)
in *GitHub*, this quite easy (yeah, sure). We start again with a
*forked repository* of our own. You already created a **new feature branch**
starting from our **dev** branch and commited your changes. Finally, you
[pushed](http://www.mariopareja.com/blog/archive/2010/01/11/how-to-push-a-new-local-branch-to-a-remote.aspx)
your local branch to *your* GitHub repository: `git push -u origin <yourLocalBranchName>`

Now let's start a *review*. Open the *GitHub* homepage, go to your repository and
switch to your *pushed feature branch*. Select the green **compare & review**
button. Now compare the changes between **your feature branch** and **our dev**.

Everything looks good? Submit it as a **pull request** (link in the header).

Afterwards, a fruitful ( *wuhu, we love you - don't be scared* ) *discussion*
about your **submitted change set** will start. If we find some things you
could *improve* ( *That looks awesome, all right!* ), simply change your
*local feature branch* and *push the changes back* to your GitHub repository,
to **update the pull request**.

As a **best practive agreement**, we wait for at least **two** of our
[maintainers](../README.md#maintainers-and-core-developers) to review the pull
request until it is merged.

Sharing is caring! Thank you for participating, **you are great**!

### maintainer notes

- do not *push* to the main repository on a regular basis, use **pull request**
  for your features like everyone else
- **never** do a *rebase* on the upstream repositories
  (this causes heavy problems for everyone who pulls them)
- on the other hand try to use
  [pull --rebase](http://kernowsoul.com/blog/2012/06/20/4-ways-to-avoid-merge-commits-in-git/)
  to **avoid merge commits** (in your local/topic branches)
- do not vote on your *own pull requests*, wait for the other maintainers
- we try to follow the strategy of [a-successful-git-branching-model](http://nvie.com/posts/a-successful-git-branching-model/)

Last but not least, [help.github.com](https://help.github.com/) has a very nice
FAQ section.

*******************************************************************************

coding guide lines
------------------

Well - there are some! ;)
- *coming soon* (in a separate file)

Please **add the according license header** snippet to your *new files*:
- for PIConGPU (GPLv3+): `src/tools/bin/addLicense <FileName>`
- for libraries (LGPLv3+ & GPLv3+):
  `export PROJECT_NAME=libgpugrid && src/tools/bin/addLicense <FileName>`
- delete other headers: `src/tools/bin/deleteHeadComment <FileName>`
- add license to all .hpp files within a directory (recursive):
  `export PROJECT_NAME=PIConGPU && src/tools/bin/findAndDo <PATH> "*.hpp" src/tools/bin/addLicense`
- the default project name ist `PIConGPU` (case sensitive!) and adds the GPLv3+
  only.

*******************************************************************************

Commit Rules
------------

See our [commit rules page](COMMIT.md)

*******************************************************************************

Test Suite Examples
-------------------

You know a useful setting to validate our provided methods?
Tell us about it or add it to our test sets in the examples/ folder!
