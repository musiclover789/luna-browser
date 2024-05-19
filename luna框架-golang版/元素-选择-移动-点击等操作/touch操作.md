



代码示例

```
err, p1 := browserObj.OpenPage("https://www.url.com")


	p1.Touch(100, 100)
	p1.TouchDrag(100, 100, 100, 200)
	p1.TouchTouchEvent(100, 100, "touchMove")
```





```
Touch(x, y float64)
```

- page实例对象函数
- 传入需目标点的x,y坐标
- 单位:像素
- 完成一次touch操作
- 这个操作的原理是，先启动touchStart、在启动touchEnd、中间间隔人类的反应时间。
- 这个模拟了，我们在触摸屏上面的一次点击





```
TouchDrag(startX, startY, endX, endY float64)
```

- page实例对象函数

- 函数接受、起点x,y坐标，终点x,y坐标

- 模拟一次人类的，拖动操作。

- 我们在操作手机的时候，大部分时候并不是类似move的概念，而是更类似于拖拽的方式。

- 比如我们滚动页面，希望往下翻滑动时候，其实就是在拖拽这个屏幕向下的一个过程。

  





```
TouchTouchEvent(x, y float64, touchType string)
```

- page实例对象函数
- 函数接受、x,y坐标
- 触摸类型：touchStart`, `touchEnd`, `touchMove`,`touchCancel 字符串类型
- 这个函数设计的目的是，如果你希望自己搭配这些偏向底层的操作，你可以自己组合这些事件。
- 来完成你自己的设计，如拖拽，如点击。
- 并不常用





如何获取x,y坐标，参考选择器文档

