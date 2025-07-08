# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 重要：
用中文回答我
每次都用審視的目光，仔細看我輸入的潛在問題，你要指出我的問題，並給出明顯在我思考框架之外的建議如果你覺得我說的太離譜了，你就罵回來，幫我做到瞬間清醒，你有自己的思考，我的想法不一定都是對的，請你不要客氣記得，一定要直接！甚至可以罵我！要不然我太飄了，你不能迎合我，你罵我我知道你都是為了我好，所以你千萬不要客氣，要不然是再害我！
你要基於第一性原理，從源頭幫我思考問題，直擊要害
我比較喜歡奧卡姆剃須刀的哲學，"如無必要 勿增實體"，所以我想法如果發散了，你要記得把我拉回來！
就像MVP一樣，保持最小可用，切記過渡設計！

## 项目简介
NiuTV 是一个免费的在线视频搜索与观看平台，支持多种部署方式。项目提供前端界面和后端代理功能，可部署在支持服务端功能的各类网站托管服务上。

## 核心架构

### 前端架构
- **技术栈**: HTML5 + CSS3 + JavaScript (ES6+)
- **样式**: Tailwind CSS
- **播放器**: DPlayer + HLS.js
- **存储**: localStorage
- **主要页面**:
  - `index.html` - 首页搜索界面
  - `player.html` - 视频播放页面
  - `watch.html` - 观看页面

### 后端架构
- **主服务**: `server.mjs` - Express.js 服务器（本地开发）
- **代理功能**: `/proxy` 路由处理视频流代理
- **Vercel部署**: `/api/proxy/[...path].mjs`

### 关键组件
- **API 管理**: `js/api.js` - 视频源接口管理
- **搜索功能**: `js/search.js` - 搜索逻辑
- **播放器**: `js/player.js` - 视频播放控制
- **用户界面**: `js/ui.js` - 界面交互
- **配置管理**: `js/config.js` - 配置处理

## 开发命令

### 本地开发
```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 启动生产服务器
npm run start
```

### 环境变量
- `PASSWORD` - 用户访问密码
- `ADMINPASSWORD` - 管理员密码
- `PORT` - 服务端口 (默认 8080)
- `CORS_ORIGIN` - CORS 允许的源
- `DEBUG` - 调试模式

## 部署配置

### Vercel
- 配置文件: `vercel.json`
- 函数目录: `/api/proxy/`
- 重写规则处理搜索路径和代理

## 重要文件结构

```
NiuTV/
├── server.mjs              # 主服务器文件（本地开发）
├── index.html             # 首页
├── player.html            # 播放器页面
├── js/
│   ├── app.js            # 主应用逻辑
│   ├── api.js            # API 接口管理
│   ├── search.js         # 搜索功能
│   ├── player.js         # 播放器控制
│   └── ui.js             # 用户界面
├── api/proxy/            # Vercel 代理函数
├── css/                  # 样式文件
└── libs/                 # 第三方库
```

## 开发注意事项

### 安全性
- 使用环境变量管理密码
- URL 验证防止 SSRF 攻击
- 过滤敏感响应头
- 设置适当的 CORS 策略

### 代理功能
- 支持 HLS 视频流代理
- 自动重试机制
- 请求超时处理
- 流式数据传输

### 前端状态管理
- 使用 localStorage 持久化用户设置
- API 选择状态管理
- 搜索历史记录
- 播放进度保存

## 常见任务

### 添加新的视频源
1. 在 `js/api.js` 中添加新的 API 配置
2. 确保 API 符合苹果 CMS V10 格式
3. 更新用户界面显示新源

### 修改播放器功能
1. 编辑 `js/player.js`
2. 更新 `player.html` 中的控件
3. 测试不同格式视频的播放

### 部署到Vercel
1. 确保 `vercel.json` 配置正确
2. 代理函数位于 `/api/proxy/[...path].mjs`
3. 设置必要的环境变量（PASSWORD、ADMINPASSWORD等）