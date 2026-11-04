# video-prompt

Claude Code / Codex 视频提示词 skill：分平台写出可直接粘进 Seedance / 即梦、Kling、Sora 的 prompt

[![License](https://img.shields.io/github/license/ZhongBiao-zheng/video-prompt?color=111111)](LICENSE) [![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-111111)](https://skills.sh/zhongbiao-zheng/video-prompt/video-prompt) [![Codex](https://img.shields.io/badge/Codex-skill-111111)](https://skills.sh/zhongbiao-zheng/video-prompt/video-prompt)

把想法、粗糙描述或已有 prompt 交给 agent，video-prompt 先判断目标视频平台，再按该平台的规则写出能直接粘贴的 prompt。除了写新 prompt，也能出导演方案、诊断冲突、按原结构改写。它只产出文本：不调用视频模型，不写图片提示词，不做剪辑后期。

## 为什么用 video-prompt

- **按平台换写法**：Seedance / 即梦 用 12 段详写骨架，Kling、Sora 等用结构化繁派骨架。两派规则相反，同一段 prompt 放错平台效果会变差。
- **一句话想法也能起稿**：描述不足时一次问全主体、场景、情绪、时长；描述够了直接写。
- **常见题材有配方**：产品广告、宠物、打斗、MV、恐怖等 22 类题材，自动补数量锁、相机缺陷清单和对应禁止项。
- **参考图先定用途**：给了角色图、场景图，先确定每张图管什么，再写分镜，素材统一标 `@Image N`。

只想直接生成视频，或者要写图片提示词，用不到它。

## 安装

```bash
npx skills add ZhongBiao-zheng/video-prompt
```

或手动放到 skills 目录：

```bash
git clone https://github.com/ZhongBiao-zheng/video-prompt ~/.claude/skills/video-prompt
ln -s ~/.claude/skills/video-prompt ~/.codex/skills/video-prompt   # Codex 共用同一份
```

## 使用

对 agent 说：

- 「帮我写个 Seedance 15 秒的视频提示词：……」
- 「把这段 Kling 提示词改成即梦能用的」
- 「给我一个 30 秒的导演方案，素材是图1 主角、图2 场景」
- 「只诊断这段提示词哪里冲突」
- 「写个即梦 15 秒的宠物抢镜手机实拍」（命中题材配方，自动补数量锁、相机缺陷清单和对应禁止项）

平台从上下文判断，判断不了会先问一句。Seedance 支持 5 种输出：只要提示词（默认）/ 导演方案 / 只要脚本 / 只诊断 / 按原结构改写。

## 工作原理

先分平台，再读对应规则文件：

| 平台 | 规则文件 | 特点 |
|------|------|------|
| Seedance / 即梦 | `references/seedance.md`（详写骨架）+ `references/seedance-genre-recipes.md`（题材配方） | 12 段：写死人数、参考用途、空间地图、首帧站位、按秒节拍、行为式表演、只出音效不出 BGM |
| Kling / 可灵、Sora、Runway、Hailuo、Pika、Vidu、纯文字 | `references/general.md`（繁派） | 总纲句 + 场景妆造 + 分镜序列 + 后期；运镜术语「中文（英文）」、颜色对撞 |

Seedance 输出骨架：

```
[一行全局意图：风格 / 媒介 / 光影质感，谁在哪做什么]

主体：[名]@Image 1（关键特征 + 负面约束）
[题材锁：相机 / 产品 / 画风 / 节奏，命中题材配方时才写]
场景：[关键词]
音乐：不要任何背景音乐，只生成对应音效

Shot 01（0-3s）：[机位/景别大白话] + [发生什么]。   ← 2.5 带秒段；2.0 只写 Shot 01
Shot 02（3-6s）：……
（≥30s 写成 Shot 01【阶段功能】（0-4s））

约束：[全片锁什么 + 禁止什么]
```

## 文件结构

```
SKILL.md                                   分平台、判模式、路由到下面的文件
references/general.md                      繁派：骨架 / 六维度 / 句式素材 / 颜色对撞 / 运镜词库 / 参考图绑定
references/seedance.md                     详写骨架：12 段写法 / 敏感词 / 范例 / 自检 / 2.0 与 2.5 官方补充
references/seedance-2.0-official.md        官方参数硬约束 / @素材指挥语法
references/seedance-2.5-official.md        官方场景配方（真人脸 / 30s / 延长 / 编辑 / 白模 / 转场）
references/seedance-director-workflow.md   分档 9 步 / 素材锁定表 / 输出模式 / 秒段规则
references/seedance-direction-patterns.md  参考作用域 / 因果链 / 台词预算 / 无缝转场 / 矛盾自检
references/seedance-genre-recipes.md       22 类题材配方：必写锁 / 写法 / 常见问题
evals/evals.json                           17 个测试用例（prompt + 预期 + 断言）
```

## 来源与致谢

- Seedance 详写骨架：改写自 Higgsfield Studio《HELL GRIND》Project Brief 的制作方法（2026-08）
- Seedance 早期简派心法（保留音效、故事板、分辨率结论）：[@simonxxoo 实测心得](https://x.com/ring_hyacinth/status/2076284324345987386)（@ring_hyacinth 转述，2026-07）
- 官方配方：即梦 Seedance 2.0 / 2.5 使用手册（字节跳动）
- 导演流程与手法：[liyue-aigc/seedance-2-5-video-director](https://github.com/liyue-aigc/seedance-2-5-video-director)（MIT）
- 题材配方：改写自 [LearnPrompt/awesome-seedance](https://github.com/LearnPrompt/awesome-seedance) 的分类模板（策展内容 CC BY 4.0，awesome-seedance / goodcase.ai）

## 许可证

[MIT](LICENSE)
