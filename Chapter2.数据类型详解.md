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
字符串用单引号`'`或者双引号`"`包裹
##### 2.5.1 字符字面量
String数据类型包含一些特殊的的字符字面量，也称为`转义序列`或者`转义字符`。这些特殊字符用来表示非打印字符，或具有其它用途。见下表：

字面量 | 含义
--- | ---
\n | 换行
\t | 制表
\b | 空格
\r | 回车
\f | 进纸
\\ | 斜杠
\' | 单引号`'`，'I\'m Hosea Lee.'
\" | 双引号`"`，"I said: \"I'm Hosea Lee\""
\xnn | 以十六进制码nn表示的一个字符，n为0～F，\x41表示A
\unnnn | 以十六进制码nnnn表示的一个Unicode字符，n为0～F，\u03a3表示∑

这些字符字面量可以出现在字符串任意位置，且在长度计算时占1个字符长度。

##### 2.5.2 字符串的特点
ECMAScript中的字符串是不可变的。也就是说，字符串只能创建或销毁。
>	var lang = "Java";  
>	lang = lang + "script";

上面例子中，第一步声明变量lang并初始化赋值字符串"Java"，第二步，实现的过程是：首先创建一个10个字符的新字符串，然后在这个新字符串中填充"Javascript"，最后一步，销毁之前产生的"Java"和"script"，因为这两个字符串没有被任何变量引用。

##### 2.5.3 转换为字符串
要把一个值转换为一个字符串有两种方式。

1.`toString()`  
	这是一个几乎所有值都有的方法，后面会单独讨论，先来看几个例子：  
>	var age = 11;  
>	var age_str = age.toString();  //字符串"11"  
>	var found = true;  
>	var found_str = found.toString();  //字符串"true"  

`数值、布尔值、对象和字符串值都有toString()方法，但null和undefined值没有。`  

多数情况下，调用toString()方法不必传任何参数，但是在对数值类型变量调用该方法时，可以传递一个参数：**输出数值的基数。** 默认情况，toString()方法是用十进制格式返回数值的字符串表示。而通过传递基数，可以实现输出二进制、八进制、十进制、十六进制，甚至其它任意有效进制格式表示的字符串值，见下面例子：  
 
>	var num = 10;  
>	console.log(num.toString());  //"10"  
>	console.log(num.toString(2));  //"1010"  
>	console.log(num.toString(8));  //"12"  
>	console.log(num.toString(10));  //"10"  
>	console.log(num.toString(16));  //"a"

2.`String()`  
	在不知道待转换变量是不是null或undefined的情况下，可以使用`String()`，这个函数可以将任何类型的值转换为字符串。  
	
转换规则如下：  
	
* 如果值有toString()方法，调用该方法（无参）并返回结果
* 如果值是null，返回"null"
* 如果值是undefined，返回"undefined"

看下面例子：  
>	var value1 = 10;  
>	var value2 = true;  
>	var value3 = null;  
>	var value4;  
>	console.log(String(value1));  //"10"  
>	console.log(String(value2));  //"true"  
>	console.log(String(value3));  //"null"  
>	console.log(String(value4));  //"undefined"

#### 2.6 Object类型
ECMAScript中的对象其实是一组数据和功能的组合。可以通过`new`操作符后跟要创建的对象类型名字来创刊对象。如：
>	var o = new Object();		//括号可以省略，如果不需要给构造函数传递参数，但不推荐

仅仅创建Object的实例并没有什么用处，在ECMAScript中，Object类型是所有它的实例的基类。  
Object的每一个实例都具有下列属性he方法：

*	Constructor:  保存用于创建当前对象的函数，对于上面的例子，构造函数（constructor）就是Object()。
*	hasOwnProperty(propertyName): 用于检查给定的属性(propertyName)在当前实例中是否存在。
*	isPrototypeOf(object): 用于检查传入的对象是否是另一个对象的原型。
*	propertyIsEnmumerable(propertyName): 用于检查给定的属性是否能够使用for-in语句来枚举。
*	toLocaleString(): 返回对象的字符串表示，该字符串与执行环境的地区对应。
*	toString(): 返回对象的字符串表示。
*	valueOf(): 返回对象的字符串、数值或布尔值的表示，通常与toString()的返回值相同

由于Object是所有对象的基础，因此所有对象都具有上面这些基本的属性和方法。因为Object相对其它数据类型较复杂，我们后面再详细讲。


