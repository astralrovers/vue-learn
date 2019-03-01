# VUE学习

## 介绍

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## 安装

- 我们可以在 Vue.js 的官网上直接下载 vue.min.js 并用 **<script>** 标签引入

- **Staticfile CDN（国内）** : <https://cdn.staticfile.org/vue/2.2.2/vue.min.js>
- **unpkg**：<https://unpkg.com/vue/dist/vue.js>, 会保持和 npm 发布的最新的版本一致。
- **cdnjs** : <https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js>

## 简单示例

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>简单示例</title>
        <script src="https://unpkg.com/vue/dist/vue.js"></script>
    </head>
    <body>
        <div id="app">
            {{ message }}
        </div>
    </body>
    <script src="example.js"></script>
</html>
```

```javascript
let app = new Vue({
    el : "#app",
    data : {
        message : "Hello world!"
    }
});
```



## 使用NPM

### 安装

- 首先安装稳定版vue`cnpm install vue`
- Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用：`cnpm install --global vue-cli`
- 创建一个基于webpack模板的项目，webpack是啥以后再学习

```shell
? Project name my-project
? Project description A Vue.js project
? Author ywl <astralrovers@outlook.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests Yes
? Pick a test runner jest
? Setup e2e tests with Nightwatch? Yes
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "my-project".
```

接下来：

```shell
$ cd my-project
$ cnpm install
$ cnpm run dev
 DONE  Compiled successfully in 4388ms

> Listening at http://localhost:8080

 DONE  Compiled successfully in 9667ms                                                

 I  Your application is running here: http://localhost:8080
```

就可以在浏览器中看到项目了。

## 目录结构

| 目录/文件    | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| build        | 项目构建(webpack)相关代码                                    |
| config       | 配置目录，包括端口号等。我们初学可以使用默认的。             |
| node_modules | npm 加载的项目依赖模块                                       |
| src          | 这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：assets: 放置一些图片，如logo等。components: 目录里面放了一个组件文件，可以不用。App.vue: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。main.js: 项目的核心文件。 |
| static       | 静态资源目录，如图片、字体等。                               |
| test         | 初始测试目录，可删除                                         |
| .xxxx文件    | 这些是一些配置文件，包括语法配置，git配置等。                |
| index.html   | 首页入口文件，你可以添加一些 meta 信息或统计代码啥的。       |
| package.json | 项目配置文件。                                               |
| README.md    | 项目的说明文档，markdown 格式                                |

这里不会过多学习，先把基本内容学习了再倒回来。

## 关于MVVM

引用自：[廖雪峰的javascript教程](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001475449022563a6591e6373324d1abd93e0e3fa04397f000)

什么是MVVM？[MVVM](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel)是Model-View-ViewModel的缩写。

要编写可维护的前端代码绝非易事。我们已经用MVC模式通过koa实现了后端数据、模板页面和控制器的分离，但是，对于前端来说，还不够。

这里有童鞋会问，不是讲Node后端开发吗？怎么又回到前端开发了？

对于一个全栈开发工程师来说，懂前端才会开发出更好的后端程序（不懂前端的后端工程师会设计出非常难用的API），懂后端才会开发出更好的前端程序。程序设计的基本思想在前后端都是通用的，两者并无本质的区别。这和“不想当厨子的裁缝不是好司机”是一个道理。

当我们用Node.js有了一整套后端开发模型后，我们对前端开发也会有新的认识。由于前端开发混合了HTML、CSS和JavaScript，而且页面众多，所以，代码的组织和维护难度其实更加复杂，这就是MVVM出现的原因。

在了解MVVM之前，我们先回顾一下前端发展的历史。

在上个世纪的1989年，欧洲核子研究中心的物理学家Tim Berners-Lee发明了超文本标记语言（HyperText Markup Language），简称HTML，并在1993年成为互联网草案。从此，互联网开始迅速商业化，诞生了一大批商业网站。

最早的HTML页面是完全静态的网页，它们是预先编写好的存放在Web服务器上的html文件。浏览器请求某个URL时，Web服务器把对应的html文件扔给浏览器，就可以显示html文件的内容了。

如果要针对不同的用户显示不同的页面，显然不可能给成千上万的用户准备好成千上万的不同的html文件，所以，服务器就需要针对不同的用户，动态生成不同的html文件。一个最直接的想法就是利用C、C++这些编程语言，直接向浏览器输出拼接后的字符串。这种技术被称为CGI：Common Gateway Interface。

很显然，像新浪首页这样的复杂的HTML是不可能通过拼字符串得到的。于是，人们又发现，其实拼字符串的时候，大多数字符串都是HTML片段，是不变的，变化的只有少数和用户相关的数据，所以，又出现了新的创建动态HTML的方式：ASP、JSP和PHP——分别由微软、SUN和开源社区开发。

在ASP中，一个asp文件就是一个HTML，但是，需要替换的变量用特殊的`<%=var%>`标记出来了，再配合循环、条件判断，创建动态HTML就比CGI要容易得多。

但是，一旦浏览器显示了一个HTML页面，要更新页面内容，唯一的方法就是重新向服务器获取一份新的HTML内容。如果浏览器想要自己修改HTML页面的内容，就需要等到1995年年底，JavaScript被引入到浏览器。

有了JavaScript后，浏览器就可以运行JavaScript，然后，对页面进行一些修改。JavaScript还可以通过修改HTML的DOM结构和CSS来实现一些动画效果，而这些功能没法通过服务器完成，必须在浏览器实现。

用JavaScript在浏览器中操作HTML，经历了若干发展阶段：

第一阶段，直接用JavaScript操作DOM节点，使用浏览器提供的原生API：

```javascript
var dom = document.getElementById('name');
dom.innerHTML = 'Homer';
dom.style.color = 'red';
```

第二阶段，由于原生API不好用，还要考虑浏览器兼容性，jQuery横空出世，以简洁的API迅速俘获了前端开发者的芳心：

```javascript
$('#name').text('Homer').css('color', 'red');
```

第三阶段，MVC模式，需要服务器端配合，JavaScript可以在前端修改服务器渲染后的数据。

现在，随着前端页面越来越复杂，用户对于交互性要求也越来越高，想要写出Gmail这样的页面，仅仅用jQuery是远远不够的。MVVM模型应运而生。

MVVM最早由微软提出来，它借鉴了桌面应用程序的MVC思想，在前端页面中，把Model用纯JavaScript对象表示，View负责显示，两者做到了最大限度的分离。

把Model和View关联起来的就是ViewModel。ViewModel负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model。

ViewModel如何编写？需要用JavaScript编写一个通用的ViewModel，这样，就可以复用整个MVVM模型了。

一个MVVM框架和jQuery操作DOM相比有什么区别？

我们先看用jQuery实现的修改两个DOM节点的例子：

```html
<!-- HTML -->
<p>Hello, <span id="name">Bart</span>!</p>
<p>You are <span id="age">12</span>.</p>
```

Hello, **Bart**!

You are **12**.

用jQuery修改name和age节点的内容：

```javascript
var name = 'Homer';
var age = 51;

