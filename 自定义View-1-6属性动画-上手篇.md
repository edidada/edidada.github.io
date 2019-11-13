---
title: 自定义View_1_6属性动画_上手篇
date: 2017-09-07 11:12:26
categories:
- Tech
tags: 
- Android
- View

---
[自定义View 1_6属性动画_上手篇](http://hencoder.com/ui-1-6/)

仅作为个人的笔记，版权归原作者所有

### 动画可以分为两类：

- Animation
- Transition

其中 Animation 又可以再分为 

- View Animation
- Property Animation

两类

### ViewPropertyAnimator

<!-- more -->

![相关方法](https://ws1.sinaimg.cn/large/006tKfTcgy1fj7x3rm1xxj30u50laq6y.jpg "相关方法")


### ObjectAnimator

使用方式：

- 1、如果是自定义控件，需要添加 setter / getter 方法；
- 2、用 ObjectAnimator.ofXXX() 创建 ObjectAnimator 对象；
- 3、用 start() 方法执行动画。


	public class SportsView extends View {
		float progress = 0;
		
		......
		
		// 创建 getter 方法
		public float getProgress() {
			return progress;
		}
		
		// 创建 setter 方法
		public void setProgress(float progress) {
			this.progress = progress;
			invalidate();
		}
	
		@Override
		public void onDraw(Canvas canvas) {
			super.onDraw(canvas);
		
			......
	
			canvas.drawArc(arcRectF, 135, progress * 2.7f, false, paint);
	
        ......
		}
	}
	
	......
	
	// 创建 ObjectAnimator 对象
	ObjectAnimator animator = ObjectAnimator.ofFloat(view, "progress", 0, 65);
	// 执行动画
	animator.start();




#### 通用功能
##### 1. setDuration(int duration) 设置动画时长
##### 2. setInterpolator(Interpolator interpolator) 设置 Interpolator

- AccelerateDecelerateInterpolator
- LinearInterpolator
- AccelerateInterpolator
- DecelerateInterpolator
- AnticipateInterpolator
- OvershootInterpolator
- AnticipateOvershootInterpolator
- BounceInterpolator
- CycleInterpolator
- PathInterpolator
- FastOutLinearInInterpolator
- FastOutSlowInInterpolator
- LinearOutSlowInInterpolator

##### 3. 设置监听器

###### 3.1 ViewPropertyAnimator.setListener() / ObjectAnimator.addListener()
###### 3.1.1 onAnimationStart(Animator animation)
###### 3.1.2 onAnimationEnd(Animator animation)
###### 3.1.3 onAnimationCancel(Animator animation)
###### 3.1.4 onAnimationRepeat(Animator animation)
###### 3.2 ViewPropertyAnimator.setUpdateListener() / ObjectAnimator.addUpdateListener()
###### 3.2.1 onAnimationUpdate(ValueAnimator animation)
###### 3.3 ObjectAnimator.addPauseListener()
###### 3.3 ViewPropertyAnimator.withStartAction/EndAction()

