# CSS3-Animation


CSS3 Animation 有八个属性

    1.animation-name
  
    2.animation-durition
  
    3.animation-delay
    
    4.animation-interation-count　　n　|　infinite
    
    5.animation-direction　　　　　normal　|　alternate
    
    6.animation-play-state　　　　running　|　paused
    
    7.animation-fil-mode
    
    8.animation-timing-function
    

 前面六个很好理解,看W3C对animation-fill-mode的解释：
    
    
  ![img](https://github.com/herohql521/js-tips/blob/master/imgs/animation-fill-mode.JPG)
  
  
##animation-timing-funcition 规定动画的速度曲线
  ![img](http://images0.cnblogs.com/blog/329084/201507/110906315961940.png)
  
  但是漏掉了很重要的一个 <b>steps</b>
 
####理解steps

    steps(argument1,argument2) 指定了一个阶跃函数
    
    第一个参数指定了时间函数中的间隔数量（必须是正整数）
    
    第二个参数可选，接受 start 和 end 两个值，指定在每个间隔的起点或是终点发生阶跃变化，默认为 end
    
    step-start等同于steps(1,start)，动画分成1步，动画执行时为开始左侧端点的部分为开始
    
    step-end等同于steps(1,end)：动画分成一步，动画执行时以结尾端点为开始，默认值为end
    
    
看看W3C的规范 [transition-timing-function](https://www.w3.org/TR/2012/WD-css3-transitions-20120403/#transition-timing-function-property)
    
####steps第一个参数的正确的理解：

step(5,start)</br>
    
第一个参数 number 为指定的间隔数，即把 keyframes 每帧分为 n 步阶段性展示，作用于<b>每两个关键帧之间，而不是整个动画</b></br>


比如一张5帧的雪碧图，每个精灵图宽100px。

![img](https://herohql521.github.io/CSS3-Animation/5fps.jpg)


```css
  @-webkit-keyframes circle {
        0% {background-position-x: 0;}
        100%{background-position-x: -500px;}
 }
 ```
 
 此刻设置steps(5，end）那么会发现5张图会出现帧动画的效果，因为steps中的5把 0%  – 100%的规则，内部分成5个等份，每份占20%，也就是在两帧之间又添加了（n-1）个帧

实际内部会执行这样一个关键帧效果<br>

```css
@-webkit-keyframes circle {
        0%  {background-position-x: 0;}
        20% {background-position-x: -100px;}
        40% {background-position-x:-200px;}
        60% {background-position-x: -300px;}
        80% {background-position-x: -400px;}
        100%{background-position0x: -500px;}
```

###timing-function 作用于每两个关键帧之间，而不是整个动画　　[查看demo](https://herohql521.github.io/CSS3-Animation/5fps.html)

如果稍微修改一下，加入一个50%的状态</br>

```css
@-webkit-keyframes circle {
        0% {background-position-x: 0;}
        50% {background-position-x: -200px;}
        100%{background-position-x: -400px;}
 }
 ```
 
就好比把动画整体分成3帧，每两帧之间分成5个等份，好比0% ~ 50%之间分成了5个等份 ,50% ~ 100%也分成了5个等份。等同于每2帧之间插入了(n-1)帧 

实际内部会执行这样的关键帧效果

```css
@-webkit-keyframes circle{
        0% {background-position-x: 0;}
        
            10% {background-position-x: -50px;}
            20% {background-position-x: -100px;}
            30% {background-position-x: -150;}
            40% {background-position-x: -200;}
            
        50%{background-position-x: -250px;}
            
            60% {background-position-x: -300;}
            70% {background-position-x: -350;}
            80% {background-position-x: -400;}
            90% {background-position-x: -450;}
            
        100%{background-position-x: -500;}
}
```

###[查看demo](https://herohql521.github.io/CSS3-Animation/5fps2.html)
    
    从demo可以看出来，每次动画移动-50px,和上面的分解动作一样。
    
###再次强调　　timing-function 作用于每两个关键帧之间，而不是整个动画

####steps第二个参数的正确的理解：

    第二个参数可选，接受 start 和 end 两个值，指定在每个间隔的起点或是终点发生阶跃变化，默认为 end。
    
    2个参数都会选择性的跳过前后部分，start跳过0%，end跳过100%
    
    下面是w3c　step的工作机制图

![img](http://images.cnitblog.com/i/596159/201406/091121212334792.png)

看完这个图，我整个人都不好了，这表达是的什么鬼啊，作为一个数学呆完全不能明白啊。于是我画了下面一张草图

![img](https://herohql521.github.io/CSS3-Animation/zb.jpg)

当参数是start的时候，跳过0%，从20%开始动。

当参数是end的时候，跳过100%，到80%的时候就结束。

为什么会这样呢？比如 steps(5,end) 规定动画5帧，但是看我的草图，5个间隔(帧)，但却有6个阶跃状态，所以要砍掉一个，去头或者去尾？就靠start和end来规定。


 </br> </br> </br>
#####最后要感谢一个叫[Aaron艾伦](http://www.cnblogs.com/aaronjs/p/4642015.html)的大神,，这篇文章让我收货不少,点击名字有传送门。

    
    
    
    