$('#name').text(name);
$('#age').text(age);
```

------

什么是MVVM？[MVVM](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel)是Model-View-ViewModel的缩写。

要编写可维护的前端代码绝非易事。我们已经用MVC模式通过koa实现了后端数据、模板页面和控制器的分离，但是，对于前端来说，还不够。

这里有童鞋会问，不是讲Node后端开发吗？怎么又回到前端开发了？

对于一个全栈开发工程师来说，懂前端才会开发出更好的后端程序（不懂前端的后端工程师会设计出非常难用的API），懂后端才会开发出更好的前端程序。程序设计的基本思想在前后端都是通用的，两者并无本质的区别。这和“不想当厨子的裁缝不是好司机”是一个道理。

当我们用Node.js有了一整套后端开发模型后，我们对前端开发也会有新的认识。由于前端开发混合了HTML、CSS和JavaScript，而且页面众多，所以，代码的组织和维护难度其实更加复杂，这就是MVVM出现的原因。

在了解MVVM之前，我们先回顾一下前端发展的历史。

在上个世纪的1989年，欧洲核子研究中心的物理学家Tim Berners-Lee发明了超文本标记语言（HyperText Markup Language），简称HTML，并在1993年成为互联网草案。从此，互联网开始迅速商业化，诞生了一大批商业网站。

最早的HTML页面是完全静态的网页，它们是预先编写好的存放在Web服务器上的html文件。浏览器请求某个URL时，Web服务器把对应的html文件扔给浏览器，就可以显示html文件的内容了。

如果要针对不同的用户显示不同的页面，显然不可能给成千上万的用户准备好成千上万的不同的html文件，所以，服务器就需要针对不同的用户，动态生成不同的html文件。一个最直接的想法就是利用C、C++这些编程语言，直接向浏览器输出拼接后的字符串。这种技术被称为CGI：Common Gateway Interface。

很显然，像新浪首页这样的复杂的HTML是不可能通过拼字符串得到的。于是，人们又发现，其实拼字符串的时候，大多数字符串都是HTML片段，是不变的，变化的只有少数和用户相关的数据，所以，又出现了新的创建动态HTML的方式：ASP、JSP和PHP——分别由微软、SUN和开源社区开发。

在ASP中，一个asp文件就是一个HTML，但是，需要替换的变量用特殊的`<%=var%>`标记出来了，再配合循环、条件判断，创建动态HTML就比CGI要容易得多。

但是，一旦浏览器显示了一个HTML页面，要更新页面内容，唯一的方法就是重新向服务器获取一份新的HTML内容。如果浏览器想要自己修改HTML页面的内容，就需要等到1995年年底，JavaScript被引入到浏览器。

有了JavaScript后，浏览器就可以运行JavaScript，然后，对页面进行一些修改。JavaScript还可以通过修改HTML的DOM结构和CSS来实现一些动画效果，而这些功能没法通过服务器完成，必须在浏览器实现。

用JavaScript在浏览器中操作HTML，经历了若干发展阶段：

第一阶段，直接用JavaScript操作DOM节点，使用浏览器提供的原生API：

```
var dom = document.getElementById('name');
dom.innerHTML = 'Homer';
dom.style.color = 'red';
```

第二阶段，由于原生API不好用，还要考虑浏览器兼容性，jQuery横空出世，以简洁的API迅速俘获了前端开发者的芳心：

```
$('#name').text('Homer').css('color', 'red');
```

第三阶段，MVC模式，需要服务器端配合，JavaScript可以在前端修改服务器渲染后的数据。

现在，随着前端页面越来越复杂，用户对于交互性要求也越来越高，想要写出Gmail这样的页面，仅仅用jQuery是远远不够的。MVVM模型应运而生。

MVVM最早由微软提出来，它借鉴了桌面应用程序的MVC思想，在前端页面中，把Model用纯JavaScript对象表示，View负责显示，两者做到了最大限度的分离。

把Model和View关联起来的就是ViewModel。ViewModel负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model。

ViewModel如何编写？需要用JavaScript编写一个通用的ViewModel，这样，就可以复用整个MVVM模型了。

一个MVVM框架和jQuery操作DOM相比有什么区别？

我们先看用jQuery实现的修改两个DOM节点的例子：

```
<!-- HTML -->
<p>Hello, <span id="name">Bart</span>!</p>
<p>You are <span id="age">12</span>.</p>
```

Hello, **Bart**!

You are **12**.

用jQuery修改name和age节点的内容：

`'use strict'; ``// 执行代码并观察页面变化 ` Run

