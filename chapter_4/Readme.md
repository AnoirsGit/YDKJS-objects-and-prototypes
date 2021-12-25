# Chapter 4  
### Terms  
  - ***CALL SITE*** - The location where function is called

## "Class"

> **Class Theory**  
>  OO or class-oriented programming stresses that data intrinsically has associated behavior that operates on it, so proper designing to package up the data and behavior together.


> * **nheritance** is the mechanism of basing an object or class upon another object (prototype-based inheritance) or class (class-based inheritance), retaining similar implementation.


> * **polymorphism** describes the idea that a genearal behavior from aparent class can be overridden in a chikls class to give it more specifics


>  **JavaScript Classes**  
> Does JavaScript actually has classes? ***NO***   
> Since Class are a design pattern, you can with quite a bit of effort implement approcimations for much of classical class functionality.


> **Building**   
> The traditional memtaphor for "class" - and "instance" besed thinking comes from building construction
> * A class is a blueprint. To actually get an object we can interact with we must build ( aka instantiate ) something from the class. The end result of such ( construction ) is an object, typically called an **instance**. which we can directly call methods on and access any public data properties from, as necessary
> * The object is a copy of all the characteristics described by the class  


> **Mixins**
> JS objext mechanism does not automatically perform copy behavior when u inherit or instantioate. Objexts dont het copied to other objects, they get **linked together**
> Since observed class behaviors in other languages imply copies, JS developers fake the missing copy behavior of class

> **Explict Mixins** 
> Since Js will not automatically copy behavioor form Vehicle to Car. We can create a utility that manually copies. Mostly a utility called extend(...)  
>```
>function extend( sourceObj, targetObj ) {
> for ( var key in sourceObj ) {
>   if (!( key in targetObj)){
>     targetObj[key] = sourceObj[key];
>     }
>   }
> return targetObj;  
>}; 
>
>var Vehicle = {
> engines: 1,
> ignition: someFunction...,
> drive: someFunction...  
>}
>
>var Car = extend( 
> Vehicle , 
> { 
>   wheel: 4, 
>   drive: function(){
>     Vehicle.drive.call( this )
>     someOtherLogic... 
>   }
> }
>)
>```


> **Parasitic inheritance**
> Variation on this explicit mixin pattern. which is both in same ways explicit and in other implicit
>```
>function Vnehicle(){
> this.engines = 1;
>}
>
>Vehicle.prototype.drive = function() {
> this.ignition();
> ... someLogic
>}
>
>function Car() {
> var car = new Vehicle();
> car.wheels = 4;
> car vehDrive = car.drive;
> car.drive = function (){
>   vehDrive.call( this );
>   ... someLogic
>   return car
>}
>```


> **Implicit Mixins**
> it related with explicit polymorphism   
> ```
> var Something = {
>   cool: function(){
>     this.greeting = 'hi world';
>     this.count = count? count ++ : 1;
>   }
> };
> var Another = {
>   cool: function() {
>     Something.cool.call( this );
>   }
> }
>
>Something.cool();
>Something.greeting; //hi world
>Something.count; //1
>
>
>Another.cool();
>Another.greeting; //hi world
>Another.count; //1 (not shared state with SOmething)
> ```
>The end result is theat the assignment that `Something.cool()` makes are applied against the `Another` objext rather than the `Something` object