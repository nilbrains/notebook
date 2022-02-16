# Axios安装与封装

## 起步

安装使用  [Axios 中文文档 (axios-http.cn)](https://www.axios-http.cn/docs/intro)

**使用命令行安装`axios`**

```bash
npm install axios -S
```



## `vue`项目中封装使用

### request.js

文件夹: `/src/plugins`

```javascript
import axios from "axios";
import { ElNotification } from "element-plus";

// 创建axios实例
const service = axios.create({
  baseURL: "https://data.nilbrains.com", // api 的 base_url
  timeout: 5000, // 请求超时时间
  withCredentials: true, // 是否携带cookie?
});

// request拦截器
service.interceptors.request.use(
  (config) => {
  	// 自定义 请求 header 内容 
    config.headers["token"]  =  "123456789"
    return config;
  },
  (error) => {
    Promise.reject(error);
  }
);

// response 拦截器
service.interceptors.response.use(
  (response) => {
    // 返回信息
    return response.data;
  },
  (error) => {
    let code = 0;
    try {
      code = error.response.data.status;
    } catch (e) {
      if (error.toString().indexOf("Error: timeout") !== -1) {
        ElNotification({
          title: "Error",
          message: "网络请求超时",
          type: "error",
        });
        return Promise.reject(error);
      }
    }
    console.log("req err code == > ", code);
    if (code) {
      // TODO: 可以 根据不同的code 弹出 不同的提示
    } else {
        ElNotification({
          title: "Error",
          message: "接口请求失败",
          type: "error",
        });
    }
    return Promise.reject(error);
  }
);
export default service;

```

`ElNotification` 使用需先安装 `element-ui`或者`element-plus`

### api.js

```javascript
import request from "@/plugins/request";

/**
 * API_GET
 * @param {string} url 路由
 * @param {object} data 参数
 * @returns {import('axios').AxiosPromise<any>} 返回
 */
export function API_GET(url, data = {}) {
  return request({
    url,
    method: "GET",
    params: data,
  });
}

/**
 * API_POST
 * @param {string} url 路由
 * @param {object} data 参数
 * @returns {import('axios').AxiosPromise<any>} 返回
 */
export function API_POST(url, data = {}) {
  return request({
    url,
    method: "POST",
    data,
  });
}

/**
 * API_PUT
 * @param {string} url 路由
 * @param {object} data 参数
 * @returns {import('axios').AxiosPromise<any>} 返回
 */
export function API_PUT(url, data = {}) {
  return request({
    url,
    method: "PUT",
    data,
  });
}

/**
 * API_DELETE
 * @param {string} url 路由
 * @param {object} data 参数
 * @returns {import('axios').AxiosPromise<any>} 返回
 */
export function API_DELETE(url, data = {}) {
  return request({
    url,
    method: "DELETE",
    data,
  });
}
```

### js 自定义 `axios` 返回类型

创建一个新的文件夹 types 

1. 创建js文件 `axios.d.ts`

```javascript
import axios from "axios";

declare module "axios" {
  interface IAxios<D = null> {
    success?: boolean;
    message?: string;
    data?: D;
    code?: number;
    timestamp?: number
  }
  export interface AxiosResponse<T = any> extends IAxios<D> {}
}
```

2. 修改 jsconfig.json

```json
{
    ....,
    "compilerOptions": {
    	"typeRoots": ["./node_modules/@types", "./src/types/"],
    }
}
```