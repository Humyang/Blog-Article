layout: [post]
title: "React 指南"
date: 2015-11-29 23:10:17
tags: 
- React
categories: 
- 前端
- React
id: "Reacttutorial"
---

一遍翻译一遍学的 React 官方指南。

<!-- more -->

[原文地址](https://facebook.github.io/react/docs/tutorial.html)

[Demo 地址](https://github.com/Humyang/front-end-example/tree/gh-pages/React/react-tutorial-master)

文章前面的部分漏了，直接从例子开始。

---

# React

## 第一个例子

创建一个自己的 Component，只是一个简单的 <div> 元素：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>React Tutorial</title>
    <!-- Not present in the tutorial. Just for basic styling. -->
    <link rel="stylesheet" href="css/base.css" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.6.15/browser.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/marked/0.3.2/marked.min.js"></script>
  </head>
  <body>
    <div id="content"></div>

    <script type="text/babel">
      // To get started with this tutorial running your own code, simply remove
      // the script tag loading scripts/example.js and start writing code here.

      var CommentBox = React.createClass({
          render:function(){
            return (
                <div className="commentBox">
                  Hello,world! I am a CommentBox.
                 </div> 
              );
          }
        });

      ReactDOM.render(
          <CommentBox />,
          document.getElementById('content')
        );

    </script>
  </body>
</html>

```


注意，HTML 元素以小写开头，React 自定义 Class 以大写开头。

React 使用的 JSX 语法，它是原生 JavaScript 的语法糖，与下面的原生例子一样，但更简洁：

```javascript
var CommentBox = React.createClass({displayName: 'CommentBox',
  render: function() {
    return (
      React.createElement('div', {className: "commentBox"},
        "Hello, world! I am a CommentBox."
      )
    );
  }
});
ReactDOM.render(
  React.createElement(CommentBox, null),
  document.getElementById('content')
);
```

在这个例子中我们对一个 JavaScript 对象添加了一些方法，然后传递给 React.createClass() 创建新的组件。这些方法中最重要的是 `render`，它返回将要渲染成 HTML 的 React 组件。

`<div>` 标签不是实际的 Node 节点，它是 React 提供的 `div` 组件的实例。你可以吧这些当作标签或者 React 知道如何处理的数据。因此 React 是安全的，不会生成 HTML 字符串，所以可以避免受到 XSS 攻击。

请不要在 render 返回基础 HTML，你可以返回由你 (或其他人) 构建的组件树,这是 React 可组合的原因，前端维护的关键原则。

`ReactDOM.render()` 实例化根组建，启动框架，并注入标记到原生 DOM，给第二个参数。

`ReactDOM` 模块暴露指定的 DOM 操作方法，它是 React 在不同的平台的核心工具。

## 第二个例子

这个例子在上一个例子的基础上添加两个自定义 Class，`<CommentList />` 和 `<CommentForm />` ：

```javascript

	  var CommentList = React.createClass({
        render:function(){
          return (
              <div className="commentList">
                Hello,world!I am a CommentList.
                </div>
            );
        }
      });

      var CommentForm = React.createClass({
        render : function(){
          return (
              <div className="commentForm">
                Hello,world! I am a CommentForm.
               </div> 
            );
        }
      });


       var CommentBox = React.createClass({
          render:function(){
            return (
                <div className="commentBox">
                  <h1>Comments</h1>
                  <CommentList />
                  <CommentForm />
                 </div> 
              );
          }
        });

      ReactDOM.render(
          <CommentBox />,
          document.getElementById('content')
        );



    </script>
  </body>

```

我们将 HTML 标签的组件混合在一起构建。HTML 组件也是正常的 React 组件，就像你所定义的组件一样，有一点不同。JSX 编译器会自动使用 `React.createElement(tagName)` 重写 HTML 标签，这是为了防止污染全局命名空间。

## 使用 props

让我们来创建一个 comment，它依赖从上级传递过来的数据，从上级传递来的数据可以通过 `property` 使用，我们通过 `this.props` 访问 properties，通过 props，comment 可以读取从 CommentList 读取数据，和渲染一些标记。

```javascript

var Comment = React.createClass({
        render : function(){
            return (
                <div className="comment">
                  <h2 className="commentAuthor">
                    {this.props.author}
                  </h2>
                  {this.props.children}  
                </div>
              );  
          }
      });

```

在 JSX 语法的括号内 (属性或子级) 可以写 JavsScript 表达式，你可以放置文本或 React 组件到树中。我们通过 `this.props` 访问组件的属性名，`this.props。children` 访问组件的内嵌元素。

## 组件属性

我们已经定义了 `Comment` 组件，我们想传递作者名和评论文本给 `Comment` 组件。这样我们就可以使用一份代码完成所有的单独评论工作。现在我们开始添加：

```javascript

var CommentList = React.createClass({
  render: function() {
    return (
      <div className="commentList">
        <Comment author="Pete Hunt">This is one comment</Comment>
        <Comment author="Jordan Walke">This is *another* comment</Comment>
      </div>
    );
  }
});

```

现在我们已经从上级 `CommentList` 组件传递了一些数据给子级 `Comment` 组件。例如我们传递了 Pete Hunt (通过属性) 和它的评论文本 (通过类 XML 子级) 给第一个 `Comment`。然后如之前所说，`Comment` 组件将会通过 `this.props.author` 访问 properties，和通过 `this.props.children` 访问子级。

> `CommentList` 组件包含 `Comment` 组件，这里的 `Comment` 组件被传递了属性和子级。在 `Comment` 组件的定义中 (React.createClass()) 就可以通过 `this.props` 访问这些值。


## 添加 Markdown

Markdown 是一种简单的排版格式。

首先在页面引入第三方库 `<script src="https://cdnjs.cloudflare.com/ajax/libs/marked/0.3.2/marked.min.js"></script>`。然后调用函数即可将字符串转换成 HTML。

接着，我们将评论使用 Markdown 转换成 HTML。

```javascript

var Comment = React.createClass({
  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        {marked(this.props.children.toString())}
      </div>
    );
  }
});

