

- ##### 会影响 js 获取的useragent、无论是否是headless模式

- 格式--luna_user_agent=value

```
--luna_user_agent=Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.107 Safari/537.36
```

拓展阅读:

- 设置版本时、如果是pc版建议最大版本117最小112,请在这个区间设置主版本号；理由是这个是一个116版本编译的
- 如果考虑css特性等因素在这个版本内最佳
- 如果是mobile版本，暂时并无此限制，但是最好遵循。
- 至于full-version；则可以在这个主版本号范围内查询
- https://chromium.googlesource.com/chromium/src/+refs
- 里面有大量的112-117之间的全版本号可以查询
- 





- ##### 会影响 http 请求数据包内的useragent

```
--luna_header_1=User-Agent-lunareplace-Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.107 Safari/537.36"
```

拓展阅读:

- luna_header_1 数字1,这里并不是写错了，而是可以支持1-9个协议数据包修改项

- 也就是说，不仅仅可以修改useragent，可以修改任何你需要替换的数据包

- 格式--luna_header_1=key-lunareplace-value,其中-lunareplace-作为分隔符，代表替换的意思，

- 还有对应的-lunaremove-

  

