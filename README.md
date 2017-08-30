# Javascript学习笔记

![Js icon](https://maxcdn.icons8.com/Share/icon/ios7/Logos//javascript1600.png =100x100)

## Overview 概述
这是我在学习Javascript时，边学边记下的一些要点，供参考、复习及速查使用，也希望能够帮助到您。
我会不断完善这个文档，也希望您能提出宝贵意见。

***

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

***

### 2. 数据类型详解
#### 2.1 Undefined类型
Undefined类型只有一个值，即"undefined"。在使用var声明变量但未对其初始化时，这个变量的值就是undefined,例如：  
>	var message;  
>	console.log(message)    //输出 undefined  
>	console.log(message == undefined)   //输出 true

这个例子声明了变量message，但未对其初始化，输出这个值会得到undefined，比较这个变量与undefined字面量，输出true，表明它们是相等的。  
>	var message = undefined;  
>	console.log(message == undefined)    //输出 true  

上面例子使用了undefined值显式的初始化了变量message，但是这是不必要的，因为未经初始化的变量的默认值就是undefined。  

不过，包含undefined值的变量与尚未声明的变量是不一样的，比如：  
>	var message;  
>	//下面这个变量并没有声明  
>	//var age;  
>	console.log(message);  //undefined  
>	console.log(age);  //报错  

对于尚未声明的变量只能执行一个操作，那就是typeof。但是返回值却是undefined，来看下面例子：  
> 	var message;  
>	//未声明age变量  
> 	// var age;  
> 	typeof message; //undefined  
> 	typeof age;  //undefined  
> 	typeof message == typeof age; //true  

这个结果虽然很奇怪，但是有其合理性，因为这两种变量都是不可能执行真正操作的。  

#### 2.2 Null类型
Null 类型是第二个只有一个值的数据类型。从逻辑角度来看，null表示一个对象空指针，而这也是对其使用typeof操作符时得到object返回值的原因，如下：  
>	var message = null;
>	typeof message  //"object" 

如果声明的变量将来准备用来保存对象，那么最好初始化为null，而不是其他值。这样做，只要直接检查null值就可以知道该变量是否已经保存了一个对象的引用，如下面的样子：  
>	if(message != null){  
>	    //一些操作  
>	}

实际上undefined值是派生自null， 因此ECMA-262规定对他们的相等性测试要返回true：  
>	null == undefined //true

#### 2.3 Boolean类型
该类型有两个字面值：true 和 false， 区分大小写，true和True不等，也就是说True和False不是boolean类型，只是标识符。  
这两个值与数字值不是一个概念，因此，true不等于1， false不等于0，所以在做判断时需要注意，不要使用boolean类型和数字进行比较。
ECMAScript中的所有类型都与boolean值有等价的值，要将一个值转换为boolean值，可以调用转型函数Boolean(), 例如：  
>	var message = "Hello world";  
>	var msgBoolean = Boolean(message);  

上面例子中，字符串message被转换为boolean值，该值保存在msgBoolean变量中。可以对任何数据类型值调用Boolean()。至于是返回true还是false，要取决于转换值的数据类型和实际值。参考下表：  

数据类型 | 转换为true的值 | 转换为false的值
------------ | ------------- | ------------
Boolean | true | false
String | 任何非空字符串 | ""(空字符串)
Number | 任何非零数字值(包括无穷大) | 0和NaN
Object | 任何对象 | null
Undefined | N/A | undefined

上表的转换规则对于流控制语句的判断非常重要，因为我们在实际开发中可能不会或每次判断前都将其他类型数据转换为Boolean类型后再做判断。看下面例子：  
>	var message = "Hello world";  
>	if(message){  
>	    console.log("Value is true");  
>	}

运行这段代码，控制台会输出Value is true，因为字符串变量message被自动转换为对应的Boolean值。  

#### 2.4 Number类型
Number类型使用IEEE754格式来表示整数和浮点数。  
其最基本的字面量格式是十进制整数。除了十进制表示外，还可以通过八进制、十六进制的字面值表示。其中八进制值的第一位必须是0，然后是八进制数字（0 － 7）。如果后面的值超过了八进制值范围，前导0将被忽略，且认为是十进制。例如：  
>	var n1 = 072； //八进制  
>	var 呢 ＝ 079； //十进制79

八进制在严格模式下是无效的，Javascript引擎会抛出错误。

十六进制前两位必须是0x，后跟十六进制数字（0-9, A-F）

在进行算数计算时，所有八进制十六进制表示的数值都被转换为十进制

##### 2.4.1 浮点数值  
>	var floatNum1 = 1.1;  
>	var floatNum2 = 0.1;  
>	var floatNum3 = .1; //有效，但不推荐  

保存浮点数值使用的空间是整数的两倍，所以ECMAScript会在可能的时候将浮点数值转换为整数：  
>	var floatNum1 = 1.;  //解析为1
>	var floatNum2 = 10.0; //解析为10

对于极大或极小的浮点数值可以使用科学计数法：
>	var floatNum1 = 3.124e7 //等于31240000，含义为3.124乘以10的7次方  
>	var floatNum2 = 3e-5 //等于0.00003  

注意，在默认的情况下，ECMAScript会将小数点后面有6个零以上的浮点数值转换为e表示法表示的数值  
浮点数值的最高精度是17位小数，但在进行计算时，其精度远远不如整数，例如，0.1加0.2的结果不是0.3，而是0.30000000000000004，这个误差导致无法测定特定的浮点数值。例如：
>	if(a+b == 0.3){  
>	    console.log("You got a result: 0.3");  
>	}

上面的例子中，你永远无法得到0.3， 所以不要使用浮点数值做特定的检测  
##### 2.4.2 数值范围  
Javascript像其他语言中的数值一样存在内存限制。  
ECMAScript能够表示的最小数值保存在`Number.MIN_VALUE`中，在大多数浏览器中，这个值是5e-324。  
ECMAScript能够表示的最大数值保存在`Number.MAX_VALUE`中，在大多数浏览器中，这个值是1.7976931348623157e+308。
如果某次计算得到了一个超出Javascript数值范围的值，那么这个数值将会被自动转换成特殊的Infinity值。具体来说，如果这个值是负数，则转换为`-Infinity`，如果这个值是正数，则转换为`Infinity`。
要想确定一个数值是不是无穷的，即位于最大值和最小值之间，我们应该使用`isFinite()`来检测，如果数值在最大最小值之间，则返回true。如下所示：  
>	var result = Number.MAX_VALUE + Number.MAX_VALUE;  
>	console.log(isFinite(result)); //false  

##### 2.4.3 NaN
NaN,即非数值（Not a Number）。这个数值是一个特殊数值，用来表示一个本来要返回数值的操作数未返回数值的情况，避免了抛出错误而中断脚本的执行。在其他语言中，如果0做为分母，会导致错误，从而停止执行代码。但在ECMAScript中，任何数除以0会得到NaN，因此不影响其他代码的执行，只要你的代码足够健壮。  

NaN有两个特点：

1. 任何涉及NaN的操作，都会返回NaN
2. NaN与任何数值都不想等，包括NaN本身  

针对这两个特点，ECMAScript定义了isNaN()函数。这个函数接收一个参数，然后对参数进行类型转换，尝试将该参数转换为数值类型。如果转换失败，则返回true。例如：  
>	console.log(isNaN(NaN)); //true  
>	console.log(isNaN(10)); //false  
>	console.log(isNaN("10")); //false  
>	console.log(isNaN("Im a String")); //true  
>	console.log(isNaN(true)); //false boolean会被转换为0或1  

```isNan()也适用于对象。```
```在基于对象调用该函数时，会首先调用对象的valueOf()方法，然后确定该方法返回值是否可以转换为数值```
```如果不能则调用对象的toString()方法，在测试返回值。```
```这个流程也是ECMAScript中内置函数和操作符的一般执行流程```

##### 2.4.4 数值转换
有三个函数可以把非数值转换为数值：

<table class="table table-bordered table-striped table-condensed">
	<tr>
		<td rowspan="7">
			Number()	
			<br/>
			可用于任何类型
		</td>
		<td>Boolean</td>
		<td>true 1， false 0 </td>
	</tr>
	<tr>
		<td>数值</td>
		<td>返回该数值</td>
	</tr>
	<tr>
		<td>null</td>
		<td>0</td>
	</tr>
	<tr>
		<td>undefined</td>
		<td>NaN</td>
	</tr>
	<tr>
		<td>字符串</td>
		<td>
			<table>
				<tr>
					<td>"1"</td>
					<td>1</td>
				</tr>
				<tr>
					<td>"123"</td>
					<td>123</td>
				</tr>
				<tr>
					<td>"011"</td>
					<td>11</td>
				</tr>
				<tr>
					<td>"1.1"</td>
					<td>1.1</td>
				</tr>
				<tr>
					<td>"01.1"</td>
					<td>1.1</td>
				</tr>
				<tr>
					<td>"0xf"</td>
					<td>15</td>
				</tr>
				<tr>
					<td>除前面以外的字符</td>
					<td>NaN</td>
				</tr>
			</table>
		</td>
	</tr>
	<tr>
		<td>对象</td>
		<td>valueOf()->toString(),参考上面isNaN()的流程</td>
	</tr>
</table>


           
<table class="table table-bordered table-striped table-condensed">
	<tr>
		<td rowspan="10">
			parseInt()	
			<br/>
			用于字符串
		</td>
		<td rowspan="4">步骤</td>
		<td colspan="2">1.忽略字符串前的空格</td>
	</tr>
	<tr>
		<td colspan="2">2.取得第一个非空字符，如果不是数字字符或负号，返回NaN</td>
	</tr>
	<tr>
		<td colspan="2">3.第一个字符是数字字符或负号，向后继续解析</td>
	</tr>
	<tr>	
		<td colspan="2">4.解析到字符结束，或遇到一个非数字字符</td>
	</tr>
	</tr>
	<tr>
		<td rowspan="5">例子</td>
		<td>
			"   1234hosea" 
		</td>
		<td>1234</td>
	</tr>
	<tr>
		<td>
			"22.5"
		</td>
		<td>
			22
		</td>
	</tr>
	<tr>
		<td>
			""
		</td>
		<td>
			NaN
		</td>
	</tr>
	<tr>
		<td>
			"0xA"
		</td>
		<td>
			10
		</td>
	</tr>
	<tr>
		<td>
			"070"
		</td>
		<td>
			56
		</td>
	</tr>
</table>
>	使用parseInt()解析八进制字面量的字符串时，ECMAScript3和5存在分歧。如上面的"070", 在ECMAScript3中被认作是八进制进行解析转换，在ECMAScript5中，parseInt()已经不具备解析八进制字面量的能力，因此前导零会被认为是数值0，所以结果会得到十进制的数值0。那么，为了避免这样的问题，可以为这个函数提供第二个参数：转换时的基数（即，进制）。  
>	例如:  
>	        `var num1 = parseInt("AF", 16)` //得到175  
>	        `var num2 = parseInt("10", 2)`//  2  
>	        `var num3 = parseInt("10", 8)`  //  8  
>	        `var num4 = parseInt("10", 10)`  //  10  
>	        `var num5 = parseInt("10", 16)`  //  16  

<table class="table table-bordered table-striped table-condensed">
	<tr>
		<td rowspan="10">
			parseFloat()	
			<br/>
			用于字符串
		</td>
		<td rowspan="4">步骤</td>
		<td colspan="2">1.忽略字符串前的空格</td>
	</tr>
	<tr>
		<td colspan="2">2.取得第一个非空字符，如果不是数字字符或负号，返回NaN</td>
	</tr>
	<tr>
		<td colspan="2">3.第一个字符是数字字符或负号，向后继续解析</td>
	</tr>
	<tr>	
		<td colspan="2">4.解析到字符结束，或遇到一个非浮点数字字符</td>
	</tr>
</table>
>	parseFloat()解析字符串时，遇到的第一个小数点，是有效的，第二个小数点则是无效的，因此后面的字符串将被忽略。  
>	parseFloat()会忽略前导0， 也就是八进制会去掉前导0，然后按照十进制解析  
>	parseFloat()可以解析前面提到的所有浮点数值和十进制整数  
>	十六进制字符串始终会解析为0  
>	parseFloat()没有第二个参数  
>	如果字符串是一个可以解析为整数的字符串，会返回整数  
>	例子：  
>	        `var num1 = parseFloat('1234blue');`  //  1234  
>	        `var num2 = parseFloat('0xA');`  //  0  
>	        `var num3 = parseFloat('22.5');`  // 22.5  
>	        `var num4 = parseFloat('22.34.5');`  // 22.34  
>	        `var num5 = parseFloat('098.5');`  // 98.5  
>	        `var num6 = parseFloat('3.125e7');`  // 31250000

#### 2.5 String类型










