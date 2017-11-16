### 4. 语句
说明：前三章边看书边写，内容啰哩啰嗦，不方便后续查找重要内容。从此章开始，内容简要陈述一下，主要描述一些语法特点和经验。  
#### 4.1 if语句
if语句的语法是：if(condition) statement 1 else statement2  
其中，condition是条件，可以是任意表达式；而且对这个表达式求值的结果不一定是布尔值。  
推荐的写法 ：
>  if( condition ) {  
>  &#8195;&#8195;statement1  
>  } else {  
>  &#8195;&#8195;statement2  
>  }

####4.2 do-while语句
do-while语句是一种后测试循环语句。  
格式：
>  do {  
>  &#8195;&#8195;statement;  
>  }while( condition )  

#### 4.3 while语句
while语句是前测试语句。  
格式：  
>  while ( expression ) {  
>  &#8195;&#8195;statement;  
>  }

#### 4.4 for语句
for语句也是一种前测试循环语句， 但它具有在执行循环之前，初始化变量和定义循环后要执行的代码的能力。
格式：  
>	for( initialization; expression; post-loop-expression ) {  
>	&#8195;&#8195; statement;  
>	}

**注意：使用while循环做不到的事情，for循环同样也做不到。for循环只是把与循环有关的代码集中在一个位置。**

#### 4.5 for-in语句
for-in语句是一种精准的迭代语句，常用来枚举对象属性。  
格式：
>	for( property in expression ) statement

示例：  
>	for(var propName in window){  
>	&#8195;&#8195;  document.write( propName );  
>	}

如果表示要迭代的对象的变量值为 null 或 undefined，for-in 语句会抛出错误。ECMAScript 5 更正了这一行为；对这种情况不再抛出错误，而只是不执行循环体。为了保证最大限度的兼容性，建议在使用for-in 循环之前，先检测确认该对象的值不是 null 或 undefined。

#### 4.6 label语句
不常用，略...

#### 4.7 break 和  continue 语句

break强制退出循环并执行循环后面的语句。  
continue强制退出本次循环并返回循环顶部继续下一次循环。

#### 4.8 with语句
with语句的作用是将代码的作用域设置到一个特定的对象中。
格式：  
>	with( expression ) statement;  

定义 with 语句的目的主要是为了简化多次编写同一个对象的工作，例如：  
>	var qs = location.search.substring(1);  
>	var hostname = location.hostname;  
>	var url = location.href;  

上面例子中每行都使用了location对象，如果使用with，则：  
> 	with(location){  
> 	&#8195;&#8195;var qs = search.substring(1);  
> 	&#8195;&#8195;var hostname = hostname;  
> 	&#8195;&#8195;var url = href;  
> 	}

**注意：大量使用with语句会导致性能下降，也给debug调试造成困难。严格模式下不允许使用with语句**

#### 4.9 switch语句
格式：  
>	switch ( expression ){  
>	&#8195;&#8195;case value:  
>	&#8195;&#8195;&#8195;&#8195;statement;  
>	&#8195;&#8195;case value:
>	/*向下合并*/  
>	&#8195;&#8195;case value:  
>	&#8195;&#8195;&#8195;&#8195;statement;  
>	&#8195;&#8195;&#8195;&#8195;break;  
>	&#8195;&#8195;&#8195;&#8195;break;  
>	&#8195;&#8195;default:  
>	&#8195;&#8195;&#8195;&#8195;statement;

#### 4.10 函数








