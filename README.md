## spring-boot-vue-blog
a blog based on spring boot and vue 
[TOC]
## reference 
- [spring-boot](https://spring.io/projects/spring-boot)
- [vue](https://cn.vuejs.org/index.html)
- [BootstrapVue](https://bootstrap-vue.js.org/docs/)
- [vue cli ](https://cli.vuejs.org/)
- [core-ui](https://github.com/coreui/coreui-vue)
## Project Init
project init ,include vue and spring-boot
###  Vue Init 
1. create a vue project 
use vue cli3 create a vue project 
```
vue create blog
```
2. install 
```
npm install
```

3. Compiles and hot-reloads for development
```
npm run serve
```
project preview 
![hello vue](https://raw.githubusercontent.com/erzhiqianyi/spring-boot-vue-blog/master/image/hello.PNG)

4. Compiles and minifies for production
```
npm run build
```

5. Run  tests
```
npm run test
```

5. Lints and fixes files
```
npm run lint
```

7. Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

8.  defult project structure
```
blog
├─ node_modules 安装的依赖包
├─ public 存放静态资源，该目录下的静态资源会被复制到输出目录中（默认输出目录为dist）,不经过 webpack。需要通过绝对路径来引用它们。
│  ├─ favicon.ico 浏览器首段图标 
│  └─ index.html index 文件
├─ src 代码
│  ├─ assets 静态资源，如图片、图标、字体等
│       └─ logo.png
│  ├─ components  公共组件
│       └─ HelloWorld.vue
│  ├─ App.vue 路由组件的顶层路由
│  ├─ main.js vue入口文件
├─ babel.config.js  babel配置
├─ package-lock.json 锁定安装时的包的版本号,保证依赖一致
├─ package.json 定义项目所需要的各种模块，以及项目的配置信息，npm install下载所需的模块
```
9. 引入bootstrap vue 
```
vue add bootstrap-vue
```
会新建一个pugins目录
```
blog
├─ plugins
│       └─ bootstrap-vue.js
```

bootstrap-vue.js
```js
import Vue from 'vue'

import BootstrapVue from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue)

```

main.js中自动引入插件
```js
import './plugins/bootstrap-vue'
```
### Spring-boot  Init
在[https://start.spring.io/](https://start.spring.io/)新建一个spring boot项目，使用maven管理项目。添加lombok和Spring Reatvice Web依赖，其他依赖用到再添加。

pom 文件如下
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.6.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.erzhiqianyi</groupId>
	<artifactId>spring-boot-blog</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>sprint boot blog</name>
	<description>a blog based on spring boot  </description>

	<properties>
		<java.version>10</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-webflux</artifactId>
		</dependency>

		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>io.projectreactor</groupId>
			<artifactId>reactor-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```
项目结构如下
```
spring-boot-blog
├─ src 源代码目录
│  ├─ main 
│       ├─ java java代码目录
│       ├─ resources 资源文件
│           ├─  application.properties默认配置文件
│  ├─ test  测试目录
│       ├─ java 测试java代码目录
├─ pom.xml project object model，项目对象模型

```
在idea中打开项目，运行BlogApplication的main函数，执行该方法，即可运行项目。

## Login 
login page and interface
### login page 
在src目录下新建一个目录"views"，用来存放所有的路由组件,再新建一个pages来存放单独（没有其他页面结构）的路由组件，
```
blog
├─ src 代码
│  ├─ views 所有路由组件
│       └─ pages
│            └─ login
│                 └─ index.vue 登录路由

```
#### a vue page structure 
```js
<template>
//组件 一个tempalte只能有一个根div组件
</template>

<script>
//脚本
</script>

<style scoped>
//样式
</style>
```
#### used components
##### [simple-line-icons](https://www.npmjs.com/package/simple-line-icons)
Simple line icons with CSS, SAAS, LESS & Web-fonts files. 

把依赖加到package.json的dependencies中，depencies为生产环境需要的依赖，devDependencies为开发环境需要的依赖，开发环境需要构建工具，生产环境不需要。

这个依赖主要是一些icon,指定元素class即可使用相应的icon。
如
```html
<i class="icon-user"></i>
```
元素效果如下
![hello vue](https://github.com/erzhiqianyi/spring-boot-vue-blog/blob/master/image/simple-line-pre.PNG?raw=true)

在App.vue的style标签中引入```simple-line-icons```
```js
<style  lang="scss">
$simple-line-font-path: '~simple-line-icons/fonts/';
@import '~simple-line-icons/scss/simple-line-icons.scss';
</style>
```
##### [BootstrapVue](https://bootstrap-vue.js.org/docs)
- [Layout and grid system](https://bootstrap-vue.js.org/docs/components/layout/#rows-b-row-and-b-form-row)
	- b-container
	- b-row
	- b-form-row
	- b-col
- [Cards](https://bootstrap-vue.js.org/docs/components/card/#comp-ref-b-card)
	- b-card
	- b-bard-body
#### il18n

#### use Login.vue
在App.vue中引入Login.vue ,并注册,把Login.vue当作组件使用。
App.vue代码
```js
<template>
  <div id="app">
    <Login/>
  </div>
</template>

<script>
import Login from './views/pages/login'

export default {
  name: 'app',
  components: {
    Login
  }
}
</script>

<style  lang="scss">
$simple-line-font-path: '~simple-line-icons/fonts/';
@import '~simple-line-icons/scss/simple-line-icons.scss';

@import 'assets/scss/style';
</style>
```
main.js 代码
```js
import '@babel/polyfill'
import 'mutationobserver-shim'
import Vue from 'vue'
import './plugins/bootstrap-vue'
import App from './App.vue'

new Vue({
  render: h => h(App),
}).$mount('#app')
```
运行项目
![Login page ](https://github.com/erzhiqianyi/spring-boot-vue-blog/blob/master/image/login_pre.png?raw=true)
#### login page detail
### spring boot login interface