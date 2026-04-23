---
uid: WORKFLOW-001
title: "知识库使用指南"
type: guide
domain: [knowledge-management]
tags: [工作流, 维护, SOP]
created: 2026-04-07
status: active
---

# 知识库使用指南

> 如何高效使用和维护这个双轨制知识库

---

## 🎯 知识库架构理解

### 四层结构

```
10_Theory/      → 理解"为什么"
20_Frameworks/  → 知道"怎么做"  
30_Mechanics/   → 直接"拿来用"
40_CaseStudies/ → 看"别人怎么做"
50_Projects/    → 当前"自己在做"
```

### 核心原则

> **永远不要复制粘贴，永远使用 [[UID]] 链接。**

这样当"温度系统"需要调整时，只需改一处，所有项目自动更新。

---

## 📝 日常维护 SOP

### 1. 新增资料时的决策树

```
收到新资料（如一篇GDC讲座）
    ↓
是学术理论？ → 放入 10_Theory/，打标签 #理论
    ↓
是设计方法/模板？ → 放入 20_Frameworks/，打标签 #框架
    ↓
是具体游戏分析？ → 放入 40_CaseStudies/，打标签 #案例
    ↓
包含可复用机制？ → 抽离到 30_Mechanics/，原案例用 [[引用]]
    ↓
是项目专属？ → 放入 50_Projects/[当前项目]/，打标签 #项目
```

### 2. 文档创建模板

**必须包含的 YAML frontmatter**：

```yaml
---
uid: {类型缩写}-{年份}-{序号}
title: "文档标题"
type: {theory/framework/mechanic/case/project/topic}
domain: [所属领域]
tags: [标签1, 标签2]
sources: [来源资料]
projects: [相关项目]
related:
  - uid: XXX-XXXX-XXX
    title: "相关文档标题"
status: {draft/verified/mature/archived}
needs-validation: {true/false}
last-reviewed: YYYY-MM-DD
---
```

### 3. 引用规范

**正确引用**：
```markdown
本项目的温度系统基于 [MECH-001](../30_Mechanics/abiotic-hazards.md) 非生物威胁系统，
但做以下调整：
- 极寒范围：设施冷库区（而非地下复合体）
```

**错误引用**（复制粘贴）：
```markdown
❌ 温度系统的工作原理是...
[大段复制30_Mechanics/abiotic-hazards.md的内容]
```

### 4. 认知冲突记录规范（重要）

**不要平滑处理分歧**——当个人分析与设计师意图、或不同信源之间存在冲突时，显式记录张力而非抹平。

**正确做法**：
```markdown
## 未解决张力

| 设计师声称 | 我的体验/分析 | 冲突点 |
|-----------|-------------|--------|
| "权限卡强化官僚主题" | 实际感受是"门控设计偷懒" | 主题化 vs 玩法乐趣的失衡 |
| "委员会与希斯是善恶对立" | 二者实为同一控制逻辑的两极 | 设计师意图 vs 文本潜文本 |

**待验证**：需要对比其他玩家的体验报告，或查看 DLC 是否有对此的修正
```

**错误做法**（平滑处理）：
```markdown
❌ Control 的官僚恐怖设计成功地创造了平凡与怪异的冲突...
[引用设计师采访，但忽略自己的真实体验与之不符]
```

**为什么重要**：
- 保留真实的思维过程，而非虚假的"完整结论"
- 设计师意图与实际体验的裂缝，往往是真正洞察的来源
- 三个月后回看，你能看到自己当时在哪里犹豫，追踪认知如何演化

---

## 🔍 查找资料的三种方式

### 方式1：按层级浏览
- 需要理论支持 → 10_Theory/
- 需要实现方法 → 20_Frameworks/
- 需要可复用代码 → 30_Mechanics/
- 需要参考案例 → 40_CaseStudies/

### 方式2：按主题入口
- [topic-abiotic-factors.md](topic-abiotic-factors.md) - 非生物因素专题
- [knowledge-map.md](knowledge-map.md) - 完整知识地图

### 方式3：按UID搜索
```bash
grep -r "MECH-001" ~/code/game-design/
```

---

## 🔄 项目复盘时的归档流程

当自有项目完成时：

### 步骤1：归档项目
```bash
cd ~/code/game-design/
mkdir -p 90_Archive/my-project-2026/
mv 50_Projects/my-project/* 90_Archive/my-project-2026/
```

### 步骤2：添加复盘文档
```markdown
# my-project 项目复盘

## 哪些机制有效？
- ✅ 温度系统：2D化表现良好
- ⚠️ 实验系统：等待时间过长，需要优化

## 哪些需要调整？
- 黑雾视觉效果不够明显
- 收容物AI行为树过于简单

## 反馈到机制库
- 更新 [MECH-001](../30_Mechanics/abiotic-hazards.md) 的"实践验证记录"
- 创建新的 MECH-006 改进版收容AI
```

### 步骤3：更新相关机制文档
在 30_Mechanics/ 对应文件的"实践验证记录"章节添加项目反馈。

---

## ⚠️ 常见错误

### ❌ 错误1：在项目中重复机制细节
```markdown
# bad: my-project/gdd.md

## 温度系统
温度系统的工作原理是...[复制粘贴300字]
```

### ✅ 正确：引用+差异说明
```markdown
# good: my-project/gdd.md

## 温度系统
基于 [[MECH-001]] 非生物威胁系统，
调整参数：
- 崩溃阈值：从-40°C调整为-30°C（2D游戏节奏更快）
- 视觉反馈：增加屏幕结冰效果
```

### ❌ 错误2：忘记更新 last-reviewed
每次修改文档后，更新 YAML 中的 `last-reviewed` 字段。

### ❌ 错误3：不建立 related 链接
新文档创建时，检查是否有相关已有文档，建立双向链接。

### ❌ 错误4：平滑处理认知冲突
将"设计师说 X"和"我认为 Y"之间的张力抹平，写成看似一致的 Z。这会丢失：
- 真实的设计错位（体验与意图的偏差）
- 你当时的认知位置（忘了自己曾怀疑过什么）
- 未来可追溯的思维演化路径

---

## 📊 每周维护清单（15分钟）

- [ ] 检查是否有新资料待分类
- [ ] 检查 50_Projects/ 文档是否正确引用 30_Mechanics/
- [ ] 更新 topic-abiotic-factors.md 的链接（如有新增）
- [ ] 检查是否有文档需要 review（last-reviewed 超过30天）

---

## 🚀 快速开始

### 新增一个机制文档

1. 复制模板：
```bash
cp 30_Mechanics/abiotic-hazards.md 30_Mechanics/your-mechanic.md
```

2. 修改 YAML：
- 更改 uid（如 MECH-006）
- 更新 title、tags、related

3. 撰写内容：
- 核心设计原则
- 具体机制说明
- 参数建议
- 实践验证记录（留空待填）

4. 更新索引：
- 在 topic-abiotic-factors.md 添加链接
- 在 knowledge-map.md 添加条目

5. 提交：
```bash
git add . && git commit -m "Add MECH-006: 机制名称"
```

---

## 🔗 相关文档

- [knowledge-map.md](knowledge-map.md) - 完整知识地图
- [topic-abiotic-factors.md](topic-abiotic-factors.md) - 非生物因素专题
- [README.md](../README.md) - 知识库总览

---
**创建时间**: 2026-04-07  
**最后更新**: 2026-04-12（新增认知冲突记录规范）  
**维护者**: Opus
