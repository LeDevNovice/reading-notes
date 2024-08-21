# Effective TypeScript - 2nd Edition
## Item 1 - Understand the relationship between TypeScript and JavaScript

When we talk about TypeScript code, it's important to remember that what actually gets executed is JavaScript after it has been compiled.

TypeScript is a superset of JavaScript, which means that all valid JavaScript code is also valid in TypeScript. It is entirely possible to rename a .js file to .ts since all JavaScript programs are TypeScript programs. However, the reverse is not true: a TypeScript program can include additional syntax that is not understood by JavaScript.

One of TypeScript's main goals is to catch potential errors before the program is even executed. With its type system, TypeScript can flag inconsistencies or errors, such as typos, that could prevent the code from functioning correctly. TypeScript replicates the runtime behavior of a JavaScript program while adding extra checks. Although JavaScript's quirks are accepted, TypeScript imposes some constraints and generates warnings, for example, when a function is called with the wrong number of arguments.

By adding type annotations to the code, the developer explicitly states their intentions to TypeScript. This allows the type checker to ensure that the code aligns with these intentions and to raise warnings if it does not.

> [!NOTE]  
> The author mentions TypeScript's type system and type checker without going into detail. But what exactly are these elements that seems to be inherent to TypeScript? <br><br>The type system is a set of rules that define how types are used. It ensures that the program manipulates data in a consistent way. For example, if a variable is declared as a number, the type system ensures that this variable is used appropriately as a number. The type checker, on the other hand, is a tool or feature that analyzes the code to ensure that the rules of the type system are followed. The type checker scans the source code and verifies that the types of variables, functions, and expressions are used correctly according to the rules defined by the type system. For example, it can flag an error if you try to pass a string to a function that expects a number. In TypeScript, these two elements work together