# IM系统目录结构规范

## 📁 项目根目录结构

```
im-last/
├── 📄 .env                          # 环境变量配置文件
├── 📄 .gitignore                    # Git忽略文件
├── 📄 docker-compose.yml            # Docker Compose主配置
├── 📄 package.json                  # Node.js依赖配置
├── 📄 package-lock.json             # 依赖锁定文件
│
├── 📁 backend/                      # 后端服务目录
│   ├── 📄 Dockerfile               # 后端Docker配置
│   ├── 📄 package.json             # 后端依赖
│   ├── 📄 server.js                # 主服务文件
│   ├── 📁 models/                  # 数据模型
│   │   ├── User.js                 # 用户模型
│   │   ├── Message.js              # 消息模型
│   │   ├── Group.js                # 群组模型
│   │   └── FriendRequest.js        # 好友请求模型
│   └── 📁 uploads/                 # 文件上传目录
│
├── 📁 frontend/                     # 前端应用目录
│   ├── 📄 Dockerfile               # 前端Docker配置
│   ├── 📄 nginx.conf               # Nginx配置
│   ├── 📄 package.json             # 前端依赖
│   ├── 📄 vite.config.js           # Vite构建配置
│   ├── 📄 tailwind.config.js       # Tailwind CSS配置
│   ├── 📄 index.html               # HTML入口文件
│   └── 📁 src/                     # 源代码目录
│       ├── 📄 App.jsx              # 主应用组件
│       ├── 📄 main.jsx             # 入口文件
│       ├── 📁 pages/               # 页面组件
│       │   ├── Login.jsx           # 登录页面
│       │   ├── Register.jsx        # 注册页面
│       │   ├── ChatList.jsx        # 聊天列表
│       │   ├── ChatWindow.jsx      # 聊天窗口
│       │   ├── ContactsPage.jsx    # 联系人页面
│       │   └── ConversationsPage.jsx # 会话页面
│       ├── 📁 context/             # React Context
│       │   └── AuthContext.jsx     # 认证上下文
│       └── 📁 components/          # 公共组件
│
├── 📁 docs/                        # 📚 文档目录
│   ├── README_IM.md                # 系统说明文档
│   ├── README_PRODUCTION.md        # 生产环境文档
│   ├── DELIVERY_PACKAGE.md         # 交付说明
│   ├── DEPLOYMENT_REPORT.md        # 部署报告
│   └── IMPORT_FORMAT.md            # 导入格式说明
│
├── 📁 scripts/                     # 🛠️ 脚本目录
│   ├── start.sh                    # 启动脚本
│   ├── deploy.sh                   # 部署脚本
│   ├── check_connectivity.sh       # 连通性检查
│   ├── db_manager.sh               # 数据库管理
│   ├── import_chat_records.sh      # 聊天记录导入
│   ├── test_features.sh            # 功能测试
│   └── import_data.js              # 数据导入脚本
│
├── 📁 config/                      # ⚙️ 配置文件目录
│   ├── env.example                 # 环境变量示例
│   ├── env.production              # 生产环境配置
│   ├── ecosystem.config.js         # PM2配置
│   ├── nginx.production.conf       # 生产Nginx配置
│   └── docker-compose.backup.yml   # Docker配置备份
│
├── 📁 samples/                     # 📄 示例文件目录
│   ├── sample_chat_records.json    # JSON格式示例
│   ├── sample_chat_records.csv     # CSV格式示例
│   └── sample_wechat_export.txt    # 微信格式示例
│
├── 📁 backup/                      # 💾 备份文件目录
│   ├── app_production.js           # 生产版本备份
│   ├── frontend_eCrrk.tar.gz       # 前端备份包
│   ├── im-system-production.tar.gz # 系统备份包
│   └── frontend_server.js          # 前端服务器备份
│
├── 📁 data/                        # 🗄️ 数据目录
│   └── mongo/                      # MongoDB数据目录
│
├── 📁 init/                        # 🚀 初始化目录
│   └── init_data.json              # 初始化数据
│
├── 📁 uploads/                     # 📎 上传文件目录
│   └── (用户上传的文件)
│
├── 📁 logs/                        # 📝 日志目录
│   └── (系统日志文件)
│
└── 📁 node_modules/                # 📦 Node.js依赖包
```

## 🎯 目录用途说明

### 核心应用目录
- **`backend/`** - 后端Node.js服务，包含API、数据模型、文件上传
- **`frontend/`** - 前端React应用，包含所有页面和组件
- **`data/`** - 数据库持久化存储目录
- **`uploads/`** - 用户上传的文件存储

### 管理和维护目录
- **`docs/`** - 所有项目文档，包括使用说明、部署指南
- **`scripts/`** - 运维脚本，包括启动、部署、测试、管理工具
- **`config/`** - 配置文件，包括环境配置、服务配置
- **`backup/`** - 备份文件和历史版本
- **`samples/`** - 示例数据和模板文件
- **`logs/`** - 系统运行日志
- **`init/`** - 初始化数据和脚本

## 📋 文件命名规范

### 配置文件
- `*.config.js` - JavaScript配置文件
- `*.conf` - Nginx等服务配置
- `env.*` - 环境变量文件
- `docker-compose*.yml` - Docker配置

### 脚本文件
- `*.sh` - Shell脚本 (可执行)
- `*.js` - Node.js脚本

### 文档文件
- `README*.md` - 说明文档
- `*.md` - Markdown文档

### 备份文件
- `*.backup.*` - 备份文件
- `*.tar.gz` - 压缩包
- `*副本*` - 中文备份标识

## 🚀 快速访问

### 常用脚本
```bash
# 启动系统
./scripts/start.sh

# 检查连通性
./scripts/check_connectivity.sh

# 管理数据库
./scripts/db_manager.sh status

# 导入聊天记录
./scripts/import_chat_records.sh -h
```

### 常用文档
```bash
# 查看系统说明
cat docs/README_IM.md

# 查看部署报告
cat docs/DEPLOYMENT_REPORT.md

# 查看导入格式
cat docs/IMPORT_FORMAT.md
```

### 配置文件
```bash
# 环境配置
cp config/env.example .env

# 生产环境配置
cp config/env.production .env
```

## ⚠️ 注意事项

1. **不要直接编辑 `node_modules/`** - 这是自动生成的依赖目录
2. **备份重要数据** - `data/` 和 `uploads/` 目录包含重要数据
3. **保持目录结构** - 移动文件时注意更新相关引用路径
4. **权限管理** - 确保脚本文件有执行权限 (`chmod +x`)
5. **环境配置** - 不同环境使用对应的配置文件

---

**目录整理完成时间**: $(date)
**整理规则**: 按功能分类，便于维护和管理
