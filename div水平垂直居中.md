# code示例

```
<div class="parent">
  <div class="child"></div>
</div>
```

## 示例一

利用flex 水平和垂直居中的属性

```
div.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## 示例二

利用绝对定位、css3、margin auto

```
div.parent {
    position: relative; 
}
div.child {
    position: absolute; 
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);  
}
/* 或者 */
div.child {
    width: 50px;
    height: 10px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -25px;
    margin-top: -5px;
}
/* 或 */
div.child {
    width: 50px;
    height: 10px;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
```

## 示例三

使用grid

```
div.parent {
  display: grid;
}
div.child {
  justify-self: center;
  align-self: center;
}
```

## 示例四

使用伪类 + vertical-align

```
div.parent {
  font-size: 0;
  text-align: center;
  &::before {
    content: "";
    display: inline-block;
    width: 0;
    height: 100%;
    vertical-align: middle;
  }
}
div.child{
  display: inline-block;
  vertical-align: middle;
}
```

## 示例五

利用flex、margin auto

```
div.parent{
  display:flex;
}
div.child{
  margin:auto;
}
```

## 示例六

利用table、table-cell

```
div.parent {
  display: table;
}
div.child {
  display: table-cell
  vertical-align: middle;
  text-align: center;
}
```
