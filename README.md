# javascript-temp
js学习笔记
  
## 数据类型  
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

*math.pow(2, 53)*-2的53次幂   

*Number.MAX_VALUE-1.7976931348623157e+308*   

*Number.MIN_VALUE-5e-324*  
   
在ES5中+0等于-0，NaN！=NaN，在ES6中+0！=-0， NaN = NaN   
```  
Object.is(+0, -0) // false  
Object.is(NaN, NaN) // true   
```   
***  

#### 关于NaN和infinite   
```   
typeof NaN  // Number  
```   
NaN与任何数运算（包括本身）都是NaN，可以通过isNaN来判断  
```   
isNaN(NaN)  // true  
```   
**NaN只对数值有效，输入其他的会先转换为数字，因此返回true的不一定就是NaN，可以通过函数判断**   
```  
function tmpIsNaN(val) {
    return typeof(val) === 'number' && isNaN(val);
}  
```   
