# CSS3-Animation


CSS3 Animation 有八个属性

    1.animation-name
  
    2.animation-durition
  
    3.animation-delay
    
    4.animation-interation-count
    
    5.animation-direction
    
    6.animation-play-state
    
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
    
####steps第一个参数的错误的理解：

    step(5,start)
    
    第一个参数 number 为指定的间隔数，即把 keyframes 每帧分为 n 步阶段性展示，作用于<b>每两个关键帧之间，而不是整个动画</b>
    
```css
  @-webkit-keyframes circle {
        0% {background-position-x: 0;}
        100%{background-position-x: -400px;}
 }
 ```
    此刻设置steps(5，start）那么会发现5张图会出现帧动画的效果，因为steps中的5把 0% – 100%的规则，内部分成5个等分

实际内部会执行这样一个关键帧效果

```css
@-webkit-keyframes circle {
        0% {background-position-x: 0;}
        25% {background-position-x: -100px;}
        50% {background-position-x:-200px;}
        75%{background-position-x: -300px;}
        100%{background-position-x: -400px;}
```

    
    
    
    
