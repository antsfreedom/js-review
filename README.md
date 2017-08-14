# js-review
复习了js，归纳了一些js知识


消除数组里重复的元素

	 var arr1 = [2,2,3,4,5,4,6,8,4,9];
	 var arr2 = [];
	 for(var i=0;i<arr1.length;i++){
	 	if(arr2.indexOf(arr1[i])<0){
	 		arr2.push(arr1[i])
	 	}
	 }
	 console.log(arr2)


隔行变色

	 var arrLi = document.getElementsByTagName('li');
	 for(var i=0;i<arrLi.length;i++){
	 	if(i%2==0){
	 		arrLi[i].onmouseover = function(){
	 			this.style.background = "green"
	 		}				
	 	}
	 }

时间转换

	 var a= 123;
	 alert(parseInt(a/60)+"hour"+a%60+"minutes")

arguments 相当用于数组，可循环求和,在不知道个数以及数据类型的情况下可用

	 function sum(){
	 	var result = 0;
	 	for(var i=0;i<arguments.length;i++){
	 		result +=arguments[i];
	 	}
	 		return result;
	 }
	 alert(sum(2,3,4,3,5,7,4,5))


 再补充arguments

	 function show(){
	 	// arguments.push(5)   //报错
	 	console.log(arguments)   //这里的arguments是类数组，可循环，但无法添加新的数组元素
	 }
	 show(2,3,4,1)
	
	 function show(...args){
	 	args.push(5)
	 	console.log(args)    //这个是可以添加新数组元素，是真正的数组
	 }
	 show(2,6,4,8)

封装获取标签样式

	 function getStyle (obj,style){
	 	if(obj.currentStyle){
	 		return obj.currentStyle[style]
	 	}else{
	 		return getComputedStyle(obj,false)[style];
	 	}		
	 }

	// var obox = document.getElementById("box");
	// alert(getComputedStyle(obox,false).width);//兼容火狐 chorme
	// alert(obox.currentStyle.width)  //兼容IE
	// alert(obox.style.width)   //针对行间样式可用此方式直接获取
	// alert(getStyle(obox,"width"))

数组的length 可获取也可设置

	 var arr= [2,3,4,5,9]
	 arr.length=0;
	 console.log(arr)

	// var arr =[2,3,4,5,6,7,8];
	// arr.splice(2,4);   splice(起点，长度)  删除
	// 插入 splice(起点，长度，元素)
	// arr.splice(2,4,9,0,1) 
	// alert(arr.join("*") )

//综合 先消除重复项，再进行排序

	 var arr=[2,7,3,7,3,10,23,99,121,23];
	 var arr1=[];
	 for(var i=0;i<arr.length;i++){
	 	if(arr1.indexOf(arr[i])<0){
	 		arr1.push(arr[i])
	 	}
	 }
	 arr1.sort(function(n1,n2){
	 	return n1-n2
	 })
	 console.log(arr1)

插入新元素且按照顺序排序

	 var arr=[2,4,6,99,32,123,18];
	 //arr.push(36)   push一个数
	 arr.splice(2,0,1,88,77)
	  //插入n个数
	 console.log(arr)
	 alert(arr.sort(function(n1,n2){
	 	return n1-n2
	 }))

字符串有长度且可获取其索引

	 var str = "26383922"
	 console.log(str.length)	
	 alert(str[2])
	 alert(str.charAt(2))    //做IE兼容


复制数组

	1.循环，可以复制数组

	2. Array.from(arr1)

	3. [...arr1]

	 var arr1 = [1,2,3,4];

	 var arr2 = Array.from(arr1)  //复制数组

	 var arr2 = [...arr1]       //复制数组

	for(var i=0;i<arr.length;i++){
		arr2[i]=arr1[i]
	}

	 arr1.pop()
	 console.log(arr1,arr2)




 循环

	  var arr=[2,3,5,8,11];
	  var sum = 0;
	//普通循环
	  for(var i=0;i<arr.length;i++){
	  	console.log(i)     //i代表索引
	  }

	//for in 
	  for(var i in arr){
	  	// console.log(i)   //i代表索引
	  	sum += arr[i]
	  }
	 console.log(sum)

	//for of
	 for(var i of arr){
	 	console.log(i)     
	//i代表 "值"  for of  可以循环数组，不能循环json ，其真正的目的为了循环map对象
	 }



 map 对象：和json相似，也是一种key-value形式，Map对象为了和for of循环配合而生的
	
	// var map = new Map();
	// 设置：
	// map.set(name,value);
	// 获取：
	// map.get(name)
	//删除：
	//map.delete(name)
	
	 var map = new Map();
	 map.set("a","23");
	 map.set("b","55");
	 alert(map.get("a"))

	 for(var [key,value] of map){
	 	console.log(key,value)
	 }
	
	 for(var key of map.keys()){     //只循环key
	 	console.log(key)
	 }


箭头函数

	// 注意：this问题，this指向了window
			 arguments,在箭头函数里不能使用



面向对象
 
	原先的写法：
	 function Person(name,age){
	 	this.name = name;
	 	this.age = age;
	 }
	 Person.prototype.showName = function(){
	 	return this.name;
	 };
	 Person.prototype.showAge = function(){
	 	return this.age;
	 };
	
	//原型继承
	 function worker(name,age){
	 	Person.apply(this,arguments)
	 }
	 worker.prototype = new Person();
	 var p1 = new Person("sheep",22);
		// var w1 = new Person("ccc",33)
	 console.log(p1.showName())
	 alert(w1.showName())


	ES6写法
	class Person{
		constructor(name,age){     //执行构造函数，生成完实例后，自己就执行
			 this.name = name;
			 this.age = age;
		}
		showName(){
			return this.name
		}
		showAge(){
			return this.age
			}
		}
	//继承
		class worker extends Person{
				//super(name.age)   //调用父级构造
		}

	// var p1 = new Person("sheep",101);
	// var p2 = new Person("cheaper",101);
	var w1 =new worker("eee",56)
	// alert(p2.name)
	// alert(p1.showName())
	alert(w1.showName())




