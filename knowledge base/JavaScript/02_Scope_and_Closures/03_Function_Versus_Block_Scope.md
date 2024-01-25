### Scope from functions

Inside of function a new scope bubble is created. This scope contains definitions for all local variables no matter where they were declared.


### Hiding in Plain Scope

When a variable or a function is used only in specific place it useful to keep them as close as possible to the place according to the [Principle of Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege)(// TODO write more about the principle).


### Collisions Avoidance

Another benefit of hiding variable inside of a scope is to avoid of unintended collisions between two different identifiers with the same name but different usage.

#### Global namespace

Many collisions can occur in the global scope because many libraries use global scope to keep their settings and constants.

#### Module management

Use module approach to keep every variable in its place and avoid collisions.


### Functions as Scopes




