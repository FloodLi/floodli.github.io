---
layout: post
title:  layer层动画
date:   2017-01-17 18:43:57
comments: true
tags: 
	- 移动开发
---

#### 一、系统自带动画效果
```obj-c
// layer层动画
CATransition *transition = [CATransition animation];
// 动画效果
transition.type = @"rippleEffect";
// 动画方向
[transition setSubtype: kCATransitionFromBottom];
// 动画时长
[transition setDuration:1];
// 动画重复次数, NSIntegerMax 无限次数
[transition setRepeatCount:NSIntegerMax];
// 给myView的layer属性添加一个动画效果
[self.myView.layer addAnimation:transition forKey:@"transition"];
```
> 附type值列表

<!--more-->

| type  |  效果 |
| :------------: | :------------: |
| "cube"  | 立方体翻滚效果   |
| "moveIn"  |  新视图移到旧视图上面 |
| "reveal"  |  显露效果(将旧视图移开,显示下面的新视图) |
| "fade"  |  交叉淡化过渡(不支持过渡方向)  (默认为此效果) |
| "pageCurl"  | 向上翻一页  |
| "pageUnCurl"  | 向下翻一页  |
| "suckEffect"  |  收缩效果，类似系统最小化窗口时的神奇效果(不支持过渡方向) |
| "rippleEffect"  |  滴水效果,(不支持过渡方向) |
| "oglFlip"  | 上下左右翻转效果  |
| "rotate"  | 旋转效果  |
| "push"  |   |
| "cameraIrisHollowOpen"  |  相机镜头打开效果(不支持过渡方向) |
| "cameraIrisHollowClose"  |  相机镜头关上效果(不支持过渡方向) |

#### 二、CAPropertyAnimation 属性动画
> CAPropertyAnimation 它是一个抽象类, 我们用它的两个子类来实现属性动画, 也是layer层动画

1.scale
```obj-c
// path参数填写的是transform的属性 scale是改变view的缩放比例
CABasicAnimation *basicAnimation = [CABasicAnimation animationWithKeyPath:@"transform.scale"];
// 时长
[basicAnimation setDuration:1];
// 次数
[basicAnimation setRepeatCount:NSIntegerMax];
// 设置缩放起始值
basicAnimation.fromValue = [NSNumber numberWithInt:0];
// 设置缩放结束值
basicAnimation.toValue = [NSNumber numberWithInt:1.5];
[self.myImageView.layer addAnimation:basicAnimation forKey:@"basicAnimation"];
// 设置动画结束后是否恢复到原来的状态
basicAnimation.autoreverses = YES;
```
2.rotation
```obj-c
// 设置旋转动画效果 ratation旋转
CABasicAnimation *basicAnimation2 = [CABasicAnimation animationWithKeyPath:@"transform.rotation"];
basicAnimation2.fromValue = [NSNumber numberWithInt:0];
basicAnimation2.toValue = [NSNumber numberWithInt:M_PI * 100];
[basicAnimation2 setDuration:200];
[basicAnimation2 setRepeatCount:NSIntegerMax];
[basicAnimation2 setAutoreverses:YES];
[self.myImageView.layer addAnimation:basicAnimation2 forKey:@"rotatiom"];
```
#### 三、关键帧动画
> 关键帧动画, 实现是通过一帧一帧的点或者角度等, 来实现整个动画过程

```obj-c
// path的值为路径位置
CAKeyframeAnimation *keyFrameAnimation = [CAKeyframeAnimation animationWithKeyPath:@"position"];
// 创建一个路径, 用来记录移动的每一帧
CGMutablePathRef path = CGPathCreateMutable();
// 指定移动的起始点坐标
CGPathMoveToPoint(path, NULL, self.myImageView.center.x, self.myImageView.center.y);
// 设置移动轨迹 也就是每一帧 (坐标)
// 参数1.为移动路径
// 参数2.备用参数, 设为NULL
// 参数3.移动的x坐标
// 参数4.移动的y坐标
CGPathAddLineToPoint(path, NULL, 100, 100);
CGPathAddLineToPoint(path, NULL, 10, 10);
CGPathAddLineToPoint(path, NULL, 200, 300);
CGPathAddLineToPoint(path, NULL, 300, 500);
    
// 给视图指定一条曲线路径
CGPathAddCurveToPoint(path, NULL, 200, 200, 100, 120, 40, 60);
CGPathAddCurveToPoint(path, NULL, 80, 10, 20, 100, 300, 100);
CGPathAddCurveToPoint(path, NULL, 30, 60, 80, 100, 200, 300);
CGPathAddCurveToPoint(path, NULL, 50, 90, 110, 10, self.myImageView.center.x, self.myImageView.center.y);
    
// 将路径添加到关键帧动画对象中
[keyFrameAnimation setPath:path];
[keyFrameAnimation setDuration:5];
[keyFrameAnimation setRepeatCount:NSIntegerMax];
[self.myView.layer addAnimation:keyFrameAnimation forKey:@"keyFrameAnimation"];
```
