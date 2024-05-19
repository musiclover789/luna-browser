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

 
