# *this* keyword
**_this_** keyword refers to an object which is executing the current bit of code.

In other word, Every function while executing, has a reference to its current execution context, called **_this_**. 
Execution context means here is how the function is called, when it is called.

To understand **_this_** keyword, only we need to know how, when and from where the function is called, 
does not matter where function is declared.

``` 
function bike() {
  console.log(this.name);
}

var name = "Ninja";
var obj1 = { name: "Pulsar", bike: bike };
var obj2 = { name: "Gixxer", bike: bike };

bike();           // "Ninja"
obj1.bike();      // "Pulsar"
obj2.bike();      // "Gixxer"
```

## Default and Implicit Binding of *this* keyword

  * If we are in strict mode then defaulted **_this_** keyword to undefined value otherwise defaulted **_this_**  keyword as global object, 
  it’s called default binding of **_this_**  keyword. (Window Object incase of browser).
  * when there is an object property which we are calling as a method then that object(context object) becomes **_this_** keyword, 
  it’s implicit binding of **_this_**  keyword.

```
var obj1 = {
  name: "Pulsar",
  bike: function() {
    console.log(this.name);
  }
}
var obj2 = { name: "Gixxer", bike: obj1.bike };
var name = "Ninja";
var bike = obj1.bike;

bike();           // "Ninja"
obj1.bike();      // "Pulsar"
obj2.bike();      // "Gixxer"
```

Its important to know how, when and from where the function is called
```
function bike() {
  var name = "Pulsar";
  baz();
}

function baz() {
  console.log(this.name);
}

var name = "Ninja";
bike();       // "Ninja" 
```

## Explict and Fixed Binding of *this* keyword
  * If we use call and apply method with calling function, both of those methods take as their first parameter as execution conext.
  that is **_this_** binding.
```
function bike() {
  console.log(this.name);
}

var name = "Ninja";
var obj = { name: "Pulsar" }

bike();           // "Ninja"
bike.call(obj);   // "Pulsar"
```
  * In Fixed binding or Hard binding we can force the **_this_** object to be same always no matter from where it get called.
```
var bike = function() {
  console.log(this.name);
}

var obj1 = { name: "Pulsar" };
var obj2 = { name: "Gixxer" };

var originalFun = bike;
bike = function() {
  originalFun.call(obj1);
};

bike();           // "Pulsar"
bike.call(obj2);  // "Pulsar"
```
  * In Javascript Function.prototype.bind()  method helps to achive explicit **_this_** binding.
 ```
 var bike = function(maker, engine) {
  console.log("Name:" + this.name + ", Maker:"+ maker+ ", Engine:"+engine);
}

var obj = {name: "Ninja"};
bike = bike.bind(obj, "Kawasaki");

bike('1000cc');   // "Name:Ninja, Maker:Kawasaki, Engine:1000cc"
 ```
# The *new* keyword
The **_new_** keyword in front of any function turns the function call into constructor call
Below things occured when new keyword put in front of function 
  * a brand new empty object get created
  * new empty object get linked to different object
  * new object gets bound as **_this_** keyword for the purpose of that function call
  * if that function does not return anything then it implicit insert a return **_this_**
```
function bike() {
  var name = "Ninja";
  this.maker ="Kawasaki";
  console.log(this.name + " " + maker);
}

var name = "Pulsar";
var maker = "Bajaj";

obj = new bike();
```
# Precedence of this keyword binding
  * First it checks whether the function is called with new keyword.
  * Second it checks whether the function is called with call or apply method means explicit binding.
  * Third it chceks if the function called via context object (implicit binding).
  * Default global object (undefined incase of strict mode).

  

