## Design Pattern Lesson Learned

babygoat@twreporter.org

2018.04.26

---
## Outline

* Overview
    * What is design pattern?
    * Software design
* Factory Pattern

---
## What is design pattern?

Christopher Alexnder et al., 'A Pattern Language'

> A pattern is a process and a thing

---
## Process is "How to do"

e.g, Strategy, Observer, etc 

---
## Thing is "what to solve" or target

Erich Gamma, author "Gof Design Pattern", said

> Do not start immediately throwing patterns into a design, but use them as you go and understand more of the problem. Because of this I really like to use patterns after the fact, refactoring to patterns…

---
## Software design

* Top-down approach

e.g, Apply clean-architecture in project

* Bottom-up approach

e.g, Implement "Attack" in OLG by strategy pattern

---

Erich Gamma, author "Gof Design Pattern", said

> Rather than coming up with a set of interwoven patterns top-down, micro-architectures are more independent patterns that eventually relate to each other bottom-up. A pattern language guides you through the whole design, whereas we have these little pieces, bites of engineering knowledge. 

---

## Real world scenario: Both

---

## So how to use a pattern?

* Problem Analysis
    * (Name)
    * Context
    * Problem
    * Force
    * Solution
    * (Resulting Context)

---

## Factory Pattern

* Context:
    * Given a common "abstract product" interface which would be implmented by different product details. Client requires these "Concrete products".

* Problem: How to new an product?
---

## Factory Pattern

* Force:
    * Concrete product class is agnostic during compile-time.
    * Need arguments or objects to determine what product to build.

---

## Factory pattern

* Force(Cont.):
    * Naive way would be managing the building process in client side directly. However, client has to change from time to time whenever the product requirement changes.
    * Or using simple factory to encapsulate all the creation conditions (if else). However, once a new product is added, simple factory method should update accordingly.

---

## Factory Pattern

* Solution:
    * Encapsulate the building process within factory method and client is required to get the product through the method. Define an interface for creating an object, but let its subclass  which class to instantiate.

---

## Example

```javascript
// Parent object
function WarriorMaker() {}

// Common method
WarriorMaker.prototype.fight = function () {
    console.log("Use " + this.weapon + " to fight!")
}

```

---

## Example

```javascript
//Static factory method
WarriorMaker.factory = function(type) {
    var warrior, constr = type
    
    ...
    
    //Make child object inherent
    if(typeof WarriorMaker[constr].prototype.drive !== "function") [
      WarriorMaker[constr].prototype = new WarriorMaker()
    }
   
    warriror = new WarriorMaker[constr]();
    return warrior
}

```

---

## Example

```javascript

// Define child object
WarriorMaker.Archer = funciton() {
    this.weapon = "arch"
}

WarriorMaker.Saber = function() {
    this.weapon = "sword"
}
```

---

## Example

```
// Test
var archer = WarriorMaker.factory("Archer")
var saber = WarriorMaker.factory("Saber")

archer.fight() // "Use archer to fight!"
saber.fight() // "Use sword to fight!"
```
