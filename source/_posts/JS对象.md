title: JS对象
date: 2015-03-11 17:27:04
tags:
- JavaScript
- 对象
categorise:
- JavaScript
---
###JavaScript对象
对象在js中非常重要,对象中包含一系列属性,这些属性是无序的,每个属性都有一个字符串key和对应的value.
js对象中的每个属性有很多属性标签 ,每个对象还有一个原形,一个class标签(表示对象是哪个种类)，一个extensible标签(说明对象是否允许 新增属性) 

#####创建对象
######对象字面量 
```{bash}
          var obj1={
               x : 1,
               y : 2,
               o : {
                    z : 3,
                    n : 4
               }
          }
 ```
######new构造器创建
```{bash}
function foo(){}
foo.prototype.z=3;
     
     var obj = new foo();
     obj.y=2;
     obj.x=1;
     
     obj.x;// 1
     obj.y;// 2
     obj.z// 3
     typeof obj.toString; // 'function'
     'z' in obj; // true
     obj.hasOwnProperty('z'); // false
```
当我们访问对象上的某一个属性的时候,如果这个对象上没有这个属性,他会通过原型链向上去查找一直找到Null.没找到就会返回undefined
如果是赋值的话会直接在当前对象赋值,而不会向原型链上去查找.

######Object.create
```{block}
     var obj = Object.create({x:1})
     obj.x // 1 
     typeof obj.toString // 'function'
```

######属性操作
######读写对象属性
```{bash}
        var obj ={x:1,y:2};
          obj.x;// 1
          obj['y']; //2
          obj.y=4;
          obj['x']=3;
//最好通过.的方式来读写单个属性
     var  obj={x1:1,x2:2};
     var i=1,n=2;
     for(;i<n;i++){
          console.log(obj['x'+i])
     }
     //可以通过for循环动态处理
```
属性删除
delete 删除属性  delete person.age
用var 定义的变量 不能被删除,函数也不可以被delete
属性 getter/ setter 方法
```{bash}
var man={
     name:'Bosn',
     weibo:'@Bosn',
     get age(){
          return new Date().getFullYear() - 1988;
     },
     set age(val){
          console.log('Age can\'t be set to ' + val)
     }
}
console.log(man.age) // 27
man.age=100;// age can't be set to 100
console.log(man.age);// 27
```
对象标签
     _proto_  一般对象会指向 Object.prorotype
    class标签
    可以通过 Object.prototype.toString;
     
     
