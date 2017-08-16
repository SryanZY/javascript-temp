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

**Math常用函数**  
math.pow(2, 53)-2的53次幂
