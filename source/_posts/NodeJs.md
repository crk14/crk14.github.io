### Node.js 是一个基于Chrome V8引擎的JavaScript运行环境

> ### node.js官网： https://nodejs.org/en/
### node.js特点
#### 单线程  非阻塞I/O(异步)  事件驱动
<!-- more -->
#### 查看版本
#### 打开cmd，输入node -v

1. ###### windows系统命令行：
``` bash
    打开方式：win + r  输入 cmd 回车
   命令 c: 或 d: 或 e:  进入相应的磁盘
   命令 mkdir xx  创建xx目录
   命令 cd xx  进入xx文件夹
   命令 cd ..  返回上一级目录
   命令 cd /  返回根目录
   命令 echo.> xx.xx  创建xx文件(包含换行的文件)
   命令 dir  查看当前目录下的全部文件
   命令 del xx  删除xx文件
   命令 cls  清屏
   命令 exit  退出cmd窗口

命令 ipconfig  查看本机ip地址( 系统环境变量Path末尾处加上 ";C:\Windows\System32" )
```
### NPM介绍
#### 官网：https://www.npmjs.cn/
#### NPM是随同NodeJS一起安装的包管理工具，包的结构使您能够轻松跟踪依赖项和版本。
#### NPM能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：
#### 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
#### 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
#### 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。
```bash
生成 package.json 配置文件
$ npm init

$ npm init -y  跳过所有提问
安装包

本地安装（当前项目能访问到）
$ npm install 包名

全局安装（其他项目都能访问到）
$ npm install 包名 -global

缩写形式
$ npm i 包名 -g

项目依赖（添加到dependencies）
$ npm install 包名 -save
项目上线需要用到的包，缩写 $ npm install 包名 -S (大写)

开发依赖（添加到devDependencies）
$ npm install 包名 --save-dev
开发测试需要用到的包，缩写 $ npm install 包名 -D (大写)

移除依赖模块
$ npm uninstall 包名 -save
$ npm uninstall 包名 --save-dev

清除缓存数据
npm cache verify
如报错 -4048 时使用

淘宝 NPM 镜像
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
```bash
## 编写nodejs程序
方式一：在window命令行环境中输入指令node并回车，进行node的交互式环境,编写javascript代码执行即可。其中node交互式环境也称之为REPL(Read Eval Print Loop-读取评估打印循环 )，按两次ctrl+c,可退出REPL环境。

先输入node指令，进入node的交互式环境，再输入js代码。

方式二：把javascript代码写在后缀为.js的文件中
如有一个hello.js文件，在window命令行中输入node hello.js即可执行。
注：在浏览器环境中全局对象是window，在node环境中全局对象变为global
```
## 搭建web服务器
文档链接：http://nodejs.cn/api/http.html#http_http_createserver_options_requestlistener
```bash
步骤：
    1. 加载http模块
    2. 创建http服务
    3. 服务端对象监听request 请求事件，用于监听客户端的请求
    4. 启动http服务，监听端口

参考代码：
1. 加载http模块 var http = require('http');
2. 创建http服务 var server = http.createServer();
3. 服务对象监听request 请求事件，用于监听客户端的请求
server.on('request',function (req, res) {
    //req-请求对象 , res-响应对象
    //处理客户端请求逻辑
    console.log('收到请求: '+ req.url); //用户请求地址
    res.end(); //必须结束响应，否则浏览器会被挂起
});
4. 启动http服务，开始监听3000端口
server.listen(3000, function () {
    console.log('服务已经启动，请访问： http://localhost:3000 或 http://127.0.0.1:3000');
});
```

注意：
 1. 在监听request事件中，最后一定要res.end()结束响应。
 2. 浏览器显示中文可能是乱码，需设置响应头告诉浏览器显示时所使用的编码，要在res.end()之前设置

 **node.js没有根目录、没有web容器的概念！**

 ### nodejs 读写文件
 使用到的文件系统模块 var fs = require('fs');  // file system
```bash
读文件：fs.readFile(file[, options], callback)
    * 参数1：要读取的文件路径，必填。
    * 参数2：读取文件时的选项，比如：文件编码utf8。选填。
    * 参数3：文件读取完毕后的回调函数，必填。
    读文件注意：
    * 该操作采用异步执行
    * 回调函数有两个参数，分别是err和data
    * 如果读取文件时没有指定编码，返回的是二进制数据，如指定编码utf8，会返回指定的编码数据。
    * 只要异步操作，回调函数第一个都是错误对象err优先

写文件：fs.writeFile(file, data[, options], callback);
    * 参数1：要写入的文件路径，必填。
    * 参数2：要写入的数据，必填。
    * 参数3：写入文件时的选项，比如：文件编码。
    * 参数4：文件写入完毕后的回调函数，必填。

写文件注意：
    * 该操作采用异步执行
    * 如果文件存在则替换原内容
    * 默认写入的文件编码为utf8
    * 回调函数有1个参数：err，表示在写入文件的操作过程中是否出错了。
    * 如果出错了err != null，成功时 err === null
    * 写入文件（文件不存在则自动创建）
    ```

注：writeFile写入文件是先把文件内容清空再写入，如果要追加写入的话可以使用appendFile函数