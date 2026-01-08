# 底层原理 (Foundations)

> Android 图形系统的核心机制与架构原理。

## 概念地图

→ 详见 [`graphics-concept-map.md`](./graphics-concept-map.md)

## 内容索引

| 主题 | 文件 | 状态 |
|------|------|------|
| EGL 架构 | `egl-architecture.md` | ⏳ |
| BufferQueue 机制 | `buffer-queue.md` | ⏳ |
| SurfaceFlinger | `surface-flinger.md` | ⏳ |
| HWUI 与硬件加速 | `hwui-hardware-acceleration.md` | ⏳ |
| Vulkan 渲染管线 | `vulkan-pipeline.md` | ⏳ |

## 学习顺序建议

1. EGL（桥接层）→ 理解渲染 API 与窗口系统的连接
2. BufferQueue（缓冲机制）→ 理解生产者-消费者模型
3. SurfaceFlinger（合成器）→ 理解系统级渲染流程
4. HWUI（硬件加速）→ 理解应用层渲染优化
5. Vulkan（显式控制）→ 理解现代图形 API 设计

