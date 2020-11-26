---
title: webpack-plugin-初始
date: 2020-11-24 09:47:19
tags: webpack
---

## webpack-plugin
loader，通常就是扮演一个翻译角色。
plugin可以做到比loader更复杂的功能。

## 第一个plugin配置使用

第一个plugin就是html-webpack-plugin,这个插件的作用就是复刻一个index.html模板到dist目录下,并把依赖都自动载入到index.html中,再配合webpack-dev-server使用事就很方便了。

步骤：
1. 安装html-webpack-plugin
2. 导入html-webpack-plugin
3. 实例化，并配置模板路径

```js
const path = require('path')
const template = require('html-webpack-plugin')
module.exports = {
    mode:: 'development',
    context: path.resolve(__dirname,  './webpack-html-plugin'),
    entry: './src/index.js',
    output: {
        filename: 'main.js'
    },
    modules: {
        rules: [
            {
                test: /\.css$/,
                use:[
                    'style-loader',
                    'css-loader'
                ]
            }
        ]
    },
    plugins: {
        new template(
            {
                template: './src/index.html'
            }
        )
    }
}
```
