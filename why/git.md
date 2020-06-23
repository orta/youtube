## Why Git?

- git from is a long lineage of version control software
- it sorta represents the end-state, while there may be better VCS after git will never be beaten
- it's kinda like the qwerty of VCS, some people will come up with better ways and like 10 people will use it and we'll probably be using git for the rest of our careers

## So what is git?

Git is a de-centralized version control system, which represents your code as a tree of changes over time. 

## What made it different?

There are a few key differences from before git:

- first "de-centralized"

  git took what used to be a server to client architecture, and flipped it to be client to client.
  This meant that everyone had a fully copy of the repo available at all times on their computer.

  this helped a lot in removing the 2nd key difference

- it was fast

  I used a few tools before adopting git: CVS and SVN and they were all extremely slow to use. 
  Doing anything effectively relied on asking the server what the difference was between your current setup and the main 

- it was free

  Back then you if you wanted to handle a large VCS you had to pay:

   - microsoft had SourceSafe
   - BitKeeper 
   - a main competitor was called Perforce 
  
### Competitors

seriously, 2004-2006 was the period to start a DVCS

- https://www.mercurial-scm.org (2005)
- https://fossil-scm.org/home (2006)
- bazaar (2004)

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
