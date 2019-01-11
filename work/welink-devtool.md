# H5本地调试工具

## 什么是 H5 本地调试工具？

在开发阶段通过 PC 浏览器来调试设备（虚拟设备、真实设备）的一款工具。

- 虚拟设备：是指京东 IoT 平台模拟出来的设备。
- 真实设备：是指正在开发或已开发完成的设备比如开发板、空调、插座等。

## 如何使用？

### 安装 nodejs
 
根据操作系统[下载](http://nodejs.cn/download/)对应的 nodejs 安装包。

### 环境依赖

nodejs 版本大于等于 8。


### 安装 H5 本地调试工具

```
npm install welink-devtool -g
```

### 开发项目的目录结构示例

```
  │-welink
  ├── project
  │   ├── css
  │   │   └── style.css
  │   ├── index.html
  │   └── js
  │       └── app.js
  └── welinkconfig.json
```

### welinkconfig.json

在开发目录中新建一个 `welinkconfig.json` 文件

```
 {
   jd.nsng.smart.url": "https://sbappgw.jd.com",
   "authenticationTokenKey": "0882741796_91900007_150149604599245054_c0b963d6",
   "staticPath": "project"
 }
```

- `jd.nsng.smart.url` 可以配置沙箱或线上地址，默认沙箱地址。

- `authenticationTokenKey` 需要在微联开发者中心获得（必填）。

- `staticPath` 要调试的HTML5项目目录（必填）。



#### jd.nsng.smart.url

- 沙箱：https://sbappgw.jd.com
- 线上：https://gw.smart.jd.com

#### authenticationTokenKey

`authenticationTokenKey` 是 H5 本地调试工具的令牌。

**虚拟设备或真实设备通过小京鱼 APP 绑定到开发者账号下**才会生成 `authenticationTokenKey`。

#### 如何找到 authenticationTokenKey ?

1. [登录](http://smartdev.jd.com)到小京鱼服务平台
![login](https://user-images.githubusercontent.com/25784101/51011113-231ca880-1592-11e9-846f-a9655b6b1f3e.png)

2. 进入控制台
![console](https://user-images.githubusercontent.com/25784101/51011160-5fe89f80-1592-11e9-8fb2-05cecac03f29.png)

3. 产品联调
![join](https://user-images.githubusercontent.com/25784101/51011815-f9b14c00-1594-11e9-9f54-16200ded2987.png)

**备注：`authenticationTokenKey` 有效期 24 小时，如果失效，需要从新登陆小京鱼服务平台获取。** 

#### 页面中引用 H5 调试工具的 SDK

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>demo</title>
    <!--引入调试工具的 SDK-->
    <script src="https://unpkg.com/welink-devtool-sdk@1.0.15/dist/index.js"></script>
    <!--注释掉线上使用的 SDK-->
    <!--<script src="https://static.360buyimg.com/smart/jdsmart-1.0.3.js"></script>-->
</head>
<body>
    
</body>
</html>
```

**备注：在引入调试工具 SDK 的时候 一定要注释掉线上使用的 SDK。**

#### 启动调试工具

```
cd welink
welink-devtool
```

#### 打开前端页面

浏览器输入：http://localhost:3000/project/index.html

**备注：`http://localhost:3000/project/index.html` 中的 project 是 welinkconfig.json 文件中设置的 staticPath 的值**

### vue 开发者

我们提供了 **[vue-stone](https://jd-smart-fe.github.io/vue-stone/#/) 组件库** 和 **vue 工程化开发模板**。

#### 什么是 vue 工程化开发模板？

基于 vue-cli 2.0 模板进行修改使其支持本地化调试工具（welink-devtool）同时支持 webpack 相关特性（如：热重载）。

#### 如何使用 vue 工程化开发模板?

全局安装 `welink-cli`

```
npm install welink-cli -g
```

通过 `welink init` 命令下载模板

```
welink init demo
```
![init demo](https://user-images.githubusercontent.com/25784101/51019633-97694300-15b6-11e9-93fb-b8a331186bdd.png)

#### 安装依赖

```
npm install 
```

#### 设置 `authenticationTokenKey`

在 demo 文件夹中找到 `welinkconfig.json` 设置 `authenticationTokenKey`（获取方式同上）

#### dev
自动引入调试环境的 SDK
```
npm run dev
```

#### build

自动引用线上的 SDK

```
npm run build
```

### 常见问题

- 为什么设置 `authenticationTokenKey` 还是控制不了设备？

  1. 请检查设备是否绑定到了**登录的开发者平台的账号**下

  2. `authenticationTokenKey` 是否失效



