

-如果使得设置生效则一定要设置"--luna_header_set=true"

- --luna_header_1
- 取值范围1-9也就是如:--luna_header_1 、--luna_header_2、--luna_header_3    ... --luna_header_9
- 根据需要可以写1个或者多个
- 分隔符    -lunareplace-
- 匹配到key 替换成 value
- 分隔符   -lunaremove-
- 匹配到key 删除掉此条header项

- ```
  "--luna_header_set=true",
  "--luna_header_1=accept-language-lunareplace-en;q=0.9",
  "--luna_header_2=sec-ch-ua-arch-lunaremove-",
  ```

  

