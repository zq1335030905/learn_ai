# 2026-01-08 EGL 基础学习

## 核心问题 (The Problem)

> 理解 EGL 作为桥接层的角色，掌握 EGL 初始化流程和核心概念。

## 会话途中快照 (In-Session Captures)

### 核心收获

1. **EGL 的定位**：连接渲染 API（OpenGL ES）与原生窗口系统的桥接层
   - OpenGL 只定义"怎么画"
   - EGL 定义"画到哪里"

2. **EGL 核心三元组**：
   - EGLDisplay：与显示系统的连接抽象（不是物理显示器）
   - EGLSurface：渲染目标（Window/Pbuffer/Pixmap）
   - EGLContext：GL 状态机容器

3. **Context 线程绑定规则**：
   - 一个 Context 同一时刻只能绑定到一个线程
   - 转移 Context：先在原线程解绑（makeCurrent 到 NO_CONTEXT），再在新线程绑定
   - 不需要销毁线程

4. **资源共享规则**：
   - 可共享：Texture、VBO/EBO/UBO/SSBO、Renderbuffer、Shader/Program、Sampler、Sync Object
   - 不可共享（容器对象）：VAO、FBO、Transform Feedback、Query Object
   - 原因：容器对象只是引用/配置，不包含实际数据

5. **Pbuffer vs FBO**：
   - Pbuffer 是 EGL 层的 Surface 类型，用于离屏渲染或作为 makeCurrent 的占位符
   - FBO 是 OpenGL 层的概念，用于"渲染到纹理"
   - 层次不同：要使用 FBO，必须先有 EGLSurface 能 makeCurrent

6. **eglMakeCurrent 必须有 Surface**：
   - 这是 EGL 规范的强制要求
   - 即使只是后台加载纹理，也需要一个 Pbuffer 作为占位符
   - EGL 1.5+ 支持 Surfaceless Context

## 概念地图更新 (Concept Map Update)

- **概念地图**：`knowledge-base/foundations/graphics-concept-map.md`
  - 今天推进的概念节点：EGL、EGLDisplay、EGLSurface、EGLContext、EGLConfig、eglMakeCurrent、shareContext
  - 状态变化：
    - EGL: ⏳ → 🔄
    - EGLDisplay: ⏳ → ✅
    - EGLConfig: ⏳ → ✅
    - EGLSurface: ⏳ → 🔄
    - EGLContext: ⏳ → ✅
    - eglMakeCurrent: ⏳ → 🔄
    - shareContext: ⏳ → ✅

## 直觉构建 (Intuition Builder)

- **Before**: 我以为 OpenGL 可以直接渲染到屏幕
- **After**: 现在我理解 OpenGL 只定义渲染命令，需要 EGL 告诉它渲染到哪里

- **Before**: 我以为共享 Context 可以共享所有 GL 对象
- **After**: 现在我理解容器对象（VAO/FBO）不能共享，因为它们只是引用配置

- **Before**: 我以为后台线程可以直接用 FBO 做离屏渲染
- **After**: 现在我理解必须先有 EGLSurface（Pbuffer）做 makeCurrent，才能使用任何 GL 函数

## 关键反直觉点

1. **EGLContext 不能跨线程直接使用** → 必须先解绑再绑定
2. **VAO 不能共享但 VBO 可以** → 因为 VAO 只是引用配置
3. **使用 GL 必须有 Surface** → 即使只是加载纹理，也需要 Pbuffer 作为占位符

## 待办与复习 (Next Steps)

- [ ] 完成 EGLImage 的学习
- [ ] 创建 EGL 初始化最小实验
- [ ] 更新 `learning-log/mastery/egl.md`
- [ ] 更新 `roadmap/README.md` 进度

## 学习反馈

### 做得好的地方
- 主动提问澄清基础概念（Java层/Native层、VAO/VBO区别等）
- 敢于说"我不清楚"，而不是猜测

### 可改进的地方
- 对 eglMakeCurrent 为什么需要 Surface 的理解还需加强
- 建议动手写一个 EGL 初始化的代码来加深理解

### 系统改进建议
- 无

