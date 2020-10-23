1. 函数作为普通函数被调用，这是函数调用的常用形式。

   ```javascript
   function add(a, b) {
     return a + b;
   }
   add(); // 调用add函数
   ```

   **非严格模式**下，函数执行时，**`this`指向全局对象，对于浏览器而言则是`window`对象**；如果在**严格模式**下，`this`的值则是`undefined`。

2. ### 作为对象的方法

   函数也可以作为对象的成员，这种情况下，该函数通常被称为对象方法。当函数作为对象的方法被调用时，**`this指向该对象`**，此时便可以通过`this`访问对象的其他成员变量或方法。

   ```javascript
   var counter = {
     num: 0,
     increase: function() {
       this.num++;
     }
   }
   counter.increase();
   ```

3. ### 作为构造函数

   函数配合`new`关键字使用时就成了构造函数。构造函数用于实例化对象，构造函数的执行过程大致如下：

   1. 首先创建一个新对象，这个新对象的`__proto__`属性指向构造函数的`prototype`属性。
   2. 此时构造函数的`this`指向这个新对象。
   3. 执行构造函数中的代码，一般是通过`this`给新对象添加新的成员属性或方法。
   4. 最后返回这个新对象。

4. ### 通过call, apply调用

   `apply`和`call`是函数对象的原型方法，挂载于`Function.prototype`。利用这两个方法，我们可以显示地绑定一个`this`作为调用上下文，同时也可以设置函数调用时的参数。

   `apply`和`call`的区别在于：提供参数的形式不同，`apply`方法接受的是一个参数**数组**，`call`方法接受的是参数**列表**。

   ```javascript
   someFunc.call(obj, 1, 2, 3)
   someFunc.apply(obj, [1, 2, 3])
   ```

   注意，在非严格模式下使用`call`或者`apply`时，如果**第一个参数被指定为`null`或`undefined`，那么函数执行时的`this`指向全局对象（浏览器环境中是`window`）；如果第一个参数被指定为原始值，该原始值会被包装**。







手写new函数　　

```
function newTest (constructFunction){
	let obj = {};
	obj.__proto__ = constructFunction.prototype;
	return function(){
		constructFunction.apply(obj,arguments);
		return obj;
	}
}
```

　　　注意：当构造函数中有返回对象时候，最终new出来的对象会是构造函数的返回值，而不是new过程中生成的对象。仅当构造函数返回值是对象时有效，当不是对象时依旧返回new过程中形成的对象（无论如何new 构造函数之后都会返回一个对象值）。



例题：

```
var name = '222'
var a = {
	name : '111',
	say : function(){
		console.log(this.name)
	}
}
var fun = a.say
fun();  //222 fun = a.say,fun指向a.say方法，调用fun()相当于执行say(),this.name====>window.name						
a.say();//111 a.say() a调用了say方法，this指向 a this.nam ====> a.name

var b = {
	name : '333',
	say : function (fun){
		fun()
	}
}
b.say(a.say)//222  a.say 指向 方法say 相当于 b.say(say(){console.log(this.name)})
						var b = {
              name : '333',
              say : function (fun){ //同理 fun=a.say
                fun()
              }
            }
b.say = a.say
b.say()// 333

```



