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

### 三.背景

#### 1.背景颜色

* 设置背景采用background属性
* background属性值
  * 颜色英文名: `eg.white/black`
  * 颜色色号RGB: `eg.#FF0000 -> 等同于 #F00`
  * `hsl(色相,饱和度,亮度)`: eg.`hsl(0, 100%, 50%)`
  * `hsla(色相,饱和度,亮度,透明度)`: eg.`hsla(0, 100%, 50%, .3)`设置为0.3的透明度
  * rgb: eg.`rgb(255, 0, 0)`相当于FF0000
  * rgba: eg.`rgba(255,0,0,.3)` 

#### 2.渐变色背景

* 实例代码

  ```css
  .c {
      background: -webkit-linear-gradient(left, red, green); //线性渐变,从左开始从红到绿
      background: linear-gradient(to right, red, green); //新写法的线性渐变,从左开始从红到绿
      background: linear-gradient(0deg, red, green); //角度的线性渐变,0deg表示从下到上,90deg表示从左往右
      background: linear-gradient(135deg, red 0, green 50%, blue 100%); //多颜色渐变
  }
  ```

#### 3.多背景叠加

* 实例代码

  ```css
  .c {
      background: linear-gradient(135deg, transparent 0, transparent 49.5%, green 49.5% green 50.5%, transparent 50.5%, transparent 100%),
          linear-gradient(45deg, transparent 0, transparent 49.5%, blue 49.5% blue 50.5%, transparent 50.5%, transparent 100%);
      background-size: 30px 30px;
      // 通过设置两个背景叠加实现网格效果，都是在百分比为49.5到50.5期间绘制带颜色线,且通过background-size设置一个背景的区间，如果一行有120px，则会出现4对交叉线
  }
  ```

#### 4.背景图片和属性（雪碧图）

* 实例代码

  ```css
  .c {
      height: 900px;//设置尺寸高度
      background: red url(./test.png);//如果单设这一个属性则当背景图小于900px时会出现多个平铺的背景图占满height
      background-repeat: no-repeat;//设置背景不可平铺,则会只显示一个背景图,其余颜色为红色遮盖
      background-position: center; //设置背景图的位置,可以设置为center/top...或是指定距左距上像素位置
      background-size: 100px 20px;//如果背景图足够大,但不希望显示那么大的背景图时可以通过此属性设置背景图大小
  }
  ```

* **CSS雪碧图**是用来做性能优化的，如我们在一个页面上显示三个图片内容，我们可以将三个图片内容拼接到一个图片中，并在页面中通过背景图片切割的方式设置要显示的部分，这样就是请求一个图片即可完成所有的操作

#### 5.base64进行性能优化

* base64实质是一个文本
* 可以通过将图片变成base64编码来引用，可以通过转码的方式获得对应的图片文本，并将对应的文本填写到background属性中即可显示。如:`background: url(data:image/png;base64,xxxxxxx)`
* 优点: 减少http请求连接数
* 缺点: 会增大图片的体积(增大约1/3)；通过我们会将image文件单存，但如果这样使用会增大css文件体积，故通常我们会用此方式显示图标；增大了解码消耗

#### 6.多分辨率适配

* 在多分辨率适配方面，手机上通常1px会有多个像素点去占用，会使得图片模糊，我们可以通过设置`background-size`属性值缩小背景的大小，这样在手机端就可以显示的更加清楚了

### 四.边框

#### 1.边框的属性

* 线型：直线solid，虚线dashed
* 大小：粗细 m px
* 颜色：色号指定即可

#### 2.边框背景图

* 通过`border-image: url('xxx')`的形式可以设置边框背景

#### 3.边框衔接（三角形）

* **绘制三角形**

  * 如果设置

    ```css
    .c {
        width: 200px;
        height: 40px;
        border-bottom: 20px solid red;
        border-right: 20px solid blue;
    }
    ```

    * 可以看到下方是红色，右下角斜切均分，右侧是蓝色（斜切的分）

  * 如果将右侧设为transparent透明，则可以看到右下角是尖的角

  * 同样如果左侧也设为transparent透明，则左右都是尖角，即等腰梯形

  * width控制包裹的div宽度，如果width设为0px，则会出现三角形

* 绘制扇形

  * 可以通过添加border-radius设置圆角度数，从而实现成为扇形

### 五.滚动

#### 1.滚动行为和滚动条

* 滚动条隐藏：visible（容器如果显示不下内容时，内容会溢出到容器外显示）
* 滚动条隐藏：hidden（容器如果显示不下内容时，溢出内容隐藏）
* 滚动条显示：scroll
* 滚动条自动显示：auto

#### 2.auto和scroll明显区别

* 在Mac系统下无明显区别
* 在Windows系统下如果内容不超过外边框则auto属性不会有滚动条，而scroll属性滚动条会一直存在

### 六.文本折行

#### 1.文字折行

* overflow-wrap(word-wrap)通用换行控制 -> 是否保留单词
  * break-word值表示是否打断单词，如果选择了此属性值则意味着单词会被折行显示，但仍然保持单词的完整性
* work-break针对多字节文字 -> 是否把单词/字母看成一个单位，中文句子也是单词
  * break-all值表示打断所有的单词以适应页面显示
  * keep-all值表示所有单词保证完整，且一个中文句子也会保持完整
* white-space 空白处是否断行
  * no-wrap值表示所有内容都不换行，都一行显示

### 七.装饰性属性

#### 1.装饰性属性

* 字重（粗体）font-weight
* 斜体font-style: itatic
* 下划线text-decoration
* 指针cursor

### 八.CSS Hack

#### 1.什么是CSS Hack

* 在一部分浏览器上生效的CSS写法称为CSS Hack

* Hack即不合法但生效的写法

* **主要用于解决浏览器兼容性问题**

* 缺点：难理解、难维护、易失效

* 替代方案：特性检测

* 替代方案：针对性加class

* 实例代码

  ```css
  body {
      width: 200px;
      width: 180px\9;
  }
  ```

  * 当我们希望在ie下width为180px时可以如上定义，注意统一生效样式写到上面，因为width:200px在ie下同样会生效，下面的180px也会生效，如果反着写最后效果还是200px，即没有替换成功

### 九.CSS面试题

#### 1.CSS样式（选择器）的优先级

* 计算权重确定
* !important
* 内联样式
* 后写的优先级高

#### 2.雪碧图的作用

* 合并图片，减少Http请求数，提高加载性能
* 有一些情况下可以减少图片大小

#### 3.自定义字体的使用场景

* 宣传、品牌、banner等固定文案
* 当字体图标使用

#### 4.base64的使用

* 用于减少Http请求
* 适用于小图片
* base64的体积约为原图的4/3

#### 5.伪类和伪元素的区别

* 伪类表状态
* 伪元素是真的有元素
* 前者单冒号，后者双冒号

#### 6.如何美化checkbox

* 使用label的for属性指向定义的checkbox的id属性值
* 隐藏原生的input
* 样式的写法`:checked + label`通过样式的状态来切换

