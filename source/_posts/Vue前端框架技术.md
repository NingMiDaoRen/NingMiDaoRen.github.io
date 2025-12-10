---
title: Vue前端框架技术
declare: true
date: 2021-08-31 16:28:16
tags: [前端]
categories: [Vue]
toc: true
---



<meta name="referrer" content="no-referrer" />  

<!--more-->

# Vue 前端框架技术

[TOC]

## Part 0 序章

### 0x01 什么是Vue

Vue (pronounced /vjuː/, like **view**) is a **progressive framework** for building user interfaces.

**What is progressive? 什么是渐进式框架 ?**

渐进式是指可以将Vue嵌入至一个完整的项目中，然后逐渐将原项目改为Vuejs项目。如之前使用Angular做的前端，然后我们需要改成Vue架构，那么就可以一部分一部分地替代原来的功能。不用重新开发。

### 0x02 特性

1. 解耦视图和数据
2. 前端路由
3. 状态管理
4. 虚拟DOM
5. 可复用组件

### 0x03 环境配置

1. CDN引入

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/165000_c4625f6c_5550632.png "屏幕截图.png")

2. 下载并引入

   ![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/165119_6e3ad9f0_5550632.png "屏幕截图.png")

3. NMP 安装

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/165345_110bee82_5550632.png "屏幕截图.png")

<br>

## Part 1 Vue 的初体验

### 0x01 旅程开始

先写一个Demo演示一下vue的用法

```HTML
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF_8">
    <title>Hello world</title>
</head>
<body>
    <div id = "app">
        {{message}}
    </div>
    <script src="../js/vue.js"></script><!--引入Vue.js-->
    <script>
        let app = new Vue({
            el:'#app',//用于挂载管理的元素
            data:{
                //定义数据
                message:'你好'
            }
        });
    </script>
</body>
</html>


```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/171133_56da8d76_5550632.png "屏幕截图.png")

1. el：声明挂载的元素
2. data：可以是从服务器传回来的数据

### 0x02 Vue列表展示

如何使用Vue展示从后端传过来的对象数组？（v-for 后面会详细说明）

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <ul>
            <!-- Vue的v-for可以帮您实现数组的遍历操作-->
            <li v-for="item of materials">id:{{item.id}};name:{{item.name}}</li>
        </ul>
    </div>

    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data:{
                msg:'list',
                //加入这是后端传过来的对象数组
                materials:[
                    {id:0,name:'Cpp'},
                    {id:1,name:'C'},
                    {id:2,name:'Python'},
                    {id:3,name:'Java'}]
            }
        });
    </script>
</body>
</html>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/173656_2af3035a_5550632.png "屏幕截图.png")

<br>

### 0x03 计数器案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <h2>当前计数:{{counter}}</h2>
        <!--<button v-on:click="counter++">+</button>
        <button v-on:click="counter--">-</button>-->
        <button v-on:click="add">+</button>
        <button v-on:click="subtract">-</button>
    </div>
    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue(
            {
                el:'#app',
                data:{
                    //计数器变量
                    counter:0
                },
                methods:{
                    add:function(){
                        this.counter++;
                    },
                    subtract:function(){
                        this.counter--;
                    }
                }
            });
    </script>
</body>
</html>
```

新指令：v-on:click 

新属性：methods 用于定义该对象的方法

（Vue对象中还能定义什么属性呢？）

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/175251_5d748b74_5550632.png "屏幕截图.png")

## Part 2 Vue 的MVVM 与 options对象

### 2.1 MVVM

Model->ViewModel->View
后端传回来的数据->绑定的对象->前端视图

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/175506_c18b1c15_5550632.png "屏幕截图.png")

### 2.2 options对象

实例化Vue对象时传入的对象就是options对象，它可以包含如下属性：

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/180444_c3ca27b2_5550632.png "屏幕截图.png")

剩余的请在[VueAPI](https://vuejs.org/v2/api/)下查看：

![输入图片说明](https://images.gitee.com/uploads/images/2021/0831/180714_af923d27_5550632.png "屏幕截图.png")

Vue对象的生命周期(Vue对象从创建到销毁)：

<img src="https://vuejs.org/images/lifecycle.png" style="zoom:67%;" />

其中**红框红字**的关键字是可以写在options对象中，用于对Vue对象本身初始化时的回调。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">

    </div>
    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data:{},
            methods:{},
            //生命周期中的回调函数(hook)
            created:function(){
                console.log('created');
            },
            mounted:function(){
                connsole.log('mounted');
            }
        });
    </script>
</body>
</html>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/145129_ad188952_5550632.png "屏幕截图.png")

<br>

## Part 3 Vue 基本语法

### 3.1 插值操作

#### 0x01 Mustache

```html
    <div id="app">
      <h2>{{id+' '+name+' '+age}}</h2>
      <h2>{{num * 2}}</h2>
    </div>

    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            
            data:{
                id:'1',
                name:'name1',
                age:18,
                num:100
            }
                
        });
    </script>
