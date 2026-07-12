# Chromium Double-Click Close Tab

This is a custom-built Chromium browser, not a Chrome extension.

Features:

- Double-click the thin top area of a tab to close that tab.
- Double-click the top tab-strip / draggable browser area to close the current active tab.
- When only one tab remains, the tab is not closed and the browser window stays open.

Current version:

- Chromium: `152.0.7945.0`
- Commit: `18c53a66ca1e6ed76ab23985ce3950876aa81a98`
- Platform: Windows x64

Run locally:

```powershell
C:\src\chromium\src\out\DoubleClickClose\chrome.exe --user-data-dir=C:\src\chromium-user-data-double-click-close
```

Main modified files:

- `chrome/browser/ui/views/tabs/tab.cc`
- `chrome/browser/ui/views/frame/browser_desktop_window_tree_host_win.cc`

Notes:

- This is custom Chromium, not official Google Chrome.
- It does not auto-update with Chrome Stable.
- To update Chromium later, re-apply the patch and rebuild.
