
# Basics
There are two major 'types' of datatypes. Primitives, of which 7 out of 8 are, and Complex, of which 1 out of 8 are. Primitive datatypes can only store one value.

Complex datatypes can store a collection of values, with each value being of another datatype or itself. This complex datatype is called an **object**.

Objects store **store keyed collections of various data and more complex entities**.

An object can be created with figure brackets `{…}` with an optional list of _properties_. A property is a “key: value” pair, where `key` is a string (also called a “property name”), and `value` can be anything.
```javascript
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
```
Usually, the figure brackets `{...}` are used. That declaration is called an _object literal_.
## Literals and Properties
A property has a key (also known as “name” or “identifier”) before the colon `":"` and a value to the right of it. There are no limitations on these key names, words that would generally be restricted are allowed as object properties. Other, non-string datatypes are automatiacally converted into strings when used as keys, such as `0` -> `"0"`.
```javascript
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30        // by key "age" store value 30
};
```
We can access properties and their values using `.` notation.
```javascript
// get property values of the object:
alert( user.name ); // John
alert( user.age ); // 30
```
We can add/change values using the same syntax for variables. The `key` is the variable name (`object.keyName`) and the value is the value of that property.
```javascript
user.isAdmin = true;
```
To delete properties, we can use the `delete` operator.
```javascript
delete user.age;
```

We can also use property names that are multiple words, but they must be in quotes.
```javascript
let user = {
  name: "John",
  age: 30,
  "likes birds": true,  // multiword property name must be quoted
};
```
To call a property with a multi-word key, we use `['']` square brackets. 
```js
alert(user.["likes birds"])
```
Also, the last property may end with a comma. This is called a *trailing comma*.

Square brackets also be used to add properties last minute. The same can't be done with the `.` method.
```javascript
let user = {
  name: "John",
  age: 30
};
let key = prompt("What do you want to know about the user?", "name");
// access by variable
alert( user[key] ); // John (if enter "name")
```
Square brackets also enable complex functions such as adding a variable and name in the key section of a parameter. In general, when we know the values, we use dot notation but when something more complex is need we swap to square brackets.
```javascript
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

Somtimes, instead of typing the full property, it is faster to just type the value (and that value becomes the key too). Usually, this is done when variables are being used as properties.
```javascript
let user = {
  name,  // same as name:name
  age: 30
};
```
## "in" operator
We can check for the existence of a property in a dataset using the `in` operator.
```javascript
let user = { name: "John", age: 30 };

alert( "age" in user ); // true, user.age exists
alert( "blabla" in user ); // false, user.blabla doesn't exist
```
## Looping through Objects
We can loop through an Object using a `for` loop.
```javascript
for (key in object) {
  // executes the body for each key among object properties
}
```
An example is necessary to explain how it'd be done.
```javascript
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // keys
  alert( key );  // name, age, isAdmin
  // values for the keys
  alert( user[key] ); // John, 30, true
}
```

**Orders in Objects**
Generally, properties that have keys that are just numbered are ordered ascending from the smallest numbered key to the largest. 
```javascript
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

for (let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```
Otherwise, when they are non-number strings (strings that can't be converted into numbers and back), they are ordered by creation (the order above would be `49, 44, 41, 1`).

# Object References and Copying
When objects are copied, their references are copied, not the object itself.

The way it works in JS, the object is stored in one place and the reference to that object is stored in the variable where the object is created, which means that copying the variable copies the reference to the object, not the object itself.
```javascript
let user = { name: "John" };

let admin = user; // copy the reference
```
As you can see in this case, both variables reference the same object.
![[obj_reference_and_copying_diagram.png]]

[!Equality in Objects]
Two references to the same object are equal, but two objects that are identical are not equal. 
```js
let a = {};
let b = {}; // two independent objects

alert( a == b ); // false
```
Values stored in `const` variables can be modified. This is because the reference stays constant, but because the object is stored elsewhere, the properties of the object can modified freely.

## Duplicating Objects
We can duplicate objects by looping over all their properties.
```javascript
let user = {
  name: "John",
  age: 30
};

let clone = {}; // the new empty object

// let's copy all user properties into it
for (let key in user) {
  clone[key] = user[key];
}

// now clone is a fully independent object with the same content
clone.name = "Pete"; // changed the data in it

alert( user.name ); // still John in the original object
```
Or, we can use the `Object.assign()` method.
```javascript
Object.assign(dest, ...sources) // Syntax
```
For example, we can add objects `permissions1` and `permissions2` to the object `user`. If the copied property name already exists, it gets overwritten.
```javascript
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// copies all properties from permissions1 and permissions2 into user
Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }
alert(user.name); // John
alert(user.canView); // true
alert(user.canEdit); // true
```
We can also just leave the original blank to do simple object cloning.
```javascript
let clone = Object.assign({}, user);
```

**Nested Cloning**
We can have objects as properties of other objects too. This is called **nested cloning**.
```javascript
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