```

Mustache语法就是双括号取值语法，他有一些有趣的操作如上述代码展示

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/151635_0943e90b_5550632.png "屏幕截图.png")

#### 0x02 v-once

```html
<div id="app">
    <h2>{{msg}}</h2>
    <h2 v-once>{{msg}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el:'#app',

        data:{
            msg:"Hello"
        }
    });
</script>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/151905_12d99c95_5550632.png "屏幕截图.png")

使用v-once 指令后，无论值如何改变，它只会显示第一次出现的值。

#### 0x03 v-html

如果后端字段传回来的是某种html标签类的数据，那么我们可以通过v-html进行解析

```html
<div id="app">
    <h2>{{url}}</h2>
    <h2 v-html="url"></h2>
</div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el:'#app',
        data:{
            url:'<a href="http://www.baidu.com">百度一下</a>',
        }
    });
</script>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/152652_edce083d_5550632.png "屏幕截图.png")

#### 0x04 v-text (用的少)

和Mustache语法的结果一样，都是取值操作

```html
    <div id="app">
        <h2>{{msg}},啊</h2>
        <h2 v-text="msg"></h2>
    </div>
  
    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello'
            }
        });
    </script>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/153018_7e39b16a_5550632.png "屏幕截图.png")

#### 0x05 v-pre (用的少)

使用v-pre指令可以禁止Vue进行解析

```html
    <div id="app">
        <h2>{{msg}},啊</h2>
        <!--使用v-pre禁止解析-->
        <h2 v-pre>{{msg}}</h2>
    </div>
  
    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello'
            }
        });
    </script>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/153227_ffcf5e9c_5550632.png "屏幕截图.png")

#### 0x05 v-cloak

cloak:斗篷

用于前端卡住，且不想让用户看到$\{\{...\}\}$时，使用它

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        [v-cloak]{
            display: none;
        }
    </style>
</head>
<body>
    <!--使用v-cloak 当作标志位，当服务器响应慢时不渲染{{}}的内容-->
    <div id="app" v-cloak>
        <h2>{{msg}},啊</h2>
        
        <h2 v-pre>{{msg}}</h2>
    </div>
  
    <script src="../js/vue.js"></script>
    <script>
        //在Vue解析前存在 v-cloak属性，解析后就不存在了
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello'
            }
        });
    </script>
</body>
</html>
```

<br>

### 3.2 v-bind （绑定标签属性）

如果服务器动态返回一个图片的src，那么我们希望绑定的不是为用户显示的内容，而是**标签的属性**，如何写？

#### 0x01 基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app" >
        <img v-bind:src="imgURL" alt="">
        <a v-bind:href="ahref">百度一下</a>
    </div>
  
    <script src="../js/vue.js"></script>
    <script>
        
        const app = new Vue({
            el:'#app',
            data:{
                imgURL:'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwx1.sinaimg.cn%2Flarge%2F006TLXuhgy1gtabs54orjj311y0lcwfj.jpg&refer=http%3A%2F%2Fwx1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1633074608&t=0c34986365d09a095fb75ded1bc3e7db',
                ahref:"http://www.baidu.com"
            }
        });
    </script>
</body>
</html>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0901/155229_1e19aa3c_5550632.png "屏幕截图.png")

语法：

```
<标签名 v-bind:属性名="...">
```

##### v-bind 语法糖

```
:属性名="..."
```

```html
<img :src="imgURL" alt="">
<a v-bind:href="ahref">百度一下</a>
```

上下两种等价

#### 0x02 v-bind 绑定class属性(对象语法)

案例，点击按钮变颜色：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .active{
            color: red;
        }
    </style>
</head>
<body>
    <div id="app" >
        <h2 class="active">{{msg}}</h2>
        <!--绑定class-->
        <h2 v-bind:class="{active:isActive}">{{msg}}</h2>
        <button v-on:click="onClick()">点我变色</button>
    </div>
  
    <script src="../js/vue.js"></script>
    <script>
        
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },
            methods:{
                onClick:function(){
                    this.isActive = !this.isActive;
                }
            }
        });
    </script>
</body>
</html>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/0903/173831_91f23207_5550632.png "屏幕截图.png")

#### 0x03 v-bind 绑定class属性(数组语法-用的少)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .active{
            color: red;
        }
    </style>
</head>
<body>
    <div id="app" >
        <h2 class="active">{{msg}}</h2>
        <!--绑定class-->
        <h2 v-bind:class="{active:isActive}">{{msg}}</h2>
        <h2 v-bind:class="getClasses()">{{msg}}</h2>
        <button v-on:click="onClick()">点我变色</button>
    </div>
  
    <script src="../js/vue.js"></script>
    <script>
        
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },
            methods:{
                onClick:function(){
                    this.isActive = !this.isActive;
                },
                getClasses:function(){
                    return {active:this.isActive};
                }
            }
        });
    </script>
