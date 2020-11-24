

# taro-clear-bug
- [x] wx > 2.x.x
- [x] Taro > 2.1.x
- [x] node > 9.x
## 快速开始

### 引入SDK
- 1、SDK下载地址: [clear-bug-miniprogram.js](https://log.haitunshenghuo.com/clear-bug-miniprogram.min.js.zip)

- 2、在你的Taro小程序工程的App.jsx中引入SDK
>代码示例
```JavaScript
  import React from 'react';
  import { Component } from 'react';
  ...
  var clearbug = require('./utils/clear-bug-miniprogram.js')

```

### SDK实例暴露的方法

#### 启用SDK init({appKey, appSecret})
- `appKey` {String} 你创建好应用的appKey
- `appSecret` {String} 该app对应的密钥
- `appVersion` {String} 应用当前版本名 *（可选，若不传，默认为1.0.0）*
- `config: {logLever: 0 | 1}` {object} SDK 配置 *（可选，logLever = 0 时禁用SDK控制台输出）*
- returns void
> 代码示例 - App.jsx *（推荐在App.jsx中完成初始化）*
```JavaScript
  import React from 'react';
  import { Component } from 'react';
  ...
  var clearbug = require('./您的路径/clear-bug-miniprogram.js')

  clearbug.init({
   appKey: '*********',
   appSecret: '**********',
   appVersion: '1.0.2'
  })

  class App extends Component ...
```
>初始化成功后，控制台会有相应提示，此时你就可以使用 **global.clearbug** 访问SDK实例

#### 异常上报 errorLog({error,tagName})
- `error` {String} 异常信息
- `tagName` {String} 你给当前异常场景取得别名（非必填）
- returns void <br/>
*系统会默认收集并聚合error_tag,并在管理后台呈现，未填写具名tag的errorlog将会被统一具名tag: `other`*<br/>
*SDK不采集用户数据，所有身份识别由SDK内部专门针对用户设备生成UUID指纹信息来跟踪分析用户行为。*<br/>
> 该方法由你自己业务需要决定，例如：

```JavaScript
try{
  //你需要处理的业务逻辑，例如首页商品数据加载
}catch(e){
  //捕获到异常之后调用errorLog方法
  global.clearbug.errorLog({
      error: e,
      tagName: '首页商品数据加载',
  })
}
```

### SDK实例内部方法

#### 全局异常收集
- SDK会全局捕获应用内未被开发着拦截的错误/异常，并自动上报，聚合错误类型。但tag将会被标记为`other`

#### 用户下线事件上报 + 引用释放
- SDK会在应用程序生命周期结束时自动释放所有引用与事件句柄，无需开发者手动释放。
- SDK会在用户关闭应用程序/网页时上报最后一次离线事件，开发者可在后台中查看用户活跃数据。