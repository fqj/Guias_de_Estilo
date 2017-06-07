# Angular 2 conventions

Working with Angular 2, you should export all needed modules in order to import them from the Angular main App. Working with the starter kit, the webpack configuration should be able to Tree Shake your files and takes only the necessary for the build.

 * Name your component file with . as type separator by functionality. header.component.ts. 
 * Define one component per file.
 * Do use upper camel case for class names.
 * Do use a custom prefix for a component selector. If the project is "Santander", you can use stn-header as component selector.
 * Do use upper camel case when naming classes.
 * Do declare variables with const if their values should not change during the application lifetime.
 * Do use lower camel case to name properties and methods.
 * Do name the file such that you instantly know what it contains and represents.
 * Do use dashed-case or kebab-case for naming the element selectors of components.
 * Do define components as elements via the selector.selector: 'stn-hero-button' should have class HeroButtonComponent  
 * Define as @Input every property to has be defined by the parent.
 * Do limit logic in a component to only that required for the view. All other logic should be delegated to services.
 * Do name events without the prefix on.
 * Do put presentation logic in the component class, and not in the template.
 * Do use attribute directives when you have presentation logic without a template.
 * Do implement the lifecycle hook interfaces.
 
You can read the full [Angular guidelines](https://angular.io/styleguide) for more reference.

Those rules should be validated with codelyzer and every component that no follows the rules should be rejected.

# Type Script conventions

 * Use PascalCase for type names.
 * Do not use "I" as a prefix for interface names.
 * Use PascalCase for enum values.
 * Use camelCase for function names.
 * Use camelCase for property names and local variables.
 * Do not use "_" as a prefix for private properties.
 * Use whole words in names when possible.
 * 1 file per logical component (e.g. parser, scanner, emitter, checker).
Do not add new files. :)
 * files with ".generated.*" suffix are auto-generated, do not hand-edit them.
 * Do not export types/functions unless you need to share it across multiple components.
 * Do not introduce new types/values to the global namespace.
 * Shared types should be defined in 'types.ts'.
 * Within a file, type definitions should come first.
 * Use undefined, do not use null.
 * Consider objects like Nodes, Symbols, etc. as immutable outside the component that created them. Do not change them.
 * Consider arrays as immutable by default after creation.
 * For consistency, do not use classes in the core compiler pipeline. Use function closures instead.
 * More than 2 related Boolean properties on a type should be turned into a flag.
 * Use JSDoc style comments for functions, interfaces, enums, and classes.
 * Use double quotes for strings.
 * All strings visible to the user need to be localized (make an entry in diagnosticMessages.json).
 * Use arrow functions over anonymous function expressions.
 * Only surround arrow function parameters when necessary. 
 * Always surround loop and conditional bodies with curly braces.
 * Open curly braces always go on the same line as whatever necessitates them.
 * Parenthesized constructs should have no surrounding whitespace. 
A single space follows commas, colons, and semicolons in those constructs.
 * Use a single declaration per variable statement 
 * `else` goes on a separate line from the closing curly brace.

 You can read the full [TypeScript guidelines](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines) for more reference.