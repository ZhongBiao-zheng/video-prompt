# video-prompt

AI 视频生成提示词 skill：给 Claude Code / Codex 等 agent 用，把想法或粗糙描述改写成能直接粘进视频平台的 prompt。

核心判断只有一条：**先分平台，两派规则相反。**

| 平台 | 走法 | 特点 |
|------|------|------|
| Seedance / 即梦 | B 节（简派） | 一头 + 四段 + 一尾；Shot 只编号、大白话机位、只出音效不出 BGM、不堆形容词 |
| Kling / 可灵、Sora、Runway、Hailuo、Pika、Vidu、纯文字 | A 节（繁派） | 总纲句 + 场景妆造 + 分镜序列 + 后期；运镜术语「中文（英文）」、颜色对撞 |

## 安装

```bash
npx skills add ZhongBiao-zheng/video-prompt
```

或手动放到 skills 目录：

```bash
git clone https://github.com/ZhongBiao-zheng/video-prompt ~/.claude/skills/video-prompt
```

Codex 共用：`ln -s ~/.claude/skills/video-prompt ~/.codex/skills/video-prompt`。

## 使用

对 agent 说：

- 「帮我写个 Seedance 15 秒的视频提示词：……」
- 「把这段 Kling 提示词改成即梦能用的」
- 「给我一个 30 秒的导演方案，素材是图1 主角、图2 场景」
- 「只诊断这段提示词哪里冲突」

没说平台会先问一句。Seedance 支持 5 种输出：只要提示词（默认）/ 导演方案 / 只要脚本 / 只诊断 / 按原结构改写。

Seedance 输出骨架：

```
[一行全局意图：风格 / 媒介 / 光影质感，谁在哪做什么]

主体：[名]@Image 1（关键特征 + 负面约束）
场景：[关键词]
音乐：不要任何背景音乐，只生成对应音效

Shot 01：[机位/景别大白话] + [发生什么]。
Shot 02：……
（≥30s 写成 Shot 01【阶段功能】）

约束：[全片锁什么 + 禁止什么]
```

## 文件

```
SKILL.md                                   路由 + A 节 + B 节
references/seedance-2.0-official.md        官方参数硬约束 / @素材指挥语法
references/seedance-2.5-official.md        官方场景配方（真人脸 / 30s / 延长 / 编辑 / 白模 / 转场）
references/seedance-director-workflow.md   分档 9 步 / 素材锁定表 / 输出模式 / 时间轴模式
references/seedance-direction-patterns.md  参考作用域 / 因果链 / 台词预算 / 无缝转场 / 矛盾自检
evals/evals.json                           11 个测试用例（prompt + 预期 + 断言）
```

## 来源与致谢

- Seedance 简派心法：[@simonxxoo 实测心得](https://x.com/ring_hyacinth/status/2076284324345987386)（@ring_hyacinth 转述，2026-07）
- 官方配方：即梦 Seedance 2.0 / 2.5 使用手册（字节跳动）
- 导演流程与手法：[liyue-aigc/seedance-2-5-video-director](https://github.com/liyue-aigc/seedance-2-5-video-director)（MIT）

## License

MIT
