# Android Graphics 术语表

> 关键术语的标准化定义。格式：英文术语 | 中文翻译 | 一句话解释

---

## EGL 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| EGL | EGL | 连接渲染 API 与原生窗口系统的桥接层标准 |
| EGLDisplay | EGL 显示连接 | 与物理显示设备的连接抽象 |
| EGLSurface | EGL 表面 | 渲染目标表面，可以是窗口、离屏缓冲或 Pixmap |
| EGLContext | EGL 上下文 | OpenGL ES 状态机容器，必须绑定到线程才能使用 |
| EGLConfig | EGL 配置 | 帧缓冲配置，指定颜色/深度/模板位数 |
| EGLImage | EGL 图像 | 跨进程/跨 API 共享图像资源的机制 |
| eglMakeCurrent | 绑定上下文 | 将 EGLContext 绑定到当前线程的操作 |

---

## BufferQueue 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| BufferQueue | 缓冲队列 | 生产者-消费者模型的图形缓冲区队列 |
| GraphicBuffer | 图形缓冲区 | 可跨进程共享的图形内存缓冲区 |
| Producer | 生产者 | 向 BufferQueue 提交帧的一方（如 App、Camera） |
| Consumer | 消费者 | 从 BufferQueue 获取帧的一方（如 SurfaceFlinger） |
| dequeueBuffer | 出队缓冲区 | 生产者从队列获取空闲 Buffer 的操作 |
| queueBuffer | 入队缓冲区 | 生产者将已填充 Buffer 提交到队列的操作 |
| acquireBuffer | 获取缓冲区 | 消费者从队列获取待处理 Buffer 的操作 |
| releaseBuffer | 释放缓冲区 | 消费者将已处理 Buffer 归还队列的操作 |
| Fence | 同步栅栏 | GPU/CPU 同步原语，确保操作完成后才继续 |
| Acquire Fence | 获取栅栏 | 标记 Buffer 可被消费者读取的信号 |
| Release Fence | 释放栅栏 | 标记 Buffer 可被生产者重新使用的信号 |

---

## Surface 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| Surface | 表面 | ANativeWindow 的 Java/Native 实现，渲染目标 |
| ANativeWindow | 原生窗口 | Native 层的窗口抽象接口 |
| SurfaceTexture | 表面纹理 | 将 Surface 内容转为 GL 纹理的机制 |
| SurfaceView | 表面视图 | 拥有独立 Surface 的 View，独立于 View 层级渲染 |
| TextureView | 纹理视图 | 将 Surface 内容作为纹理显示的 View |
| GL_TEXTURE_EXTERNAL_OES | OES 外部纹理 | SurfaceTexture 使用的特殊纹理类型 |
| Gralloc | 图形分配器 | 图形内存分配器 HAL |

---

## SurfaceFlinger 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| SurfaceFlinger | 表面合成器 | Android 系统的图形合成服务 |
| Layer | 图层 | 合成层抽象，一个可见的绘制表面 |
| BufferLayer | 缓冲图层 | 带有 BufferQueue 的图层 |
| ColorLayer | 颜色图层 | 纯色填充的图层 |
| ContainerLayer | 容器图层 | 只用于组织子图层的容器 |
| Transaction | 事务 | 原子提交多个图层属性变更的机制 |
| VSync | 垂直同步 | 显示器刷新时产生的同步信号 |
| VSYNC-app | 应用垂直同步 | 通知应用开始渲染的 VSync 信号 |
| VSYNC-sf | 合成器垂直同步 | 通知 SurfaceFlinger 开始合成的 VSync 信号 |
| Choreographer | 编排器 | 应用层接收 VSync 并调度渲染的组件 |
| CompositionEngine | 合成引擎 | SurfaceFlinger 的合成逻辑模块 |

---

## HWC 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| HWC | 硬件合成器 | Hardware Composer，硬件合成 HAL |
| Device Composition | 设备合成 | 使用显示硬件（DPU）进行的合成 |
| Client Composition | 客户端合成 | 使用 GPU 进行的合成 |
| Overlay | 叠加层 | 硬件合成器支持的独立显示层 |
| DPU | 显示处理单元 | Display Processing Unit，专用显示硬件 |

---

## HWUI 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| HWUI | 硬件UI库 | Android 的硬件加速 UI 渲染库 |
| RenderThread | 渲染线程 | 专门执行 GPU 渲染命令的线程 |
| DisplayList | 显示列表 | 记录的绘制命令序列 |
| RenderNode | 渲染节点 | 渲染树中的节点，包含 DisplayList |
| RecordingCanvas | 录制画布 | 用于记录绘制命令而非立即执行的 Canvas |
| Skia | Skia | Google 的 2D 图形引擎 |
| Hardware Layer | 硬件图层 | 将 View 渲染到独立纹理的机制 |

---

## Vulkan 相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| VkInstance | Vulkan 实例 | Vulkan 库的实例化对象 |
| VkPhysicalDevice | 物理设备 | GPU 硬件的抽象 |
| VkDevice | 逻辑设备 | 与物理设备的逻辑连接 |
| VkQueue | 命令队列 | 提交命令到 GPU 的队列 |
| VkCommandBuffer | 命令缓冲区 | 记录 GPU 命令的缓冲区 |
| VkSwapchain | 交换链 | 管理用于显示的图像队列 |
| VkRenderPass | 渲染通道 | 描述渲染过程中 attachment 使用方式 |
| VkPipeline | 管线 | 完整的图形管线状态对象 |
| VkDescriptorSet | 描述符集 | 着色器资源绑定的集合 |
| VkFence | 栅栏 | CPU 等待 GPU 完成的同步原语 |
| VkSemaphore | 信号量 | GPU 队列间的同步原语 |
| Pipeline Barrier | 管线屏障 | 命令间的执行依赖和内存可见性控制 |

---

## 性能分析相关

| 英文术语 | 中文翻译 | 一句话解释 |
|----------|----------|-----------|
| Jank | 卡顿 | 帧渲染超时导致的视觉卡顿 |
| Frame Drop | 掉帧 | 未能在 VSync 周期内完成渲染 |
| Overdraw | 过度绘制 | 同一像素被多次绘制 |
| Triple Buffering | 三重缓冲 | 使用三个缓冲区的策略，减少等待 |
| Perfetto | Perfetto | Android 系统级性能追踪工具 |
| Systrace | 系统追踪 | Android 系统追踪工具（Perfetto 前身） |

---

## 更新记录

- **2026-01-07**：初始创建，包含 EGL/BufferQueue/Surface/SurfaceFlinger/HWC/HWUI/Vulkan 核心术语

