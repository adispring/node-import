# 在 Nodejs 中使用 import

## 一、 安装必须的库:

### 1. [babel-preset-es2015](http://babeljs.io/docs/plugins/preset-es2015/):

### 2. [babel-preset-stage-2](http://babeljs.io/docs/plugins/preset-stage-2/):

This preset includes the following plugins:

- syntax-dynamic-import
- transform-class-properties
- transform-decorators – disabled pending proposal update (can use the legacy transform in the meantime)

And all plugins from presets:

preset-stage-3

### 3. [babel-register](https://babeljs.io/docs/usage/babel-register/): 

babel-register 模块改写 require 命令，为它加上一个钩子。此后，每当使用 require 加载 .js、.jsx、.es 和 .es6 后缀名的文件，就会先用 Babel 进行转码。

```console
$ npm install --save-dev babel-register
```

使用时，必须首先加载babel-register。

```js
require("babel-register");
require("./index.js");
```

然后，就不需要手动对index.js转码了。

需要注意的是，babel-register只会对require命令加载的文件转码，而不会对当前文件转码。另外，由于它是实时转码，所以**只适合在开发环境使用** 。

## 二、 babelrc 配置

```json
{
  presets: [ "es2015", "stage-2"],
}
```

## 三、 在 Nodejs 使用 import 代替 require 引入库

假如要在 `server.js` 中使用 `import`，先创建一个 `index.js`, 在 `index.js` 中先注册 babel: `require(babel-register)`, 此后，在 index.js 中使用 require  加载 .js、.jsx、.es 和 .es6 后缀名的文件，就会先用 Babel 进行转码。这样就可以在 server.js 中使用 `import` 了。

index.js

```js
require("babel-register");
require("./server.js");
```

## Explaination

The TC39 categorizes proposals into the following stages:

Stage 0 - Strawman: just an idea, possible Babel plugin.
Stage 1 - Proposal: this is worth working on.
Stage 2 - Draft: initial spec.
Stage 3 - Candidate: complete spec and initial browser implementations.
Stage 4 - Finished: will be added to the next yearly release.
