# IM 系统部署说明

## 🚀 快速部署

### Windows 系统
1. **解压文件**到任意目录
2. **双击运行** `deploy.bat` 或 `start.bat`
3. **访问** http://localhost:3001

### Linux 系统
1. **解压文件**到服务器目录
2. **运行命令**：
   ```bash
   chmod +x deploy.sh
   ./deploy.sh
   ```
3. **访问** http://你的服务器IP:3001

## 📋 系统要求

### 必需环境
- **Node.js** 16.0+ 
- **npm** 8.0+
- **MongoDB** 4.0+

### 可选环境
- **Nginx** (用于生产环境)
- **PM2** (用于进程管理)

## 🔧 手动部署

### 1. 安装依赖
```bash
cd backend
npm install
```

### 2. 启动 MongoDB
```bash
# Linux
sudo systemctl start mongod

# Windows
# 启动 MongoDB 服务
```

### 3. 启动后端
```bash
cd backend
npm start
```

### 4. 配置前端
前端文件在 `frontend/` 目录，可直接部署到 Web 服务器。

## 🌐 生产环境部署

### 使用 Docker
```bash
docker-compose -f docker-compose.prod.yml up -d
```

### 使用 PM2
```bash
cd backend
npm run pm2:start
```

## 📱 访问地址

- **后端 API**: http://localhost:3001/api
- **前端页面**: http://localhost:3001 (如果配置了静态文件服务)
- **WebSocket**: ws://localhost:3001

## 🔍 故障排除

### 端口被占用
```bash
# Linux
sudo kill -9 $(lsof -t -i:3001)

# Windows
taskkill /f /im node.exe
```

### MongoDB 连接失败
1. 检查 MongoDB 是否启动
2. 检查连接字符串配置
3. 检查防火墙设置

### 前端无法访问
1. 检查前端文件是否正确部署
2. 检查 Nginx 配置
3. 检查跨域设置

## 📞 技术支持

如遇问题，请检查：
1. 系统日志：`logs/app.log`
2. 控制台输出
3. 网络连接状态

---
**版本**: 1.0.0  
**更新日期**: 2025-10-12