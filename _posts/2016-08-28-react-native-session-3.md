---
layout: post
published: true
title: REACT NATIVE 系列第三讲
subtitle: 从React开始实操 - session three
---

在阔别上次第二讲几周之后，谢老板终于给我们带来了React Native系列第三弹。  
这次谢老板改变了课程形式，强调workshop鼓励全程动手操作的模式，领着大家体验了一把React + Reduce从init project到run test的整个操作过程。

### 第一节，从创建项目目录、安装JS包开始
~~~
mkdir lession01
cd lession01
npm init
npm install react react-dom --save
npm install babel webpack webpack-dev-server babel-preset-es2015 babel-preset-react --save
~~~
这里一共安装了三类包，react\webpack\babel。  

**react**就不用说了，请见前两次session。  
**webpack**是前端的一种代码模块化工具，默认支持JS模块化，其他前端代码或者静态资源如CSS，则需要安装相应loader，如css-loader style-loader。  
**babel**是JS的语法转化器，可以让编程人员选择最新的JS语法，而不用等待到浏览器支持时才开始使用。并且提供了JSX\React的相应支持。  
其中--save的选项，是将项目中的包依赖自动保存入项目目录下的package.json文件。

第一个实践而成的Demo，见下图：
![React_Native_3_1.png]({{site.baseurl}}/img/React_Native_3_1.png)
这个demo的功能主要是试了一把babel的语法转化的效果，左边是ES6、JSX，右边是Babel转化后的语句。  
具体代码实现详情，请见[谢老板github](https://github.com/wesleyxie/lesson1)

### 第二节，开始实现一个Redux的reducer，还是从安装JS包开始
~~~
npm install babel-core babel-preset-es2015 babel-preset-react babel-preset-stage-2 expect mocha react-addons-test-utils --save-dev
~~~
这里用到的测试框架是**mocha**,由于mocha自身不带断言库，因此引入断言库是**expect**。  
实现一个最简单的recuder用来将数字+1或者-1，并且带有对应的单元测试。
![React_Native_3_2.png]({{site.baseurl}}/img/React_Native_3_2.png)

运行测试后输出：
![React_Native_3_3.png]({{site.baseurl}}/img/React_Native_3_3.png)

接着，开始使用Redux的方式来操作React的state，见[github中的counter.js文件](https://github.com/wesleyxie/lesson1/blob/master/counter.js)

完成后的效果如下：
![React_Native_3_4.png]({{site.baseurl}}/img/React_Native_3_4.png)
![React_Native_3_5.png]({{site.baseurl}}/img/React_Native_3_5.png)

### 最后，用最简易的方式自实现了一把Redux
~~~
const createStore = (reducer) => {
  let state;
  let listeners = [];

  const getState = () => state;

  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach(listener => listener());
  };

  const subscribe = (listener) => {
    listeners.push(listener);
    // return () => {
    //   listeners = listeners.filter(l => l !== listener);
    // };
  };

  dispatch({});

  return {getState, dispatch, subscribe};
}
~~~

## 相关链接：
[课程代码github](https://github.com/wesleyxie/lesson1)  
[webpack tutorials](http://webpack.github.io/docs/tutorials/getting-started/)  
[webpack官方文档](http://webpack.github.io/docs/what-is-webpack.html)  
[Babel官网](http://babeljs.io/)  
