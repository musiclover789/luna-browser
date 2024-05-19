- 支持的代理类型包括 HTTP、HTTPS 和 SOCKS5，同时也支持白名单和用户名密码格式。
- 使用国外代理时，有些代理可能是域名而不是直接的 IP 地址。这可能导致 WebRTC 隐私信息泄漏和访问速度变慢。最好避免选择这种类型的供应商，或者如果您有能力，可以通过域名获取单一 IP 地址。



代码示例:

```

func TestProxy(t *testing.T) {
	//启动前先杀死其他的chromium进程;为了防止程序以及停止但是依然在内存中贮存;
	//他会根据你的系统不同,使用命令行的命令进行杀死进程
	luna_utils.KillProcess()

	//初始化浏览器对象
	chromiumPath := "/Users/Chromium.app/Contents/MacOS/Chromium"
	_, browserObj := devtools.NewBrowser(chromiumPath, &devtools.BrowserOptions{
		//设置你的代理IP、他支持所有主流的种类https http socks5 有无密码均支持、白名的模式也支持、
		//"http://46.19.160.60:39349"
		//"http://API1M5T:9BFF4922D11@48.19.160.60:39349"
		//"https://46.19.160.60:39349"
		//"https://API1M5T:9BFF4922D11@48.19.160.60:39349"
		//"socks5://API1M5V:9BF49220D11@42.179.160.60:39349"
		ProxyStr: "http://API1M5TV:9BFF49220D11@42.179.160.60:39349",
	})

	
}

```





ProxyStr

- 字符串类型
- 格式参考上面的示例
