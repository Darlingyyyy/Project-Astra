# Unity 工程搭建规范 — Project Astra

> **版本**: v0.1 · 2026-06-02  
> **引擎**: Unity 2022.3 LTS + URP  
> **目标**: 定义 Unity 项目的目录结构、渲染配置、Package 清单、编码规范，确保任何开发者克隆仓库后能直接开搞。

---

## 一、引擎版本

```
Unity 2022.3 LTS（长期支持版本）
渲染管线：Universal Render Pipeline (URP)
着色器风格：Cel Shading（卡通渲染）
```

---

## 二、目录结构

```
Project-Astra/
├── Assets/
│   ├── _Project/                 # 游戏核心资源
│   │   ├── Scenes/              # 场景文件
│   │   │   ├── Prologue.unity   # 序章·远古战场
│   │   │   ├── Chapter01.unity  # 第一章·神树村
│   │   │   └── DevTest.unity    # 开发测试用
│   │   ├── Prefabs/             # 预制体
│   │   │   ├── Characters/      # 角色预制体
│   │   │   ├── Enemies/         # 敌人预制体
│   │   │   ├── Environment/     # 环境物件
│   │   │   └── UI/              # UI 预制体
│   │   ├── Scripts/             # 脚本
│   │   │   ├── Core/            # 核心系统（GameManager 等）
│   │   │   ├── Combat/          # 战斗系统
│   │   │   ├── Character/       # 角色控制
│   │   │   ├── AI/              # 敌方 AI
│   │   │   ├── UI/              # UI 逻辑
│   │   │   └── Data/            # 数据定义（ScriptableObject）
│   │   ├── Art/                 # 美术资源
│   │   │   ├── Models/          # 3D 模型
│   │   │   ├── Textures/        # 贴图
│   │   │   ├── Materials/       # 材质
│   │   │   ├── Shaders/         # Cel Shading 自定义着色器
│   │   │   ├── Animations/      # 动画片段
│   │   │   └── VFX/             # 特效
│   │   ├── Audio/               # 音频
│   │   │   ├── BGM/
│   │   │   ├── SFX/
│   │   │   └── Voice/
│   │   └── Settings/            # URP 渲染设置
│   │       └── URP_Settings.asset
│   └── Plugins/                 # 第三方插件
├── Packages/                    # Package Manager manifest
├── ProjectSettings/             # 项目设置（自动生成）
└── UserSettings/                # 用户个人设置（.gitignore）
```

---

## 三、Package 依赖清单

```json
{
  "dependencies": {
    "com.unity.render-pipelines.universal": "14.0.x",
    "com.unity.inputsystem": "1.7.0",
    "com.unity.cinemachine": "2.9.7",
    "com.unity.textmeshpro": "3.0.6",
    "com.unity.timeline": "1.7.6",
    "com.unity.addressables": "1.21.20",
    "com.unity.shadergraph": "14.0.x",
    "com.unity.animation.rigging": "1.2.1"
  }
}
```

| Package | 用途 |
|---------|------|
| URP | 渲染管线 |
| Input System | 键鼠 + 手柄统一输入 |
| Cinemachine | 第三人称相机（原神风动态镜头） |
| TextMeshPro | 高质量 UI 文字 |
| Timeline | 过场动画编排 |
| Addressables | 资源异步加载（开放世界必需） |
| Shader Graph | Cel Shading 可视化着色器制作 |
| Animation Rigging | IK 绑定（脚踩地面、手部武器） |

---

## 四、渲染配置

### URP Settings

| 设置项 | 默认值 | 说明 |
|--------|--------|------|
| MSAA | 4x | 抗锯齿 |
| Shadow Resolution | 2048 | 主方向光阴影 |
| Shadow Distance | 150m | 阴影最大距离 |
| HDR | On | 支持泛光后处理 |
| Render Scale | 1.0 | 目标分辨率缩放 |
| Soft Shadows | On | 柔和阴影 |

### Cel Shading 配置

```
自定义 Shader Graph 着色器：
- ToonLighting.shadergraph   基础卡通光照（Banded Diffuse + Rim Light）
- ToonOutline.shadergraph    描边效果（Vertex Extrusion 法）
- ToonCharacter.shadergraph  角色完整材质（合并以上两个）
```