</body>
</html>
```

#### 0x04 v-bind 动态绑定style

![输入图片说明](https://images.gitee.com/uploads/images/2021/0907/091323_cfbe3029_5550632.png "屏幕截图.png")

<br>

### 3.3 计算属性

对后端传来的数据进行结合再显示，第一种方式，可以写个方法组织：

![输入图片说明](https://images.gitee.com/uploads/images/2021/0907/092512_3f8d098a_5550632.png "屏幕截图.png")

第二种方法，**计算属性**

![输入图片说明](https://images.gitee.com/uploads/images/2021/0907/092740_1c0b7da6_5550632.png "屏幕截图.png")

**计算属性的getter和setter**

![输入图片说明](https://images.gitee.com/uploads/images/2021/0907/094124_c3170ed5_5550632.png "屏幕截图.png")

### 3.4 v-on

v-on语法糖@,用于绑定一些事件(函数)。

![输入图片说明](https://images.gitee.com/uploads/images/2021/0908/154643_19ad800f_5550632.png "屏幕截图.png")



### 3.5 v-for

用于遍历数组，对象。

![输入图片说明](https://images.gitee.com/uploads/images/2021/0925/090500_c5cafea8_5550632.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2021/0925/090703_5a27c863_5550632.png "屏幕截图.png")

### 3.6 v-model 表单绑定

v-model可以实现数据和表单的双向绑定。

input标签内的数据和Vue中的data选项中的数据是同步的。

**v-model与radio **(互斥选项)

![输入图片说明](https://images.gitee.com/uploads/images/2021/0926/113451_7e5b53f9_5550632.png "屏幕截图.png")

**v-model与checkbox**(单选框，多选框)

![输入图片说明](https://images.gitee.com/uploads/images/2021/0926/114105_a23ab452_5550632.png "屏幕截图.png")

**v-model与select(下拉列表框)**

![输入图片说明](https://images.gitee.com/uploads/images/2021/0926/115423_45a5a4c7_5550632.png "屏幕截图.png")

v-model的修饰符。v-model.修饰符

![输入图片说明](https://images.gitee.com/uploads/images/2021/0926/120120_51897413_5550632.png "屏幕截图.png")

<br>

## Part 4 组件化开发

把一个页面看作若干功能模块的功能集合。通过将页面分解成功能块的方式，可以使前端开发系统化，结构化。

![输入图片说明](https://images.gitee.com/uploads/images/2021/0927/101016_baaf9391_5550632.png "屏幕截图.png")

如何创建组件：

1. 创建组件构造器
2. 注册组件
3. 使用组件

![输入图片说明](https://images.gitee.com/uploads/images/2021/0927/103143_8d89d2ed_5550632.png "屏幕截图.png")

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>


    <div id="app" >
        <my-cpn></my-cpn>
    </div>
    
    <script src="../../js/vue.js"></script>
    <script>
        //ES6:
        // ``字符串[可换行]('',"")

        //1.创建组件构造器对象
        const constructor = Vue.extend({
                template:`
                <div>
                    <h2>H2</h2>
                    <p>ppppp</p>
                </div>
                `
            })
        //2.注册组件(全局组件)
        Vue.component('my-cpn',constructor)
        //3.使用
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },
            
        });
    </script>
</body>
</html>
```

只要是自定义的组件在Vue的管理范围内，就可以生效

![输入图片说明](https://images.gitee.com/uploads/images/2021/0927/104941_d3bc7bc0_5550632.png "屏幕截图.png")

但是，如果把自定义组件写在了Vue的管理范围外，自然就不生效了。

![输入图片说明](https://images.gitee.com/uploads/images/2021/0927/105048_b1fa9a7f_5550632.png "屏幕截图.png")

### 4.1 全局组件和局部组件

全局组件意味着，可以在多个Vue的实例下使用。那么局部组件如何注册呢？在实例化Vue类时注册。

```javascript
const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },
            components:{
                c_name:constructor
            }
        });
```

### 4.2 父组件和子组件

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>


    <div id="app" >
        <cpn2></cpn2>    
    </div>
    
    
    <script src="../../js/vue.js"></script>
    <script>
        //子组件
        const cpnC1 = Vue.extend({
                template:`
                <div>

                    <h2>我是cpn1的H2</h2>
                    <p>我是cpn1内容</p>
                </div>
                `
            })
        //父组件
        const cpnC2 = Vue.extend({
            template:`
            <div>

                <h2>我是cpn2的H2</h2>
                <p>我是cpn2内容</p>
                <cpn1></cpn1> 
            </div>
            `,
            //在cnp2内注册cpn1组件
            components:{
                cpn1:cpnC1,
            }
        })

        //根组件
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },    
            //注册组件cpn2
            components:{
                cpn2:cpnC2
            }    
        });
    </script>
</body>
</html>
```

Vue对象本身可以看作根组件。如果一个组件A在另一个组件B中被声明，那么B是A的父组件，且A只能在B组件中使用，因为A是在B中注册的。

**组件注册语法糖**

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>


    <div id="app" >
        <cpn></cpn>    
    </div>
    
    
    <script src="../../js/vue.js"></script>
    <script>
        //全局组件注册语法糖
        //注册组件
        Vue.component('cpn',{
            template:`
            <div>
                <h2>啊这....</h2>    
            </div>`
        })

        //根组件
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },    
           
        });
    </script>
</body>
</html>
```

