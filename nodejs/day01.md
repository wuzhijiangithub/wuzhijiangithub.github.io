## node基础第一天

### 课程介绍
---
#### 自我介绍
* 凃俊雄, 湖北人,30岁,已婚,有个女儿,2岁

#### 课程明细
* 15天课程
    - 前7天->node基础课程
        + ES6:不管全栈开发,ES6必须学好
        + 2天:node环境搭建，基本API理论知识
        + 3天: 黑客新闻网站--> 前端html页面+css+js，以及通过服务器做运算
        + 4天: express框架、mongodb
        + 5天: cookie和session(面试必问)
        + 6天: 我的音乐网站，搭建基本的架构、响应数据，及利用cookie和session技术完成登录和注册
        + 7天: 音乐数据的增删改查、post、get提交数据的细节、同步和异步提交方式
* vue + node项目(后8天)：
    - vue2.0
    - webpack前端构建工具
    - CMS content manager system
        + vue

#### 学习方式
* 如果课程中遇到了不懂的地方。一定要迅速的记录下来，课下问老师。
* 课下要多敲、多敲代码才能加深理解
* 人生困难的事情不仅仅是学习

### ES6
---
* JavaScript语言随着使用的人越来越多，ECMA语法规范：if/else
* 为了让js语言更适应大型应用的开发、旨在消除一些怪异的行为

### 包含内容(strict严格模式)
---
* 使用严格模式的方式：
    - 在全局中或者文件中直接使用
        + `use strict`;
        + 以下的代码就按照严格模式来执行
    - 在函数中开启严格模式
        + `function xx(){ "use strict"; }`
        + 以上函数内的代码就执行严格模式，非该函数内的代码正常模式
* 全局变量显式声明

```javascript
'use strict';

// function aa(){
//     'use strict'
// }
personName = 'jack'; //personName is not defined
console.log(personName);

```
* 禁止使用with语句

```javascript
 'use strict';
    var person = {
        name: 'jack'
    };
    //下面一行报错：Strict mode code may not include a with statement
    with(person) { //针对参数对象做一些操作
        name = 'rose';
    }
    console.log(person);

```
* 禁止this关键字指向全局对象
```javascript

function aaa() {
    return this; //开启严格模式的时候，返回的this是undefined，以前是window
}

aaa();//在ES5中没有开启严格模式返回值是window,而开启以后进制this指向全局对象，所以是undefend
```
* 保留字
    - implements, interface, package, private, protected, public, static, yield

#### LET关键字
* LET是块级作用域,块级就代表着{},如果没有在{}内，就是全局的作用域
* 不存在变量类型提升
    - 不会出现:不管在哪里使用，最终都变成了全局对象
* 注意事项:
    - 1:变量查找机制:和以前一样，就近原则，如果当前作用域{}内没有该变量的声明,就往上级作用域查找
    - 2:每个块内使用的是自己各自的let声明变量
    - 3:不允许同一个作用域下,还同一个名称的声明
* let就是为了解决变量会自动提升成全局变量的一个问题

#### 严格模式和关键字的区别
* 严格模式的开启，影响着代码的限制(我们使用上的不同)
* 关键字对代码的功能的增强(效果上的不同)
* 通常使用ES6，就建议开启严格模式,避免有依赖报错

#### const关键字
* 也是块级作用域
* 注意点:
    - 1：必须一次性完成初始化,声明+赋值
    - 2: 不能够二次赋值：`const p = {}; p='abc';//不能`
        + 可以给对象挂载属性，不会改变对象的指向
            * `const p = {}; p.name= 'abc';//可以`

#### 小总结
* 严格模式
    - 约束以前代码的方式的一些限制
        + 必须显示声明全局变量(先声明后使用，否则报错)
    - 禁止this指向全局对象,如果全局函数中return this;返回的是undefined
    - with在ES5中是根据传入的对象才做相关操作，ES6严格模式下是禁止的
* Let：块级作用域,如果不再{} 下就是全局的变量，在{}下就属于自己块的声明
    - 查找机制: 就近原则,当前块内没有声明就向上级作用域查找
    - 不存在变量类型提升(不会自动提升成全局变量)
    - 使用细节:
    - 同一个块内不允许同名变量的声明
* const
    - 块级作用域，不存在变量类型提升
    - 必须一次性完成初始化，声明+赋值
    - 不允许二次赋值，可以挂载属性

#### 模板字符串(字符串扩展)
* 使用方式:
    - tab键的上方，反引号包括起来`字符串扩展`
