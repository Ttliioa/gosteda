## 一键部署 Gost(ss+mws) 到 heroku  [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/Ttliioa/gosteda)

> 1. 服务端部署后，view查看，显示`404 page not found`，表示部署成功。

> 2. 客户端本地代理，直接运行以下命令，本地开放端口1080，默认支持socks协议。
> ```
>    gost.exe -L=:1080 -F=ss+mwss://method:password@appname.herokuapp.com:443
> ```

> 3. 客户端[下载](https://github.com/ginuerzh/gost/releases/tag/v2.11.0)
 
> 4.  技术文档[站点](https://docs.ginuerzh.xyz/gost/)

> 5. 可通过cloudflare pages中转流量：
新建 一个 _worker.js 文件，内容如下，替换 xxx.herokuapp.com为自己的应用。
```_worker.js
export default {
  async fetch(request, env) {
    let url = new URL(request.url);
    if (url.pathname.startsWith('/')) {
      url.hostname = 'xxx.herokuapp.com'
      let new_request = new Request(url, request);
      return fetch(new_request);
    }
    return env.ASSETS.fetch(request);
  },
};
```
在 cloudflare 中 选择 Pages ,点击 ，建立专案  选择 直接上传 上传_worker.js文件 

部署网站后。xxxxx.pages.dev  就是 pages 的代理。

### 参考 
*https://github.com/ginuerzh/gost*

*https://github.com/gfwlist/gfwlist*

*https://github.com/xausky/ShadowsocksGostPlugin*
