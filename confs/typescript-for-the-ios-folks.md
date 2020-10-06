For NSSpain 2020 /

## Intro

[I'm orta blah]

## A quick comparison

We're going to try get the easy stuff covered fast, mainly so that we can get to the good stuff.

Here's a class:

```swift
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

```ts
class VideoMode {
  resolution = new Resolution();
  interlaced = false;
  frameRate = 0.0;
  name;
}
```

Here's a struct (and a struct-ish):

```ts
struct Resolution {
    var width = 0
    var height = 0
}
```

```ts
const Resolution = {
  width: 0,
  height: 0,
};
```

And functions can be basically the same:

```swift
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
```

```ts
function greetAgain(person: string): string {
  return "Hello again, " + person + "!";
}
```

Swift's `protocol`s - well there are ways to re-create a few of it's more advanced features, but in TypeScript we
basically have the same thing as Objective-C's interfaces:

```swift
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}
```

```ts
interface SomeProtocol {
  mustBeSettable: number;
  readonly doesNotNeedToBeSettable: number;
}
```

Weirdly, TypeScript has a second variant of this code:

```ts
type SomeProtocol = {
  mustBeSettable: number;
  readonly doesNotNeedToBeSettable: number;
};
```

Odd, this feature both confuses newbies and oldbies alike. Moving code between files and targets is a bit different

```ts
import MyKit

myFunc("123")
```

```ts
import MyKit from "mykit";

MkyKit.myFunc("123");
```

or

```ts
import { myFunc } from "mykit";

myFunc("123");
```

Personally, I prefer this way, because it's explicit where every function, object or type comes from.

OK, that's enough covering the basics, you could use that knowledge to get a lot of pretty simple programs done.

Let's talk about the more interesting problem. Why make TypeScript?

---

Obj-C without the C

---

This wasn't the only way that it could have gone, back in 2014 I asked Andy Arvantis to give a talk at a CocoaPods meetup about his version of Objective-C but with the C. Eero (aero). He created a language which converted directly to Objective-C, and then that was compiled to make your app.

```eero
#import "GHDAppDelegate.h"
#import 'GHDMainViewController.h'

using prefix UI

interface GHDAppDelegate ()
   NavigationController navigationController {nonatomic, strong}
end


implementation GHDAppDelegate

   #pragma mark UIApplicationDelegate

   application: Application, didFinishLaunchingWithOptions: Dictionary, return BOOL

      mainViewController := GHDMainViewController.alloc.initWithNibName: nil, bundle: nil

      self.navigationController = NavigationController.alloc.initWithRootViewController: mainViewController

      self.window = Window.alloc.initWithFrame: Screen.mainScreen.bounds
      self.window.backgroundColor = Color.whiteColor
      self.window.rootViewController = self.navigationController
      self.window.makeKeyAndVisible

      return YES

end
```

The language had features to drop prefixes, used indentation instead of curly braces and always used dot notation.
It wasn't a drastic re-write, but it would be pretty trivial to port any Objective-C to Eero.

This process was the route that TypeScript made: TypeScript is JS but with the JS.

To understand this we need to cover the idea of "expression space" and "type space" - you do this in your head already to write code, but I want to make it explicit.

```swift
struct Person {
  let name: String
}

func greeting(person: Person) -> String {
    return "Hello again, " + person.name + "!"
}

let person = Person(name: "Danger")
let msg = greeting(person: person)
print(msg)
```

Here we have a code sample which does three things, it declares a struct, a function and then uses it.

Let's highlight the expression space. Expressions are compiler-speak for basically the runtime code, the stuff that is actually evaluated - I had a bit of trouble making some decisions on what to highlight here so let's call it a reasonably complex topic which I'm not going into.

Next we'll look at the type space. Again, a simplification. But you can think of it as the parts of the language which tell the Type System exactly what types are coming in and out.

TypeScript aims to only add code in the type space.

```js
function greeting(person) {
  return "Hello again, " + person.name + "!";
}

let person = { name: "Danger" };
let msg = greeting(person);
console.log(msg);
```

```ts
interface Person {
  name: string;
}

function greeting(person: Person): string {
  return "Hello again, " + person.name + "!";
}

