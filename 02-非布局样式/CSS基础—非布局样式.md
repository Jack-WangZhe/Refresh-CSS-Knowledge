## CSS基础—非布局样式

### 一.字体

#### 1.字体族

* 衬线字体[字体周围有装饰内容]：`serif`
* 非衬线字体[起笔落笔都规矩]:`sans-serif`
* 等宽字体[每一个字母占的空间相等]:`monospace`
* 手写体:`cursive`
* 花体[华丽歪歪拐拐的字体]:`fantasy`

#### 2.多字体fallback

* 当一个字体指定之后，但又找不到，即往后找【定义多个字体如：微软雅黑，宋体，楷体，当找不到微软雅黑时即会使用宋体，以此类推】

#### 3.网络字体、自定义字体

* 当希望显示自定义字体的内容

#### 4.iconfont

#### 5.实例演示

* Fallback Demo

  ```html
  <style>
      .test {
          // 使用font-family定义字体
          font-family: "monaco";
      }
  </style>
  <html>
      <p class="test">
          Hello Jack 你好，杰克
      </p>
  </html>
  ```

  * 在页面显示时，我们可以查看**控制台中Computed -> Rendered Fonts**会显示用什么字体真正渲染的页面，可以看到有Monaco和PingFang，因为Monaco只定义了英文字体，当给“你好，杰克”设置样式时，默认使用PingFang字体进行渲染

* 字体族使用 Demo

  ```html
  <style>
      .test {
          // 使用font-family定义字体
          font-family: "Microsoft Yahei", serif;
      }
  </style>
  <html>
      <p class="test">
          Hello Jack 你好，杰克
      </p>
  </html>
  ```

  * 注意**当使用字体时需要使用引号包裹，当使用字体族时不要加引号包裹，渲染时会自动给定字体族内的字体进行渲染**
  * 还需要注意当定义字体时需要将针对性强的放到前面，普遍都有的字体放到后面，即`font-family: "PingFang SC", "Microsoft Yahei", monospace`，其中Microsoft Yahei字体在大部分电脑上都会安装，如果定义到PingFang SC前则可能PingFang SC字体永远不会适用

* 自定义字体 Demo

  ```html
  <style>
      // 定义font-family自定义类型
      @font-face {
          font-family: "Jack-font";//自定义字体名
          src: url("./IndieFlower.ttf");//定义字体源,可以使本地的ttf也可以远程的ttf
          // 如果使用的是远程的ttf还需要考虑到跨域的问题
      }
      .custom-font {
          font-family: Jack-font;
      }
  </style>
  <html>
      <p class="custom-font">
          Hello Jack 你好，杰克
      </p>
  </html>
  ```

* 使用iconfont

  * 登录阿里巴巴矢量图选择需要的字体并添加到项目中
  * 统一将需要的所有icon字体全部导出
  * 导出的内容会包括html的demo文件，可以查看具体的使用方式，如`<i class="会在demo文件中给出"></i>`，其中需要先引入导出的css文件，由于在i后添加了`::before`，会在添加的css中进行处理进而显示对应的iconfont图标内容

### 二.行高

#### 1.行高的构成

* 行高设置的元素`line-height`

* 实例代码

  ```html
  <span style="line-height:20px">inline box 01</span>
  <span style="line-height:20px">inline box 02</span>
  <span style="line-height:20px">inline box 03</span>
  <span style="line-height:30px">inline box 04</span>
  ```

  * 页面显示代码可以看到四个inline box元素显示在同一行，渲染高度一样
  * 原因：line-height只会撑开当前inline元素的整体行高，即实际当前此行的行高为30px

* 整个inline-box的底部是bottom底线，字母的最下部分是基线，inline-box的顶部是top顶线

#### 2.行高相关的现象和处理方案

* 实例代码01

  ```html
  <div style="border:solid 1px red;">
      <span style="background: blue; color: #fff; font-size: 20px; line-height: 60px">元素内容</span>
  </div>
  ```

  * span的背景区域是根据字体大小(底线与顶线)决定的
  * 上述代码可以看到div的高度是60px，span的高度是20px(因为是由字体的顶线与底线决定的)，超出的40px将分布到span上下两侧

* 实例代码02

  ```html
  <div>
      <span style="font-size:10px;">第一段</span>
      <span style="font-size:20px;">第二段</span>
      <span style="font-size:30px;">第三段</span>
  </div>
  ```

  * 上述代码可以看到一行中的三段文字是基于基线对齐的
  * 如果想基于底线对齐则:`vertical-align:bottom;`，基于顶线对齐:`vertical-align: top`，居中对齐:`vertical-align:middle`
  * vertical-align默认是base-line像素，如果想上移指定像素则直接赋值像素值即可

* 实例代码03**【图片3px缝隙问题—面试题】**

  ```html
  <div>
      <span>文本</span>
      <img src="test.jpg"/>
  </div>
  ```

  * 上述代码在页面中显示时会发现图片下有一行空白缝隙
  * 原因：img是inline元素，遵守行高构成，默认基于基线对齐(base-line)，基线对齐即元素下方还会与容器有一部分空隙的
  * 可以通过设置img的style样式`vertical-align: bottom`基于底线对齐，则会实现消除缝隙

### 二.背景

> 未完待续...

### 三.边框

> 未完待续...

### 四.滚动

> 未完待续...

### 五.文本折行

> 未完待续...

### 六.装饰性属性

> 未完待续...