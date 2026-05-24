# Codex Chrome / Browser 插件安装解决方案

> [English](README.md) | 中文

## 问题描述

在某些工位设备上，Codex 的插件列表中**没有显示最新增加的 Chrome 和浏览器（Browser）插件**，导致无法使用浏览器自动化功能。

## 解决思路

参考个人可用设备上的 `config.toml` 配置，通过手动复制插件文件并配置本地 marketplace 的方式解决。

---

## 解决步骤

### 步骤 1：定位 openai-bundled 插件文件

在 Windows 设备上，使用 **Everything** 或 **Listary** 等本地搜索软件，搜索 `openai-bundled`。

搜索结果中会出现一个位于 `WindowsApps` 内的文件夹，如下图所示：

![搜索 openai-bundled](assets/P1.png)

进入该文件夹后，可以看到 `.agents` 和 `plugins` 两个子文件夹：

![openai-bundled 目录结构](assets/P2.png)

在 `plugins` 文件夹内，可以看到 `browser`、`chrome` 等插件文件夹：

![plugins 子目录](assets/P3.png)

### 步骤 2：复制 openai-bundled 到自定义路径

将找到的 `openai-bundled` 文件夹**整个复制**到自己指定的目录中。

例如，复制到 `C:\Users\<Username>\.codex\plugins\cache\` 目录下：

![复制 openai-bundled](assets/P4.png)

复制完成后，目标路径应包含 `openai-bundled` 文件夹：

![目标路径确认](assets/P5.png)

### 步骤 3：配置 Codex 的 config.toml

打开 Codex 的配置文件 `config.toml`，添加或修改 `[marketplaces.openai-bundled]` 配置段：

```toml
[marketplaces.openai-bundled]
last_updated = "2026-05-24T11:32:39Z"
source_type = "local"
source = "\\\\?\\C:\\Users\\<Username>\\.codex\\.tmp\\bundled-marketplaces\\openai-bundled"
```

> **注意**：将 `<Username>` 替换为你的 Windows 用户名，例如 `C:\Users\lihua\.codex\XXX`。

配置示例截图：

![config.toml 配置示例](assets/P7.png)

### 步骤 4：重启 Codex

保存 `config.toml` 后，**完全关闭并重新启动 Codex**。

重启后，在 Codex 的插件列表中应该能看到 Chrome 和浏览器插件：

![插件列表显示 Chrome](assets/P6.png)

### 步骤 5：启用浏览器和 Chrome 插件

进入 Codex 设置，找到**浏览器**选项，确保浏览器插件已启用：

![浏览器设置](assets/P8.png)

同时，在**电脑操控**设置中，确认 Google Chrome 插件已连接：

![电脑操控 - Google Chrome](assets/P9.png)

---

## 配置参考

```toml
[marketplaces.openai-bundled]
last_updated = "2026-05-24T11:32:39Z"
source_type = "local"
source = "\\\\?\\C:\\Users\\<Username>\\.codex\\.tmp\\bundled-marketplaces\\openai-bundled"
```

