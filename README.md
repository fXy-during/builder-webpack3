# builder-webpack


[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/iv-web/feflow/blob/master/LICENSE)
[![npm package](https://img.shields.io/npm/v/builder-webpack3.svg?style=flat-square)](https://www.npmjs.org/package/builder-webpack3)
[![NPM downloads](http://img.shields.io/npm/dt/builder-webpack3.svg?style=flat-square)](https://npmjs.org/package/builder-webpack3)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/cpselvis/builder-webpack3/pulls)

Webpack 构建器, 适用于NOW直播业务和活动类型的项目构建

## 特性

- 对H5开发友好，默认集成 Rem 方案，解决适配问题
- 支持 SCSS 和 JS 模块 import 时的绝对路径写法
- 支持多页面打包的开发方式
- 支持 FIS3 的 html 文件 inline 语法糖
- 支持雪碧图(图片后缀加__sprite)
- 使用Happypack 多实例构建，飞一般的构建速度

## 安装

确保feflow的版本在 v0.12.0 以上, 可以通过如下命令安装最新feflow版本
```
$ npm install feflow-cli -g
```

## 快速使用

### 添加feflow.json配置文件

在项目根目录添加 `feflow.json` 配置文件

``` sh
{
    "builderType": "builder-webpack3",
    "builderOptions": {
        "product": "now",                                    // 产品，此处可以是 now 或者 shangfen
        "domain": "now.qq.com",                              // 域名，离线包的域名需要使用
        "cdn": "11.url.cn",                                  // 资源发布到的cdn名称
        "moduleName": "mobile",                              // 部署的模块
        "bizName": "category",                               // 业务名称
        "minifyHTML": true,                                  // 是否压缩 html
        "minifyCSS": true,                                   // 是否压缩 js
        "minifyJS": true,                                    // 是否压缩 css
        "inlineCSS": true,                                   // 生成的 css 是否内联到首屏
        "usePx2rem": true,                                   // 是否使用 Rem
        "useReact": true,                                    // 是否是 React，如果为false，则不会在 html 中引用 React 框架 
        "remUnit": 37.5,                                     // Rem 单位，对于 375 视觉稿，此处填写 37.5，750视觉稿需要改成 75 
        "remPrecision": 8,                                   // Rem 的精度，即 px 转换成了 rem 后的小数点后位数
        "inject": true,                                      // 打包生成的 js 文件是否自动注入到 html 文件 body 之后
        "port": 8001,                                        // 本地开发的 webpack 构建服务进程端口号
        "externals": [                                       // 基础框架不打入到 bundle 里面
            {
                "module": "react",
                "entry": "//11.url.cn/now/lib/16.2.0/react.min.js?_bid=3123",
                "global": "React"
            },
            {
                "module": "react-dom",
                "entry": "//11.url.cn/now/lib/16.2.0/react-dom.min.js?_bid=3123",
                "global": "ReactDOM"
            }
        ]
    }
}
```

### 命令

```sh
$ feflow dev      # 本地开发时的命令
$ feflow build    # 发布时的打包命令, 打出的包在工程的public目录, 包含 cdn, webserver 和 offline 三个文件夹
```

## 文档

### 内联

同时支持Fis3项目的inline语法糖写法和ejs的写法

- 内联 html:

``` sh
<!--inline[/assets/inline/meta.html]-->
```

- 内联 javascript

``` sh
<script src="@tencent/report-whitelist?__inline"></script>
```

备注：如果希望内联某个 JS 文件，需要使用相对路径的写法。

### 代理设置

- 执行 `feflow dev` 命令后会在本地的 8001 端口开启一个 WDS 服务，所有的静态资源(html, css, js, img) 都会在内存里面。可以通过 http://127.0.0.1:8001/webpack-dev-server  查看

![](https://qpic.url.cn/feeds_pic/ajNVdqHZLLDpvNiayyEbzqB9V61CRiallnRdEKFaViaxw7pibicBKgEI8vw/)

- Fiddler配置把之前的本地绝对路径改成 本地server 路径即可：

![](https://qpic.url.cn/feeds_pic/Q3auHgzwzM72dIPZyXSdy8srwzIOTovf0VSaNlBzE98ueBiaibIVSHkA/)

## 版本日志

[版本日志](CHANGELOG.md)

## 许可证

[MIT](https://tldrlegal.com/license/mit-license)
