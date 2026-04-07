# 游戏设计知识库 | Game Design Knowledge Base

> 双轨制知识架构：理论 → 框架 → 机制 → 案例

## 🗂️ 新目录结构 (双轨制)

```
game-design/
├── 00_Index/                    # 导航入口
│   └── knowledge-map.md         # 完整知识地图
│
├── 10_Theory/                   # 学术理论层
│   ├── survival-game-blueprint.md    (TH-2024-001)
│   ├── systemic-design.md            (TH-2024-002)
│   └── environmental-storytelling.md (TH-2024-003)
│
├── 20_Frameworks/               # 设计框架层
│   ├── scp-official-standards.md     (FR-2024-004)
│   ├── scp-framework.md              (FR-2024-003)
│   └── gdd-template.md               (FR-2024-002)
│
├── 30_Mechanics/                # 机制组件层 (待填充)
│   └── [从案例中提取的通用机制]
│
├── 40_CaseStudies/              # 案例分析层
│   └── abiotic-factor/
│       ├── overview.md               (CS-2024-001)
│       └── deep-dive.md              (CS-2024-002)
│
├── 50_Projects/                 # 当前项目层
│   └── 9th-containment/
│       └── gdd.md                    (PRJ-2024-001)
│
└── 90_TechRefs/                 # 技术实现层
    └── 2d-topdown-guide.md           (TECH-2024-001)
```

## 🚀 快速导航

**入口**: [00_Index/knowledge-map.md](00_Index/knowledge-map.md) - 完整知识地图

**按角色查找**:
- **系统策划** → 10_Theory/ + 30_Mechanics/
- **文案策划** → 20_Frameworks/SCP + 10_Theory/环境叙事
- **数值策划** → 10_Theory/生存游戏学术理论
- **技术策划** → 90_TechRefs/

## 📝 使用规范

每个文档包含 YAML frontmatter:
```yaml
---
uid: TH-2024-001          # 唯一标识符
type: theory              # 类型: theory/framework/mechanic/case/project
domain: [survival-game]   # 领域
tags: [心流理论]          # 标签
related:                  # 关联文档
  - uid: FR-2024-002
    title: "GDD模板"
created: 2026-04-07
status: mature
---
```

## 📊 统计

- **理论文档**: 3
- **框架文档**: 3
- **案例分析**: 2 (Abiotic Factor)
- **项目文档**: 1 (第9号收容所)
- **技术参考**: 1
- **总计**: 10个知识节点

---
**重构时间**: 2026-04-07  
**架构版本**: v2.0 (双轨制)
