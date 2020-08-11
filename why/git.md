Hey folks, I'm orta therox - a developer / designer currently working on the TypeScript team at Microsoft. 
My work ranges from package managers, languages to figuring out how to describe and compose complex developer tools.

In this video we're gonna talk about why git was made

## Why Git?

So, git from is a long lineage of version control software. It sorta represents the end-state, while there may be better VCS after git will never be beaten.
It's kinda like the qwerty of VCS, some people will come up with better ways and like 10 people will use it and we'll probably be using git for the rest of our careers

## So what is git?

Git is an open source, de-centralized version control system, which represents your code as a tree of changes over time. 

### Generations of VCS

- Stage 1: files on disk (SCSS, RCS) - 1970s - fast but dumb
- Stage 2: central servers (CVS, SVN, Perforce) - 1990-2000s - smart but slow
 - CVS = you pull some files and push each one by one
 - SBV = chunk changes into a diff, and a diff could pass/fail being merged
- Stage 2.5: You have the files, but not quite smart enough 
 - Bitkeeper (files not changesets)
 - DARCs (first chunks)
 - Monotone (DAG (directed acyclic graph) with sha with SQLite as a db)
- Stage 3: duped files on disks stored in servers (BitKeeper, git, hg, fossil, bzr) - fast and smart

## What made it different?

There are a few key differences from before git:

- it was free

  Back then you if you wanted to handle a large VCS you had to pay:

   - microsoft had SourceSafe
   - BitKeeper 
   - a main competitor was called Perforce 

- first "de-centralized"

  git took what used to be a server to client architecture, and flipped it to be client to client.
  This meant that everyone had a fully copy of the repo available at all times on their computer.

  this helped a lot in removing the 2nd key difference

- it was fast

  I used a few tools before adopting git: CVS and SVN and they were all extremely slow to use. 
  Doing anything effectively relied on asking the server what the difference was between your current setup and the main 

  
### Competitors

seriously, 2004-2006 was the period to start a DVCS.

- git (2005)
- https://www.mercurial-scm.org (2005)
- https://fossil-scm.org/home (2006)
- bazaar (2004)

At the time the majority of OSS work was using BitKeeper, a closed-source VCS grudgingly.

> February of 2002, Linux creator Linus Torvalds decided that BitKeeper was "the best tool for the job" 
and started using it to manage the mainline kernel, 

https://web.archive.org/web/20120523134437/http://kerneltrap.org/node/4966


Hard to differentiate between them TBH:

```sh
hg clone https://www.mercurial-scm.org/repo/hello
cd hello
hg add .
hg commit -m 'My changes'
hg push
```

vs

```
git clone https://www.github.org/orta/why-make
cd hello
git add .
git commit -m 'My changes'
git push
```

So, realistically, git won because GitHub won! hah

### Git Evo

- git submodules
- git lfs - https://git-lfs.github.com
- `git switch` and `git restore` - https://www.infoq.com/news/2019/08/git-2-23-switch-restore/
- shallow clone
- git subtree

maybe not worth the section? 

### Reference 

Great reads!

- https://initialcommit.io/blog/Technical-Guide-VCS-Internals
- https://initialcommit.io/blog/Evolution-of-VCS-Internals-2

Useful for ref:

- https://en.wikipedia.org/wiki/Git
- https://tom.preston-werner.com/2009/05/19/the-git-parable.html
- http://mid.gmane.org/Pine.LNX.4.64.0605050944200.3622@g5.osdl.org
- http://mid.gmane.org/Pine.LNX.4.64.0610191258290.3962@g5.osdl.org
- http://verificationexcellence.in/basics-of-version-control/
