# Codex Chrome & Browser Plugin Manual Installation Guide

<div align="center">

**[English](README.md) | [中文](README.zh-CN.md)**

</div>

> **Applicable Scenario**: The Codex plugin list does not display the newly added Chrome/Browser plugins, requiring manual configuration of a local plugin source.

---

## Problem Description

On certain workstation devices, the Codex plugin list fails to automatically sync the latest Chrome and Browser plugins. This solution addresses the issue by manually copying plugin files and configuring a local source.

---

## Solution Steps

### Step 1: Locate the Plugin Files

1. Use a local search tool such as **Everything** or **Listary**, and search for the keyword: `openai-bundled`
2. In the search results, find the folder located within `WindowsApps` (e.g., under the Codex application directory)
3. Navigate into the folder, and you will see the following structure:

```
openai-bundled/
©À©¤©¤ .agents/
©¸©¤©¤ plugins/
```

> The `plugins` folder contains plugin directories such as `browser` and `chrome`.

---

### Step 2: Copy Plugins to a Local Directory

1. **Copy the entire `openai-bundled` folder** to a path of your choice, for example:

```
C:\Users\<YourUsername>\.codex\plugins\cache\openai-bundled
```

2. The copied directory structure should look like this:

```
openai-bundled/
©À©¤©¤ .agents/
©¸©¤©¤ plugins/
    ©À©¤©¤ browser/
    ©¸©¤©¤ chrome/
```

---

### Step 3: Modify the Codex Configuration File

1. Open the Codex configuration file (usually located at `C:\Users\<YourUsername>\.codex\config.toml`)
2. Add or modify the `[marketplaces.openai-bundled]` section:

```toml
[marketplaces.openai-bundled]
last_updated = "2026-05-24T11:32:39Z"
source_type = "local"
source = ''\\?\C:\Users\<YourUsername>\.codex\.tmp\bundled-marketplaces\openai-bundled''
```

> **Notes**:
> - Replace `<YourUsername>` with your actual username (e.g., `lihua`)
> - The `source` path must be a **full absolute path**, keeping the `\\?\` prefix

---

### Step 4: Restart Codex

1. Save the `config.toml` configuration file
2. **Fully close and restart Codex**
3. Go to the plugin management page and confirm that the Chrome and Browser plugins are now visible

---

## Configuration Example

Below is a complete `config.toml` example (for reference only; adjust paths according to your actual setup):

```toml
[marketplaces.openai-primary-runtime]
last_updated = "2026-05-24T11:32:29Z"
source_type = "local"
source = ''\\?\C:\Users\<YourUsername>\.cache\codex-runtimes\codex-primary-runtime\plugins\openai-primary-runtime''

[marketplaces.openai-bundled]
last_updated = "2026-05-24T11:32:39Z"
source_type = "local"
source = ''\\?\C:\Users\<YourUsername>\.codex\.tmp\bundled-marketplaces\openai-bundled''
```

---

## Verification

After restarting Codex, check the following locations to confirm the plugins are loaded successfully:

- **Browser Plugin**: Settings ¡ú Browser ¡ú Ensure the "Browser" toggle is enabled
- **Chrome Plugin**: Settings ¡ú Computer Control ¡ú Confirm "Google Chrome" shows "Connected to browser extension, more control available"

---

## Frequently Asked Questions

| Issue | Solution |
|-------|----------|
| Plugins still not showing | Double-check the `source` path is correct and uses a full absolute path |
| Path contains Chinese or special characters | Use an English path to avoid encoding issues |
| Permission denied after copying | Ensure the current user has read permissions for the directory |

---

## Summary

By manually copying the `openai-bundled` plugin package and configuring a local `marketplace` source, you can resolve the issue of Codex failing to automatically sync the latest plugins on certain devices. The core steps are: **Locate ¡ú Copy ¡ú Configure ¡ú Restart**.

---

*Last Updated: 2026-05-24*

