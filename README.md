# redux基础流程
* 1 关联: 在configStore里, 把所有的reducer和store先关联起来
* 2 分发action: 创建的store 通过dispatch一个action, 分发到各个reducers里
* 3 更新state: reducers根据action.type 来更新对应state, 确保store数据是最新的
* 4 更新view: react-redux提供的connect方法, 将原始根节点包装在connect下,
并将state对象中的props和store中的dispatch函数传递给原始根节点props, 从而改变全局view

# 主要部分介绍

## Redux主要分三个部分: Action Reducer Store

### Action
action主要用来传递操作state的信息, 一般是以Js Plain Object的形式存在
实际上, 我们都是通过创建函数来生产action, 这类函数统称为Action Creator
```javascript
function addTodo(text) {
  return { type: types.ADD_TODO, text };
}
```

### Reducer
reducer为state的处理函数, 通过传入旧的state和action来更新state

### Store
Store是单一的, 维护着一个全局的state, 并根据action来进行事件分发处理state
所以看出, Store是一个把Action和Reducer结合起来的对象
而store.dispatch(action)用于将action对象发送给reducer处理, 减少对reducer的直接调用, 并且能够更好的管理state

### bindActionCreators
我们通过ActionCreator来生产action, 所以实际调用为 store.dispatch(actionCreator(...args))
而bindActionCreators就是将store.dispatch 和 ActionCreator进行再一次封装, 转换成一个参数(actions),
在组件里通过调用actions里的方法,就相当于dispatch了一个action, 进而分发到reducers里

## React-Redux
redux并不依赖于react, 它是一个javascript状态容器, 提供可预测化的状态管理.
而react和redux结合, 就是要在更新state后, 会触发重新render函数, 进行更新组件.

### connect
它主要为react-components提供 Store里的state数据和dispatch方法. 这样组件可以通过dispatch来更新state.
最后connect把state和dispatch通过props的方式 传递给组件.

### Provider
connect组件需要Store, 所以redux提供了Provider来注入Store,
使其子组件能够在[context](https://facebook.github.io/react/docs/context.html)中得到store对象.