* 模板字符串支持换行符的输出
* 可以嵌入对象或者变量`${对象.属性名}`
* 了解:可以支持原生字符串的输出 `String.raw`hello\r\nworld``

#### 扩展ES6函数
* 字符串操作
    - 字符串对象.includes(参数);
        + 判断调用的字符串对象是否包含参数字符串,返回值Boolean
    - 字符串对象.startsWith(参数);
        + 判断调用的字符串对象是否以参数字符串开头,返回bool
    - 字符串对象.endsWith(参数);
        + 判断调用的字符串对象是否以参数字符串结尾,返回bool
    - 字符串对象.repeat(num);//了解
        + 返回调用字符串对象的num次字符串内容
* 数学操作
    - Math.trunc(float); //返回截取掉小数位的整数部分
        + Math.trunc(3.1415926);// 3 
* 数组操作
    - 在数组中查找指定元素
        + 数组对象.find(callback);
        + callback:参数列表: ele元素,index下标,arr原数组
        + 注意:该函数的返回值同过回调函数内部的return来做控制
        + 返回值:返回元素的值，如果没有查找到返回undefined

* 获取数组
    + 获取数组Array.of(3,3,5); //了解就可以，返回一个数组[3,3,5]
    + 通过对象参数获取数组` Array.from({length:3,1:'abc','2':'def'});`
    + length是必须的属性,其他的属性可以是1或者'1' -->

```javascript
    let citys = ['北京', '上海', '广州'];
    //找到上海元素
   let city = citys.find(function(ele, index, arr) {
       console.log('ele', ele);
        return '上海' === ele; //结束遍历并返回元素
    });
      console.log(city);
// 在数组中查找元素的下标
// 返回的是指定元素的下标，如果没有查找到元素返回-1
   let citys = ['北京', '上海', '广州'];
    // //找到上海元素
   let index = citys.findIndex(function(ele, index, arr) {
       console.log('ele', ele);
        return '上海' === ele; //结束遍历并返回元素
    });
      console.log(index);
```

#### 箭头函数
* 让this不再多变
    - 箭头函数本身是没有this的,在声明时箭头函数会根据上层函数的this进行绑定，不再是根据调用时的this去改变了
* 没有参数
    - `()=>1;` //没有参数返回1
* 一个参数
    - `num => num;` //这种情况可以省略参数的括号
* 多个参数
    - `(n1,n2) => n1+n2;` //返回n1+n2
* 多行代码
    - `(n1,n2) => {//code.....} `
* 箭头函数本没有arguments,会根据声明绑定上一次function拿到其中的arguments
* 箭头函数不可以用作构造函数

#### ESpromise
* promise是一个容器,该容器内会执行各个异步的流程，通过异步流程的控制，解决万恶的回调函数的问题。
* promise有三种状态,如果没有调用resolve函数或者没有调用reject函数,状态就是pending
* promise状态不允许回退、暂停
* resolved也叫做fulfilled
* 待发、已解决(已满足)、已拒绝
* `new Promise(callback)`
    - `callback(成功的回调函数,失败的回调函数)`
    - 对应未来获取到这个`对象以后.then(成功,失败)`
* 每一个promise对象的then函数,第二个失败的函数可以省略.
    - 最终统一的通过`catch(function(err){});`函数来处理

* readyState状态
```
readyState  
存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
0: 请求未初始化
1: 服务器连接已建立
2: 请求已接收
3: 请求处理中
4: 请求已完成，且响应已就绪
status  
200: "OK"
404: 未找到页面
```

### 模块化
---
#### commonJs规范
* 后端语言的规范,nodejs执行了commonjs
    - Module、能够操作文件、能够操作底层进程
    - Module中:模块的引入使用require
    - 由此我们常说的require就是commonjs中的代码风格
* ES6 引入不再是require: import 
* 全局变量同名覆盖、命名冲突
* 非常依赖文件的加载顺序

#### browserify
* 安装全局命令行工具browserify `npm install browserify -g`
* 对我们需要操作的文件入口做命令操作，让browserify分析其结构，解析其require
* 最终合并文件,解决浏览器require的问题
* `browserify ./m_index.js -o ./build.js` 
* browserify可以解决浏览器require的问题，并且通过插件实现合并压缩等打包操作、
    - 早期也会配合grunt使用、现在使用比较多的是gulp

