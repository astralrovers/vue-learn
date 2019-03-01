# `VUE-CLI`

## 简介

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，提供：

- 通过 `@vue/cli` 搭建交互式的项目脚手架。
- 通过 `@vue/cli` + `@vue/cli-service-global` 快速开始零配置原型开发。
- 一个运行时依赖  (`@vue/cli-service`)，该依赖：
  - 可升级；
  - 基于 webpack 构建，并带有合理的默认配置；
  - 可以通过项目内的配置文件进行配置；
  - 可以通过插件进行扩展。
- 一个丰富的官方插件集合，集成了前端生态中最好的工具。
- 一套完全图形化的创建和管理 Vue.js 项目的用户界面。

Vue CLI 致力于将 Vue 生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注在撰写应用上，而不必花好几天去纠结配置的问题。与此同时，它也为每个工具提供了调整配置的灵活性，无需 eject。

## 安装

```shell
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

看版本：

```shell
vue --version
```

## 快速开发

你可以使用 `vue serve` 和 `vue build` 命令对单个 `*.vue` 文件进行快速原型开发，不过这需要先额外安装一个全局的扩展：

```shell
npm install -g @vue/cli-service-global
```

`vue serve` 的缺点就是它需要安装全局依赖，这使得它在不同机器上的一致性不能得到保证。因此这只适用于快速原型开发。

[细节参考](https://cli.vuejs.org/zh/guide/prototyping.html)

## 创建项目

```shell
vue create hello-world
```

这里默认使用的是`npm`，很慢，需要设置源：

```shell
npm config set registry https://registry.npm.taobao.org
```

### `preset`

这是对于一些基本配置，可以选择默认的，也可以手动选择，可以保存下来：

> ~/.vuerc
>
> 被保存的 preset 将会存在用户的 home 目录下一个名为 `.vuerc` 的 JSON 文件里。如果你想要修改被保存的 preset / 选项，可以编辑这个文件。
>
> 在项目创建的过程中，你也会被提示选择喜欢的包管理器或使用[淘宝 npm 镜像源](https://npm.taobao.org/)以更快地安装依赖。这些选择也将会存入 `~/.vuerc`。

### 图形化界面

```shell
vue ui
```

```shell
cd hello
npm run serve # 运行
```

提示：

```shell
 DONE  Compiled successfully in 7631ms                                                                                                                                 9:17:07 AM


  App running at:
  - Local:   http://localhost:8080/
  - Network: http://10.7.6.76:8080/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
```

### 插件

Vue CLI 使用了一套基于插件的架构。如果你查阅一个新创建项目的 `package.json`，就会发现依赖都是以 `@vue/cli-plugin-` 开头的。插件可以修改 webpack 的内部配置，也可以向 `vue-cli-service` 注入命令。在项目创建的过程中，绝大部分列出的特性都是通过插件来实现的。



每个 CLI 插件都会包含一个 (用来创建文件的) 生成器和一个 (用来调整 webpack 核心配置和注入命令的) 运行时插件。当你使用 `vue create` 来创建一个新项目的时候，有些插件会根据你选择的特性被预安装好。如果你想在一个已经被创建好的项目中安装一个插件，可以使用 `vue add` 命令：

```shell
vue add @vue/eslint
```

>提示
>
>`vue add` 的设计意图是为了安装和调用 Vue CLI 插件。这不意味着替换掉普通的 npm 包。对于这些普通的 npm 包，你仍然需要选用包管理器。
>
>警告
>
>我们推荐在运行 `vue add` 之前将项目的最新状态提交，因为该命令可能调用插件的文件生成器并很有可能更改你现有的文件。

这个命令将 `@vue/eslint` 解析为完整的包名 `@vue/cli-plugin-eslint`，然后从 npm 安装它，调用它的生成器。

```sh
# 这个和之前的用法等价
vue add @vue/cli-plugin-eslint
```



`vue-router` 和 `vuex` 的情况比较特殊——它们并没有自己的插件，但是你仍然可以这样添加它们：

```shell
vue add router
vue add vuex
```

> 提示
>
> 如果出于一些原因你的插件列在了该项目之外的其它 `package.json` 文件里，你可以在自己项目的 `package.json` 里设置 `vuePlugins.resolveFrom` 选项指向包含其它 `package.json` 的文件夹。
>
> 例如，如果你有一个 `.config/package.json` 文件：
>
> ```json
> {
>   "vuePlugins": {
>     "resolveFrom": ".config"
>   }
> }
> ```
>
> 

如果你需要在项目里直接访问插件 API 而不需要创建一个完整的插件，你可以在 `package.json` 文件中使用 `vuePlugins.service` 选项：

```json
{
  "vuePlugins": {
    "service": ["my-commands.js"]
  }
}
```

每个文件都需要暴露一个函数，接受插件 API 作为第一个参数。关于插件 API 的更多信息可以查阅[插件开发指南](https://cli.vuejs.org/zh/dev-guide/plugin-dev.html)。

你也可以通过 `vuePlugins.ui` 选项添加像 UI 插件一样工作的文件：

```json
{
  "vuePlugins": {
    "ui": ["my-ui.js"]
  }
}
```

### 几个命令

可以通过`package.json`来查看：

```json
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  }
```

可以通过`npm`来调用他们：

```shell
npm run serve # 启动服务
npm run build 
npm run lint
```

`vue-cli-service build` 会在 `dist/` 目录产生一个可用于生产环境的包，带有 JS/CSS/HTML 的压缩，和为更好的缓存而做的自动的 vendor chunk splitting。它的 chunk manifest 会内联在 HTML 里。

这里还有一些有用的命令参数：

- `--modern` 使用[现代模式](https://cli.vuejs.org/zh/guide/browser-compatibility.html#%E7%8E%B0%E4%BB%A3%E6%A8%A1%E5%BC%8F)构建应用，为现代浏览器交付原生支持的 ES2015 代码，并生成一个兼容老浏览器的包用来自动回退。
- `--target` 允许你将项目中的任何组件以一个库或 Web Components 组件的方式进行构建。更多细节请查阅[构建目标](https://cli.vuejs.org/zh/guide/build-targets.html)。
- `--report` 和 `--report-json` 会根据构建统计生成报告，它会帮助你分析包中包含的模块们的大小。

### 文件结构

```shell
├── babel.config.js
├── node_modules
├── package.json
├── public
├── README.md
├── src
```

`public`:

```shell
├── favicon.ico
└── index.html
```

`src`:

```shell
├── App.vue
├── assets
│   └── logo.png
├── components
│   └── HelloWorld.vue
└── main.js
```

简单说明下这些文件：

- `public`是用来存放静态资源的

  - index.html是入口文件:

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <link rel="icon" href="<%= BASE_URL %>favicon.ico">
        <title>hello</title>
      </head>
      <body>
        <noscript>
          <strong>We're sorry but hello doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
        </noscript>
        <div id="app"></div>
        <!-- built files will be auto injected -->
      </body>
    </html>
    ```

    不过它是一个模板文件，这里的app会被vue里的实例渲染替换([html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin))。

