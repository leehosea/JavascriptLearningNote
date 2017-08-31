### 1. 基础部分
#### 1.1 标识符
##### 指变量、函数、属性的名字，或者函数的参数  
##### 规则：  
1. 第一个字符必须是字母、下划线、美元符号  
2. 其他字符可以是字母、下划线、美元符号或数字  
3. ECMAScript标识符采用驼峰命名法
4. 不能用做标识符的有：关键字、保留字、true、false、null  

#### 1.2 注释 
##### ECMAScript使用C风格注释
##### 两种注释方式:  
1. 单行注释  
>	//两个左斜杠 
2. 块级注释  
>/\*  
> * 注释内容，此行首的星号可省略，一般为提高注释可读性  
> \*/

#### 1.3 语句  

##### ECMAScript中的语句以一个分号（;）结束，如果省略分号，则由解释器确定语句的结尾  
>	var  sum = a + b	//即使没有分号，也是有效语句，但是不推荐  
>	var diff = a - b;	//有效的语句，推荐

##### 可以使用C风格的语法，把多条语句组合到一个代码块中，即放入到花括号｛｝中，例如：  
>	if(test){  
>	    console.log(test);  
>	}


#### 1.4 关键字 和 保留字  
##### ECMA-262 确定了一组具有特殊用途的关键字，这些关键字可用于语句控制或者一些特殊指令，关键字不能用于标识符 如下：
`break`  `do`  `instanceof`  `typeof`  
`case`  `else`  `new`  `var`  `catch`  
`finally`  `return`  `void`  `continue`  
`for`  `switch`  `while`  `debugger`  
`function`  `this`  `with`  `default`  
`if`  `throw`  `delete`  `in`  `try`  
##### ECMA-262 还定义了一组保留字，同样不可用于标识符，这组保留字留作将来使用，如下：  
`abstract`  `enum`  `int`  `short`  `boolean`  `export`  `interface`  `static`  
`byte`  `extends`  `long`  `super`  `char`  `final`  `native`  `synchronized`  
`class`  `float`  `package`  `throws`  `const`  `goto`  `private`  `transient`  
`debugger`  `implements`  `protected`  `volatile`  `double`  `import`  `public`  
##### 在第五版非严格模式下运行时，保留字缩减为一下这些：  
`class`  `enum`  `extends`  `super`  `const`  `export`  `import`  
##### 在第五版严格模式下，还对以下保留字做了限制：  
`implements`  `package`  `public`  `interface`  
`private`  `static`  `let`  `protected`  `yield`  
##### let 和 yield是第五版新增保留字，其余都是第三版  
```第五版中，虽然不能使用关键字和保留字作为标识符，但是用做对象的属性名。```
```但不推荐这样做，以便于将来更好的与ECMAScript版本兼容。```

#### 1.5 变量  
ECMAScript的变量是松散类型  
定义变量时要使用`var`操作符，例如：`var message;`  这里定义了一个名为message的变量，该变量可以用于保存任何值。  
ECMAScript也支持直接初始化变量，因此在声明变量的同时就可以做赋值操作，例如：`var message = 'Hi';`  
也可以更改变量类型，如下：  
         `var message = 'Hi'; //声明message为字符串变量`  
         `message = 100;  //更改message变量类型为数字，有效的操作，但是不推荐`  
需要注意的是，`var`声明的变量将成为该变量所在作用域的局部变量，如果该变量是在一个函数内定义，那么变量在函数执行完毕退出后就会被销毁，例如:  
>	function test(){  
>	    var message = 'Hi';  //局部  
>	}  
>	test();  
>	console.log(message);  //错误的  

上面的console输出会报错，但如果省略var，直接声明message，那么该变量则为全局变量，但是不建议这样做，因为过多的全局变量会造成难以控制而导致全局变量污染。  
我们也可以用一条语句定义多个变量，如下：  
>	var message = 'Hi',  
>	      found = false,  
>	      age = 32;

#### 1.6 数据类型  
ECMAScript中有五种简单数据类型，也称作基本数据类型: 

* Undefined  
* Null
* Boolean
* String
* Number  

还有一种复杂数据类型：

* Object  

Object本质上是由一组无序键值对组成。ECMAScript不支持任何形式的自定义类型，所有值最终都是上述六种类型之一。因为ECMAScript数据类型的动态性这个特点，也确实没有定义其他更多类型的必要了。

#### 1.7 使用typeof检测数据类型
*typeof是**操作符**，不是~~函数~~*  

返回值是以下某个字符串

* "undefined" 
* "boolean"  
* "string"
* "number"
* "object"
* "function"  

有时候，typeof会返回一些比较迷惑人的但正确的值，比如`typeof null`，会返回"object"， 因为特殊值null被认为是一个空对象引用，Safari5及之前版本、Chrome7及之前版本对正则表达式调用typeof操作符会返回"function", 而其他浏览器会返回"object"。  
