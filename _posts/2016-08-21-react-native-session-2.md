---
layout: post
title:  REACT NATIVE 系列第二讲
subtitle: 谢老板 - session two
date: '2016-08-21'
---
#### 状态管理架构

谢老板React native系列讲座的第二次session，介绍了管理应用状态的两个概念：Flux和Redux。React native 是以React的方式抽象UI组件，只不过前者抽象原生App组件，后者抽象DOM元素。所以使用 React native 构建App，也需要一个状态管理工具管理数据流，以根据不同的状态更新UI。

#### Flux
Flux 是 Facebook 使用的一套前端应用的架构模式。
React或React native是MVC(Model，View，Controller里面View的部分，那么Flux就相当于添加 Model 和 Controller 的部分。

![Flux_Overview]({{site.baseurl}}/img/flux-overview.png)

 Flux 的核心是“单向数据流“
 `Action -> Dispatcher -> Store -> View`
 
* 首先要有action，通过定义一些 action creator 方法根据需要创建 Action 提供给 dispatcher 
* View 层通过用户交互（比如 onClick）会触发 Action
* Dispatcher 会分发触发的 Action 给所有注册的 Store 的回调函数
* Store 回调函数根据接收的 Action 更新自身数据之后会触发一个 change 事件通知 View 数据更改了
* View 会监听这个 change 事件，拿到对应的新数据并调用 setState 更新组件 UI

所有的状态都由 Store 来维护，通过 Action 传递数据，构成了如上所述的单向数据流循环.

#### Redux
Redux 是状态容器，提供可预测化的状态管理，其实也是 Flux 里面“单向数据流”的思想，只是它充分利用函数式的特性,让整个实现使用起来也更简单。

![Rudux_Flow]({{site.baseurl}}/img/rudux.png)

应用中所有的 state 都以一个对象树的形式储存在一个单一的 store 中。惟一改变 state 的办法是触发 action，一个描述发生什么的对象。
为了描述 action 如何改变 state 树，需要编写 reducers。


#### 参考链接   
* Flux: [**https://hulufei.gitbooks.io/react-tutorial/content/flux.html**](https://hulufei.gitbooks.io/react-tutorial/content/flux.html)
* Redux: [**http://cn.redux.js.org/**](http://cn.redux.js.org/)
* Redux Github: [**https://github.com/reactjs/redux**](https://github.com/reactjs/redux)