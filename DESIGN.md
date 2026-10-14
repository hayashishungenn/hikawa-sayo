# 冰川纱夜 Codex Pet v2 设计说明

## 2026-10 修订

当前安装图集为头发边缘细节修复。标准动作组从原版逐组编辑，16 个视线重新绘制，保留角色识别特征与服装。左右跑步最后再绘制一次，将触及外轮廓的白色高光改为青绿色。本次证据见 `qa/hair-edge-fix-20261013/`，其余 QA 文档描述初版。

安装包与图集的 SHA-256、尺寸和 manifest 均已回读核对。原生应用识别与实时动画播放未验证。下文底稿、生成目录和初版 QA 说明是历史记录。

## 交付范围

本仓库交付一个可安装的 Codex Pet v2：

- `pet.json`：兼容性最好的标准 manifest 字段。
- `spritesheet.webp`：8 × 11、每格 192 × 208、1536 × 2288 的透明 RGBA 图集。
- `qa/`：图集校验、去色键溢出、状态 contact sheet、动画预览、16 方向视线图、连续性测量与三路盲测记录。
- `README.md`：本地安装说明。

角色唯一参考底稿是仓库中的 `ChatGPT Image 2026年8月10日 15_45_57.png`。旧底稿对应的运行目录没有被用于最终包；最终图集、QA 与安装包均来自新底稿版本 `hikawa-sayo-v2-154557`。

## 官方设定对齐