alert( user.sizes.height ); // 182
```

To clone such objects (and generally, almost all datatypes), we can use the `structuredClone()` method.
```javascript
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = structuredClone(user);

alert( user.sizes === clone.sizes ); // false, different objects

// user and clone are totally unrelated now
user.sizes.width = 60;    // change a property from one place
alert(clone.sizes.width); // 50, not related
```
This doesn't work in certain cases, such as when a function is defined within an object. 

## Garbage Collection

**Reachable Values**
Items that are 'reachable' (values that are accessible or usable) are guaranteed to be stored in memory.
1. There’s a base set of inherently reachable values, that cannot be deleted for obvious reasons. These values are called _roots_.
	- The currently executing function, its local variables and parameters.
	- Other functions on the current chain of nested calls, their local variables and parameters.
	- Global variables.
	- (there are some other, internal ones as well)

2. Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.
   
   For instance, if there’s an object in a global variable, and that object has a property referencing another object, _that_ object is considered reachable. And those that it references are also reachable. Detailed examples to follow.

A background process in JavaScript called a **garbage collector** which removes objects that are unreachable and tracks/monitors all objects.
```javascript
// user has a reference to the object
let user = {
  name: "John"
};
```
![[ojects_js_garbage_collection_example_1.png]]
The global box represents the global variable 'user' and the arrow represents an reference to the Object.

If the reference from user is changed, the object becomes unreachable and therefore is deleted by the garbage collector to free up memory.
```js
user = null;
```
![[jsinfo_garbage_collection_example _2.png]]
If there are two references and one is changed, the object is not deleted as it is still reachable by one of the references. 
**As a rule of thumb, if any object doesn't have incoming references, it will be deleted.**
How The Garbage Collector Works
The following “garbage collection” steps are regularly performed:
- The garbage collector takes roots and “marks” (remembers) them.
- Then it visits and “marks” all references from them.
- Then it visits marked objects and marks _their_ references. All visited objects are remembered, so as not to visit the same object twice in the future.
- …And so on until every reachable (from the roots) references are visited.
- All objects except marked ones are removed.
It starts with the objects directly connected to `<global>` and moves out the chain. All the ones that can't be reached are not marked and all the unmarked objects are removed.
![[jsinfo_garbage_collector_algorithm.png]]

**Garbage Collector Optimisations**
- **Generational collection** – objects are split into two sets: “new ones” and “old ones”. In typical code, many objects have a short life span: they appear, do their job and die fast, so it makes sense to track new objects and clear the memory from them if that’s the case. Those that survive for long enough, become “old” and are examined less often.
- **Incremental collection** – if there are many objects, and we try to walk and mark the whole object set at once, it may take some time and introduce visible delays in the execution. So the engine splits the whole set of existing objects into multiple parts. And then clear these parts one after another. There are many small garbage collections instead of a total one. That requires some extra bookkeeping between them to track changes, but we get many tiny delays instead of a big one.
- **Idle-time collection** – the garbage collector tries to run only while the CPU is idle, to reduce the possible effect on the execution.

# Object Methods; 'This'
When a function is created in an object, it might need data from the object (such as the `name` of the user in this case) in order to perform it's functions. For this case, we can use the `this` word to reference any property within the object. 
```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // "this" is the "current object"
    alert(this.name);
  }

};

user.sayHi(); // John
```
`this` is evaluated at runtime and can be re-used for all objects.
```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// use the same function in two objects
user.f = sayHi;
admin.f = sayHi;

