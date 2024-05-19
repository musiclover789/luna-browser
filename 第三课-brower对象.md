我们来了解这个Browser对象；

包括：如何创建对象、如何使用对象的函数、如何关闭。

**核心**：其实他所有的核心就是一句话，一个browser对象，就是一个chromium浏览器的实例，你操作这个对象，就等于在操作

chromium浏览器。



对象的数据结构

```
type Browser struct {
	ChromiumPath    string         //你浏览器的实际路径
	Port            int            //端口，你无需关注
	BrowserOptions  BrowserOptions //可选参数，配置proxy、窗口大小等、
	DevtoolsManager *protocol.DevtoolsRoot//，你无需关注
	DevToolsConn    *protocol.DevToolsConn//，你无需关注
	First           bool //是不是第一次打开窗口
	mu              sync.Mutex//，你无需关注
	Pages           []*Page//这个浏览器当前的所有页面
	ImgPath         string                     //存放目标图片的基础目录，你无需关注
	Proxy           *reverse_proxy.ProxyServer //proxy对象
	TargetID        string //这个browser的唯一id、多线程时候、可以作为区分对象使用。
}
```



- NewBrowser 对象：

  - 创建一个浏览器对象，建立了Luna框架和浏览器之间的链接。
  - 可对该浏览器执行操作，如打开浏览器、关闭浏览器。

  参数：

  1. chromiumPath：实际浏览器的路径，例如 c:\default\chromium.exe。
  2. options：BrowserOptions 对象，设置浏览器初始化时的参数，如隐身模式、窗口大小、代理IP等。

  可根据需要传递参数，不需要的可不传。

  举例，如果只想设置不使用隐身模式和窗口大小。

  

```
	_, browserObj := devtools.NewBrowser(chromiumPath, &devtools.BrowserOptions{
		
		//设置非隐身模式
		Headless: false,
		
		WindowSize: &devtools.WindowSize{
			Width: 1024,
			Height: 768,
		},
	})
```





- 完整代码示例：

- 你也可以完整的操作

  ```
  	_, browserObj := devtools.NewBrowser(chromiumPath, &devtools.BrowserOptions{
  		//设置缓存目录,
  		CachePath: luna_utils.CreateCacheDirInSubDir("C:\\workspace\\tempcatch"),
  		//设置你认为需要的指纹信息/更多指纹信息查看如何修改指纹文档
  		Fingerprint: []string{"--luna_languages=en-GB","--luna_platform=win64"},
  		//设置非隐身模式
  		Headless: false,
  		ProxyStr: "http://API1M5TV:9BFF49220D11@42.179.160.60:39349",
  		WindowSize: &devtools.WindowSize{
  			Width: 1024,
  			Height: 768,
  		},
  	})
  ```



BrowserOptions 的完整参数如下：

- CachePath：浏览器缓存目录。
- ImgPath：存放目标图片的基础目录，通常可忽略。
- Headless：浏览器显示或隐身模式下运行。
- ProxyStr：整个浏览器生命周期内使用的代理IP。
- Fingerprint：浏览器运行时的指纹。
- WindowSize：浏览器窗口大小设置。"





这些参数是可选的、你可以传递你需要的一个或者多个；