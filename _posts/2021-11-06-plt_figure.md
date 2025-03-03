---
layout: post
title: Matplotlib画布
categories: python
tags: plt
author: renql
---

* content
{:toc}

每张画布只有一个Figure，而一个Figure可以包含多个Axes对象。一个axes对象即一个子图，这个对象包含大量的子元素，包括线条、文本、坐标轴复合对象等等。之所以和Figure进行分离的原因是，Figure用来控制尺寸等一些和元素无关的属性。Axes则用来管理内部的元素。通过Figure.add_axes()可以创建一个axes。或者，直接调用fig,ax = plt.subplots(n)一次创建这两个对象。

第三个重要的层是x(y)axis，这个层也是一个复合对象（实际上是mpl.axis.Axis和mpl.axis.Tick两个类），包含X或者Y轴的元素，包括刻度(Ticks)、刻度文字(Tick Labels ; Offset text)，轴标签(Axis Label)等。这一层用来控制图形的尺度，比如x/ylim用来控制坐标轴范围。比如xlabel用来设置label的一些属性，比如字体大小、旋转、颜色、背景和透明度等。

当调用plt.plot()方法的时候，如果系统没有检测到存在Figure对象和Axes对象，则会创建一个，如果检测到，则直接使用。

对于想要重新画一幅图，而不是将图形绘制在一个Figure中并且区分成几个subplot，直接使用plt.figure()创建一个新的Figure对象，使用plt.gcf()也可以捕获这个对象。

每个图形可以有很多子图形构成，每个子图形只有一个Axes，它们可以共享坐标轴，每个子图形都有其各自的AxesSubplot子轴，包含在总的Axes中。

使用plt进行绘图固然很方便，但如果需要细微调整，则不太方便。调用axes单个元素可以获得更精细的控制，并且更面向对象一些。

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0.1, 4, 0.5)
y = np.exp(-x)

#几种创建图形 Fig 和 Axes 的方法
fig = plt.figure(figsize=(12,9),dpi=100)
axe = plt.axes(projection=cart_proj)

fig = plt.figure(figsize=(12,9),dpi=300) 
axe = fig.add_axes([0.05, 0.05, 0.9, 0.65]) # 括号中列表指定了该Axes对象的左下角的x、y值、长dx，高dy

fig = plt.figure(figsize=(12,9),dpi=100)
axe = plt.subplot(1,2,i+1,projection=cart_proj) # 创建一行两列子图

fig, ax = plt.subplots(3, 3, sharex=True, sharey=True) # 返回的ax是一个图形列表

fig, ((ax1,ax2,ax3),(ax4,ax5,ax6),(ax7,ax8,ax9)) = plt.subplots(3,3)
print(ax)

# plot the linear_data on the 5th,8th subplot axes
ax[2][2].plot(x,y, '-')
ax[1][1].plot(x,y**2, '-')

# 对于一个包含多个轴的fig，可以使用 gcf().get_axis，或者直接对矩阵进行索引和操纵
for ax in plt.gcf().get_axes():
    for label in ax.get_xticklabels() + ax.get_yticklabels():
        label.set_visible(True)
        
# necessary on some systems to update the plot
plt.gcf().canvas.draw()
```

参考资料:    
- plt常用函数列表 <a href="https://matplotlib.org/stable/api/pyplot_summary.html" target="_blank">https://matplotlib.org/stable/api/pyplot_summary.html</a>   
- <a href="https://matplotlib.org/stable/gallery/lines_bars_and_markers/timeline.html#sphx-glr-gallery-lines-bars-and-markers-timeline-py" target="_blank">处理时间坐标轴的例子</a>
- <a href="https://blog.mazhangjing.com/2018/02/28/learn_matplotlib/#1-matplotlib%E7%AE%80%E8%A6%81%E4%BB%8B%E7%BB%8D" target="_blank">https://blog.mazhangjing.com/2018/02/28/learn_matplotlib/#1-matplotlib%E7%AE%80%E8%A6%81%E4%BB%8B%E7%BB%8D</a> 
