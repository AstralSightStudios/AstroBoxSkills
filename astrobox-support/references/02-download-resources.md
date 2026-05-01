# 下载安装资源篇

> 来源：https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1下载资源安装篇.html

## Q：首页的 bandbbs 栏目为什么空的 / 显示"No BandBBS account"？

你没在设置里登录米坛账号。

## Q：Bandbbs 的资源点击下载后不会和官方源一样自动下载？

Bandbbs 的资源点击下载后需要选择下拉框里的文件再下载安装，请下载前自行确定资源适配的穿戴设备型号是否与你的设备型号一致。

## Q：资源显示 404 或"resource not found"

这个资源不存在，请联系资源作者解决。

## Q：出现"error sending request for url"？

解决方案：在设置中切换 CDN 并重启，或使用代理。

## Q：出现"No devices are connected"/"deadline has elapsed"怎么办

请确认手环是否已经连接，回到主页确定当前连接状态，建议多重启应用，重试几次。

## Q：出现"channel closed"？

解决方案：连接断开或 Authkey 错误。请尝试重新连接或重新同步 Authkey。

## Q：出现"Prepare not READY！"？

解决方案：手环空间或电量不足。重启手环，或尝试在资源队列中点击"编辑"按钮随机修改一个 ID。

对于 Redmi Watch 5 esim（rw5e），如果你在安装快应用，请你降级版本，系统限制了应用安装。

## Q：出现"Timeout waiting for protokey"怎么办

请重启 AstroBox 和手环并再次尝试。

## Q：出现"failed to open file"怎么办

1. 请检查自己的文件是否下载完整。
2. 检查是否授予 AstroBox 足够的文件读取权限。

## Q：出现"failed to get metadata of path"怎么办

你可以检查一下手环是否安装上了这个应用，大概率是 AstroBox 本身的 bug。

## Q：出现"url is not a valid path"怎么办

请检查你的文件格式是否正确，通常为 bin 或者是 rpk（快应用）。

## Q：固件安装可以用吗？

风险极高：固件安装是危险操作，可能导致设备变砖，AstroBox 团队概不负责。不建议在安卓手机上操作。如要尝试，建议将发包间隔改为 10。

> 补充：请最好别用安卓手机传输固件，容易丢包，建议用其他设备尝试。安卓的固件安装功能建议移步隔壁 Notify For Xiaomi。固件安装过程中请不要对手机、手环做任何操作！不要安装非同一型号、非同一地区的固件到手环！

## Q：安装多个表盘只显示一个？

原因：表盘开发者使用了相同的 ID。

解决方案：关闭"自动安装"，在下载队列中点击"画笔"图标，随机生成一个新的 ID 后再发送到设备。
