# ACL4SSR Mannix 订阅转换极速版

用于在 Clash(Meta/mihomo)、Clash proxies、base64 和 uri 订阅格式之间进行快速转换，纯 TypeScript 实现，最大化转换速度

emoji、代理策略组和路由规则与 [ACL4SSR_Online_Full_Mannix.ini](https://github.com/zsokami/ACL4SSR) 大致相同，url-test 间隔时间改为随节点数变化，最少 15 秒

## 远程转换

[配套 Web 前端](https://github.com/zsokami/scweb)

用法

```
https://arx.cc[/!<args>]/<from>
```

`<args>`

参数列表，格式：`key=value&key2=value2...`

| 参数 | 默认 | 说明 |
| - | - | - |
| to | clash | 目标订阅类型，支持 clash、clash-proxies、base64、uri 或 auto(Clash 客户端则 clash 否则 base64)，该参数可省略 `to=` 前缀 |
| filename | 无 | 文件名 |

`<from>`

http/s 订阅链接或用 base64/base64url 编码的订阅内容

可以是除 http/s 代理的 uri，但需 URL 编码

多个先用 | 分隔，然后再 URL 编码

获取零节点订阅用 empty，可用于去广告

例子

```
https://arx.cc/https://example.com/subscribe?token=xxx
```
```
https://arx.cc/!auto/https://example.com/subscribe?token=xxx
```

## 本地转换

### 本地服务

需先安装 [Deno](https://deno.com/)

运行

```sh
deno run -A https://raw.githubusercontent.com/zsokami/cvt/main/scripts/server.ts
```

指定端口

```sh
deno run -A https://raw.githubusercontent.com/zsokami/cvt/main/scripts/server.ts 8000
```

指定主机名/IP:端口

```sh
deno run -A https://raw.githubusercontent.com/zsokami/cvt/main/scripts/server.ts [::1]:8000
```

更新版本并运行

```sh
deno run -A -r https://raw.githubusercontent.com/zsokami/cvt/main/scripts/server.ts
```

查看版本

```
http://127.0.0.1:8000/version
```

### 命令行

需先安装 [Deno](https://deno.com/)

用法

```sh
deno run -A https://raw.githubusercontent.com/zsokami/cvt/main/scripts/cvt.ts [-o <path>] [<from>] [<to>] [<ua>]
```

参数

- `-o <path>` 输出路径

- `<from>` http/s 订阅链接、除 http/s 代理的 uri 或用 base64/base64url 编码的订阅内容，多个用 | 分隔。获取零节点订阅用 empty，可用于去广告

- `<to>` clash、clash-proxies、base64、uri 或 auto(若 ua 含 clash 则 clash 否则 base64)

- `<ua>` User-Agent 请求头

例子

```sh
deno run -A https://raw.githubusercontent.com/zsokami/cvt/main/scripts/cvt.ts -o clash.yaml 'https://example.com/subscribe?token=xxx'
```
