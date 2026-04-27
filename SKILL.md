---
name: dark-fantasy
description: Generate high-quality AI art prompts for anime gacha game characters, optimized for ChatGPT Image2 (GPT-4o with image generation). Converts brief character descriptions into copy-paste positive/negative prompts. Covers character portraits, profile cards, gacha pull screens, and multi-variant illustration sets. Compatible with Midjourney and Stable Diffusion. Use when the user wants to create anime-style game character prompts, generate 二游 prompts, or needs structured prompts for AI image generation of anime characters. Triggers on requests like "生成提示词", "画一个角色", "二游 prompt", "gacha prompt", or the command "/dark-fantasy".
---

# 二游AI绘画提示词生成器

Convert user-provided character descriptions into professional AI art prompts for anime gacha game characters.

## Input

User provides a character description (name, identity/archetype, optional appearance keywords).

Examples:
- "恶堕修女"
- "冰霜女王 伊莎贝拉，银发红瞳"
- "暗黑修女 艾莉丝，破损圣衣"

## Workflow

### Step 1: Receive Character

Display welcome message and wait for user input.

### Step 2: Derive + Confirm

Parse the character description and derive:

| Dimension | Derivation Rules |
|-----------|-----------------|
| Identity | Queen → 女王 / Nun → 神职 / Succubus/Fallen → 恶堕 / Warrior → 战士 / Mage → 法师 / God → 神明 |
| Faction | Holy → 神圣 / Dark → 黑暗 / Ice → 冰霜 / Nature → 自然 / Royal → 王权 / Magic → 魔法 |
| Temperament | Holy(A) / Elegant(B) / Seductive(C) / Dignified(D) / Dark(E) |
| Costume | Derived from identity + faction |
| Pose | Derived from faction + temperament |
| Background | Derived from faction |
| UI Color Scheme | Derived from faction (see color mapping below) |
| Style Preset | Derived from identity + faction + temperament |

Display derivation results. Ask user to confirm or adjust.

Options:
1. Confirm → Step 3
2. Adjust → revise and re-confirm
3. Fast mode → skip to Step 3 with derived defaults
4. Multi-variant mode → show variant plan first, then generate all

**Twin character mode**: If input contains "双子/双人/姐妹/姐弟/羁绊/双生/一对", derive two characters separately with interaction poses.

### Step 3: Generate Prompts

Generate **Positive Prompt** (5-segment) + **Negative Prompt** (standalone).

---

## Positive Prompt Format (5 Segments)

### Segment 1: Style & Quality Tags (English)

Fixed opening:
```
highly detailed anime illustration, dark fantasy, gothic fantasy, [UI-type tag], central composition, [aspect-ratio tag], masterpiece, best quality, absurdres, ultra detailed, sharp focus
```

UI-type tags:
- Character profile UI: `gacha game character profile screen`
- Character card UI: `gacha game character card`
- Gacha pull UI: `gacha game gacha pull screen`

Aspect-ratio tags:
- 16:9 horizontal: `16:9 horizontal composition`
- 9:16 vertical: `9:16 vertical composition`
- 1:1 square: `1:1 square composition`

### Segment 2: Character Core (Pure Chinese Narrative)

**CRITICAL**: Describe pose as a continuous spatial narrative in Chinese. Forbidden: English pose tags.

Write in sequence: **body orientation → ground contact → limb positions → head direction → expression**

**Correct** (continuous narrative):
```
画面中央是一位不洁修女，她侧躺在崩塌的暗黑大教堂地面上，身体完全朝向左侧，左肩和左腿贴地，右手臂自然枕在头下撑住头部托腮，左手轻抬勾弄一缕银黑渐变发丝，头部轻转向镜头回眸，眼神冰冷魅惑。
```

**Wrong** (tag堆砌 — causes pose deviation):
```
lying on side, head supported by hand, looking back over shoulder...
```

**Pose rules**:
1. Chinese narrative only. No English pose tags in this segment.
2. Specify body-ground contact: "左肩贴地", "右腿弯曲", "胸口朝向地面".
3. For ambiguous poses (side-lying vs stomach-lying), add exclusion: "身体完全侧向，不是趴在地上".
4. Expressions must carry contradictory tension: "悲悯、虔诚、禁欲、堕落、神圣与邪异并存".

