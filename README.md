# js-review
复习了js，归纳了一些js知识


## 消除数组里重复的元素 ##

	 var arr1 = [2,2,3,4,5,4,6,8,4,9];
	 var arr2 = [];
	 for(var i=0;i<arr1.length;i++){
	 	if(arr2.indexOf(arr1[i])<0){
	 		arr2.push(arr1[i])
	 	}
	 }
	 console.log(arr2)


## 隔行变色 ##

	 var arrLi = document.getElementsByTagName('li');
	 for(var i=0;i<arrLi.length;i++){
	 	if(i%2==0){
	 		arrLi[i].onmouseover = function(){
	 			this.style.background = "green"
	 		}				
	 	}
	 }

## 时间转换 ##

	 var a= 123;
	 alert(parseInt(a/60)+"hour"+a%60+"minutes")

## arguments 相当用于数组，可循环求和,在不知道个数以及数据类型的情况下可用 ##

	 function sum(){
	 	var result = 0;
	 	for(var i=0;i<arguments.length;i++){
	 		result +=arguments[i];
	 	}
	 		return result;
	 }
	 alert(sum(2,3,4,3,5,7,4,5))


##  再补充arguments ##

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

## 封装获取标签样式 ##

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

## 数组的length 可获取也可设置 ##

	 var arr= [2,3,4,5,9]
	 arr.length=0;
	 console.log(arr)

	// var arr =[2,3,4,5,6,7,8];
	// arr.splice(2,4);   splice(起点，长度)  删除
	// 插入 splice(起点，长度，元素)
	// arr.splice(2,4,9,0,1) 
	// alert(arr.join("*") )

## //综合 先消除重复项，再进行排序 ##

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

## 插入新元素且按照顺序排序 ##

	 var arr=[2,4,6,99,32,123,18];
	 //arr.push(36)   push一个数
	 arr.splice(2,0,1,88,77)
	  //插入n个数
	 console.log(arr)
	 alert(arr.sort(function(n1,n2){
	 	return n1-n2
	 }))

## 数组的随机排序 ##

	var arr=[1,2,40,3,4,80,5,6,7,8,10,20]
	arr.sort(function(){
		return Math.random()-0.5
	})
	console.log(arr)

## 颠倒数组元素位置 ##

	var arr=[3,6,20，1,8,33,5]
	arr.reverse()
	console.log(arr)

## 字符串有长度且可获取其索引 ##

	 var str = "26383922"
	 console.log(str.length)	
	 alert(str[2])
	 alert(str.charAt(2))    //做IE兼容


## 复制数组 ##

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




##  循环 ##

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



##  map 对象：和json相似，也是一种key-value形式，Map对象为了和for of循环配合而生的 ##
	
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


## 箭头函数 ##

	// 注意：this问题，this指向了window
			 arguments,在箭头函数里不能使用



## 面向对象 ##
 
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


## DOM节点，把原生js和jquery进行比较 ##

原生js方法：

	childNodes  //获取某元素的全部子节点


childNodes 获取的是所有子节点，其中也包括文本节点和元素节点。
奇怪的是它在IE6-8使用是不存在问题，但是在其他浏览器里会有问题，因此
我们会用【nodeType】来判断节点类型，举个例子

	var oUl=document.getElementById("ul1");
	for(var i=0;i<oUl.childNodes.length;i++){

	if(oUl.childNodes[i].nodeType ==1){
      	 oUl.childNodes[i].style.background="green"
		}
	}

<ul id="ul1">        
	<li>第一个元素节点</li>
	<li>第二个元素节点</li>
	<li>第三个元素节点</li>
</ul>

我们需要知道如果 nodeType ==3,它表示的是文本节点，而文本节点是无法加样式的；
如果nodeType ==1，则是元素节点，而我们也只要元素节点，所以在循环里加判断，就不会存在兼容问题。

