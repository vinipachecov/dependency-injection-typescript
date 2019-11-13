# About this repo

This is a repo with the purpose of teaching myself the ideas and hands on examples of Dependency Injection <strong>with typescript
</strong>.

I have no copyrights to this code feel free to thank [Kevin](https://medium.com/@nehalist).

# About Depdency injection

Dependency injection is a powerfull parttern to organize our code structure.

This is a repo for my future self to always remember the usage and maybe help some lost souls in the subject during the learning process.

This repo follows the code, examples and explanations from the article: [dependency Injection in typescript](https://nehalist.io/dependency-injection-in-typescript/)

All my explanations here are my understandings of what the article attempts to teach.

- [A typical class structure without DI](#tipical-class-structure)
- [Solution with Dependency injection](#Solution-with-Dependency-injection)

## A typical class structure without DI

```ts
class Foo {}

class Bar {
  foo: Foo;

  constructor() {
    this.foo = new Foo();
  }
}

class Foobar {
  foo: Foo;
  bar: Bar;
  constructor() {
    this.foo = new Foo();
    this.bar = new Bar();
  }
}
```

The code above is just an example that repeats a lot in code without dependency injection. but <strong>what</strong> is repeating?<br>
What is repeating here is the instantiation and the parameters of classes that depends on a specific constructor.

> _Each time the use needs a class that depends from another class it will need to write the code to instantiate it, again and again and again...._

This doesn't sound very [DRY](https://deviq.com/don-t-repeat-yourself/) code...

## Solution with Dependency injection

Using Dependency injection this problems disappears giving us a much more testable, reliable code.

### First example

```ts
class Foo {}

class Bar {
  constructor(foo: Foo) {}
}

class Foobar {
  constructor(foo: Foo, bar: Bar) {}
}
```

This code already takes away the dependency problem but instantiation code doesn't look much better...

```ts
const foobar = new Foobar(new Foo(), new Bar(new Foo()));
```

This is where the <strong>injector</strong> comes in:

```ts
const foobar = Injector.resolve<Foobar>(Foobar); // returns an instance of Foobar, with all injected dependencies
```

Already looks cooler and more promising.
But:

- Where does this Injector class comes from?
- How does this Injector returns an instance of a giving class?
- Will it work for multiple classes?

## Dependency Injection with Typescript
