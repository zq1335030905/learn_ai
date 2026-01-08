# EGL（掌握证据）

- **对应知识库条目（KB）**：[`EGL 架构`](../../knowledge-base/foundations/egl-architecture.md)（待创建）
- **掌握状态**：🔄

## 我的复述（一句话）

> EGL 是连接渲染 API（OpenGL ES）与原生窗口系统的桥接层，负责管理渲染表面和渲染上下文。

## 我的解释（What / Why / How）

- **What**：EGL 是 Khronos 定义的平台无关接口，用于连接 OpenGL ES 与原生窗口系统
- **Why**：OpenGL 只定义"怎么画"，不定义"画到哪里"；EGL 填补了这个空缺
- **How**：
  1. eglGetDisplay() - 获取显示连接
  2. eglInitialize() - 初始化 EGL
  3. eglChooseConfig() - 选择帧缓冲配置
  4. eglCreateWindowSurface/PbufferSurface() - 创建渲染表面
  5. eglCreateContext() - 创建渲染上下文
  6. eglMakeCurrent() - 绑定 Context 到当前线程

## 我最容易搞错的点

- 以为后台线程可以不用 Surface 直接使用 GL（实际上 makeCurrent 必须有 Surface）
- 以为 eglMakeCurrent 会创建 Surface（实际上它只绑定已存在的 Surface）

## Socratic Check（我已回答的题目）

- **Q**：为什么 OpenGL ES 不能直接渲染到屏幕，必须通过 EGL？
  - **A（我的回答）**：因为 OpenGL ES 是用来渲染画面，但是渲染到哪个窗口/帧缓冲由 EGL 来控制。✅

- **Q**：EGLDisplay 代表的是物理显示器吗？
  - **A（我的回答）**：不代表物理显示器，它代表的是显示系统的连接抽象。✅

- **Q**：如果你在线程 A 创建了 EGLContext，想在线程 B 中使用它，需要做什么？
  - **A（我的回答）**：先在线程 A 调用 eglMakeCurrent 解绑（使用 EGL_NO_CONTEXT），然后在线程 B 调用 eglMakeCurrent 绑定。✅（纠正后）

- **Q**：在共享 Context 中，VAO 能共享吗？VBO 能共享吗？
  - **A（我的回答）**：VAO 不能共享，VBO 可以共享。因为 VAO 只是存储 VBO 绑定到哪些 attribute 的配置，而 VBO 是实际的顶点数据。✅

- **Q**：后台线程加载纹理需要 Surface 吗？
  - **A（我的回答）**：需要，因为 eglMakeCurrent 必须有 Surface 参数。🔄（理解了需要，但对原因理解还需加强）

## 导师反馈（Mentor Feedback）

- **我答得对的地方**：
  - 理解了 EGL 作为桥接层的角色
  - 理解了 EGLDisplay 是抽象连接
  - 理解了 Context 线程绑定规则
  - 理解了容器对象 vs 数据对象的共享规则

- **我需要纠正/更精确的地方**：
  - eglMakeCurrent 需要 Surface 是 EGL 规范的强制要求，不是为了获取渲染结果
  - Surface 在后台加载纹理场景中只是"占位符"，实际上没有使用

- **当前掌握状态（⏳/🔄/✅）**：🔄
- **继续追问（若未通过）**：
  - 需要动手实现 EGL 初始化流程
  - 需要理解 EGLImage 的用途

## 例子（我自己举的）

- （待补充）

## 变更记录（滚动更新）

- **2026-01-08**：
  - 我新增理解：EGL 核心三元组、Context 线程绑定、资源共享规则、Pbuffer vs FBO
  - 仍然不确定：eglMakeCurrent 为什么设计成必须要 Surface（历史原因？）

