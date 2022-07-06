## 文字的wxss样式

https://blog.csdn.net/zhaoyazhi2129/article/details/53443308

https://blog.csdn.net/LoraRae/article/details/105245079


## 微信小程序设置border-radius=“50px”无法成圆角的问题

https://blog.csdn.net/weixin_46060121/article/details/104966665

要加上overflow: hidden;

width: 100px;
height: 100px;
border-radius:50px;
overflow:hidden;

## flex

https://cloud.tencent.com/developer/article/1915780


https://blog.csdn.net/dxnn520/article/details/79342637
**非常详细的flex说明，看这篇就够了**

https://www.php.cn/xiaochengxu-445662.html#:~:text=%E5%B0%8F%E7%A8%8B%E5%BA%8F%E4%B8%AD%E8%AE%A9%E5%9B%BE%E7%89%87,%E5%9E%82%E7%9B%B4%E6%96%B9%E5%90%91%E5%B1%85%E4%B8%AD%E5%8D%B3%E5%8F%AF%E3%80%82

居中需要在父级写display:flex;

## wxs改变颜色，文字

https://blog.csdn.net/xiaokangna/article/details/121607852

非常好的代码

## tab切换卡片

https://www.freesion.com/article/9117829727/



## 边框大小 | box-sizing

https://cloud.tencent.com/developer/section/1071900

```css
/* Keyword values */
box-sizing: content-box;
box-sizing: border-box;
```

## wxss margin-left有效 margin-top无效

https://developers.weixin.qq.com/community/develop/doc/00042600a50a9882bea8c68c85bc00

text是行内元素，margin-top肯定没有效果，可以加个display:inline-block或display:block或者换成view标签

## 微信小程序wxss设置样式

https://www.cnblogs.com/yang-shuai/p/6899430.html

全面

## swiper-dots 样式

https://developers.weixin.qq.com/community/develop/doc/00084eca9c80b0a43dca3343551800

```css

.swiperContainer swiper-item {

  width: 100%;

  height: 400rpx;

  display: flex;

  justify-content: center;

  align-items: center;

}



.swiperContainer .wx-swiper-dot {

  display: inline-flex;

  justify-content: space-between;

  border-radius: 50%;

  height: 10rpx;

  width: 10rpx;

}



.swiperContainer .wx-swiper-dot::before {

  content: '';

  flex-grow: 1;

  border-radius: 50%;

}



.swiperContainer .wx-swiper-dot-active {

  width: 29rpx;

  height: 10rpx;

  border: none;

  border-radius: 4rpx;

  background: #327DFB;

}



.swiperContainer .wx-swiper-dot-active::before {

  border-radius: 50%;

}
```

### 修改指示器圆点的样式位置等

https://blog.csdn.net/mochenangel/article/details/107026362

.wx-swiper-dots 是小圆点指示器的父容器

.wx-swiper-dot 是圆点指示器一个点的样式

所以只需要重写 上述两个类名的样式，就可以做简单控制了

还有一点 关于swiper横向与纵向 小圆点指示器的类名是不一样的

.wx-swiper-dots-horizontal 表示横向（因为默认是横向的，所以可以直接用.wx-swiper-dots控制横向swiper的修改）

.wx-swiper-dots-vertical 表示纵向



## 分割线

https://blog.csdn.net/weixin_44531304/article/details/89014260

## 如何让多个button或者多个view显示在一行内，并且自动适应于屏幕的宽度

https://developers.weixin.qq.com/community/develop/doc/000e6a58238e48747ef71265756c00

整个父标签裹起来，设上 display:flex;justify-content:space-around;

## button组件样式

https://www.jianshu.com/p/93d7104be420

没有用，可以直接用colorUI

