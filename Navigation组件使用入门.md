# Navigation组件使用入门

## 向 Activity 添加 NavHost

**注意**：Navigation 组件旨在用于具有一个主 Activity 和多个 Fragment 目的地的应用。主 Activity 与导航图相关联，且包含一个负责根据需要交换目的地的 `NavHostFragment`。在具有多个 Activity 目的地的应用中，每个 Activity 均拥有其自己的导航图。

- `app:defaultNavHost="true"` 属性确保您的 `NavHostFragment` 会拦截系统返回按钮。请注意，只能有一个默认 `NavHost`。如果同一布局（例如，双窗格布局）中有多个宿主，请务必仅指定一个默认 `NavHost`。