组件的分离写法

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <!--使用Script标签-->
    <script type="text/x-template" id="cpnC1">
        <div>
            <h2>cpn1-我是标题1</h2>
            <p>cpn1-我是内容1</p>    
        </div>
    </script>
    <!--使用template标签-->
    <template id="cpnC2">
        <div>
            <h2>cpn2-我是标题2</h2>
            <p>cpn2-我是内容2</p>    
        </div>
    </template>

    <div id="app" >
        <cpn></cpn>    
        <cpn2></cpn2> 
    </div>
   
    
    <script src="../js/vue.js"></script>
    <script>
        //注册组件
        Vue.component('cpn',{template:"#cpnC1"})
        Vue.component('cpn2',{template:"#cpnC2"})
        //根组件
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },    
            /*components:{
                'cpn':{
                    template:'#cpnC1'
                },
                'cpn2':{
                    template:'#cpnC2'
                }
            }*/
          
        });
    </script>
</body>
</html>
```

后期有更好用的写法，这种写法可以优化

且，**组件不可以访问Vue实例中的数据**

 解决方式1:

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    
    <!--使用template标签-->
    <template id="cpnC1">
        <div>
            <h2>cpn-我是标题-{{title}}</h2>
            <p>cpn-我是内容</p>    
        </div>
    </template>

    <div id="app" >
        <cpn></cpn>    
    </div>
   
    
    <script src="../js/vue.js"></script>
    <script>
        //注册组件
        Vue.component('cpn',{
            template:"#cpnC1",
            //组件内部有data,但它必须是一个函数,函数返回一个对象,对象里的值我们可以访问
            data(){
                return {
                    title:"abc"
                }
            }
    
        })
       
        //根组件
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                isActive:false,
            },    
            /*components:{
                'cpn':{
                    template:'#cpnC1'
                },
                'cpn2':{
                    template:'#cpnC2'
                }
            }*/
          
        });
    </script>
</body>
</html>
```

### 4.3 父子组件通信

前端的数据大多数都是从后端传过来的。那么存在两个问题：

1.如何拿到后端数据

2.如何展示数据

在组件化开发过程中，我们的所有网络请求都是根组件发出的。假设我们要呈现一个学生的信息，学生类的定义如下：

```java
class Student{
	private String name;
    private int age;
    private char gender;
    private double height;
}
```

网页的设计如下：

<img src="https://images.gitee.com/uploads/images/2021/1128/100544_e9b709d2_5550632.png" alt="输入图片说明" title="屏幕截图.png" style="zoom:50%;" />

首先，在最外层组件中对服务器发出Get或Post请求，得到学生列表

```
studentList []
```

然后在橙色的子组件中使用v-for标签，**循环生成橙色组件中小的黑色子组件**，**最终在小黑组件中使用v-for遍历对象属性，完成展示工作**。

第一步发请求，我们之后会在网络请求里讲。先讲如何进行组件间的数据传输。

#### 4.3.1 父传子

**prop方法向子组件传递**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body> 
    <!--使用template标签-->
    <template id="cpnC1">
        <div>
            <h2>cpn-我是标题-{{title}}</h2>
            <ul>
                <li v-for= "item in cstudents">{{item}}</li>
            </ul>   
        </div>
    </template>

    <div id="app" >
        <!--子组件拿父组件的数据-->
        <cpn v-bind:cstudents='students'></cpn>    
    </div>
   
    
    <script src="../../js/vue.js"></script>
    <script>
        //根组件
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                students:['stu1','stu2','stu3']
            },    
            components:{
                'cpn':{
                    template:'#cpnC1',
                    //父传子props
                    //写法1:props:['cstudents'],
                    //写法2:
                    props:{
                        cstudents:Array,
                    },
                    data(){
                        return{};
                    }
                },
            }
          
        });
    </script>
</body>
</html>
```

同时，如果子组件中的变量名为驼峰式，那么在v-bind时需要进行转换。

例如：

```
prop:{
  cStudents:{
    type:Array,
    }
}
...............
 <cpn v-bind:c-students='students'></cpn>  
```

#### 4.3.2 子传父

**通过事件向父组件发送消息（自定义事件）**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    
    <!--使用template标签-->
    <template id="cpnC1">
        <div>
            <button v-for = "item in categories" @click="btnClick(item)">{{item.name}}</button>
        </div>
    </template>

    <div id="app" >
        <cpn v-on:item-click="cpnClick"></cpn>    
    </div>
   
    
    <script src="../../js/vue.js"></script>
    <script>
        //根组件
        const app = new Vue({
            el:'#app',
            data:{
                msg:'Hello',
                
            },
            methods:{
                cpnClick(item){
                    console.log('子组件点击了',item);
                    
                }
            }, 
            components:{
                'cpn':{
                    template:'#cpnC1',
                    data(){
                        return{
                            categories:[
                            {id:'1',name:'热门推荐'},
                            {id:'2',name:'手机数码'},
                            {id:'3',name:'电脑办公'},
                        ]
                        };
                    },
                    methods:{
                        btnClick(item){
                            //子组件已知数据-如何传？
                            //子组件发送自定义事件
                            this.$emit('item-click',item)//事件名,参数
                        }
                    }
                },
            }
          
        });
    </script>
</body>
</html>
```