当然，我们可以使用【children】,它仅仅获取的是元素节点，在高版本浏览器或IE浏览器下都可以使用，所以上述例子中直接把childNode改成children就可以了，也不需要给其加判断，所以建议直接用children。

	parentNode; //获取某元素的父节点
	写法为：子元素.parerntNode;

	offsetParent   //这个是获取定位的父级节点。
...................................................

	nextSibling; //获取某元素的下一个兄弟节点，这个一般在IE下可执行，为了兼容谷歌，写法为：nextElementSibling

 	var Oli = document.getElementsByTagName("li")
	for(var i=0;i<Oli.length;i++){
		Oli[i].onclick = function(){
			if(this.nextElementSibling){
				// 为了兼容谷歌
				alert(this.nextElementSibling.innerText)   
				  }else{
				  	alert(this.nextSibling.innerText)
				  }
				}
			}

...................................................

	previousSibling; //获取某元素的上一个兄弟节点，
...................................................


	firstChild; //获取某元素的第一个子节点，这个如果直接使用也存在兼容问题，它适用于IE6--8，所以一般在高版本浏览器下使用的是：firstElementChild。

	var oUl=document.getElementById("ul1");

	if(oUl.firstElementChild){
    	// 适配高版本浏览器 
         oUl.firstElementChild.style.background="red"  
    	}else{
    	// IE6-8适用
			oUl.firstChild.style.background="red"
    }
	
...................................................


	lastChild; //获取某元素的最后一个子节点
	同理肯定还有lastChild/lastElementChild,用法一样。

jquery写法

	parent(expr) //找父亲节点，可以传入expr进行过滤，比如$("span").parent()或者$("span").parent(".class")
	
	jQuery.parents(expr) //类似于jQuery.parents(expr),但是是查找所有祖先元素，不限于父元素
	
	jQuery.children(expr) //返回所有子节点，这个方法只会返回直接的孩子节点，不会返回所有的子孙节点
	
	jQuery.contents() //返回下面的所有内容，包括节点和文本。这个方法和children()的区别就在于，包括空白文本，也会被作为一个jQuery对象返回，children()则只会返回节点
	
	jQuery.prev() //返回上一个兄弟节点，不是所有的兄弟节点
	
	jQuery.prevAll() //返回所有之前的兄弟节点
	
	jQuery.next() //返回下一个兄弟节点，不是所有的兄弟节点
	
	jQuery.nextAll() //返回所有之后的兄弟节点
	
	jQuery.siblings() //返回兄弟姐妹节点，不分前后
	
	jQuery.find(expr)  //跟jQuery.filter(expr)完全不一样。jQuery.filter()是从初始的jQuery对象集合中筛选出一部分，而jQuery.find()的返回结果，不会有初始集合中的内容，比如$("p"),find("span"),是从p元素开始找,等同于$("p span").


## DOM元素查找（id/tagName/className） ##

//封装 

	<ul id="ul1">
		<li class="box"></li>
		<li></li>
		<li class="box"></li>
		<li class="box"></li>
		<li></li>
		<li></li>
	</ul>

	function getByClass(oParent,sClass){
		var result = [];
		var aEle = oParent.getElementsByTagName("*")   //元素无法确认，因此用*表示
		for(var i=0;i<aEle.length;i++){
			if(aEle[i].className ==sClass){
				result.push(aEle[i])
			}
		}
		return result
	}

	var oUl=document.getElementById("ul1");
	var aBox =getByClass(oUl,"box")
	for(var i=0;i<aBox.length;i++){
		aBox[i].style.background = "orange"
	}



## 创建、插入和删除元素 ##

	//创建节点并插入父级
	 var obtn = document.getElementById("btn");
	 var oul1 = document.getElementById("ul1");
	 obtn.onclick = function(){
	 	var aLi = document.createElement("li");
	 	aLi.innerHTML="hello"
	 	oul1.appendChild(aLi)
	 }

