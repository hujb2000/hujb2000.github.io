---
---
layout: post
title:  "Node Tech Stack"
date:   2016-05-05 13:35:30
categories: allen.hu update
---

#  Tech Stack

 Node, Docker ,Reactor, Angular, Meteor, Webpack


# ReactJS

[react-router-tutorial](https://github.com/reactjs/react-router-tutorial)

bundle.js:1 Warning: It looks like you're using a minified copy of the development build of React. When deploying React apps to production, make sure to use the production build which skips development warnings and is faster. See https://fb.me/react-minification for more details


# Webpack

* Webpack 是什么

Webpack 是德国开发者 Tobias Koppers 开发的模块加载器，在 Webpack 当中, 所有的资源都被当作是模块, js, css, 图片等等..
因此, Webpack 当中 js 可以引用 css, css 中可以嵌入图片 dataUrl
对应各种不同文件类型的资源, Webpack 有对应的模块 loader。

```

	module: {
	　　loaders: [
	　　　{ test: /\.coffee$/, loader: 'coffee-loader' },
	　　　{ test: /\.js$/, loader: 'jsx-loader?harmony' } // loaders can take parameters as a querystring
	　　]
	　},
* CommonJS 与 AMD支持

Webpack 对 CommonJS 的 AMD 的语法做了兼容, 方便迁移代码

不过实际上, 引用模块的规则是依据 CommonJS 来的
require('lodash') // 从模块目录查找
require('./file') // 按相对路径查找
AMD 语法中, 也要注意, 是按 CommonJS 的方案查找的

```

define (require, exports. module) ->
　require('lodash') # commonjs 当中这样是查找模块的
　require('./file')


* 特殊模块的Shim

```

	{test: require.resolve('jquery'), loader: 'expose?jQuery'},
	{test: require.resolve('pen'), loader: 'exports?window.Pen'},

* 基本使用

```
	// webpack.config.js
	module.exports = {
	　entry: './main.js',
	　output: {
	　　filename: 'bundle.js'　　　　
	　}
	};


	// webpack.config.js
	module.exports = {
	　entry: './main.js',
	　output: {
	　　path: './build', // This is where images AND js will go
	　　publicPath: 'http://mycdn.com/', // This is used to generate URLs to e.g. images
	　　filename: 'bundle.js'
	　},
	　module: {
	　　loaders: [
	　　　{ test: /\.less$/, loader: 'style-loader!css-loader!less-loader' }, // use ! to chain loaders
	　　　{ test: /\.css$/, loader: 'style-loader!css-loader' },
	　　　{test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'} // inline base64 URLs for <=8k images, direct URLs for the rest
	　　]
	　}
	};

1. url-loader

url-loader

```
	.demo {
	　background-image: url('a.png');
	}

	module: {
	　loaders: [
	　　{test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'} // inline base64 URLs for <=8k images, direct URLs for the rest
	　]
	}

2. file-loader

```

* 打成多个包

	// webpack.config.js
	var webpack = require('webpack');
	var commonsPlugin = new webpack.optimize.CommonsChunkPlugin('common.js');

	module.exports = {
	　entry: {
	　　Profile: './profile.js',
	　　Feed: './feed.js'
	　},
	　output: {
	　　path: 'build',
	　　filename: '[name].js' // Template based on keys in entry above
	　},
	　plugins: [commonsPlugin]
	};
	require("file?name=[path][name].[ext]?[hash]!./dir/file.png")

* 对文件做hash

对文件做 revision
