# 前期准备
* 确认node npm 使用的最新稳定版本，本机环境Vue Cli(version:4.5.13),Node(version:12.18.3),NPM(version:6.14.6)
* 配置国内镜像 'npm config set registry https://registry.npm.taobao.org'
* 配置VS Code(Plugin: ESLint、Vetur、TODO Highlight、prettier)
* 使用自定义的编辑器VSCode来编写'git conmmit'日志 'git config --global core.editor "code --wait"'
* 'npm config set sass_binary_site https//npm.taobao.org/mirrors/node-sass'

# 使用脚手架工具搭建项目框架
* git init或者clone一个空项目
* vue create搭建项目基础框架（在进行preset选择时将vue router、Vuex、Sass with node-sass选中，ESLint + Standard config或者也可以ESLint + Prettier,Lint and fix on commit）
* 使用'vue add element-ui'添加Element UI,考虑到后期有可能需要修改element的默认样式，所以再添加element的时候需要选择使用scss theme（安装过程会提示）

# 完善项目目录结构
使用vue-cli工具搭建完项目基础框架后，根据项目的具体情况对目录结构进行进一步的调整
* 根据模块建立视图文件夹，所有视图根据模块来保存在对应的文件夹内
* 在views下简历layout目录，用于保存页面的整体布局
* 创建utils文件夹，用于保存存放功能文件
* 创建services(api)文件夹，用于保存服务（接口）调用文件
* 创建assets文件夹，防止所有的公共静态资源（图片、图标，样式）
* components下创建gloabl文件夹，放置全局公共组件
···
    build
    public
    src
        lang
        assets
            images
            icons
            styles
        components(全剧组件)
            global
        views
            layout
            user
            news
        utils
            request.js
        services(api)
            user
            news
            index.js
        router
            user
            news
            index.js
        store
            user
            news
            index.js
        App.vue
        main.js
    .env
    .env.development
    .env.production
    vue.config.js
        
···

# 第三方通用工具包安装

## normalize.css
使用normolize.css能够让我们在各个浏览器得到一样的渲染样式效果，因为各个浏览器的默认样式是存在细微出入的，使用normolize.css能够解决这个问题

## axios
使用axios来实现ajax的请求，并通过配置拦截器来实现通用配置的添加
* 从环境变量获取接口请求的地址，根据环境的不同可以将地址配置在不同的文件中'.env.development'和'.env.production'
* 在util文件夹下新建文件request.js,实现axios的实例化和拦截器方法，并导出实例
* 请求拦截器，对用户的授权token进行统一添加
* 响应拦截器，对响应的信息进行统一前置处理，使用element-ui的'Message'组件实现提示功能

## MProgress
NProgress能够为我们在路由跳转，ajax请求加载过程中提供友好的进度条效果，谷歌，Youtube,Media都有类似的效果，使用这种方式对操作用户非常友好，通用使用场景有两个地方：
* 路由切换的时候，在全局路由导航守卫添加该方法
* ajax请求过程中，在请求拦截器和相应拦截器实现该方法

## 强制代码规范检查
* husky和list-staged（使用vue cli已经有集成了，可以直接使用https://cli.vuejs.org/guide/cli-service.html#git-hooks），实现代码规范性检查