let person = { name: "Danger" };
let msg = greeting(person);
console.log(msg);
```

This is the key goal of TypeScript, don't add cool new expression features to JavaScript, make it character to character the same but also allow for this new type space where you can design the connections between your objects.

This is why TypeScript won the "compile to JavaScript" wars - there have been a lot of languages which aim to improve writing code which runs in a web browser (Objective-J) but every improvement to JavaScript or new language feature which has to be ported over brings a level of mis-direction. I started my career as a mac programmer using RubyCocoa which as Ruby mapped to Objective-C, and to be proficient in it you had to be a master of both Objective-C and Ruby. You needed to understand the constraints of both languages and how a Ruby thing could work _as_ an Objective-C thing to debug a problem.

TypeScript has none of that, you're writing JavaScript and you're also adding types in a few places.

I'm almost done here but I need to repeat this point above. Because TypeScript aims to be "types only" TypeScript _cannot_ add new syntax outside of the type space. Basically these positions in the source code:

```ts
interface XY {}

type ZX = {};

const a: thing = "123" as string;

function abc(name: string): number {}
```

Because of that... You're going to see some really odd looking features in this language. So, lets go in escalating levels of 'Huh?'

## JSDoc

Let's start with the fact that around 70% of the features in TypeScript have the ability to be defined in a comment.

You'll have seen code like this:

```swift
/// Creates an `AuthenticationInterceptor` instance from the specified parameters.
///
/// - Parameters:
///   - authenticator: The `Authenticator` type.
///   - credential:    The `Credential` if it exists. `nil` by default.
///   - refreshWindow: The `RefreshWindow` used to identify excessive refresh calls. `RefreshWindow()` by default.
function createAuth(authenticator: AuthenticatorType,
            credential: Credential? = nil,
            refreshWindow: RefreshWindow? = RefreshWindow()) -> AuthenticationInterceptor {
    return AuthenticationInterceptor(credential, refreshWindow)
}
```

I based this same on the Alamofire source code, it's documenting a function and providing addition info on the parameters. 
In TypeScript, you could do something like:

```swift
/// Creates an `AuthenticationInterceptor` instance from the specified parameters.
///
/// - Parameters:
///   - authenticator: {AuthenticatorType} The `Authenticator` type.
///   - credential:    {Credential}        The `Credential` if it exists. `nil` by default.
///   - refreshWindow: {RefreshWindow}     The `RefreshWindow` used to identify excessive refresh calls. `RefreshWindow()` by default.
/// - Returns: {AuthenticationInterceptor}
function createAuth(authenticator,
            credential = nil,
            refreshWindow = RefreshWindow()) {
    return AuthenticationInterceptor(credential, refreshWindow)
}
```

This takes all of the type definitions out of the code, and moves it entirely into the comments. Kinda wild that they both exist, infact this entire feature is basically one person's work on the team - he keeps finding ways creative ways to let people use JavaScript code without annotations.

```ts
/**
 * Creates an `AuthenticationInterceptor` instance from the specified parameters.
 * 
 * @param {AuthenticatorType} authenticator The `Authenticator` type.
 * @param {Credential} credential The `Authenticator` type.
 * @param {RefreshWindow} refreshWindow The `Authenticator` type.
 * @param {AuthenticationInterceptor}
 */
function createAuth(authenticator, 
             credential = null, 
             refreshWindow = new RefreshWindow()) {
    return new AuthenticationInterceptor(credential, refreshWindow)
}
```

Kinda cool.

## Structural Types

OK, let's talk about how you can assign objects. 

```ts
struct Resolution {
    var width = 0
    var height = 0
}

struct Rectangle {
    var width = 0
    var height = 0
}

var a = Resolution(width: 100, height: 200)
var b = Rectangle(width: 100, height: 200)

a = b
b = a
```

Even though a `Resolution` and a `Rectangle` are the exact same shape - they are not interchangable without work. 
This is called a nominal type system, basically what matters is the identifier - the name of the type, not actually what's inside it. I mean, a resolution and a rectangle have different contextual meaning right?

```ts
type Resolution = {
    x: number
    y: number
}

type Rectangle = {
    x: number
    y: number
}

let a: Resolution = { x: 100, y: 200 }
let b: Rectangle = { x: 100, y: 200 }

a = b
b = a
```

Well TypeScript has to map existing code and existing code is pretty wild. 

- Type Literals

This is where

```ts
```


- Unions
- Mapped Types
- Conditional Types
- Template Literal Types
