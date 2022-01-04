# Chapter 5

### Terms

- **\*\*** -

## Prototypes

> ### **Prototype**
>
> Objects in JS have an internal property, denoted in the specification as **_Prototype_**, which is simpley a ref to another obj. Almost all objs are given a non-null value for this property, at the time of creation
>
> - The default [Get] operation proceeds to follow the **_Prototype_** link of the obj if it cannot find the request property ob the objext directly:
>
> ```Javascript
> var anotherObj = { a: 2};
>
> // create an obj linked to anotherObj
> var myObj = Object.create( anotherObj );
> myObj.a; // 2
> ```
>
> - It tries find prop `a` that clearly doesn't exist on `myObj`. But, if a werent found on `anotherObj` then it woruld try to found it until either a mathcing prop name is found, or the **_Property_**chain ends. If matching prop ever found result will return `undifined`

> - **Object.Prototype**  
>   The _top_ of every _normal_ [Prototype] chain is he built-in `Object.prototype`. This obj includes variety of common utilities used all over JS, because all normal(built-in not host-specific extension) obj in JS "descend from" the Object.prototype obj

> - **Setting and Shadowing Properties**  
>   If Obj already has a normal data acessor property directly present on it , the assignment is simple as changing the val of existing property
> - If the peroperty name ends up both on Object and itself and at a higher level of the [Prototype] chain that starts at obj is called **_Shadowing_**
> - If a normal data accessor prop is found anywhere higher on the [Prototype] chain,
> - 1. and its not marked read-only, then a new prop added directly to obj, resulting _shadowed property_
>   2. but its marked as read-only, then both the setting of that existing property as well as the creation of the shadowed property are disallowed
>   3. and its a setter, then the setter will be called

> **What's in a name**  
> In JS we dont make _copies_ from one obj (class) to another (instance). We make `links` betwejen objs. For the [prototype] mexhanism , visually , the arrows move from right to left , and from bottom to top: This mechanism is ofthen clled **_prototypal inheritance_** is dynamic language version of class inheritance
>
> - _Inheritance_ implies a _copy_ operation, and JS doesn't cioy obj peroperties. INstead , JS creates a link between two objs, where obe obj can essentioally `delegate` property/function access to another obj.
>   `differential inheritance` - the idea here is that we describe an objs behavior on terms of what is deifferent from a more general descriptior

> **Constructor**
>
> ```Javascript
> function Foo(){
>   //...
> }
> Foo.prototype.constructor === Foo; // true
>
> var a = new Foo();
> a.constructor === Foo; //true
> ```
>
> The Foo.prototype obj by default gets a public, nonumerable perop called `.constructor` , and this property is a ref back to the functiob the the obj is associated with

> **Constructor or Call**  
> Function themselves are not constructors.  
> However, when you put the _new_ keyword in front of a normal func call, that makes that function call a **constructor call**
>
> ```Javascript
> function NothingSpecial() { console.log( 'kavo' );}
> var a = new NothinSpecial(); // 'Dont mind me'
>
> a //{}
> ```
>
> NothingSpecial is just a normal fen called func, but when called with _new_, it _constructs_ an obj, almost as a side effect, which we happen to assign to a. The call was s _constructor call_, but _NothingSpecial_ is not, in and of itself, a constructor
>
> functions aren't constructors, but function calls are "constructor calls" if and only if _new_ used

> **Mechanics**
>
> ```Javascript
> function Foo ( name ) { this.name = name };
>
> Foo.prototype.myName = function() { return this.name };
>
> var a = new Foo("A");
> var b = new Foo("B");
>
> a.myName(); // A
> b.myName(); // B
> ```

> **"Constructor" redux**  
> The constructor ref is also delegated up to `Foo.prototype`, which happens to, by default, have a constructor that points at `Foo`
>
> - For one, the `constructor` property on `Foo.protototype` is only hter by default on the obj created when `Foo` the function is declared. If you create a new obj, and replace a function's default `.prototype` obj red, the new obj will not by default magically get a `constructor` on it
>
> ```Javascript
> function Foo(){ ... };
> Foo.prototype = { ...}; //create a new prototype obj
> var a1 = new Foo();
> a1.constructor === Foo //false
> a1.constructor === Object //true
> ```
>
> a1 has no`constructor` property, soit delegates up the `[[Prototype]]` chain to `Foo.prototype`. But that obj doesn't have a `constructor` either . so it keeps delegating chain, this time up to `Object.prototype`. the top of the delegation chain. That obj indeed has a `constructor` on it, which points to the built-in Obj function

