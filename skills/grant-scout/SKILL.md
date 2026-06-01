---
name: grant-scout
description: "持续监控基金机会，自动匹配你的研究方向，生成申请提醒。P3 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, funding, grants, opportunities, AI4S]
---

# Grant Scout — 基金猎人

> 大部分基金不是因为不够好被拒的——是因为根本没申请。
> 你的工作不是找基金。是让基金来找你。

## 触发条件

- 每周自动监控（cron）
- 用户问"现在有什么基金可以申请？"
- 论文被接收后（触发 new grant opportunities search）
- 基金申请季开始前

## 监控源

| 来源 | 覆盖 | 频率 |
|------|------|------|
| Grants.gov | 美国联邦基金（NIH/NSF/DOE等） | 每日 |
| NSFC 官网 | 中国国家自然科学基金 | 按申请季 |
| EURAXESS | 欧洲基金 + 博后职位 | 每周 |
| Research Professional | 全球基金数据库 | 每周 |
| 各大学基金页面 | 校内基金/Fellowship | 不定期 |
| Twitter/X | 学者分享的基金信息 | 实时 |
| 邮件列表 | 领域基金通知 | 按邮件频率 |

## 匹配逻辑

```
对每个基金机会，计算匹配度：

1. 主题匹配 (40%)
   - 关键词与你的研究重叠度
   - 基金 description 中的关键词命中

2. 资格匹配 (30%)
   - 你是否符合申请条件？
   - 国籍/学位/年限要求

3. 时间可行性 (20%)
   - 截止日期是否够远？
   - 准备时间是否充足？（至少 2 个月）

4. 战略价值 (10%)
   - 与你的长期目标对齐？
   - 申请这个基金的 prestige 如何？
```

## 输出格式

```markdown
# 🎯 基金机会监控: {date_range}

## 🔴 本周推荐申请（匹配度 >80%）

### #1: {funding_name}
- **来源**: {agency/organization}
- **金额**: ${amount} / {duration}
- **截止日期**: {deadline}（剩余 {N} 天）
- **匹配度**: {score}%
- **为什么匹配**: {理由}
- **申请要求**: {key_requirements}
- **你的优势**: {why_you}
- **需要准备**: {what_you_need}
- **竞争对手估计**: {competition_level}

## 🟡 值得关注（匹配度 50-80%）

| 基金 | 金额 | 截止 | 匹配度 | 关键要求 |
|------|------|------|--------|---------|
| ... | ... | ... | ... | ... |

## 🟢 存档备查（匹配度 <50%）

| 基金 | 金额 | 截止 | 备注 |
|------|------|------|------|
| ... | ... | ... | ... |

## 📅 即将到期的基金

| 基金 | 截止 | 剩余 | 状态 |
|------|------|------|------|
| ... | ... | {N}天 | ⚠️ 紧迫 |
| ... | ... | {N}天 | 🟡 可准备 |

## 🧭 申请策略

### 本月行动计划
1. {action_1}
2. {action_2}

### 下一季度
1. {action_1}

## ❓ 需要你决定的

- [ ] {funding_X} 的资格要求你满足吗？（需要确认）
- [ ] {funding_Y} 需要合作者，你有合适的人选吗？
```

## Cron 配置

```bash
hermes cron create "0 9 * * 1" \
  --name "ac-gstack-grant-scout" \
  --prompt "加载 grant-scout skill。扫描本周新发布的基金机会，匹配所有在研课题。" \
  --skills "grant-scout" \
  --deliver "telegram" \
  --enabled_toolsets "web,skills,memory"
```

## 注意事项

- 基金截止日期是最重要的信息——错了后果严重
- 资格要求仔细检查——国籍/学位/年限等硬性限制
- 不要只推荐大基金——小基金/fellowship 成功率更高
- 如果用户有导师/合作者可以帮忙写推荐信，标注哪些基金需要
