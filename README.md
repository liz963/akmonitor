# Akile Monitor 前端

![预览](https://github.com/Seikoa/akmonitor/blob/main/akile_monitor.png?raw=true)

Akile Monitor 是一个开源的服务器监控面板前端项目。支持多服务器监控、实时数据展示、自定义背景等功能。

## 功能特点

- 多服务器监控
- 实时数据展示
- CPU/内存/网络监控
- 支持自定义背景图片
- 支持亮色/暗色主题
- 支持按地区分类查看
- 支持在线/离线筛选
- 支持服务器到期提醒

## 快速开始

### 方式一：直接下载

1. 从 [Actions](https://github.com/Seikoa/akmonitor/actions) 页面下载最新构建版本
   - 进入最新的成功构建记录
   - 在 Artifacts 区域下载构建文件
2. 解压后修改 `config.json` 文件：
```json
{
  "socket": "ws://后端主控ip:3000/ws",
  "apiURL": "http://后端主控ip:3000"
}
```
  如果开启tls则
```json
{
  "socket": "wss://后端主控域名/ws",
  "apiURL": "http://后端主控域名"
}
```

3. 将文件部署到您的 Web 服务器

### 方式二：手动构建

1. 克隆项目
```bash
git clone https://github.com/Seikoa/akmonitor.git
cd akmonitor
```

2. 安装依赖
```bash
npm install
```

3. 开发模式
```bash
npm run dev
```

4. 构建
```bash
npm run build
```

构建后的文件在 `dist` 目录下，修改 `config.json` 后即可部署。

## 配置说明

### config.json
```json
{
  "socket": "ws(s)://服务器IP:3000/ws",  // WebSocket 服务器地址
  "apiURL": "http(s)://服务器IP:3000"    // API 服务器地址
}
```

## 自定义背景

1. 点击右下角图片图标
2. 可以输入图片 URL 或上传本地图片
3. 调节透明度
4. 点击确认保存

## 开源协议

MIT License

## 相关项目

- [Akile Monitor 后端](https://github.com/akile-network/akile_monitor)
- [Akile Monitor 客户端](https://github.com/akile-network/akile_monitor_client)

# akmonitor