如果我们使用MVVM框架来实现同样的功能，我们首先并不关心DOM的结构，而是关心数据如何存储。最简单的数据存储方式是使用JavaScript对象：

```
var person = {
    name: 'Bart',
    age: 12
};
```

我们把变量`person`看作Model，把HTML某些DOM节点看作View，并假定它们之间被关联起来了。

要把显示的name从`Bart`改为`Homer`，把显示的age从`12`改为`51`，我们并不操作DOM，而是直接修改JavaScript对象：

Hello, !

You are .

```javascript
person.name = 'Homer';
person.age = 51;
```

执行上面的代码，我们惊讶地发现，改变JavaScript对象的状态，会导致DOM结构作出对应的变化！这让我们的关注点从如何操作DOM变成了如何更新JavaScript对象的状态，而操作JavaScript对象比DOM简单多了！

这就是MVVM的设计思想：关注Model的变化，让MVVM框架去自动更新DOM的状态，从而把开发者从操作DOM的繁琐步骤中解脱出来！

**VUE也是使用的MVVM设计模式，将M(js对象)和V(html dom)使用MV(VUE核心)双向绑定起来，我们只需要修改js对象数据就可以达到视图动态变化，实现分离。**

## 数据绑定

每个 Vue 应用都需要通过实例化 Vue 来实现:

```javascript
var vm = new Vue({
  // 选项
});
```

来看一个示例：

```html
<div id="vue_det">
    <h1>site : {{site}}</h1>
    <h1>url : {{url}}</h1>
    <h1>{{details()}}</h1>
</div>
<script type="text/javascript">
    var vm = new Vue({
        el: '#vue_det',
        data: {
            site: "mysite",
            url: "www.local.com",
            alexa: "10000"
        },
        methods: {
            details: function() {
                return  this.site + " - 学习使我超痛苦！";
            }
        }
    })
</script>
```

分析：

- Vue构造器里面有一个el属性，表示element的缩写，那么它就表示一个元素，属性值支持css语法，这里是指id为vue_det的元素，此时这个构造器就绑定到div这个元素上边，2.0以后不允许绑定`body`和`html`元素；

- data用于定义数据属性，里面的属性名完全是自定义的，改变属性值会在dom文档中得到体现。关于如何数据绑定到div，下一节学习模板

- methods属性用于定义函数，可以在html模板中直接调用得到返回值

- 另外还有一些钩子函数：created，compiled， ready ，destroyed

  ```javascript
  let vm = new Vue({
      el : "vue_det",
      data : {
          message : "hello"
      },
      created() {
          console.log("created"); // 在实例创建时调用
      }
  });
  ```

  

**el绑定元素，data绑定数据， methods绑定方法**



除了数据属性，Vue 实例还提供了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。例如：

```javascript
var data = { site: "菜鸟教程", url: "www.runoob.com", alexa: 10000}
var vm = new Vue({
    el: '#vue_det',
    data: data
})
 
document.write(vm.$data === data) // true
document.write("<br>") 
document.write(vm.$el === document.getElementById('vue_det')) // true
```

## 模板

Vue.js 使用了基于 HTML 的模版语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。

Vue.js 的核心是一个允许你采用简洁的模板语法来声明式的将数据渲染进 DOM 的系统。

结合响应系统，在应用状态改变时， Vue 能够智能地计算出重新渲染组件的最小代价并应用到 DOM 操作上。

- 文本，使用：

  ```html
  <div id="app">
    <p>{{ message }}</p>
  </div>
  
  <script>
  new Vue({
    el: '#app',
    data: {
      message: 'Hello Vue.js!' // 对应模板中的message
    }
  })
  </script>
  ```

- html，使用 v-html 指令用于输出 html 代码

  ```html
  <div id="app">
      <div v-html="message"></div>
  </div>
  	
  <script>
  new Vue({
    el: '#app',
    data: {
      message: '<h1>菜鸟教程</h1>' // 这个会被解析成html
    }
  })
  </script>
  ```

- 属性，HTML 属性中的值应使用 v-bind 指令，以下实例判断 class1 的值，如果为 true 使用 class1 类的样式，否则不使用该类

  ```html
  
  <style>
  .class1{
    background: #444;
    color: #eee;
  }
  </style>
  
  <div id="app">
    <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
    <br><br>
    <div v-bind:class="{'class1': use}">
      v-bind:class 指令
    </div>
  </div>
      
  <script>
  new Vue({
      el: '#app',
      data:{
        use: false
    }
  });
  </script>
  ```

- 表达式，Vue.js 都提供了完全的 JavaScript 表达式支持

  ```html
  <div id="app">
  	{{5+5}}<br>
  	{{ ok ? 'YES' : 'NO' }}<br>
  	{{ message.split('').reverse().join('') }}
  	<div v-bind:id="'list-' + id">菜鸟教程</div>
  </div>
  	
  <script>
  new Vue({
    el: '#app',
    data: {
  	ok: true,
      message: 'RUNOOB',
  	id : 1
    }
  })
  </script>
  ```

- 指令，指令是带有 v- 前缀的特殊属性。

  指令用于在表达式的值改变时，将某些行为应用到 DOM 上。如下例子：

  ```html
  <div id="app">
      <p v-if="seen">现在你看到我了</p>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      seen: true //这里， v-if 指令将根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素
    }
  })
  </script>
  ```

- 参数，参数在指令后以冒号指明。例如， v-bind 指令被用来响应地更新 HTML 属性：

  ```html
  <div id="app">
      <pre><a v-bind:href="url">菜鸟教程</a></pre>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      url: 'http://www.runoob.com'
    }
  })
  </script>
  ```

  在这里 href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定。

  另一个例子是 v-on 指令，它用于监听 DOM 事件：

  ```html
  <a v-on:click="doSomething">
  ```