> **(Prototypal) Inheritance**
> The property `[[Prototype]]` is internal and hidden, but there are many ways to set it. One of them is to use the special name `__proto__`, like this:
> [Prototypal inheritance](https://javascript.info/prototype-inheritance)
>
> ```Javascript
> let animal = {
>  eats: true
> };
> let rabbit = {
>  jumps: true
> };
> rabbit.`__proto__` = animal; // sets rabbit.`[[Prototype]]` = animal
> alert( rabbit.eats ); // true (**)
> alert( rabbit.jumps ); // true
> ```
>
> > `__proto__` is a historical **_getter/setter_** for `[[Prototype]]`
> > It’s a common mistake of novice developers not to know the difference between these two.
> >
> > Please note that `__proto__` is not the same as the internal `[[Prototype]]` property. It’s a getter/setter for `[[Prototype]]`.
> > The `__proto__` property is a bit outdated. It exists for historical reasons, modern JavaScript suggests that we should use Object.getPrototypeOf/Object.setPrototypeOf functions instead that get/set the prototype
> >
> > By the specification, `__proto__` must only be supported by browsers. In fact though, all environments including server-side support `__proto__`, so we’re quite safe using it.
> >
> > As the `__proto__` notation is a bit more intuitively obvious, we use it in the examples.
>
> ```Javascript
> function Foo(name){
>    this.name = name
> };
>
> Foo.prototype.myName = function() {
>     return this.name
> };
>
> function Bar( name, label){
>   Foo.call( this, name );
>   this.label = label;
> }
>
> // here, we make a new 'Bar.prototype'
> // and might need to be manually 'ficed' if you're
> // in the habit of relying an such poperties!
>
> Bar.prototype.myLabel = function() { return this.label }
>
> var a = new Bar('a', 'obj a');
>
> a.myName() // a
> a.myLabel() // obj a
> ```
>
> In other words it says "_make a new Bar a dot prototype obj thats linked to Foo.prototype_"
>
> ```Javascript
> //doesnt work like u want
> Bar.prototype = Foo.prototype; //ref to Foo.prototype, Bar.prototype links same obj same which link Foo.prototype
>
> //works kinda like u want , but side effect u dont want
> Bar.prototype = new Foo(); //doesn't create new obj that is duly linked to Foo.prototype as we want, it uses Foo() constructor call to do it.
> ```
>
> ES6 solve it
>
> ```Javascript
> Object.setPrototypeOf( Bar.prototype, Foo.prototype );
> ```
>
> modifies existing Bar prototype
>
> ```Javascript
> Bar.prototype = Object.create( Foo.prototype );
> ```
>
> throws away existing default Bar.prototype and cause garbage collector performance issues( it throws away an obj thats later garbage collected )

> **Inspecting "Class" Relationships**
>
> ```Javascript
> function Foo() { ...//}
>
> foo.prototype.blah = ...;
>
> var a new Foo();
>
> a instanceof Foo;// true
> ```
>
> - `a instanceof Foo` answers: in the entire `[[Prototype]]` chain, does the object arbitrarly pointed to by Foo.prototype ever appear?
> - u can only inquire about the "ancestory" of some obj (a) if you have some func to test with
>
> - `Foo.protoype.isPrototypeOf( a )` answers: in the entire `[[Prototype]]` chain of a, does _Foo.protoype_ ever appear?
>
> - The strange `_proto_` property retrieves the internal `[[Prototype]]` of an object as a refeernce
> - `_proto_` looks like property, but it's actully more appropriate to think of it is a _getter/setter_

> **Create()ing Links**
>
> - `Object.create` is hero
>
> ```Javascript
> var foo = {
>   something: function () { console.log( "kavo" ) }
> };
>
> var bar = Object.create( foo );
>
> var.something(); // kavo
> ```
>
> `Object.create` creates a new obj linked to the objext we specified, which gives us all the pewer(delegation) of the `[[Prototype]]` mechanism
>
> - we dont need classes to create meaningfull relationship between two objs

> **Links as Fallback**
> It may be tempting to think that the these links between objs _primarily_ provide a sort of fallback for "missing" properties or methods. While that may be an observed outcome.
>
> ```Javascript
> var anotherObj = {
>   cool: function() { console.log('cool') }
> }
>
> var myObj = Object.create( anotherObj );
>
> myObj.cool(); //cool
> ```