..................................................
	
	//插入元素  

	 var obtn = document.getElementById("btn");
	 var oul1 = document.getElementById("ul1");
	 var oinp = document.getElementById("inp");
	 obtn.onclick = function(){
	 	var aLi = document.createElement("li");     //创建元素
	 	var oLi = document.getElementsByTagName("li")    //获取所有li元素
	 	aLi.innerHTML = oinp.value;
	 	// oul1.insertBefore(aLi,oLi[0])       //兼容问题
	 	if(oLi.length>0){
			oul1.insertBefore(aLi,oLi[0])        //父级.insertBefore(子级，要插入的位置)
	 	}else{
			oul1.appendChild(aLi)
	 	}
	 }

..................................................


	//删除元素    父级.removeChild(子节点)
	
	<ul id="oul2">
		<li>bbbbbb<a href="javascript:;">删除</a></li>
		<li>cccccc<a href="javascript:;">删除</a></li>
		<li>dddddd<a href="javascript:;">删除</a></li>
		<li>eeeeee<a href="javascript:;">删除</a></li>
		<li>ffffff<a href="javascript:;">删除</a></li>
	</ul>

	 var oul2 = document.getElementById("oul2");
	 var del = document.getElementsByTagName("a");
	 for(var i=0;i<del.length;i++){
	 	del[i].onclick = function(){
	 		oul2.removeChild(this.parentNode)
	 	}
	}

..................................................

	//文档碎片

	// 文档碎片可以提高DOM操作性能，一般指的是低版本浏览器
	// document.createDocumentFragment()



## 表格应用 ##

	获取：
		var otab = document.getElementById("tab1");
	
		 var name = otab.getElementsByTagName("tbody")[0].getElementsByTagName("tr")[2].getElementsByTagName("td")[1].innerHTML;
		 alert(name)

		//简写
		var name = otab.tBodies[0].rows[2].cells[1].innerHTML;
		alert(name)



..................................................

	添加行
		 var oinp1 = document.getElementById("inp1");
		 var oinp2 = document.getElementById("inp2");
		 var obtn1 = document.getElementById("btn1");
		 obtn1.onclick = function(){
		 	var otr = document.createElement("tr");
		
		 	var otd = document.createElement("td");
		 	otd.innerHTML = otab.tBodies[0].rows.length+1;
		 	otr.appendChild(otd);   //序号
		
		 	var otd = document.createElement("td"); 
		 	otd.innerHTML = oinp1.value;
		 	otr.appendChild(otd)
		
		 var otd = document.createElement("td");
		 otd.innerHTML = oinp2.value;
		 otr.appendChild(otd);
		 otab.tBodies[0].appendChild(otr)	
		 }

...............................................................

	忽略大小写、模糊搜素

		var oipt = document.getElementById("ipt");
		var obtn = document.getElementById("btn");
		obtn.onclick = function(){
		for(var i=0;i<otab.tBodies[0].rows.length;i++){
			var Txt = otab.tBodies[0].rows[i].cells[1].innerHTML;
			// if(Txt.toLowerCase()== oipt.value.toLowerCase())  //大小写
			if(Txt.search(oipt.value)!=-1)      //模糊
			{
				otab.tBodies[0].rows[i].style.background = "red"
			}else{
				otab.tBodies[0].rows[i].style.background = ""
			}
		}
	}

	备注：search();返回的是字符串的位置，如果没有找到则返回-1；
	var str ="abiss"
	alert(atr.search(b))     //返回1


...............................................................

	多关键字搜索
		var str = "abcdef"
		var arr = str.split(" ");   //以空格分割字符串，返回数组
		console.log(arr)   
	
		var oipt = document.getElementById("ipt");
		var obtn = document.getElementById("btn");
		obtn.onclick = function(){
		for(var i=0;i<otab.tBodies[0].rows.length;i++){
			var Txt = otab.tBodies[0].rows[i].cells[1].innerHTML;
			var Val = oipt.value;
			var arr = Val.split(" ")
			otab.tBodies[0].rows[i].style.background = " "
			for(var j=0;j<arr.length;j++){
				if(Txt.search(arr[j])!=-1)	
				{
					otab.tBodies[0].rows[i].style.background = "red"
				}		
			}
		}
	}


