# Function
Function引用类型
每个函数都是Function类型的实例，而且都与其他引用类型一样具有属性和方法。由于函数是对象，因此函数名实际上也是一个指向函数对象的指针。
## 1、创建函数的方式：
* 函数声明：`function sum (num1, num2) { return num1 + num2; }`
* 函数表达式：`var sum = function(num1, num2){ return num1 + num2; }; `
* 构造函数：`var sum = new Function("num1", "num2", "return num1 + num2");`

注意：我们不推荐使用构造函数来创建函数，因为这种语法会导致解析两次代码（第一次是解析常规ECMAScript代码，第二次是解析传入构造函数中的字符串），从而影响性能。
## 2、函数特点：
* 没有重载：后面函数覆盖前面的
* 函数声明提升：解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。除了什么时候可以通过变量访问函数这一点区别之外，函数声明与函数表达式的语法其实是等价的。
* 函数特有的内部属性：this 和 arguments
  * 函数.caller：这个属性中保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值为null。
  * arguments.callee：该属性是一个指针，指向拥有这个arguments对象的函数。可以消除函数的执行与函数名紧紧耦合在了一起，这种紧密耦合的现象
  * arguments.caller：在严格模式下访问它也会导致错误，而在非严格模式下这个属性始终是undefined。定义这个属性是为了分清arguments.caller和函数的caller属性。
  
```
//因为outer()调用了inter()，所以inner.caller就指向outer()。
function outer(){     
  inner();  
} 
function inner(){     
  alert(inner.caller); 
  //为了实现更松散的耦合，也可以通过arguments.callee.caller来访问相同的信息。
  //alert(arguments.callee.caller);
} 
outer(); 
```
## 函数属性
每个函数都包含两个属性：
* length：表示函数形参的个数
* prototype：保存它们所有实例方法的真正所在。prototype属性是不可枚举的，因此使用for-in无法发现。
## 函数非继承的方法：
* call()
* apply()
* bind(）
## 函数继承的方法：
* toString()/toLocaleString()：始终都返回函数的代码字符串形式。返回代码的格式则因浏览器而异——有的返回的代码与源代码中的函数代码一样，而有的则返回函数代码的内部表示，即由解析器删除了注释并对某些代码作了改动后的代码。
* valueOf()：返回函数代码。
