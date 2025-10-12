# IM系统聊天记录导入格式说明

## 📋 功能测试结果

根据刚才的测试，系统功能状态如下：

✅ **正常工作的功能:**
- 用户注册/登录 
- 好友列表获取
- 私信功能
- 聊天列表
- 文件上传接口
- Socket.io实时通信

⚠️ **需要注意的功能:**
- 群组功能接口 (API路径可能需要调整)

## 🗂️ 数据库结构分析

### 消息表 (messages) 字段结构:
```javascript
{
  sender: ObjectId,           // 发送者用户ID (必填)
  receiver: ObjectId,         // 接收者用户ID (私信时必填)
  group: ObjectId,           // 群组ID (群聊时必填)
  content: String,           // 消息内容 (必填)
  type: String,              // 消息类型: 'text', 'image', 'file', 'audio', 'video', 'location', 'emoji'
  fileInfo: {                // 文件信息 (文件消息时使用)
    filename: String,        // 服务器文件名
    originalName: String,    // 原始文件名
    fileSize: Number,        // 文件大小
    mimeType: String,        // MIME类型
    fileUrl: String,         // 文件访问URL
    thumbnail: String        // 缩略图URL
  },
  metadata: {                // 元数据
    latitude: Number,        // 位置纬度
    longitude: Number,       // 位置经度  
    address: String,         // 地址
    duration: Number,        // 音视频时长
    width: Number,           // 图片/视频宽度
    height: Number           // 图片/视频高度
  },
  read: Boolean,             // 是否已读
  readBy: [ObjectId],        // 已读用户列表
  timestamp: Date            // 时间戳
}
```

## 📥 聊天记录导入格式

### 1. JSON格式导入 (推荐)

```json
{
  "messages": [
    {
      "sender": "用户ID或用户名",
      "receiver": "用户ID或用户名", 
      "content": "消息内容",
      "type": "text",
      "timestamp": "2025-10-11T10:30:00Z"
    },
    {
      "sender": "用户ID或用户名",
      "group": "群组ID或群组名",
      "content": "群聊消息内容", 
      "type": "text",
      "timestamp": "2025-10-11T10:31:00Z"
    },
    {
      "sender": "用户ID或用户名",
      "receiver": "用户ID或用户名",
      "content": "图片描述",
      "type": "image",
      "fileInfo": {
        "originalName": "photo.jpg",
        "fileSize": 1024000,
        "mimeType": "image/jpeg",
        "fileUrl": "/uploads/photo.jpg"
      },
      "metadata": {
        "width": 1920,
        "height": 1080
      },
      "timestamp": "2025-10-11T10:32:00Z"
    }
  ]
}
```

### 2. CSV格式导入

```csv
sender,receiver,group,content,type,timestamp,fileUrl,fileName,fileSize
user1,user2,,你好！,text,2025-10-11T10:30:00Z,,,
user2,user1,,你好，很高兴认识你,text,2025-10-11T10:31:00Z,,,
user1,,group1,大家好,text,2025-10-11T10:32:00Z,,,
user1,user2,,看看这张图片,image,2025-10-11T10:33:00Z,/uploads/photo.jpg,photo.jpg,1024000
```

### 3. 微信聊天记录格式 (自动转换)

```
2025-10-11 10:30:00 张三
你好！

2025-10-11 10:31:00 李四  
你好，很高兴认识你

2025-10-11 10:32:00 张三
[图片]

2025-10-11 10:33:00 李四
[文件: document.pdf]
```

## 📤 支持的文件类型

### 图片类型:
- JPG/JPEG
- PNG  
- GIF
- WebP
- BMP

### 文件类型:
- PDF
- DOC/DOCX
- XLS/XLSX
- PPT/PPTX
- TXT
- ZIP/RAR

### 音视频类型:
- MP3/WAV (音频)
- MP4/AVI (视频)

## 🛠️ 导入工具使用方法

### 方法1: 使用批量导入API

```bash
# 导入JSON格式数据
curl -X POST http://localhost:3001/api/admin/messages/batch \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d @chat_records.json
```

### 方法2: 使用导入脚本

```bash
# 使用我们提供的导入脚本
./import_chat_records.sh chat_records.json
```

### 方法3: MongoDB直接导入

```bash
# 直接导入到MongoDB
docker exec im-mongodb mongoimport --db im-system --collection messages --file /tmp/messages.json --jsonArray
```

## 📁 文件处理说明

### 文件上传流程:
1. 先上传文件到 `/uploads/` 目录
2. 获取文件URL
3. 创建包含fileInfo的消息记录

### 图片处理:
- 自动生成缩略图
- 提取图片尺寸信息
- 支持Base64格式图片

### 大文件处理:
- 支持分块上传
- 自动压缩处理
- 生成下载链接

## ⚡ 批量导入优化

### 性能建议:
- 单次导入建议不超过1000条消息
- 大量数据请分批导入
- 文件先批量上传再创建消息记录

### 数据验证:
- 自动验证用户ID存在性
- 检查群组ID有效性
- 验证文件路径可访问性

## 🔧 故障排查

### 常见问题:
1. **用户ID不存在** - 请先导入用户数据
2. **文件路径错误** - 确保文件已上传到正确目录
3. **时间格式错误** - 使用ISO 8601格式
4. **权限不足** - 确保使用管理员token

---

**注意**: 导入前请备份现有数据，导入过程不可逆！
