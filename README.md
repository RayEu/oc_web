# OpenCode Session Viewer

基于 opencode serve HTTP API 的 Session 会话记录查看器。

<img width="1363" height="644" alt="image" src="https://github.com/user-attachments/assets/1706773d-df57-457f-8275-4bfc73ea9606" />


## 功能

- **Session 列表** (左侧): 展示所有会话，显示标题、ID、agent、时间，支持按 ID 搜索
- **刷新按钮**: 左侧标题栏 ↻ 按钮，手动刷新 session 列表
- **删除 Session**: hover 每条 session 右侧出现 × 按钮，点击删除
- **对话记录** (右侧): 展示选中会话的完整对话，包括:
  - 用户消息 (蓝色背景)
  - AI 回复 (文本内容)
  - 思考过程 (紫色，可折叠，默认收起)
  - 工具调用 (绿色，可折叠，默认收起，展开可查看 input/output)
  - 展开状态在轮询刷新时自动保持，不会被收起
- **发送消息**: 底部输入框，Enter 发送，向会话追加新消息
- **轮询自动刷新**: 定时拉取最新消息，无需手动刷新
- **新消息提示**: 向上翻看历史消息时，若新消息到达，输入框上方出现提示条，点击即可跳到底部
- **设置面板**: 左侧标题栏齿轮按钮，可配置 OpenCode URL 地址和轮询间隔 (默认10秒)
- **可调面板**: 拖拽左右面板分隔线调整宽度
- **主题切换**: 右上角按钮切换黑/白主题，默认白色，自动保存偏好

## 启动方式

### 前置条件

1. 启动 opencode serve (默认端口 4096):

```bash
opencode serve
```

2. 启动本页面的 HTTP 服务 (端口 8080):

```bash
cd oc_web
python -m http.server 8080
```

或直接双击运行 `start.bat`。

### 访问

浏览器打开 `http://127.0.0.1:8080/index.html`

## API 说明

opencode官方API接口，目前是V2版本，https://opencode.ai/v2/docs/api

| 功能 | API 端点 | 版本 |
|------|----------|------|
| Session 列表 | `GET /api/session` | v2 |
| Session 消息 | `GET /session/:id/message` | legacy |
| 发送消息 | `POST /session/:id/message` | legacy |
| 删除 Session | `DELETE /session/:id` | legacy |

> v2 消息接口 (`/api/session/:id/message`) 当前返回空数据，故消息相关操作使用 legacy 接口。

## 技术栈

- 纯 HTML/CSS/JS，无任何依赖
- 黑/白双主题，等宽字体
- CORS 跨域请求 opencode serve API

## 文件结构

```
oc_web/
├── index.html   # 主页面
├── start.bat    # 快速启动脚本
└── README.md    # 本文件
```