### 后处理 Volume 预设
- **序章·远古战场**: 暗红调 · Bloom(低) · Vignette(强) · Film Grain(微弱)
- **第一章·神树村**: 暖色调 · Bloom(中) · Depth of Field(远景微模糊) · Color Grading(温暖偏移)

---

## 五、输入映射（Input System）

```
Action Map: Gameplay

Move         → WASD / 左摇杆
Look         → Mouse Delta / 右摇杆
Attack       → Mouse Left / □
HeavyAttack  → Mouse Right / △
Skill1       → Q / R1+○
Skill2       → E / R1+×
Skill3       → R / R1+△
Skill4       → F / R1+□
Dodge        → Shift / ×
Block        → Space / ○
LockOn       → Tab / R3
Switch1      → 1 / ↑
Switch2      → 2 / ←
Switch3      → 3 / →      (待队友系统完善)
Interact     → E(短按) / △(短按)
Pause        → Esc / Options
```

---

## 六、编码规范

### 命名约定
```
类名: PascalCase        PlayerController.cs
方法: PascalCase        public void DoAttack()
私有字段: _camelCase    private float _moveSpeed;
公共属性: PascalCase    public float MoveSpeed { get; }
常量: UPPER_SNAKE       private const float MAX_HP = 100f;
枚举: PascalCase        public enum ElementType { Fire, Ice, Thunder }
```

### 文件夹命名
```
Scripts/      — 脚本
Materials/    — 材质
Textures/     — 贴图
Prefabs/      — 预制体
```

### 数值规范
```
- 所有数值通过 ScriptableObject 定义（GameData → CharacterStats → num）
- 运行时不得硬编码数值
- 数值文件存于 Assets/_Project/Scripts/Data/ 下
- 原型阶段允许 [PLACEHOLDER] 值，但必须用 // TODO 标记
```

---

## 七、Git 配置

### .gitignore 关键条目
```
/[Ll]ibrary/
/[Tt]emp/
/[Oo]bj/
/[Bb]uild/
/[Bb]uilds/
/[Ll]ogs/
/[Uu]ser[Ss]ettings/
.idea/
.vs/
*.csproj
*.sln
```

### Git LFS（大文件版本控制）
```
*.psd filter=lfs diff=lfs merge=lfs -text
*.fbx filter=lfs diff=lfs merge=lfs -text
*.blend filter=lfs diff=lfs merge=lfs -text
*.tga filter=lfs diff=lfs merge=lfs -text
*.png filter=lfs diff=lfs merge=lfs -text
*.jpg filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.mp3 filter=lfs diff=lfs merge=lfs -text
*.ogg filter=lfs diff=lfs merge=lfs -text
```

---

## 八、搭建检查清单

- [ ] Unity Hub 安装 Unity 2022.3 LTS
- [ ] 新建 URP 项目，命名为 `Project-Astra`
- [ ] 安装上述 Package 依赖
- [ ] 配置 URP Settings（MSAA / Shadow / HDR）
- [ ] 导入 Input System，配置 Gameplay Action Map
- [ ] 设置目录结构（`_Project/` 下全部子目录）
- [ ] 创建 Cel Shading Shader Graph
- [ ] 创建后处理 Volume Profile（序章 + 第一章）
- [ ] 配置 .gitignore + Git LFS
- [ ] 首次构建测试（确保空场景能 Build）

---

## 九、第一步：序章灰盒迁移

Unity 工程就绪后，第一步任务是将 Three.js 灰盒原型（`greybox/prologue-greybox.html`）迁移为 Unity 场景：

1. 创建 `Prologue.unity` 场景
2. 用 Cube/Capsule 搭建 80m 竞技场 + 边界石柱
3. 方块玩家 + WASD 移动（Input System）
4. Cinemachine 第三人称相机
5. E 键拾取剑 → 左键普攻 → Q 辉光斩
6. 简易敌人 AI（追踪 + 近身攻击）
7. Boss 占位 + 节拍系统（Beat 0-5）
8. 大法师 + 女主 NPC 站位
9. 与 Three.js 原型行为一致后再细化

---

**此文档随项目迭代持续更新。每一次 Package 增删、目录结构调整、渲染设置变更，都要同步修改本文件。**