- 修饰符，修饰符是以半角句号 **.** 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，**.prevent** 修饰符告诉 **v-on** 指令对于触发的事件调用 **event.preventDefault()**：

  ```html
  <form v-on:submit.prevent="onSubmit"></form>
  ```

- 用户输入，在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定：

  ```html
  <div id="app">
      <p>{{ message }}</p>
      <input v-model="message">
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      message: 'Runoob!'
    }
  })
  </script>
  ```

  **v-model** 指令用来在 input、select、text、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

  按钮的事件我们可以使用 v-on 监听事件，并对用户的输入进行响应。

  点击按钮字符翻转：

  ```html
  <div id="app">
      <p>{{ message }}</p>
      <button v-on:click="reverseMessage">反转字符串</button>
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      message: 'Runoob!'
    },
    methods: {
      reverseMessage: function () {
        this.message = this.message.split('').reverse().join('')
      }
    }
  })
  </script>
  ```

- 过滤器，Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下：

  ```html
  <!-- 在两个大括号中 -->
  {{ message | capitalize }}
  
  <!-- 在 v-bind 指令中 -->
  <div v-bind:id="rawId | formatId"></div>
  ```

  过滤器函数接受表达式的值作为第一个参数。

  以下实例对输入的字符串第一个字母转为大写:

  ```html
  <div id="app">
    {{ message | capitalize }}
  </div>
      
  <script>
  new Vue({
    el: '#app',
    data: {
      message: 'runoob'
    },
    filters: {
      capitalize: function (value) {
        if (!value) return '';
        value = value.toString();
        return value.charAt(0).toUpperCase() + value.slice(1);
      }
    }
  })
  </script>
  ```

  过滤器可以串联：

  ```
  {{ message | filterA | filterB }}
  ```

  过滤器是 JavaScript 函数，因此可以接受参数：

  ```
  {{ message | filterA('arg1', arg2) }}
  ```

  这里，message 是第一个参数，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。

## 语句

上一节提到了`{{ }}`可以支持表达式，但是并不支持语句(语句块？)，语句需要使用命令。

### 条件语句

#### v-if

条件判断使用 v-if 指令:

```html
<div id="app">
    <p v-if="seen">现在你看到我了</p>
    <template v-if="ok">
      <h1>菜鸟教程</h1>
      <p>学的不仅是技术，更是梦想！</p>
      <p>哈哈哈，打字辛苦啊！！！</p>
    </template>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    seen: true,
    ok: true
  }
})
</script>
```

#### v-else

可以用 v-else 指令给 v-if 添加一个 "else" 块：

```html
<div id="app">
    <div v-if="Math.random() > 0.5">
      Sorry
    </div>
    <div v-else>
      Not sorry
    </div>
</div>
    
<script>
new Vue({
  el: '#app'
})
</script>
```

#### v-else-if

v-else-if 在 2.1.0 新增，顾名思义，用作 v-if 的 else-if 块。可以链式的多次使用：

```html
<div id="app">
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    type: 'C'
  }
})
</script>
```

#### v-show

其实和v-if差不多

我们也可以使用 v-show 指令来根据条件展示元素：

```html
<h1 v-show="ok">Hello!</h1>
```

### 循环语句

循环使用 v-for 指令。

v-for 指令需要以 **site in sites** 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。

v-for 可以绑定数据到数组来渲染一个列表：

```html
<div id="app">
  <ol>
    <li v-for="site in sites">
      {{ site.name }}
    </li>
  </ol>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    sites: [
      { name: 'Runoob' },
      { name: 'Google' },
      { name: 'Taobao' }
    ]
  }
})
</script>
```

模板中使用 v-for：

```html
<ul>
  <template v-for="site in sites">
    <li>{{ site.name }}</li>
    <li>--------------</li>
  </template>
</ul>
```

v-for 可以通过一个对象的属性来迭代数据：

```html
<div id="app">
  <ul>
    <li v-for="value in object">
    {{ value }}
    </li>
  </ul>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    object: {
      name: '菜鸟教程',
      url: 'http://www.runoob.com',
      slogan: '学的不仅是技术，更是梦想！'
    }
  }
})
</script>
```

你也可以提供第二个的参数为键名：

```html
<div id="app">
  <ul>
    <li v-for="(value, key) in object">
    {{ key }} : {{ value }}
    </li>
  </ul>
</div>
```

第三个参数为索引：

```html
<div id="app">
  <ul>
    <li v-for="(value, key, index) in object">
     {{ index }}. {{ key }} : {{ value }}
    </li>
  </ul>
</div>
```

v-for 也可以循环整数:

```html
<div id="app">
  <ul>
    <li v-for="n in 10">
     {{ n }}
    </li>
  </ul>
</div>
```

## 计算属性

计算属性关键词: computed。

计算属性在处理一些复杂逻辑时是很有用的。

可以看下以下反转字符串的例子：

```html
<div id="app">
  {{ message.split('').reverse().join('') }}
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'Runoob!'
  }
})
</script>
```

实例 1 中模板变的很复杂起来，也不容易看懂理解。

看看计算属性的实例：

```html
<div id="app">
  <p>原始字符串: {{ message }}</p>
  <p>计算后反转字符串: {{ reversedMessage }}</p>
</div>
 
<script>
var vm = new Vue({
  el: '#app',
  data: {
    message: 'Runoob!'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join(''); // 这里涉及到data里面的哪些属性，就与这些属性相关，这些属性改变后，这个函数会执行
    }
  }
})
</script>
```

实例 2 中声明了一个计算属性 reversedMessage 。

提供的函数将用作属性 vm.reversedMessage 的 getter 。

vm.reversedMessage 依赖于 vm.message，在 vm.message 发生改变时，vm.reversedMessage 也会更新。

### computed vs methods

我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。

