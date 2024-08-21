# Effective TypeScript - 2nd Edition
## Item 2 - Know which TypeScript options you're using

The behavior of TypeScript is determined by a wide range of options specified in a `tsconfig.json` file. This file allows all developers on a project to share the same TypeScript configuration, ensuring consistency in how TypeScript is used. The options chosen can make TypeScript behave very differently from one project to another.

The noImplicitAny option controls how TypeScript reacts when it cannot determine the type of a variable.

```typescript
function add(a, b) {
    return a + b;
}

function add(a: any, b: any): any
```
In this code, TypeScript cannot infer the types of the parameters a and b, nor the return type of the function. By default, it assigns the any type to these elements. The any type disables the type checker for any code that uses it, which can lead to unexpected errors. This is called an implicit any because this type is not explicitly specified by the developer.

If the noImplicitAny option is turned off, TypeScript will not generate an error. However, if this option is enabled, TypeScript will return an error like this:

```bash
Parameter 'a' implicitly has an 'any' type
```
To fix this error, you need to explicitly declare the types of the parameters or the return type of the function, either by using any or by specifying a more precise type:

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```
TypeScript becomes particularly useful when you provide precise information about types. Enabling noImplicitAny encourages better type definitions, which improves code comprehension. Without this option, TypeScript is very permissive, which can reduce the benefits it provides in terms of code consistency checking.

The strictNullChecks option controls whether null and undefined values are allowed in types. If this option is turned off, null and undefined can be assigned to variables even if they are typed as numbers, strings, etc.

```typescript
const x: number = null; // OK, null is a valid number
```
However, if strictNullChecks is enabled, TypeScript will return an error:

```typescript
const x: number = null; // 'null' is not assignable to type 'number'
```
To allow null as a possible value, you need to adjust the variable's type:

```typescript
const x: number | null = null;
```
If you want to disallow null and this option is enabled, you must explicitly check that the variable is not null before using it.

```typescript
const statusEl = document.getElementById('status');

// Option 1: Check with an `if`
if (statusEl) {
    statusEl.textContent = 'Ready'; // OK, null has been excluded
}

// Option 2: Use the `!` operator
statusEl!.textContent = 'Ready'; // OK, we've asserted that statusEl is non-null
```

Checking the variable's value with an if is a technique called narrowing or type refining. The use of the ! operator is a non-null assertion. Type assertions are useful in TypeScript, but they can sometimes lead to runtime errors if not used carefully.

Enabling these options increases the rigor required to write code in TypeScript, making the language stricter and demanding greater discipline from developers. However, this leads to safer and more maintainable code. If a developer shares TypeScript code and you cannot reproduce a reported error, check the TypeScript configuration of the project. Differences in configured options might lead to different TypeScript behavior.

> [!NOTE]  
> Type inference means that the TypeScript compiler automatically deduces the type of a variable or expression from the context in which it is used, without the developer needing to explicitly specify the type. This allows for more concise code while still benefiting from type safety.

> [!NOTE]  
> Type assertions are mechanisms that allow the developer to explicitly tell the compiler: "I know better than you, and I’m telling you that this expression has this particular type." In TypeScript, they are used to inform the compiler that a value is of a certain type, even if TypeScript is not able to determine it on its own. If the assertion is incorrect (for example, if you assert that a value is of a certain type when it really isn’t), this can lead to runtime errors. This is essentially telling the compiler not to worry about what you’re doing. Type assertions should be used with caution.