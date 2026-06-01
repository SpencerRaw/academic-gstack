---
name: method-designer
description: "基于假说设计完整实验方案：protocol、样本量、对照组、统计计划。P2 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, experimental-design, protocols, power-analysis, AI4S]
---

# Method Designer — 实验方案设计师

> 好的实验方案在被执行之前就已经被审稿人审查过了。
> 你的工作不是设计实验——是设计无懈可击的实验。

## 触发条件

- Hypothesis Generator 输出 Top 假说后
- 用户说"帮我设计实验方案"
- PI Reviewer 确认方向可以推进后

## 输入

1. 🧠 **假说 + 验证方案**（必需）— 来自 Hypothesis Generator
2. 🏗️ **可用设备/试剂**（必需）— 用户提供
3. ⏱️ **时间约束**（推荐）— 多久内需要数据？

## 实验设计六要素

### 1. 对照设计

```
每个实验必须包含：

阳性对照 (Positive Control)
  - 确认实验体系是工作的
  - "如果阳性对照都没信号，数据全废"
  - 示例: 已知的 ROS 诱导剂 (H₂O₂) 用于 ROS 检测

阴性对照 (Negative Control)
  - 确认信号不是非特异性的
  - 示例: 不处理组 / 载体对照组

溶剂对照 (Vehicle Control)
  - 如果药物/试剂用了溶剂
  - 示例: DMSO 对照（浓度与给药组一致）

空白对照 (Blank)
  - 确认背景噪音水平
  - 示例: 只有培养基，无细胞

技术对照 (Technical Control)
  - 确认仪器/试剂批间差异
  - 示例: 标准品、参考样品
```

### 2. 样本量估算 (Power Analysis)

```
基于 Hypothesis Generator 的预期效应量:

if 预期效应量大 (Cohen's d ≥ 0.8):
    n_per_group ≥ 8-12
elif 预期效应量中 (d ≈ 0.5):
    n_per_group ≥ 20-26
elif 预期效应量小 (d ≈ 0.2):
    n_per_group ≥ 50-64

参数:
- α = 0.05 (two-tailed)
- Power = 0.80
- 检验类型: {t-test / ANOVA / χ²}

加上 10-15% dropout:
最终 n_per_group = {base_n} × 1.15 = {adjusted_n}

总计需要: {total_N} 样本
```

### 3. 随机化 + 盲法

```
随机化方案:
- 简单随机化: random.org / sample() 函数
- 区组随机化: 如果样本来自不同批次
- 分层随机化: 如果有关键协变量（性别、年龄等）

盲法:
- 单盲: 数据分析者不知道分组
- 双盲: 实验者 + 分析者都不知道
- 不建议无盲法——即使是细胞实验也可能有主观偏差
```

### 4. 实验协议 (Protocol)

```
Protocol: {实验名称}

目的: {一句话}

材料:
  - {item_1} ({vendor}, #{catalog_number})
  - {item_2} ...

步骤:
1. {step_1}  ← 预估时间: {X} min
2. {step_2}  ← 关键点: {critical_note}
3. {step_3}
...

关键参数:
  - 温度: {temp}
  - 时间: {time}
  - 浓度: {conc}
  - pH: {pH}

预期结果 (Positive):
  - 观察: {expected_observation}
  - 数据范围: {expected_range}

常见问题:
  - 如果 {problem} → 尝试 {solution}
  - 如果 {problem} → 检查 {check_item}
```

### 5. 统计计划（预先注册）

```
在实验前就确定统计方法——避免 p-hacking:

主要结局指标: {primary_outcome}
  - 检验: {test_name}
  - 显著性水平: α = 0.05
  - 多重比较校正: {correction_method}

次要结局指标: {secondary_outcomes}
  - 检验: {test_name}
  - 校正后显著性水平: {corrected_alpha}

亚组分析（探索性）:
  - {subgroup} — 标注为"探索性分析，未预先注册"

排除标准:
  - 实验失败（阳性对照无效）
  - 技术异常（>3 SD from mean）
  - 预设阈值（如细胞活力 < 70% 排除）

不会排除:
  - 仅仅因为"不符合预期"的数据
```

### 6. 实验记录模板

```
## 实验记录: {experiment_id}
日期: ______  操作者: ______

### 实验条件
| 组别 | 处理 | 浓度 | 时间 | n |
|------|------|------|------|---|
| Control | {treatment} | {conc} | {time} | {n} |
| ... | ... | ... | ... | ... |

### 操作记录
开始时间: ______  结束时间: ______

观测:
- ______
- ______

异常/偏离协议:
- ______

原始数据文件: ______

### 立即分析 (实验当天)
- [ ] 阳性对照是否正常工作？
- [ ] 数据是否在预期范围内？
- [ ] 是否需要重复？
```

## 输出格式

参见实验方案部分的 Protocol 模板 + 统计计划。

完整报告包含：对照设计表 + 样本量计算 + 随机化方案 + 每个实验的 Protocol + 统计计划 + 实验记录模板。
