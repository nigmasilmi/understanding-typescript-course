# Understanding TypeScript Course by Maximilian Schwarzmüller

[udemy link](https://www.udemy.com/course/understanding-typescript)

## Installing and using TypeScript

[typescriptlang.org / install the compiler](https://www.typescriptlang.org/)

- invoke the compiler with

```
tsc <name-of-the-file>
```

## TypeScript Basics and Basic Types

[Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
[TypeScript types vs. JavaScript types](https://www.geeksforgeeks.org/difference-between-typescript-and-javascript/)

### Type Assignment and Type Inference

[article by Level Up Coding](https://levelup.gitconnected.com/type-annotation-vs-type-inference-in-typescript-85ba2194ebe1)

### Object Types

[objects handbook section](https://www.typescriptlang.org/docs/handbook/2/objects.html)

### TypeScript Tuples

[GeeksForGeeks article](https://www.geeksforgeeks.org/typescript-tuples/)

### Enums

[enums in handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#enums)

```ts
enum Flag {
  AMARILLO,
  AZUL,
  ROJO,
}

// will compile to this in JS:

var Flag;

(function (Flag) {
  Flag[(Flag["AMARILLO"] = 0)] = "AMARILLO";
  Flag[(Flag["AZUL"] = 1)] = "AZUL";
  Flag[(Flag["ROJO"] = 2)] = "ROJO";
})(Flag || (Flag = {}));

// and this

enum Places {
  FIRST = "first",
  SECOND = "2",
  THIRD = "tercero",
}

// will compile to this:
var Places;

(function (Places) {
  Places["FIRST"] = "first";
  Places["SECOND"] = "2";
  Places["THIRD"] = "tercero";
})(Places || (Places = {}));
```

### The "any" type

[any in the handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any)

### The | Union type

[go to the handbook chapter](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)

### The Literal types

[definition](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)
[inference](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-inference)

- is useful if we want a specific type but not use an enum

```ts
interface Literals {
  purchase: "PayPal" | "CreditCard";
}
```

### The "unknown" type

[see an article](https://mariusschulz.com/blog/the-unknown-type-in-typescript)<br />
The main difference between unknown and any is that unknown is much less permissive than any: we have to do some form of checking before performing most operations on values of type unknown, whereas we don't have to do any checks before performing operations on values of type any.

```ts
let userInput: unknown;
let userName: string;

userInput = 5;
userInput = "holamundo";
if (typeof userInput === "string") {
  userName = userInput;
}
```

### The "never" type

- exception or one that never returns. Variables also acquire the type never when narrowed by any type guards that can never be true.

```ts
function generateError(message: string, code: number): never {
  throw { message, errorCode: code };
}
```

### Type Aliases / Custom types

[handbook reference](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)

```ts
type Combinable = number | string;

let myVar: Combinable;

// or

type PurchaseType = "PayPal" | "CreditCard";
let purchase: PurchaseType;

// or

type User = { name: string; age: number };
let activeUser: User;
```

## Functions

[more on functions](https://www.typescriptlang.org/docs/handbook/2/functions.html)

### Function Return Types & void

```ts
// remember always prefer inference over typification

function add(n1: number, n2: number): number {
  return n1 + n2;
}

// with void

function printMessage(msg: string): void {
  console.log(msg);
}
```

### Functions as Types

```ts
let combineValues: Function; // this is valid but not precise
let moreCombining: (a: number, b: number) => number; // this is not an arrow function, this is a specific function type
moreCombining: add; // see add definition in the previous code block
moreCombining(4, 5); // is ok
moreCombining("a", 5); // not ok
```

### Function Types & callbacks

```ts
function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
  const result = n1 + n2;
  cb(result);
}

addAndHandle(1, 2, (theResult) => console.log(theResult));
```

- heads up: Callback functions can return something even if the argument on which they're passed does NOT expect a returnd value; so, this is valid code:

```ts
function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
  const result = n1 + n2;
  cb(result);
}

addAndHandle(1, 2, (theResult) => theResult);
```
