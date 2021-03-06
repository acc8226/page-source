---
title: 使用GitHub搭建免费图床/网盘(CDN加速)
date: 2019-11-18 23:41:00
---

当我购买了域名后, 让我想好好利用这个已有域名获取免费的图床服务. 另一方面我所有写的md文章会用到, 不想受制于目前的简书图床. 

### 自己的服务器开放图床
服务器到期后就尴尬了, 排除. 到时候只能提前迁出, 非常麻烦. 另外一方面也说明文件命名非常重要.

### 尝试阿里云, 腾讯云等其他品牌的OOS
服务虽好, 可是需要付费

### 尝试七牛图床
存储服务创建完成后，需要配置一个融合CDN域名，融合CDN域名简单来说就是指资源对象的外链域名，七牛云提供了融合CDN的测试域名，官方提示为：七牛融合 CDN 测试域名（以 clouddn.com/qiniucdn.com/qiniudn.com/qnssl.com/qbox.me 结尾），每个域名每日限总流量 10GB，每个测试域名自创建起 30 个自然日后系统会自动回收，仅供测试使用并且不支持 Https 访问。因此需要我们自己配置一个CDN加速域名. 

**七牛测试域名1个月失效的问题(网友提供的解决方法)**
七牛提供的测试域名1个月就失效了，通常是够用的 。 如果失效了，也不用担心，找到原始的markdown 文件，用下面的命令对文件做个替换即可（new.bkt.clouddn域名需要按照实际进行替换）。
```
 sed -i "s#//.*bkt.clouddn#//new.bkt.clouddn#g" file.md
```
**注: 目前七牛不再提供测试域名了, 只能挥手告别. 哪怕按月或年付费也是可以的, 只要服务好**

### 尝试简书的免费图床
这是我一直不抛弃简书的原因, 目前一直在用, 想要用到图片的地方直接ctrl + V就可以了. 可是万一哪天简书突然变政策了就不好了.

### (最终方案)尝试使用Page服务的图床
腾讯旗下的coding 和 oschina旗下的码云在国内比较靠谱, 一方面空间没仔细看,空间不知道大不大. 
想的是开启Page服务然后git上传获得外链这种解决方案. 就是整体操作起来太麻烦.

