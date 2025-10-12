# CI/CD 配置说明

## 🚀 GitHub Actions 工作流

### 触发条件
- **Push** 到 `main` 或 `develop` 分支
- **Pull Request** 到 `main` 分支
- **手动触发** (workflow_dispatch)

### 工作流程

#### 1. 测试阶段 (test)
- ✅ 检查代码
- ✅ 设置 Node.js 18
- ✅ 启动 MongoDB 服务
- ✅ 安装依赖
- ✅ 运行测试
- ✅ 构建前端
- ✅ ESLint 检查
- ✅ TypeScript 检查

#### 2. 构建阶段 (build)
- ✅ 创建部署包
- ✅ 上传构建产物
- ✅ 保留 30 天

#### 3. 部署阶段
- **Staging**: `develop` 分支自动部署到测试环境
- **Production**: `main` 分支自动部署到生产环境

#### 4. Docker 构建
- ✅ 构建后端镜像
- ✅ 构建前端镜像
- ✅ 推送到 Docker Hub

## 🔧 配置要求

### GitHub Secrets 配置
在 GitHub 仓库设置中添加以下 Secrets：

```bash
DOCKER_USERNAME=你的Docker用户名
DOCKER_PASSWORD=你的Docker密码
```

### 环境变量
- **NODE_VERSION**: 18
- **MONGODB_VERSION**: 6.0

## 📋 使用步骤

### 1. 推送代码
```bash
git add .
git commit -m "feat: 新功能"
git push origin develop  # 触发测试环境部署
git push origin main     # 触发生产环境部署
```

### 2. 查看工作流
- 访问 GitHub 仓库的 "Actions" 标签
- 查看工作流执行状态
- 下载构建产物

### 3. 手动部署
- 在 GitHub Actions 页面点击 "Run workflow"
- 选择分支和参数
- 执行部署

## 🎯 部署环境

### Staging (测试环境)
- **分支**: `develop`
- **用途**: 功能测试、集成测试
- **访问**: https://staging.your-domain.com

### Production (生产环境)
- **分支**: `main`
- **用途**: 正式发布
- **访问**: https://your-domain.com

## 🔍 监控和日志

### 构建状态
- ✅ 绿色：构建成功
- ❌ 红色：构建失败
- 🟡 黄色：构建中

### 日志查看
1. 点击失败的步骤
2. 查看详细日志
3. 定位问题原因

## 🛠️ 自定义配置

### 修改 Node.js 版本
```yaml
env:
  NODE_VERSION: '20'  # 修改为需要的版本
```

### 添加测试
```yaml
- name: Run tests
  run: |
    cd backend
    npm test
```

### 自定义部署
```yaml
- name: Deploy to server
  run: |
    # 添加你的部署命令
    rsync -avz deployment-package/ user@server:/path/to/app/
```

---
**配置完成时间**: 2025-10-12  
**支持版本**: GitHub Actions v4+