### Segment 3: Costume & Material (Chinese + English Tags)

```
[发色] [发型描述]，[服装主描述]，[配饰细节]，[特殊标记]。intricate lace texture, ornate metal details, rich texture, polished rendering。
```

Required material tags: `intricate lace texture`, `ornate metal details`, `rich texture`, `polished rendering`.

### Segment 4: Background & Lighting (Chinese + English Tags)

**Background Faction Adaptation**: The background environment and color tone must match the character's faction to create visual harmony:

| Faction | Background Environment | Color Tone | Atmosphere |
|---------|----------------------|------------|------------|
| 神圣 (Holy) | cathedral, holy light, divine pillars | warm golden light | 神圣光辉，教堂穹顶 |
| 黑暗 (Dark) | gothic ruins, crimson moon, dark throne | dark red-black | 暗黑废墟，血月王座 |
| 冰霜 (Ice) | frozen palace, ice crystals, aurora | ice blue-silver | 冰封宫殿，极光晶体 |
| 自然 (Nature) | ancient forest, glowing vines, moonlight | emerald green | 古树森林，月光藤蔓 |
| 王权 (Royal) | throne room, royal banners, golden hall | gold-purple | 王座大厅，金色宫殿 |
| 魔法 (Magic) | arcane library, floating runes, mystical void | deep blue-purple | 奥术图书馆，符文虚空 |
| 火焰 (Fire) | volcanic throne, lava flows, ember sky | orange-red | 火山王座，熔岩天空 |
| 雷电 (Thunder) | storm citadel, lightning pillars, electric sky | electric purple | 风暴城堡，雷电天空 |

**Important**: Choose the background environment and color tone that matches the character's faction from the table above.

```
[背景环境描述 - 根据阵营选择]，[光影系统描述 - 根据阵营色调]，cinematic lighting, volumetric light, rim light, high contrast, glowing particles, reflective floor, dramatic atmosphere。
```

Required lighting tags: `cinematic lighting, volumetric light, rim light, high contrast`.

### Segment 5: UI Overlay (If Applicable)

**UI Color Scheme Mapping** (adapt frame colors to character faction):

| Faction | UI Frame Colors | Accent Colors | Description |
|---------|----------------|---------------|-------------|
| 神圣 (Holy) | gold + ivory white | soft golden glow | 金色与象牙白边框，柔和金色光晕 |
| 黑暗 (Dark) | black + crimson red | red cracks | 黑金边框，镶嵌赤红裂纹 |
| 冰霜 (Ice) | silver + ice blue | frost patterns | 银色与冰蓝色边框，霜花纹样 |
| 自然 (Nature) | emerald green + gold | leaf patterns | 翠绿与金色边框，叶纹装饰 |
| 王权 (Royal) | gold + deep purple | royal patterns | 金色与深紫色边框，王室纹章 |
| 魔法 (Magic) | deep blue + purple | arcane glyphs | 深蓝与紫色边框，奥术符文 |
| 火焰 (Fire) | gold + orange-red | flame patterns | 金色与橙红色边框，火焰纹样 |
| 雷电 (Thunder) | silver + electric purple | lightning | 银色与电紫色边框，闪电纹路 |

**Important**: Replace the fixed "黑金哥特雕花风，镶嵌赤红裂纹与暗纹" with the faction-specific color scheme from the table above.

Character profile UI:
```
完整游戏UI叠层，左侧角色稀有度与信息面板，巨大金色SSR发光字样、星级、属性图标；右侧基础属性、技能图标、专属武器面板；底部costume/skin切换栏与功能按钮。UI边框为[根据阵营使用对应配色方案]哥特雕花风。
```

Character card UI:
```
完整的游戏角色卡牌界面，左上角显示稀有度标识与星级，下方显示角色名称。左侧占据大部分画面的大型角色立绘展示区。右侧排列多个小方框展示角色不同角度特写。底部显示角色介绍文本框。UI边框为[根据阵营使用对应配色方案]哥特雕花风。
```

