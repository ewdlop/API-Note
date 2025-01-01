### 中文 (Chinese)
Axios 是一个流行的 JavaScript 库，用于发送 HTTP 请求。它支持 Promise，使得处理异步操作更加方便。Axios 可以在 Node.js 和浏览器环境中使用，常用于与 REST API 交互。

---

### 安装 Axios

```bash
# 使用 npm
npm install axios

# 使用 yarn
yarn add axios
```

---

### 基本用法

#### 发送 GET 请求

```javascript
const axios = require('axios');

axios.get('https://api.example.com/data')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('获取数据时出错:', error);
  });
```

#### 发送 POST 请求

```javascript
axios.post('https://api.example.com/data', {
  name: '张三',
  age: 25
})
  .then(response => {
    console.log('成功发送数据:', response.data);
  })
  .catch(error => {
    console.error('发送数据时出错:', error);
  });
```

#### 使用 `async/await`

```javascript
const fetchData = async () => {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error('获取数据时出错:', error);
  }
};

fetchData();
```

---

### 配置 Axios

#### 全局配置

```javascript
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = 'Bearer YOUR_TOKEN';
axios.defaults.timeout = 10000; // 10秒
```

#### 每次请求配置

```javascript
axios.get('/data', {
  params: { id: 123 },
  headers: { 'Custom-Header': 'CustomValue' }
})
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('出错:', error);
  });
```

---

### 拦截器 (Interceptors)

拦截请求或响应以进行日志记录、修改或全局错误处理。

#### 请求拦截器

```javascript
axios.interceptors.request.use(config => {
  console.log('请求发送时间:', new Date());
  return config;
}, error => {
  return Promise.reject(error);
});
```

#### 响应拦截器

```javascript
axios.interceptors.response.use(response => {
  console.log('接收到响应:', response.data);
  return response;
}, error => {
  console.error('响应错误:', error);
  return Promise.reject(error);
});
```

---

### 取消请求

```javascript
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('/long-request', {
  cancelToken: source.token
}).catch(thrown => {
  if (axios.isCancel(thrown)) {
    console.log('请求已取消', thrown.message);
  } else {
    console.error('其他错误:', thrown);
  }
});

// 取消请求
source.cancel('操作被用户取消。');
```

---

### 总结

Axios 是一个功能强大且灵活的 HTTP 请求库。无论是在浏览器还是 Node.js 中，它都可以简化 GET、POST 等 HTTP 请求，同时提供拦截器、请求取消等高级功能，适合更复杂的工作流。

---

如果需要更多语言的翻译或改编，请告诉我！
