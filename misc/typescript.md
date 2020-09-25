## Intro and what is TS?

Hi, I'm Orta and I'm a member of the TypeScript team. 

TypeScript is a project from Microsoft which aims to help the scalability of JavaScript projects by adding types to the language. 

JavaScript is the most popular programming language in the world - it got there by being the only programming language you can use to make a website interactive. So, the bigger and more complex the web became, the more requirements were needed in the JavaScript language. Over time, people started using JavaScript in all sorts of places, from applications to servers. These projects can be very big, and have a lot of contributors - JavaScript projects make up the majority of GitHub's most active repos for example.

Bigger projects need more tooling, and TypeScript provides that.

## Team Setup

The TypeScript team is split into two major sections, there's the TypeScript & JavaScript DevTools team and the Compiler Team. 

The DevTools team focuses on integration with Microsoft properties like Visual Studio and Visual Studio Code, owning areas like how the language communicates with these editors and large scale testing that TypeScript works at any scale. The compiler team focuses on, well, the compiler. This ranges from converting TypeScript code to JavaScript to the code inference which allows people to write less syntax.

Both of these teams collaborate to create the TypeScript project. 

## Problem Domain

TypeScript is an interesting in the programming language space because it has some interesting constraints. TypeScript's goal is to just add types to JavaScript, and to explicitly not be responsible for the features in JavaScript. 

This means the team can't add new syntax to the language whenever it wants nor does it control the JavaScript roadmap, because that is the responsibility of the JavaScript language committee TC39. The TypeScript team are members of TC39, but there's a lot of people and companies involved which makes for a great representation of the scale of JavaScript's usage