Gacha pull UI:
```
完整的二次元手游抽卡招募界面，限定SSR角色概率UP活动海报UI。左上角活动横幅展示限时UP标识。左侧超大中文宣传标题位于画面左上方，标题下方有副标语飘带装饰。画面中央偏右是[角色名]大立绘，角色从金色与紫色光芒中登场，周围环绕光效粒子和能量流。右上角显示概率UP和活动时间。右侧竖向排列限定特典奖励栏，包含角色头像方框、专属武器卡片、契约道具图标、结晶资源图标四个奖励方框。左下角有限定标识、巨大SSR稀有度发光字样、角色名、CV信息和简介文本区。底部中央有两个巨大按钮分别为召唤一次和召唤十次，按钮旁边有保底计数框显示当前抽取次数。右下角有必出SSR圆形徽章。整体UI边框为[根据阵营使用对应配色方案]哥特雕花风，带金属浮雕、发光描边、装饰角花。整体必须是完整抽卡页面，不是普通角色海报，充满动态感和视觉冲击力，像高端二次元手游抽卡界面截图。
```

---

## Negative Prompt

Standard:
```
lowres, bad anatomy, bad hands, error, missing fingers, extra digit, fewer digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark, username, blurry, bad feet, mutation, deformed, extra limbs, extra arms, extra legs, malformed limbs, fused fingers, too many fingers, long neck, cross-eyed, mutated hands, polar lowres, bad face, out of frame, oversaturated, overexposed
```

Additional exclusions by character type:
- Non-human features (wings/horns/tail): `floating wings, detached horns, floating tail, bad anatomy`
- Complex costume: `clothes mismatch, asymmetrical clothes, missing accessories`
- Exclude readable text/watermark: `gibberish text, garbled text, nonsense text, unreadable symbols, corrupted characters, english text, watermark, signature, logo, artist name, copyright`

**Important**: Exclude garbled/corrupted text and English text, but allow natural Chinese UI text to appear.

---

## Multi-Variant Mode (Optional)

When user selects multi-variant mode in Step 2, generate 3 variants:

| Element | Variant 1 (Surface) | Variant 2 (Awakened) | Variant 3 (Truth) |
|---------|--------------------|---------------------|------------------|
| Expression | Pure/confident | Resolute/powerful | Cold/seductive/real |
| Costume | Fully concealed | Partial reveal | Full exposure |
| Pose | Standard classic | Dynamic advanced | Unconventional |
| Background | Bright/solemn | Explosive/energetic | Dark/abyssal |
| Lighting | Warm/soft | Burst/energy | Dark/rim light |

Output each variant's full positive + negative prompt independently.

---

## Core Rules

1. **English tags ONLY for**: style (dark fantasy, gothic fantasy), quality (absurdres, ultra detailed), lighting (cinematic lighting, rim light), material (intricate lace texture). Never for pose description.
2. **Pose library codes** (e.g., 4.2, H3, M11) are for internal reference only. Expand to full Chinese spatial narrative in output.
3. **Side-lying vs stomach-lying MUST be distinguished**: side-lying = shoulder/hip on ground; stomach-lying = belly/chest on ground. Always add exclusion clause for ambiguous poses.
4. **Faction-based color adaptation**: Background environment, lighting color tone, and UI frame colors must match the character's faction. Use the mapping tables in Segment 4 and Segment 5.
5. **Non-human anatomy**: If character has wings/horns/tail/mechanical limbs, explicitly state attachment point in positive prompt.

---

## Reference Files

Load these when generating detailed prompts:

- **Pose library** (`references/poses.md`): Full pose catalog with spatial descriptions and ambiguity exclusions. Read when selecting or describing poses.
- **Color system** (`references/color-system.md`): 6-dimension style control (ornateness, saturation, temperament, detail, effects, rendering) + aspect ratios.
- **UI specifications** (`references/ui-specs.md`): UI type details + pose conflict warnings + anti-breakage guidelines.
- **Examples** (`examples/`): Complete sample outputs for reference.
