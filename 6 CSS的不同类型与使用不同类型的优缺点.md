CSS的不同类型与使用不同类型的优缺点
============================
## css的不同类型
根据css代码在文件中的位置，可以将css代码分为三种类型：内联样式、内部样式、外部样式。
## 内联样式、内部样式、外部样式
### 内联样式
使用style关键字将css代码嵌入到html代码中，与html代码混写。具体如下：
```html
<p style="color:red; text-align:center">内容</p>
```
### 内部样式
在html文件中head中使用一对标签style,将css代码声明其中。
```html
<p>内容</p>
```
```css
<head>
<style>
    p {
      color:red;
      text-align:center
    }
</style>
</head>
```
### 外部样式
将css样式单独写成一个文件，在html文件中通过link引入。

举例css文件名: `example.css`

```html
<head>
<link href="example.css" rel="stylesheet">
</head>
```
## 使用不同类型css的优缺点
### 内联样式
#### 优点
1. 方便，快捷
2. 与某个元素的有关样式一目了然
3. 加载和渲染html时同时加载和渲染css文件，减少http请求，减少文件下载数量
#### 缺点
1. 优先级最高，容易造成混乱，不利于后期维护
2. html与css混合写，代码显得冗余、复杂。不符合html与css分离的要求。
3. 代码可复用性查
### 内部样式
#### 优点
1. 减少页面请求
2. 实现基本的html与css分离
3. 加载和渲染html时同时加载和渲染css文件，减少http请求，减少文件下载数量
#### 缺点
1. 不能跨html文件进行代码复用

### 外部样式
#### 优点
1. css单独写成一个文件，便于管理css代码
2. 复用代码方便，可以跨多个html文件管理css代码
#### 缺点
1. 需要单独加载文件，增加HTTP请求数，占用资源，延缓了网页加载速度

2019/1/15 23:32:16 
