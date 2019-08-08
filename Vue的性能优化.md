# Vue的性能优化

## 利用object.freeze

1. 通过object.freeze冻结一个对象
2. 属性均不可更改，因此Vue就不会对这个对象进行数据劫持
