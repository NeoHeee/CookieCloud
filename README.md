<div align="center">
  <img src="ext/public/icon/128.png" width="128" alt="CookieCloud Community for Firefox">
  <h1>CookieCloud Community for Firefox</h1>
  <p><strong>Firefox Desktop 与 Firefox Android 专用的 CookieCloud 社区版扩展</strong></p>
  <p>同步 Cookie，并可选同步匹配域名的 Local Storage；数据在浏览器本地加密后发送到用户配置的 CookieCloud 服务端。</p>

  <p>
    <a href="PRIVACY.md">隐私说明</a> ·
    <a href="https://github.com/easychen/CookieCloud">上游项目与服务端</a> ·
    <a href="https://github.com/NeoHeee/CookieCloud-Community-for-Firefox/issues">问题反馈</a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Firefox-1.0.4-FF7139?logo=firefox-browser&logoColor=white" alt="Firefox 1.0.4">
    <img src="https://img.shields.io/badge/Desktop-supported-success" alt="Firefox Desktop supported">
    <img src="https://img.shields.io/badge/Android-Firefox%20120%2B-success" alt="Firefox Android 120+">
    <img src="https://img.shields.io/badge/license-GPL--3.0-blue" alt="GPL-3.0">
  </p>
</div>

---

## 仓库范围

本仓库**只保留 Firefox 浏览器扩展**及其构建、测试、AMO 审核所需文件，不包含：

- CookieCloud 服务端源码或 Docker 部署文件；
- Chrome、Edge 或其他 Chromium 浏览器的构建与发布流程；
- 上游示例、SDK、截图和无关脚手架文件。

CookieCloud 服务端和其他平台版本请前往上游项目：[easychen/CookieCloud](https://github.com/easychen/CookieCloud)。

> 本项目是社区维护的 Firefox 适配版本，不是 easychen 原作者发布的官方 Firefox 扩展。

## 支持范围

| 平台 | 状态 | 最低版本 |
|---|---|---|
| Firefox Desktop | ✅ 支持 | 由 AMO Manifest 决定 |
| Firefox Android | 🧪 已适配 | Firefox 120+ |

Firefox Android 已加入 Manifest 声明、全屏移动布局、触控尺寸和安全区域适配。发布前仍建议在真机复测上传、下载、定时同步和 Local Storage 同步。

## 功能

- 手动或定时上传、下载 Cookie；
- 按域名关键词筛选同步范围；
- 域名黑名单；
- 可选同步 Local Storage；
- Cookie Keep Alive；
- 用户自定义服务端地址和附加请求 Header；
- 本地加密后再传输同步载荷。

## 安全提醒

Cookie 属于高敏感登录凭据。本扩展需要申请 `cookies`、`<all_urls>` 等高权限才能工作。建议：

- 优先连接可信的自建 CookieCloud 服务端，并使用 HTTPS；
- UUID 和密码使用互不重复的随机值，密码建议至少 24 位；
- 不同步网银、支付、主邮箱、密码管理器、域名注册商、Cloudflare 或 NAS 管理后台；
- 不需要 Local Storage 时将其关闭；
- Firefox 与 Chrome/Edge 使用不同 UUID，避免数据格式相互覆盖。

详见 [PRIVACY.md](PRIVACY.md)。

## 本地开发

需要 Node.js 22 与 pnpm 10.28.0：

```bash
git clone https://github.com/NeoHeee/CookieCloud-Community-for-Firefox.git
cd CookieCloud-Community-for-Firefox/ext

corepack enable
corepack prepare pnpm@10.28.0 --activate
pnpm install --frozen-lockfile
pnpm compile
pnpm dev
```

## 构建 Firefox 包

```bash
cd ext
pnpm install --frozen-lockfile
pnpm compile
pnpm zip
```

输出目录：

```text
ext/dist/*firefox*.zip
```

未签名 ZIP 只适合开发测试。正式版 Firefox 长期安装需要由 Mozilla AMO 签名。

## 目录结构

```text
.github/workflows/build-firefox.yml  Firefox 构建与校验
ext/                                Firefox 扩展源码
  entrypoints/                      后台、内容脚本与设置界面
  public/                           多语言和图标
  utils/                            Cookie、存储和加密逻辑
  AMO_BUILD.md                      Mozilla 可复现构建说明
LICENSE                             GPL-3.0
PRIVACY.md                          隐私说明
```

## 许可证与来源

- 上游项目：[easychen/CookieCloud](https://github.com/easychen/CookieCloud)
- Firefox 社区版：[NeoHeee/CookieCloud-Community-for-Firefox](https://github.com/NeoHeee/CookieCloud-Community-for-Firefox)
- 许可证：[GNU General Public License v3.0](LICENSE)

感谢原作者 easychen 及所有贡献者。本仓库的修改继续按照 GPL-3.0 发布。
