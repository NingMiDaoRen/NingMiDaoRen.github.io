---
title: PyGame基础
declare: true
date: 2020-08-01 11:30:50
tags: Python
categories: [计算机基础,Python]
---



<meta name="referrer" content="no-referrer" />  

<!--more-->

# PyGame基础

[TOC]

## Part 1 PyGame是什么

Pygame是Python中用于开发2D游戏的游戏引擎（可以作为游戏引擎），它可以给我们提供一个对游戏开发的宏观流程体验，来验证游戏的逻辑。它不适用于商业游戏开发，适合让那些游戏爱好者学习和算法学吐了的程序员消遣解闷。所以这又是一个不定期更新的文章。



## Part 2 最小开发框架

C语言的入口是main函数，同理作为游戏，它也有它自己的编程框架，这个框架是由于游戏的运行机制决定的。

![输入图片说明](https://images.gitee.com/uploads/images/2020/0801/114316_7388098d_5550632.png "屏幕截图.png")

事件（Event）：就是游戏中的各种I/O，键盘啦，鼠标点击啦，声音控制啦等等

所有游戏都是一个大循环里面监听玩家的输入，然后绘制结果到屏幕，进而达到人机交互。

```python
import pygame
import sys

pygame.init() #模块初始化
screen = pygame.display.set_mode((600,400))
pygame.display.set_caption("Hello World")
while True:
    for event in pygame.event.get(): #事件监听
        if event.type == pygame.QUIT: #游戏退出事件
            sys.exit()

    pygame.display.update() # 刷新窗体
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/0801/120109_b60f22fe_5550632.png "屏幕截图.png")

游戏开发的坐标系是笛卡尔坐标系，即，电脑屏幕左上角为(0,0)点，和网页开发的坐标系是一样的。

![输入图片说明](https://images.gitee.com/uploads/images/2020/0806/112720_67775d8e_5550632.png "屏幕截图.png")

### 0x00 小Demo - 小球碰撞实验

实验目的，掌握游戏开发下的坐标系，了解如何将图片转化成游戏中的一个矩形实体。

```python
import pygame
import sys
PICT_PATH = r"ball.gif"

size = (800,600)

pygame.init() #模块初始化

screen = pygame.display.set_mode(size)
pygame.display.set_caption("Hello World")

ball = pygame.image.load(PICT_PATH)
ball_rect = ball.get_rect()#使用Surface对象的get_rect,给球做一个外接矩形,
# 同时可以获取到一个对象的空间属性
speed = [1,1]
while True:
    for event in pygame.event.get(): #事件监听
        if event.type == pygame.QUIT: #游戏退出事件
            sys.exit()
    ball_rect = ball_rect.move(speed[0],speed[1]) #x,y轴的偏移量，单位是像素，必须为整数
    if ball_rect.left < 0 or ball_rect.right > size[0]:#边界判断
        speed[0] = -speed[0]
    if ball_rect.top <0 or ball_rect.bottom > size[1]:
        speed[1] = -speed[1]


    screen.fill((0,0,0))#小球移动后，背景色会变白，我们要还原背景(RGB)
    screen.blit(ball,ball_rect)#使图像绘制在另一个图像上(将小球画到矩形框里)
    pygame.display.update() # 刷新窗体
```

没法截动图，效果就不掩饰了。

### 0x01 改变小球的速度

小球运动，是由于循环一遍又一遍的做，你的CPU性能有多强大，你的循环运行速度就有多快，小球就会运动多快。所以控制小球速度主要就在于控制循环次数的速度。（你画的屏幕越大，感觉上速度会变慢）

```python
import pygame
import sys
PICT_PATH = r"ball.gif"

size = (600,400)
fps = 60 #一秒60帧

pygame.init() #模块初始化

screen = pygame.display.set_mode(size)
pygame.display.set_caption("Hello World")

fps_clock = pygame.time.Clock() #获取Clock对象，它可以自动计算刷新时间
ball = pygame.image.load(PICT_PATH)
ball_rect = ball.get_rect()

speed = [1,1]
while True:
    for event in pygame.event.get(): #事件监听
        if event.type == pygame.QUIT: #游戏推出事件
            sys.exit()
    ball_rect = ball_rect.move(speed[0],speed[1])
    if ball_rect.left < 0 or ball_rect.right > size[0]:
        speed[0] = -speed[0]
    if ball_rect.top <0 or ball_rect.bottom > size[1]:
        speed[1] = -speed[1]


    screen.fill((0,0,0))
    screen.blit(ball,ball_rect)
    pygame.display.update() # 刷新窗体
    fps_clock.tick(fps) #按帧率刷新
```



### 0x02 使用键盘控制小球的速度

规则：上箭头->纵向绝对速度->增加1个像素，下箭头，左箭头，右箭头同理。

**如何获取键盘输入，如何调节速度**

```python
import pygame
import sys
PICT_PATH = r"ball.gif"

size = (600,400)
fps = 300 #一秒300帧

pygame.init() #模块初始化

screen = pygame.display.set_mode(size)
pygame.display.set_caption("Hello World")

fps_clock = pygame.time.Clock() #获取Clock对象，它可以自动计算刷新时间
ball = pygame.image.load(PICT_PATH)
ball_rect = ball.get_rect()

speed = [1,1] #左右,上下
while True:

    for event in pygame.event.get(): #事件监听
        if event.type == pygame.QUIT: #游戏推出事件
            sys.exit()
        elif event.type == pygame.KEYDOWN:#有键盘输入
            if event.key == pygame.K_LEFT:#键盘输入的值判断
                if speed[0] <= 0:
                    pass
                else:
                    speed[0] = abs(speed[0]) - 1
            elif event.key == pygame.K_RIGHT:
                speed[0]+=1
            elif event.key == pygame.K_UP:
                speed[1]+=1
            elif event.key == pygame.K_DOWN:
                if speed[1] <= 0:
                    pass
                else:
                    speed[1] = abs(speed[1]) - 1
    print("Speed: ",speed)
    ball_rect = ball_rect.move(speed)
    if ball_rect.left < 0 or ball_rect.right > size[0]:
        speed[0] = -speed[0]
    if ball_rect.top <0 or ball_rect.bottom > size[1]:
        speed[1] = -speed[1]


    screen.fill((0,0,0))
    screen.blit(ball,ball_rect)
    pygame.display.update() # 刷新窗体
    fps_clock.tick(fps) #按帧率刷新
```



## Part 3 屏幕绘制机制

#### 0x00 Pygame屏幕绘制机制简介

pygame.display来绘制屏幕，如果想开启第二个窗口必须把第一个屏幕关掉。我们再来看一下用于描述屏幕的笛卡尔坐标系。

![输入图片说明](https://images.gitee.com/uploads/images/2020/0806/112720_67775d8e_5550632.png "屏幕截图.png")

根据我们对游戏窗体的需求，如:游戏全屏,窗口大小可调节,游戏屏幕无边框,更改游戏图标。

大致可以分出三种要求:

> 屏幕尺寸和模式
>
> >pygame.display.set_mode() 设置相关屏幕模式
> >
> >pygame.display.Info() 生成屏幕相关信息
>
> 窗口标题和图标
>
> >pygame.display.set_caption() 设置标题信息
> >
> >pygame.display.set_icon() 设置图标信息
> >
> >pygame.display.get_caption() 获得图标
>
> 窗口感知和刷新
>
> > pygame.display.get_active()
> >
> > pygame.display.flip()
> >
> > pygame.display.update()

同时支持OpenGL和硬件加速。

#### 0x01 Pygame屏幕尺寸和模式设置

```python
def set_mode(size=00, flags=0, depth=0, display=0): # real signature unknown; restored from __doc__
    """
    set_mode(size=(0, 0), flags=0, depth=0, display=0) -> Surface
    Initialize a window or screen for display
    """
    pass
```

size->设置分辨率，单位为像素

flag->显示标签有3种：

pygame.RESIZEABLE 窗口可调节大小

pygame.FULLSCREEN 窗口全屏显示

pygame.NOFRAME 无边界显示

**注: 每种显示模式有不同的处理机制**

以之前的小球游戏为例

设置了

```python
screen = pygame.display.set_mode(size,flags=pygame.RESIZABLE)
```

后改变屏幕大小会出现白框。这是因为游戏逻辑没有改变，边界判断是固定的，这就导致无论屏幕拉的多大，它只在初始边界内弹跳。

![image-20200806114104638](C:\Users\micha\AppData\Roaming\Typora\typora-user-images\image-20200806114104638.png)

通过pygame.display.Info()方法可以获取一个关于一个VideoInfo对象，即当前窗体的各种信息。

我们先改造一个全屏的游戏模式：

```python
import pygame
import sys
PICT_PATH = r"ball.gif"


fps = 300 #一秒300帧

pygame.init() #模块初始化

vInfo = pygame.display.Info()
size = (vInfo.current_w,vInfo.current_h)#获取系统当前的屏幕分辨率
screen = pygame.display.set_mode(size,flags=pygame.FULLSCREEN)#设置显示模式为全屏
pygame.display.set_caption("Hello World")

fps_clock = pygame.time.Clock() #获取Clock对象，它可以自动计算刷新时间
ball = pygame.image.load(PICT_PATH)
ball_rect = ball.get_rect()

speed = [1,1] #左右,上下
while True:

    for event in pygame.event.get(): #事件监听
        if event.type == pygame.QUIT: #游戏推出事件
            sys.exit()
        elif event.type == pygame.KEYDOWN:#有键盘输入
            if event.key == pygame.K_LEFT:
                if speed[0] <= 0:
                    pass
                else:
                    speed[0] = abs(speed[0]) - 1
            elif event.key == pygame.K_RIGHT:
                speed[0]+=1
            elif event.key == pygame.K_UP:
                speed[1]+=1
            elif event.key == pygame.K_DOWN:
                if speed[1] <= 0:
                    pass
                else:
                    speed[1] = abs(speed[1]) - 1
            elif event.key == pygame.K_ESCAPE:
                sys.exit()
    print("Speed: ",speed)
    ball_rect = ball_rect.move(speed)
    if ball_rect.left < 0 or ball_rect.right > size[0]:
        speed[0] = -speed[0]
    if ball_rect.top <0 or ball_rect.bottom > size[1]:
        speed[1] = -speed[1]


    screen.fill((0,0,0))
    screen.blit(ball,ball_rect)
    pygame.display.update() # 刷新窗体
    fps_clock.tick(fps) #按帧率刷新
```

再改造一个可以伸缩尺寸的版本：

VIDEORESIZE 事件可以返回一个当前新窗体的宽度和高度



```python
import pygame
import sys
PICT_PATH = r"ball.gif"


fps = 300 #一秒300帧

pygame.init() #模块初始化


size = (600,400)
screen = pygame.display.set_mode(size,flags=pygame.RESIZABLE)
pygame.display.set_caption("Hello World")

fps_clock = pygame.time.Clock() #获取Clock对象，它可以自动计算刷新时间
ball = pygame.image.load(PICT_PATH)
ball_rect = ball.get_rect()

speed = [1,1] #左右,上下
while True:

    for event in pygame.event.get(): #事件监听
        if event.type == pygame.QUIT: #游戏推出事件
            sys.exit()
        elif event.type == pygame.KEYDOWN:#有键盘输入
            if event.key == pygame.K_LEFT:
                if speed[0] <= 0:
                    pass
                else:
                    speed[0] = abs(speed[0]) - 1
            elif event.key == pygame.K_RIGHT:
                speed[0]+=1
            elif event.key == pygame.K_UP:
                speed[1]+=1
            elif event.key == pygame.K_DOWN:
                if speed[1] <= 0:
                    pass
                else:
                    speed[1] = abs(speed[1]) - 1
            elif event.key == pygame.K_ESCAPE:
                sys.exit()
        elif event.type == pygame.VIDEORESIZE:#监听到新的事件，屏幕尺寸更改
            size = width,height = event.size[0],event.size[1]
            pygame.display.set_mode(size,flags = pygame.RESIZABLE)
            
    print("Speed: ",speed)
    ball_rect = ball_rect.move(speed)
    if ball_rect.left < 0 or ball_rect.right > size[0]:
        speed[0] = -speed[0]
    if ball_rect.top <0 or ball_rect.bottom > size[1]:
        speed[1] = -speed[1]


    screen.fill((0,0,0))
    screen.blit(ball,ball_rect)
    pygame.display.update() # 刷新窗体
    fps_clock.tick(fps) #按帧率刷新
```



#### 0x02 Pygame窗口标题和图标设置

pygame.display.set_caption(title,) #设置标题

pygame.display.get_caption(title)

#### 0x03 Pygame窗口感知和刷新应用



## Part 4 事件处理机



## Part 5 色彩与绘图机制

