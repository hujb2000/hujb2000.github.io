1. cd easynode-icp; webpack-dev-server --content-base plugins

2. http://localhost:8080/webpack-dev-server/views/index.html

3. npm install file-loader url-loader --save-dev

4.  npm install  webpack --save-dev

5. 3rd-party plugins

	npm install html-webpack-plugin open-browser-webpack-plugin --save-dev

6. You can enable some codes only in development environment with environment flags

	env DEBUG=true weback

7. Code splitting

	For big wen apps it's not efficient to put all code into a single file.  Webpack allows you to split them into serveral chunks.

	Especially if some blocks of code are only required under some circumstances. these chunks could be loaded on demand

* on demand

    copy 1.../build/1.js to views directory, now the page'll work.


8. Common chunk

When multi scripts have common chunks. you can extract the common part into a separate file with CommonsChunkPlugin.

9. Vendor chunk

npm install jquery --save-dev

 You can also extract the vendor libraries from a script into a separate  file with CommonsChunkPlugin.

10. Vendor chunk use ProvidePlugin

If you want a module available as variable in every module. such as making $ and jQuery available in every module without

writing require('jquery') . Your should use ProvidePlugin

11. Exposing global variables

If your want to use some global variables , and don't want to includes them in  teh Webpack bundle, you can enable externals filed in webpack.config.js


12. Hot Module Replacement

npm install webpack-dev-server --save-dev

cd plugins

webpack --watch

13. React router

npm install react-router

14. webstorm JSX Emmet

File | Settings | Editor | Emmet - JSX for Windows and Unix

WebStorm | Preferences | Editor | Emmet - JSX for OS X

15. babel-loader

Webpack plugin for Babel

16. react-hot-loader

Cannot define 'query' and multiple loaders in loaders list

loaders: ['react-hot', 'babel']
query: {
                    presets: ['es2015', 'react']
      },
Q: How to solve?
query json object as query parameter?

17. Matcher

{ test: /\.(js|jsx)$/, loader: 'babel-loader' } - 匹配 js 和 jsx

import UploadPhoto from './forms/UploadPhoto.jsx';

18.  webpack_and_react

JSX is a superset of JavaScript that allows you to mix XMLish syntax with JavaScript

 You can expect bundle sizes for small applications to be around 150-200k, React included

19. Webstrom turn off updating indecies

Mark directory  as/Excluded