manifest 的描述采用 BanG Dream! 官方角色页对冰川纱夜的设定转述：她是认真冷静、对自己和他人都严格的 Roselia 吉他手，持续磨练自己的琴艺，并且在游戏与点心制作上也不妥协。[官方角色页](https://bang-dream.com/artist/roselia/hikawa-sayo/)

Codex Pet 的编码伴侣行为只是承载角色动作的应用场景，不把“coding companion”写入角色设定描述，也不替官方设定增加新的身份关系。

名称关键词补全为：`冰川纱夜`、`氷川紗夜`、`ひかわ さよ`、`ひかわさよ`、`Hikawa Sayo`、`Sayo Hikawa` 和 `Roselia`。`pet.json` 保留官方要求的标准字段，并将关键词作为兼容的附加元数据。

## 视觉拆解

新底稿的识别锚点被保留为跨状态不变量：

- 冰青色长发，侧分刘海和波浪发束；左右移动使用独立生成的侧视状态，避免简单镜像破坏发缝方向。
- 绿色大眼睛；视线行让虹膜、瞳孔、眼睑、刘海遮挡和头部朝向共同变化，不叠加替换眼睛贴片。
- 棕色学院制服、白色水手领、红色领结、深色袜鞋。
- 清晰的 chibi 非像素风、略加强的暗轮廓与克制的 cel shading，保证在深色 Codex 背景和小尺寸缩放下仍能辨认。
- 脚底、膝盖高度和下身作为稳定锚点；视线变化由眼睛先动，头部、颈部、刘海、头发和上半身小幅跟随。

不复制参考图中的 Logo、文字或 UI 元素。

## 动作语义

图集标准行按 Hatch Pet v2 契约使用：

| 行 | 状态 | 设计意图 |
| --- | --- | --- |
| 0 | `idle` | 冷静呼吸与轻微头发/衣摆微动 |
| 1 | `running-right` | 面向屏幕右侧的专注移动 |
| 2 | `running-left` | 独立生成的屏幕左侧移动，保持侧分发型身份 |
| 3 | `waving` | 面向用户的短促挥手 |
| 4 | `jumping` | 小幅跃起，脚底离地后回到稳定锚点 |
| 5 | `failed` | 失误后的低头、塌肩与沮丧表情 |
| 6 | `waiting` | 安静等待，呼吸幅度低 |
| 7 | `running` | 正面专注工作，手部保持键盘/编码伴侣语义 |
| 8 | `review` | 检查结果时的抬眼和轻微确认动作 |

标准状态的帧数遵循确定性运行记录：`idle` 6、左右移动各 8、`waving` 4、`jumping` 5、`failed` 8、`waiting` 6、`running` 6、`review` 6。未使用单元格保持透明，不填充伪背景。

## 16 方向视线机制

行 9 和行 10 合计 16 个连续方向：

```text
000 up
022.5 up-right    045 up-right    067.5 up-right    090 screen-right
112.5 down-right  135 down-right  157.5 down-right  180 down
202.5 down-left   225 down-left   247.5 down-left   270 screen-left
292.5 up-left     315 up-left     337.5 up-left
```

四个基准方向使用稳定的 cardinal anchor：`000` 向上、`090` 屏幕右、`180` 向下、`270` 屏幕左。对角方向按 22.5° 顺序渐变，禁止整只角色旋转、突然替换眼睛或让脚底漂移。红色领结与胸口保持连接，头发对头部转向有轻微滞后和遮挡变化。

`qa/direction-semantics.json` 记录了每个方向的期望语义、观察结果和证据。`qa/look-continuity.json` 中的局部像素差异被保留为 review warning；`qa/blind-review-resolution.json` 说明了为什么在标注视线图确认没有可见跳变、反向、裁切或身份断裂后接受这些告警。

## QA 决策

确定性检查结果：

- 图集为 RGBA WebP，8 × 11，`spriteVersionNumber: 2`，1536 × 2288。
- 去色键边缘溢出检查通过，透明 RGB 残留为 0。
- 9 个标准状态均有帧；`failed` 和 `review` 使用 stable-slots 提取并进行过预览复核，保留了“需确认播放稳定”的工具告警。
- 16 方向 continuity checker 为 `ok: true`，但要求人工 review；标注视线图确认四个 cardinal 与全部象限顺序。
- 三路独立盲测的硬 cardinal 对通过；其余少量中间对因对角视线线索细微产生 reviewer 分歧，已写入接受记录，没有未确认项。
- QA 工具产生的 Pillow `DeprecationWarning` 属于工具运行时警告，不影响图集结果。

## 参考与适配边界

- [OpenAI Hatch Pet skill](https://github.com/openai/skills/blob/main/skills/.curated/hatch-pet/SKILL.md)：v2 图集尺寸、行语义、透明图集、确定性 QA 与安装结构的协议来源。
- [冰川纱夜官方角色页](https://bang-dream.com/artist/roselia/hikawa-sayo/)：性格、Roselia 吉他手身份以及对音乐、游戏和点心制作的严谨设定来源。
- [Codex issue #20863](https://github.com/openai/codex/issues/20863)：动画状态由应用侧控制的实现背景；因此 manifest 只使用标准字段。
- [Codex issue #20808](https://github.com/openai/codex/issues/20808)：社区反馈的缩放/重采样伪影关注点；本包针对小尺寸轮廓、透明边缘和暗背景做 QA。
- [Minty Codex Pet](https://github.com/Somnusochi/minty-codex-pet)：社区 v2 图集和本地打包实现的交叉参考。
- [Codex Pets Hatch guide](https://github.com/openai/codex/blob/main/docs/pets.md)：本地 Pet 目录和使用流程参考。
- [Reddit：Pet 设计与可读性经验](https://www.reddit.com/r/codex/comments/1t8va3o/)：用于暗背景、白边和缩放可读性检查。
- [Reddit：多轮迭代经验](https://www.reddit.com/r/codex/comments/1v0xzmi/)：用于保持跨状态身份和颜色一致性。
- [Reddit：实际安装经验](https://www.reddit.com/r/codex/comments/1var8cb/)：用于本地安装与回读验证。

这些社区内容仅作设计与 QA 补充，不改变官方协议字段。

## 版权与使用说明

这是个人使用的同人风格资产，原条目见 [Codex Pets Gallery](https://codex-pets.net/#/pets/hikawa-sayo)。本包不带商标、Logo、文字或第三方 UI 资产；角色视觉根据用户提供的新底稿进行再设计。若要进一步公开分发，应另行确认角色版权、底稿授权和平台发布要求。