github服务器在国外, 直接访问肯定太慢. 知道看到了教程**[PicGo](https://github.com/Molunerfinn/PicGo), [jsdelivr](https://www.jsdelivr.com/), [github](https://github.com/)**的组合. 令我眼前一亮.

> 放在Github的资源在国内加载速度比较慢，因此需要使用CDN加速来优化网站打开速度，jsDelivr + Github便是免费且好用的CDN，非常适合博客网站使用

> CDN的全称是Content Delivery Network，即内容分发网络。CDN是构建在网络之上的内容分发网络，依靠部署在各地的边缘服务器，通过中心平台的负载均衡、内容分发、调度等功能模块，使用户就近获取所需内容，降低网络拥塞，提高用户访问响应速度和命中率。CDN的关键技术主要有内容存储和分发技术。——百度百科

参考教程: [视频教程](https://www.bilibili.com/video/av65336062?from=search&seid=4753922999762898690)  / [文字教程](https://301technology.cn/2019/08/03/picgojsdelivrgithub/)

条件就是你得拥有一个github账号, 下载一个PicGo的软件(mac还是win系统都支持)

---华丽的分割线---留存, 换行`784(8-26*0f9f16*bfdaaf~2e90b-193f)240-9709ffff0~5`---华丽的分割线---

#### Github配置
见上方参考教程.

#### jsDelivr配置
jsDelivr由于和PicGo搭配使用, 无需额外配置

#### PicGo配置说明
* 设定仓库名：按照【用户名 / 图床仓库名】的格式填写
* 设定分支名：【master】
* 设定Token：粘贴之前生成的【Token】
* 指定存储路径：填写想要储存的路径，如【images/】，这样就会在仓库下创建一个名为 images 的文件夹，图片将会储存在此文件夹中
* 设定自定义域名：它的的作用是，在图片上传后，PicGo会按照【自定义域名+上传的图片名】的方式生成访问链接，放到粘贴板上，因为我们要使用jsDelivr加速访问，所以可以设置为【https://cdn.jsdelivr.net/gh/用户名/图床仓库名 】
`jsDelivr参考格式: The URL structure is /gh/user/repo@version/file.js
`

最终成品的地址如下, 图片是我通过PicGo上传的, yml则是我直接通过github网页上传的, 都能完美预览和下载.
```
https://cdn.jsdelivr.net/gh/acc8226/JsDelivrCDN/img/20191117181015.png

https://cdn.jsdelivr.net/gh/acc8226/JsDelivrCDN/img/20191117180214.jpg

https://cdn.jsdelivr.net/gh/acc8226/JsDelivrCDN/img/latest-mac.yml

https://cdn.jsdelivr.net/gh/acc8226/JsDelivrCDN/.travis.yml
```

#### PicGo mac版的自定义配置
![](https://upload-images.jianshu.io/upload_images/1662509-63eb930b124b85ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)对于追求[效率](https://www.iplaysoft.com/tag/%E6%95%88%E7%8E%87)的键盘党而言，你还可以使用键盘快捷键 `CTRL+SHIFT+P` (Win / Linux) 或者 `Command+SHIFT+P` (macOS) 来快速上传剪贴板里的 (第一张) 图片。

#### 国内如何下载 GitHub release 中的内容？
> 作者：dwing
> 链接：https://www.zhihu.com/question/48480151/answer/803199369
> 来源：知乎
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
> 
> release中的下载链接虽然是[http://github.com](https://link.zhihu.com/?target=http%3A//github.com)开头,但会跳转到*.[s3.amazonaws.com](https://link.zhihu.com/?target=https%3A//github-production-release-asset-2e65be.s3.amazonaws.com/7190986/d5bdc4c4-93b1-11e7-918b-63a983282388%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Credential%3DAKIAIWNJYAX4CSVEH53A%252F20170914%252Fus-east-1%252Fs3%252Faws4_request%26X-Amz-Date%3D20170914T170257Z%26X-Amz-Expires%3D300%26X-Amz-Signature%3Db375ba0ecc76ed7a6fc8f732cefbe9caff49226fda3f54e109e9a79a94673d66%26X-Amz-SignedHeaders%3Dhost%26actor_id%3D0%26response-content-disposition%3Dattachment%253B%2520filename%253Dshadowsocks-nightly-4.2.5.apk%26response-content-type%3Dapplication%252Fvnd.android.package-archive)这个域名, 后面带了很长的参数, 貌似是一次性的只能临时下载用, 很快就会失效, 然后只能从github.com开头的地址重新跳转取得新的实际下载链接.
> 
> 至于release的下载速度, 最快只有几十KB/s, 慢的时候可能掉到十几K甚至几K. 如果把跳转后的真实下载链接中的https手动改为http开头, 则下载速度会提高到几百K甚至更高. 怀疑是https有墙在阻碍.
> 
> 然而, release下载的稳定性并不好, 如果下载文件很大, 很容易在中途中断(http方式下载还经常在99%的进度中断), 然后有的下载工具还续不上

目前找到比较好的方式是用 **Free Download Manager** 直接下载[http://github.com](https://link.zhihu.com/?target=http%3A//github.com)开头的**原链接**, 可以自动跳转并多线程下载. 如果中途中断, 可在右键菜单里选择"更改URL"然后之间点确定就会重新跳转新的临时下载地址并续传.

## 总结
本来想着那个购买的域名大做文章, 发现好用自在身边. 感谢PicGo的作者, 感谢jsdelivr提供的cdn服务, 感谢所有!

## 相关下载
Github官网
https://github.com/

PigGo
https://github.com/Molunerfinn/PicGo/releases

## 参考
[活动作品](https://www.bilibili.com/blackboard/activity-newstar4.html?msource=caitiao "叮！你的笔记本电脑和季度大会员等待领取中！")关于博客的最稳定的图床方案
https://www.bilibili.com/video/av65336062?from=search&seid=4753922999762898690

目前最稳定的免费图床方案 - 301技术-HuanHao
https://301technology.cn/2019/08/03/picgojsdelivrgithub/

Github+jsDelivr+PicGo 打造稳定快速、高效免费图床
https://blog.csdn.net/qq_36759224/article/details/98058240

PicGo - 免费开源的图片上传与管理工具 (Markdown写作贴图 / 跨平台图床应用)
https://www.iplaysoft.com/picgo.html