
layout: [post]
title: 关于 Babel 6 你需要知道的 6 件事情
date: 2016-01-03 22:29:18
tags: 
- 前端
categories: 
- 前端
- 工具
---

快速了解 Babel 6 和 Babel 5 之间的区别。

<!-- more -->


---

[原文地址](http://jamesknelson.com/the-six-things-you-need-to-know-about-babel-6/)

# 关于 Babel 6 你需要知道的 6 件事情

> Over the last year, Babel has become the go-to tool for transforming ES2015 and JSX into boring old JavaScript. But seemingly overnight, Babel 6 changed everything. The babel package was deprecated, running babel doesn’t actually transform ES2015 to ES5, and the old docs have basically disappeared.

在过去的一年，Babel 变成了最流行的将 ES2015 和 JSX 转换成旧 JavaScript 的工具。但似乎一夜之间，Babel 6 更改了一切。`babel` 包已经被移除，运行 babel 不会将 ES2015 转换成 ES5，并且旧的文档基本已经消失了。

> But Don’t Panic! To get you up to speed, I’ve put together a brief list of the six most important changes. And if you need a little more help, my Complete Guide to ES6 with Babel 6 will walk you through the practical details; including the CLI, Webpack, Mocha and Gulp.

但是不要惊慌，为了让你加快速度，我挑出了 6 个最重要的更改进行简要说明，如果你需要更多帮助，我的 [Complete Guide to ES6 with Babel 6](http://jamesknelson.com/the-complete-guide-to-es6-with-babel-6/) 会讲解实用的详细细节；包含 CLI，Webpack，Mocha 和 Gulp。

> 1.The `babel` npm package no longer exists. Instead, Babel has been split into multiple packages:

> * babel-cli, which contains the babel command line interface
> * babel-core, which contains the Node API and require hook
> * babel-polyfill, which when required, sets you up with a full ES2015-ish environment

> To avoid accidental conflicts, make sure to remove any previous Babel packages like babel, babel-core, etc. from your package.json, and then npm uninstall them.

1.**`babel` npm 包已经不存在**。作为替代，Babel 已经分割成多个包：

[babel-cli](),包含 babel 命令行接口。
[babel-core]()，包含 Node API 和 `require` hook
[babel-polyfill](),当 `require` d (漏了内容？)，为你设置 ES2015 需要的完整环境。

为了避免冲突，请你在 `package.json` 移除之前的 babel 包例如 babel,babel-core 等。然后运行 `npm uninstall` 卸载它们。


> 2.Every single transform is now a plugin, including ES2015 and JSX. And as a result, nothing happens by default – so you’ll need to install the correct plugins. Actually, ES2015 consists of about 20 plugins. You don’t want to install each of these manually, which is why Babel has added presets.

2.**每个单独的转换现在都以 plugin 形式出现，包括 ES2015 和 JSX**。因此，默认的 bable 什么都不发生 － 因此你需要正确的安装 plguin。但实际上，ES2015 包含了大约 20 个plugin。你不会想手动安装它们的，因此 Babel 添加了 presets 的概念。

> 3.Babel 6 adds presets, or collections of plugins. And it provides two presets for the functionality provided by default in Babel 5:

>   `npm install babel-preset-es2015 babel-preset-react --save-dev`
>   
> But even after installing a preset, you need to tell Babel to use it.
 
3.**Babel 6 增加了 preset，或 plugin 集合**。它提供了两个 Babel 5 默认提供的功能：

`npm install babel-preset-es2015 babel-preset-react --save-dev`

但即使安装了 preset 之后，你仍需要告诉 Babel 使用它。



> 4.`.babelrc` is kinda a necessity now. Since Babel no longer uses ES2015 and React transforms by default, the require hook used by gulpfile.babel.js and mocha will not actually do anything. Fix this by creating a .babelrc in your project directory:

```javascript

{
  "presets": ["es2015", "react"]
}

```


`.babelrc` 现在是**有点必要性**，自从 Babel 默认不具备 ES2015 和 React 转换，`gulpfile.babel.js` 和 [mocha]() 中通过 `require` hook 使用 Babel，不会进行任何操作。要修复这个问题请在你的项目目录创建一个 `.babelrc` 文件，包含这些内容：

```javascript

{
  "presets": ["es2015", "react"]
}

```

> 5.Stage 0 is now a separate preset, not an option. Previously, you enabled ES7 features like decorators and async/await by passing --stage 0 to babel. Now, you install and load the babel-preset-stage-0 package.

**Stage 0 现在是单独的 preset，不再是一个选项**。以前，通过传递 --stage 0 给 babel 启用 ES7 的功能例如修饰符和 `async`/`await`。现在你需要安装和加载 `babel-preset-stage-0` 包。


> 6.The --external-helpers option is now a plugin. To avoid repeated inclusion of Babel’s helper functions, you’ll now need to install and apply the babel-plugin-transform-runtime package, and then require the babel-runtime package within your code (yes, even if you’re using the polyfill).

`-external-helpers` 选项现在是 plugin。为了避免反复包含 Babel 的 helper function，你现在需要安装和应用 `babel-plugin-transform-runtime` 包，然后 require `babel-runtion` 包到你的代码中 (是的，即使你在使用 polyfill)。


> And there you have it, you’re now up to speed on Babel 6’s packages, plugins, presets and options! But what about Webpack? What about passing presets via the CLI? I’ve tried to keep this list as succinct as possible, and to do so I’ve kept my Complete Guide to ES6 with Babel 6 as a separate series — covering the CLI, Webpack, Gulp and Mocha.

现在已经快速了解了 Babel 6 的包，plugin，preset 和 option！但关于 Webpack 呢？如何通过 CLI 传递 preset？为了保持文章的简洁风格，我把这些内容写在了 [Complete Guide to ES6 with Babel6](http://jamesknelson.com/the-complete-guide-to-es6-with-babel-6/) 作为独立的系列 - 包含 CLI，Webpack，Gulp 和 Mocha。

## But everything moves so fast. How will I keep up to date?

但一切进展都那么快，我该如何才能跟上脚步呢？



> With ES2015 already standardised, there is no argument that Babel is a necessary tool for most JavaScript developers. But does the thought of integrating an entire platform for transforming JavaScript into every new project worry you a little bit? The speed at which the JavaScript ecosystem is growing can feel demoralising. But luckily, it doesn’t have to be that way!
 
ES2015 已经实现标准化，没有参数的 Babel 对大部分开发者来说是必要的工具。但整合整个平台把 JavaScript 转换到新的项目你是否会有一点担心？JavaScript 生态系统的快速增长会然人感觉到有些泄气。但很幸运，不用这样做。


> The thing is that for most projects, scaling is a problem you’d like to have. And until you’re at that point, you’ll be more productive by focusing on a few important tools than trying to grasp everything.

对于大部分项目都会遇到的伸缩问题，在你遇到这个问题时你会明白，通过关注一个最小最重要的工具你将更有效率，而不是试图抓住一切。



One way to keep focussed on the tools which count is to join my Newsletter. You’ll receive one e-mail every couple weeks with information tailored to small apps using React. And in return for your e-mail, you’ll immediately receive three bonus print-optimised PDF cheatsheets – on React (see preview), ES6 and JavaScript promises. All for free!


One more thing – I love hearing your questions, offers and opinions. If you have something to say, leave a comment or send me an e-mail at james@jamesknelson.com. I’m looking forward to hearing from you!