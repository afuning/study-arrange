# webpack

## 热更新过程

1. 当修改了一个或多个文件
2. 文件系统接收更改并通知webpack
3. webpack重新编译构建一个或多个模块，并通知HMR服务器进行更新
4. HMR(Hot Module Replacement) Server 使用webSocket通知HMR runtime 需要更新，HMR运行时通过HTTP请求更新jsonp
5. HMR运行时替换更新中的模块，如果确定这些模块无法更新，则触发整个页面刷新

## HMR配置

1. 使用webpack-dev-server作为服务器启动
2. webpack.config的devServer中配置hot: true
3. webpack.config的plugins增加HotModuleReplacementPlugin
4. 使用module.hot.accept增加HMR代码

## 谈谈webpack

webpack是一个模块打包工具，通过编译输出静态文件