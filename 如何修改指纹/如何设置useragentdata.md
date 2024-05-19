设置主版本号、和全版本号时 、要考虑和user-agent设置匹配。



```
对应的js是:
navigator.userAgentData
```





- ##### luna_userAgentData

- --luna_userAgentData为key

- 格式：--luna_userAgentData=value

- -luna- 作为每一项的分隔符

- : 作为每一个子项的分隔符;

```
--luna_userAgentData=Chromium:116-luna-Google Chrome:116-luna-Not-A.Brand:24-luna-platform:Android-luna-mobile:true-luna-platform_version:12.0.0-luna-ua_full_version:116.0.4515.186-luna-model:Samsung Galaxy-luna-architecture:arm64
```

- `luna_userAgentData`: 用户代理数据的标识符。
- `Chromium:116`: 使用的浏览器引擎是Chromium，版本号为116。
- `Google Chrome:116`: 浏览器是Google Chrome，版本号为116。
- `Not-A.Brand:24`: 浏览器品牌是“Not-A.Brand”，版本号为24。
- `platform:Android`: 使用的操作系统平台是Android。
- `mobile:true`: 设备是移动设备。
- `platform_version:12.0.0`: Android平台的版本号为12.0.0。
- `ua_full_version:116.0.4515.186`: 用户代理的完整版本号为116.0.4515.186。
- `model:Samsung Galaxy`: 设备型号是Samsung Galaxy。
- `architecture:arm64`: 设备的处理器架构是arm64。





pc版示例:

- 每一个都是:作为key、value的分隔符。
- -luna- 这个只是分隔符;

```
--luna_userAgentData=Google Chrome:92-luna-Chromium:92-luna-Not-A.Brand:24-luna-platform:win32-luna-mobile:false-luna-platform_version:6.1-luna-ua_full_version:92.0.4515.186-luna-model:PC-luna-architecture:x86_64
```

- `luna_userAgentData`: 用户代理数据的标识符。
- `Google Chrome:92`: 浏览器是Google Chrome，版本号为92。
- `Chromium:92`: 使用的浏览器引擎是Chromium，版本号为92。
- `Not-A.Brand:24`: 浏览器品牌是“Not-A.Brand”，版本号为24。
- `platform:win32`: 使用的操作系统平台是Windows 32位。
- `mobile:false`: 设备不是移动设备。
- `platform_version:6.1`: Windows平台的版本号为6.1。
- `ua_full_version:92.0.4515.186`: 用户代理的完整版本号为92.0.4515.186。
- `model:PC`: 设备型号是PC。
- `architecture:x86_64`: 设备的处理器架构是x86_64。



