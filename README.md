# 部署说明（GitHub → Cloudflare Pages）

## 文件
- `index.html` — 册子本体（单文件，图片/代码全内嵌，无任何外部请求）
- `sw.js` — 离线缓存：访客第一次打开后，页面会被缓存，之后断网也能打开
- `_headers` — 让 sw.js 不被强缓存，保证离线逻辑能更新

三个文件要放在仓库根目录（或 Pages 的输出根目录）一起部署。

## 部署
1. GitHub 新建仓库，把这三个文件传到根目录。
2. Cloudflare 控制台 → Workers & Pages → Create → Pages → Connect to Git → 选这个仓库。
3. 构建设置：Framework 选 None，Build command 留空，Build output directory 留空（或 `/`），Deploy。
4. 完成后用分配的 `*.pages.dev` 域名打开即可；也可以绑自己的域名。

也可以不用 GitHub：Pages → Create → Upload assets，直接把这三个文件（或部署包 zip）拖上去。

## 更新页面时注意
每次换了新的 index.html，把 `sw.js` 第一行的版本号数字 +1（现在是 `books-v2`，下次改成 `books-v3`……），
否则老访客的浏览器会一直用缓存里的旧版。本地双击打开的离线版不受影响。
