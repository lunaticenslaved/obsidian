In JS proccessing/compiling occurs in a separate phase before execution begins.

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