```

为了正确的调用 Marked 库，我们需要将值使用 `.toString()` 转换成字符串。现在出现了一个问题，我们的评论成了 `<p>This is <em>another</em> comment</p>` 这样字符！我们想看到的是实际的 HTML。

这是 React 为了防止 **XSS 攻击**。下面可以绕过这个问题，但框架不建议你这样做！

```javascript

var Comment = React.createClass({
  rawMarkup: function() {
    var rawMarkup = marked(this.props.children.toString(), {sanitize: true});
    return { __html: rawMarkup };
  },

  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        <span dangerouslySetInnerHTML={this.rawMarkup()} />
      </div>
    );
  }
});

```

这是一个特殊的 API，专门用来插入原生的 HTML 代码。

记住：使用这个功能时一定要保证安全，我们传递了 `sanitize: true` 告诉 marked 转义任何传递过来 HTMl 的标记，而不是不变的传递它。


## 挂钩数据模型

现在我们已经直接将评论插入源代码中，现在我们将 `JSON` 数据插入评论列表。最终我将是从服务器获取，但现在我们直接写进代码中。

```javascript

var data = [
  {id: 1, author: "Pete Hunt", text: "This is one comment"},
  {id: 2, author: "Jordan Walke", text: "This is *another* comment"}
];

```

我们需要使用模块化方式将 data 放置到评论列表中，修改 `CommentBox` 和 `ReactDOM.render()` 调用这个数据并通过 props 传递给 `CommentList`。


```javascript

var CommentBox = React.createClass({
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.props.data} />
        <CommentForm />
      </div>
    );
  }
});

ReactDOM.render(
  <CommentBox data={data} />,
  document.getElementById('content')
);

```

现在 `CommentList` 可以获取 `data` 数据了，让我们来动态渲染评论数据吧：

```javascript

      var CommentList = React.createClass({
        render:function(){
              var commentNodes = this.props.data.map(function(comment) {
                return (
                    <Comment author={comment.author} key={comment.id}>
                      {comment.text}
                    </Comment>
                  );
              });
              return (
                  <div className="commentList">
                    {commentNodes}
                  </div>
                );
        }
      });

