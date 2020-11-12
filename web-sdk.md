

# Web-SDK引入

1、SDK下载地址: [web-sdk.js](https://log.haitunshenghuo.com)

2、在Vue工程的main.js中完成SDK挂载
```JavaScript
  import Vue from 'vue';
  import VueClearBug from './views/app/vue-clear-bug-sdk';
  ...
  ...
  Vue.use(VueClearBug)
```

3、接下来就可以在vue项目的任意组件中访问到VueClearBug的实例： **clearBug**

>例如： this.$clearBug.xxxx

# SDK实例内置方法
> SDK需要初始化之后才能开始工作<br>

1、初始化SDK init()

在App.vue中
```JavaScript
export default {
  name: 'App',
  created() {
    this.$clearBug.init({
      appKey: "你创建好应用的appKey",
      appSecret: "该app对应的密钥"
    });
  }
}
```

2、异常上报 errorLog()
>该方法由你自己业务需要决定，例如：

```JavaScript
try{
  //你需要处理的业务逻辑
}catch(e){
  
}
```