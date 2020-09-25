For NSSpain 2020

## Intro

[I'm orta blah]

## A quick comnparison

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

Swift's `protocol`s - well there are ways to re-create a few of it's more advanced features, but in TypeScript we basically have the same thing as Objective-C's interfaces:

```swift
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}
```

```ts
interface SomeProtocol {
    mustBeSettable: number,
    readonly doesNotNeedToBeSettable: number
}
```

Weirdly, TypeScript has a second variant of this code:

```ts
type SomeProtocol  = {
    mustBeSettable: number,
    readonly doesNotNeedToBeSettable:  number
}
```

Odd, this feature both confuses newbies and oldbies alike.
