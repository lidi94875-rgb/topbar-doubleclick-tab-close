# Chromium Double-Click Close Tab / Chromium 双击顶部关闭标签页

## 中文说明

这是一个基于 Chromium 源码定制编译的浏览器版本，不是 Chrome 扩展程序。

它增加了一个小功能：在浏览器窗口顶部区域双击鼠标左键时，关闭当前活动标签页。

### 功能行为

- 双击标签页顶部薄区域：关闭当前标签页。
- 双击浏览器窗口最顶端的标签栏/可拖拽区域：关闭当前活动标签页。
- 如果当前窗口只剩 1 个标签页：不会关闭标签页，也不会关闭浏览器窗口。

### 当前构建版本

- Chromium 版本：`152.0.7945.0`
- Chromium commit：`18c53a66ca1e6ed76ab23985ce3950876aa81a98`
- 源码时间：`2026-07-11`
- 平台：Windows x64
- 本地构建目录：`C:\src\chromium\src\out\DoubleClickClose`

### 启动方式

如果你使用的是本地构建产物，可以运行：

```powershell
C:\src\chromium\src\out\DoubleClickClose\chrome.exe --user-data-dir=C:\src\chromium-user-data-double-click-close
```

建议使用单独的 `--user-data-dir`，避免和正式版 Google Chrome 的用户数据混用。

### 与官方 Chrome 的区别

这个版本是自编译 Chromium，不是官方 Google Chrome。

- 不包含完整的 Google Chrome 品牌和部分 Google 服务集成。
- 不会像官方 Chrome 一样自动更新。
- 后续如果要跟随 Chromium 官方源码更新，需要重新同步源码、保留补丁并重新编译。

### 已修改的源码位置

主要改动在两个文件：

- `chrome/browser/ui/views/tabs/tab.cc`
- `chrome/browser/ui/views/frame/browser_desktop_window_tree_host_win.cc`

实现要点：

- 在标签页顶部区域处理双击左键关闭。
- 在 Windows 主窗口消息层处理顶部客户区和非客户区双击。
- 关闭前检查当前窗口标签数量，只有标签数大于 1 时才关闭当前标签页。

### 维护说明

如果以后更新 Chromium 源码：

1. 执行 `gclient sync` 更新源码。
2. 检查这两个文件是否发生冲突。
3. 重新应用补丁。
4. 执行增量编译：

```powershell
autoninja -C out\DoubleClickClose chrome -j 8
```

首次完整编译耗时很长；后续只改这几个 UI 文件时，通常是增量编译和重新链接，速度会快很多。

---

## English

This is a custom-built Chromium browser, not a Chrome extension.

It adds one small behavior: double-clicking the top area of the browser window with the left mouse button closes the current active tab.

### Behavior

- Double-click the thin top area of a tab: closes that tab.
- Double-click the top tab-strip / draggable area of the browser window: closes the current active tab.
- If the current window has only 1 tab left: the tab is not closed and the browser window stays open.

### Current build

- Chromium version: `152.0.7945.0`
- Chromium commit: `18c53a66ca1e6ed76ab23985ce3950876aa81a98`
- Source date: `2026-07-11`
- Platform: Windows x64
- Local build directory: `C:\src\chromium\src\out\DoubleClickClose`

### Run locally

If you are using the local build output, run:

```powershell
C:\src\chromium\src\out\DoubleClickClose\chrome.exe --user-data-dir=C:\src\chromium-user-data-double-click-close
```

Using a separate `--user-data-dir` is recommended so this custom Chromium profile does not mix with your official Google Chrome profile.

### Difference from official Google Chrome

This build is custom Chromium, not official Google Chrome.

- It does not include the full Google Chrome branding and some Google service integrations.
- It does not auto-update like official Chrome.
- To follow newer Chromium versions, the source must be synced again, the patch must still apply, and the browser must be rebuilt.

### Modified source files

The main changes are in:

- `chrome/browser/ui/views/tabs/tab.cc`
- `chrome/browser/ui/views/frame/browser_desktop_window_tree_host_win.cc`

Implementation summary:

- Handle left-button double-clicks on the top area of individual tabs.
- Handle Windows client-area and non-client-area double-click messages for the top browser region.
- Before closing, check the current tab count and close only when the window has more than one tab.

### Maintenance

When updating Chromium later:

1. Run `gclient sync`.
2. Check whether the two modified files have conflicts.
3. Re-apply the patch if needed.
4. Rebuild incrementally:

```powershell
autoninja -C out\DoubleClickClose chrome -j 8
```

The first full Chromium build is expensive. Later changes to these UI files usually require only incremental compilation and relinking.
