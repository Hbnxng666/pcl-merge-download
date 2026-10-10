# PCL 合并下载修改版（第三方修改）

本仓库**不是** PCL 官方仓库。它是基于 [PCL2](https://github.com/Hex-Dragon/PCL2) 的第三方修改版本，只做了一件事：
在 PCL 自带的「下载」页里加入**多选批量下载**能力。

本仓库本身**不包含** PCL 的完整源码。编译时由 GitHub Actions 自动去拉取锁定了版本的官方源码，
再把本仓库 `patch/` 下的 5 个改动文件覆盖上去，然后编译。

- 官方源码版本（锁定）：`Hex-Dragon/PCL2` @ `0e0d12fdce6a2804916fb2be60e41144da637c18`
- 子模块 `MeloongCore` 会自动一并拉取

---

## 改了什么

| 文件 | 改动 |
|---|---|
| `Pages/PageDownload/Resource/MyResourceItem.xaml` | 列表项左侧加入批量选择复选框（默认隐藏，由 `ShowSelect` 控制） |
| `Pages/PageDownload/Resource/MyResourceItem.xaml.vb` | 新增 `ShowSelect` / `IsSelected` 属性与勾选回调；修正点击复选框时会误打开详情页的问题 |
| `Pages/PageDownload/Resource/PageResource.xaml` | 搜索按钮行新增「批量下载选中」按钮 |
| `Pages/PageDownload/Resource/PageResource.xaml.vb` | 勾选状态收集、批量下载主逻辑、版本匹配逻辑 |
| `Modules/Resource/ResourceProject.vb` | `ToResourceItem` 增加可选参数 `ShowSelect` |

行为说明：

- 在「下载 → Mod / 资源包 / 光影 / 数据包」页勾选若干项目，点「批量下载选中」。
- 目标版本与加载器优先取页面上的筛选项；筛选项为「全部」时，自动使用**当前选中的游戏版本**。
- 自动补齐前置 Mod，同一个前置只下载唯一一份。
- 目标文件夹中已存在同名文件的会自动跳过。
- 整合包不支持批量下载（安装整合包会创建新版本，仍请单个安装）。

---

## 怎么编译

推送到本仓库，或在仓库的 **Actions** 页面点 **Run workflow**。
编译完成后，在对应的运行记录页面底部下载 `PCL-MergeDownload-Mod` 这个产物。
产物是 `Plain Craft Launcher 2.exe`（PCL 官方的单文件形式，direct 运行即可）。

---

## 许可与署名

本修改版基于 PCL 二次创作，遵循 PCL 官方的
[《PCL 分发有限许可》与《PCL 存储库合理使用指南》](https://github.com/Hex-Dragon/PCL2/blob/main/LICENCE)。
按该指南对「重度使用」的要求：

1. 本内容为**第三方基于 PCL 独立进行二次创作的产物**，与龙腾猫跃及 PCL 官方无关。
2. 本内容名称以 `PCL` 开头并带有第三方修改后缀（`合并下载修改版`）。
3. 关于页面保留了龙腾猫跃的署名与赞助链接，本仓库公开源代码，并继续沿用上述指南文件。
4. 保留了 PCL 原有的购买正版劝导逻辑。
5. 未修改界面主色相，仍为蓝色。

原著作权归 **龙腾猫跃** 所有。支持作者请前往 PCL 官方页面。

---

## 指南原文

以下内容摘自 PCL 官方仓库，为便于查阅一并附上：

> 《PCL 存储库合理使用指南》
>
> 本指南仅作为说明，不是法律文件或协议。
> 除《PCL 分发有限许可》明确授予的权利外，开发者保留软件及其相关知识产权中的全部权利。但开发者承诺，在遵守本指南，且善意、合理使用的情况下，不会追究责任。
>
> 二、重度使用
>
> 若不符合轻度使用的情形，即为重度使用。
> 其常见情形例如：
> · 基于本存储库进行修改。
>
> 若属于重度使用，您需要：
> 1、明确表示您的内容是第三方基于 PCL 独立进行二次创作的产物。
> 2、您的内容的名称必须以 Plain Craft Launcher (PCL) 开头，并在其后添加足以表现其由第三方修改的后缀。
> 3、在关于页面的首位给出龙腾猫跃的署名及对应的赞助链接，公开源代码，且继续使用本文件作为指南（可参考 CC BY-SA 协议）。
> 4、软件若有 Minecraft 启动功能，则应实现与 McLaunchPrecheck 函数一致（或更激进）的 Minecraft 正版购买劝导与赞助劝导。
> 5、软件在 Windows 系统上运行时，不应有与 PCL 的赞助解锁功能类似的功能或表现。

完整的《PCL 分发有限许可》请见 <https://shimo.im/docs/rGrd8pY8xWkt6ryW#anchor-X0bo>。
