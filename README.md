# Unary Short-circuit Operators for JavaScript

## Status
Current Stage:
* Stage 0

## Authors
* Wyatt Arent ([github](https://github.com/warent), [linkedin](https://www.linkedin.com/in/warent/), [hacker news](https://news.ycombinator.com/user?id=warent))

## Overview and motivation
When a variable exists but its truthiness is unknown, it is standard to utilize short-circuit logic to ensure a default value.
```javascript
// Greets a person. If no name is assigned, rename to "stranger"
function greet(people) {
    for (let person of people) {
        person.name = person.name || "stranger";
        console.log("Hello, " + person.name);
    }
}
```
This works well, but is verbose and redundant. `person.name` is referenced twice, and while this doesn't have any meaningful impact on performance, it does make the code unnecessarily repetitive with no added value.

The same applies for more functional applications.
```javascript
function render() {
    let toRender = this.props.component;
    toRender = toRender && this.modulatePass1(toRender);
    toRender = toRender && this.modulatePass2(toRender);
    toRender = toRender && this.modulatePass3(toRender);
    return toRender || "No component available!";
}
```
Again, here we're seeing a lot of repetitions--almost as much as using the ternary conditional. Even with full if/then/else conditionals this code just becomes bloated.

The unary short-circuit operators are intended to make code more elegant and terse.

## Syntax
### Unary OR
*Base case*. When the left-hand variable is falsey, evaluate and assign the right-hand value. Otherwise, keep original value.

```javascript
// Greets a person. If no name is assigned, rename to "stranger"
function greet(people) {
    for (let person of people) {
        person.name ||= "stranger";
        console.log("Hello, " + person.name);
    }
}
```

### Unary AND
*Base case*. When the left-hand variable is truthy, evaluate and assign the right-hand value. Otherwise, keep original value.

```javascript
function render() {
    let toRender = this.props.component;
    toRender &&= this.modulatePass1(toRender);
    toRender &&= this.modulatePass2(toRender);
    toRender &&= this.modulatePass3(toRender);
    return toRender || "No component available!";
}
```

## Notes
TODO

## Prior Art
TODO

## Specification
TODO

## TODO
Per the [TC39 process document](https://tc39.github.io/process-document/), here is a high level list of work that needs to happen across the various proposal stages.

* [ ] Identify champion to advance addition (stage-1)
* [ ] Prose outlining the problem or need and general shape of the solution (stage-1)
* [ ] Illustrative examples of usage (stage-1)
* [ ] High-level API (stage-1)
* [ ] Initial spec text (stage-2)
* [ ] Babel plugin (stage-2)
* [ ] Finalize and reviewer signoff for spec text (stage-3)
* [ ] Test262 acceptance tests (stage-4)
* [ ] tc39/ecma262 pull request with integrated spec text (stage-4)
* [ ] Reviewer signoff (stage-4)