总结一下流程：

现在子组件想把数据传给父组件，怎么办？

1.子组件自己本身需要拿到数据

2.使用**$emit方法**，向父组件发射一个二元组：<事件名,参数>，事件名指的是在父组件里用来接受参数的方法名（事件名，函数名）

3.在父组件里定义一个和发射的二元组中相同的事件名。**注意，在接受参数时无需写形式参数，系统会默认把需要传递的值传进去的**，写了形参反而会报错。

4.在父组件里定义的接受事件中，就可以使用该数据了。

子组件有发送方法，方法里有个emit，参数是个二元组，前者名称后者值，父组件有接受方法，名称与参数1相同，不写形参默认传，不要忘记v-on，不绑事件没法玩。

#### 4.3.3 父子组件访问方法

在开发中有时我们希望可以在父组件中直接调用或操纵子组件的某些方法又或者子组件向调用父组件里的一些方法，何解？

父组件访问子组件：

```
$children(用的少，但可以拿到一个包含所有子组件的数组)
$refs(给子组件上写个标签 ref="key",然后在父组件中就可以this.$refs.key.属性(方法))
```

子组件访问父组件：

```
$parent
```

访问根组件：

```
$root
```

### 4.4 插槽 slot

组件的插槽可以让组件有更好的可扩展性，类似于接口。

比如导航栏，每个页面都有导航栏，但每个页面的导航栏都不一样。

<img src="https://images.gitee.com/uploads/images/2021/1130/150222_ca173460_5550632.png" alt="输入图片说明" title="屏幕截图.png" style="zoom:50%;" />

我们可以这样做：

```html
<body>



  <template id="mcpn1">
      <div>
          <h2>我是组件</h2>
          <span>我是span</span> 
          <slot></slot>  
      </div> 
  </template>  

  <div id="app" >
    <mcpn><button>按钮</button></mcpn>
    <mcpn><span>我是插槽span</span></mcpn>
  </div>
    
    
    
  <script src="../../js/vue.js"></script>
  <script>
    
    //根组件
    const app = new Vue({
        el:'#app',
        data:{
            
        },    
        components:{
            'mcpn':{
                tempelate:'#mcpn1'
            }
        }
        
    });

  </script>

</body>
```

这是只用一个插槽时的方式（有Bug）

但是，还有另外一个问题，如果在一个组件里我用三个插槽，但我只想改变某一个插槽的内容，其它不变，怎么办？

给slot起名字。**具有名字的插槽（具名插槽）**

```html
<template id="mcpn1">
    <div>
        <h2>我是组件</h2>
        <span>我是span</span> 
        <slot name="left"></slot>
        <slot name="middle"></slot>
        <slot name="right"></slot>  
    </div> 
</template>  
```

在组件中使用的话：

```html
<mcpn><button slot="left">按钮</button></mcpn>
```

需要给插槽内容加个slot属性告诉它往哪插。

<br>

## Part 5 模块化开发

#### 5.1 前端模块化与CommonJS

在Node环境下，CommonJS导出和导入语法：

导出：

```js
module.exports = {
	...,
	...
}
```

导入：

```
var{...,...} = require('file_path')
```



#### 5.2  ES模块的导入和导出

导出：

```
export {
函数/变量/类,...
}

export 函数/变量/类,...

```

导入：

```
import{...,...} from 'file_path'
```

<br>

## Part 6 Webpack 打包

webpack可以把一大堆js打包成一个浏览器可以识别的东西。

按照模块化开发思路后的js代码，需要一个类似于编译器的东西让其可以被浏览器识别并执行。

首先webpack需要nodejs环境。

全局安装webpack：

```
cnpm install webpack@3.6.0 -g
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/1111/151124_54e50805_5550632.png "屏幕截图.png")

对上图红框内的两个js进行打包：

```
在项目根目录下:webpack ./src/main.js ./dist/bundle.js
```

然后只需要在我们的HTML里面引入 **bundle.js**，就可以运行了

现在我们还想做到一件事，**命令行里的参数太长了，想通过配置文件的方式告诉webpack从哪个文件夹开始打包，输出到哪个文件夹下**，怎么办？

此时需要配置webpack.config文件

```javascript
const path = require('path')

module.exports = {
    entry:'./src/main.js',
    output:{
        path:path.resolve(__dirname,'dist'),//路径必须是绝对路径,所以需要动态获取它
        filename:'bundle.js'
    }
}
```

我们从外部导入了一个path包，但是项目中并没有，所以需要使用npm（cnpm）来配置一下**package.json**文件，在当前工程目录下输入

```
cnpm init
```

<img src="https://images.gitee.com/uploads/images/2021/1125/133750_616744d2_5550632.png" alt="输入图片说明" title="屏幕截图.png" style="zoom:67%;" />

一路输入就会在根目录下生成一个package.json文件，它长这样：

```json
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}

