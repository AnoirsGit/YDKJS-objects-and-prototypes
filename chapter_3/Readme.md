# Chapter 3
### Terms  
  - ***SIMPLE PREMITIVES*** - is a premitive types (`string, boolean, number, `)

## Object
> **Syntax**  
>  * ***Literal:*** `let obj = { key: value, ... }`  
>  * ***Constructed:*** `let obj = new Object(); `   
>  ` obj.key = value;`


>  **Type**  
> * `null` is sometimes referred as an object type   
> * `typeof null` returns `object`   
> * **function** is a subtype of object ( **callable object**)  
> * **array** is also object
> * ***everything in JavaScript is an object*** is a misstatement
>

> **Built-in Objects**  
> String, Number, Boolean, Object, Function, Array, Date, RegExp, Error
> ```
>var strObj = new String("sdf");
>typeof strObj;  //sdf
>```

> **Contents**
> * **Contents** implies that these values are actually stored inside the object.
> * Engine stores values in *implementation-dependent ways*, and my very well noot store them in some object container. It stores property names which will be used as pointer


> **Computed Property Names**   
> `let kavo = { [prefix + 'str'] = value}`


> **Deep Copy of Object**  
>`let newObj = JSON.parse( JSON.stringify( oldObj ) )`