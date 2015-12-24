#Zendesk 的介绍和使用
###介绍
Zendesk 是比较有名的客户支持服务提供商，而且是云服务提供商，也就是说购买了 Zendesk 的服务后，数据也是委托在 Zendesk 的服务器上的。
提供了多种客户支持的渠道，即 channel，如果 email， 电话，Twitter，Facebook， web widget，Android SDK， iOS SDK。而且根据订阅的不同 plan 可以使用的 feature 也是不同的。好像在2015年11月修改了他们的四个不同的 level 的服务。如果是购买的是 Enterprise 的 plan 就可以支持多个品牌的 support。因为一个公司可能有多个产品，每个产品对应的 help center 是不同的。这时候就需要support multibrand 了。可以参考这个链接 [Configuring your channels to support multiple brands (Professional Add-on and Enterprise)](https://support.zendesk.com/hc/en-us/articles/204577963-Configuring-your-channels-to-support-multiple-brands-Professional-Add-on-and-Enterprise-)

###使用
集成 Mobile SDK 是很方便的，如果是 iOS 的集成可以直接通过 cocoapods 的方式，也可以手动导入 Zendesk 的 framework 和 bundle 就可以了。托管在 github 上。导入framework 后，进入管理员后台，找到 mobile sdk， add app，填写 app name后，就会生成一段代码，直接将代码 copy 到需要使用 Zendesk 服务的 viewController 就可以完成 Zendesk 的初始话工作了。可以参考 Zendesk 的 Docs 都有很详细的使用说明 [Mobile SDK tutorial - Part 1: Getting started with the SDK](https://support.zendesk.com/hc/en-us/articles/205500817-Mobile-SDK-tutorial-Part-1-Getting-started-with-the-SDK)

Tips:
1. 验证方式有两种，Anonymous 和 JSON web token，两种方式各有利弊，根据自己的需求去选择。
2. 如果在管理员后台修改了 app configuration 后，需要1个小时后才会生效。如果想马上生效，记得在真机或者模拟器上卸载改 app，重新安装。