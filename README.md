# DHCG.KA 部署说明（状态栏前端产物）

本目录内容即为 GitHub 空仓库 `DHCG-Alpha/DHCG.KA` 应包含的完整内容，用于通过 jsdelivr 推送状态栏前端。

## 目录结构
```
dist/合成兽人会不会梦到电子学长/界面/状态栏/index.html   ← 自包含产物（已内联 JS/CSS）
```

## 上线后的 CDN 地址（jsdelivr）
将本目录全部内容推送到 `DHCG-Alpha/DHCG.KA` 的 `main` 分支后，状态栏地址为：

```
https://testingcf.jsdelivr.net/gh/DHCG-Alpha/DHCG.KA/dist/合成兽人会不会梦到电子学长/界面/状态栏/index.html
```

> 该地址对应主项目 `正则/状态栏界面.html` 中的占位符，已在其中替换。

## 推送方式（任选其一）
1. 本机命令行（需已具备 GitHub 认证）：
   ```bash
   cd deploy/DHCG.KA
   git init
   git add .
   git commit -m "statusbar frontend"
   git remote add origin https://github.com/DHCG-Alpha/DHCG.KA.git
   git branch -M main
   git push -u origin main
   ```
2. 用 GitHub 网页「Add file → Upload files」把 `dist/` 目录拖进去提交。

## 重新部署（修改前端后）
- 在 `tavern_helper_template` 重新运行产线构建（见下方），然后用新的 `index.html` 覆盖本目录同名文件再推送；或直接用新的内容 push 覆盖旧文件。
- jsdelivr 对 `main` 分支缓存最长 7 天；如需即时生效可另打 tag 用 `@v1` 引用，或访问
  `https://purge.jsdelivr.net/gh/DHCG-Alpha/DHCG.KA@main/dist/合成兽人会不会梦到电子学长/界面/状态栏/index.html` 手动刷新缓存。

## 本地重新构建命令（Node22 需用类型剥离绕过 ts-node/TS6 冲突）
在 `tavern_helper_template` 根目录：
```
node --experimental-transform-types .build-runner.mjs
```
产物输出到 `dist/合成兽人会不会梦到电子学长/界面/状态栏/index.html`。