20.
[icp_ui](file:///Users/hujiabao/workspace_docker/icp/icp_ui/%E9%A1%B5%E9%9D%A2%E6%A0%87%E6%B3%A8%E5%AF%BC%E5%87%BA/index.html)

21. plugins

cd plugins;  webpack -w & mcss mcss/index.mcss -o css/ -w
cd ..; webpack-dev-server --content-base plugins --port 80

22. fieldset没有问题,legend margin-left设置有问题不用,改用div替代, 整体在form外的div里设置margin

23. 原生option高度不可调的,很多样式不支持,需要div模拟

24. <label><input type="checkbox" name="3"><span>英语</span></label> 点中文字也能选中
	<input type="checkbox" name="4"><span>日语</span> 这样点中文字不能选中

25. 行内元素,对宽度没有影响, 必须设置为块

26. popover 用绝对定位, 元素用relative, 本元素用absolute

27. 相差一个像素是小数点的缘故( 350-15*3 - 2*4)/4 , border-width=2

28. Mac chrome浏览器下, select 设置高度无效,要先设置下border: 1px solid #

29.  psd-> sketch(marketch plugin)->html
    psd->svg(Affinity design)
* Affinity Design
Affinity Designer是一款专业的设计绘图工具，适用于苹果操作系统，主要用于矢量图形的绘制，适用于图标、UI 设计、网站设计、宣传素材等图像的制作，具有较强的易用性，操作也十分方便

30. loginCallback

[2016-01-11 19:51:45.135] [INFO] console - tenantId b261f52d302b43ba821a6d731b17034c
[2016-01-11 19:51:45.135] [INFO] console - expire Mon Jan 11 2016 19:52:00 GMT+0800 (CST)
[2016-01-11 19:51:45.136] [INFO] console - status 1
[2016-01-11 19:51:45.136] [INFO] console - regIn undefined
[2016-01-11 19:51:45.136] [INFO] console - persist e8edea596b18befda5525e266951a58398d86e758d19a2e7aa224fc9661e79a9ad36ea9d4a5a3912e72bd326ebd2292eb04d6b92226285e68b255796c1f4c08982f9ea690d34e03e98a6603b6b35090d
[2016-01-11 19:51:45.136] [INFO] console - code 200
[2016-01-11 19:51:45.136] [INFO] console - loginType 1
[2016-01-11 19:51:45.136] [INFO] console - sign l0QGcLPrWAo2pe5xLfQcAs4sjnzBem87MQHcd4UC7Zw=
[2016-01-11 19:51:45.136] [INFO] console - category 0
[2016-01-11 19:51:45.136] [INFO] console - email hujb2000@163.com
[2016-01-11 19:51:45.136] [INFO] console - callback https://c.163.com/?action=login
[2016-01-11 19:51:45.136] [INFO] console - userName hujb2000@163.com

31. React的每个组件包含状态和属性，且状态和属性和dom隔离。dom的部分就是动态模板。
1. React认为页面dom不可变，所以当状态和属性发生变化时会re-render dom。
2. React的会根据新的状态和属性生成新的VirtualDOM Tree然后和旧的VirtualDOM Tree做对比(类似于版本控制的机制)。
3. 通过对比计算出最小的更新代价，然后将这些更新的方法进入队列。
4. 批量更新。

31. setState 是异步操作 this.state不能获取到值
handleNature: function(e){
        e.preventDefault();
        this.setState({nature: e.target.value});
        console.log("nature",e.target.value);
    },


32.  popoover
farther: position: relative
son: postion: absolute; left: 100%指为farther的宽度,margin-top: 10p

> select {
    width: 100%;
    height: $m-companyinfo_item_height;
}

select.item-ctrl-three{

32.  {this.state.idTypeEnable == 0 ? 'disabled':''} 用不起来

33.
 //externals: {'react': 'React', 'react-dom': 'ReactDOM'},
  plugins: [
    new webpack.optimize.OccurenceOrderPlugin(),
    new webpack.DefinePlugin({
      'process.env': {
        'NODE_ENV': JSON.stringify('production')
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      compressor: {
        warnings: false
      }
    })
  ],
  module: {
    loaders: [
      { test: /\.jsx?$/, loaders: ['babel'] },
      { test: /\.(css|less)$/, loader: 'style-loader!css-loader?localIdentName=[hash:base64:8]!less-loader' },
      { test: /\.(ttf|eot|woff|woff2|otf|svg)/, loader: 'file-loader?name=./font/[name].[ext]' },
      { test: /\.json$/, loader: 'file-loader?name=./json/[name].json' },
      { test: /\.(png|jpg|jpeg|gif)$/, loader: 'url-loader?limit=10000&name=./images/[name].[ext]' },
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'react']
        },
        include: path.join(__dirname,'.')
      }
    ]
  }

34. 处理file样式
farther: position: relative,  overflow : hidden;
file:    position: absolute,  bottom: 0, opacity: 0, border: 1px solid #ccc;  font-size: 200px;

35. model field defined ,can't camelNamed, and database table filed named can't use camelName,
操作数据库字段全为小写,注意

36. ant.design  基于react, validate

37. App.js 到了 Linux下变成app.js了,后来改成 App.jsx OK, 是Linux下git忽烈大小写的问题

38. sh start.sh 把../views/index.html改成 ../views/index2.html
  如果本地调试时../views/index2.html改成 ../views/index.html

39. .item-ctrl不要设置高度,由内容撑开

40. 用了postion: absolute,不要用margin-top,margin-left:去定位了,改用
right: 10px;
top: 10px;
z-index: 2;

41. var count = this.state.sitesCount+1; 不用用  var count = this.state.sitesCount++
            this.setState({
                sitesCount: count
            });

42. easynode 用了 upload跟径,改用 /upl

