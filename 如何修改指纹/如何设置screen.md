要考虑和luna_devicePixelRatio设置匹配，因为你的实际屏幕分辨率是根据这2项算出来的。



```
对应的js是:

console.log("屏幕宽度: " + window.screen.width);
console.log("屏幕高度: " + window.screen.height);
console.log("可用宽度: " + window.screen.availWidth);
console.log("可用高度: " + window.screen.availHeight);
console.log("颜色深度: " + window.screen.colorDepth);
console.log("像素比例: " + window.devicePixelRatio);

```





- ##### luna_screen

- 格式：--luna_screen=value

- : 作为每一个子项的分隔符;

```
--luna_screen=height:803,width:360,availHeight:803,availWidth:360,availLeft:0,availTop:0,colorDepth:24,pixelDepth:24"

```

- `screen`: 指的是屏幕的相关信息。
- `height`: 屏幕的高度，这里是803像素。
- `width`: 屏幕的宽度，这里是360像素。
- `availHeight`: 可用的屏幕高度，即减去了系统任务栏等占用的部分后的高度，这里也是803像素。
- `availWidth`: 可用的屏幕宽度，即减去了系统任务栏等占用的部分后的宽度，这里也是360像素。
- `availLeft`: 可用的屏幕左侧边界的位置，这里是0。
- `availTop`: 可用的屏幕顶部边界的位置，这里是0。
- `colorDepth`: 屏幕的颜色深度，即每个像素点可以表示的颜色数量，这里是24位。
- `pixelDepth`: 像素深度，与颜色深度类似，指的是每个像素所占用的比特数，这里也是24位。



- ##### 2025年5月11日版本更新了如下内容；
- 对应js的检测点是:
  ```
  1. --luna_deviceWidth=360
  对应js: window.matchMedia('(device-width: 360px)').matches


2. --luna_deviceHeight=803
    对应js: window.matchMedia('(device-height: 803px)').matches


3. --luna_visualViewportWidth=360
   对应js: window.visualViewport?.width（现代浏览器）

4. --luna_visualViewportHeight=803
   对应js: window.visualViewport?.height（现代浏览器）

5. --luna_outerWidth=360
   对应js: window.outerWidth

6. `--luna_outerHeight=803`
   对应js: window.outerHeight

7. `--luna_innerWidth=360`
   对应js: window.innerWidth

8. --luna_innerHeight=803
   对应js: window.innerHeight

```
- 
```
	arr = append(arr, "--touch-events")
	arr = append(arr, "--luna_screen=height:803,width:360,availHeight:803,availWidth:360,availLeft:0,availTop:0,colorDepth:24,pixelDepth:24")

	arr = append(arr, "--luna_deviceWidth=360")
	arr = append(arr, "--luna_deviceHeight=803")

	arr = append(arr, "--luna_visualViewportWidth=360")
	arr = append(arr, "--luna_visualViewportHeight=803")

	arr = append(arr, "--luna_outerWidth=360")
	arr = append(arr, "--luna_outerHeight=803")
	arr = append(arr, "--luna_innerWidth=360")
	arr = append(arr, "--luna_innerHeight=803")

	arr = append(arr, "--luna_devicePixelRatio=3")
```

- `--touch-events`: 启用触摸事件支持。
- `--luna_screen`: 屏幕的完整配置信息集合。
- `height`: 屏幕的逻辑高度，值为803像素（与设备方向有关）。
- `width`: 屏幕的逻辑宽度，值为360像素（与设备方向有关）。
- `availHeight`: 可用屏幕高度（排除系统UI后的最大高度），值为803像素。
- `availWidth`: 可用屏幕宽度（排除系统UI后的最大宽度），值为360像素。
- `availLeft`: 可用区域左侧起始位置，值为0（无偏移）。
- `availTop`: 可用区域顶部起始位置，值为0（无偏移）。
- `colorDepth`: 颜色深度，表示每个像素可显示的颜色位数，值为24位。
- `pixelDepth`: 像素深度（通常与颜色深度一致），值为24位。
- `--luna_deviceWidth`: 设备的物理显示宽度，值为360像素（与硬件分辨率相关）。
- `--luna_deviceHeight`: 设备的物理显示高度，值为803像素（与硬件分辨率相关）。
- `--luna_visualViewportWidth`: 可视视口宽度（用户可见区域的布局宽度），值为360像素。
- `--luna_visualViewportHeight`: 可视视口高度（用户可见区域的布局高度），值为803像素。
- `--luna_outerWidth`: 窗口外部宽度（包含浏览器边框和控件），值为360像素。
- `--luna_outerHeight`: 窗口外部高度（包含浏览器边框和控件），值为803像素。
- `--luna_innerWidth`: 窗口内部宽度（包含滚动条的内容区域），值为360像素。
- `--luna_innerHeight`: 窗口内部高度（包含滚动条的内容区域），值为803像素。
- `--luna_devicePixelRatio`: 设备像素比（物理像素与逻辑像素的比率），值为3（如 1080px / 360px = 3）。

 
