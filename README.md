# .config

个人终端美化配置，同时维护 **Windows 11** 与 **WSL2 Arch Linux** 两套环境：

- [fastfetch](https://github.com/fastfetch-cli/fastfetch)：系统信息面板
- [starship](https://starship.rs/)：命令行提示符

> [!IMPORTANT]
> 这里只是分享我自己的配置，**并非开箱即用**。不同机器上的硬件、桌面环境、WSL 发行版和已安装的工具链各不相同，使用前请按自己的系统进行调整。
>
> 尤其要注意 fastfetch 配置底部的 **Development** 分组：其中每个 `command` 模块都会执行对应命令来读取版本号，请根据自己实际安装的工具链增删模块、修改命令，否则可能出现报错或空缺。

> [!NOTE]
> 默认您已了解 fastfetch 和 starship 的安装及其配置文件的路径

## 预览

### Windows 11

![Windows 11 demo](Windows%2011%20demo.png)

### WSL2 Archlinux

![WSL2 Archlinux demo](WSL2%20Archlinux%20demo.png)

## 配置文件

| 工具      | Windows 11                             | WSL2 Arch Linux                         |
| --------- | -------------------------------------- | --------------------------------------- |
| fastfetch | `fastfetch/Windows 11/config.jsonc`    | `fastfetch/WSL2 Archlinux/config.jsonc` |
| starship  | `starship/Windows 11/starship.toml`    | `starship/WSL2 Archlinux/starship.toml` |

- **fastfetch**：分别使用 Windows 11 / Arch 内置 Logo，按 System、Desktop、Hardware、Development、Network & Power 分组展示；开发工具版本通过 `command` 模块读取。
- **starship**：单行提示符，依次显示系统图标、`用户@主机`、当前目录、Git 分支与提交哈希；`add_newline = false` 让提示符更紧凑。

## 依赖

- [fastfetch](https://github.com/fastfetch-cli/fastfetch)
- [starship](https://starship.rs/)
- 一款 Nerd Font 字体（本人使用 [Jetbrains Maple Mono NF-XX-XX-XX](https://github.com/SpaceTimee/Fusion-JetBrainsMapleMono/releases)），并在终端中启用，否则图标会显示为方块
- Windows 端需要 PowerShell 5.1+（fastfetch 的 WSL2 与开发工具模块通过 PowerShell 执行命令）
- WSL2 + Arch Linux（WSL 配置中的部分命令依赖 `ghc`、`ocaml`、`elixir` 等工具）

## 自定义

- **配色**：修改 starship 中的 `[palettes.frappe]`，或在 fastfetch 的 `display.color` 中调整键名颜色。
- **提示符顺序**：修改 starship 的 `format`，模块名与下方 `[模块名]` 一一对应。
- **fastfetch 模块**：`modules` 数组按顺序渲染，字符串表示使用默认配置，对象可以覆盖 `key`、`keyIcon`、`format` 等属性。
- **开发工具版本**：`Development` 分组中的 `command` 模块会调用对应命令；请按自己的工具链增删或修改命令，未安装的工具建议删除或注释掉，避免输出报错。
- **WSL 内核磁盘**：WSL 配置中有一项磁盘模块硬编码了内核源码目录：

  ```jsonc
  "/usr/src/linux-headers-6.18.54.1-microsoft-standard-WSL2"
  ```

  内核升级后该路径会变化，可用 `uname -r` 查看当前版本并同步修改。

## 常见问题

**图标显示为方块或问号**

安装 Nerd Font，并在 Windows Terminal / 终端模拟器的字体设置中选择对应的 Nerd Font 字体。

**fastfetch 某些行显示命令错误**

对应工具未安装或不在 `PATH` 中。删除该 `command` 模块，或安装工具后重试。

**Windows 上不想显示 WSL2 发行版**

删除 `fastfetch/Windows 11/config.jsonc` 中 `"key": "WSL2"` 的 `command` 模块即可。

**WSL 磁盘占用显示的不是当前内核**

更新上文提到的 `linux-headers-*` 路径，使其与 `uname -r` 的输出一致。

## 参考

- [fastfetch 配置文档](https://github.com/fastfetch-cli/fastfetch/wiki/Configuration)
- [starship 配置文档](https://starship.rs/config/)
- [Nerd Fonts](https://www.nerdfonts.com/)
- [Catppuccin](https://catppuccin.com/)

## 许可证

本仓库采用 [Unlicense](UNLICENSE) 授权，内容贡献至公有领域。你可以自由复制、修改、分发或用于任何目的，无需署名。
