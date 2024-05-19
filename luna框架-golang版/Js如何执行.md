- 两种方式执行js
- A：需要返回结果的
- B：不需要获取返回结果的



在哪个page对象上面执行，就等同于在哪个页面上执行js



A:代码示例:

```
  _,p1:=browserObj.OpenPage("www.baidu.com")
	p1.RunJS(" your js ")
	err,result:=p1.RunJSSync("your js",time.Minute)
```

- 这里的p1指的是您的page对象
- 详细: RunJSSync
- 参数: js、超时时间
- 该函数在指定时间内尝试获取返回结果，如果超时未获取到则错误“EvaluateWithResultSync timeout”。
- 返回结果类型:gjson 类型、如果您对gjson不熟悉，建议先大概看看<github.com/tidwall/gjson>。



RunJS

- 无返回值

RunJSSync

- 有返回值



B:代码示例:

```
_, pageObj := browserObj.OpenPageAndListen("https://capcut.com/login", func(devToolsConn *protocol.DevToolsConn) {
    //第一种
		runtime.Evaluate(devToolsConn, "your js")
		runtime.EvaluateWithResultSync(devToolsConn, "your js", time.Minute)
	})
	//第二种
	runtime.Evaluate(pageObj.DevToolsConn, "your js")
	runtime.EvaluateWithResultSync(pageObj.DevToolsConn, "your js", time.Minute)
	
	
```

- 使用方式同上

- 区别是，此用法可以不依托page对象

- 但是依托devToolsConn，任何page、或者browserObj对象都有devToolsConn属性

  