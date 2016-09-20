# Angular Typescript style guide for YOPA
Opinionated development style guide for Typescript Angular 1.5 by YOPA's Dev Team

## Table of contents
1. App folder structure
1. Module folder structure
1. File naming convention


## App folder structure

App structure depicted, with most important files and folders for reference.

```
- app/
    + components/
    + config/
    + run/
    + sass/
- assets/
- docs/
- public/
- reports/
- typings/
- .gitignore
- gulpfile.js
- index.php
- karma.conf.js
- main.d.ts
- meta.php
- package.json
- yconfig.json
```

**[⬆ back to top](#table-of-contents)**

## Module folder structure
The interfaces folder contains only a instances.d.ts file for instances that represent object structures. 
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

## File naming convention

Javascript and Typescript files [js, ts]

Configuration files:
- Config: `<moduleName>.config.<ext>`
- Run: `<moduleName>.run.<ext>`
- Routes: `<moduleName>.routes.<ext>`
- Spec: `<originalFileName>.spec.<ext>`

Module files:
- Constants: `<camelCaseName>.constant.<ext>`
- Controllers: `<camelCaseName>.controller.<ext>`
- Components: `<camelCaseName>.component.<ext>`
- Directives: `<camelCaseName>.directive.<ext>`
- Enum: `<camelCaseName>.enum.<ext>`
- Factories: `<camelCaseName>.factory.<ext>`
- Filters: `<camelCaseName>.filter.<ext>`
- Interfaces: `instances.d.ts`
- Services: `<camelCaseName>.service.<ext>`

HTML Files [.html]
- Components: `<yp-component-name>.component.html`
- Directives: `<yp-directive-name>.directive.html`
- Layout: `<file-name>.html`
- Modals: `<file-name>.modal.html`
- Templates: `<file-name>.template.html`
- Views: `<module>.<file-name>.html`
- Views (after refactoring): `<file-name>.html`
