目前为止的操作都是 Dispatch 一个 Action 后立即响应，但实际程序应用场景会更复杂，例如一个http 请求在发出前 dispatch 一个 “准备发射” 的 action，收到响应后

对于异步操作，我们用三种 action 表示他，分别是表示发出请求，请求成功，请求失败。在不同的时间点分发 action。

```javascript
{ type: 'FETCH_POSTS' }
{ type: 'FETCH_POSTS', status: 'error', error: 'Oops' }
{ type: 'FETCH_POSTS', status: 'success', response: { ... } }
```

或者

```javascript
{ type: 'FETCH_POSTS_REQUEST' }
{ type: 'FETCH_POSTS_FAILURE', error: 'Oops' }
{ type: 'FETCH_POSTS_SUCCESS', response: { ... } }
```