```javascript
methods: {
  reversedMessage2: function () {
    return this.message.split('').reverse().join('')
  }
}
```

可以说使用 computed 性能会更好，但是如果你不希望缓存，你可以使用 methods 属性。



computed 属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：

```javascript
var vm = new Vue({
  el: '#app',
  data: {
    name: 'Google',
    url: 'http://www.google.com'
  },
  computed: {
    site: {
      // getter
      get: function () {
        return this.name + ' ' + this.url
      },
      // setter
      set: function (newValue) {
        var names = newValue.split(' ')
        this.name = names[0]
        this.url = names[names.length - 1]
      }
    }
  }
})
// 调用 setter， vm.name 和 vm.url 也会被对应更新
vm.site = '菜鸟教程 http://www.runoob.com';
document.write('name: ' + vm.name);
document.write('<br>');
document.write('url: ' + vm.url);
```

## 监听属性

类似于事件，Vue.js 监听属性 watch，我们可以通过 watch 来响应数据的变化。

以下实例通过使用 watch 实现计数器：

```html
<div id = "app">
    <p style = "font-size:25px;">计数器: {{ counter }}</p>
    <button @click = "counter++" style = "font-size:25px;">点我</button>
</div>
<script type = "text/javascript">
var vm = new Vue({
    el: '#app',
    data: {
        counter: 1
    }
});
vm.$watch('counter', function(nval, oval) {
    alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
});
</script>
```



## 样式绑定

class 与 style 是 HTML 元素的属性，用于设置元素的样式，我们可以用 v-bind 来设置样式属性。

Vue.js v-bind 在处理 class 和 style 时， 专门增强了它。表达式的结果类型除了字符串之外，还可以是对象或数组。

```html
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
</style>

<div id="app">
  <div v-bind:class="{ active: isActive }"></div>
    <!--对象里面可以有多个样式-->
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true // 为true表示有效
  }
})
</script>
```

```html
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
.text-danger {
	background: red;
}
</style>
<div id="app">
  <div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
  </div>
    <!--相当于<div class="static active text-danger"></div>-->
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true,
	hasError: true
  }
})
</script>
```

计算属性：

```html
<div id="app">
  <div v-bind:class="classObject"></div>
</div>
<script>

new Vue({
  el: '#app',
  data: {
    isActive: true,
    error: {
      value: true,
      type: 'fatal'
    }
  },
  computed: {
    classObject: function () {
      return {
  		base: true,
        active: this.isActive && !this.error.value,
        'text-danger': this.error.value && this.error.type === 'fatal',
      }
    }
  }
})
</script>
```

数组：

```html
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
.text-danger {
	background: red;
}
</style>
<div id="app">
	<div v-bind:class="[activeClass, errorClass]"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
})
</script>
```

三元表达式：

```html
<style>
.text-danger {
	width: 100px;
	height: 100px;
	background: red;
}
.active {
	width: 100px;
	height: 100px;
	background: green;
}
</style>
<div id="app">
	<div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true,
	activeClass: 'active',
    errorClass: 'text-danger'
  }
})
</script>
```

内联样式：

```html
<div id="app">
	<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">菜鸟教程</div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    activeColor: 'green',
	fontSize: 30
  }
})
</script>
```

直接来个对象：

```html
<div id="app">
  <div v-bind:style="styleObject">菜鸟教程</div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    styleObject: {
      color: 'green',
      fontSize: '30px'
    }
  }
})
</script>
```



> 其实使用`v-bind`绑定属性非常灵活，可以使用任何数据类型，不过字符串要用单引号，不然会识别成对象（普通变量、数组、函数、对象）。

-------------

## 事件处理器

> 事件监听可以使用 v-on: 指令，简写为@.

可以是表达式或者方法。

```html
<div id="app">
  <button v-on:click="counter += 1">增加 1</button>
  <p>这个按钮被点击了 {{ counter }} 次。</p>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    counter: 0
  }
})
</script>
```

```html
<div id="app">
   <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
 
<script>
var app = new Vue({
  el: '#app',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件，要使用的话需要使用greet($event)
      if (event) {
          alert(event.target.tagName)
      }
    }
  }
})
// 也可以用 JavaScript 直接调用方法
app.greet() // -> 'Hello Vue.js!'
</script>
```

```html
<div id="app">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
 
<script>
new Vue({
  el: '#app',
  methods: {
    say: function (message) {
      alert(message)
    }
  }
})
</script>
```

### 事件修饰符

Vue.js 为 v-on 提供了事件修饰符来处理 DOM 事件细节，如：event.preventDefault() 或 event.stopPropagation()。

Vue.js通过由点(.)表示的指令后缀来调用修饰符。

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`

```html
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>

<!-- click 事件只能点击一次，2.1.4版本新增 -->
<a v-on:click.once="doThis"></a>
```

### 按键修饰符

Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：

```html
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">
```

记住所有的 keyCode 比较困难，所以 Vue 为最常用的按键提供了别名：

```html
<!-- 同上 -->
<input v-on:keyup.enter="submit">
<!-- 缩写语法 -->
<input @keyup.enter="submit">
```

> 全部的按键别名：

- `.enter`
- `.tab`
- `.delete` (捕获 "删除" 和 "退格" 键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`
- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

