

# vue-clear-bug
- [x] vue > 2.x.x
- [x] node > 9.x
## 快速开始

### 引入SDK
- 1、SDK下载地址: [web-sdk.js](https://log.haitunshenghuo.com/vue-clear-bug.min.js.zip)

- 2、在你的Vue工程的main.js中完成SDK挂载
>代码示例
```JavaScript
  import Vue from 'vue';
  import VueClearBug from './views/app/vue-clear-bug-sdk';
  ...
  ...
  Vue.use(VueClearBug)
```

- 3、接下来就可以在vue项目的任意组件中访问到VueClearBug的实例： **clearBug**

>例如： this.$clearBug.xxxx

### SDK实例暴露的方法

#### 启用SDK init({appKey, appSecret})
- `appKey` {String} 你创建好应用的appKey
- `appSecret` {String} 该app对应的密钥
- returns void
> 代码示例 - App.vue *（推荐在App.vue中完成初始化）*
```JavaScript
export default {
  name: 'App',
  created() {
    this.$clearBug.init({
      appKey: "*************",
      appSecret: "**************"
    });
  }
}
```

#### 异常上报 errorLog({err,tag})
- `err` {String} 异常信息
- `tag` {String} 你给当前异常场景取得别名（非必填）
- returns void <br/>
*系统会默认收集并聚合error_tag,并在管理后台呈现，未填写具名tag的errorlog将会被统一具名tag: `other`*<br/>
*SDK不采集用户数据，所有身份识别由SDK内部专门针对用户设备生成UUID指纹信息来跟踪分析用户行为。*<br/>
> 该方法由你自己业务需要决定，例如：

```JavaScript
try{
  //你需要处理的业务逻辑，例如首页商品数据加载
}catch(e){
  //捕获到异常之后调用errorLog方法
  errorLog({
      err: e,
      tag: '首页商品数据加载'
  })
}
```

### SDK实例内部方法

#### 全局异常收集
- SDK会全局捕获应用内未被开发着拦截的错误/异常，并自动上报，聚合错误类型。但tag将会被标记为`other`

#### 用户下线事件上报 + 引用释放
- SDK会在应用程序生命周期结束时自动释放所有引用与事件句柄，无需开发者手动释放。
- SDK会在用户关闭应用程序/网页时上报最后一次离线事件，开发者可在后台中查看用户活跃数据。