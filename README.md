# CSS Secrets

Better Solutions to Everyday Web Design Problems

---
#老生常谈
> CSS2.1的布局分为3种：
1. 常规流(Normal Flow)
2. 浮动(Float)
3. 绝对定位(Absolute Position)
这3种不能混用。如果代码里看到position:absolute;display:block;这种明显是概念混乱。
很多人也错把position:relative跟position:absolute归为一类。position:relative是常规流中的一种，例外是它可以和Float一起使用。

#开始整理
## background-size
这里讲background-size属性的cover值

> 按比例调整背景图片，这个属性值跟contain正好相反，背景图片会按照比如自适应铺满整个背景区域。假如背景区域不足以包含背景图片的话，那么背景图片就会被咔嚓。

个人认为非常适用于不可重复背景图的某些特定大背景之下的场景
```css
body {
    background: url("@{img-path}bg.jpg") #000 50% no-repeat; //此时#000是为IE8之下做的降级处理
    width: 100%;
    background-size: cover;
    background-attachment: fixed;
}
```

## 毛玻璃
### 移动端
backdrop-filter 属性
```css
@supports (-webkit-backdrop-filter: none) {
  .Box-header {
      background: rgba(255,255,255,.6);
      -webkit-backdrop-filter: brightness(1.5) blur(4px);
  }
}
```
### PC应用
```css
body, main::before{
    background:url("img.jpg")0/cover fixed;
}
main{
    position:relative;
    background:hsla(0,0%,100%, .3);
    overflow:hidden;
}
main::before{
    content:"";
    position:absolute;
    top:0;
    right:0;
    bottom:0;
    left:0;
    filter:blur(20px);
    margin:-30px;
}
```

### 为什么移动端页面（H5）的边框都使用1px的div而不用border？
> 解决一：1px的div是用来实现2倍3倍屏下的1px, boder设置成1px，iPhone6这种device ratio是2的屏幕会变成2px，效果近似于WEB页面放大的效果。
> 解决二：用来解决1px在iphone 4 5 6上2倍，6p3倍的屏幕像素比，然后通过scale缩小，达到一像素效果。weui使用此方式。

### webkit-backface-visibility:hidde
> webkit-backface-visibility:hidden: 隐藏被旋转的 div 元素的背面 这个是解决多层级之间的混乱关系的。浏览器会自动帮你在轴上分层，之后遮罩。


### word-wrap word-break 
```
word-wrap 断行
word-wrap: normal
word-wrap: break-word
word-wrap: inherit
```
```
word-break 断词
word-break: normal 
word-break: break-all 
word-break: keep-all
word-break: inherit
```
