I'm Orta Therox, a developer/designer working on the TypeScript team.

I've been writing code across many platforms for about 15 years. Let's politely call the first 5 years of that a write-off. Which means I have shipped about 10 years of useful professional code. It's hard to quantify how much of that code is still running or even can run today without work, but I'd be very suprised if even half of it is still in active use.

In the tech industry this idea known as code rot, and I want to try dive into some of the reasons why good code stops working. So, this is a rebase on 

---- intro ----

## How Does Un-Touched Code Rot?

Working on a software project is always about treading a balance between two major conflicts: Doing stuff and making it easy to do stuff over time. We tend to think of it in terms of 'features' vs 'tech debt'.

Software can grow eternally as a program grows to fully explore the design space for it's original goals, and that design space can expand as you see new horizons. 

For example, I doubt Linus was thinking about the ubiquity of android smart phones when Linux was starting to rattle around in his head and that the same project would be powering virtual apps inside virtual servers in containerized data-centers running under the sea. 

This trade-off can make figuring out what abstraction level you want to be working at a real struggle because you often want to be working a the highest level of abstraction possible - but the more layers of indirection you use, the more space there is for things to change without your influence.

That to me is one of the core idea when thinking about the long term maintainability for a project: at what point, does every abstraction you use, stop paying for itself.

#### Abstractions as Systems

Let's take two priors: All software is just shifting bits around in CPU registers, and that software is infinitely malleable. In theory, there's no conceptual difference to a processor between a python script running with a machine learning model to add coloured lipstick to a video or a bash script. As long as the programming environment is "turing complete" any program can be made by any environment.

However, there is a massive difference in the tooling for those environments and the sets of capabilities which that tooling makes easy. Minecraft, or the TypeScript type system may be turing complete environments but you're going to be facing one hell of a challenge in getting it to find the edges in an image. In python you have all sorts of well maintained dependencies and a lot of prior art to help you get there. 

This is one of the interesting parts of the JavaScript ecosystem, it's basically like the English language and everyone ends up catering for it: doing machine learning? Well Tensorflow was ported to JavaScript, want to build apps: you've got options like Electron or React Native, games you have WebGL and many game engines to work with.

The important question to consider is what does it mean for one of these abstractions to pay for itself?

#### Reading the Layers

If I wanted to build a codebase which would last 50 years, that single idea would severely constrain what sort of project I could make. You'd want to work with old, stable tools which haven't changed in years, which basically means using less layers of abstractions and only ones which have really proven themselves to last. For example, using the C language and it's standard library - or even HTML, you can still visit the world's first website created from 1989. I would bet a lot of money that in another 11 years that website will still be chugging along just fine in a modern browser.

###  How would you audit a layer?

Let's consider a modern website like the TypeScript site:

[React]
[React community ecosystem]
[Gatsby]
[Gatsby Dependency Tree] ()
[TypeScript]
[JavaScript]
[Node]
[v8]



You could use a language like C, which has a simple standard library which could be enough to make an app which doesn't have to 



- Apple's 32-bit wipe
- 

## The Business Needs Changed

I've spent 6 months working on a feature used 



- https://news.microsoft.com/features/under-the-sea-microsoft-tests-a-datacenter-thats-quick-to-deploy-could-provide-internet-connectivity-for-years/
- https://begriffs.com/posts/2020-08-31-portable-stable-software.html

