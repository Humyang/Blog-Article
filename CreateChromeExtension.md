layout: [post]
title: "创建 Chrome 拓展"
date: 2015-05-24 12:45:26
tags: 
- 前端
categories: 
- 前端
- Chrome 拓展
id: "CreateChromeExtension"

---


因为最近在翻译一些文章，文章标题的 H1~H6 标签有时候挺难分清楚大小，就想利用 jQuery 区分它们，但有的网站没使用 jQuery。所以就打算写一个插件解决类似的问题。

<!-- more -->

## 入门例子

先照着[官方例子](https://developer.chrome.com/extensions/getstarted)来一遍。

### 创建 manifest 文件

首先创建一个 manifest 文件 `manifest.json`。这是 JSON 格式的元数据文件,属性包括拓展的名称，描述，版本号等等。

Chrome 会加载这个文件对拓展功能的描述，和它需要什么权限去做什么事情，需要学习更多有关 manifest 文件的资料，请阅读 [Manifest File Format documentation](https://developer.chrome.com/extensions/manifest)。

在这个例子的 manifest 中，会定义一个 [browser action](https://developer.chrome.com/extensions/browserAction)，和获取当前标签的 URL 的 [activeTab permission](https://developer.chrome.com/extensions/activeTab)，和 host [permission](https://developer.chrome.com/extensions/declare_permissions) 访问外部的 Google 图像搜索 API。

``` 

{
  "manifest_version": 2,

  "name": "Getting started example",
  "description": "This extension shows a Google Image search result for the current page",
  "version": "1.0",

  "browser_action": {
    "default_icon": "icon.png",
    "default_popup": "popup.html"
  },
  "permissions": [
    "activeTab",
    "https://ajax.googleapis.com/"
  ]
}


```

### 资源

manifest.json 中指向了两个资源文件 `icon.png` 和 `popup.html`，这两个文件必须存在于拓展包中，现在我们来创建它：

* `icon.png` 将会显示在浏览器的多功能框中，等待用户的交互。将 ![](./icon.png) 保存到工作中的目录中。你也可以自己创建该图像，需要是 19px 的正方形 PNG 文件。
* `popup.html` 会在响应用户点击 browser action 时会弹出的窗口内显示。它是一个标准 HTML 文件，就像进行 web 开发一样，给你完全控制内容的显示。[从这里下载 popup.html 文件](https://developer.chrome.com/extensions/examples/tutorials/getstarted/popup.html) ，并保存到工作中的目录。<br />popup 内容实际的渲染逻辑由 `popup.js` 实现，建议你仔细阅读这个文件的注释了解更多相关的逻辑。[从这里下载 popup.js 文件](https://developer.chrome.com/extensions/examples/tutorials/getstarted/popup.js) 并保存到工作中的目录。
	
你现在应该有四个文件在工作目录中：`icon.png`,`manifest.json`,`popup.html`,`popup.js`。下一步将会加载这些文件到 Chrome 中。

### 加载拓展

从 Chrome Web Store 下载的文件包是 `.crx` 文件，这是一种很好的分配方式，但对开发不方便。Chrome 为测试而提供了一种快速加载工作目录的方式。

1.打开浏览器访问 `chrome://extensions` (或点击 ![](./hotdogmenu.png) 打开 Chrome 菜单中 Tool 下面的 Extensions)。


2.确保右上角的选项 **Developer mode** 已经选上。

3.点击 **Load unpacked extension...** 弹出文件选择对话框。

4.选中你的拓展目录。

另外，你也可以把目录文件拖入 **chrome://extensions** 让浏览器加载它。

如果拓展是有效的，它将会加载和正确运行！如果它是无效的，一个错误信息会显示在页面的顶部。修正错误，然后再试一次。

### 修改代码

现在你有了第一个拓展并正在运行。让我们来修改一些东西来熟悉开发过程。例如，设置 brower action 按钮的提示。

根据 brwoserAction 文档，按钮提示可以通过 manifest 文件中的 `default_title` 键设置。打开 `manifest.json`，然后添加 `default_title` 键到 `browser_action` 中。需要确保 JSON 是有效的，所以必须添加一个逗号。

```
{
  ...
  "browser_action": {
    "default_icon": "icon.png",
    "default_popup": "popup.html",
    "default_title": "Click here!"
  },
  ...
}


```

manifest 文件只有拓展被加载时会被解析，如果你想见到上面的改动，拓展需要重新加载。访问拓展页面 (**chrome://extensions**, 或 Chrome 菜单下的 **Tools** > **Extensions**)，然后点击拓展下面的 **Reload**。当拓展页面重新加载时，所有的拓展都会重新加载，等同于按下 F5 或 Ctrl－R。

### 下一步做什么？
你已经知道 manifest 文件的核心作用是整合资源，还知道主要的定义 browser action 的基础。这是很好的开始，希望你有足够的兴趣进一步的探索，这里还有更多东西等待你发现：

* [Chrome Extension Overivew](https://developer.chrome.com/extensions/overview) 描述了大量的关于拓展的总体架构细节，和一些你想进一步熟悉的特别概念。这是你迈向拓展大师最好的开始。
* 没有人第一次尝试就能写出完美的代码，这意味着你需要学习有关调试的知识。我们非常推荐你去阅读 [debugging tutorial](https://developer.chrome.com/extensions/tut_debugging) 。
* Chrome 拓展可以访问超出所打开网站的能力的强大 API。browser actions 只是冰山一角。我们的 [chrome.* APIs documentation](https://developer.chrome.com/extensions/api_index) 将会引导你每个 API 的使用。
* 最后，[developer's guide](https://developer.chrome.com/extensions/devguide) 有额外的几十个文档文件的连接，你可能会感兴趣。


### 分析

官方的简单例子已经完成，接下来分析一下这个插件的行为，然后再进行进一步学习，最后完成自己想实现的功能。

点击拓展图标时，拓展会获取当前活动标签的 URL，然后分析图片的地址并传递给 Google 提供的图像搜索 API 查找这些图片，然后返回一个图片地址。

`popup.js` 代码分析：

1.首先添加事件监听 `document.addEventListener`。第一个参数是 `DOMContentLoaded`，根据名称意思是 `popup.html` 加载后触发事件，那就可以理解为点击拓展图标后，浏览器显示 `popup.html` 内容，触发响应事件。

2.然后在响应事件内调用 `getCurrentTabUrl` 。在 `getCurrentTabUrl` 中，会使用 Chrome 提供的 API `chrome.tabs.query` 获取当前活动页面的 URL。这个 URL 传入了两个参数，第一个是数组 `queryInfo`，指定条件为当前窗口的和活动的标签。第二个参数是回调函数。当打开拓展时，一定会有一个窗口和至少一个标签，而一个窗口只有一个活动标签，所以 tabs[0] 就是这个活动标签。`tab.url` 只有拥有 **activeTab** 权限时才可以使用。如果需要其它标签页的权限 (`queryInfo` 去掉 `active:true`)。那么需要拥有 **tabs** 权限。在回调函数最后会调用 `callback(url)`，这是因为 `chrome.tabs.query` 是异步的。

3.获取当前活动标签的 URL 后，对 `getImageUrl` 传入标签 URL 获取图像地址，宽度和高度。函数内部使用 ajax 访问 Google 提供的 API。对 API 的返回值进行解析，图像地址和宽度，高度就包含在其中。

4.调用 `document.getElementById('status').textContent = statusText;` 修改 `popup.html` 的内容。拓展为了不影响当前页面，分成了几个部分使页面代码和拓展代码分开，接下来会学习到。 



---




