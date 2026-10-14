# 冰川纱夜 Codex Pet

`冰川纱夜` · `氷川紗夜` · `ひかわ さよ` · `ひかわさよ` · `Hikawa Sayo` · `Sayo Hikawa` · `Roselia`

这是一个 Codex Pet v2。同人风格角色来自用户提供的新底稿，描述与角色定位参考《BanG Dream!》官方设定：纱夜是认真冷静、对己对人都严格的 Roselia 吉他手，持续磨练琴艺，在游戏与点心制作上也从不妥协。[官方角色页](https://bang-dream.com/artist/roselia/hikawa-sayo/)

角色视觉保留冰青色长发、绿色眼睛、棕色制服、白色水手领与红色领结，并为 Codex 的标准工作状态制作了连续动作和 16 个视线方向。

## 2026-10 头发边缘细节修复

已用 imagegen 重绘全部标准动作组与视线，清理头发边缘的白色高光和透明缺口。保留原角色服装与动作顺序；左右跑步行经过二次轮廓修复。

- [安装包](hikawa-sayo-pet.zip) · [待机预览](qa/previews/idle.gif) · [向右跑预览](qa/previews/running-right.gif)。
- [本次 QA 摘要](qa/hair-edge-fix-20261013/run-summary.json) · [逐格视觉复核](qa/hair-edge-fix-20261013/final-visual-review.json)。
- 最终图集 SHA-256：`03ea7cc0b7ac8e80fdf6fc38d45d545ad369ad0c8411124f10bafc6805da24a0`。
- 已复核 74 个使用单元格及 9 组 GIF 的全部 57 帧。原生 Codex 识别、激活与实时播放仍未验证。

本次为原版的细节修复，名称仍为“冰川纱夜”，ID 仍为 `hikawa-sayo`。本仓库和本地安装已直接替代旧素材；网站原条目的图集替换待完成。

当前图集与预览已替代原版素材。`qa/hair-edge-fix-20261013/` 为本次证据，其他旧版 QA 记录保留作历史参考。

## 内容

- 可安装的 `pet.json` 与 `spritesheet.webp`。
- 9 个标准状态：`idle`、`running-right`、`running-left`、`waving`、`jumping`、`failed`、`waiting`、`running`、`review`。
- 16 个连续视线方向：`000` 到 `337.5`，每步 22.5°。
- [设计说明](DESIGN.md)、[最终 contact sheet](qa/contact-sheet-extended.png)、[视线 QA](qa/look-directions.png) 和 [QA 摘要](qa/run-summary.json)。

## 安装

将 `pet.json` 和 `spritesheet.webp` 复制到：

```text
%USERPROFILE%\.codex\pets\hikawa-sayo\
```

重启 Codex，在 Pets 设置中选择“冰川纱夜”。安装目录只需要这两个文件；仓库中的 `qa/` 是设计与验证记录，不需要复制到 Pet 目录。

## v2 规格

- 图集：8 列 × 11 行。
- 单格：192 × 208；完整尺寸：1536 × 2288。
- 格式：透明 RGBA WebP。
- manifest：`spriteVersionNumber: 2`。
- 不包含悬浮层、用量条、额外运行时逻辑或自定义 UI。

## QA

最终图集已通过 v2 尺寸、透明度、色键残留和组件完整性检查；标准状态与 16 方向均保留了 contact sheet、动画预览和确定性 JSON 记录。少量 stable-slots 与视线连续性 review warning 已记录在 [blind-review-resolution.json](qa/blind-review-resolution.json)，没有硬性失败项。

## 版权与使用

这是个人使用的同人风格资产，原条目见 [Codex Pets Gallery](https://codex-pets.net/#/pets/hikawa-sayo)。仓库不包含商标、Logo、文字或第三方 UI 资产；如需进一步公开分发，请先确认角色版权、底稿授权和平台发布要求。