```html
<p><!-- Alt + C -->
<input @keyup.alt.67="clear">
<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

## 表单

> 我们可以使用`v-model`指令来实现表单控件元素上创建双向数据绑定。
>
> `v-model` 会根据控件类型自动选取正确的方法来更新元素。

![](readme-img/20151109171527_549.png)

### 例子

**输入框**

```html
<div id="app">
  <p>input 元素：</p>
  <input v-model="message" placeholder="编辑我……">
  <p>消息是: {{ message }}</p>
    
  <p>textarea 元素：</p>
  <p style="white-space: pre">{{ message2 }}</p>
  <textarea v-model="message2" placeholder="多行文本输入……"></textarea>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    message: 'Runoob',
    message2: '菜鸟教程\r\nhttp://www.runoob.com'
  }
})
</script>
```

**复选**

```html
<div id="app">
  <p>单个复选框：</p>
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">{{ checked }}</label>
    
  <p>多个复选框：</p>
  <input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
  <label for="runoob">Runoob</label>
  <input type="checkbox" id="google" value="Google" v-model="checkedNames">
  <label for="google">Google</label>
  <input type="checkbox" id="taobao" value="Taobao" v-model="checkedNames">
  <label for="taobao">taobao</label>
  <br>
  <span>选择的值为: {{ checkedNames }}</span>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    checked : false,
    checkedNames: []
  }
})
</script>
```

**单选**

```html
<div id="app">
  <input type="radio" id="runoob" value="Runoob" v-model="picked">
  <label for="runoob">Runoob</label>
  <br>
  <input type="radio" id="google" value="Google" v-model="picked">
  <label for="google">Google</label>
  <br>
  <span>选中值为: {{ picked }}</span>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    picked : 'Runoob'
  }
})
</script>
```

**select**

```html
<div id="app">
  <select v-model="selected" name="fruit">
    <option value="">选择一个网站</option>
    <option value="www.runoob.com">Runoob</option>
    <option value="www.google.com">Google</option>
  </select>
 
  <div id="output">
      选择的网站是: {{selected}}
  </div>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    selected: '' 
  }
})
</script>
```

### 修饰符

`.lazy`

在默认情况下， v-model 在 input 事件中同步输入框的值与数据，但你可以添加一个修饰符 lazy ，从而转变为在 change 事件中同步：

```html
<!-- 在 "change" 而不是 "input" 事件中更新 -->
<input v-model.lazy="msg" >
```

`.number`

如果想自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 number 给 v-model 来处理输入值：

```html
<input v-model.number="age" type="number">
```

这通常很有用，因为在 type="number" 时 HTML 中输入的值也总是会返回字符串类型。

`.trim`

如果要自动过滤用户输入的首尾空格，可以添加 trim 修饰符到 v-model 上过滤输入：

```html
<input v-model.trim="msg">
```

## 组件

> 组件（Component）是 Vue.js 最强大的功能之一。
>
> 组件可以扩展 HTML 元素，封装可重用的代码。
>
> 组件系统让我们可以用独立可复用的小组件来构建大型应用，几乎任意类型的应用的界面都可以抽象为一个组件树：

![](readme-img/components.png)

注册一个全局组件语法格式如下：

```javascript
Vue.component(tagName, options);
```

tagName 为组件名(不能取名为`template`)，options 为配置选项。注册后，我们可以使用以下方式来调用组件：

```html
<tagName></tagName>
```

### 全局组件

> 所有实例都能用全局组件。

```html
<div id="app">
    <runoob></runoob>
</div>
 
<script>
// 注册
Vue.component('runoob', {
  template: '<h1>自定义组件!</h1>'
})
// 创建根实例
new Vue({
  el: '#app'
})
</script>
```

组件类似于定义一个自定义标签，它会被解析为对应的`template`值。

### 局部组件

就是在生成实例时注册：

```html
<div id="app">
    <runoob></runoob>
</div>
 
<script>
var Child = {
  template: '<h1>自定义组件!</h1>'
}
 
// 创建根实例
new Vue({
  el: '#app',
  components: {
    // <runoob> 将只在父模板可用，只能用于id为app下的标签
    'runoob': Child
  }
})
</script>
```

在`.vue`文件里面有一个`<template>`标签，表示这里的`template`属性。

### prop

prop 是父组件用来传递数据的一个自定义属性。

父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：

```html
<div id="app">
    <!-- 这是父组件，这里表示使用child这个子组件，message是要传递给子组件的数据。 -->
    <child message="hello!"></child>
</div>
 
<script>
// 注册
Vue.component('child', {
  // 声明 props
  props: ['message'],  // 数组里面的对象数据是从父组件接受过来的
  // 同样也可以在 vm 实例中像 "this.message" 这样使用
  template: '<span>{{ message }}</span>' // 这是子组件的内容
})
// 创建根实例
new Vue({
  el: '#app'
})
</script>
```

上边的代码表示`<child message="hello!"></child>`会被替换为`<span>{{ message }}</span>`，但是message的值是组件中的mesaage属性值，要将他们绑定起来需要在props中注册。

HTML 中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名：

```html
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

重申一次，如果你使用字符串模板，那么这个限制就不存在了。

指定对象类型：

```javascript
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object
}
```



### 动态prop

类似于用 v-bind 绑定 HTML 特性到一个表达式，也可以用 v-bind 动态绑定 props 的值到父组件的数据中。每当父组件的数据变化时，该变化也会传导给子组件：

```html
<div id="app">
    <div>
      <input v-model="parentMsg">
      <br>
      <child v-bind:message="parentMsg"></child>
    </div>
</div>
 
<script>
// 注册
Vue.component('child', {
  // 声明 props
  props: ['message'],
  // 同样也可以在 vm 实例中像 "this.message" 这样使用
  template: '<span>{{ message }}</span>'
})
// 创建根实例
new Vue({
  el: '#app',
  data: {
    parentMsg: '父组件内容'
  }
})
</script>
```



```html
<div id="app">
    <ol>
    <todo-item v-for="item in sites" v-bind:todo="item"></todo-item>
      </ol>
</div>
 
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
new Vue({
  el: '#app',
  data: {
    sites: [
      { text: 'Runoob' },
      { text: 'Google' },
      { text: 'Taobao' }
    ]
  }
})
</script>
```

### prop验证

组件可以为 props 指定验证要求。

