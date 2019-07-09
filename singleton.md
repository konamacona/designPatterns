---
marp: true
---

<!-- _class: lead -->

# Design Patterns: Singleton

### Mitch Keenan

---

# Design Patterns: Singleton

1. What are design patterns?
2. What is the Singleton pattern?
3. When should it be used?
4. Examples

---

# Design Patterns

> A **design pattern** is a general repeatable solution to a commonly occurring problem in software design.

– Gang of Four

Examples:

* **Singleton**
* Observer
* Factory

---

# Singleton

The intent of the Singleton is to...

> Ensure a class only has one instance, and provide a global point of access to it.

Which also implies that **it's only created once**

---

# When should Singleton be used?

When you need to

* Persist state and make it available throughout your codebase
* Provide access to a shared resource
* Model a **truly unique** domain class

---

# When should Singleton *not* be used?

* Modelling domain classes which are not unique
* *Ever?*

---

# Singletons in JavaScript - 1

```js
const myObject = {
  getMessage: function () {
    return "Pssst... Object Literals are secretly singletons";
  }
}
```

---

# Singletons in JavaScript - 2

```js
function MySingleton() {
  if (MySingleton.instance) {
    return MySingleton.instance;
  }

  MySingleton.getMessage = function () {
    return "I'm a singleton!!";
  }

  MySingleton.instance = this;
}

const s1 = new MySingleton();
const s2 = new MySingleton();
console.log(s1 === s2); // true
```

[demo](https://repl.it/repls/UnhealthyStupendousNagware)

---

# Singletons in TypeScript - 1

```typescript
class MySingleton {
  private static instance: MySingleton;

  private constructor () {}

  // Only way to access an instance of the class.
  static getInstance() {
    if(!MySingleton.instance) {
      MySingleton.instance = new MySingleton();
    }

    return MySingleton.instance;
  }
}

const s1 = MySingleton.getInstance();
const s2 = MySingleton.getInstance();
console.log(s1 === s2); // true

const s3 = new MySingleton(); // Compile time error
```

---

# Singletons in TypeScript - 2

```typescript
namespace MySingleton {
  // Any initialisation goes here

  export  getMessage() {
    return "I'm a singleton!!";
  }
}
const s3 = new MySingleton(); // Compile time error
```

---

# Angular Demo

[Demo](https://stackblitz.com/angular/yvoxyppqrkr?file=src%2Fapp%2Fitems%2Fitems.service.ts)

---

# Singleton Pros

1. Controlled access
2. Global State

# Singleton Cons

1. Hard to test
2. Global State
3. **Global State**

---

# Resources

## Demos

* [Typescript Singleton Demo 1](https://www.typescriptlang.org/play/#code/MYGwhgzhAECyCeBlAlgOwOYgKYBcD2q0A3gLABQ00ADgE7IBuYOW0EOTyw0abYqwWAFxwkaTLgIBucuUq0GTFsAJsaAV2D4a0ABQBKYgF8ZFaAHoz0APKoQ8aAHcw9-NDDABUN4R7t+LPAAzaBwACyVwKAA6WWo1ACMQTlZ2HGT0XABJVF5-fWJYymRAnQBCBBQMbHxUKN8+AQMiEUrxGrqcvwFoAF5oVCwHFrFqgn1JaGNTShpcNRpCCpGJWvr-aVMpqfJlTtYARl7hqpWojJxs3IFxnZUcVgAmI6WT9vPLrqwbsl2IPGwoiA8OgdBBDj0IY89BMLCF1FgTL97hAAMxHAZDF5tMbQ8yWADCeAAtlRkNgQsgiSwsDQaHgaEA)
* [Typescript Singleton Demo 2](https://www.typescriptlang.org/play/#code/MYGwhgzhAECyCeBlAlgOwOYgKYBcD2q0A3gLABQ00ADgE7IBuYOW0EOTyw0abYqwWAFxwkaTLgIBucuUq0GTFsAJsaAV2D4a0ABQBKYgF8ZFaAHoz0APKoQ8aAHcw9-NDDABUN4R7t+LPAAzaBwACyVwKAA6WWo1ACMQTlZ2HGT0XABJVF5-fWJYymRAnQBCBBQMbHxUKN8+AQMiEUrxGrqcvwFoAF5oVCwHFrFqgn1JaGNTShpcNRpCCpGJWvr-aVMpqfJlTtYARl7hqpWojJxs3IFxnZUcVgAmI6WT9vPLrqwbsl2IPGwoiA8OgdBBDj0IY89BMLCF1FgTL97hAAMxHAZDF5tMbQ8yWADCeAAtlRkNgQsgiSwsDQaHgaEA)
* [Javascript Demo](https://repl.it/repls/UnhealthyStupendousNagware)
* [Angular Demo](https://stackblitz.com/angular/yvoxyppqrkr?file=src%2Fapp%2Fitems%2Fitems.service.ts)

## Reading

* [Rod Dodson: Singleton](https://robdodson.me/javascript-design-patterns-singleton/) (*warning*: explicit language)
* [Source Making: Singleton](https://sourcemaking.com/design_patterns/singleton)
* [Addy Osmani: Singleton](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#singletonpatternjavascript)
* [Design Patterns - Gang of Four](http://www.uml.org.cn/c++/pdf/DesignPatterns.pdf) (*warning*: **slow** pdf link)
