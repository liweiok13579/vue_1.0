vue:
	读音:	v-u-e
	view

	vue到底是什么?
		一个mvvm框架(库)、和angular类似
		比较容易上手、小巧
	mvc:
		mvp
		mvvm
		mv*
		mvx
	官网:http://cn.vuejs.org/	
	手册： http://cn.vuejs.org/api/

vue和angular区别?
	vue——简单、易学
		指令以 v-xxx
		一片html代码配合上json，在new出来vue实例
		个人维护项目

		适合: 移动端项目,小巧

		vue的发展势头很猛，github上start数量已经超越angular
	angular——上手难
		指令以 ng-xxx
		所有属性和方法都挂到$scope身上
		angular由google维护
		
		合适: pc端项目

	共同点: 不兼容低版本IE
-------------------------------------------
vue基本雏形:
	angular展示一条基本数据:
		var app=angular.module('app',[]);

		app.controller('xxx',function($scope){	//C
			$scope.msg='welcome'
		})

		html:
		div ng-controller="xxx"
			{{msg}}
	vue:
		html:
			<div id="box">
				{{msg}}
			</div>

			var c=new Vue({
				el:'#box',	//选择器  class tagName
				data:{
				    msg:'welcome vue'
				}
			});
常用指令:
	angular: 
		 ng-model   ng-controller
		 ng-repeat
		 ng-click
		 ng-show  

		$scope.show=function(){}
	指令: 扩展html标签功能,属性

	v-model	一般表单元素(input)	双向数据绑定

	循环:
		v-for="name in arr"
			{{$index}}

		v-for="name in json"
			{{$index}}	{{$key}}
	
		v-for="(k,v) in json"
	事件:
		v-on:click="函数"

		v-on:click/mouseout/mouseover/dblclick/mousedown.....

		new Vue({
			el:'#box',
			data:{ //数据
			    arr:['apple','banana','orange','pear'],
			    json:{a:'apple',b:'banana',c:'orange'}
			},
			methods:{
			    show:function(){	//方法
			        alert(1);
			    }
			}
		});
	显示隐藏:
		v-show=“true/false”
bootstrap+vue简易留言板(todolist):
	
	bootstrap: css框架	跟jqueryMobile一样
		只需要给标签 赋予class，角色
		依赖jquery

	确认删除？和确认删除全部么?
-----------------------------------------
事件:
	v-on:click/mouseover......
	
	简写的:
	@click=""		推荐

	事件对象:
		@click="show($event)"
	事件冒泡:
		阻止冒泡:  
			a). ev.cancelBubble=true;
			b). @click.stop	推荐
	默认行为(默认事件):
		阻止默认行为:
			a). ev.preventDefault();
			b). @contextmenu.prevent	推荐
	键盘:
		@keydown	$event	ev.keyCode
		@keyup

		常用键:
			回车
				a). @keyup.13
				b). @keyup.enter
			上、下、左、右
				@keyup/keydown.left
				@keyup/keydown.right
				@keyup/keydown.up
				@keyup/keydown.down
			.....
-----------------------------------------
属性:
	v-bind:src=""
		width/height/title....
	
	简写:
	:src=""	推荐

	<img src="{{url}}" alt="">	效果能出来，但是会报一个404错误
	<img v-bind:src="url" alt="">	效果可以出来，不会发404请求
-----------------------------------------
class和style:
	:class=""	v-bind:class=""
	:style=""	v-bind:style=""

	:class="[red]"	red是数据
	:class="[red,b,c,d]"
	
	:class="{red:a, blue:false}"

	:class="json"
		
		data:{
			json:{red:a, blue:false}
		}
	--------------------------
	style:
	:style="[c]"
	:style="[c,d]"
		注意:  复合样式，采用驼峰命名法
	:style="json"
-----------------------------------------
模板:
	{{msg}}		数据更新模板变化
	{{*msg}}	数据只绑定一次
	
	{{{msg}}}	HTML转意输出
-----------------------------------------
过滤器:-> 过滤模板数据
	系统提供一些过滤器:
	
	{{msg| filterA}}
	{{msg| filterA | filterB}}

	uppercase	eg:	{{'welcome'| uppercase}}
	lowercase
	capitalize

	currency	钱

	{{msg| filterA 参数}}

	....
