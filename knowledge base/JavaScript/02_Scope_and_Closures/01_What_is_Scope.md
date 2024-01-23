### Compiler Theory

In JS proccessing/compiling occurs in a separate phase before execution begins. It is not compiled in advance nor compiler result is portable among various distributed systems.

In JS functions are first-class values: they can be assigned and passed around just like numbers and strings. But function also have their own scope no matter where in the program the function is eventually running. This scope is called **closure**.


### Compilied vs. Interpreted

**Compilation** is a set of steps that process the text of your code and turns it into instructions the computer can understand. All text in processed at once and all instructions are saved as output.

**Interpretation** is pretty much like compilation but the code is read and turned into instructions and executed line by line.

![[Pasted image 20240121215824.png]]

Modern JS engines actually employ numerous variations of both compilation and interpretation in the handling of JS programs. In general JS us mostly **compiled language** as the compilation is passed in a separate phase before execution begins.


### Compiling Code

Scope is created into compilation phase so understanding compilation leads to mastering scope.

In classic compiler theory, a program is processed by a compiler in three basic stages:

1. **Tokenizing/Lexing**: break the code into meaningful (to the language) chunks. For instance, consider the program: `var a = 2;`. This program would likely be broken up into the following tokens: var, a, \=, 2, and ;. Whitespace may or may not be persisted as a token, depending on whether it's meaningful or not.
2. **Parsing**: taking a stream of tokens and turning it into a tree of nested elements, which collectively represents an **Abstract Syntax Tree** (**AST**).
3. **Code Generation**: taking an AST and turning it into an executable code. The JS engine takes the just described AST for `var a = 2;` and turns it into a set of machine instructions to actually _create_ a variable called `a` (including reserving memory, etc.), and then store a value into `a`.


### Understanding Scope

Let's meet hte cast of chacters that interact to process a program.

- **Engine** is responsible for start-to-finish compilation and execution of the copiled code.
- **Compiler** handles of the dirty work os parsing and AST generation.
- **Scope** collect and maintains a look-up list of all the declared variables.

#### Back and Forth

Let's see what happens when `var a = 2` in being executed:

1. Compiler starts it's works and sees the variable `a`. It asks Scope to check if there is a variable named `a` in the particular scope collection. If true then Compiler moves on. Otherwise it asks Scope to declare a new variable called `a` in the collect scope collection.
2. Compiler produces a code for Engine to later Execute. Compiler asks Scope if there is a variable named `a`. If so, Engine uses this variable. If not, Scope looks somewhere else.

If Engine finds the variable it assings the value. If not, it throws an error.



### Required: Two Phases

Processing of JS programs occurs in two phases: parsing/compilation, then execution.

This can be shown with the example below. The program does not print `Hello` because the execution not started because of `SyntaxError`:

```
var greeting = "Hello";

console.log(greeting);

greeting = ."Hi";
// SyntaxError: unexpected token .
```

Some errors in **strict mode** behaive in similar way.
**Hoisting** also works in compiling phase.


### Compiler Speak

All occurrences of variables/identifiers in a program serve into one on two "roles": either they're the _target_ of an assignment or they're the _source_ of a value.

#### Targets

There are several ways to mark variable as a target:
- `students = [..]`
- `for (let student of students) {`
- `getStudentName(73)` - argument assignment
- `function getStudentName(studentID) {`


#### Sources

In `for (let student of students)`, we said that `student` is a _target_, but `students` is a _source_ reference. In the statement `if (student.id == studentID)`, both `student` and `studentID` are _source_ references. `student` is also a _source_ reference in `return student.name`.

In `getStudentName(73)`, `getStudentName` is a _source_ reference (which we hope resolves to a function reference value). In `console.log(nextStudent)`, `console` is a _source_ reference, as is `nextStudent`.


### Cheating: Runtime Scope Modifications
