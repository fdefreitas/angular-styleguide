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
1. [Components](#components)
1. [Directives](#directives)
1. [Factories](#factories)
1. [Services](#services)
1. [ui-router States](#ui-router-states)
1. [Design principles](#design-principles)
1. [Comments and documentation](#comments-and-documentation)
1. [Blocks](#blocks)
1. [Angular Components](#angular-components)
1. [Specs](#specs)


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

The modules follow the fractal hierarchy approach, proposed by Google for projects using Angular and Polymer, (For more info check [Angular Best Practice for App Structure](https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/edit))
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

#### Spec files:
Spec files should be named just like the module component that it contains the tests for, appending `.spec` to the file 
name before its extension. This to avoid confussion and possible duplicated files on a git merge when using different file names 
- `<originalFileName>.spec.<ext>`

For a detailed explanation fo the spec files structure go to [Specs](#specs)

### HTML Files [.html]
Templates should be used only for custom html for third party plugins of reusable "components" outside of angular's symbol 
scope, like modals.
- Components: `<ypComponentName>.component.html`
- Directives: `<ypDirectiveName>.directive.html`
- Layout: `<fileName>.html`
- Modals: `<fileName>.modal.html`
- Templates: `<fileName>.template.html`
- Views: `<module>.<fileName>.html`

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

- Define small methods that have a single responsibility, like mapping an address to an object.
- Follow the dependency injection principle, so it receives everything it needs, like an `id`, a `product` or `user` object, to work via its parameters, apart from Services.

Why? 
- That makes them reusable
- They are easier to read
- They are easier to test
- They can be used inside of bigger methods
- Avoids the need to kno

**[⬆ back to top](#table-of-contents)**

## Types

### Classes

- Use PascalCase/UpperCamelCase for the class name
- Place members on top of `$inject` and the constructor
- Place `public` members on top of all other members

### Function, methods 
- Place `public` methods right under the `constructor` method
- Place `private` methods on the bottom of the class
- Don't do initialization logic directly in the constructor, wrap it in a private method 
and invoke it from there. Why? Because that way it's easier to understand  what's being done 
in the constructor and also helps making the file easier to navigate.
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

For more info on the way Javascript handles coercion: [Truth, Equality and Javascript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108)

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
- Avoid single line comments, except for TODO and FIXME tags. They're usually a code smell.

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

## Angular Components

  The following refers to Angular's set of components and not just the new component component (Yeah, a bit confusing right?)

### Controllers

- Controller classes (or functions) should be named `<controllerName>Controller`, avoid using `Ctrl` or other abbreviations 
for the naming.

```js
// avoid
class controllerNameCtrl {
  //...
}
angular.module('<moduleName>').controller('controllerNameCtrl', controllerNameCtrl);

// do
class controllerNameController {
  //...
}
angular.module('<moduleName>').controller('controllerNameController', controllerNameController);

```

### Components

- Component classes (or functions) should be named `yp<ComponentName>Component` and inyected into angular 
as `yp<ComponentName>` with no `Component` suffix., avoid using `Cmp` or other abbreviations 
for the naming. The `yp` prefix helps identify our own components from third parties'.

```js
// avoid
class componentNameCmp {
  //...
}
angular.module('<moduleName>').component('componentName', componentNameCmp);

// do
class ypComponentNameComponent {
  //...
}
angular.module('<moduleName>').component('ypComponentName', ypComponentNameComponent);

```

### Directives

- Directive classes (or functions) should be named `yp<DirectiveName>Directive`, avoid using `Dir`, `Drtv` or other abbreviations 
for the naming. The `yp` prefix helps identify our own directives from third parties'.

```js
// avoid
class directiveNameDir {
  //...
}
angular.module('<moduleName>').directive('directiveName', () => new directiveNameDir());

// do
class ypDirectiveNameDirective {
  //...
}
angular.module('<moduleName>').directive('ypDirectiveName', () => new ypDirectiveNameDirective());

```

### Filters

- Filter classes (or functions) should be named `yp<FilterName>Filter` and inyected into angular 
as `yp<FilterName>` with no `Filter` suffix. The `yp` prefix helps identify our own filters from third parties'.

```js
// avoid
class filterName {
  //...
}
angular.module('<moduleName>').filter('filterName', filterName);

// do
class ypFilterNameFilter {
  //...
}
angular.module('<moduleName>').filter('ypFilterName', ypFilterNameFilter);

```

### Services, Factories, Constants

- Services and factories classes (or functions) don't need to have the `Service` suffix, use a name that explicitely 
states the service/factory function instead.

```js
// avoid
class ViewingService {
  //...
}

// do
class Viewing {
  //...
}

// do
class ViewingHelperService {
  //...
}

// do
class ViewingManagerService {
  //...
}

```

### Providers

- Provider classes (or functions) should be named `<providerName>Provider`.

**[⬆ back to top](#table-of-contents)**

## Specs

The general structure of a spec file will look like this:

```js
(function() {
    'use strict';
    /* Describe the component being covered by this spec file.
    *  Under this approach of one spec file per component there will be just one main describe block 
    *  for the component being tested
    */
    describe('<componentName>', () => {

        // Define variables for the dependencies need to be injected to run the tests, and also for 
        // general use variables
        var httpBackend,
            scope,
            q,
            Auth;

        // This beforeEach will be needed for any describe block. It mocks the app
        beforeEach(angular.mock.module('yopa'));

        // This beforeEach will handle the dependency injection, as well as any mock data you need to create
        beforeEach(inject((_Auth_, $httpBackend, $q, $rootScope) => {

            httpBackend = $httpBackend;
            q = $q;
            scope = $rootScope.$new();
            Auth = _Auth_;

            var propertyId = 9999;

            var mockResponse = {
              //...
            };

        }));

        // Inside the main describe block for the file there will be as many describe blocks as methods 
        // (or attributes when it applies) are being tested
        describe("methodName()", () => {
          // There will be as many `it` blocks as input/output combination are being tested for the method
          // Each `it` block should be limited to testing one outcome
          it('should validate discount code', () => {
            // ...
            // There will be `expect` expresions. this has a set of `matcher functions` like `toBe`, 'toBeTruthy`
            // with negation options as well like `not.toBe`
            expect('<something>').toBe('<expected value>');
          });
        });

        // Generally in the afterEach contains only a call to the scope's apply method
        afterEach(() => {
            scope.$apply();
        })

    });
})();
```

**[⬆ back to top](#table-of-contents)**