-----------------------------------------
交互:
	$http	（ajax）

	如果vue想做交互

	引入: vue-resouce

	get:
		获取一个普通文本数据:
		this.$http.get('aa.txt').then(function(res){
		    alert(res.data);
		},function(res){
		    alert(res.status);
		});
		给服务发送数据:√
		this.$http.get('get.php',{
		    a:1,
		    b:2
		}).then(function(res){
		    alert(res.data);
		},function(res){
		    alert(res.status);
		});
	post:
		this.$http.post('post.php',{
		    a:1,
		    b:20
		},{
		    emulateJSON:true
		}).then(function(res){
		    alert(res.data);
		},function(res){
		    alert(res.status);
		});
	jsonp:
		https://sug.so.360.cn/suggest?callback=suggest_so&word=a

		https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=a&cb=jshow

		this.$http.jsonp('https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',{
		    wd:'a'
		},{
		    jsonp:'cb'	//callback名字，默认名字就是"callback"
		}).then(function(res){
		    alert(res.data.s);
		},function(res){
		    alert(res.status);
		});
		
https://www.baidu.com/s?wd=s
----------------------------------------- 2
vue制作weibo
	交互

vue->  1.0
	vue-resource	ajax	php
	服务器环境(node)

	this.$http.get()/post()/jsonp()

	this.$http({
		url:地址
		data:给后台提交数据,
		method:'get'/post/jsonp
		jsonp:'cb' //cbName
	});
----------------------------------
vue事件:
	@click=""
数据:


添加一条留言：

获取某一页数据:
	getPageData(1);
	123
----------------------------------
vue生命周期:
	钩子函数:

	created	->   实例已经创建	√
	beforeCompile	->   编译之前
	compiled	->   编译之后
	ready		->   插入到文档中	√

	beforeDestroy	->   销毁之前
	destroyed	->   销毁之后
----------------------------------
用户会看到花括号标记:
	
	v-cloak		防止闪烁, 比较大段落
----------------------------------
<span>{{msg}}</span>		->   v-text
{{{msg}}}			->   v-html
123
----------------------------------
ng:  $scope.$watch

计算属性的使用:
	computed:{
		b:function(){	//默认调用get
			return 值
		}
	}
	--------------------------
	computed:{
		b:{
			get:
			set:
		}
	}

	* computed里面可以放置一些业务逻辑代码，一定记得return
---------------------------------
vue实例简单方法:
	vm.$el	->  就是元素
	vm.$data  ->  就是data
	vm.$mount ->  手动挂在vue程序
	
	vm.$options	->   获取自定义属性
	vm.$destroy	->   销毁对象

	vm.$log();	->  查看现在数据的状态
---------------------------------
循环：
	v-for="value in data"

	会有重复数据？
	track-by='索引'	提高循环性能

	track-by='$index/uid'
---------------------------------
过滤器:
	vue提供过滤器:
		capitalize	uppercase	currency....

		debounce	配合事件，延迟执行
	数据配合使用过滤器:
		limitBy	限制几个
		limitBy 参数(取几个)
		limitBy 取几个  从哪开始

		filterBy	过滤数据
		filterBy ‘谁’

		orderBy	排序
		orderBy 谁 1/-1
			1  -> 正序
			2  -> 倒序

	自定义过滤器:  model ->过滤 -> view
		Vue.filter(name,function(input){
			
		});

	时间转化器
	过滤html标记

	双向过滤器:*
	Vue.filter('filterHtml',{
	            read:function(input){ //model-view
	                return input.replace(/<[^<+]>/g,'');
	            },
	            write:function(val){ //view -> model
	                return val;
	            }
	});

	数据 -> 视图
	model -> view

	view -> model
---------------------------------
v-text
v-for
v-html
	指令: 扩展html语法

自定义指令:
	属性:

	Vue.directive(指令名称,function(参数){
		this.el	-> 原生DOM元素
	});

	<div v-red="参数"></div>

	指令名称: 	v-red  ->  red

	* 注意: 必须以 v-开头

	拖拽:
	-------------------------------