```

此时在命令行中直接敲击**webpack**，就可以不指定路径自动打包了。

![输入图片说明](https://images.gitee.com/uploads/images/2021/1125/133935_ba2f2472_5550632.png "屏幕截图.png")

但是又要等一下，现在我不想通过webpack部署项目，我想通过npm管理并部署项目，怎么办？其实很简单，我们只需要在package.json中写好npm run -> webpack间的映射关系就行了。

```json
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build":"webpack"
  },
  "author": "",
  "license": "ISC"
}

```

![输入图片说明](https://images.gitee.com/uploads/images/2021/1125/134957_444627a1_5550632.png "屏幕截图.png")

###### 开发依赖与运行依赖

使用npm管理时，如果命令为：

```
cnpm install --save-dev css-loader ts-loader
```

里面存在**--save-dev**那就是开发时依赖，所导入的包都是开发时生效的。如果写成：

```
cnpm install --save css-loader ts-loader
```

那么它就是运行依赖的，

### 6.1 loader

除了模块化打包js，如果我们还想打包ts，图片,css的时候该怎么办呢？

我们就要用到webpack里的loader

使用步骤：

1.通过npm安装不同的文件使用不同的loader

2.在webpack.config.js的modules关键字下进行配置

我们可以去官网查询，不同类型的loader如何配置[点这里](https://webpack.docschina.org/loaders)

假如我的项目中想打包这个css：

![输入图片说明](https://images.gitee.com/uploads/images/2021/1125/140950_b035ce9d_5550632.png "屏幕截图.png")

按照官网要求首先需要安装css-loader，并进行配置后就可以直接使用了。

## Part 7 Vue CLI

安装脚手架：

```
cnpm install -g @vue/cli
```

使用脚手架3，创建Vue项目：

```
vue create 项目名称
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/1126/112956_2a0c5797_5550632.png "屏幕截图.png")

但是，配置文件去哪儿了？

在命令行中，通过 **vue ui**命令进行配置

#### 7.1 箭头函数

箭头函数是定义函数的一种新方式。

之前，我们是这样定义函数的：

```javascript
const func = function(){
}

//在对象中定义函数
const obj = {
    bar(){
	}
}
```

ES6的箭头函数：

```javascript
const func = () =>{} //无参无返回值版
const pow = num => {return num*num}//放入一个参数,可省略小括号
const sum = (num1,num2) =>{return num1+num2}//放入多个参数
const mul = (num1,num2) => num1*num2//函数代码块中只有一行代码
```

那么什么时候使用箭头函数呢？

**我们把函数当参数传的时候，使用箭头函数**

那么在箭头函数里使用this，就会出现很多奇怪的问题。

箭头函数的this，引用的是最近作用域中的this，向外层一层层查找this，直到找到为止。

## Part 8 路由 (Vue-Router)

#### 8.1 什么是路由

通俗说，路由在前端的主要展现方式就是页面跳转。

路由中有个非常重要的东西，叫做**路由表**。它决定了数据的传输路径。

在前后端分离开发时代，一个页面（HTML+CSS+JS）对应一个URL，在静态服务器中存在着好几套。浏览器里输入不同的URL就去访问不同的页面。

目前前端开发是这样一个时代：**单页面富应用**，即，SPA应用（Simple page web Application），就是我们整个前端项目只有一个html页面。

用户访问页面时，在静态服务器中**有且仅有一套页面元素**，通过路由的方式给页面挂载不同的组件，最终实现系统功能。

#### 8.2 基本使用

1. 导入路由对象，调用Vue.use(VueRouter)
2. 创建路由实例，传入**路由映射配置**
3. 在Vue实例中挂载路由实例

![输入图片说明](https://images.gitee.com/uploads/images/2021/1203/103157_f5eeb9fc_5550632.png "屏幕截图.png")

先创建一个router文件夹建一个index.js。在脚手架2中可以如下使用router

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'


//传入插件,并安装.
Vue.use(VueRouter)

//配置路由信息
const routes = [
  
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes:routes
})

//导出
export default router

```

再vue-router内，还有两个内置组件。

```vue
<router-link to="" tag=""></router-link>
/*本标签用于更改URL
to:跳转路径
tag:渲染成的标签（2020-12已被移除）
replace:只写属性名用户就不能用浏览器的回退按钮了
active-class:"类名",为router-link标签添加一个样式类名，在点击悬浮有改颜色的需求时就相对好做了。
*/
<router-view></router-view>/*告知渲染内容的位置*/
```

在脚手架4中则须这样声明：

```javascript
//脚手架4专用写法
import { createRouter, createWebHashHistory } from 'vue-router'

//导入组件
import Home from '../views/home/Home.vue'
import UserInfo from '../views/userInfo/UserInfo.vue'
import NotFound from '../components/common/notFound/NotFound.vue'
//传入插件,并安装. CL2才可使用
//Vue.use(VueRouter)

