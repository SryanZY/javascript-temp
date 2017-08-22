# javascript-temp
js学习笔记
  
## ***数据类型***  

typeof null = object, null == undefined(true)  
空字符在布尔值上表现为false，然而空[] 或 ｛｝表现为true  
```  
if ([]) {
  console.log(true);
}
// true

if ({}) {
  console.log(true);
}
// true   
```  
### 数值  
JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的。  
```  
1 === 1.0 // true  
```   
    
**数值常用函数**   

*math.pow(2, 53)*  -2的53次幂   

*Number.MAX_VALUE*  -1.7976931348623157e+308   

*Number.MIN_VALUE*  -5e-324 

*parseInt*  -将字符串转换为整数  


   
在ES5中+0等于-0，NaN！=NaN，在ES6中+0！=-0， NaN = NaN   
```  
Object.is(+0, -0) // false  
Object.is(NaN, NaN) // true   
```   
***  

#### ***关于NaN和infinity***   

```   
typeof NaN  // Number  
```   
NaN与任何数运算（包括本身）都是NaN，可以通过isNaN来判断  
```   
isNaN(NaN)  // true  
```   
**isNaN只对数值有效，输入其他的会先转换为数字，因此返回true的不一定就是NaN，可以通过函数判断**   
```  
function tmpIsNaN(val) {
    return typeof(val) === 'number' && isNaN(val);
}  
```   
   

0 / 0 结果是NaN， 而非零值除以0结果是infinity， 1  / 0: infinity   
infinity与NaN比较总是返回false，
```  
Infinity > NaN // false
-Infinity > NaN // false
-Infinity < NaN // false  
```   

isFinity返回一个布尔值，用来判断某个值是不是正常数值，而不是判断infinity  
```   
isFinite(Infinity) // false
isFinite(-1) // true
isFinite(true) // true
isFinite(NaN) // false  
```   

******   
******   
## ***字符串***   

如果要在单引号内部使用单引号（双引号内部使用双引号），则需要在前面进行转义   
```  
'he is a brand new boy\'template\'!'  
```   

如果需要分成多行写，则在每行的尾部使用反斜杠   
```  
var longString = "Long \
long \
long \
string"; 
// "Long long long string"  
```   

***转义***   
```   
\0 null（\u0000）
\b 后退键（\u0008）
\f 换页符（\u000C）
\n 换行符（\u000A）
\r 回车键（\u000D）
\t 制表符（\u0009）
\v 垂直制表符（\u000B）
\' 单引号（\u0027）
\" 双引号（\u0022）  
```   

### base64转码  
bota()  -字符串或二进制值转为Base64编码   
atob()  -Base64格式的编码转回原来的格式  
```  
var string = 'Hello World!';
btoa(string) // "SGVsbG8gV29ybGQh"
atob('SGVsbG8gV29ybGQh') // "Hello World!"  
```   
***   
***   
## ***对象***  

引用数据类型（对象、函数、数组）可以任意扩展属性。  
js规定，如果行首是大括号一律解释为语句（即代码块），如果需要解释成表达式（即对象）   
需要在大括号前加上圆括号。  
```  
({obj: 123})  
eval('{foo: 123}') // 123,解释为代码块
eval('({foo: 123})') // {foo: 123}，解释为语句
```   


*关于delete命令*：   
> 用于删除对象的属性且删除后返回true，删除一个不存在的属性不报错而且还会返回true；   
如果对象的enumberable属性设置为false（Object.defineProperty），则该属性  
不能删除；delete只能删除对象本身的属性，不能删除继承来的属性；最后，delete不可删除通过var等   
声明来的变量，只能删除属性。    


*关于for in循环*：   
1. 遍历所有可枚举的属性，即configurable为true的属性  
2. 会遍历继承来的属性   

***   
***   
## ***数组***   
> 1、length属性   
将数组清空的方法之一就是将length值变为0.   
因为数组是对象的一种（引用数据类型），可以扩展属性但不会影响length  
```   
var a = [];

a['p'] = 'abc';
a.length // 0

a[2.1] = 'abc';
a.length // 0   
```   

### 类数组对象（长得很像数组，也具有length属性但不可使用数组的方法）  
```   
var obj = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};

obj[0] // 'a'
obj[2] // 'c'
obj.length // 3
obj.push('d') // TypeError: obj.push is not a function   
```   

典型的类数组对象有arguments参数、DOM元素集以及字符串：
```   
// arguments对象
function args() { return arguments }
var arrayLike = args('a', 'b');
arrayLike[0] // 'a'
arrayLike.length // 2
arrayLike instanceof Array // false

// DOM元素集
var elts = document.getElementsByTagName('h3');
elts.length // 3
elts instanceof Array // false

// 字符串
'abc'[1] // 'b'
'abc'.length // 3
'abc' instanceof Array // false   
```   

*可以使用数组的slice方法将类数组对象变为真正的数组*
```   
Array.prototype.slice.call(arraylike) 或者 Array.from(arraylike) ES6实现   
```   
> 2、in 运算符  
用来判断某个键名是否存在。  
```  
var arr = [ 'a', 'b', 'c' ];
2 in arr  // true
'2' in arr // true
4 in arr // false   
```   
**如果数组的某个位置是空位则返回false**  
```  
var arr = [];
arr[100] = 'a';

100 in arr // true
1 in arr // false,数组只有一个成员arr[100],所以其他的均是false  
```   
> 3、数组空位   
使用delete删除数组成员会形成空位但不会影响length属性。
```   
var a = [1, 2, 3];
delete a[1];

a[1] // undefined
a.length // 3    

```   

注：**空位不同于undefined，使用Object.keys、for in以及for each等方法   
遍历数组时空位会被跳过但undefined不会**   
```   
/*遍历空位时*/
var a = [, , ,];

a.forEach(function (x, i) {
  console.log(i + '. ' + x);
})
// 不产生任何输出  

/*遍历undefined时*/
var a = [undefined, undefined, undefined];

a.forEach(function (x, i) {
  console.log(i + '. ' + x);
});
// 0. undefined
// 1. undefined
// 2. undefined   
```   

***   
***  
## 函数  

函数调用自身就是**递归**。   
由于变量提升，在函数声明之前可以调用，但是通过采用赋值语句定义的函数会报错:   
```  
f();
var f = function (){};
// TypeError: undefined is not a function  
```    

函数的toString()方法返回函数的源码：  
```  
function f() {
  a();
  b();
  c();
}

f.toString()
// function f() {
//  a();
//  b();
//  c();
// }  
```   
 
