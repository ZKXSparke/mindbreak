# MindBreak

AI 工作健康提醒 Skill。在你使用 Claude Code 持续工作时，自动在回复末尾插入休息提醒。

## 原理

提醒逻辑完全由 hook 脚本计算，Claude 只需响应触发信号。不依赖 Claude "记住"去检查，保证不遗漏。

```
用户发消息 → hook 脚本自动运行 → 算时长、判断阈值 →
  未达标 → 不输出（Claude 无感知，无打扰）
  达标   → 输出 MINDBREAK_xxx 信号 → Claude 看到，在回复末尾加提醒
```

## 安装

### 1. 放置文件

```
~/.claude/
├── skills/mindbreak/
│   ├── SKILL.md
│   └── README.md
└── scripts/
    ���── mindbreak_hook.sh
```

### 2. 配置 Hook

在 `~/.claude/settings.json` 中添加��

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bash ~/.claude/scripts/mindbreak_hook.sh",
            "timeout": 5
          }
        ]
      }
    ]
  }
}
```

### 3. 验证

重启 Claude Code，连续工作 45 分钟以上后，hook 应输出触发信号，Claude 在回复末尾自动附加提醒。

## 提醒类型

| 类型 | 触发条件 | 说明 |
|------|---------|------|
| 轻提醒 | 连续工作 >= 45 分钟 | 建议起来走动 |
| 饭点提醒 | 11:30-12:30 / 17:30-18:30 | 附带任务小结 |
| 加班提醒 | 21:00 后仍在工作 | 建议收尾 |

## 限制

- 每个工作段最多 3 次提醒
- 两次提醒间隔至少 30 分钟
- 中断 15 分钟以上回来不会立即提醒（识别为新工作段）
- 用户说"不用提醒"可关闭当次会话

## 状态文件

| 文件 | 用途 |
|------|------|
| `~/.claude/mindbreak_activity.log` | 活动时间戳（自动清理 >24h） |
| `~/.claude/mindbreak_last_reminder` | 上次提醒时间 |
| `~/.claude/mindbreak_reminder_count` | 当前工作段提醒次数 |
| `~/.claude/mindbreak_segment_start` | 当前工作段起始时间 |