CREATE TABLE `website` (
	`id` bigint(20) NOT NULL COMMENT '记录ID',
	`name` varchar(50) NOT NULL COMMENT '网站名称',
	`domain` varchar(256) NOT NULL COMMENT '网站域名',
	`domain1` varchar(256) DEFAULT NULL COMMENT '网站域名1',
	`domain2` varchar(256) DEFAULT NULL COMMENT '网站域名2',
	`domain3` varchar(256) DEFAULT NULL COMMENT '网站域名3',
	`domain4` varchar(256) DEFAULT NULL COMMENT '网站域名4\n',
	`homeurl` varchar(256) NOT NULL COMMENT '网站首页URL',
	`servicecontent` varchar(256) NOT NULL COMMENT '网站服务内容',
	`languages` varchar(256) NOT NULL COMMENT '网站语言,json结构',
	`ispname` varchar(256) NOT NULL COMMENT 'ISP名称',
	`ip` varchar(32) NOT NULL COMMENT '网站IP地址:1.2.3.4',
	`accessmethod` varchar(100) NOT NULL COMMENT '网站接入方式,json结构',
	`serverregion` varchar(32) NOT NULL COMMENT '服务器放置地:json结构',
	`managername` varchar(32) NOT NULL COMMENT '负责人姓名',
	`idtype` tinyint(1) NOT NULL COMMENT '证件类型：1-身分证 2-护照 3-军官证 4-台胞证',
	`idnumber` varchar(50) NOT NULL COMMENT '证件号码',
	`officephoneregion` varchar(10) NOT NULL COMMENT '办公室电话区号',
	`officephonenumber` varchar(20) NOT NULL COMMENT '办公室电话号码',
	`mobile` varchar(20) NOT NULL COMMENT '手机号码',
	`email` varchar(50) NOT NULL COMMENT '电子邮箱',
	`qq` varchar(50) DEFAULT NULL COMMENT 'qq号码',
	`updatetime` bigint(20) NOT NULL COMMENT '记录更新时间',
	`createtime` bigint(20) NOT NULL COMMENT '记录创建时间',
	PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4



43.  etc/EasyNode.conf easynode.framework.mvc.model.defaultIdFieldName = id 修改identify fieldname


44.  static savedraft(app){
                var me = this;
                return function *(){
                    console.log("sessionid");
                    console.dir(this.cookies.get('koa.sid'));

45. serverregion , website.serverregion record website.serverregion varchar
 "1"=>hz1

46. sh-3.2# host icp.hzspeed.cn
    icp.hzspeed.cn is an alias for hzspeed.cn.
    hzspeed.cn has address 115.28.79.35
    hzspeed.cn has address 218.205.113.98

47.
React automatically understands booleans for this purpose, so you can simply write

<option value={option.value} selected={optionsState == option.value}>{option.label}</option>
and it will output 'selected' appropriately.

However, React makes this even easier for you. Instead of defining selected on each option, you can (and should) simply write value={optionsState} on the select tag itself:

<select value="B">
  <option value="A">Apple</option>
  <option value="B">Banana</option>
  <option value="C">Cranberry</option>
</select>

48.aliyun rds, program and cloud console not inconsistent

49. can't work
UPDATE record SET COMPANYID = 88 WHERE ID = 0
model.merge( Object.assign({}, {id:id,websiteid:websiteid} ));
                       r = yield conn.update(model);

50. ip varchar(32)  存为JSON字符串时不够长,截断了.

51. 这样HEADER Request header为空,只家{page:1}
var tid = __globals__.user == undefined ? '111111' : __globals__.user.tenantId;
        reqwest({
            url: '/getapplyrecord',
            method: 'post',
            data: JSON.stringify({page:1,tenantId:1}),

var reqData = {page:1,tenantId:tid};
        reqwest({
            url: '/getapplyrecord',
            method: 'post',
            data: reqData,
            提示
            17:59:35.954] [ERROR] console -   Error: invalid JSON, only supports object and array
                  at parse (/Users/hujiabao/workspace_docker/icp/easynode-icp/node_modules/koa-body/node_modules/co-body/lib/json.js:53:13)
                  at /Users/hujiabao/workspace_docker/icp/easynode-icp/node_modules/koa-body/node_modules/co-body/lib/json.js:39:16
                  at run (/usr/local/lib/node_modules/babel-cli/node_modules/babel-polyfill/node_modules/core-js/modules/es6.promise.js:104:47)
                  at /usr/local/lib/node_modules/babel-cli/node_modules/babel-polyfill/node_modules/core-js/modules/es6.promise.js:115:28
                  at flush (/usr/local/lib/node_modules/babel-cli/node_modules/babel-polyfill/node_modules/core-js/modules/$.microtask.js:19:5)
                  at doNTCallback0 (node.js:407:9)
                  at process._tickDomainCallback (node.js:377:13)
还必须是字符串.

52. after page refresh, the  __globals__ only keep the user and logincallback object.

53. onload发生在 login之后,

54. deploy based on docker tecknology:
 * docker pull node@5.5.0-wheezy
 * docker run -t -i --name node  node@5.5.0-wheezy /bin/bash
 * npm install -g cnpm --registry=https://r.cnpmjs.org
 * npm install -g babel-cli
 * npm install -g webpack
 * docker commit -m "cnpm,babel,webpack" -a "hujiabao" 6b075ceaa41d  hujb2000/easynode@5.5.0
 * edit Dockerfile
 ```
	FROM hujb2000/easynode@5.5.0

	MAINTAINER hujiabao

	RUN mkdir -p /usr/src/app

	COPY . /usr/src/app

	WORKDIR /usr/src/app
	RUN cnpm install

	WORKDIR /usr/src/app/plugins
	RUN webpack --config webpack.prod.config.js

	WORKDIR /usr/src/app/bin

	CMD ["./start.sh"]
 * docker build -t hujb2000/icp@0.0.2 .
 * docker run -ti --name bbb --env CONFIG_URL='http://218.205.113.98:6006/configicp_prod.json' hujb2000/icp@0.0.2
 * docker run -ti --name ddd --net=host --env CONFIG_URL='http://218.205.113.98:6006/configicp.json' hujb2000/icp@0.0.1

 55. deploy to c.163.com
 * docker login –u 用户名 –p 密码 –e 邮箱 hub.c.163.com // docker login –u 用户名 –e 邮箱 hub.c.163.com
 * docker tag hujb2000/icp@0.0.1 hub.c.163.com/hujb2000/icp@0.0.1
 * docker push hub.c.163.com/hujb2000/icp@0.0.1
 * start container server, map the host and container port, and start lb, inject the CONFIG_URL env.

CONFIG_URL: http://218.205.113.98:6006/configicp_prod.json
PORT: 80 || 8899

 56. 数据库所有设置为小字字段暂时作为一个原则,因为easynode's bug

57. fc's container access fc's rds fail, but can't look log, site bug,  It's ok to access fc's rds by local hos

58. easynode对delete 方法有问题
console.log( this.parameter );
console.log( this.body );
console.log( this.query );取不到数据

reqwest({
    url: '/records',
    method: 'delete',
    data: {id:this.props.record.id},
    type:'json'

59. validator , 对长度,内容,失焦和提交时做校验, validator.js前端,后端用koa-validate

60. whitelist

61. test: react: 0.14.7 , ee.target 会null ,回退出0.14.6,重新webpack 则ok
onChange: function(ee){
    var file = ee.target.files[0];

62. Mac  webpack 0.12.12 suppprt width character, but linux 0.12.11 and 0.12.14 can't support width character

63.
down vote
favorite
3
What is the difference between a shim an a sham?

Is it enough to include es5-shim.min.js and es6-shim.min.js or should I also include es5-sham.min.js and es6-sham.min.js?

64. babel-node Utilities.js

65. IE10中ajax的responseText内容不正确，因IE10的缓存304导致 ie8,11 OK, 唯独IE10

66. starting  service [icp],  HTTP port: [80]
    module.js:341
        throw err;
        ^

    Error: Cannot find module 'core-js/library/fn/get-iterator'
        at Function.Module._resolveFilename (module.js:339:15)
        at Function.Module._load (module.js:290:25)
        at Module.require (module.js:367:17)
        at require (internal/module.js:16:19)
        at Object.<anonymous> (/usr/src/app/node_modules/babel-runtime/core-js/get-iterator.js:1:93)
        at Module._compile (module.js:413:34)
        at Module._extensions..js (module.js:422:10)
        at Object.require.extensions.(anonymous function) [as .js] (/usr/local/lib/node_modules/babel-cli/node_modules/babel-register/lib/node.js:136:7)
        at Module.load (module.js:357:32)
        at Function.Module._load (module.js:314:12)

node_modules/babel-runtime, npm 网络问题,一般,2~3分钟,时间长有问题?

67.  减小压缩文件webpack --config webpack.prod.config.js  -w

68. http://**/views/docs/#api-Ops-getRecordb

69. 私有网部署
http://cloud.netease.com/vpn  获取VPN密码,每次登陆重新获取一次

70. .babelrc can't add to .dockerignore文件中

71. 测试环境,检查下c.163.com RDS白名单设置: docker run -d --name icp93 -p 8899:8899 -e CONFIG_URL="http://static.hzspeed.cn/configicpfc.json" -e PORT=8899 hub.c.163.com/hujb2000/icp:0.0.9

72. 类似List控制, 图片预览要定义成一个组件,而不是到模块里面

外面是:display:table,里面是:display:table-cell
.m-uploadmaterial-ctrl-picture-table{
		display: table;
		width: 140px;
		height: 140px;
		table-layout: fixed;
	}

	.m-uploadmaterial-ctrl-picture{
		width: 140px;
		height: 140px;
		background: #f5f5f5;
		border: 1px solid #DDD;
		display: table-cell;
        vertical-align: middle;
        text-align: center;
		> img {
            max-height: 100%;
            max-width: 100%;
	    }

	}

73. finaly 的return 为准

74. prod config http://apollodev.nos.netease.com/1457513596557

75. hz3/hz15 can enter

76. 注释模板
        /**
         * @method 上报数据
         * @apiName isp_upload
         * @apiGroup ISP
         * @apiPermission whitelist
         * @apiVersion 0.0.2
         *
         * @apiDescription 通过白名单管理权限
         *
         * @apiParam {Number} filter 查询状态过滤条件 0-全部(除草稿) 1-待审核  2-已审核通过 3-审核失败的
         * @apiParam {Number} page 页号.
         * @apiParam {Number} rpp  每页记录数.
         *
         * @apiSampleRequest http://icp.hzspeed.cn/records
         *
         * @apiSuccess {Object[]} data 记录列表
         * @apiSuccess {Number} data.id 记录id
         * @apiSuccess {String} data.checklisturl 核验单图片URL
         * @apiSuccess {String} data.protocolurl1 云平台协议第一页图片
         * @apiSuccess {String} data.protocolurl2 云平台协议第二页图片
         * @apiSuccess {String} data.securityurl1 信息安全管理责任书第一页图片URL
         * @apiSuccess {String} data.securityurl2 信息安全管理责任书第二页图片URL
         * @apiSuccess {Number} data.companyid 公司id
         * @apiSuccess {Number} data.websiteid 网站id
         * @apiSuccess {String} data.tenantid 租户id
         * @apiSuccess {Number} data.type  备案类型: 0-首次备案, 1-新增网站, 2-新增接入
         * @apiSuccess {Number} data.status 备案状态: 0-草稿,1-初审中,2-初审未通过,3-初审已通过,4-照片审核中,5-照片审核未通过,6-照片审核已通过,7-通管局审核中,8-通管局审核未通过,9-通管局审核已通过,10-未知状态
         * @apiSuccess {String} data.code 备案编号
         * @apiSuccess {Number} data.updatetime 记录更新时间
         * @apiSuccess {Number} data.createtime 记录创建时间
         * @apiSuccess {Number} page 页号
         * @apiSuccess {Number} pages 总页数
         * @apiSuccess {Number} rows 总记录数
         * @apiSuccess {Number} rpp 每页显示数
         *
         * @apiUse  EmptyRecord
         */

77. ReferenceError: regeneratorRuntime is not defined

cnpm install  babel-polyfill --save-dev

require("babel-polyfill");
