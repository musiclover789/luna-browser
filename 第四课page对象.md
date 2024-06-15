**核心**：其实核心就是一句话，你操作page对象，就是等同于操作一个浏览器页面对象！



page对象是Luna框架中的核心概念，它代表着你真实浏览器打开的每一个页面。无论是鼠标点击、元素选择、鼠标移动、拖拽、键盘输入、触摸操作、多页面切换，还是网络数据包获取、cookie等操作，几乎所有常用操作都在page对象中完成。如果需要关闭某个页面，也是在对应的页面对象上进行操作。



```
type Page struct {
    DevToolsConn         *protocol.DevToolsConn //浏览器和luna框架的底层链接
    PageID               string //窗口ID
    CurrentURL           string //当前链接
    Title                string //title
    WebSocketDebuggerUrl string //url形式的浏览器和luna框架的底层链接
    Port                 int //端口
    Alive                bool //页面是否还存活
    ImgPath              string //存放图片的基础目录//视觉方面的-暂时无需了解
}
```



你可以这样创建一个浏览器的page对象

```
err,pageobj:=browserObj.OpenPage("https://www.baidu.com")
```



你也可以这样创建

```
	err, pageobj := browserObj.OpenPageAndListen("https://www.baidu.com", func(session *protocol.Session) {

	})
```



区别是什么呢？

第一种创建方式是专为初学者设计的。



OpenPageAndListen：

- "这个函数需要两个参数：

  1. 要打开的网址。

  2. 作为参数传递进来的函数，你可以理解就是页面打开过程中的回调函数。

     

  它的作用是在打开页面时，创建监听。大致有两种用途：

  1. 拦截页面打开过程中的请求数据包和后续数据包。

  2. 判断页面是否加载完成。

     

  

  

举个完整的例子、来判断页面是否打开完成

```
                var wg sync.WaitGroup
		wg.Add(1)
		err, pagePro := browserObj.OpenPageAndListen("https://www.baidu.com", func(Session *protocol.Session) {
			page.PageEnable(Session)
			Session.SubscribeOneTimeEvent("Page.loadEventFired", func(param interface{}) {
				fmt.Println("Waiting for the page to fully load")
				wg.Done()
			})
		})
		if err != nil {
			fmt.Println(err.Error())
			return
		}
		wg.Wait()
```

你也可以在任何你逻辑需要的地方这么写

```
               var wg1 sync.WaitGroup
		wg1.Add(1)
                //打开页面监听
		page.PageEnable(pagePro.Session)
		pagePro.Session.SubscribeOneTimeEvent("Page.loadEventFired", func(param interface{}) {
			fmt.Println("Waiting for the page to fully load")
			wg1.Done()
		})
		wg1.Wait()
```

举个完整的例子、来说明如何拦截数据包



```
err, p1 = browserObj.OpenPageAndListen("https://www.baidu.com/", func(session *protocol.Session) {
network.EnableNetwork(session)
network.RequestResponseAsync(session, func(requestId string, request, response map[string]interface{}) {
 fmt.Println(luna_utils.FormatJSONAsString(request),luna_utils.FormatJSONAsString(response))
    //平时用不上,并不是每个请求都有请求报体；需要根据请求的url自行判断是否需要使用
    //network.GetResponseBody(session, requestId, time.Minute)
  })
})
```





选择器的作用是定位页面上的元素，比如按钮或输入框，以便进行操作。Luna框架支持三种选择器：CSS选择器、XPath和视觉选择器。在这里，我将重点介绍前两种。

- CSS选择器：使用CSS选择器语法来定位元素，例如通过类名、ID或标签名。
- XPath：使用XPath语法来定位元素，它提供了更强大的定位功能，可以通过元素的层级结构、属性等进行定位。



```
pageObj.GetElementPositionByCssOnPage(selector string) (err error, randomX, randomY float64) 
```



要获取元素的坐标点，可以使用CSS选择器来指定元素。你可以在浏览器的开发者模式下（按下F12键），使用元素面板选中需要的元素，然后右键复制其选择器，将该选择器作为参数传递给相应的函数即可。







返回的randomX和randomY是指元素的坐标点。之所以称为random，是因为元素实际上是一个矩形区域，而不是一个像素点。举个例子，如果是一个按钮，它实际上是一个矩形区域，random的意思是返回该矩形区域内的任意坐标点，确保可以点击到元素而不会留下机器人的痕迹。想要了解更多选择器示例，请查看选择器相关的文档，这里只提供了一个示例。





##### 鼠标操作：

 鼠标操作目前支持、点击、移动、拖拽、touch（手机端一般需要用）

```
pageObj.SimulateMouseMoveToTarget(endX, endY float64) error
```

这个函数接收两个参数，分别是鼠标移动的目标终点的x和y坐标。它会将鼠标移动到指定的位置。你可以参考上一个选择器的示例来获取目标位置的坐标。至于起点坐标，函数会自动获取当前鼠标的位置。然后，它会模拟多级贝塞尔曲线，以一种更接近人类的方式移动到目标位置。无论是通过轨迹分析还是trusted状态，这种移动过程都无法被识别。





点击

```
p1.SimulateMouseClickOnPage(x, y)
```

此函接受2个参数、分别是你需要点击的目标元素的x、y坐标，坐标哪里来，也请参考选择器的示例。这样鼠标就会在这个地方单击

并且他在单击的时候，会模拟人类的卡顿感。



键盘操作

```
SimulateKeyboardInputOnPage(text string)
```

这个函数只需要一个参数，就是你要输入的内容。我没有设计像其他框架那样直接给元素添加值的方式，因为那样不会触发输入事件，容易被检测出来。在使用这个函数时，你需要先点击一下你的输入框，确保代码操作方式类似于人类。函数会模拟输入法输入，并根据你的打字速度模拟输入。







```
paegObj.GetPages()
```

我们接下来讲一下这个函数，我们先简单的看一个小例子，其实他是一个在browser对象需要操作的，但是我们拿到这里来讲

是因为他最终的目的更像是在操作页面。

```
	_, ps := browserObj.GetPages()
	for _, pi := range ps {
		browserObj.SwitchPage(pi)
		fmt.Println(pi.CurrentURL, pi.Title)
		fmt.Println(">>>>>>>>>>>>")
	}
```



这个函数的作用是在打开页面、点击按钮后，可能会弹出许多不同的页面，我们需要切换到我们希望操作的页面。它会返回一个包含当前打开的所有页面的page对象的数组。你可以通过页面的标题或URL来过滤你需要的页面，然后对这些页面对象进行类似page对象的操作，没有太大区别。至此为止，其他函数的详细用法可以查看具体文档。