//配置路由信息
const routes = [
  {
    path:"",
    redirect:"/home"
  },
  {
    path: '/userinfo',//路径
    component:UserInfo
  },
  {
    path: '/home',
    component:Home
  },
  { path: '/:pathMatch(.*)', 
    component: NotFound
  }, 
]

const router = createRouter({
  history: createWebHashHistory(),
  routes:routes
})

//导出
export default router

```

路由的默认路径设置：

```vue
{
	path:"",
	redirect:"/路径"
}
```

在main.js中注册挂载：

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router/index.js'

createApp(App).use(router).mount('#app')
```

使用方法来控制页面跳转：

```vue
<template>
	<div class="left-bar-body">
		<a class="left-bar-item" v-for = "item in leftBarItemList" :key="item.index" @click=itemClick(item.path)>	
			<span class="left-bar-icon">
				<img class="icon" v-bind:src="item.icon_path" alt="图片未显示">
			</span>
			<span>{{item.name}}</span>
		</a>		
	</div>

</template>

<script>
export default {
		name: 'LeftBarItem',
		props: {
		},
		data(){
			return {
				leftBarItemList:[
					{
						name:"资料",
						icon_path:require("assets/images/leftBar/material.png"),
						path:null
					},
					{
						name:"题库",
						icon_path:require("assets/images/leftBar/homework.png"),
						path:null
					},
					{
						name:"记录",
						icon_path:require("assets/images/leftBar/record.png"),
						path:null
					},
					{
						name:"我的",
						icon_path:require("assets/images/leftBar/me.png"),
						path:"/userinfo"
					}],
			}
		},
		computed: {
			
		},
		methods: {
			itemClick(path){
				console.log(this.$router)
				this.$router.push(path).catch(err=>{err});
			}
		}
	}
</script>

<style scoped>

</style>

```

其中$\$router$是一个全局变量，它用于将组件压入浏览器的history栈中，以此进行页面跳转。该对象中有如下几种添加方式：

router.go(n) 这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似
window.history.go(n)

router.push(location) 想要导航到不同的 URL，则使用 router.push 方法。这个方法会向 history
栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。

router.replace(location) 跟 router.push 很像，唯一的不同就是，它不会向 history添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录。

#### 8.3 动态路由

