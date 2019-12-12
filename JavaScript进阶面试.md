# JavaScript进阶面试

## 1. `ES6`模块化如何使用，开发环境如何打包

- 模块化的基本语法
- 开发环境配置
- 关于`JS`众多模块化标准

基本语法

export语法

```javascript
// util1.js
export default {
	a: 100
}

// util2.js
export function fn1(){
    alert('fn1')
}
export function fn2(){
    alert('fn2')
}
```

import语法

```javascript
// index.js
import util1 from './util1.js'
import { fn1, fn2 } from './util2.js'
console.log(util1)
fn1();
fn2();
```

开发环境 - babel

- 电脑有 node 环境，运行 `npm init`
- `npm i -D babel-core babel-preset-es2015 babel-preset-latest`
- 创建 `.babelrc` 文件
- `npm i --global babel-cli`
- `babel --version`

开发环境 - webpack

- `npm i webpack babel-loader -D`

- 配置 `webpack.config.js`

- 配置 `package.json`中的 `scripts`

  "start": "webpack"

- 运行 `npm start`

```javascript
// webpack.config.js
module.exports = {
    entry: './src/index.js',
    output: {
        path; __dirname,
        filename: './build/bundle.js'
    },
    module: {
        rules: [{
            test: /\.js?$/,
            exclude: /(node_modules)/,
            loader: 'babel-loader'
        }]
    }
}
```

开发环境 - rollup

- `npm i`

- `npm i rollup rollup-plugin-node-resolve rollup-plugin-babel babel-plugin-external-helpers babel-preset-latest babel-core -D`

- 配置 `.babelrc`

  ```javascript
  {
      "presets": [
          [
              "latest", {
                  "es2015": {
                      "modules": false
                  }
              }
          ]
      ],
      "plugins": ["external-helpers"]
  }
  ```

- 配置 `rollup.config.js`

  ```javascript
  import babel from 'rollup-plugin-babel'
  import resolve from 'rollup-plugin-node-resolve'
  
  export default {
      entry: "./src/index.js",
      format: 'umd',
      plugins: [
          resolve(),
          babel({
              exclude: "node_modules/**"
          })
      ],
      dest: 'build/bundle.js'
  }
  ```

- 修改`package.json`的`scripts`

  `"start": "rollup -c rollup.config.js"`

- 运行`npm start`

`rollup` 功能单一，`webpack`功能强大

参考设计原则和《Linux/Unix设计思想》

工具要尽量功能单一，可集成，可扩展



关于JS众多模块化标准

- `AMD`成为标准， `require.js` （也有`CMD`）
- 前端打包工具，使用 `node.js`模块化可以被使用
- `ES6`出现，想统一现在所有模块化标准
- `nodeJs`积极支持，浏览器尚未统一
- 可以自造`lib`，但是不要自造标准

问题解答：

- 语法：`import` `export`（注意有无default）
- 环境： `babel`编译 `ES6`语法，模块化可用`webpack` 和 `rollup`
- 扩展： 说一下自己对模块化标准统一的期待



## 2. `Class` 和普通构造函数有何区别

- `JS`构造函数
- `Class`基本语法
- 语法糖
- 继承

例子：

```jsx
class Ad extends React.Component {
    constructor(props){
        super(props);
        this.state = {
            data: []
        }
    }
    render(){
        return (
            <div>hello world</div>
        )
    }
    componentDidMount(){
        
    }
}
```

`JS`构造函数

```javascript
function MathHandle(x, y) {
    this.x = x;
    this.y = y;
}

MathHandle.prototype.add = function () {
    return this.x + this.y;
};

var m = new MathHandle(1, 2);
console.log(m.add())
```

`Class`语法

```javascript
class MathHandle {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    add(){
        return this.x + this.y
    }
}
const m = new MathHandle(1, 2)
console.log(m.add())
```

语法糖

```javascript
typeof MathHandle	// "function"
MathHandle === MathHandle.prototype.constructor	// true
m.__proto__ === MathHandle.prototype	// true

// 这种语法糖形式，看起来和实际原理不一样的东西，我个人不太赞同
// 形式上强行模仿 java C#，却失去了它的本性和个性
```

