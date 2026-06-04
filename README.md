# 警民合作小程序

基于 uni-app、Vue 3 和 Vite 初始化的微信小程序项目。

## 常用命令

```bash
npm install
npm run dev:mp-weixin
npm run build:mp-weixin
```

## 微信开发者工具

运行开发命令后，在微信开发者工具中导入：

```text
dist/dev/mp-weixin
```

正式构建产物路径：

```text
dist/build/mp-weixin
```

微信小程序 AppID 可在 `src/manifest.json` 的 `mp-weixin.appid` 中配置。