```

完成！

## 从服务器获取数据

让我们把硬编码的方式替换成从服务器获取动态数据的方式吧，我们把 data 属性移除，使用 URL 来捕获数据。

```javascript

    ReactDOM.render(
          <CommentBox url="/api/comments" />,
          document.getElementById('content')
        );

```

这个组件与之前的组件不一样，因为它会预渲染自身，这个组件本身不会有任何数据，直到请求从服务器获得返回，这意味着组件会渲染一些新评论。

注意，在这一步组件不会工作。

## 活性状态

目前位置，每个组件都是基于 props 获取数据，渲染自身。`props` 是不变的：它是从它的上级传递过来并且是 “属于” 它的上级的。要实现互动，我们来介绍可变状态给组件。 `this.state` 是私有提供给组件的并且可以通过调用 `this.setState()` 发生更改。当状态改变时，组件会重新渲染它自身。

`render()` 方法是写了 `this.props` 和 `this.state` 的函数的声明，框架会确保界面始终与输入一致。

当服务器返回数据，我们将更改评论数据。让我们添加评论数据的数组到 `CommentBox` 组件作为它的 `state`。

```javascript

var CommentBox = React.createClass({
  getInitialState: function() {
    return {data: []};
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});

```

`getInitialState` 在组件的生命周期准确的只执行一次并设置组件的初始状态。

### 更新状态

当组件首次被创建，我们想 GET 一些 JSON 从服务器并将状态成最新的数据。我们使用 jQuery 做一些匿名请求给服务器获取我们早期需要的数据：

```javascript

[
  {"author": "Pete Hunt", "text": "This is one comment"},
  {"author": "Jordan Walke", "text": "This is *another* comment"}
]

```

```javascript

var CommentBox = React.createClass({
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});

```

在这里，`componentDidMount` 方法在组件被渲染后自动被 React 调用。更新状态的关键地方是 `this.setState()`。我们在这里将旧的评论数据替换成新的从服务器获取的评论数据，然后 UI 会自动更新它自己。因为这是响应式的，只要有一个很小的改动都会实时更新，我们这里使用了简单的轮询，但你可以使用更简单的 WebSocket 或其它技术。



```javascript

var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});

ReactDOM.render(
  <CommentBox url="/api/comments" pollInterval={2000} />,
  document.getElementById('content')
);

```

我们将 AJAX 调用放置到单独的方法中并在组件首次加载时调用它和之后每隔两秒再次调用。尝试一下在浏览器运行然后更改文件目录下的 `comment.json`，两秒之后，你将会看到更改！

## 添加新评论

现在我们来构建来源，我们的 `CommentFrom` 组件应该询问用户他的名字和评论并发送请求给服务器保存评论。

```javascript

var CommentForm = React.createClass({
  render: function() {
    return (
      <form className="commentForm">
        <input type="text" placeholder="Your name" />
        <input type="text" placeholder="Say something..." />
        <input type="submit" value="Post" />
      </form>
    );
  }
});

