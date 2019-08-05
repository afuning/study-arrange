# Vue知识点

## 父子组件渲染过程

1. 加载渲染过程
父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted
2. 子组件更新过程
父beforeUpdate->子beforeUpdate->子updated->父updated
3. 父组件更新过程
父beforeUpdate->父updated
4. 销毁过程
父beforeDestroy->子beforeDestroy->子destroyed->父destroyed

## 响应式原理

使用发布订阅的设计模式。有三个角色Dep(依赖收集，类似于广播员的功能)，Watcher（观察者），Observer（发布者）。

1. Dep通过Object.defineProperty中对对象的属性getter来收集依赖（addSub），setting进行通知(notify)观察者。
2. Observer就是遍历对象，对数据进行绑定。为了绑定数据的方法，则重写数组方法（push、pop、shift、unshift、splice、sort、reverse）。
3. Watcher则是会被存储在Deps中，数据变动时Deps会通知Watcher去执行回调cb，进行视图更新等操作

## 事件

4个事件API：$on, $emit, $off, $once

1、 初始化的时候会在vm上创建一个_events存放事件

```
{
    eventName: [func1, func2, func3]
}
```

2、 $on是把事件名字存入_events

3、 $once首先调用$on的方法，然后回调时$off
4、 $off注销事件，_events中删除对应的事件名和方法

## VNode

VNode是一个简化了DOM属性的JS对象，VNode节点组成一个VNode树，即虚拟DOM树。Vue中有创建空节点、文本节点、组件节点。
通过createElement来创建虚拟节点

## 虚拟DOM和diff算法实现

1. Vue通过_update方法更新视图
2. _update中调用patch将新老VNode节点树进行对比，进行最小单位地修改视图。patch核心即diff算法。diff算法是通过同层的树节点进行比较而非对树进行逐层搜索遍历的方式，所以时间复杂度只有O(n)
3. diff算法中，当oldVnode与vnode在sameVnode的时候才会进行patchVnode，也就是新旧VNode节点判定为同一节点的时候才会进行patchVnode这个过程，否则就是创建新的DOM，移除旧的DOM

```
function sameVnode (a, b) {
  return (
    a.key === b.key &&
    a.tag === b.tag &&
    a.isComment === b.isComment &&
    isDef(a.data) === isDef(b.data) &&
    sameInputType(a, b)
  )
}

function sameInputType (a, b) {
  if (a.tag !== 'input') return true
  let i
  const typeA = isDef(i = a.data) && isDef(i = i.attrs) && i.type
  const typeB = isDef(i = b.data) && isDef(i = i.attrs) && i.type
  return typeA === typeB
}
```

### patchVnode的规则[具体详解](https://github.com/answershuto/learnVue/blob/master/docs/VirtualDOM%E4%B8%8Ediff(Vue%E5%AE%9E%E7%8E%B0).MarkDown)

1. 如果新旧VNode都是静态的，同时它们的key相同（代表同一节点），并且新的VNode是clone或者是标记了once（标记v-once属性，只渲染一次），那么只需要替换elm以及componentInstance即可。
2. 新老节点均有children子节点，则对子节点进行diff操作，调用updateChildren，这个updateChildren也是diff的核心。
3. 如果老节点没有子节点而新节点存在子节点，先清空老节点DOM的文本内容，然后为当前DOM节点加入子节点。
4. 当新节点没有子节点而老节点有子节点的时候，则移除该DOM节点的所有子节点。
5. 当新老节点都无子节点的时候，只是文本的替换。
