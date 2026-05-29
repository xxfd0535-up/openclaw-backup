# ops.md - 变更历史记录

## 记录格式

| 日期 | 变更内容 | 原因 | 验证结果 |
|------|----------|------|----------|
| YYYY-MM-DD | 描述 | 原因 | 验证 |

---

## 版本信息

- OpenClaw 版本：2026.5.22
- Node.js 版本：22.22.2
- 安装方式：pnpm global install

---

## 变更历史

| 日期 | 变更内容 | 原因 | 验证结果 |
|------|----------|------|----------|
| 2026-05-29 | 创建运维记忆系统 | 方法论积累框架 | ✅ 已推送到Git |
| 2026-05-29 | 修复WSL配置文件换行符问题 | CRLF导致JSON解析失败 | ✅ Gateway正常启动 |
| 2026-05-29 | 多飞书bot配置部署 | 支持3个独立Agent | ⚠️ API端口18791是WebSocket非REST |
| 2026-05-29 | 安装飞书CLI @larksuite/cli | 让AI直接操作飞书 | ✅ v1.0.43已安装并配置App ID |
| 2026-05-29 | 修复jiangtao-zs agent工作区 | 缺少BOOTSTRAP.md和完整配置 | ✅ 已初始化git仓库和完整文件 |
| 2026-05-30 | 修复sandbox=off解决Docker缺失问题 | WSL无Docker守护进程 | ✅ Gateway正常启动 |
| 2026-05-30 | Agent权限隔离配置完成 | sandbox=off + tools.deny | ✅ 3账号运行中 |
| 2026-05-30 | 身份漂移问题已解决 | 删除admin agent，统一小冬瓜身份 | ✅ INC-003已记录 |

---

## Agent配置信息

### xiajie-zs (夏姐-小吕专用群)
- 工作区：`/home/administrator/.openclaw/agents/xiajie-zs/agent`
- 飞书AppID：cli_aa9dee2a4238dbb5
- 群组ID：oc_8435d436e743ad2144feb848d46ba0e3

### jiangtao-zs (江涛专用龙虾群)
- 工作区：`/home/administrator/.openclaw/agents/jiangtao-zs/agent`
- 飞书AppID：cli_aa9d861976f85be9
- 群组ID：oc_bb3353f1bbdaddfa476002b74abe693c

### main (小龙虾外部群)
- 工作区：`/home/administrator/.openclaw/agents/main/agent`
- 飞书AppID：cli_aa9b593264b8dbdb
- 群组ID：oc_bb32e5befdda6949efe320cee8802ebb