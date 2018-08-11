## apply与call
#### apply:可以劫持另一个对象的方法，集成另一个对象的属性。
```
Function.apply(obj,arg)

obj:代替Function类里的this.(obj可以用Function里的方法。Function里的this是obj)

arg:是数组，作为参数传给Function(arg-->arguments)

apply的参数是以数组的形式传入
```
###### apply的一个巧妙的用处,可以将一个数组默认的转换为一个参数列表([param1,param2,param3] 转换为 param1,param2,param3)
````
Math.max 可以实现得到数组中最大的一项:
因为Math.max 参数里面不支持Math.max([param1,param2]) 也就是数组
但是它支持Math.max(param1,param2,param3…)参数列表,所以可以根据刚才apply的那个特点来解决
var max=Math.max.apply(null,array),这样轻易的可以得到一个数组中最大的一项
(apply会将一个数组装换为一个参数接一个参数的传递给方法)

实现两个数组合并利用push
push方法没有提供push一个数组,但是它提供了push(param1,param,…paramN)
vararr1=new Array("1","2","3");
vararr2=new Array("4","5","6");
Array.prototype.push.apply(arr1,arr2);
arr1调用了push方法,参数是通过apply将数组装换为参数列表的集合.
````
###### 总结:一般在目标函数只需要n个参数列表,而不接收一个数组的形式([param1[,param2[,…[,paramN]]]])可以通过apply的方式巧妙地解决这个问题!




#### call:与apply一样，只是在参数不一样
```
Function.call(obj,[param1[,param2[,…[,paramN]]]])

obj:代替Function类里的this.(obj可以用Function里的方法。Function里的this是obj)

params：这个是一个参数列表

call的参数是以列表的形式传入
```

#### 实例
```
/*定义一个类*/
function person(name,age){
  this.name = name;
  this.age = age;
}

/*定义一个学生类*/
function stu(name,age,g){
  person.apply(this,arguments);
  this.g = g;
}

/*实例化*/
var s = new stu('xiaoming','10','一年级');
console.log(s.name+','+s.age+','+s.g)

分析: person.apply(this,arguments);

this:在创建对象new这个时候代表的是student

arguments:是一个数组,也就是[“xiaoming”,”10”,”一年级”];
也就是用student去执行person这个类里面的内容,在person这个类里存在this.name等之类的语句,这样就将属性创建到了student对象里面

```
