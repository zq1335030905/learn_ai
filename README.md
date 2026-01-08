# Android Graphics 学习系统

把 Android 图形系统学习做成**可复用的工程资产**：每次会话都有断点、每个概念都有掌握证据、每个主张都尽量可实验/可验证。

## 这套系统的亮点

- **断点续航**：`SESSION_STATE.md` 记录当前 Phase、焦点、下一步待办，下次进来直接从断点继续。
- **可验证的学习闭环**：以「概念地图 → Pattern → 最小实验 → 掌握证据」推进，避免只读不练/只聊不落盘。
- **证据化掌握**：`learning-log/mastery/` + Socratic Check，把"我以为懂了"变成可追溯的掌握记录（✅/🔄/⏳）。

## 60 秒开始一次学习会话

- **开始前**：先读 `SESSION_STATE.md`（断点）与 `roadmap/README.md`（路线与进度）。
- **学习中**：
  - 新概念/边界/反例：写入 `knowledge-base/`
  - 新类比/顿悟/心智模型：写入 `ai-intuition/`
  - 需要验证的想法：做一个最小实验放到 `experiments/`
  - 随手捕捉：先追加到 `learning-log/INBOX.md`，会话结束再收敛
- **结束时**：按 `WORKFLOW.md` 做总结归档（更新日志/路线/断点）。

## 目录结构

```
learn_ai/
├── README.md                 # 本文件
├── WORKFLOW.md               # AI 导师协作准则
├── SESSION_STATE.md          # 会话断点存档
├── ROADMAP.md                # 原始详细路线图（含代码示例）
│
├── roadmap/
│   └── README.md             # 学习路线图与进度追踪
│
├── knowledge-base/           # 知识库（结构化沉淀）
│   ├── foundations/          # 底层原理（EGL / BufferQueue / SurfaceFlinger 等）
│   ├── patterns/             # 应用模式（Camera Preview / Video Render 等）
│   └── concepts/             # 概念辨析（术语表、常见误解）
│
├── ai-intuition/             # 直觉构建（心智模型、类比）
│
├── experiments/              # 实验库
│   ├── templates/            # 实验模板
│   ├── evals/                # 评测模板
│   └── foundations/          # 实验代码
│
├── learning-log/             # 学习日志
│   ├── INBOX.md              # 即时捕捉
│   ├── mastery/              # 掌握证据
│   └── YYYY-MM-DD-*.md       # 每日日志
│
└── prompt/
    └── mentor_system_prompt.md  # AI 导师系统提示词
```

## 学习目标

**一年内系统掌握 Android 图形系统：**

| Phase | 主题 | 时间 |
|-------|------|------|
| Phase 1 | EGL 基础与巩固 | Month 1-2 |
| Phase 2 | BufferQueue 与 Surface 体系 | Month 3-4 |
| Phase 3 | SurfaceFlinger 深入 | Month 5-7 |
| Phase 4 | 硬件加速与 HWUI | Month 8-9 |
| Phase 5 | Vulkan 渲染管线 | Month 10-11 |
| Phase 6 | 综合实践与性能优化 | Month 12 |

详细进度：[`roadmap/README.md`](./roadmap/README.md)

## 核心文件导航

| 文件 | 用途 |
|------|------|
| [`SESSION_STATE.md`](./SESSION_STATE.md) | 会话断点，下次从哪继续 |
| [`WORKFLOW.md`](./WORKFLOW.md) | AI 导师协作准则 |
| [`roadmap/README.md`](./roadmap/README.md) | 学习路线图与进度 |
| [`knowledge-base/foundations/graphics-concept-map.md`](./knowledge-base/foundations/graphics-concept-map.md) | 概念级学习进度 |
| [`knowledge-base/concepts/graphics-glossary.md`](./knowledge-base/concepts/graphics-glossary.md) | 术语表 |
| [`ROADMAP.md`](./ROADMAP.md) | 原始详细路线图（含代码示例和反直觉点） |

## 写作与产出约定

- **概念优先**：先在概念地图里定位，再深入细节，最后落到 Pattern/实验。
- **证据优先**：涉及具体事实（API/源码位置/性能数字）尽量附来源；无法核验就标注"未验证"并留 TODO。
- **输出优先**：每次会话至少沉淀一项可复用资产：概念条目/心智模型/实验/检查清单。

## 前置条件

- 熟悉 OpenGL 渲染管线和基本图形渲染概念
- 有 Android 开发基础
- 可以阅读 AOSP 源码

## 工具链

- **源码导航**：[Android Code Search](https://cs.android.com/)
- **性能分析**：Perfetto, Android GPU Inspector, RenderDoc
- **调试命令**：`adb shell dumpsys SurfaceFlinger`, `adb shell dumpsys gfxinfo`