- `src`是源码，也是核心

  - main.js会被index.html使用

    ```javascript
    import Vue from 'vue'
    import App from './App.vue'
    
    Vue.config.productionTip = false
    
    new Vue({
      render: h => h(App),
    }).$mount('#app') // 对应html里的id - app
    ```

  - `App.vue`是主组件，它会调用其他子组件：

    ```vue
    <template>
      <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
      </div>
    </template>
    
    <script>
    import HelloWorld from './components/HelloWorld.vue'
    
    export default {
      name: 'app',
      components: {
        HelloWorld  // 注册这个子组件 ==> "HelloWorld" : HelloWorld
      }
    }
    </script>
    
    <style>
    #app {
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
      margin-top: 60px;
    }
    </style>
    ```

  - `HelloWorld.vue`就是一个子组件实例，

    ```vue
    <script>
    export default {
      name: 'HelloWorld',
      props: {
        msg: String
      }
    }
    </script>
    ```

  - 注意这里的组件不用定义`template`属性，因为vue文件里有`template`这个标签来替换

### 注意

前面的`index.html`没有引用`main.js`，那他们是怎么联系起来的呢，这里的话是使用了`webpack`来管理的：

```shell
vue inspect > output.js
```

里面有：

```javascript
plugins: [
    /* config.plugin('vue-loader') */
    new VueLoaderPlugin(),
    /* config.plugin('define') */
    new DefinePlugin(
        {
            'process.env': {
                NODE_ENV: '"development"',
                BASE_URL: '"/"'
            }
        }
    ),
    ...
      /* config.plugin('hmr') */
      new HotModuleReplacementPlugin(),
      /* config.plugin('progress') */
      new ProgressPlugin(),
      /* config.plugin('html') */
      new HtmlWebpackPlugin(
        {
          templateParameters: function () { /* omitted long function */ },
          template: '/mnt/f/github/vue-learn/vue-cli/hello/public/index.html'
        }
      ),
          /* config.plugin('copy') */
      new CopyWebpackPlugin(
        [
          {
            from: '/mnt/f/github/vue-learn/vue-cli/hello/public',
            to: '/mnt/f/github/vue-learn/vue-cli/hello/dist',
            toType: 'dir',
            ignore: [
              '.DS_Store'
            ]
          }
        ]
      )

    entry: {
      app: [
        './src/main.js'
      ]
    }

```

[参考](https://github.com/jantimon/html-webpack-plugin)

## `HTML`和静态资源

对于上一节最后面的内容，官方文档也在[指南](https://cli.vuejs.org/zh/guide/html-and-static-assets.html#index-%E6%96%87%E4%BB%B6)里提到。