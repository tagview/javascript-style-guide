# Tagview Javascript Style Guide

## Variables

**Always** use `var` to declare variables.

```javascript
// Bad
user = new User;

// Good
var user = new User;
```

Use one `var` declaration when declaring multiple variables, and declare each one on a new line.

```javascript
// Bad
var project = Project.fetch(1);
var tasks = project.tasks;
var lol = 3;

// Good
var project = Project.fetch(1),
    tasks = project.tasks,
    lol = 3;
```

Declare unused variables last.

```javascript
// Bad
var rating, experience,
    weight,
    name = "Sasha",

// Good
var actress = "Sasha",
    rating,
    experience,
    weight;
```

Align the variable names on the left but **don't** align its values.

```javascript
// Bad, aligning values
var project        = Project.fetch(10),
    pendingTasks   = project.getTasks("pending"),
    completedTasks = project.getTasks("completed");

// Bad, names not aligned
var firstName = "Rodrigo",
lastName = "Navarro";

// Good
var project = Project.fetch(10),
    pendingTasks = project.getTasks("pending"),
    completedTasks = project.getTasks("completed");
```

## White Space

Use soft tabs with 2 spaces.

```javascript
// Bad
function hello() {
∙∙∙∙return "Hello";
}

function hello() {
∙return "Hello";
}

// Good
function hello() {
∙∙return "Hello";
}
```

**Don't** put spaces between parentheses.

```javascript
// Bad
if ( name ) {
}

while ( true ) {
}

function triangle( base, height ) {
  return base * height / 2;
}

// Good
if (name) {
}

while (true) {
}

function triangle(base, height) {
  return base * height / 2;
}
```

Put one space before a leading brace.

```javascript
// Bad
if (name){
}

user.save(function(){
  // callback
});

// Good
if (name) {
}

user.save(function() {
  // callback
});
```

Put a space before a `if`, `while` and `for` parentheses.

```javascript
// Bad
if(name) {
}

while(true) {
}

for(var i = 0; i < 10; i++) {
}

// Good
if (name) {
}

while (true) {
}

for (var i = 0; i < 10; i++) {
}
```

Don't put a space before the `function` parentheses.

```javascript
// Bad
var func = function (arg) {
}

// Good
var func = function(arg) {
}
```

Put a space after a comma.

```javascript
// Bad
var user = new User("Bruce","Lee");

// Good
var user = new User("Bruce", "Lee");
```

## Naming

Use camelCase for objects, functions and primitives.

```javascript
// Bad
var User = { name: "Sasha" };
var check-powerlevel = function() {};
var powerfull_user = { name: "Vegeta" };
var power_level = 9000;

// Good
var user = { name: "Sasha" };
function checkPowerLevel();
var powerfullUser = { name: "Vegeta" };
var powerLevel = 9000;
```
Use [PascalCase](http://c2.com/cgi/wiki?PascalCase) for function constructors and classes.

```javascript
// Bad
function user(name) {
  this.name = name;
}

var bad = new user("Noooooo");

// Good
function User(name) {
  this.name = name;
}

var good = new User("Yeah");
```

Prefix jQuery/zeptojs objects with a `$`.

```javascript
// Bad
var header = $(".header");

// Good
var $header = $(".header");
```

## Strings

Use double `""` quotes.

```javascript
// Bad
var name = 'Vegeta';

// Good
var name = "Vegeta";
```

When you need to programatically concatenating a string, use `Array#join`. [JSPerf](http://jsperf.com/string-vs-array-concat/2).

```javascript
var users = [{
  name: "Vegeta",
  powerLevel: 8999
}, {
  name: "Goku",
  powerLevel: 9001
}];

// Bad
var names = "";

for (var i = 0, length = users.length; i < length; i++) {
  names += users[i].name + " " + users[i].powerLevel + " ";
}

console.log(names);

// Good
var names = [];

for (var i = 0, length = users.length; i < length; i++) {
  names.push(users[i].name + " " + users[i].powerLevel + " ");
}

console.log(names.join());
```

## Arrays

Always use array literals.

```javascript
// Bad
var names = new Array;

// Good
var names = []
```

When you need to transform an array-like object into an array, use Array#slice.

```javascript
function test() {
  var args = Array.prototype.slice.apply(arguments);
}
```

## Objects

Always use object literals.

```javascript
// Bad
var obj = new Object;

// Good
var obj = {};
```

Don't use strings as keys.

```javascript
// Bad
var obj = {
  "name": "Sasha",
  "age": 23
};

// Good
var obj = {
  name: "Sasha",
  age: 23
};
```

Put a whitespace after the key.

```javascript
// Bad
var obj = {
  name:"Sasha",
  rating:10
}

// Good
var obj = {
  name: "Sasha",
  rating: 10
}
```

Put each key-value pair on its own line.

```javascript
// Bad
var obj = {
  name: "Sasha", age: 23,
  rating: 10
}

// Good
var obj = {
  name: "Sasha", 
  age: 23,
  rating: 10
}
```

Inline objects are allowed, but put a whitespace between the braces.

```javascript
// Bad
var obj = {name: "Sasha"};

// Good
var obj = { name: "Sasha" };
```

## Functions

Don't use `arguments` as a parameter, as it will override its value inside the function.

```javascript
// Bad
function test(name, arguments) {
  ...
}

// Good
function test(name, args) {
  ...
}
```

## Classes and Constructor Functions

Don't open the parentheses when creating objects from classes that don't accept arguments.

```javascript
// Bad
var user = new User();

// Good
var user = new User;
```

Don't reasign the prototype object when adding methods.

```javascript
function Car(model) {
  this.model = model;
}

// Bad
Car.prototype = {
  move: function() {
    ...
  },
  stop: function() {
    ...
  }
};

// Good
Car.prototype.move = function() {
  ...
};

Car.prototype.stop = function() {
  ...
};
```

When possible, don't define methods inside the constructor.

```javascript
// Bad
function Car() {
  this.move = function() {
    ...
  };

  this.stop = function() {
    ...
  };
}

// Good
function Car() {
}

Car.prototype.move = function() {
  ...
};

Car.prototype.stop = function() {
  ...
};
```

Don't forget to set the correct constructor when implementing inheritance.

```javascript
function Character(name) {
  this.name = name;
}

// Bad
function Enemy() {
  Character.apply(this, arguments);
}

Enemy.prototype = new Character;

// Good
function Enemy() {
  Character.apply(this, arguments);
}

Enemy.prototype = new Character;
Enemy.prototype.constructor = Enemy;
```

## Comments

Use `//` for single line comments, and always put a newline before then.

```javascript
// Bad
var user = new Admin; // the admin

// Good
var active = true;

// The admin
var user = new Admin;
```

Use `/** .. */` for multiline comments.

```javascript
/**
 * @method Moves the character.
 * @param {Float} distance which the character should move.
 * @return {Boolean} true if the character moved.
*/
function walk(distance) {
  ...
}
```

## Leading commas

Please don't.

```javascript
// Bad
var user = new User
  , admin = new Admin;

// Good
var user = new User,
    admin = new Admin;
```

## Semicolons

Always...

```javascript
var user = new User;

var object {
  name: "Sasha",
  age: 23
};

if (true) console.log("Yeah!");
```

...except after a multiline function declaration, if, while or for blocks.

```javascript
// Bad
var func = function() {
  ...
};

if (true) {
  ...
};

while (true) {
};

// Good

var func = function() {
  ...
}

if (true) {
  ...
}

while (true) {
  ...
}
```
