### 解构

>  destructuring ,按照规则从数组或者对象中取值,并对变量进行赋值

#### 解构对象用于变量声明

```javascript
let userInfo = {
  	name : '张三',
  	age : '28'
};
let {name ,age} = userInfo || {};//userInfo 可能为undefined
console.log(name); //张三
console.log(age); //28
```

#### 解构对象赋值给名称不同得变量

```javascript
let userInfo = {
  	name : '张三',
  	age : '28'
};
let {name : names} = userInfo;
console.log(names);
```

#### 解构对象变量默认值

```javascript
let userInfo = {
  	name : '张三',
  	age : '28'
};
let {name : names,age,address='aaa'} = userInfo || {};
console.log(names);
console.log(address);
```

#### 嵌套对象赋值

```javascript
let userInfo = {
  	name : '张三',
  	age : '28',
  	basicInfo:{
   	 test:{
      	desc:'测试'
     },
     level : 5
  }
};

let { basicInfo:{test}} = userInfo;
console.log(test);//{desc: "测试"}
```

#### 数组解构

> 数组解构是根据坐标定位进行赋值得 

```javascript
let types = ['type1' ,'type2' ,'type3'];
let [a ,b] = types; //[]中为变量列表
console.log(a);
console.log(b);
```

#### 使用占位符获取特定位置得赋值

```javascript
let types1 = ['type1' ,'type2' ,'type3'];
let [ ,c] = types1; //[]中 ,为占位
console.log(b); //type2
```

#### 嵌套数组解构

```javascript
let types3 = ['type1',['type11','type22'],'type2'];
let [test1,test2] = types3;
console.log(test1);//type1
console.log(test2); // ["type11", "type22"]
```

#### 剩余元素使用展开表达式赋值

> 展开赋值必须是需要赋值得最后一个元素,不然会报错

```javascript
let types44 = ['type1','type2','type3','typy4'];
let [test3,...test4] = types44;
console.log(test4); //["type2", "type3", "typy4"]
//实现数组得copy
let [...test5] = types44;
console.log(test5);// ["type1", "type2", "type3", "typy4"]
```

#### **对象和数组的混合解构**

```javascript
let {
  basicInfo:{test8},
  card5:[cardIndex]
} = userInfo1;

console.log(test8); //{desc: "测试"}
console.log(cardIndex); //card1
```

#### 解构函数参数

```javascript
function testFunction(parm1,parm2,{parm3,parm4}){
  console.log(1111);
}
等价于
let options = {parm3:12,parm4:13};
function testFunction1(parm1,parm2,option){
  let {parm3,parm4} = option;
  console.log(1111);
}
testFunction1(1,2,options);
```

#### 考虑使用解构参数

```javascript
let options1 = {parm3:12,parm4:13};
function testFunction2(parm1,parm2,{parm3 = options1.parm3,parm4 = options1.parm4} = options1){
  console.log(1111);
}
testFunction2(1,2);
```



