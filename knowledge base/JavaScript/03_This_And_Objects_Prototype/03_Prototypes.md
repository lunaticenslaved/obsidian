# \[\[Prototype]]

Any object has a property \[\[Prototype]] that references to another object. 

**`for ... in` loop looks up in prototype chains.**

At the top of every prototype chain is `Object.prototype` object.

When assigning to an object with = the property will added on the object. But in the prototype chain the property exists and marked as `writtable: false` of as setter. Then the property will not be assigned. To shadow the property use `Object.defineProperty`.

The prototype object can be get with `.prototype`.

When a `function` is created a `prototype` property is assigned with the prototype. When any object is created with `new Function` the prototype for the object equals to the common `Function.protytype` object. Remarcable that not copies of the prototype object are created. Instead every instance is linked to the same object. This mechanism is called **prototype inheritance**.

