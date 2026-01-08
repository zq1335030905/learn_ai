# 实验库 (Experiments)

> 用最小实验验证认知，把"我以为"变成"我验证过"。

## 目录结构

```
experiments/
├── templates/
│   └── EXPERIMENT_TEMPLATE.md
├── evals/
│   └── EVAL_TEMPLATE.md
└── foundations/
    └── YYYY-MM-DD-<topic>/
        ├── README.md
        └── code files...
```

## 内容索引

| 实验 | 目录 | 验证假设 | 状态 |
|------|------|----------|------|
| EGL 初始化流程 | `foundations/egl-init/` | 理解 EGL 初始化每个步骤的意义 | ⏳ |
| Context 线程绑定 | `foundations/context-threading/` | 验证 Context 必须绑定当前线程 | ⏳ |
| SurfaceTexture + Camera | `foundations/surface-texture-camera/` | 理解 OES 纹理消费者机制 | ⏳ |

## 实验原则

1. **最小化**：只验证一个核心假设
2. **可复现**：包含完整的运行说明
3. **有结论**：明确支持/反驳假设
4. **有链接**：关联到对应的知识库条目

