关于spy-debugger
==========
一站式页面调试、抓包工具。远程调试任何手机浏览器页面，任何手机移动端webview（如：微信，HybirdApp等）HTTP/HTTPS  

[![npm](https://img.shields.io/npm/v/spy-debugger.svg)](https://www.npmjs.com/package/spy-debugger)
[![npm](https://img.shields.io/npm/dt/spy-debugger.svg)](https://www.npmjs.com/package/spy-debugger)
[![Build Status](https://travis-ci.org/wuchangming/spy-debugger.svg?branch=master)](https://travis-ci.org/wuchangming/spy-debugger)  

Language: [English](README_EN.md)

特性
------------
1、页面调试＋抓包  
2、[操作简单](#三分钟上手)   
3、**支持HTTPS**。  
4、`spy-debugger`内部集成了[`weinre`](http://people.apache.org/~pmuellr/weinre/docs/latest/)、[`node-mitmproxy`](https://github.com/wuchangming/node-mitmproxy)、[`AnyProxy`](https://github.com/alibaba/anyproxy)。  
5、自动忽略原生App发起的https请求，只拦截webview发起的https请求。对使用了SSL pinning技术的原生App不造成任何影响。  
6、可以配合其它代理工具一起使用(默认使用AnyProxy) [(设置外部代理)](#设置外部代理默认使用anyproxy)  


Demo
------------
#### 调试页面
<img src="demo/img/demo.png" width="650px" />

#### 抓包
<img src="demo/img/AnyProxy.jpg" width="650px" />

安装
------------
Windows 下
```
    npm install spy-debugger -g
```

Mac 下
```
    sudo npm install spy-debugger -g
```

## 三分钟上手

第一步：手机和PC保持在同一网络下（比如同时连到一个Wi-Fi下）

第二步：命令行输入`spy-debugger`，按命令行提示用浏览器打开相应地址。

第三步：设置手机的HTTP代理，代理IP地址设置为PC的IP地址，端口为`spy-debugger`的启动端口(默认端口：9888)。

第四步：安装证书。**注：手机必须先设置完代理后再通过(非微信)手机浏览器访问`http://spydebugger.com/cert`[`(地址二维码)`](demo/img/QRCodeForCert.png)安装证书**（手机首次调试需要安装证书，已安装了证书的手机无需重复安装)。

第五步：用手机浏览器访问你要调试的页面即可。

自定义选项
------------
#### 端口
(默认端口：9888)
```
spy-debugger -p 8888
```

#### 设置外部代理（默认使用AnyProxy）
```
spy-debugger -e http://127.0.0.1:8888
```
spy-debugger内置AnyProxy提供抓包功能，但是也可通过设置外部代理和其它抓包代理工具一起使用，如：Charles、Fiddler。

#### 是否让weinre监控iframe加载的页面
(默认： false)
```
spy-debugger -i true
```

#### 是否只拦截浏览器发起的https请求
(默认： true)
```
spy-debugger -b false
```
有些浏览器发出的connect请求没有正确的携带userAgent，这个判断有时候会出错，如**UC浏览器**。这个时候需要设置为false。大多数情况建议启用默认配置：true，由于目前大量App应用自身（非WebView）发出的请求会使用到SSL pinning技术，自定义的证书将不能通过app的证书校验。

#### 是否允许HTTP缓存
(默认： false)
```
spy-debugger -c true
```

更多
------------
`spy-debugger`原理是集成了`weinre`，简化了`weinre`需要给每个调试的页面添加js代码。`spy-debugger`原理是拦截所有html页面请求注入`weinre`所需要的js代码。让页面调试更加方便。
