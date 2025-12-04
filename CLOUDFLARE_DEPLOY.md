# Cloudflare Pages 部署配置指南

## 环境变量设置（必须！）

在 Cloudflare Pages 项目的 Settings > Environment variables 中添加：

### Production & Preview 都需要设置：

```
HUGO_VERSION = 0.152.2
NODE_VERSION = 22.11.0
```

## 构建配置

在 Cloudflare Pages 项目设置中：

### Framework preset
选择 **Hugo** 或 **None**

### Build command
```bash
npm run build:cloudflare
```

### Build output directory
```
public
```

### Root directory
```
/
```

## Node.js 版本

项目已包含 `.nvmrc` 文件，指定 Node.js 22.11.0

## 故障排查

### 如果部署失败，检查：

1. **环境变量是否正确设置**
   - `HUGO_VERSION` 必须设置为 `0.152.2` 或更高
   - 确保是 Hugo Extended 版本

2. **构建命令是否正确**
   - 使用 `npm run build:cloudflare`
   - 不要使用 `yarn`（除非你全项目改用 yarn）

3. **检查构建日志**
   - 查看是否有 Hugo 模块下载失败
   - 查看是否有 Node.js 依赖安装失败

4. **baseURL 配置**
   - `hugo.toml` 中的 `baseURL` 应该是你的部署域名
   - 当前设置为：`https://hugoplate-sha-cloudflare-pages.pages.dev/`

5. **网站打不开可能原因**
   - 构建成功但 `public` 目录为空
   - Hugo 版本不匹配（必须是 Extended 版本）
   - 构建命令未正确执行 `themeGenerator.js`

## 常见错误解决

### Error: "Hugo command not found"
➜ 在环境变量中设置 `HUGO_VERSION = 0.152.2`

### Error: "This feature is not available in your version of Hugo"
➜ 确保使用 Hugo Extended 版本，设置环境变量

### 网站显示空白或 404
➜ 检查 `public/index.html` 是否生成
➜ 查看构建日志确认构建成功
➜ 验证 `baseURL` 配置正确

## 验证部署成功

部署后访问：
- 首页：https://hugoplate-sha-cloudflare-pages.pages.dev/
- 关于：https://hugoplate-sha-cloudflare-pages.pages.dev/about/
- 博客：https://hugoplate-sha-cloudflare-pages.pages.dev/blog/

## 自动部署

推送到 GitHub 的 `main` 分支会自动触发 Cloudflare Pages 构建和部署。