prop 是一个对象而不是字符串数组时，它包含验证要求：

```javascript
Vue.component('example', {
  props: {
    // 基础类型检测 （`null` 意思是任何类型都可以）
    propA: Number,
    // 多种类型
    propB: [String, Number],
    // 必传且是字符串
    propC: {
      type: String,
      required: true
    },
    // 数字，有默认值
    propD: {
      type: Number,
      default: 100
    },
    // 数组／对象的默认值应当由一个工厂函数返回
    propE: {
      type: Object,
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        return value > 10
      }
    }
  }
})
```

type 可以是下面原生构造器：

- String
- Number
- Boolean
- Function
- Object
- Array

type 也可以是一个自定义构造器，使用 instanceof 检测。



### 自定义事件

父组件是使用 props 传递数据给子组件，但如果子组件要把数据传递回去，就需要使用自定义事件！

我们可以使用 v-on 绑定自定义事件, 每个 Vue 实例都实现了事件接口(Events interface)，即：

- 使用 `$on(eventName)` 监听事件
- 使用 `$emit(eventName)` 触发事件

另外，父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件。

以下实例中子组件已经和它外部完全解耦了。它所做的只是触发一个父组件关心的内部事件。

```html
<div id="app">
    <div id="counter-event-example">
      <p>{{ total }}</p>
      <button-counter v-on:increment="incrementTotal"></button-counter>
      <button-counter v-on:increment="incrementTotal"></button-counter>
    </div>
</div>
 
<script>
Vue.component('button-counter', {
  template: '<button v-on:click="incrementHandler">{{ counter }}</button>',
    // 这里是回传，貌似不用定义props
  data: function () {
    return {
      counter: 0 // 这里是定义一个自己的属性
    }
  },
  methods: {
    incrementHandler: function () {
      this.counter += 1
      this.$emit('increment')
    }
  },
})
new Vue({
  el: '#counter-event-example',
  data: {
    total: 0
  },
  methods: {
    incrementTotal: function () {
      this.total += 1
    }
  }
})
</script>
```

如果你想在某个组件的根元素上监听一个原生事件。可以使用 .native 修饰 v-on 。例如：

```html
<my-component v-on:click.native="doTheThing"></my-component>
```

**data 必须是一个函数**

上面例子中，可以看到 button-counter 组件中的 data 不是一个对象，而是一个函数：

```javascript
data: function () {
  return {
    count: 0
  }
}
```

这样的好处就是每个实例可以维护一份被返回对象的独立的拷贝，如果 data 是一个对象则会影响到其他实例，如下所示：

```html
<div id="components-demo3" class="demo">
    <button-counter2></button-counter2>
    <button-counter2></button-counter2>
    <button-counter2></button-counter2>
</div>
 
<script>
var buttonCounter2Data = {
  count: 0
}
Vue.component('button-counter2', {
    /*
    data: function () {
        // data 选项是一个函数，组件不相互影响
        return {
            count: 0
        }
    },
    */
    data: function () {
        // data 选项是一个对象，会影响到其他实例
        return buttonCounter2Data
    },
    template: '<button v-on:click="count++">点击了 {{ count }} 次。</button>'
})
new Vue({ el: '#components-demo3' })
</script>
```

## 自定义指令

除了默认设置的核心指令( v-model 和 v-show ), Vue 也允许注册自定义指令。

下面我们注册一个全局指令 v-focus, 该指令的功能是在页面加载时，元素获得焦点：

```html
<div id="app">
    <p>页面载入时，input 元素自动获取焦点：</p>
    <input v-focus>
</div>
 
<script>
// 注册一个全局自定义指令 v-focus
Vue.directive('focus', {
  // 当绑定元素插入到 DOM 中。
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
// 创建根实例
new Vue({
  el: '#app'
})
</script>
```

我们也可以在实例使用 directives 选项来注册局部指令，这样指令只能在这个实例中使用：

```html
<div id="app">
  <p>页面载入时，input 元素自动获取焦点：</p>
  <input v-focus>
</div>
 
<script>
// 创建根实例
new Vue({
  el: '#app',
  directives: {
    // 注册一个局部的自定义指令 v-focus
    focus: {
      // 指令的定义
      inserted: function (el) {
        // 聚焦元素
        el.focus()
      }
    }
  }
})
</script>
```

### 钩子函数

指令定义函数提供了几个钩子函数（可选）：

- `bind`: 只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。
- `inserted`: 被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于 document 中）。
- `update`: 被绑定元素所在的模板更新时调用，而不论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新（详细的钩子函数参数见下）。
- `componentUpdated`: 被绑定元素所在模板完成一次更新周期时调用。
- `unbind`: 只调用一次， 指令与元素解绑时调用。

钩子函数的参数有：

- **el**: 指令所绑定的元素，可以用来直接操作 DOM 。
- **binding**: 一个对象，包含以下属性：
  - **name**: 指令名，不包括 `v-` 前缀。
  - **value**: 指令的绑定值， 例如： `v-my-directive="1 + 1"`, value 的值是 `2`。
  - **oldValue**: 指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - **expression**: 绑定值的表达式或变量名。 例如 `v-my-directive="1 + 1"` ， expression 的值是 `"1 + 1"`。
  - **arg**: 传给指令的参数。例如 `v-my-directive:foo`， arg 的值是 `"foo"`。
  - **modifiers**: 一个包含修饰符的对象。 例如： `v-my-directive.foo.bar`, 修饰符对象 modifiers 的值是 `{ foo: true, bar: true }`。
- **vnode**: Vue 编译生成的虚拟节点。
- **oldVnode**: 上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

