# Chapter 3

### Terms

- **_SIMPLE PREMITIVES_** - is a premitive types (`string, boolean, number, `)

## Object

> ### **Syntax**
>
> - **_Literal:_** `let obj = { key: value, ... }`
> - **_Constructed:_** `let obj = new Object(); `  
>   ` obj.key = value;`

> **Type**
>
> - `null` is sometimes referred as an object type
> - `typeof null` returns `object`
> - **function** is a subtype of object ( **callable object**)
> - **array** is also object
> - **_everything in JavaScript is an object_** is a misstatement

> **Built-in Objects**  
> String, Number, Boolean, Object, Function, Array, Date, RegExp, Error
>
> ```Javascript
> var strObj = new String("sdf");
> typeof strObj;  //sdf
> ```

> **Contents**
>
> - **Contents** implies that these values are actually stored inside the object.
> - Engine stores values in _implementation-dependent ways_, and my very well noot store them in some object container. It stores property names which will be used as pointer

> **Computed Property Names**  
> `let kavo = { [prefix + 'str'] = value}`

> **Deep Copy of Object**  
> `let newObj = JSON.parse( JSON.stringify( oldObj ) )`
