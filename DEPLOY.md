# 部署说明

本项目是纯静态站点：没有后台、没有数据库、没有构建步骤。把仓库里的文件原样放到任何静态托管即可。

当前线上地址由 **GitHub Pages** 提供：<https://rapids2.github.io/oxford5000/>
（Settings → Pages → Source 选 `Deploy from a branch`，分支 `main`，目录 `/ (root)`）

---

## 换到 Cloudflare Pages

访问速度更均衡，尤其是中国大陆方向。

1. 打开 [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. 选中本仓库
3. 构建设置全部留空：Framework preset 选 `None`，Build command 空着，Output directory 填 `/`
4. Deploy，一两分钟后得到 `xxx.pages.dev`

仓库里的 `_headers` 会被自动识别，用来设置缓存策略。

## Netlify

- 拖拽：把文件夹拖到 <https://app.netlify.com/drop>，立刻得到网址
- 或在 Netlify 后台连接本仓库，构建命令留空，发布目录填 `.`

## 绑定自定义域名

**GitHub Pages**：仓库根目录新建一个名为 `CNAME` 的文件，内容写域名（如 `oxford.example.com`），
再到域名商处添加一条 CNAME 记录指向 `rapids2.github.io`。

**Cloudflare Pages**：项目页 → Custom domains → Set up a domain，按提示添加记录即可，证书自动签发。

## 更新内容

在 GitHub 网页上点 **Add file → Upload files**，把改动过的文件拖上去覆盖并提交，托管平台会自动重新发布。

改动 `data.json` 时，记得同时把 `sw.js` 里的 `oxford-v1` 改成 `oxford-v2`，
让已经安装过 PWA 的用户能拿到新词库。