```html
<div id="app"  v-runoob:hello.a.b="message">
</div>

<script>
Vue.directive('runoob', {
  bind: function (el, binding, vnode) {
    var s = JSON.stringify
    el.innerHTML =
      'name: '       + s(binding.name) + '<br>' +
      'value: '      + s(binding.value) + '<br>' +
      'expression: ' + s(binding.expression) + '<br>' +
      'argument: '   + s(binding.arg) + '<br>' +
      'modifiers: '  + s(binding.modifiers) + '<br>' +
      'vnode keys: ' + Object.keys(vnode).join(', ')
  }
})
new Vue({
  el: '#app',
  data: {
    message: '菜鸟教程!'
  }
})
</script>
```

有时候我们不需要其他钩子函数，我们可以简写函数，如下格式：

```javascript
Vue.directive('runoob', function (el, binding) {
  // 设置指令的背景颜色
  el.style.backgroundColor = binding.value.color
})
```

指令函数可接受所有合法的 JavaScript 表达式，以下实例传入了 JavaScript 对象：

```html
<div id="app">
    <div v-runoob="{ color: 'green', text: '菜鸟教程!' }"></div>
</div>
 
<script>
Vue.directive('runoob', function (el, binding) {
    // 简写方式设置文本及背景颜色
    el.innerHTML = binding.value.text
    el.style.backgroundColor = binding.value.color
})
new Vue({
  el: '#app'
})
</script>
```

## 路由

Vue.js 路由允许我们通过不同的 URL 访问不同的内容。

通过 Vue.js 可以实现多视图的单页Web应用（single page web application，SPA）。

Vue.js 路由需要载入 [vue-router 库](https://github.com/vuejs/vue-router)

中文文档地址：[vue-router文档](http://router.vuejs.org/zh-cn/)。

### 安装

- ```
  https://unpkg.com/vue-router/dist/vue-router.js
  ```

- ```shell
  cnpm install vue-router
  ```

### 简单示例

Vue.js + vue-router 可以很简单的实现单页应用。

**`<router-link>`** 是一个组件，该组件用于设置一个导航链接，切换不同 HTML 内容。 **to** 属性为目标地址， 即要显示的内容。

以下实例中我们将 vue-router 加进来，然后配置组件和路由映射，再告诉 vue-router 在哪里渲染它们。代码如下所示：

```html
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>

<script>
// 0. 如果使用模块化机制编程，導入Vue和VueRouter，要调用 Vue.use(VueRouter)

// 1. 定义（路由）组件。
// 可以从其他文件 import 进来
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由
// 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，
// 或者，只是一个组件配置对象。
// 我们晚点再讨论嵌套路由。
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. 创建 router 实例，然后传 `routes` 配置
// 你还可以传别的配置参数, 不过先这么简单着吧。
const router = new VueRouter({
  routes // （缩写）相当于 routes: routes
})

// 4. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，
// 从而让整个应用都有路由功能
const app = new Vue({
  router
}).$mount('#app')

// 现在，应用已经启动了！
</script>
```

### `<router-link>` 相关属性

#### to

表示目标路由的链接。 当被点击后，内部会立刻把 to 的值传到 router.push()，所以这个值可以是一个字符串或者是描述目标位置的对象。

```html
<!-- 字符串 -->
<router-link to="home">Home</router-link>
<!-- 渲染结果 -->
<a href="home">Home</a>

<!-- 使用 v-bind 的 JS 表达式 -->
<router-link v-bind:to="'home'">Home</router-link>

<!-- 不写 v-bind 也可以，就像绑定别的属性一样 -->
<router-link :to="'home'">Home</router-link>

<!-- 同上 -->
<router-link :to="{ path: 'home' }">Home</router-link>

<!-- 命名的路由 -->
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>
```

#### replace

设置 replace 属性的话，当点击时，会调用 router.replace() 而不是 router.push()，导航后不会留下 history 记录。

```html
<router-link :to="{ path: '/abc'}" replace></router-link>
```

#### append

设置 append 属性后，则在当前 (相对) 路径前添加基路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

```html
<router-link :to="{ path: 'relative/path'}" append></router-link>
```

#### tag

有时候想要 `<router-link>` 渲染成某种标签，例如 `<li>`。 于是我们使用 `tag` prop 类指定何种标签，同样它还是会监听点击，触发导航。

```html
<router-link to="/foo" tag="li">foo</router-link>
<!-- 渲染结果 -->
<li>foo</li>
```

#### active-class

设置 链接激活时使用的 CSS 类名。可以通过以下代码来替代。

```html
<style>
   ._active{
      background-color : red;
   }
</style>
<p>
   <router-link v-bind:to = "{ path: '/route1'}" active-class = "_active">Router Link 1</router-link>
   <router-link v-bind:to = "{ path: '/route2'}" tag = "span">Router Link 2</router-link>
</p>
```

注意这里 **class** 使用 **active_class="_active"**。

#### exact-active-class

配置当链接被精确匹配的时候应该激活的 class。可以通过以下代码来替代。

```html
<p>
   <router-link v-bind:to = "{ path: '/route1'}" exact-active-class = "_active">Router Link 1</router-link>
   <router-link v-bind:to = "{ path: '/route2'}" tag = "span">Router Link 2</router-link>
</p>
```

#### event

声明可以用来触发导航的事件。可以是一个字符串或是一个包含字符串的数组。

```html
<router-link v-bind:to = "{ path: '/route1'}" event = "mouseover">Router Link 1</router-link>
```

以上代码设置了 event 为 mouseover ，及在鼠标移动到 Router Link 1 上时导航的 HTML 内容会发生改变。

## 关于动画和过渡

[动画和过渡](http://www.runoob.com/vue2/vue-transitions.html)







核心在于vm数据方法绑定，十分灵活，另外提供高度支持js的表达式与语句，提供ajax，事件等特性方法。



# 关于express

[参考手册](http://www.runoob.com/w3cnote/express-4-x-api.html)

# webpack

[参考手册](https://www.webpackjs.com/concepts/)