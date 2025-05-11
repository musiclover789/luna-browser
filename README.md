# 具体文档看上面  ↑ 指纹部分以项目表格表格为最终参考

# luna-browser
luna抗指纹浏览器|文档

项目地址:https://github.com/musiclover789/luna

qq群 179991677
**更新日志 - 2025年5月11日**

**更新内容：**

**
	更新了

 
 	arr = append(arr, "--luna_deviceWidth=360")
	arr = append(arr, "--luna_deviceHeight=803")

	arr = append(arr, "--luna_visualViewportWidth=360")
	arr = append(arr, "--luna_visualViewportHeight=803")

	arr = append(arr, "--luna_outerWidth=360")
	arr = append(arr, "--luna_outerHeight=803")
	arr = append(arr, "--luna_innerWidth=360")
	arr = append(arr, "--luna_innerHeight=803")
 **

**更新日志 - 2024年8月28日**

**更新内容：**

**全面更新了指纹技术、cavans、rect、audio等指纹算法、此版本更为真实、但是取值范围相对较小，根据自己需要选择。**



**更新日志 - 2024年8月2日**

**更新内容：**

**1.修复go-python-luna框架-传入非luna命令行参数失效bug**

**更新日志 - 2024年7月31日**

**更新内容：**

**1.更新client_rects指纹项**


**更新日志 - 2024年7月30日**

**更新内容：**

**1. 更新声卡指纹同步识别问题**

**更新日志 - 2024年7月12日**

**更新内容：**

**1. 修复webgpu相关指纹项**

**1.1 修复内核子数据包 meta header 问题；

**1.2 修复headless模式下、useragent 头问题



**更新日志 - 2024年5月4日**

**更新内容：**

**1. 重新修改了canvas-bug-指纹大量重复bug**

**1.1 增加了声卡指纹、webrtc公网ip设置、语音合成器设置；

**1.2 其他指纹项 和老版本一样，参考luna golang版本 如何设置

```
请注意新的版本-抗指纹部分要用这个、这里以手机的指纹为例：


Fingerprint: []string{
			"--luna_user_agent=Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Mobile Safari/537.36",
			"--luna_header_1=User-Agent-lunareplace-Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Mobile Safari/537.36",
			"--luna_userAgentData=Chromium:116-luna-Google Chrome:116-luna-Not-A.Brand:24-luna-platform:Android-luna-mobile:true-luna-platform_version:12.0.0-luna-ua_full_version:116.0.4515.186-luna-model:Samsung Galaxy-luna-architecture:arm64",
			"--luna_languages=zh-CN",
			/*****
			luna_screen 这个的用法稍微有点改变，不过相信应该直接能看懂
			****/
			"--luna_screen=height:803,width:360,availHeight:803,availWidth:360,availLeft:0,availTop:0,colorDepth:24,pixelDepth:24",
			"--luna_devicePixelRatio=3",             //屏幕缩放
			/*****
			luna_cavans_random_int_number 这个的用法改变，改成1-99999内的任意整数，步长根据自己的需求；
			在100内随机；举个例子比如1、102、199、268，反正随机即可。
			****/
			"--luna_cavans_random_int_number=99981", //取值1-99999 步长100 内随机
			"--luna_audio_random_int_number=9997",   //取值1-9999 声卡指纹
			"--luna_platform=Linux armv81",
			"--luna_maxTouchPoints=5", //手机触控点数量
			//"--webrtc-ip-handling-policy=disable_non_proxied_udp",
			"--luna_webrtc_public_ip=111.29.120.230", //公网ip 总之你希望出口的ip是什么就写什么，要保持一致就行。
			/***
			手机上要尽量不要用语音合成器、如果不用就注释掉即可。
			*/
			//"--luna_speechSynthesisVoice=name:clark<>lang:en-US<>voice_uri:mock.voice.clark<-luna->name:Google Deutsch<>lang:de-DE<>voice_uri:Google Deutsch",
			/**
			voice1->voice_uri = String("mock.voice.clark");
			 voice1->name = String("clark");
			 voice1->lang = String("en-US");
			*/
			/***
			 */

		}
```

**更新日志 - 2024年4月26日**

**更新内容：**

**1. 重新修改了canvas机制，目前采用真实指纹库技术；**

**1.1 影响框架部分:**

- 废弃了之前传入canvas的两个参数：
  - `--luna_canvas_random_str`
  - `--luna_canvas_random_int`
- 改为：
  - `--luna_canvas_random_int_number=4`
  - 类型：整数
  - 取值范围：1-999
- 注：由于采用真实指纹库机制，即使改动了canvas，仍有可能保持不变，但这种可能性较低。解决办法是调整步长，例如1、3、5、7、9等。但通常情况下不会改变，根据自身需要自行决定。

**2. 更新了对应的Chromium内核；**

**2.1 优化指纹部分；**



# 更新日志 - 2024年4月11日

1. **优化指纹失效**：解决了指纹可能失效的问题。
2. **微调代理速度**：对代理速度进行了优化调整。
3. **新增窗口设置功能**：增加了`browserObj.SetWindowBounds()`方法，用于设置窗口大小和位置。
4. **修复JavaScript失效问题**：解决了Windows系统中JavaScript可能失效的问题。
5. **调整关闭代理方式**：改进了关闭代理的显式和隐式方式。
6. **修复多进程意外退出**：修复了在多进程情况下可能导致程序意外退出的问题。
