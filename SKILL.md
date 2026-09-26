---
name: video-prompt
description: 写或优化视频生成模型的提示词：Seedance/即梦、Kling、Sora、Runway、海螺、Pika、Vidu，含参考图绑定与 Seedance 导演方案、诊断、改写。用户要能直接投喂视频模型的 prompt 时用；生成视频本身、图片提示词、剪辑后期不用。
---

## 动手第一步：先分平台

写或优化任何视频 prompt 之前，**先确定目标平台，再读对应文件**——两派规则相反，搞混两边都拉垮：

- **Seedance / 即梦** → 读 `references/seedance.md`（简派：反故事板、反长 prompt、大白话机位、只出音效）；题材属于产品广告、宠物、打斗、MV、恐怖等 22 类之一时，再读 `references/seedance-genre-recipes.md`
- **Kling / 可灵、Sora、Runway、Hailuo / 海螺、Pika、Vidu** → 读 `references/general.md`（繁派：结构化骨架、分镜序列、运镜术语、颜色对撞）

平台从上下文判断：用户明确说了平台名，以平台名为准；没说时，用了 `@Image N` 素材标签或 `Shot 01` 编号按 Seedance 写。判断不了再问一句：「这是给哪个视频模型用的？」问清再写。

> 为什么必须分：Seedance 吃简洁，华丽故事板 / 长 prompt 丢进去反而错漏百出；Kling 这类吃结构化堆料。同一段 prompt 在两边效果相反。

**再判断模式**（两派通用）：

- **创作**：有想法没 prompt。描述不足就一次性问全（主体外形 / 场景光线 / 情绪基调 / 时长镜头数），够清楚就直接写。
- **优化**：已有 prompt。内部对照找差距，直接输出优化版，不讲分析过程。
- **参考图**：给了图 / 截图 / 卡面 / 角色图，优先级最高，先定每张图用途再写分镜（繁派走资产绑定，图片引用保持用户原样；简派内联进主体 / 镜头行，素材统一标 `@Image N / @Video N / @Audio N`）。

## 文件

- `references/general.md`：繁派骨架、六维度、句式素材库、颜色对撞、运镜词库、参考图绑定、输出铁律
- `references/seedance.md`：简派骨架与硬规则、范例、抽卡策略、出稿前自检、Seedance 2.0 / 2.5 官方补充
- `references/seedance-director-workflow.md`：分档 9 步、素材锁定表、输出模式、秒段规则（2.5 带秒段，2.0 只编号）
- `references/seedance-direction-patterns.md`：参考作用域、因果链、台词预算、延长方向、无缝转场、多宫格、矛盾自检
- `references/seedance-genre-recipes.md`：22 类题材的必写锁、写法、常见问题（写实与手机实拍 / 商业与产品 / 叙事与表演 / 风格化动画 / 动作与奇观）
- `references/seedance-2.0-official.md`、`references/seedance-2.5-official.md`：官方参数硬约束与场景配方
