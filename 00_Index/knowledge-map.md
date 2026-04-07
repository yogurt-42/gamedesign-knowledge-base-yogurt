---
uid: IDX-2024-001
title: "知识库导航地图"
type: index
domain: [game-design, knowledge-management]
tags: [导航, 索引, 知识管理]
created: 2026-04-07
status: active
---

# 🧭 游戏设计知识库导航

> 双轨制知识库：理论/框架/机制/案例四层架构

---

## 📚 知识层级

### 10_Theory/ 学术理论
**基础原理，理解"为什么"**

| UID | 文档 | 核心内容 |
|-----|------|---------|
| TH-2024-001 | [生存游戏学术理论](10_Theory/survival-game-blueprint.md) | 心流理论、经济系统、风险回报 |
| TH-2024-002 | [系统式设计原则](10_Theory/systemic-design.md) | 涌现性、元素交互、刺激-反应 |
| TH-2024-003 | [环境叙事理论](10_Theory/environmental-storytelling.md) | 指数叙事、指示符、场景设计 |

### 20_Frameworks/ 设计框架
**标准化方法，知道"怎么做"**

| UID | 文档 | 核心内容 |
|-----|------|---------|
| FR-2024-001 | [SCP文档框架](20_Frameworks/scp-official-standards.md) | 官方标准、临床语调、等级分类 |
| FR-2024-002 | [GDD模板](20_Frameworks/gdd-template.md) | 机制九要素、资源八要素 |
| FR-2024-003 | [SCP设计框架](20_Frameworks/scp-framework.md) | 收容物设计、游戏化机制 |

### 30_Mechanics/ 机制组件
**可复用零件，直接"拿来用"**

> 待创建：从案例中提取通用机制

### 40_CaseStudies/ 案例分析
**具体游戏，看"别人怎么做"**

| UID | 文档 | 核心内容 |
|-----|------|---------|
| CS-2024-001 | [非生物因素概览](40_CaseStudies/abiotic-factor/overview.md) | 基础分析、核心机制 |
| CS-2024-002 | [非生物因素深度](40_CaseStudies/abiotic-factor/deep-dive.md) | 拆解系统、非生物威胁、空间叙事 |

### 50_Projects/ 当前项目
**正在进行的项目**

| UID | 文档 | 核心内容 |
|-----|------|---------|
| PRJ-2024-001 | [第9号收容所GDD](50_Projects/9th-containment/gdd.md) | 项目概述、MVP规划 |

### 90_TechRefs/ 技术参考
**实现指南**

| UID | 文档 | 核心内容 |
|-----|------|---------|
| TECH-2024-001 | [2D俯视角实现](90_TechRefs/2d-topdown-guide.md) | Godot架构、ECS、多人联机 |

---

## 🎯 主题入口

### 非生物因素设计
**Abiotic Factor Design**

非生命的物理和化学因素作为游戏机制：
- 环境危害（温度、辐射、重力）
- 物理交互（拆解、改造）
- 静态异常物
- 空间叙事

**相关资源**：
- 理论：[系统式设计](10_Theory/systemic-design.md)
- 案例：[非生物因素深度分析](40_CaseStudies/abiotic-factor/deep-dive.md)
- 技术：[2D实现指南](90_TechRefs/2d-topdown-guide.md)

### 收容物/异常设计
**Anomaly/Containment Design**

- 框架：[SCP文档框架](20_Frameworks/scp-official-standards.md)
- 机制：[SCP设计框架](20_Frameworks/scp-framework.md)
- 项目：[第9号收容所](50_Projects/9th-containment/gdd.md)

---

## 🚀 快速开始

### 策划流程
```
1. 理论理解 → 10_Theory/
2. 方法选择 → 20_Frameworks/
3. 机制组合 → 30_Mechanics/
4. 案例参考 → 40_CaseStudies/
5. 项目实践 → 50_Projects/
```

### 按角色查找
- **系统策划** → 10_Theory/ + 30_Mechanics/
- **文案策划** → 20_Frameworks/SCP + 10_Theory/环境叙事
- **数值策划** → 10_Theory/生存游戏学术理论
- **技术策划** → 90_TechRefs/

---

## 📝 使用规范

### 添加新文档
1. 确定类型：Theory/Framework/Mechanic/Case/Project
2. 分配 UID：{类型缩写}-{年份}-{序号}
3. 添加 YAML frontmatter
4. 更新此导航

### 建立关联
在 YAML 中使用 `related:` 字段：
```yaml
related:
  - uid: TH-2024-001
    title: "相关文档标题"
```

---

## 🔗 外部资源

- GitHub: [game-design-knowledge](https://github.com/)
- 维护者: Opus
- 最后更新: 2026-04-07
