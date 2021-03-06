# 页面重构库

使用方法:

1. 下载node [下载node](http://nodejs.cn/download/)
2. window+r打开命令行，找到本项目根目录
3. 输入 npm install （如果下载太慢可以选择[淘宝镜像](https://segmentfault.com/n/1330000009480793)）
4. 输入gulp执行自动化任务。 

## 项目介绍

本项目目标是为方便所有页面重构工作者进行页面重构。技术栈node+gulp（自动化构建工具）+jade（预编译html）+sass（预编译css）。

## 规范

### 页面结构规范（jade）

在jade中把文件分为页面和组件两部分：

#### 组件

* header（页头）
* nav（导航）
* banner（横幅）
* button（按钮）
* input（表单输入）
* paging（分页）
* pop（弹窗）
* tab（标签页）
* sidebar（侧边栏）
* widget（窗口控件）

其中编写项目中公用的组件结构以便复用。

#### 页面

* page.base（页面通用模板）
* index（首页）
* xxx（项目用页面）


> 在gulp中，为了区分需要编译和不需要编译的文件，本项目中将不需要编译为html的jade文件以"_"开头命名（如页头为"_header.jade"，页面模板为"_page.base.jade"），页面jade则不以"_"开头命名（如首页为"index.jade"）

### 页面样式规范（scss）

在scss中分为组件样式、通用样式、页面独立样式三部分：

#### 组件样式

目前抽离出来的组件样式为：

* banner（横幅样式）
* button（按钮样式）
* footer（页脚样式）
* nav（导航样式）
* paging（分页样式）
* pop（弹窗样式）
* sidebar（侧边栏）
* widget（窗口样式）

其中编写项目中可能重用的组件样式。

#### 通用样式

目前整理的通用样式为：

* animate（动画样式-以类名方式进行引用）
* edge（边距样式-以类名方式进行引用）
* grid（栅格样式-以类名方式进行引用）
* mixins（常用样式简写-以mixin方式进行引用）
* normal（css reset样式-以类名方式进行引用）
* utils（功能样式-以类名方式进行引用）
* variables（变量样式-以sass变量方式进行引用）
* my-css-common（开发者自定义的通用样式-以类名方式进行引用）

#### 页面样式

页面样式以页面类型命名：

* index（首页样式）


在gulp中，为了区分需要编译和不需要编译的文件，本项目中将按照需求编译scss文件，规则如下:

不合并页面样式：

* base（组件样式+通用样式+开发者自定义通用样式，所有页面都需要引用）
* index（页面独立样式，在需要的页面中单独引用）

合并页面样式：

自己新建一个scss文件（一般以项目名称命名如taobao.scss），其中引用：

1. 所有的页面样式
2. base.scss

然后在gulpfile中将style任务的文件筛选为taobao.scss，引用合并任务（如需要可重命名添加.min后缀）。

### jade注意事项

1. jade对于缩进要求极其严格，如空格形式的缩进与tab形式的缩进不能共存于一个文件中，否则编译会失效；
2. jade在定义多行变量时，需要这样定义：

    ```javascript
    //注意"-"后面不能有空格！
	-
		var obj = {
			name:"Rufer",
			sex:"male",
			age:22
		};
    ```

3. jade文件中不能有多余的tab缩进，否则会编译失败。

