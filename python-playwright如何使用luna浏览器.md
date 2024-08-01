



python- playwright示例:



```
import time
from typing import List

from playwright.sync_api import sync_playwright

import portpicker


#### 随机获取一个 未被占用的远程调试端口
#### 这个函数是必要的
def get_port() -> int:
    return portpicker.pick_unused_port()

## 将指纹数据写入到文件
def write_fingerprint_to_file(fingerprint: List[str], filename: str):
    with open(filename, 'w') as f:
        for line in fingerprint:
            # 去掉每行开头的 '--'
            line = line.lstrip('-')
            # 写入到文件中
            f.write(line + '\n')

def main():
    fingerprints=[
        "--luna_webrtc_public_ip=101.29.120.1",
        "--luna_audio_random_int_number=981",
        "--luna_platform=win64"

    ]
    ##获取随机未占用远程调试端口
    random_port=str(get_port())
    ##将指纹信息写入文件即可
    ##原理:就是将指纹文件写入到端口命名的文件，这个路径一定是c:\\luna-temp\\其他目录不生效。
    write_fingerprint_to_file(fingerprints,"c:\\luna-temp\\"+random_port)
    # luna 浏览器的路径-这里一定要是luna浏览器的路径，而不是其他浏览器，否则你的指纹无效，另外你的指纹如果未经授权，也是无效
    browser_path = 'C:\\workspace\\chrome\\chrome\\src\\out\\Default\\chrome.exe'


    ###以下是playwright的正常逻辑，您正常写即可。
    with sync_playwright() as p:
        # 使用 Chromium，并指定自定义路径、指定远程调试端口
        ##如果你是多线程情况使用，请自己写好--user-data-dir=  也就是你要区分自己的用户缓存路径，否则你的指纹会造成混乱。或者程序崩溃等未知问题。
        ## 也就是说不同的线程，不同的实例，要采用不同的缓存目录，而不是同一个。
        browser = p.chromium.launch(executable_path=browser_path, headless=False, args=[
            '--remote-debugging-port='+random_port] )
        # 创建一个新的浏览器上下文和页面
        context = browser.new_context()
        page = context.new_page()
        # 导航到示例网站
        page.goto('https://www.browserscan.net')
        time.sleep(10000)
if __name__ == '__main__':
    main()

```


