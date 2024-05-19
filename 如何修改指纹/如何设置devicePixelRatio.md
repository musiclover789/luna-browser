要考虑和luna_screen设置匹配，因为你的实际屏幕分辨率是根据这2项算出来的。





```
对应的js是:
var pixelRatio = window.devicePixelRatio;
console.log("Device Pixel Ratio: " + pixelRatio);
```





- ##### luna_devicePixelRatio

- 指的是屏幕的缩放比;

- 格式：--luna_devicePixelRatio=value

- float类型

- 这里的value 一般根据你的实际情况，取值1 、1.5、 2 、2.5、 3 一般屏幕越大这个值越小

```
--luna_devicePixelRatio=3
```



 