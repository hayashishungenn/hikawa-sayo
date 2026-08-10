# 冰川纱夜视线机制

## Anchors

- 脚底、膝盖高度和下半身作为稳定锚点；视线变化主要发生在眼睛、眼睑、刘海、头部和上半身。
- 眼睛是物理眼球结构：眼白、虹膜、瞳孔、眼睑、眼缘和高光一起改变，不叠加新的替换眼睛。
- 头部和颈部只做小幅度跟随，保持脸部比例、刘海形状和发缝身份。
- 冰青长发随头部转动产生连续的滞后和遮挡变化；不使用整只角色旋转。
- 红色领结固定在衣领，随胸口轻微转向并保持与身体连接；不独立漂移。

## Cardinal pose families

- `000` / up：瞳孔和眼球向上，眼睑略抬，额头与下巴轻微上提；身体基本正面。
- `090` / screen-right：鼻尖、瞳孔和脸部朝屏幕右侧，屏幕右侧脸更显著，远侧眼睛略被鼻梁/刘海遮挡。
- `180` / down：瞳孔向下，眼睑下压，下巴轻收，刘海对眼睛形成自然遮挡；脚底锚点不变。
- `270` / screen-left：鼻尖、瞳孔和脸部朝屏幕左侧，屏幕左侧脸更显著，远侧眼睛略被遮挡。

## Motion budget

The 22.5-degree steps use even, restrained changes. Eye direction leads; head, neck, hair and ribbon follow gradually. Intermediate cells interpolate between adjacent cardinal pose families and must not backtrack, flip sides, or change character scale.
