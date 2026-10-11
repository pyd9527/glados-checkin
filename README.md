# GLaDOS 自动签到

每天自动为 GLaDOS 账号签到领流量，无需人工操作。

## 工作原理

GitHub Actions 每天北京时间 **09:18** 和 **12:18** 自动运行一次签到脚本（`.github/workflows/gladosCheck.yml`），
用仓库里保存的 Cookie 调用 GLaDOS 接口签到，签到结果记录在 Actions 运行日志里。

## 当前配置

| 项目 | 值 |
| --- | --- |
| GLaDOS 账号 | pyd13683959746@gmail.com |
| 签到域名 | glados.cloud |
| 自动签到时间 | 每天 09:18、12:18（北京时间） |
| 密钥名称 | `GLADOS_COOKIES` |
| 自动兑换积分 | 未开启 |

## 可选的额外配置

在仓库 `Settings → Secrets and variables → Actions` 里按需添加：

| Secret 名称 | 作用 | 取值 |
| --- | --- | --- |
| `GLADOS_EXCHANGE_PLAN` | 积分攒够后自动兑换天数 | `plan100`(100分→10天) / `plan200`(200分→30天) / `plan500`(500分→100天) |
| `PUSHDEER_SENDKEY` | 签到结果推送到手机 | 在 pushdeer.com 获取 |
| `GLADOS_VERBOSE` | 日志输出更详细 | `true` |

## Cookie 过期了怎么办

GLaDOS 的 Cookie 有效期有限，失效后签到会失败（日志里显示 `No permission` 或登录错误）。更新方法：

1. 浏览器打开并登录 https://glados.cloud/console
2. 按 `F12` → 切到 `Network`（网络）标签 → 刷新页面
3. 点第一个请求，在 `Request Headers` 里找到 `Cookie`，复制它的值
4. 回到仓库 `Settings → Secrets and variables → Actions`，点 `GLADOS_COOKIES` → `Update`，粘贴新值保存

## 手动跑一次

仓库 `Actions` 页 → 左侧 `auto check` → 右侧 `Run workflow`。

## 说明

本项目基于 [Devilstore/Glados-Railgun-checkin](https://github.com/Devilstore/Glados-Railgun-checkin)（GPL-3.0）改写，
仅保留单站点签到逻辑并适配本账号。
