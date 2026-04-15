# Clash Verge Rev 全局脚本 懒人配置 / Mihomo Party 覆写脚本

项目地址：<https://github.com/kongbaitt/YaNet/tree/main/Mihomo>

## Mihomo Party 订阅链接

<https://fastly.jsdelivr.net/gh/kongbaitt/YaNet@main/Mihomo/global_script.js>

- 本脚本包含 DNS 设置，在 Mihomo Party 里使用可以尝试在`应用设置`里关闭`接管DNS设置`和`接管域名嗅探设置`
- **全局脚本和全局配置，用其中一种就可以了**
- 初次使用请阅读脚本代码的前 100 行，对脚本的功能有个大概的理解

## SubStore 使用教程

Mihomo 覆写脚本可以在 SubStore 中直接生成覆写后的订阅文件，这样就不需要在客户端里再额外执行一次覆写脚本。

### 在文件管理页签中添加一个 Mihomo 配置

在 SubStore 的脚本操作中添加脚本链接。为了下载速度更快，可以使用镜像地址：

`https://hk.gh-proxy.org/https://raw.githubusercontent.com/kongbaitt/YaNet/refs/heads/main/Mihomo/global_script.js`

也可以直接使用 GitHub 原始链接：

`https://github.com/kongbaitt/YaNet/raw/refs/heads/main/Mihomo/global_script.js`

### 参数表

#### `enable`

默认值：`true`

说明：总开关。

#### `mode`

默认值：`default`

说明：可选 `securest | secure | default | fast | fastest`，影响 DNS 分流。越靠近 `securest` 越倾向于国外 DoH，越靠近 `fastest` 越倾向于国内 IP DNS。若更重视速度，推荐 `fast`。

#### `ruleSet`

默认值：`all`

说明：代理组开关。可选 `apple | microsoft | github | google | openai | spotify | youtube | bahamut | netflix | tiktok | disney | pixiv | hbo | mediaHMT | biliintl | tvb | hulu | primevideo | telegram | line | whatsapp | games | japan | ads`，多个值用半角分号分隔。

#### `regionSet`

默认值：`all`

说明：地区分组开关。可选 `HK | US | JP | KR | SG | CN | TW | GB | DE | MY | TK | CA | AU`，多个值用半角分号分隔。

#### `excludeHighPercentage`

默认值：`true`

说明：是否过滤高倍率节点。

#### `globalRatioLimit`

默认值：`2`

说明：过滤高倍率节点的倍率阈值。

#### `skipIps`

默认值：

`10.0.0.0/8;100.64.0.0/10;169.254.0.0/16;172.16.0.0/12;192.168.0.0/16;198.18.0.0/16;FC00::/7;FE80::/10;::1/128`

说明：用于 `sniffer['skip-src-address']`、`sniffer['skip-dst-address']`、`tun['route-exclude-address']`。

#### `defaultDNS`

默认值：`119.29.29.29;223.5.5.5`

说明：作为 Mihomo 配置里的 `default-nameserver`，必须为 IP，多个值用半角分号分隔。

#### `directDNS`

默认值：`119.29.29.29;223.5.5.5`

说明：作为 Mihomo 配置里的 `direct-nameserver`，多个值用半角分号分隔。

#### `chinaDNS`

默认值：`https://doh.pub/dns-query;https://dns.alidns.com/dns-query`

说明：作为 Mihomo 配置里的 `nameserver`、`proxy-server-nameserver`，以及 `nameserver-policy` 的中国站点策略。

#### `foreignDNS`

默认值：`https://dns.google/dns-query;https://dns.adguard-dns.com/dns-query`

说明：作为 Mihomo 配置里 `nameserver-policy` 的国外站点策略。

### 生成订阅链接

在 SubStore 中配置好脚本和参数后，生成分享链接，再把这个分享链接导入客户端即可。

### 常见问题

#### 使用 tun 模式后，某些内网 IP 段无法访问

这是因为 tun 模式下流量会被路由进 VPN 隧道，内网地址可能因此无法直连。解决方法是在 `skipIps` 参数中追加你自己的内网网段。

例如，你可以在默认值基础上继续追加：

`10.0.0.0/8;100.64.0.0/10;169.254.0.0/16;172.16.0.0/12;192.168.0.0/16;192.169.0.0/16;198.18.0.0/16;FC00::/7;FE80::/10;::1/128`

建议始终以脚本默认值为基础追加，而不是整段替换掉，避免漏掉常用保留地址段。

#### FlClash 和 BettBox 报错

这两个客户端默认可能会改写 geox 配置，需要在 `资源` 中手动设置 geo 文件地址：

| 资源名称 | URL |
| --- | --- |
| `GeoIp` | `https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.dat` |
| `GeoSite` | `https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geosite.dat` |
| `MMDB` | `https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/country.mmdb` |
| `ASN` | `https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/GeoLite2-ASN.mmdb` |

## Big Changelog

- 2025-12-31：Mihomo 全局脚本支持在 SubStore 中使用，教程见上文
- 2025-11-23：修改`国外AI`代理策略
- 2025-11-22：重写脚本，提升执行效率；修改 `DNS` 服务和 `fake-ip` 策略
- 2024-09-27：添加的功能控制开关，增加策略组和分流规则
- 2024-09-24：未符合分类规则的节点全扔进其他节点策略组里
- 2024-09-22：大更新，优化图标、策略组，提升易用性
