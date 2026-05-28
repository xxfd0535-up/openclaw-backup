# backup.md - Git备份与同步流程

## 仓库结构

```
远程仓库：https://github.com/xxfd0535-up/openclaw-memory
├── .openclaw-memory/      # 运维记忆（版本化）
└── configs/              # 配置文件备份（待创建）
    └── openclaw.json     # 配置副本（不含敏感信息）
```

---

## Git 运维流程

### 1. 初始化仓库

```bash
cd C:\Users\Administrator\.openclaw-memory
git init
git add .
git commit -m "Initial: OpenClaw 运维记忆系统"
```

### 2. 添加远程仓库

```bash
git remote add origin https://github.com/xxfd0535-up/openclaw-memory.git
git push -u origin master
```

### 3. 日常变更

```bash
# 修改后即时报存
git add <changed-files>
git commit -m "描述本次变更"
git push  # 推送到远程
```

### 4. 配置备份

- 配置文件路径：`/home/administrator/.openclaw/openclaw.json` (WSL内)
- 本地副本：`C:\Users\Administrator\temp_openclaw.json`
- 敏感信息处理：记录哈希值，不记录明文密钥

---

## 同步策略

- 变更即同步
- 不积累大量未提交变更
- 每次运维操作后立即 commit

---

## 已完成

- ✅ 远程仓库已创建：https://github.com/xxfd0535-up/openclaw-memory
- ✅ 初始提交已推送
- ⏳ configs目录待创建