# Angular Typescript style guide for YOPA
Opinionated development style guide for Typescript Angular 1.5 by YOPA's Dev Team

Based on:
- [Airbnb's Javascript Style Guide](https://github.com/airbnb/javascript)
- [John Papa's Angular 1 Style Guide](https://github.com/johnpapa/angular-styleguide/tree/master/a1)
- [Todd Motto's Angular 1.x for E2015](https://github.com/toddmotto/angular-styleguide)

## Table of contents
1. [App folder structure](#app-folder-structure)
1. [Module folder structure](#module-folder-structure)
1. [File naming](#file-naming)
1. [Component naming](#component-naming)
1. [Variable declarations](#variable-declarations)
1. [Naming](#naming)
1. [Method definitions](#method-definitions)
1. [Types](#types)
1. [Comments and documentation](#comments-and-documentation)
1. [Blocks](#blocks)


## App folder structure

App structure depicted, with most important files and folders for reference.

```
- app/
    + components/
    + config/
    + run/
    + sass/
    + app.ts
- docs/
- public/
- typings/
- .gitignore
- gulpfile.js
- index.php
- karma.conf.js
- main.d.ts
- package.json
```

**[⬆ back to top](#table-of-contents)**

## Module folder structure

The modules follow the fractal hierarchy approach ([More info](https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/edit))
The `interfaces` folder contains only a `instances.d.ts` file for instances that represent object structures. 
Interfaces for angular components (services, components, directives, etc) should be on the top of the original component file.

The spec folder contains files mirroring the component files being tested, do not use a single file for all the tests in the module.

```
- /
    + components/
    + constants/
    + controllers/
    + directives/
    + factories/
    + filters/
    + interfaces/
    + services/
    + spec/
    + views/
    + components/
    + directives/
    + templates/
```

**[⬆ back to top](#table-of-contents)**

## File naming

### Javascript and Typescript files [js, ts]

#### Configuration files:
- Config: `<moduleName>.config.<ext>`
- Run: `<moduleName>.run.<ext>`
- Routes: `<moduleName>.routes.<ext>`
- Spec: `<originalFileName>.spec.<ext>`

#### Module files:
- Constants: `<camelCaseName>.constant.<ext>`
- Controllers: `<camelCaseName>.controller.<ext>`
- Components: `<camelCaseName>.component.<ext>`
- Directives: `<camelCaseName>.directive.<ext>`
- Enum: `<camelCaseName>.enum.<ext>`
- Factories: `<camelCaseName>.factory.<ext>`
- Filters: `<camelCaseName>.filter.<ext>`
- Interfaces: `instances.d.ts`
- Services: `<camelCaseName>.service.<ext>`

### HTML Files [.html]
- Components: `<ypComponentName>.component.html`
- Directives: `<ypDirectiveName>.directive.html`
- Layout: `<fileName>.html`
- Modals: `<fileName>.modal.html`
- Templates: `<fileName>.template.html`
- Views: `<module>.<fileName>.html`
- Views (after refactoring): `<fileName>.html`

### SASS Files [.scss]
- `<file_name>.scss`

**[⬆ back to top](#table-of-contents)**

## Component naming
- Constants: `<camelCaseName>Constant`
- Controllers: `<camelCaseName>Controller`
- Modal Controllers: `<camelCaseName>ModalController`
- Components: `<camelCaseName>Component`
- Directives: `<camelCaseName>Directive`
- Enums: `<camelCaseName>Enum`
- Factories: `<camelCaseName>Factory`
- Filters: `<camelCaseName>Filter`
- Service: `<camelCaseName>Service`

Angular modules' configuration and run methods:
- Config: `<camelCaseName>Config`
- Run: `<camelcaseName>Run` 

**[⬆ back to top](#table-of-contents)**

## Variable declarations

- Prefer `let` or `const` over `var`, since they have block-scoping, which means they are not visible outside of their containing block 
- Use `const` when the value of the variable is not meant to change, like a 
resource id or an attribute name, this way the variable can't get reassigned by mistake.
- Specify the variable type when you declare it, and avoid the usage of `any`. 
That way you'll force yourself to specify the proper variable type. Remember `any` 
is not a type but a compiler flag to opt-out of type-checking
- Prefer object declaration shorthand sintax over its alternatives

```js
//avoid
let person = new Object();

//do
let person = {};
person.name = name;
person.address = address;

// or

let person = {
    "name": name,
    "address": address
};
```

- Don't declare variables in a single line. Always prefer separate lines for clarity

```js
// avoid
let id: number, name: string, address: string;

// do
let id: number;
let name: string;
let address: string;
```

For more information:
- [Variable Declarations - Typescript](https://www.typescriptlang.org/docs/handbook/variable-declarations.html)


**[⬆ back to top](#table-of-contents)**

## Naming

### Variables, members, properties and attributes
*(TODO: Work on this title name)*

- Do not use single letter names
- Use lowerCamelCase
- Do not use leading or trailing underscores

**[⬆ back to top](#table-of-contents)**

## Method definitions




**[⬆ back to top](#table-of-contents)**

## Types

### Classes

- Use PascalCase/UpperCamelCase for the class name
- Place members on top of `$inject` and the constructor
- Place `public` members on top of all other members
- Place `public` methods right under the `constructor` method
- Place `private` methods on the bottom of the class

### Function, methods 

- Avoid functions of more than 75 lines of code. Long functions are usually a code smell 
- Name methods with verbs that explain what they're doing, like **unbind**, 
**create**, **update**, **retrieve**
- Callbacks for events should follow the `on<PascalCaseSomethingHappened` format
- Use default sintax rather than mutating parameters

```js
// avoid
function handleThings(opts) {
  if (!opts) {
    opts = {};
  }
  // ...
}

// do
function handleThings(opts = {}) {
  // ...
}
```

- Avoid using the `arguments` property of functions, since it's not available
for arrow functions and can be unpredictable depending on the function call

#### Return values

Always specify a function return value, it helps the compiler, specially when 
returning promises and then resolving/rejecting them inside your function. 

If it's void you can return Typescript's `void` type.

- Service methods should return promises except in cases where the return 
value is inmediately available, like accessing local storage of 
internal flags from the Service

### Boolean

- Use present tense verb conjugations as 
prefixes for the variable name, like: *is*, *has*, *can*

```js
// avoid
let loading: boolean = false;
let required: boolean = true;
let sstc: boolean = false;
let submit: boolean = false;

// do
let isLoading: boolean = false;
let isRequired: boolean = true;
let hasSstc: boolean = false;
let canSubmit: boolean = false;
```

### Number

- Prefer using the Number constructor instead of it's alternatives

```js
// avoid
let id: number = parseInt('256', 10);
// do
let id: number = Number('256');
```

### Arrays

- Use the literal syntax for array creation

```js
// avoid
const collection = new Array();

// do
const collection = [];
```

- Use the literal syntax for type. Except for `$inject`

```js
// avoid
let collection: Array<number>;
// do
let collection: number[];

// allowed
class NewComponentController {
    static $inject: Array<string> = [...];
    // or
    static $inject: string[] = [...];
}
```

- Use `Array#push` instead of direct assignment on index position

```js
const someStack = [];

// avoid
someStack[someStack.length] = {'name': "new item"};

// do
someStack.push({'name': "new item"});
```

- You can use Array spreads to copy arrays 

```js
// allowed
const collection = angular.copy(originalCollection);

// allowed
const collection = [...originalCollection];
```

### String 

- When programmatically building up strings, use template strings instead of concatenation.

```js
// avoid
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// avoid
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// do
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

**[⬆ back to top](#table-of-contents)**

## Comparison operators and equality

- Use `===` and `!==` over `==` and `!=`
- Conditional statements like `if()`, `ng-if`, `ng-show`, `ng-hide` and `ng-required` evaluate their expression using coercion, which follows these rules:
	+ **Objects** evaluate to `true`
	+ `undefined` evaluates to `false`
	+ `null` evaluates to `false`
	+ **Booleans** evaluate to `<the value of the boolean>`
	+ **Numbers** evaluate to `false` if `+0`, `-0`, or `NaN`, otherwise `true`
	+ **Strings** evaluate to `false` if an empty string `''`, otherwise `true`
- 

```js
// avoid
if(isLoading === false){
	console.log("Finished loading");
}

// do
if(!isLoading){
	console.log("Finished loading");
}
```



**[⬆ back to top](#table-of-contents)**


## Comments and documentation

- Write documentation for exposed methods of Services on top of 
the interface method definition.
- For `private` methods they can be on top of the method.
- Avoid single line comments. They're usually a code smell.
- Use single line comments only for TODO and FIXME.

**[⬆ back to top](#table-of-contents)**

## Blocks
Use braces with all multiline blocks

```js
// avoid
if (test)
  return false;

// avoid
if (test) return false;

// do
if (test) {
  return false;
}

// avoid
for(let index = 0; index < collection.length; index++ )
    console.log("This is my index", index);

// do
for(let index = 0; index < collection.length; index++ ){
    console.log("This is my index", index);
}
```
**[⬆ back to top](#table-of-contents)**