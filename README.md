# 冰川纱夜 Codex Pet

这是一个个人本地使用的 Codex Pet v2。同人风格角色保留了新底稿中的冰青长发、绿色眼睛、棕色制服、白色水手领与红色领结，并为 Codex 的标准工作状态制作了连续动作和视线方向。

## 安装

将 `pet.json` 和 `spritesheet.webp` 复制到：

```text
%USERPROFILE%\\.codex\\pets\\hikawa-sayo\\
```

然后重启 Codex，在 Pets 设置中选择“冰川纱夜”。仓库中的 `qa/` 保存了最终图集、状态 contact sheet、视线语义图、盲测结果和确定性校验结果。

## 版本约束

- v2 图集：8 列 × 11 行，每格 192 × 208，最终 1536 × 2288。
- 标准状态：`idle`、`running-right`、`running-left`、`waving`、`jumping`、`failed`、`waiting`、`running`、`review`。
- 视线行：16 个连续方向，按 22.5° 从 `000` 到 `337.5` 顺序排列。

本包不包含悬浮层、用量条、额外运行时逻辑或自定义 UI。
