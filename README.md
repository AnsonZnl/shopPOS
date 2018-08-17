# shopPOS
这个系统使用的技术栈为：Vue+Webpack+Element+Axios+vueRouter.系统是一个快餐店的POS系统，当然我们不可能实现一个完整POS系统的所有功能-收银模块的制作。
参考地址：http://jspang.com/2017/05/22/vuedemo/

## vue-cli搭建开发环境：
1. 输入vue-cli安装命令：
```
cmpm install vue-cli -g
```
-g 表示全局安装
2. 在命令行中初始化项目，我们采用的是webpack模板，输入初始化命令：
```
vue init webpack AwesomePos
```
就是在你已经提前建立好了文件夹的时候，我们也进入了文件夹，这时候我们可以省略这个文件夹名称:
```
vue init webpack
```
默认在本目录安装
- `? Generate project in current directory? ----Yes`是否在本目录安装----yes
- `? Project name (shopPOS) shop-pos`  项目的名字---shop-pos（这里不支持大写）
- `? Project description A Vue.js project` 描述--- 可不写
- `? Author (zhangningl <zhangningle@chingsoft.com>)`作者---可不写
- `? Install vue-router? Yes`   是否安装vue-router--- yes
- `? Use ESLint to lint your code? (Y/n)` ESlint-规范代码形式 团队开发必备 独立开发--no
- `? Set up unit tests (Y/n)` 测试工具 --- no
- `? Setup e2e tests with Nightwatch? (Y/n)` 模拟测试工具--- no
3. 安装依赖
- `cnpm install`
4. 启动服务器
`npm run dev`

打开： http://localhost:8080/#/
## 图标
**阿里巴巴的矢量图标库：**
1. 进入网站：Iconfont网址：http://www.iconfont.cn
2. 点击网站上方的“官方图标库”，选择自己喜欢的图标。在这里我选择天猫的图标库。
3. 选择好自己喜欢的图标，你可以有两个选择，下载代码 和 添加至项目。
4. 我们这两选择添加至项目，然后新建项目，并输入名称。
5. 项目添加好后，会自动给我们转入到我们项目库中。点击查看在线链接。
6. 生产css引入的代码，生成后就可以在项目首页index.html引入了。(具体以**最新**生成的链接为主)
 ```
 <link rel="stylesheet" href="http://at.alicdn.com/t/font_wyhhdpv5lhvbzkt9.css">
```
7. 添加i标签
```
<i class="icon iconfont icon-gongnengjianyi"></i>//icon-gongnengjianyi复制图标的代码 就可以显示了
```
## Element-UI
1. npm安装
```
cnpm install element-ui --save
```
2. 完整引入项目
在main.js中写入以下内容:
```
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-default/index.css'
import App from './App.vue'

Vue.use(ElementUI)

new Vue({
  el: '#app',
  render: h => h(App)
})
```
3. Element官网
详情用法element官网：http://element-cn.eleme.io/#/zh-CN/component/installation
---
- el-table组件制作选项卡: http://element-cn.eleme.io/#/zh-CN/component/tabs

- el-row快速布局采用24栅格系统: http://element-cn.eleme.io/#/zh-CN/component/layout

- el-table 表格快速插入数据: http://element-cn.eleme.io/#/zh-CN/component/table
---
```
 <el-table-column prop="date" label="日期" align="center" //element ui 表头文本居中的方法
```
