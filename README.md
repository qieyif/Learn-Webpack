# Webpack学习

> * ***webpack*** 是模块化开发的工具。号称**模块打包机**。
> * ***webpack*** 的功能比 gulp grunt更加强大。是前端开发必不可少的工具了。所以熟练掌握 ***webpack*** 是势在必行的！


## webpack安装

```javascript
    //全局安装
    npm install -g webpack

```

#### 项目中开始使用webpack：

第一步：创建  ***package.json*** 文件

```javascript
     //初始化一个项目
     npm init
```
第二步：本地安装 ***webpack*** 

```javascript
    //本地安装webpack 同时--save-dev 保存到packag.json文件中的开发依赖中 以后再次使用直接执行 npm install即可
    npm install --save-dev webpack
```
---
##### 小试牛刀：  

第一步：先创建一个index.html文件 创建一个js文件夹：

```js
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>webpack学习</title>
    </head>
    <body>
        <h1>Hello Webpack</h1>

        <script src="js/index.js"></script>
    </body>
    </html>
```
第二步：创建src文件夹 用来放置编译前也就是开发代码。src下创建app.js作为编译前的js入口文件, 创建scripts文件夹 用来放置js文件，也就是不同的模块。scripts下创建两个js文件 分别是bundle.js 和 util.js。

* app.js:

```js
    require('./scripts/bundle.js');
    require('./scripts/util.js');
```

* bundle.js:

```js
    console.log('this is bundle.js ...');
```

* util.js:

```js
    console.log('this is util.js ...');
```

###### 接下来用webpack打包：
```js
    webpack src/app.js js  js/index.js
```

命令行执行效果：

```bash
    $ webpack src/app.js js/index.js
    Hash: 991700bcc93185723c3f
    Version: webpack 2.6.1
    Time: 62ms
       Asset     Size  Chunks             Chunk Names
    index.js  2.89 kB       0  [emitted]  main
       [0] ./src/scripts/bundle.js 37 bytes {0} [built]
       [1] ./src/scripts/util.js 37 bytes {0} [built]
       [2] ./src/app.js 64 bytes {0} [built]

```
然后运行 ***index.html*** 到浏览器，打开控制台，就可以看到 打印了bundle.js 和 util.js 里面的代码。

---

#### webpack配置文件 （***webpack.config.js***）
* 首先webpack遵循 *** CommonJS*** 规范。
* 所以执行上面的代码有的麻烦，那么就在根目录下创建一个webpack的配置js文件，可以当做是js的一个模块。

```js
	module.exports = {
      entry:  __dirname + "/src/app.js", //已多次提及的唯一入口文件
      output: {
        path: __dirname + "/js",//打包后的文件存放的地方
        filename: "index.js" //打包后输出文件的文件名
      }
    }
```
`现在只需要在命令行里执行 ` ***webpack*** `即可！` *运行的结果同上*

---
#### 更加快捷，也是比较通用的打包 :
* 执行类似于node_modules/.bin/webpack这样的命令其实是比较烦人且容易出错的，不过值得庆幸的是npm可以引导任务执行，对其进行配置后可以使用简单的npm start命令来代替这些繁琐的命令。在 ***package.json*** 中对npm的脚本部分进行相关设置即可，设置方法如下:

```js
    {
      "name": "webpack-sample-project",
      "version": "1.0.0",
      "description": "Sample webpack project",
      "scripts": {
        "start": "webpack" //配置的地方就是这里啦，相当于把npm的start命令指向webpack命令
      },
      "author": "zhang",
      "license": "ISC",
      "devDependencies": {
        "webpack": "^1.12.9"
      }
    }
```
`接着，只需要执行` ***npm start*** 命令即可。

---

