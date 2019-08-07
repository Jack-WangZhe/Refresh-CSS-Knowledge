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