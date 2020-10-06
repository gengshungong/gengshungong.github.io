---
layout: post
title:  "react prop-types的使用"
date:   2019-08-14
categories: 
- react
tag:
- react 
--- 

##### 1首先需要通过在终端npm install prop-types或yarn add prop-types安装一个叫prop-types的第三方包

##### 2然后通过下面的写法对某一个组件中的变量进行类型检测：

```js
componentname.propTypes = {
    name1:'变量类型',
    name2:'变量类型'
}
```

> 例如： (有意写错，让其检测)
```js
import React from 'react'
import PropTypes from 'prop-types';
class Son extends React.Component{
   render(){
        return (<div style ={{padding:30}}>
                      {this.props.number}
                      <br/>
                      {this.props.array}
                      <br/>
                      {this.props.boolean.toString()}
                    </div>)
                  }
}
Son.propTypes = {
        number:PropTypes.number,
        array:PropTypes.array,
        boolean:PropTypes.bool
}
class Father extends React.Component{
    render(){
         return (<Son
                       number = {'1'}
                       array = {'[1,2,3]'}
                       boolean = {'true'}
                        />)
                  }
}
```

* propTypes能用来检测全部数据类型的变量，包括基本类型的的字符串，布尔值，数字，以及引用类型的对象，数组，函数，甚至还有ES6新增的符号类型
```js
Son.propTypes = {
     optionalArray: PropTypes.array,//检测数组类型
     optionalBool: PropTypes.bool,//检测布尔类型
     optionalFunc: PropTypes.func,//检测函数（Function类型）
     optionalNumber: PropTypes.number,//检测数字
     optionalObject: PropTypes.object,//检测对象
     optionalString: PropTypes.string,//检测字符串
     optionalSymbol: PropTypes.symbol,//ES6新增的symbol类型
}
```

  `【注意】下面这些是从官方英文文档里引用过来的，你大概能够注意到，五种基本类型中的不确定和空并不在此列，propTypes类型检测的缺憾之一是，对于不确定的和无效的值，它无法捕捉错误`

* 把上述实例中的父组件传递给子组件修改一下，改成：
```js
class Father extends React.Component{
    render(){
       return (<Son
                 number = {null}
                 array = {null}
                 boolean = {null}
                />)
             }
}
```
> 结果是输出台不报任何错误，（当然你改成未定义也是同样效果）。


##### 通过oneOfType实现多选择检测-可规定多个检测通过的数据类型
> PropTypes里的oneOfType方法可以做到这一点，oneOfType方法接收参数的是一个数组，数组元素是你希望检测通过的数据类型。

```js
import React from 'react'
import PropTypes from 'prop-types';
class Son extends React.Component{
render(){
return (<div style ={{padding:30}}>
{this.props.number}
</div>)
}
}
Son.propTypes = {
number:PropTypes.oneOfType(
[PropTypes.string,PropTypes.number]
)
}
class Father extends React.Component{
render(){
//分别渲染数字的11和字符串的11
return (<div>
<Son number = {'字符串11'}/>
<Son number = {11}/>
</div>)
}
}
```
> 这时候，因为在类型检测中，号码属性的规定类型包括字符串和数字两种，所以此时控制台无报错,当然，如果你改为number = {数组或其他类型的变量}，那么这时就会报错了


##### 通过oneOf实现多选择检测-可规定多个检测通过的变量的值
```js
Son.propTypes = {
    number:PropTypes.oneOf(
          [12,13]
      )
}
```
> 此时会报错


##### arrayOf，objectOf实现多重嵌套检测
> 如果我们检测的是基本类型的变量，那么这自然是很简单的，但当我们要检测的是一个引用类型的变量呢？当我们除了检测这个变量是否符合规定的引用类型外（对象/阵列），还想要进一步检测对象中的属性变量或阵列中数组元素的数据类型时，单靠上面的方法已经不能满足要求了。这时候就要用到PropTypes的arrayOf，objectOf方法。
- arrayOf接收一个参数，这个参数是规定的数组元素的数据类型.objectOf接收的参数则是属性的数据类型

