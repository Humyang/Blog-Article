layout: [post]
title: Webpack 入门
date: 2016-01-03 22:32:03
tags:
- 前端
categories:
- 前端
- 工具
---

跟着官网入门文章过了一遍。

<!-- more -->


---
Webpack 官网入门

[地址](http://webpack.github.io/docs/motivation.html)

# 作用

现在的网站都朝着 web app 发展：

* 页面中越来越多的 JavaScript。
* 可以在现在浏览器做更多事情。
* 更少的整个页面重载，尽管页面中的代码更多了。

这些原因导致了在客户端存在大量代码！

太大的代码库需要进行组织。Module 系统能让你将代码库分隔为不同模块。

## MODULE SYSTEM STYLES

这里有几种标准，定义模块之间如何依赖和导出值：

* `script` 标签 (无 module system)
* CommonJS
* AMD 和它的一些方言
* ES6 modules
* 更多

### `script` 标签

如果你不使用 module system 那么你会使用这种方式模块化处理你的代码库。

```javascript

<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="libraryA.js"></script>
<script src="module3.js"></script>


```

Module 导出一个接口到全局对象，即 `window` 对象。Modules 可以依赖通过全局对象访问该接口。

常见的问题：

* 全局对象之间冲突
* 加载的顺序是非常重要的
* 需要由开发者解决 modules/libraries 之间的依赖
* 在大型项目中列表过长导致难以管理

### CommonJS:同步的 `require`

这种方式使用同步的 `require` 方法加载依赖和返回一个 exported interface。module 可以通过添加一个属性到 `exports` 对象进行指定 exports，或者设置 `module.exports` 的值。

```javascript

require("module");
require("../file.js");
exports.doStuff = function() {};
module.exports = someValue;

```

这被用在 `node.js` 的服务端。

优点

* 服务端 modules 可以重用
* 有大量的 module 使用这种方式 (npm)
* 非常简单易用

缺点：

* 堵塞调用不适合在网络使用，网络请求是异步的。
* 多个 module 的 require 不是并行的。

实现

[node.js](https://nodejs.org/en/) 服务端
[browserify]()
[modules-webmake]()
[wreq]() 客户端

### AMD:asynchronous require

[Asynchronous Module Definition](https://github.com/amdjs/amdjs-api/wiki/AMD)

其它 module 系统 (浏览器方面) 同步 `require` (CommonJs) 时会有一些问题，现在来介绍一个异步加载的版本 (和定义 modules 和导出值的方式):

```javascript

require(["module", "../file"], function(module, file) { /* ... */ });
define("mymodule", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});

```

优点：

* 适合网络使用的异步加载方式
* 多个模块之间并行加载

缺点：

* 代码开销大，相对较难阅读和书写。
* 看起来像某种变通方法。

实现：

* require.js 客户端
* curl 客户端

了解更多 [CommonJs](http://webpack.github.io/docs/commonjs.html) 和 [AMD](http://webpack.github.io/docs/amd.html)。

### ES6 modules

EcmaScript6 添加了一些语言构造方法到 JavaScript，形成了另一个 module system。

```javascript

import "jquery";
export function doStuff() {}
module "localModule" {}

```

优点

* 静态分析非常简单
* 作为 ES 标准，面向未来。

不足

* 浏览器原生支持还需要时间
* 提供这种方式的模块太少

### 中立的解决方案

让开发者自行选择 module 方式。让已有的代码正常工作，也能简单的添加自定义加载 module 方式。

## 传输

Modules 应该在客户端执行，因此它们必须从服务器传输到浏览器。

这里有两个传递 modules 的方式：

* 每个 module 对应 1 个 request
* 所有 modules 合并到一个 request

这两种方式都是可以使用的，但存在优先级：

1 requrest 对应一个 module：

* 优点：只用传输需要的 modules
* 不足：过多 request 意味着大量开销
* 不足：减慢应用程序启动时间，因为太多请求。

所有 modules 合并在一个 request：

优点：最少的 request 开销，最少的延迟
不足：不需要的 modules 也同时被传输

### 分块传输

获取这两种方式之间的长处是更灵活的传输方式并且效果更好。

在编译所有模块时，分割所有 modules set 到多个更小 batches(chunk)。

我们会得到更多更小的请求，Module Chunk 不需要被初始化，只有需要时才被请求。

初始化的请求不会返回所有代码库因此更小。

## 为什么只有 JavaScript？

为什么 module system 只能帮助开发者处理 JavaScript？还有很多静态资源需要处理：

* 样式表
* 图片
* web 字体
* html 模版
* 等等

还有其它

* coffeescript → JavaScript
* less stylesheets → css stylesheets
* jade templates → javascript which generates html
* i18n files → something
* 等等。

它们应该可以简单的加载:

```css
require("./style.css");
require("./style.less");
require("./template.jade");
require("./image.png");
```

## 静态分析

当编译所有 module 时会尝试进行静态分析找到所有依赖。

传统方式只能简单的查找，不能通过表达式匹配，并且 `require("./template/" + templateName + ".jade")` 也是一种常用的构造方式却不支持。

许多链接库的依赖写法风格都不一样，有的写法相当怪异。

### 策略

智能解析可以保证大部分现有的代码可以运行。如果开发者使用一些怪异的写法那么它会尝试找到最兼容的解决方案。


# 为什么又需要另一个 module 打包工具？

已有的 module 打包工具不适合对较大的项目使用 (较大的单页面应用程序)。最重要的原因是对于代码打包工具来说代码分割和静态资源应该可以通过模块化完美结合。

作者尝试了所有现有的打包工具，但都无法同时满足这些条件。

## 目标

* 分割文件依赖树结构分配到不同块，根据需求加载内容。
* 保持快速的初始加载时间
* 每个静态资源都可以通当作 module 加载
* 可以将第三方链接裤整合成 module
* 能够自定义几乎所有的 module bundler 部分
* 适用于大型项目

## webpack 有什么不同？

### Code Splitting

webpack 在依赖关系树中有两种类型的依赖：同步和异步。异步依赖意根据分割点将资源分割成不同 chunk，之后 chunk tree 会优化，文件会被每个关联的 chunk 触发。

### Loaders

webpack 只能处理本地的 JavaScript，但使用 Loader 可以转换其它资源到 JavaScript 中，因此所有资源都可以当作模块加载。

### 智能解析

webpack 可以智能解析几乎所有的第三方库。它甚至能根据这样的表达时解析依赖 `require("./templates/" + name + ".jade")`。它也能出来大部分常用的 module 方式 CommonJS 和 AMD。

### Plugin system

webpack 拥有丰富的插件系统。大部分内置的功能都依赖于插件系统，它让你根据需要自定义 webpack 和作为开源代码分发常用组件。


# 使用 Loader

## 什么是 Loader？

Loader 可以对应用程序需要的资源进行转换。它们是一个 function (运行在 Node.js),把资源文件的来源作为参数传递给该 function ，然后返回一个新的来源。

例如，你可以使用 loader 告诉 webpack 如何加载 CoffeeScript 或 JSX。


### Loader 的功能

* Loader 可以链式使用，它们以管道的形式对处理资源。最后的 Loader 会返回 JavaScript，其它的 Loader 可以返回任意格式 (将会传递给下一个 Loader)。
* Loader 可以是同步或异步的。
* Loader 是运行在 node.js 所有能做的 node.js 能做的所有事情。
* Loader 接受查询参数。可以通过参数传递配置信息给 loader。
* 可以在配置文件通过 extension/RegExps 绑定 Loader。
* Loader 可以通过 `npm` 发布和安装。
* 正常的 module 除了 export `main` 之外还可以额外的 export loader，通过在 `package.json` 对 `loader` 配置。
* Loader 可以访问配置文件。
* Plguin 可以给 loader 更多功能。
* Loader 可以触发任意额外的文件。
* [其它](http://webpack.github.io/docs/loaders.html)


## 解析 Loader

解析 Loader 的方式[与 module 类似]()。loader module 期望需要导出一个 function 并且可以兼容 node.js 和 JavaScript。大部分情况由你管理着 npm 中的 loader，但你也可以作为文件在你的 app 加载 loader。

### 引用 loader

按照惯例，虽然不是必须的，loader 通常被命名为 `XXX-loader`，`XXX` 是上下文名称，例如 `json-loader`。

你可以使用全名进行引用 (`json-loader`) 或者缩略名 (`json`)。

Loader 的命名约定和优先权搜索顺序是定义在 webpack 配置 API  resolveLoader.moduleTemplates 中。

Loader 命名约定可能很有用，特别在 `require()` 声明内引用；见下面的用法章节。

### 安装 loader

如果 loader 可以在 npm 使用，你可以通过下面方式安装：

```javascript

$ npm install xxx-loader --save

```

或

```javascript

$ npm install xxx-loader --save-dev

```


## 用法

这里有几种用法：

* 明确使用 `require` 声明
* 通过配置文件配置
* 通过 CLI

### 使用 `require`

> 注意：避免使用这个方式，如果你的 script 打算与环境无关 (node.js 和 browser)。使用配置文件的公约来指定 loaders (见下章)。

可以通过 `require` (或 `define`，`require.ensure` 等)声明指定 loader。只需要通过 `!` 分割每一个 loader。每一个部分都会按照当前目录解析。

```javascript

require("./loader!./dir/file.txt");
// => 使用当前目录的 "loader.js" 转换
//   dir 目录的 "file.txt".

require("jade!./template.jade");
// => 使用 "jade-loader" (通过 npm 安装到 "node_modules")
//    转换 "template.jade" 文件

require("!style!css!less!bootstrap/less/bootstrap.less");
// => "bootstrap" 模块中 (通过 npm 安装) less 目录的文件 "bootstrap.less" 回通过 "less-loader" 转换。结果然后经过 "css-loader" 接着经过 style-less 转换。

```

### 配置文件方式

你可以通过配置正则表达式绑定 loader：

```javascript

{
    module: {
        loaders: [
            { test: /\.jade$/, loader: "jade" },
            // => "jade" loader 会对 ".jade" 文件使用

            { test: /\.css$/, loader: "style!css" },
            // => "style" and "css" loader is used for ".css" files
            // Alternative syntax:
            { test: /\.css$/, loaders: ["style", "css"] },
        ]
    }
}

```

### CLI 方式

你可以通过 CLI 拓展绑定 loader：

```javascript

$ webpack --module-bind jade --module-bind 'css=style!css'

```

这里使用 `jade` loader 操作 .jade 文件和使用 `style`,`css` loader 操作 .css 文件。


## 查询参数

Loader 可以通过查询字符串传递查询参数 (就像 web 一样)。查询字符串附加在 loader 的 `?` 后面，如 `url-loader?mimetype=image/png`。

注意：查询字符串的格式由具体 loader 决定，请看 loader 的文档。大部分 loader 都接受正常的查询格式 (`?key=value&key2=value2`) 和 JSON 对象 (`?{"key":"value","key2":"value2"}`)。

### 在 `require`

```javascript

require("url-loader?mimetype=image/png!./file.png");

```

### 在配置文件

```javascript

{ test: /\.png$/, loader: "url-loader?mimetype=image/png" }

```

或

```javascript

{
    test: /\.png$/,
    loader: "url-loader",
    query: { mimetype: "image/png" }
}

```

### CLI

```javascript

webpack --module-bind "png=url-loader?mimetype=image/png"

```

# 使用 Plugins

## 内置的 plugin

通过在 webpack 配置使用 plugin 属性可以使 plugin 包含在你的 module 中。

```javascript

// webpack should be in the node_modules directory, install if not.
var webpack = require("webpack");

module.exports = {
    plugins: [
        new webpack.ResolverPlugin([
            new webpack.ResolverPlugin.DirectoryDescriptionFilePlugin("bower.json", ["main"])
        ], ["normal", "loader"])
    ]
};

```

## 其它 plugins

其它非内置 plugin 如果已经发布则可以通过 npm 安装，如果没有也可以通过其它方式：

```javascript

npm install component-webpack-plugin

```

然后这样使用：

```javascript

var ComponentPlugin = require("component-webpack-plugin");
module.exports = {
    plugins: [
        new ComponentPlugin()
    ]
}

```

# 入门例子

> webpack 将会为你的 entry file 分析对其它文件的依赖。这些文件 (称为 module) 也会被包含到你的 `bundle.js` 文件中。webpack 将会给每个 module 单独的 `id`，并通过 id 使保存所有在 `bundle.js` 中的文件方便的访问。只有 entry module 会在启动时执行。这个小型的 runtime 提供了 `require` function 并在需要时执行依赖关系。

## 第一个 Loader

webpack 只能处理原生 JavaScript，因此我们需要 `css-loader` Loader 处理 CSS 文件。我们也需要 style-loader 在 CSS 文件应用样式。

运行 `npm install css-loader style-loader` 安装 loader (需要安装在本地路径，不要使用 `-g` 参数)。

通过将 Loader 的前缀传递给 module request，loader 会以管道形式处理。这些 loader 会以特定方式转换文件内容。这些转换完成后，最终会返回一个 JavaScript module 的结果。

## 绑定 Loader

我们不想写太长的 requires `require("!style!css!./style.css");`。
我们可以灵活的绑定 extensions 到 loaders 因此我们只需要写 `require("./style.css");`

```javascript

//1.12.9 版本运行失败，官网是 1.12.2 版本，未仔细查原因，已跳过。
webpack ./entry.js bundle.js --module-bind "css=style!css"


```

## 配置文件

我们像将配置选项移动到配置文件：

添加 webpack.config.js:

```javascript

module.exports = {
    entry: "./entry.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    module: {
        loaders: [
            { test: /\.css$/, loader: "style!css" }
        ]
    }
};

```

现在只需要运行

```javascript

webpack

```

webpack 命令将会尝试在当前目录寻找 `webpack.config.js`。

## 美化输出

一些项目编译的输出内容可能很久，因此我们想显示一些进度条，和一些颜色。。

我么可以这样做

```javascript

webpack --progress --colors

```

## 观察模式

我们不想每次更改之后手动重新编译。

```javascript

webpack --progress --colors --watch

```

webpack 可以缓存未更改的 module 和输出更改文件之间的差异。

当使用 watch mode，webpack 安装 file watcher 到所有文件，它会在编译过程中被使用。如果触发任意更改，它会重新运行编译。当缓存是启用时，webpack 会在内存保持每个 module 并且如果它没发生更改会重新使用它。

## 开发服务器

开发服务器甚至更好。

```javascript

npm install webpack-dev-server -g

```

```javascript

webpack-dev-server --progress --colors

```

这样会绑定一个小型的 express 服务在 localhost:8080，这个服务让你访问静态资源文件以及 bundle。它会在 bundle 重新编译时 (socket.io) 自动更新浏览器页面。

> dev server 使用了 webpack 的 watch mode。它也防止 webpack 触发更新文件到磁盘，它仍然保持从内存提取生成的文件。


## 其它

## webpack 与 webpack-dev-server

在练习 entryponits 时，一直用的是 webpack-dev-server 命令，发现不会在目录下生成文件，却直接能在 locakhost:8080 直接使用编译后的文件。而把命令改成 webpack 后，发现在目录下生成了各自的文件。

webpack.config.js

```javascript

module.exports = {
	// entry:"./entry.js",
entry: {
    bundle1: './entry.js',
    bundle2: './entry2.js'
  },
  output: {
    path: __dirname,
    filename: '[name].js' // 模版基于上边 entry 的 key
  },
	// output:{
	// 	path:__dirname,
	// 	filename:"bundle.js"
	// },
	module:{
		loaders:[
			{test:/\.css$/,loader:"style!css"}
		]
	}
};

```

使用 webpack-dev-server 时，每次更改 js 文件后，浏览器会自动刷新网站。
