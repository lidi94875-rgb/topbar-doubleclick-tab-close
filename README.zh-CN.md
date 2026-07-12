# Chromium 双击顶部关闭标签页

这是一个基于 Chromium 源码定制编译的浏览器版本，不是 Chrome 扩展程序。

功能：

- 双击标签页顶部薄区域，关闭当前标签页。
- 双击浏览器窗口最顶端的标签栏/可拖拽区域，关闭当前活动标签页。
- 只剩一个标签页时，不关闭标签页，也不关闭浏览器窗口。

当前版本：

- Chromium：`152.0.7945.0`
- Commit：`18c53a66ca1e6ed76ab23985ce3950876aa81a98`
- 平台：Windows x64

本地启动：

```powershell
C:\src\chromium\src\out\DoubleClickClose\chrome.exe --user-data-dir=C:\src\chromium-user-data-double-click-close
```

主要修改文件：

- `chrome/browser/ui/views/tabs/tab.cc`
- `chrome/browser/ui/views/frame/browser_desktop_window_tree_host_win.cc`

注意：

- 这是自编译 Chromium，不是官方 Google Chrome。
- 不会自动跟随 Chrome 稳定版更新。
- 后续更新 Chromium 源码后，需要重新应用补丁并重新编译。
