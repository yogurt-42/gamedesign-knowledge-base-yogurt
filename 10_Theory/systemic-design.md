# 系统式设计 (Systemic Design)

## 核心哲学

> **给玩家目标，但不限定解决方案。**

涌现性玩法 (Emergent Gameplay) 来源于简单规则的复杂交互。

## 核心公式

```
涌现性 = Σ(简单规则) + 交互可能性
```

## 塞尔达传说：旷野之息 案例分析

### 基础规则
1. 金属导电
2. 火融冰
3. 雨使岩石湿滑
4. 风传播火

### 涌现组合
| 组合 | 结果 |
|------|------|
| 金属武器 + 雷电天气 | 雷击战术 |
| 火 + 草地 + 风 | 可控的野火 |
| 冰 + 火 + 水 | 蒸汽遮挡视野 |

**关键**：设计师未预设这些组合，但规则允许它们发生。

## 刺激-反应系统

### 非硬编码交互
```gdscript
# 传统方式
if player.use_water_on_fire:
    fire.extinguish()

# 系统式方式
fire.emit_signal("heat", area)
water.emit_signal("wet", area)
# 两者在区域内相遇 → 蒸汽效果自动产生
```

### 元素属性基类
```gdscript
class Element:
    var conductivity: float  # 导电性
    var flammability: float  # 可燃性
    var reactivity: Dictionary  # 与其他元素的反应
    
    func react_with(other: Element) -> Effect:
        # 根据属性计算反应，而非硬编码
```

## 沉浸式模拟的核心教条

### 1. 一致性
物理规则统一应用于所有对象：
- 玩家放的火和敌人放的火行为相同
- 玩家能用的策略，AI也能用

### 2. 可预测性
玩家通过学习规则能预测结果：
- 看到油+火 → 预期爆炸
- 看到电+水 → 预期导电

### 3. 意外性
简单组合产生设计师未预期的结果：
- 这是涌现性的标志
- 也是 bug 和 feature 的模糊边界

## 给你的收容所游戏

### 非生物因素基类设计
```gdscript
class AbioticFactor:
    enum Type { ELECTRICITY, FIRE, GRAVITY, RADIATION, COLD, PRESSURE }
    var type: Type
    var intensity: float
    var radius: float
    
    func affect_target(target):
        match target.type:
            Type.METAL when self.type == ELECTRICITY:
                target.conduct(self.intensity)
            Type.WATER when self.type == FIRE:
                return Steam.new(intensity * 0.5)
            Type.LIVING when self.type == RADIATION:
                target.add_status("irradiated")
```

### 收容物 × 环境的交互示例

| 收容物 | 环境元素 | 交互结果 |
|--------|---------|---------|
| K-001 雷云 | 金属地板 | 电击传导 |
| K-002 重力异常 | 投掷物 | 轨迹改变 |
| K-003 腐蚀液 | 金属门 | 门被破坏 |
| K-004 低温场 | 水 | 冰桥形成 |

### 涌现性测试清单
- [ ] 玩家能否用意想不到的方式组合元素？
- [ ] 同一问题是否有多种解决方案？
- [ ] 玩家失败是因为理解规则不足，还是随机性？
- [ ] 是否有"我没想到还能这样"的时刻？

## 平衡性警告

### 涌现性 ≠ 混乱
需要约束条件防止系统失控：
- 元素反应有冷却时间
- 某些区域禁止特定交互
- 资源限制防止无限连锁

### 测试策略
1. **封闭测试**：给玩家目标，观察解决方案
2. **记录意外**：哪些交互是设计师未预期的？
3. **决策保留**：好的意外成为正式机制，坏的修复

---
**创建时间**: 2026-04-07
**来源**: The Artifice论文、沉浸式模拟研究、塞尔达设计分析