// these calls have different this
// "this" inside the function is the object "before the dot"
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (dot or square brackets access the method – doesn't matter)
```
In arrow functions, `this` references the outer function rather than the arrow function itself.
```javascript
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName); // References the function sayHi which references firstname from the parent object
    arrow();
  }
};

user.sayHi(); // Ilya
```
We can use method shorthands to define things quicker, for example, function expressions.
```javascript
// these objects do the same

user = {
  sayHi: function() {
    alert("Hello");
  }
};

// method shorthand looks better, right?
user = {
  sayHi() { // same as "sayHi: function(){...}"
    alert("Hello");
  }
};
```

# Constructor, operator 'new'
For single-use cases, the `{...}` syntax to create an object is good enough. When we need to create many, it is faster to use the `new` construction operator utilizing **constructor** functions.

Constructor functions have two properties. The main purpose of constructors is to create reusable object creation code.
1. They are named with capital letter first.
2. They should be executed only with `"new"` operator.
```javascript
function User(name) { // The constructor function itself
  this.name = name;
  this.isAdmin = false;
}

let user = new User("Jack"); // Referencing the function to create a new 'user' with the name = 'Jack'.

// This is the same as
let user = {
  name: "Jack",
  isAdmin: false
};
```
This is what the `User` function is essentially doing. It is creating two properties for the object. 
```javascript
function User(name) {
  // this = {};  (implicitly)

  // add properties to this
  this.name = name;
  this.isAdmin = false;

  // return this;  (implicitly)
}
```
We can also call a constructor only once by creating it during the call. It cannot be re-used because it isn't saved anywhere.
```javascript
let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // ...other code for user creation
  // maybe complex logic and statements
  // local variables etc
};
```

We can check if a constructor was called as a constructor or as a regular function using the `new.target` method. We can create separate functionality for when the function is called as a constructor and as a regular function.
```javascript
function User(name) {
  if (!new.target) { // if you run me without new
    return new User(name); // ...I will add new for you
  }

  this.name = name;
}

let john = User("John"); // redirects call to new User
alert(john.name); // John
```
## Returning Values from Constructors
Constructors generally don't use `return` statements because they are focused on constructing properties within `this`.
But if there is a `return` statement...
- If `return` is called with an object, then the object is returned instead of `this`.
- If `return` is called with a primitive, it’s ignored.
```javascript
function BigUser() {

  this.name = "John";

  return { name: "Godzilla" };  // <-- returns this object
}

alert( new BigUser().name );  // Godzilla, got that object
```

[!Creating methods within Constructors]
We can go a step further and create the methods for the object while the Constructor is being called.
```javascript
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "My name is: " + this.name );
  };
}

let john = new User("John");

john.sayHi(); // My name is: John

/*
john = {
   name: "John",
 sayHi: function() { ... }
}
*/
```

# Optional chaining '?'
As an example, let’s say we have `user` objects that hold the information about our users.

Most of our users have addresses in `user.address` property, with the street `user.address.street`, but some did not provide them.

In such case, when we attempt to get `user.address.street`, and the user happens to be without an address, we get an error:
```javascript
let user = {}; // a user without "address" property

alert(user.address.street); // Error!
```
Instead of getting an error, it's better we get `undefined`.

The optional chaining `?.` stops the evaluation if the value before `?.` is `undefined` or `null` and returns `undefined`. **Further in this article, for brevity, we’ll be saying that something “exists” if it’s not `null` and not `undefined`.**

In other words, `value?.prop`:
- works as `value.prop`, if `value` exists,
- otherwise (when `value` is `undefined/null`) it returns `undefined`.

This is an safe implementation of the above case.
```javascript
let user = {}; // user has no address

alert( user?.address?.street ); // undefined (no error)
```

<mark style="background: #FFF3A3A6;">Note: We shouldn't use this everywhere, only where undefined would make sense. It is not ideal to silence errors that should otherwise pop up and only makes the code harder to debug.</mark>

We can also use `?.()` - for functions, and `?.[]` - for square brackets.

# JavaScript Symbols
https://javascript.info/symbol

# Object to Primitive Conversion
https://javascript.info/object-toprimitive
