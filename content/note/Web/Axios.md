---
title: Axios笔记
tags:
  - Note
  - Web
  - Axios
date: 2024-03-21
description: 含有Axios的语法
slug: axios-note
---

# Axios 的特点

它本身具备以下作用：

1. 可以从浏览器中创建 XMLHttpRequest。
2. 能从 Node.js 创建 HTTP 请求。
3. 支持 Promise API。
4. 能够拦截请求和响应。
5. 可以转换请求和响应数据。
6. 也可取消请求。
7. 可以自动转换 JSON 数据。
8. 在客户端支持防止  [CSRF/XSRF](https://baike.baidu.com/item/%E8%B7%A8%E7%AB%99%E8%AF%B7%E6%B1%82%E4%BC%AA%E9%80%A0/13777878?fromtitle=CSRF&fromid=2735433&fr=aladdin)  攻击。

# 使用方式

## 执行  `get`  数据请求

```js
axios.get('url',{
  params:{
    id:'接口配置参数（相当于url?id=xxxx）'，
  },
}).then(function(res){
  console.log(res); // 处理成功的函数 相当于 success
}).catch(function(error){
  console.log(error) // 错误处理 相当于 error
})
```

## 执行  `post`  数据请求

```js
axios
  .post(
    "url",
    { data: {} },
    {
      headers: "xxxx", // 头部配置
    }
  )
  .then(function (res) {
    console.log(res); // 处理成功的函数 相当于 success
  })
  .catch(function (error) {
    console.log(error); // 错误处理 相当于 error
  });
```

## 通用请求

- `method`: 指定请求方法，例如 `get`, `post`, `put`, `delete` 等。
- `url`属性用于指定请求的目标地址
- `params` 设置 URL 查询参数（GET 请求中的参数）。
- `data` 设置请求主体的数据（例如用于 POST 请求）。
- `headers` 设置 HTTP 请求的头部信息
- `cache` 控制请求的缓存行为
- `timeout`: 设置请求超时时间，单位是毫秒

```js
//-------------------get-----------------------//
axios({
  method: "get",
  url: "xxx",
  cache: false,
  params: {
    id: 123,
  },
  headers: "xxx",
});
//-------------------post-----------------------//
axios({
  method: "post",
  url: "xxx",
  data: {
    firstName: "Tom",
    lastName: "Sun",
  },
});
```
