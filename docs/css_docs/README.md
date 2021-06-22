---
sidebar: auto
---

## CSS盒子模型
定义：用来装页面元素的矩形区域，包含内容、边框和内外边距
种类：
- 标准盒子模型（content-box）：长宽只包括内容，内外边距和边框会撑大盒子
- IE盒子模型（border-box）： 长宽包括内外边距、边框和内容，内外边距和边框不会撑大盒子


## 清除浮动
    原因：当父元素未定义高度，子元素浮动会导致父元素高度塌陷
**方法：**
1. clear:both
   在浮动的元素后插入带有clear:both属性的块级元素
2. 伪元素clearfix
   在父元素上添加clearfix类，并将样式应用如下：
   ```css
   .clearfix:after {
       content: '';
       height: 0;
       display: block;
       clear: both;
   } 
     ```
3. overflow
    父元素设置 overflow: auto;

4. 父级元素定义高度

## BFC
    块级格式化上下文，是一个独立的容器，内部元素和外部元素不相互影响。

**触发条件：**
- 根元素
- float不为none
- overflow不为visible
- display为inline-block、table-cell、table-caption
- position的值为absolute、fixed

## CSS垂直水平居中
行内元素：
```css
text_align = center;  line-height = height
```

块级元素：
```css
- margin:0 auto;
/* 除了在ie上兼容性不强。几乎是最优选择 */
- display: flex; justify-content = center; align-items = center;
/* 不需要提前知道尺寸 */
- display: absolute; left: 0; right: 0; top: 0; bottom: 0; margin: auto;
/* 垂直居中 */
- display: table-cell;  vertcal-middle: middle
/* 需提前知道尺寸, margin-top和margin-left为自己高宽的一半 */
- display: absolute; left: 50%; top: 50%; margin-top: -20px; margin-left: -40px
/* 不需要提前知道尺寸 */
- display: absolute; left: 50%; top: 50%; transform: translate(-50%, -50%);

```

  

## 画一条0.5px的线
- 使用meta viewport ,设置initial-scale、min-scale、max-scale为0.5
- 使用transform:scaleY(0.5)

## CSS选择器及优先级和可继承属性
**选择器:**
1. id选择器
2. 类选择器
3. 标签选择器
4. 属性选择器
5. 相邻选择器
6. 子元素选择器
7. 后代选择器
8. 通配符选择器
9. 伪类选择器
10. 伪元素选择器

**优先级：**
元素标签:1
类选择器：10
id选择器：100
内联样式：1000

**注：**
>！important声明的样式优先级最高；
如果优先级一样，则选择后出现的样式；
继承得到的样式优先级最低。

**可继承属性：**
1. font-size
2. font-family
3. color
4. ul
5. li
6. dl
7. dt
8. dd
   