- 对上述例子做修改：
```js
import React from 'react'
import PropTypes from 'prop-types';
class Son extends React.Component{
    render(){
       return (<div style ={{padding:30}}>
                {this.props.array}
               </div>)
           }
}
Son.propTypes = {
     array:PropTypes.arrayOf(PropTypes.number)
}
class Father extends React.Component{
    render(){
       return (<div>
                 <Son array = {[1,2,3,4]}/>
               </div>)
}
}
```
> 正常渲染，然后我们把<Son array = {[1,2,3,4]} />改为<Son array = {['1'，'2'，'3'，'4']} /> ，报错
```js
【注意】虽然报错但是这并不会影响程序的正常运行（譬如上面我们看到渲染仍然是正常的），因为本质上说类型检测报的是非致命性错误的警告而不是致命性错误的错误（区别在于是否影响了正常运行）。对objectOf也是同样的做法
```


> objectOf有一个缺陷,就是它内部的属性的数据类型被强行规定为一种，但通常一个对象里应该是有多种不同类型的属性了，那么这时候objectOf就不符合要求了，我们应该使用形状方法，其用法：
```js
PropTypes.shape({
   属性1：类型1，
   属性2：类型2，
  //...
})
```
###### 举个例子
```js
import React from 'react'
import PropTypes from 'prop-types';
class Son extends React.Component{
     render(){
        return (<div style ={{padding:30}}>
                  {'我的名字叫' + this.props.object.name}
                  <br/>
                  {'我的年龄是' + this.props.object.age}
                 </div>)
             }
}
Son.propTypes = {
     object:PropTypes.shape({
     name:PropTypes.string,
     age:PropTypes.number
      })
}
class Father extends React.Component{
    render(){
       return (<div>
                  <Son object = {{name:'彭湖湾',age:20}}/>
               </div>)
     }
}
```
`无报错，把<Son object = {{name：'彭湖湾'，年龄：20}} />改成<Son object = {{name：'彭湖湾'，年龄：'20'}} /> ，然后就能报错了`


##### 通过isRequired检测道具中某个必要的属性（如果该属性不存在就报错）
`我们在对某个变量进行类型检测时，我们不仅要求它符合预期的类型，同时也要求它是必须写入的，这时候就要用到isRequired。`
```js
Son.propTypes = {
          number:PropTypes.number
}
```
`这段代码的作用是当你中写入号码属性且号码属性类型错误时给予报错提示，可如果你压根就没有写入号码属性呢？没错，什么错误都不会报。这就是使用isRequired的必要性`

> 【注意】上述的写法是数量：PropTypes.number.isRequired，这要求数是数字类型，但如果你不想控制数的类型而仅仅是想控制它的必要性呢？难道写成号：isRequired或number：PropTypes.isRequired？ 这个时候PropTypes.any就登场啦！它代表了该变量可取任何一种数据类型，所以你可以写成这样--number：PropTypes.any.isRequired

##### 应对更复杂的类型检测 - 将PropTypes的属性值写成函数
```js
Son.propTypes = {
      prop:function(props,propName,componentName){
          if(/*判断条件*/){
               return new Error(/*错误的参数*/)
           }
    }
}
```

> 在属性prop的类型检测中，属性值是一个函数，在这里props是包含prop的props对象，propName是prop的属性名，componentName是props所在的组件名称，函数的返回值是一个Error对象
```js
import React from 'react'
import PropTypes from 'prop-types';
class Son extends React.Component{
         render(){
               return (<div style ={{padding:30}}>
                        {this.props.email}
                       </div>)
                  }
}
Son.propTypes = {
     email:function(props,propName,componentName){
            if(!/^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+(.[a-zA-Z0-9_-])+/.test(props[propName])){
                  return new Error('组件' + componentName+ '里的属性' + propName + '不符合邮箱的格式');
                         }
                }
}
class Father extends React.Component{
        render(){
             return (<div>
                        <Son email = {2314838004}/>
                     </div>)
                }
}
```

##### ES7下类型检测的新写法：
```js
class Son extends React.Component{
static propTypes = {
       //..类型检测
}
render(){
   return (/* 渲染*/)
     }
}
```

##### props-types的独立与react.PropTypes的弃用
`在上面我是利用props-types这个独立的第三方库来进行类型检测的，但在不久前（react V15.5以前），它使用的是react内置的类型检测，而不是第三方库（也就是说我们现在的prop-types是当初以react内置的PropTypes对象为基础分离出来的）`
> 所以说在你也可以这样进行类型检测，虽然并不推荐（为了保持向下兼容这在最新版本的react上仍然是可用的）
```js
Son.propTypes = {
    number:React.PropTypes.number
}
```











