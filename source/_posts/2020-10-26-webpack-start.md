---
title: webpack-start
date: 2020-10-26 11:07:32
tags: webpack
---

# webpack快速入门


## 安装webpack

- webpack依赖于node,必须所以先安装node。

- 初始化webpack-demo项目

```bash
mkdir webpack-demo2
cd webpack-demo2
npm init -y
npm i webpack webpack-cli
```

- webpack的安装分为全局安装和局部安装，推荐使用局部安装。

不使用 -g 命令就不是全局安装。

```bash

# 不填参数，默认表示dev 等效于  -s
npm i webpack 
#等效于
npm i webpack -s

# 保存为开发依赖项 -d
npm i webpack -d

```

### 打包第一个项目

1. 创建三个文件， index.js, index.html, add-content.js

index.js

```js
import addContent from './add-content.js'
document.write('webpack demo01')
addContent()
```

index.html

其中引入得js文件时打包出来的文件，需要执行接下来的打包命令之后才有

```html
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script src="./dist/bundle.js"></script>
    
</body>
</html>
```
add-content.js

```js
export default function(){
    document.write('webpack')
}
```

2. 执行打包命令

三个文件都准备好之后，执行打包命令进行打包。

```bash
npx webpack --entry=./index.js --output-filename=bundle.js --mode=development
```
解释一下，npx,局部安装使用这个命令。

npx webpack, 使用webpack打包。

--entry=./index.js, 入口文件为index.js。

--output-filename=bundle.js, 打包后的输出文件名叫bundle.js。

--mode=development, 打包方式为开发模式。

打包完成后，输出的文件在， ./dist/bundle.js。也就是我们在index.html引入的js文件路径。这个路径是webpack默认的。

3. 脚本命令简化打包

每次打包都要输入一长串的命令，不仅不方便还容易出错，所以我们可以借助npm脚本命令来简化打包。

在 package.json 文件下的 script 字段对象里添加以下

```json
"build": "webpack --entry=./index.js --output-filename=bundle.js --mode=development"
```

把 index.js 里修改

```js
document.write("<h1>webpack</h1>")
```

这下打包只需要执行,在浏览器打开 index.html，即可看到变化

```bash
npm run build
```

### 使用默认目录

创建一个src文件夹, 将add-content.js和index.js 移动到 src 里面。

在 package.json 里打包命令可以变成这样

```json
"build": "webpack --output-filename=bundle.js --mode=development"
```

如果把输出路径也改了
```json
"build": "webpack --mode=development"
```

可以得到结果 webpack 的默认入口是 src/index.js, 默认输出是 dist/main.js

### 使用配置文件

创建 webpack.config.js 文件。添加以下内容

```js
module.exports = {
    entry: "./src/index.js",
    output: {
        filename: "main.js"
    },
    mode: "development"
}
```

package.json, 改成以下

```json
"build": "webpack"
```

可以看到，配置文件把命令都以对象的方式填写进去了，脚本就变得越来越简单了。

### 使用 webpack-dev-server

![hexo](hexo.jpg)