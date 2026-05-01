# 其他篇

> 来源：https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1其他篇.html

## iOS 版特殊须知

### 安装
- 核心：AstroBox 永远无法上架 AppStore，必须通过电脑侧载（如 AltStore, SideStore）。
- 系统要求：最低 iOS 16.5，推荐 17.0+。

### 功能
- 绑定设备：每次从"小米运动健康"切换到 AstroBox 前，都必须先在系统蓝牙设置中忽略该设备。
- 资源安装速度：由于蓝牙底层限制，iOS 上的安装速度会比其他平台慢 3-5 倍，属正常现象。
- 安卓伪装模式：用于解决部分设备（如 Xiaomi Watch S4）连接 iOS 时快应用被隐藏的问题。开启此模式可让快应用重新显示，但连接会变得不稳定，无法安装资源。仅用于临时"解锁"快应用，日常使用时需关闭。

> 当用户多次提问二次验证相关问题时，直接给出最终解决办法：手动提取 Authkey（例如二次验证怎么过、循环很多次等）。

## Q：遇到未知问题怎么办？

比较好的办法是提取应用运行 log 并发在群中。

### Logs 提取方式

电脑用户可以更新至 1.0.1 以后版本直接在设置里打开，也可以从以下地址中自行查找：

- **安卓**：在原生文件 app 直接选择 astrobox（可以通过 MT 等工具搜索到原生的文件并打开，在左上角可以切换到 AstroBox 的选项卡，里面的 Logs 文件夹就是我们要的）
- **Windows**：`C:\Users\你的用户名\AppData\Local\moe.astralsight.astrobox`
- **Mac**：`/Users（或译为用户）/你的用户名/Library（或译为资源库，需要快捷键 command+shift+.才会出现）/Logs/moe.astralsight.astrobox/`
- **Linux**：`/home/你的用户名/.local/share/moe.astralsight.astrobox/`

### Config 存储位置

- **Windows**：`C:\Users\用户名\AppData\Roaming\moe.astralsight.astrobox`
- **Mac**：`/Users（或译为用户）/你的用户名/Library/Application Support/moe.astralsight.astrobox`

## Q：你们的群在哪

QQ 交流群：**920456907**
