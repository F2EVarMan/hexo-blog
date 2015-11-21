title: JS数组
date: 2015-03-23 15:46:59
tags:
- JavaScript
- 数组
categories:
- JavaScript
---
###JavaScript 数组
数组是值的有序集合,每个值叫做元素,每个元素在数组中都有数字位置编号,也就是索引。
js中的数组是弱类型的,数组中可以含有不同类型的元素,数组元素甚至可以是对象或其他数组。
var arr=[1,true,null,undefined,{x:1},[1,2,3]]
创建数组   
  字面量创建
```{bash}     
      var BAT=['Alibaba','Tenecnt','Baidu']
      var students=[{name:'Bosn',age:27},{name:'Nunnly',age:3}]
     new Array //构造器创建数组
     var arr= new Array();
     var arrWithLength = new Array(100); // undefined 
     var arrLikesLiteral=new Array(true,false,null,1,2)
```
  数组元素读写
```{bash}
     var arr=[1,2,3,4,5,];
     arr[1]; // 2
     arr.length;// 5
     arr[5]=6;
     arr.length; // 6
     delete arr[0];
     arr[0];// undedfined
```
数组元素增删
```{bash}
     var arr=[];
     arr[0]=1;
     arr[1]=2;
     arr.push(3);
     arr; // [1,2,3]
     arr[arr.length]=4;
     arr; // 1,2,3,4
     arr.unshift(0);
     arr;// [0,1,2,3,4];
     delete arr[2];
     arr;//[0,1,undefined,3,4]
     arr.length;//5
     2 in arr;//false

     arr.length -=1;
     arr;//[0,1,undefined,3],4 is removed

     arr.pop();//3 returned by pop
     arr;//[0,1,undefined],3 is removed

     arr.shift(); //0 returned by shift
     arr;//[1,undefined]
```
数组迭代
```{bash}
     var i=0,n=10;
     var arr=[1,2,3,4,5];
     for(;i<n;i++){
          console.log(arr[i])
     }
     for(i in arr){
     console.log(arr[i])
     }

     Array.prototype.x='inherited';

     for(i in arr){
        console.log(arr[i]);// 1,2,3,4,5,inherited
      }

      for(i in arr){
        if(arr.hasOwnProperty(i)){
            console.log(arr[i]);//1,2,3,4,5
          }
        }
```
#####二维数组
```{bash}
  var arr=[[0,1],[2,3],[4,5]];
  var i=0,j=0;
  var row;
  for(;i<arr.length;i++){
    row=arr[i];
    console.log('row'+i);
    for(j=0;i<row.length;j++){
      console.log(row[j]);
      }
    }
```
##### 稀疏数组
   并不含有从0开始的连续索引.一般Length属性值比实际元素个数大
```{bash}
  var arr1=[undefined];
  var arr2=new Array(1);
  0 in arr1;//true
  0 in arr 2;//false
  arr1.length=100;
  arr1[99]=123;
  99 in arr1;//true
  98 in arr1;//false

  var arr=[,,];
  0 in arr; //false
```
####数组方法
原生方法 都在 Array.prototype
```{bash}
{} => Object.prototype 
[] => Array.prototype 

Array.prototype.join
Array.prototype.reverse
Array.prototype.sort
Array.prototype.concat
Array.prototype.slice
Array.prototype.splice
Array.prototype.forEach
Array.prototype.map
Array.prototype.splice
Array.prototype.filter
Array.prototype.some
Array.prototype.reduce/reduceRight
Array.prototype.indexOf/lastIndexOf
Array.prototype.isArray

```
join将数组转化成字符串,传入参数 可以当作分隔符
```{bash}
     var arr=[1,2,3];
     arr.join();// '1,2,3,'
     arr.join('_');// '1_2_3'
```

