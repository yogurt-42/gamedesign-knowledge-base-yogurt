# 2D俯视角技术实现指南

## 引擎选择

### Godot 4（推荐）
- 内置TileMap系统
- 多人联机API（Scene Replication）
- GDScript简单易学
- 节点系统适合实体管理

### LÖVE2D
- 极简Lua框架
- 完全控制渲染
- 适合快速原型

## 核心系统架构

### 1. 实体组件系统 (ECS)
```gdscript
# 基础实体
class Entity extends CharacterBody2D:
    var components: Dictionary
    
    func add_component(type, component):
        components[type] = component
        component.entity = self
    
    func get_component(type):
        return components.get(type)

# 可拆解组件
class DismantlableComponent:
    var loot_table: Dictionary
    
    func dismantle() -> Array[Item]:
        var result = []
        for item in loot_table:
            if randf() < loot_table[item].chance:
                result.append(Item.new(item, loot_table[item].count))
        return result
```

### 2. 理智系统实现
```gdscript
class SanityComponent:
    var max_sanity: float = 100.0
    var current_sanity: float = 100.0
    var hallucination_threshold: float = 30.0
    
    func modify(amount: float):
        current_sanity = clamp(current_sanity + amount, 0, max_sanity)
        update_visual_effects()
    
    func update_visual_effects():
        if current_sanity < hallucination_threshold:
            # 启用后处理效果：边缘模糊、色彩失真
            PostProcess.enable_distortion(intensity=(1 - current_sanity/max_sanity))
            # 随机生成幻觉实体
            if randf() < 0.1:  # 10%概率每帧
                spawn_hallucination()
```

### 3. 视野与迷雾系统
```gdscript
class FogOfWar:
    var visibility_map: TileMapLayer
    var player_sight_range: float = 8.0  # 格子数
    
    func update(player_position: Vector2):
        # 使用射线投射或圆形检测
        for x in range(-player_sight_range, player_sight_range):
            for y in range(-player_sight_range, player_sight_range):
                var pos = player_position + Vector2(x, y)
                if pos.distance_to(player_position) <= player_sight_range:
                    if has_line_of_sight(player_position, pos):
                        visibility_map.set_cell(pos, VISIBILITY_VISIBLE)
                    else:
                        visibility_map.set_cell(pos, VISIBILITY_SEEN)
```

### 4. 交互系统
```gdscript
class InteractionSystem:
    var interactables: Array[Interactable] = []
    
    func check_interaction(player_pos: Vector2, mouse_pos: Vector2):
        var target = get_interactable_at(mouse_pos)
        if target and target.position.distance_to(player_pos) <= interaction_range:
            show_tooltip(target)
            if Input.is_action_just_pressed("interact"):
                target.interact()
    
    func show_tooltip(target: Interactable):
        # 显示拆解信息、科学价值等
        var text = target.get_tooltip_text()
        Tooltip.show_at(mouse_pos, text)
```

## 地图设计

### TileSet 分层
1. **地板层**：行走表面
2. **墙体层**：碰撞阻挡
3. **装饰层**：叙事细节（血迹、弹孔）
4. **交互层**：可拆解物体
5. **实体层**：动态对象（玩家、收容物）

### 房间模板
```gdscript
class Room:
    var size: Vector2i
    var type: RoomType  # OFFICE, LAB, CONTAINMENT
    var connections: Array[Doorway]
    var spawn_points: Dictionary  # { "player": Vector2, "scp": Vector2 }
    
    func generate():
        match type:
            RoomType.OFFICE:
                place_desks(randi() % 5 + 3)
                place_computers(randi() % 3 + 1)
            RoomType.LAB:
                place_lab_tables(4)
                place_containment_cell()
```

## 多人联机基础

### 主机-客户端模型
```gdscript
# 主机
class GameHost:
    func start_server(port: int):
        var peer = ENetMultiplayerPeer.new()
        peer.create_server(port, max_players)
        multiplayer.multiplayer_peer = peer
        
        multiplayer.peer_connected.connect(on_player_connected)
    
    func on_player_connected(id: int):
        spawn_player(id)
        sync_game_state(id)

# 客户端
class GameClient:
    func connect_to_server(ip: String, port: int):
        var peer = ENetMultiplayerPeer.new()
        peer.create_client(ip, port)
        multiplayer.multiplayer_peer = peer
```

### 状态同步
```gdscript
class SyncedEntity:
    @rpc
    func update_position(pos: Vector2):
        if multiplayer.is_server():
            return  # 只有服务器发送更新
        position = pos
    
    func _physics_process(delta):
        if multiplayer.is_server():
            update_position.rpc(position)  # 广播给所有客户端
```

## 性能优化

### 对象池
```gdscript
class EntityPool:
    var pool: Dictionary  # { type: Array[Entity] }
    
    func get_entity(type: String) -> Entity:
        if pool[type].size() > 0:
            return pool[type].pop_back()
        return create_new(type)
    
    func return_entity(entity: Entity):
        entity.reset()
        pool[entity.type].append(entity)
```

### 视野剔除
```gdscript
func _process(delta):
    var camera_rect = get_viewport_rect()
    for entity in entities:
        if camera_rect.has_point(entity.global_position):
            entity.visible = true
        else:
            entity.visible = false
```

## 项目结构建议

```
📁 project/
├── 📁 assets/
│   ├── sprites/        # 2D素材
│   ├── tilesets/       # 地图图块
│   └── audio/          # 音效音乐
├── 📁 src/
│   ├── entities/       # 实体定义
│   ├── components/     # 组件系统
│   ├── systems/        # 游戏系统
│   ├── ui/             # 界面
│   └── utils/          # 工具函数
├── 📁 scenes/
│   ├── levels/         # 关卡场景
│   └── ui/             # UI场景
└── project.godot
```

---
**创建时间**: 2026-04-07
**来源**: Godot文档、多人游戏开发经验
