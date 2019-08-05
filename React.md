#

## 虚拟DOM

通过一个Javascript来表示DOM节点的树形结构。该树形结构保留了DOM的一些基本属性。通过diff算法来获取是否需要修改DOM，以及如何改变DOM。React同时维护两个虚拟DOM， 通过两个新旧DOM对比来确定哪些对象被更新

## diff算法

## JSX

JSX是javascript的语法扩展，结合了HTML和javascript.

## 组件

1. 无状态组件/函数组件/展示组件：无生命周期方法，返回React元素，接受Props、无副作用的纯函数
2. 有状态组件/class组件：有state、生命周期方法
3. 受控组件：React处理表单的一种方法，通过handleChange来捕捉每个输入的数据，并放入state中
4. 非受控组件：通过Ref获取表单中的数据
5. 容器组件：处理获取数据、订阅redux存储等组件。包含展示组件和容器组件
6. 高阶组件：是将组件作为参数生成另一个组件。如Redux中的connect

## 如何在React中应用样式

1. 外部样式表：如import './App.css'; 或者import style from './App.css'; className={style.XXX}
2. 内联样式：如style={{backgroundColor: 'red'}}