reverse 将数组逆序
```{bash}
 var arr=[1,2,3];
 arr.reverse();//[3,2,1]
 arr;//[3,2,1] 原数组被修改
```
sort 排序 
```{bash}
  var arr=["a","d",'c','b'];
  arr.sort();//['a','b','c','d']

  arr=[13,24,51,3];
  arr.sort();//[13,24,3,51]
  arr;//[13,24,3,51] 原数组被修改

  arr.sort(function(a,b){
     return a-b;
  })//[3,13,24,51]
```
concat 合并数组
```{bash}
var arr=[1,2,3];
arr.concat(4,5);//[1,2,3,4,5]
arr;//[1,2,3] 原数组未被修改
arr.concat([10,11],13);//[1,2,3,10,11,13]
arr.concat([1,[2,3]]);//[1,2,3,1,[2,3]]
```
slice  返回部分数组
```{bash}
  var arr=[1,2,3,4,5];
  arr.slice(1,3);//[2,3]
  arr.slice(1);//[2,3,4,5]
  arr.slice(1,-1);//[2,3,4]
  arr.slice(-4,-3);//[2]
```
splice 数组拼接
```{bash}
  var arr=[1,2,3,4,5];
  arr.splice(2);//returns[3,4,5]
  arr;//[1,2]; 原数组被修改

  arr=[1,2,3,4,5];
  arr.splice(2,2);//retirms [3,4]
  arr;//[1,2,5];

  arr=[1,2,3,4,5];
  arr.splice(1,1,'a','b');//retirms [2]
  arr;//[1,'a','b',3,4,5];
```
forEach  数组遍历(ES5)
```{bash}
var arr=[1,2,3,4,5];
arr.forEach(function(x,index,a){
  console.log(x +'|'+index+'|'+(a===arr))
})
//1|0|true
//2|1|true
//3|2|true
//4|3|true
//5|4|true
```
map 数组映射(ES5)
```{bash}
var arr=[1,2,3];
arr.map(function(x){
  return x+10
});//[11,12,13]
arr;//[1,2,3]
```
filter 数组过滤(ES5)
```{bash}
var arr=[1,2,3,4,5,6,7,8,9,10];
arr.filter(function(x,index){
  return index % 3=== 0 || x>=8;
})//return [1,4,7,8,9,10]
arr;//[1,2,3,4,5,6,7,8,9,10]
```

every / some  数组判断(ES5)
every 表示数组中每个元素都符合条件,some 表示只要任意一个元素符合
```{bash}
var arr=[1,2,3,4,5];
arr.every(function(x){
  return x<10;
})//true
arr.every(function(x){
  return x<3;
})//false

var arr=[1,2,3,4,5];
arr.some(function(x){
  return x ===3;
})//true
arr.some(function(x){
  return x===100;
})//false

```
reduce / reduceRight   数组中的元素两两进行操作   reduceRight是从右到左
```{bash}
var arr=[3,9,6]
max=arr.reduceRight(function(x,y){
  console.log(x+'|'+y);
  return x>y?x:y
});
// 6|9
// 9|3
max;//9
```

indexOf / lastIndexOf 数组检索 (ES5)
```{bash}
var arr=[1,2,3,2,1]
arr.indexOf(2);//1
arr.indexOf(99);//-1
arr.indexOf(1,1);//4
arr.indexOf(1,-3);//4
arr.lastIndexOf(2);//3
```
Array.isArray(ES5) 判断是否为数组

```{bash}
Array.isArray([]);//true;

[] instanceof Array;//true
({}).toString.apply([])==='[object Array]';//true
[].constructor === Array;//true
```
数组本身也是对象 
数组和对象的相同点：
     都可以继承，数组是对象，对象不一定是数组，都可以当作对象添加删除属性
不同点：
     数组自动更新Length,按索引访问数组常常比访问一般对象属性明显迅速.数组对象 继承了Array.prototype上的大量数组操作方法
字符串和数组   字符串是一种类数组的东西.
```{bash}
var str='hello world';
str.charAt(0); //"h"
str[1];//e

Array.prototype.join.call(str,'_');
//"h_e_l_l_o__w_o_r_l_d"
```
