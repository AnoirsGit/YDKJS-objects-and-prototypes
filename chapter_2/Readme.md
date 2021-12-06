# Chapter 2  
### Terms  
  - ***CALL SITE*** - The location where function is called

## THIS  
> **Default Binding**  
>  * Binds **THIS** reference of CALL SITE  
>  * If function called in a global area it will take this as global area reference, (IN STRICT MODE GLOBAL OBJ IS NOT ELIGIBLE)  


>  **Implicit Binding**  
> ```
>function foo(){
>   console.log ( this.a);
>}
>
>var obj = {
>	a:2, 
>	foo:foo
>}
>
>obj.foo(); // 2
>```
>CALL SITE uses OBJ context to reference


> **Implicitly Lost**
> ```
>var bar = obj.foo;
>	var a = ‘global’;
>	bar(); // global // 
>```
>Beacuse obj.foo is reference to itself


> **Explicit Binding**
> * specify what is THIS to be as
> * `foo.call({a:’kavo’})` // kavo


> **Hard Binding**
> * its bind


> **New Binding**  
>```
>function foo(){
>    this.a = a;
>}
>var bar = new foo(2);
>console.log(bar.a) //2
> ```
> NEW  operator is no connection to class oriented functionality


> **Ignored This**
> * If u pass `null` to `apply, call`, those values will be ignored and instead the ***default binding*** will be applied


> **Lexical THIS**
> ```
>function foo () {
>    return a => console.log(this.a)
>}
>
> var obj1 = { a: 2 };
> var obj2 = { a: 3 };
> var bar = foo.call( obj1 );
> bar.call( obj2 ); //2, not 3
> ```
>
> * the arrow-func created in `foo()` lexically capctures whatever `foo()`s this at its call time `foo()` was this-bound to `obj1`, `bar` (reference to arrow-func) will also be this bound to `obj1`  
>
>The lexical binding on arrow func **cannot be overriden**


