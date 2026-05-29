# incident.md - 故障知识库

## 记录格式

### 问题编号：INC-XXX

**日期：** YYYY-MM-DD
**问题现象：**
> 描述

**原因：**
> 根因

**修复动作：**
> 解决步骤

**验证方法：**
> 确认修复的方式

**教训：**
> 下次如何避免

---

## 已记录问题

### INC-001：jiangtao-zs agent工作区不完整

**日期：** 2026-05-29

**问题现象：**
> jiangtao-zs agent工作区缺少BOOTSTRAP.md、models.json和完整配置文件，无法正常使用飞书技能

**原因：**
> 创建agent工作区时未完整初始化，只有基础文件

**修复动作：**
1. 从xiajie-zs agent复制完整文件：AGENTS.md、BOOTSTRAP.md、SOUL.md
2. 初始化git仓库并配置用户信息
3. 复制models.json到agent工作区
4. 验证文件完整性

**验证方法：**
- 检查目录包含10个文件（AGENTS.md, BOOTSTRAP.md, SOUL.md等）
- git仓库已初始化
- models.json存在

**教训：**
- 创建新agent工作区时必须确保完整初始化
- 共享技能在 `/home/administrator/.openclaw/workspace/.agents/skills/`，但agent需要自己的配置文件

---

### INC-002：OpenClaw API端口18791不存在

**日期：** 2026-05-29

**问题现象：**
> 测试API时发现18791端口不存在，HTTP请求返回404

**原因：**
> OpenClaw gateway只监听18789（HTTP控制面板），API使用WebSocket而非HTTP REST

**修复动作：**
1. 通过 `openclaw gateway status` 确认端口配置
2. 验证18789是WebSocket端口
3. 理解架构：HTTP服务器用于Control UI，API通过WebSocket调用

**验证方法：**
- `ss -tlnp | grep openclaw` 显示只监听18789
- `openclaw gateway status` 显示 "port=18789 (service args)"

**教训：**
- OpenClaw API不是REST API，是通过WebSocket调用的
- 测试API需要使用WebSocket客户端，而非HTTP REST工具

---

### INC-003：合作共赢相互学习群agent身份漂移（小智vs小冬瓜）

**日期：** 2026-05-29

**问题现象：**
> 群里agent原本是小冬瓜（正常工作），突然换了身份说自己没有名字，不记得任何事情

**原因：**
> 存在多重身份源：
> 1. `agents/admin/agent/` → IDENTITY是"小智"，但USER.md里写"小冬瓜（我）"，内部矛盾
> 2. `workspace/` 和 `workspace/main/` → 小冬瓜人格文件，但配置未指向此处
> 3. `agents/main/agent/` → 空白模板，从未初始化
> 飞书群oc_bb32e5befdda6949efe320cee8802ebb绑定到admin agent，但admin的身份文件自述矛盾

**修复动作：**
1. 确认使用"小智"作为正式身份
2. 统一USER.md：删除"小冬瓜（我）"的引用，改为"小智"
3. 统一SOUL.md：称呼部分保持"夏波→夏哥，孙波→孙哥"
4. admin agent现在身份一致：小智，服务夏哥和孙波

**验证方法：**
- IDENTITY.md显示"小智"
- USER.md合作模式写"小智提供工具/自动化支持"
- 群路由绑定到admin agent → 小智

**教训：**
- 同一个agent目录下，IDENTITY.md和USER.md必须互洽，不能矛盾
- workspace/main/等子目录的人格文件如果与配置不一致，就会造成身份漂移
- 小冬瓜人格文件存在于workspace/但配置未指向，是历史遗留问题

---

### INC-004：sandbox.mode "docker" 不支持

**日期：** 2026-05-30

**问题现象：**
> 配置main agent的 `sandbox.mode: "docker"` 时报错：`Invalid input (allowed: "off", "non-main", "all")`

**原因：**
> OpenClaw 2026.5.22版本中 `sandbox.mode` 只支持三个固定值："off", "non-main", "all"。不存在"docker"模式。

**修复动作：**
1. 先尝试 `sandbox.mode: "docker"` → 失败
2. 改用 `sandbox.mode: "all"` → 成功
3. 这意味着main agent没有任何沙箱限制

**验证方法：**
- `openclaw gateway run` 成功启动
- 日志显示 `gateway ready`
- 3个飞书账号websocket连接成功

**教训：**
- 不能想当然认为OpenClaw支持"docker"模式
- 必须先查阅官方文档或 `openclaw doctor` 确认支持的具体值
- 当前方案 `mode: all` 是折中，安全级别较低

---