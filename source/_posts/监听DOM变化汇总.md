---
title: 监听DOM变化汇总
date: 2020-12-23 11:03:51
tags: DOM
cover: /images/observer.jpeg
author: 
  nick: wzw
  link: https://github.com/ziwen-wang
categories: 项目总结
comments: true
---
## 监听DOM方式汇总

### vue中监听DOM宽高变化（持续更新
#### 全局element-resize-detector
##### 使用方式
##### 第一步 项目根目录 安装
``` javascript
    npm i element-resize-detector -D
```
##### 第二步 引入
``` javascript
    import ElementResizeDetectorMarker from 'element-resize-detector'
```
##### 使用
``` javascript
    let erd = ElementResizeDetectorMarker() //注册全局或者组件引用都可
    erd.listenTo(DOM,(element)=>{
        //todo
    })
```

### 使用iframe 模拟 window resize
##### window.resize没有兼容性问题，按照这个路子，可以使用ifrmae定位到要监听的DOM，宽高100%，当容器变化时，会触发iframe的resize事件，通过contentWindow.onresize 就可以监听

``` javascriot
    let observerReisze = (element,handle) => {
        let iframeDom = document.createElement('iframe')
        iframeDom.style.cssText = 'width:100%;height:100%;position:absolute;left:0;top:0;opcity:0;'
        iframeDom.onload = () => {
            iframeDom.contentWindow.onresize = ()=>{
                handle()
            }
        }
        element.appendChild(iframeDom)
    }
```
### ResizeObserver
#### 监听DOM宽度 变化 详细资料 https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver
```
    let callback =()=>{
        //todo
    }
    let observer = new ResizeObserver(callback)
    observer.observe(DOM,{attributes: true,characterData: true})
    //observer.unbserve() 停止监听
```
### MutationObserver 
#### 监听DOM 节点变化 详细资料 https://developer.mozilla.org/zh-CN/docs/Web/API/MutationObserver

```
    let callback = () => {
        //todo
    }
    let observer = new MutationObserver(callback)
    observer.observe(DOM,config) // 开始观察目标节点
    observer.disconnect() //停止观察
```

