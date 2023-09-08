<script setup>
import { onMounted, ref } from 'vue'
import { proxy, hook } from 'ajax-hook'

const url = 'https://mcs.snssdk.com/list'

proxy({
  // 请求发起前进入
  onRequest: (config, handler) => {
    // 可以对请求数据做点什么
    console.log('request success', config)
    if (config.url == url) {
      config.headers['content-type'] = 'text/text'
    }
    handler.next(config)
  },
  // 请求成功后进入
  onResponse: (response, handler) => {
    // 可以对响应数据做点什么
    console.log('response success', response)
    handler.next(response)
  },
  // 请求错误进入
  onError: (err, handler) => {
    // 可以统一处理错误
    console.log('request error', err)
    handler.next(err)
  },
})

// const { unHook, originXhr } = hook({
//   //拦截回调
//   onreadystatechange: function (xhr, event) {
//     console.log('onreadystatechange called: %O')
//     //返回false表示不阻断，拦截函数执行完后会接着执行真正的xhr.onreadystatechange回调.
//     //返回true则表示阻断，拦截函数执行完后将不会执行xhr.onreadystatechange.
//     return false
//   },
//   onload: function (xhr, event) {
//     // this 为代理xhr对象
//     // 原生xhr对象扩展了一个`getProxy()`方法，调用它可以获取代理xhr对象
//     // this == xhr.getProxy() //true
//     // //可以通过代理xhr对象的`xhr`属性获取原生xhr对象
//     // this.xhr == xhr //true
//     console.log('onload called')
//     return false
//   },
//   //拦截方法
//   open: function (args, xhr) {
//     console.log('open called: method:%s,url:%s,async:%s', args[0], args[1], args[2])
//     //拦截方法的返回值含义同拦截回调的返回值
//     return false
//   },
// })
</script>

<template></template>

<style lang="scss"></style>
