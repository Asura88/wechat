#  一款New工具FastjsonScan（附下载）

[ 橘猫学安全 ](javascript:void\(0\);)

**橘猫学安全** ![]()

微信号 gh_af700ee13397

功能介绍 每日一干货🙂

____

___发表于_

收录于合集 #网络安全技术 209个

# FastjsonScan

一款探测FastJson漏洞工具

## 0x00 FastjsonScan now is public 🎉🎉🎉

### WHAT?

FastjsonExpFramework一共分为探测、利用、混淆、bypass JDK等多个模块，而FastjsonScan
是其中一部分，通过报错、请求、依赖库等探测实现多方面定位fastjson版本

### WHY?

现有的fastjson扫描器无法满足迭代速度如此快的fastjson版本，大部分扫描器早已无人维护，已不适配高版本。我将持续优化此系列项目。

### HOW?

目前fastjsonScan支持  
☑️支持批量接口探测  
☑️1.2.83及以下的区间探测(主要分为48,68,80三大安全版本)  
☑️支持报错回显探测  
☑️DNS出网检测  
☑️支持AutoType状态检测  
☑️依赖库检测  
☑️延迟检测

### TODO

适配内网环境下的探测  
适配webpack做自动化扫描  
完善DNS回显探测依赖库的探测  
完善在61版本以上并且不出网的检测方式  
完善其他不同json解析库的探测 完善相关依赖库检测

### 如果在使用过程中有任何问题欢迎提出issues👏

### Demo

![]()扫描结果  
![]()

## Usage

  

  *   *   *   * 

    
    
    FastjsonScan [-u] url [-f] urls.txt [-o] result.txt-u 目标url，注意需要加上http/https-f 目标url文件，可以扫描多条url-o 结果保存文件，默认在当前文件夹下的results.txt文件

## 0x01 Dev Notes

### 2022-09-05 0.5

Framework分离出scan模块

### 2022-09-05 0.4 beta

☑️重构版本探测模块，将判断fastjson,jackson,org.json,gson分离出来做识别模块TODO:  
利用dnslog探测依赖库  
利用模块编写

### 2022-09-04 0.35 beta

☑️修复了48版本的探测payload,该payload在进行80版本的payload探测之后，会触发tojavaobject从而将java.net.InetAddress类加入白名单，当进行第二次版本探测时会产生误报  
☑️版本检测会优先判断AutoType是否开启，如果开启只能模糊区分48以下及以上

### 2022-09-03 0.34 beta

☑️重构了版本探测模块，由之前精确探测分成了3块（48，68，80）  
☑️重写了判断版本的逻辑  
☑️补充了80版本与83版本的探测TODO:  
目标依赖库环境的探测  
AutoType的状态对版本探测有影响，需要做处理

### 2022-09-02 0.33 beta

☑️修改了含有jackson字段的报错检测逻辑  
☑️DNS检测新增10秒的等待时间，防止网络原因导致误报

### 2022-09-01 0.32 beta

☑️添加多条gadget，部分gadget复现不成功，根据目标的环境添加  
☑️修改了延迟探测的bug  
☑️添加了URLReader的探测链

### 2022-08-07 0.31 beta

☑️增加了几条gadgets

### 2022-08-06 0.3 beta

☑️完成了AutoType探测模块

### 2022-08-05 0.2 beta

☑️完成了探测模块的主要部分：包括报错探测，DNS探测和延迟探测

## 0x02参考

https://github.com/safe6Sec/Fastjson  
https://github.com/hosch3n/FastjsonVulns  
https://github.com/iSafeBlue/fastjson-autotype-bypass-demo下载地址：  
https://github.com/a1phaboy/FastjsonScan/releases/tag/v1.1如有侵权，请联系删除

 **推荐阅读**

[实战|记一次奇妙的文件上传getshell](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495718&idx=1&sn=e25bcb693e5a50988f4a7ccd4552c2e2&chksm=c04d7718f73afe0e282c778af8587446ff48cd88422701126b0b21fa7f5027c3cde89e0c3d6d&scene=21#wechat_redirect)  
[「 超详细 | 分享
」手把手教你如何进行内网渗透](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495694&idx=1&sn=502c812024302566881bad63e01e98cb&chksm=c04d7730f73afe267fd4ef57fb3c74416b20db0ba8e6b03f0c1fd7785348860ccafc15404f24&scene=21#wechat_redirect)  
[神兵利器 | siusiu-
渗透工具管理套件](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495385&idx=1&sn=4d2d8456c27e058a30b147cb7ed51ab1&chksm=c04d69e7f73ae0f11b382cddddb4a07828524a53c0c2987d572967371470a48ad82ae96e7eb1&scene=21#wechat_redirect)  
[一款功能全面的XSS扫描器](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495361&idx=1&sn=26077792908952c6279deeb2a19ebe37&chksm=c04d69fff73ae0e9f2e03dd8e347f35d660a7fd3d51b0f5e45c8c64afc90c0ee34c4251f9c80&scene=21#wechat_redirect)  
[实战 |
一次利用哥斯拉马绕过宝塔waf](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495331&idx=1&sn=94b63a0ec82de62191f0911a39b63b7a&chksm=c04d699df73ae08b946e4cf53ceea1bc7591dad0ce18a7ccffed33aa52adccb18b4b1aa78f4c&scene=21#wechat_redirect)  
[BurpCrypto:
万能网站密码爆破测试工具](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495253&idx=1&sn=d4c46484a44892ef7235342d2763e6be&chksm=c04d696bf73ae07d0c16cff3317f6eb847df2251a9f2332bbe7de56cb92da53b206cd4100210&scene=21#wechat_redirect)  
[快速筛选真实IP并整理为C段 --
棱眼](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495199&idx=1&sn=74c00ba76f4f6726107e2820daf7817a&chksm=c04d6921f73ae037efe92e051ac3978068d29e76b09cf5b0b501452693984f96baa9436457e4&scene=21#wechat_redirect)  
[自动探测端口顺便爆破工具t14m4t](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495141&idx=1&sn=084e8231c0495e91d1bd841e3f43b61c&chksm=c04d6adbf73ae3cdbb0a4cc754f78228772d6899b94d0ea6bb735b4b5ca03c51e7715b43d0af&scene=21#wechat_redirect)  
[渗透工具｜无状态子域名爆破工具（1秒扫160万个子域）](http://mp.weixin.qq.com/s?__biz=Mzg5OTY2NjUxMw==&mid=2247495099&idx=1&sn=385764328aff5ec49acddab380721af0&chksm=c04d6a85f73ae393ffab22021839f5baec3802d495c34fb364cbdd9b7cb0cf642851e9527ba7&scene=21#wechat_redirect)  
 **查看更多精彩内容，还请关注** **橘猫学安全：** **每日坚持学习与分享，觉得文章对你有帮助可在底部给点个“** **再看 ”**

预览时标签不可点

微信扫一扫  
关注该公众号

[知道了](javascript:;)

微信扫一扫  
使用小程序

****

[取消](javascript:void\(0\);) [允许](javascript:void\(0\);)

****

[取消](javascript:void\(0\);) [允许](javascript:void\(0\);)

： ， 。   视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看

