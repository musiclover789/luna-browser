

代码示例:

```
_, p1 := browserObj.OpenPageAndListen("https://www.baidu.com/", func(devToolsConn *protocol.DevToolsConn) {
		network.SetCookieByURL(devToolsConn, "luna_url", "luna-cookie", "https://www.baidu.com")
    network.SetCookie(devToolsConn, "luna_domain", "luna-cookie", "www.baidu.com")
    //network.ClearBrowserCookies(devToolsConn)
})

network.SetCookie(p1.DevToolsConn, "luna_domain_abc", "luna-cookie", "www.baidu.com")

urls := []string{"https://www.baidu.com"}
cookies, _ := network.GetCookies(p1.DevToolsConn, urls)

for _, result := range gjson.Parse(luna_utils.FormatJSONAsString(cookies)).Get("result.cookies").Array() {
    fmt.Println(result.Get("name").String(), result.Get("value").String(), result.Get("domain").String())
}
```





```
conn *protocol.DevToolsConn, key, value, domain string
```

- 静态函数
- 需要传递4个函数、浏览器链接、
- 你需要设置的cookie的key，value
- domain 指的是你需要对哪个url的domain生效；
- 如:// 设置cookie 百度举例 https://www.baidu.com/  baidu.com作为domain 即可





```
SetCookieByURL(conn *protocol.DevToolsConn, key, value, url string) 
```

- 静态函数
- 需要传递4个函数、浏览器链接、
- 你需要设置的cookie的key，value
- url 指的是你需要对哪个url生效；
- 如://通过url设置cookie 百度举例https://www.baidu.com/, https://www.baidu.com作为url即可





```
ClearBrowserCookies(conn *protocol.DevToolsConn)
```

- 静态函数
- 清楚所有cookie
- 参数、浏览器链接





```
GetCookies(conn *protocol.DevToolsConn, urls []string) (map[string]interface{}, error)
```

- 静态函数
- 返回给定url链接的所有cookie相关信息
- 参数、浏览器链接、url字符串类型数组
- 