自定义元素指令:（用处不大）
	Vue.elementDirective('zns-red',{
	    bind:function(){
	        this.el.style.background='red';
	    })
	    
------------------------------------------------
@keydown.up
@keydown.enter

@keydown.a/b/c....

自定义键盘信息:
	Vue.directive('on').keyCodes.ctrl=17;
	Vue.directive('on').keyCodes.myenter=13;
	
------------------------------------------------
监听数据变化:
	vm.$el/$mount/$options/....

	vm.$watch(name,fnCb);  //浅度
	vm.$watch(name,fnCb,{deep:true});  //深度监视 
	
------------------------------------------------
vue组件:
组件间各种通信
slot
vue-loader	webpack   .vue
vue-router

------------------------------------------------3
git page：
	任何仓库 master分支，都可以发布(git page)
	
-------------------------------------
双向过滤器:
	Vue.filter(name,{
		read:
		write:
	});
	
-------------------------------------
1.0
2.0

-------------------------------------
引入 vue.js

-------------------------------------
bower-> （前端）包管理器
	npm install bower -g
		验证: bower --version

bower install <包名>
bower uninstall <包名>
bower info <包名>	查看包版本信息

<script src="bower_components/vue/dist/vue.js"></script>

-------------------------------------
vue-> 过渡(动画)
	本质走的css3: transtion ,animation

	<div id="div1" v-show="bSign" transition="fade"></div>

	动画:
		.fade-transition{
			
		}
		进入：
		.fade-enter{
			opacity: 0;
		}
		离开：
		.fade-leave{
			opacity: 0;
			transform: translateX(200px);
		}
	----------------------------------------
vue组件:
	组件: 一个大对象
定义一个组件:
1. 全局组件
var Aaa=Vue.extend({
	template:'<h3>132465</h3>'
});

Vue.component('aaa',Aaa);

	*组件里面放数据:
		data必须是函数的形式，函数必须返回一个对象(json)
2. 局部组件
	放到某个组件内部
var vm=new Vue({
	el:'#box',
	data:{
		bSign:true
	},
	components:{ //局部组件
		aaa:Aaa
	}
});
123
--------------------------------------
另一种编写方式:
	Vue.component('my-aaa',{
		template:'<strong>好</strong>'
	});

	var vm=new Vue({
		el:'#box',
		components:{
			'my-aaa':{
				template:'<h2>标题2</h2>'
			}
		}
	});
	123
-----------------------------------
配合模板:
	1. template:'<h2 @click="change">{{msg}}</h2>'

	2. 单独放到某个地方
		a). <script type="x-template" id="aaa">
			<h2 @click="change">{{msg}}</h2>
		</script>
		b). <template id="aaa">
			<h1></h1>
			<ul>
				<li v-for="val in arr">
					{{val}}
				</li>
			</ul>
		</template>
		123
-----------------------------------
动态组件:
	<component :is="组件名称"></component>
	123
--------------------------------------------
vue-devtools	->  调试工具
	https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd
	123
--------------------------------------------
vue默认情况下，子组件也没法访问父组件数据
123
--------------------------------------------
组件数据传递:	√
1. 子组件就想获取父组件data
	在调用子组件：
		<bbb :m="数据"></bbb>

	子组件之内:
		props:['m','myMsg']

		props:{
			'm':String,
			'myMsg':Number
		}
2. 父级获取子级数据
	*子组件把自己的数据，发送到父级

	vm.$emit(事件名,数据);

	v-on:	@
	123
--------------------------------------------
vm.$dispatch(事件名,数据)	子级向父级发送数据
vm.$broadcast(事件名,数据)	父级向子级广播数据
	配合: event:{}

	在vue2.0里面已经，报废了
	123
--------------------------------------------
slot:
	位置、槽口
	作用: 占个位置

	类似ng里面 transclude  （指令）
	123
--------------------------------------------
vue-> SPA应用，单页面应用
	vue-resouce	交互
	vue-router	路由

	根据不同url地址，出现不同效果

	咱上课: 0.7.13

主页	home
新闻页	news


html:
	<a v-link="{path:'/home'}">主页</a>	跳转链接
	
	展示内容:
	<router-view></router-view>
js:
	//1. 准备一个根组件
	var App=Vue.extend();

	//2. Home News组件都准备
	var Home=Vue.extend({
		template:'<h3>我是主页</h3>'
	});

	var News=Vue.extend({
		template:'<h3>我是新闻</h3>'
	});

	//3. 准备路由
	var router=new VueRouter();

	//4. 关联
	router.map({
		'home':{
			component:Home
		},
		'news':{
			component:News
		}
	});

	//5. 启动路由
	router.start(App,'#box');

