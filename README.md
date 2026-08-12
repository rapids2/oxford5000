# 部署说明

这个文件夹就是完整的网站，是纯静态的：没有后台、没有数据库、不用付服务器钱。
把整个文件夹原样上传到任何静态托管，就能得到一个网址。

```
site/
├── index.html              主页面（15 KB gzip 后）
├── data.json               词库 7632 条（1.8 MB gzip 后）
├── sw.js                   Service Worker，装过一次后断网也能用
├── manifest.webmanifest    PWA 配置，手机可"添加到主屏幕"
├── icon-192.png / icon-512.png / icon-maskable-512.png
├── _headers                Netlify / Cloudflare 的缓存规则
└── .nojekyll               GitHub Pages 用
```

> 注意：`index.html` 需要通过 http(s) 打开，直接双击会因为浏览器安全限制读不到 `data.json`。
> 想在本机离线用，请用同目录外的 **oxford-3000-5000.html** 单文件版。

---

## 推荐做法：GitHub 存代码 + Cloudflare Pages 托管

代码留在 GitHub 方便版本管理和以后扩展成个人网站，Cloudflare 负责分发（全球 CDN，国内访问比 GitHub Pages 稳）。

1. 在 GitHub 新建一个仓库，比如 `oxford5000`（Public）
2. 把 `site/` 里的文件（不是文件夹本身）上传到仓库根目录
   —— 网页上点 **Add file → Upload files**，把文件全选拖进去即可，不用命令行
3. 打开 [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
4. 选中刚才的仓库，构建设置全部留空（Framework preset 选 None，Build command 空着，Output directory 填 `/`）
5. 点 Deploy，一两分钟后拿到 `xxx.pages.dev` 的网址

以后想改内容，在 GitHub 上改文件，Cloudflare 会自动重新发布。

### 绑定自己的域名

Cloudflare Pages 项目里 → **Custom domains** → **Set up a domain** → 填 `oxford.你的域名.com`，
按提示加一条 CNAME 记录就行，HTTPS 证书自动签发，免费。

---

## 更快的做法：Netlify Drop（1 分钟，不用注册也能先试）

1. 打开 <https://app.netlify.com/drop>
2. 把 `site` 文件夹整个拖进去
3. 立刻得到一个 `xxx.netlify.app` 网址

想保留和改域名，注册一个免费账号把这个站点认领了即可。

---

## 也可以只用 GitHub Pages

1. 仓库 → **Settings** → **Pages**
2. Source 选 `Deploy from a branch`，分支选 `main`，目录选 `/ (root)`
3. 保存，等一分钟，网址是 `你的用户名.github.io/仓库名/`

绑定自定义域名：在仓库根目录加一个名为 `CNAME` 的文件，内容写你的域名（例如 `oxford.example.com`），
然后在域名商那边加一条 CNAME 指向 `你的用户名.github.io`。

**注意**：如果以后想做个人主页，把仓库改名为 `你的用户名.github.io`，
这个词表可以放在子目录 `/oxford/` 下，两者不冲突。

---

## 手机上当 App 用

网站上线后用手机浏览器打开：

- **iPhone（Safari）**：分享按钮 → 添加到主屏幕
- **Android（Chrome）**：右上角菜单 → 安装应用 / 添加到主屏幕

装好后图标在桌面，打开没有浏览器地址栏，**断网也能背单词**（词库已缓存在本机）。
学习进度存在浏览器本地，换设备请用页面上的「导出进度 / 导入进度」。

---

## 以后想更新词库

只替换 `data.json`，然后把 `sw.js` 里的 `oxford-v1` 改成 `oxford-v2`
（改版本号是为了让已经装过的用户拿到新数据），重新上传即可。