#### CommonJS中模块化的体会（总结）
* 文件依赖顺序--> 不需要、将原来依赖关系表明在html中的方式，调整为了将依赖分配到各自的js文件中自行描述依赖
* 同名函数命名冲突 --> 每一个模块(文件中)，可以声明各自的变量，不会提升为全局变量，如果外部需要使用某个变量，通过Module.exports向外部导出

#### Setter 和Getter
* 通过ES5中的
```javascript
Object.defineProperty(对象实例,属性名,{
    set:function(age){
        //由于操作直接操作当前这个属性会触发get和set
        //在此处玩的就是临时的变量
        //假如判断成功
        this._age = age;
    },
    get:function(){
        return this._age;
    }
});
```

### ES6转换
---
#### babel新一代ECMA语法转换器
* babel是一个js的语法转换工具,内部提供了转换es7->es5 es6->es5 vue,react也可以去做最终js代码的转换

#### babel
* babel本身可以安装自己的一个命令行工具 babel-cli,通过命令行来转换ES6代码
* `npm i babel-cli -g`
    - 需要预先设置一下babel,让其知道通过什么来转换到ES5
    - 安装包 `npm i babel-preset-es2015`
    - 单独使用babel命令行工具需要创建一个.babelre文件来完成配置
    - 我们可以通过 `babel ./index.js -f ./build.js`
    - babel默认只转换ES6中的关键字,Promise
        + 使用一个不默认的方式，让babel去转换API
        + 垫片：在有ES6API 的代码最上方加入 require('babel-polyfill');
    - require不能再浏览器运行，所以需要使用browserify来结合babel来使用
        + 由于browserify是需要和babel整合的,babel在6.0之后提供了一个插件babalify
* 1: 安装Browserify
* 2: 安装babel提供的babelify供Browserify使用
* 3: 安装babel预设包解析ES6关键字 babel-preset-es2015
* 4: babel默认不转换API，在代码的第一行引入 require('babel-polyfill');

#### 复习
* 严格模式注意事项`use strict`;
    - 1:在全局中先声明后使用
    - 2:禁止this指向全局对象
    - 3:with(){} 禁止使用
    - 4:保留字不要使用
* let 块级作用域 {}，不会变量类型提升到全局变量
    - 不允许同一个作用域下声明同名变量
* const 块级作用域、不允许二次赋值、可以挂载属性
    - 不允许同一个作用域下声明同名变量、必须一次性完成初始化
* 模板字符串
    - 通过反引号包括，可以识别换行
    - 可以嵌入变量 `${对象名.属性名}`
    - 可以输出原生字符串(了解)
* 箭头函数
    - 箭头函数本没有this、arguments，会根据绑定时向上级function获取相关数据
    - 让this不再是调用时的对象，而是声明时的绑定对象
* promise
    - 三种状态 
        + 待发pending
        + 已解决 resolved或者(fulfilled)
        + 已拒绝 rejected
        + 以上状态的改变取决于函数是否执行到reject或者resolve,没有执行都是pending
    - 状态不可改变和暂停
* 模块化思想
    - 非模块化的问题: 1:同名对象命名冲突/2:文件引入的依赖、3:引入对象不安全(可以修改其隐私属性)
    - commonjs中的模块化来解决上述1/2 ，每一个被require或者说require的文件都是一个模块，内部的属性不被外部都访问，如果需要访问使用`module.exports = xxx;`
    - 外部用`var xxx = require('xxx');` 来获取
* Setter和Getter数据劫持
    - 如果给属性定义了setter或者getter，在给该属性赋值或者获取的时候，都会触发其调用,容易形成死循环
    - 在setter和getter函数中操作的是,this._属性而不是其本身,避免死循环
    - `Object.defineProperty(对象实例,属性名,{里面可以配置get、set属性是一个函数，记得有参数或者return})`
* browserify、babel
    - browserify 是在早期的一个前端代码构建工具、其提供解析require语法或者配合插件完成一个混淆、合并、处理css、各种操作的构建工具，其早于webpack
    - babel 是一个代码解析器、根据需要解析的语法做预设、最终转换成我们需要的ES5代码
    - browserify、babel 都对外提供插件，供其他工具使用
        + `grunt + browserify`
        + `browserify + babelify + babel-polyfill(在文件中)`
* 最后的命令: `browserify ./index.js -o ./build.js -t [babelify --presets [es2015] ]`

#### 参考资料
* ES6参考资料：http://es6.ruanyifeng.com/
* babel参考资料: http://www.ruanyifeng.com/blog/2016/01/babel.html
* node学习 http://cnodejs.org/getstart 《Node.js 包教不包会》

