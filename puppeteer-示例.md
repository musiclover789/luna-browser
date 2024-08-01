



puppeteer示例:



```
const puppeteer = require('puppeteer');
const fs = require('fs');

(async () => {

  //这里并未进行深度封装，所以您需要自己写获取未被占用端口的逻辑
  //这里的9992仅仅是示例,您可以给任意端口号，只要是未被占用即可
  free_port='9993'
  
  // 示例指纹串数组
  const fingerprints = [
    "--luna_webrtc_public_ip=101.29.120.5",
    "--luna_audio_random_int_number=981",
    "--luna_platform=win64"
  ];

  // 去掉每个字符串开头的 '--'
  const fingerprintArray = fingerprints.map(str => str.replace(/^--/, ''));

  // 写入文件的路径和文件名，请注意这里的c:\\luna-temp\\ 这个是必须要这个路径，其他路径不生效或者引发未知问题
  const filePath = 'c:\\luna-temp\\'+free_port;

  // 将指纹数组写入文件
  fs.writeFile(filePath, fingerprintArray.join('\n'), (err) => {
    if (err) {
      console.error('Error writing file:', err);
    } else {
      console.log(`File ${filePath} has been written successfully.`);
    }
  });

  //如果你是多线程用户，你应该指定自己的
  //如果你是多线程情况使用，请自己写好--user-data-dir=  也就是你要区分自己的用户缓存路径，否则你的指纹会造成混乱。或者程序崩溃等未知问题。
  //也就是说不同的线程，不同的实例，要采用不同的缓存目录，而不是同一个。
  const browser = await puppeteer.launch({
    //luna 浏览器的路径-这里一定要是luna浏览器的路径，而不是其他浏览器，否则你的指纹无效，另外你的指纹如果未经授权，也是无效
    executablePath:'C:\\workspace\\chrome\\chrome\\src\\out\\Default\\chrome.exe',
    headless:false,
    args: ['--remote-debugging-port='+free_port] // 指定远程调试端口号
  });
  //其他的就是你自己的正常逻辑，你自己参考puppeteer文档即可。
  const page = await browser.newPage();

  await page.goto('https://www.browserscan.net/');

})();

```