```

### 控制组件

在传统的 DOM，输入元素是已呈现的和由浏览器管理状态 (它渲染的值)。这样的结果，实际的 DOM 的状态将与组件不同。可见的状态与组件不同不是个好主意。在 React，组件应该总是呈现与可见的相同状态，不仅仅只是初始化时相同。

因此，我们使用 `this.state` 保存用户的输入作为进入点。我们在初始状态定义两个属性 `author` 和 `text` 并设置他们为空字符串。在我们的 `<input>` 元素中，我们设置了 `value` prop用来反应组件的状态并绑定一个 `onChange` 处理它们。这些 `<input>` 元素的 `value` 用来控制组件。阅读更多关于控制组件的文章 [Forms article](https://facebook.github.io/react/docs/forms.html#controlled-components)。

### 事件

React 绑定事件处理到组件时使用驼峰命名法。我们添加的 `onChange` 处理两个 `<input>` 元素。当用户输入文本到 `<input>` 文本域，已绑定的 `onChange` 回调函数会触发并且修改组件的 `state`。组件的 state 状态将会更新为 `input` 元素所渲染的值。

### 提交表单

让我们开始与表单互动，当用户提交表单，我们应该清除它，然后提交请求给服务器，然后刷新评论的列表。首先，我们完成监听表单的提交事件和清理操作：

```javascript

      var CommentForm = React.createClass({
        getInitialState:function(){
          return { author:'',text:'' };
        },
        handleAuthorChange:function(e){
          this.setState({author:e.target.value});
        },
        handleTextChange:function(e){
          this.setState({text:e.target.value});
        },
        handleSubmit: function(e){
          e.preventDefault();
          var author = this.state.author.trim();
          var text = this.state.text.trim();
          if(!text || !author){
            return;
          }
          //TODO: send request to the server
          this.setState({author:'',text:''});
        },
        render : function(){
          return (
              <form className="commentForm" onSubmit={this.handleSubmit}>
              <input type="text" placeholder="Your name" value={this.state.author} onChange={this.handleAuthorChange} />
              <input type="text" placeholder="Say something..." value={this.state.text} onChange={this.handleTextChange} />
              <input type="submit" value="Post"  />
              </form>
            );
        }
      });

```

我们添加了一个 `onSubmit` 处理函数在表单提交的时候检查用户输入值有效时执行内容清理。

调用 `preventDefault()` 防止浏览器执行表单默认的执行动作。

### 回调方法作为 prop

当用户提交评论时，我们需要刷新评论的列表使新的评论出现。我们需要在 `CommentBox` 完成逻辑操作因为 `CommentBox` 包含所有表示评论列表的状态。

因此我们需要从子组件传递数据返回它的上级，然后我们在上级的 `render` 方法通过传递一个回调方法 (`handleCommentSubmit`) 到子级，将该回调方法绑定给子级的 onCommentSubmit 事件。每当事件被触发，该回调方法都会被调用：


```javascript

var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    // TODO: submit to the server and refresh the list
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});

```

当用户提交表单时从 `CommentForm` 调用回调方法：

```javascript

var CommentForm = React.createClass({
  getInitialState: function() {
    return {author: '', text: ''};
  },
  handleAuthorChange: function(e) {
    this.setState({author: e.target.value});
  },
  handleTextChange: function(e) {
    this.setState({text: e.target.value});
  },
  handleSubmit: function(e) {
    e.preventDefault();
    var author = this.state.author.trim();
    var text = this.state.text.trim();
    if (!text || !author) {
      return;
    }
    this.props.onCommentSubmit({author: author, text: text});
    this.setState({author: '', text: ''});
  },
  render: function() {
    return (
      <form className="commentForm" onSubmit={this.handleSubmit}>
        <input
          type="text"
          placeholder="Your name"
          value={this.state.author}
          onChange={this.handleAuthorChange}
        />
        <input
          type="text"
          placeholder="Say something..."
          value={this.state.text}
          onChange={this.handleTextChange}
        />
        <input type="submit" value="Post" />
      </form>
    );
  }
});

```

现在回调方法已经放置好，现在我们要做的事提交数据到服务器然后刷新列表。

```javascript

var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      type: 'POST',
      data: comment,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});

```

## 优化：预先刷新

我们的应用程序现在的功能已经但可以会感觉到速度有些慢，因为要评论列表显示之前你需要等待请求完成。我们可以把预先将评论添加到列表中使应用程序看起来非常快。

```javascript

var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    var comments = this.state.data;
    // Optimistically set an id on the new comment. It will be replaced by an
    // id generated by the server. In a production application you would likely
    // not use Date.now() for this and would have a more robust system in place.
    comment.id = Date.now();
    var newComments = comments.concat([comment]);
    this.setState({data: newComments});
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      type: 'POST',
      data: comment,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        this.setState({data: comments});
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});

```

## 恭喜！

你已经成功构建了一个评论组件，只用了很少的步骤。学习更多关于[为什么使用 React](https://facebook.github.io/react/docs/why-react.html)，或者阅读 [API 参考](https://facebook.github.io/react/docs/top-level-api.html)，祝你好运。





