![输入图片说明](https://images.gitee.com/uploads/images/2021/1205/091421_3d9337a1_5550632.png "屏幕截图.png")

如果想在组件中拿到参数，可以使用$/$$route.params.名称$来获取

#### 8.4 嵌套路由

![输入图片说明](https://images.gitee.com/uploads/images/2021/1205/100041_f23f7301_5550632.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2021/1205/100447_333aa0b2_5550632.png "屏幕截图.png")

#### 8.5 参数传递

比如说从登陆页面登陆成功后跳转回首页，此时我们想把用户Id传回来，怎么办？

其中一种方式就是之前讲的动态路由。

```
/router/:id
```

还有一种是query

```vue
<router-link v-bind:to="{path:'/test',query:{param1:1,param2:2}}"></router-link>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/1206/101646_997954ca_5550632.png "屏幕截图.png")

请注意上面的URL发生了变化。取值方法如下：

```vue
{{$route.query.param1}}...
```



#### 8.6 路由守卫

通过直接输入URL的方式访问页面是十分不安全的。所以我们需要监听页面跳转的方式。

路由护卫有两种：一种前置护卫，另一种是后置护卫，写法如下：

```javascript
const router = createRouter({
  history:createWebHistory(process.env.BASE_URL),//使用history模式去掉#
  routes:routes
})

/*全局守卫-Begin*/

//前置守卫-在跳转之前的回调函数
router.beforeEach((to,from,next)=>{
  
  //从from跳转到to
  console.log("beaforEach:"+to.name)
  document.title = to.matched[0].meta.title
  next()//必须调用next
})

//后置守卫-在跳转之后回调
router.afterEach(
  (to,from)=>{
    console.log(to)
    console.log(from)
  }
)
/*全局守卫-End*/
```

并附上vue官方判断是否绕过登录访问页面的代码：

```javascript
// GOOD
router.beforeEach((to, from, next) => {
  if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' })
  else next()
})
```

#### 8.7 keep-alive

如果想实现这个功能，那就要使用keep-alive了。

从整个页面上有页面A和页面B两个组件的跳转按钮，其中新闻，消息组件是A的子组件。

现在我在浏览A中的消息组件，然后我点击了B。此时使用浏览器的回退功能。如果想退回之前我所浏览的那个组件就需要使用keep-alive了。

keep-alive是Vue的内置组件，可以使包含的组件保存状态或避免重新渲染。

用法：

```vue
<keep-alive>
	<router-view></router-view>
</keep-alive>
```

## Part 9 Promise

### 9.1 什么是Promise

promise一般是用于处理异步操作的。比如用户登录完毕时，要在主页显示推荐信息。为了不让页面卡住，和让用户等待较长时间，我们此时就需要进行异步操作，首先让前端去服务器去请求处理结果，然后通过回调函数把结果传回来。这样业务逻辑就不是顺序执行的了，用户就可以登录之后直接进入首页浏览其它信息，等信息加载完毕后再渲染到前端。

### 9.2 基本使用

当有异步操作时，使用Promise对异步操作进行封装

```vue
<script>
    //resolve,reject也是两个函数
	new Promise((resolve,reject)=>{
        setTimeout(()=>{
         resolve("data")},1000)//回调成功
        reject("data")//回调失败
    }).then(()=>{
        //处理数据
        console.log(data)
        
        return new Promise(
        	(resolve,reject)=>{
                //...
            }).catch((err)=>{
            console.log(err)
        })
    })
</script>
```

### 9.3 Promise 的三种状态

同步，sync

异步，async



## Part 10 Vuex

### 10.1 Vuex概念

Vuex是为Vue开发的状态管理模式。

简单来说，一个登陆成功的用户，他的登陆状态应该保存在哪里合适呢？放到组件里显然是不合适的（一层一层传递），此时我们就有了状态管理工具这一概念。

或者，从编程实现的角度来看，我们需要封装出一个全局变量管理空间，来管理我们需要的全局变量。

如果这样来看，那么其实我们不需要Vuex，自己也能写。不就是一个全局变量对象吗

```vue
const publicObj = {
	state1:...,
	state2:...,
}
vue.prototype.publicObj = publicObj;
```

但是如果在某个组件中更改了它的值，全局的值是**不会发生变化的**，换句话说，**目前自己写的代码不是响应式的**。这就是使用Vuex的第二个原因了。它是一种**响应式的状态管理工具**.

一般需要使用Vuex的内容有：登录状态(token),用户的头像，名称，地理位置。商品的收藏，购物车的物品等等。

### 10.2 基本使用

既然它是个第三方插件，第一步肯定是安装，而且是安装到生产环境中。

```
cnpm install vuex --save
```

然后在mian.js中注册该组件

```javascript
createApp(App).use(store).use(router).mount('#app')
```

然后创建一个对象来使用：

```javascript
import { createStore } from 'vuex'

export default createStore({
  state: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})

```

当然以上所有都可以通过脚手架4自动生成。附上官方vuex管理流程说明：

![输入图片说明](https://images.gitee.com/uploads/images/2021/1209/144743_6d3beb74_5550632.png "屏幕截图.png")



### 10.3 vuex操作八股文

在上图中，我们可以看到Vue不希望我们直接在组件中更改状态，而是想让组件dispatch到Actions，通过Mutataion来修改状态。

这样，更改Vuex中的State就有了固定写法。

```javascript
export default createStore({
  state: {
      count = 0;
  },
  mutations: {
      increament(state){
          state.count++;
      }
      
      decrement(state){
		state.count--;   
	}
  },
  actions: {
  },
  modules: {
  }
})
```

组件中调用：

```vue
<script>
	export default{
        name:"App",
        methods:{
            add(){
				this.$store.commit("increament")
            },
            abtract(){
            	this.$store.commit("decreament")
        	}
        }
    }
</script>
```

![输入图片说明](https://images.gitee.com/uploads/images/2021/1209/155225_5ee7f5e6_5550632.png "屏幕截图.png")



## Part 11 网络请求封装

在向服务器进行网络请求时有很多方法。

1.基于XMLHttpRequest：不用，自己配置会疯掉的。

2.jQuery-Ajax:不用，因为vue中不用jQuery了。

3.Vue1.0中有个Vue-resource：不用，Vue2.0中不再维护它了

4.axios：用这个框架，支持转换请求和响应数据，支持拦截请求与响应，支持Promise API等

axios：ajax i/o System

![输入图片说明](https://images.gitee.com/uploads/images/2021/1209/174448_e8414e52_5550632.png "屏幕截图.png")

axios向服务器发post请求：

```javascript
axios({url:'http://localhost:8888/login',
            method:'post',
            data:JSON.stringify(数据对象),
            headers: {
               'Content-Type': 'application/json;charset=utf-8'
              },
      }).then(res=>{console.log(res)})
```

配置全局配置，如baseURL，超时时间等。

```
axios.default.baseURL = ...
axiso.default.timeout = ...(单位毫秒)
```

常见配置项包括：

![输入图片说明](https://images.gitee.com/uploads/images/2021/1210/105126_61b974ab_5550632.png "屏幕截图.png")

对网络请求进行封装：

```javascript
import axios from 'axios'


export function request(config){
  
  const instance = axios.create({
    baseURL:'http://localhost:8888',
    timeout:5000
  })
    
  return instance(config)
}
```

config是个对象里面包括了诸如：method，data，headers等字段的设置。本质上是返回了一个Promise对象，我们可以通过传入

resolve，reject两个函数的方式处理数据。

```javascript
request({
        url:"/login",
        method:'post',
        data:JSON.stringify(loginform),
        headers:{
          'Content-Type': 'application/json;charset=utf-8'
        }
      }).then(res=>{
          this.responseBody = res.data.body
          this.errMsgs =res.data.errMsgs
          this.status = res.data.status
        }).catch(err=>{console.log(err)})
```

