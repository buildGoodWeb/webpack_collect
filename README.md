## 启动
		npm install
		npm run start

## 学习资源
http://zhaoda.net/webpack-handbook/index.html

## 示例项目初始化
			npm init
			# webpack依赖
			npm install webpack --save-dev

## webpack安装到全局(运行webpack命令)
			npm install webpack -g

##使用

首先创建一个静态页面 index.html 和一个 JS 入口文件 entry.js：
			// touch index.html
			<!-- index.html -->
			<html>
			<head>
			  <meta charset="utf-8">
			</head>
			<body>
			  <script src="bundle.js"></script>
			</body>
			</html>


			// touch entry.js
			document.write('It works.');

然后编译 entry.js 并打包到 bundle.js：
			webpack ./entry.js bundle.js

直接打开index.html

### 添加模块
添加一个模块 module.js 并修改入口 entry.js
			// touch module.js
			module.exports = 'It works from module.js.'

			// entry.js
			document.write('It works.')
			document.write(require('./module.js')) // 添加模块

			//重新打包，然后刷新页面

Webpack 会给每个模块分配一个唯一的 id 并通过这个 id 索引和访问模块。

## loader

Webpack 本身只能处理 JavaScript 模块，要处理其他类型的文件，需要使用 loader 进行转换。

Loader 可以理解为是__模块和资源的转换器__，它本身是一个__函数__，接受源文件作为参数，返回转换的结果。这样，我们就可以通过 require 来加载任何类型的模块或文件，比如 CoffeeScript、 JSX、 LESS 或图片。

### loader特征总结
1. 管道方式链式调用；
2. 可同步、异步执行；
3. 通过文件扩展名（或正则表达式）绑定给不同类型的文件；
4. 可通过npm发布和安装

接上一个例子，在页面中引入一个 CSS 文件 style.css。首页将 style.css 也看成是一个模块，然后用 css-loader 来读取它，再用 style-loader 把它插入到页面中。
			/* style.css */
			body { background: yellow; }

			//entry.js
			require("!style!css!./style.css") // 载入 style.css
			document.write('It works.')
			document.write(require('./module.js'))

安装css loader
			npm install css-loader style-loader --save-dev

## 配置文件
Webpack 在执行的时候，除了在命令行传入参数，还可以通过指定的配置文件来执行。默认情况下，会搜索当前目录的 webpack.config.js 文件，这个文件是一个 node.js 模块，返回一个 json 格式的配置信息对象，或者通过 --config 选项来指定配置文件。

然后创建一个配置文件 webpack.config.js：
			var webpack = require('webpack')

			module.exports = {
			  entry: './entry.js',
			  output: {
			    path: __dirname,
			    filename: 'bundle.js'
			  },
			  module: {
			    loaders: [
			      {test: /\.css$/, loader: 'style!css'}
			    ]
			  }
			}

简化 entry.js 中的 style.css 加载方式：
			require('./style.css')

运行 webpack，可以看到 webpack 通过配置文件执行的结果和上一章节通过命令行 webpack entry.js bundle.js --module-bind 'css=style!css' 执行的结果是一样的。

## 插件

## 开发环境
项目逐渐变大，webpack 的编译时间会变长，可以通过参数让编译的输出内容带有进度和颜色。
			webpack --progress --colors
			// 或者启动监听模式
			webpack --progress --colors --watch

## 使用 webpack-dev-server 开发服务
			// 全局安装
			npm install webpack-dev-server -g
			// 安装依赖
			npm install webpack-dev-server --save-dev	
			// 运行
			webpack-dev-server --progress --colors		

## 故障处理
			// 打印错误详情
			webpack --display-error-details

Webpack 的配置提供了 resolve 和 resolveLoader 参数来设置模块解析的处理细节，resolve 用来配置应用层的模块（要被打包的模块）解析，resolveLoader 用来配置 loader 模块的解析。