跳转:
	router.redirect({
		‘/’:'/home'
	});
	123
--------------------------------------
路由嵌套(多层路由):
	
	主页	home
		登录	home/login
		注册	home/reg
	新闻页	news

	subRoutes:{
		'login':{
			component:{
				template:'<strong>我是登录信息</strong>'
			}
		},
		'reg':{
			component:{
				template:'<strong>我是注册信息</strong>'
			}
		}
	}
路由其他信息:
	/detail/:id/age/:age

	{{$route.params | json}}	->  当前参数

	{{$route.path}}	->  当前路径
	
	{{$route.query | json}}	->  数据
	123
--------------------------------------------
vue-loader:
	其他loader ->  css-loader、url-loader、html-loader.....

	后台: nodeJs	->  require  exports
	broserify  模块加载，只能加载js
	webpack   模块加载器， 一切东西都是模块, 最后打包到一块了

	require('style.css');	->   css-loader、style-loader

	
	vue-loader基于webpack

.css
.js
.html
.php
.....


a.vue
b.vue

	.vue文件:
		放置的是vue组件代码

		<template>
			html
		</template>
	
		<style>
			css
		</style>
	
		<script>
			js	（平时代码、ES6）	babel-loader
		</script>
		123
-------------------------------------
简单的目录结构:
	|-index.html
	|-main.js	入口文件
	|-App.vue	vue文件，官方推荐命名法
	|-package.json	工程文件(项目依赖、名称、配置)
		npm init --yes 生成
	|-webpack.config.js	webpack配置文件

ES6: 模块化开发
	导出模块：
		export default {}
	引入模块:
		import 模块名 from 地址
		123
--------------------------------------------
webpak准备工作:
	cnpm install webpack --save-dev
	cnpm install webpack-dev-server --save-dev

	App.vue	-> 变成正常代码		vue-loader@8.5.4
	cnpm install vue-loader@8.5.4 --save-dev

	cnpm install vue-html-loader --save-dev
	
	vue-html-loader、css-loader、vue-style-loader、
	vue-hot-reload-api@1.3.2

	babel-loader
	babel-core
	babel-plugin-transform-runtime
	babel-preset-es2015
	babel-runtime

最最核心：
123
--------------------------------------------4
手动配置自己:
	webpack+vue-loader

	webpack加载模块
	123
-------------------------------------
如何运行此项目？
	1. npm install	或者    cnpm install
	2. npm run dev
		->  package.json
			"scripts":{
				"dev":"webpack-dev-server --inline --hot --port 8082"
			}

以后下载模块：
	npm install <package-name>  --save-dev

EADDRINUSE	端口被占用

少了:
	webpack-dev-server
	webpack
	123
----------------------------------------
.vue 结尾，之后称呼组件
123
----------------------------------------
路由:
	vue-router

		->  如何查看版本:
			bower info vue-router

	路由使用版本: 0.7.13
配合vue-loader使用:
1. 下载vue-router模块
	cnpm install vue-router@0.7.13
2. import VueRouter from 'vue-router'

3. Vue.use(VueRouter);

4. 配置路由
	var router=new VueRouter();
	router.map({
		路由规则
	})
5. 开启
	router.start(App,'#app');

注意:
	之前: index.html	->   <app></app>
	现在: index.html	->   <div id="app"></div>

	App.vue	->   需要一个 <div id="app"></div>  根元素

home	news
123
---------------------------------------------
路由嵌套:
	和之前一模一样
	123
--------------------------------------------
上线:
	npm run build
		->	webpack -p
		132
--------------------------------------------
脚手架:
	vue-cli——vue脚手架
		帮你提供好基本项目结构

本身集成很多项目模板:
	simple		个人觉得一点用都没有
	webpack	可以使用(大型项目)
			Eslint 检查代码规范，
			单元测试
	webpack-simple	个人推荐使用, 没有代码检查	√

	browserify	->  自己看
	browserify-simple
	123
--------------------------------------------
基本使用流程:
1. npm install vue-cli -g	安装 vue命令环境
	验证安装ok?
		vue --version
2. 生成项目模板
	vue init <模板名> 本地文件夹名称
3. 进入到生成目录里面
	cd xxx
	npm install
4. npm run dev
--------------------------------------------	
一版本已经结束，二版本又大换血了，不过还是有迹可循的。待2看完了在整理一下上传上来（123为换位符）
