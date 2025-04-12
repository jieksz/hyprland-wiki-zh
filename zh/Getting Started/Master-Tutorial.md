---
weight: 2
title: 大师教程
---

第一次用Hyprland, 这是你要读首要教程.

这篇教程涵盖让事情顺利的一起. 它在必要是会链接到其它页面.

## 安装Hyprland

查看[安装](../Installation)并在成功安装Hyprland后回到这里.

安装 `kitty` (默认终端模拟器). 他在大多数发行版仓库都可用.

## 英伟达?

{{< callout type=info >}}

如果不用英伟达显卡, 跳过这步.

{{< /callout >}}

启动之前请看[英伟达显卡](../../Nvidia). 它有重新评估所需环境和修改的信息.

## 虚拟机?

{{< callout type=info >}}

如果不用, 跳过这步.

{{< /callout >}}

在虚拟机中, 确保在你的 `virtio` 配置 (或 `virt-manager`) 中启用3D加速否则Hyprland _**将不会工作**_.

你还可以通过GPU使其工作.

请注意3D加速可能使虚拟机变慢.

## 启动Hyprland

Hyprland可以在你在tty中输入 `Hyprland` 启动.

Systemd用户还可使用 [uwsm](https://github.com/Vladimir-csp/uwsm) 启动Hyprland. 这是在 systemd-based 发行版中启动Hyprland的推荐方法, 因为它提供了其它功能, 例如 [xdg-autostart](https://www.freedesktop.org/software/systemd/man/latest/systemd-xdg-autostart-generator.html) 支持, 使用 `uwsm app` 助手启动任意软件作为systemd-unit, 以及为依赖于图形会话的程序启用服务并提供此类服务的能力 (比如 waybar). 查看 [uwsm](../../Useful-Utilities/Systemd-start) 进一步了解.


{{< callout type=warning >}}

**不要**使用 `root` 权限启动Hyprland (别用 `sudo`)

{{< /callout >}}

你可以使用 `Hyprland -h` 查看启动标志, 这些包含配置路径, 忽略对上述内容的检查等.

登录管理器不受官方支持, 但这里有一个简短的兼容性列表:

- SDDM → 完美运行. 安装 sddm ⩾ 0.20.0 或者
  [最新git版](https://github.com/sddm/sddm) (或
  [sddm-git](https://aur.archlinux.org/packages/sddm-git) 从 AUR) 以防止
  SDDM bug [1476](https://github.com/sddm/sddm/issues/1476) (90s 关机).
- GDM → 首次启动时Hyprland会奔溃.
- greetd → 完美运行, 尤其与
  [ReGreet](https://github.com/rharish101/ReGreet).
- ly → 效果不佳.

## DE-like 预配置设置

你想像DE一样预先配置Hyprland，而不从头开始做自己的配置?

查看 [预配置设置](../Preconfigured-setups) 以了解一些选项.

这些 dotfiles 应该会为你做一切, 同时自己也有教程.

如果选择使用它们, 你可以跳到下一步. 然而, 它仍然会推荐阅读下面所有要点.
它们会给你推荐应用, 旧x11软件的替代品, 有关配置显示器的信息等.

## 在Hyprland中使用默认配置

严格来说, 你可以继续你的冒险.

使用 <key>SUPER</key> + <key>Q</key> 以启动 kitty. 在你继续之前,
如果你希望选择你的默认终端, 你可以在
`~/.config/hypr/hyprland.conf`
([示例配置](https://github.com/hyprwm/Hyprland/blob/main/example/hyprland.conf)).

如果你想用更少的搜索获得最佳体验, 继续阅读. 

## 关键软件

查看 [必要软件页](../../Useful-Utilities/Must-have) 了解使
Wayland / Hyprland / other 应用正常工作的关键因素.

## 显示器配置

查看 [配置Hyprland页](../../Configuring/Monitors) 以了解有关配置显示器的所有信息.

## 应用程序 / X11 替代品

查看 [有用的应用页](../../Useful-Utilities) 以及
[Sway wiki页](https://github.com/swaywm/sway/wiki/Useful-add-ons-for-sway)
你还可访问
[很棒的Hyprland](https://github.com/hyprland-community/awesome-hyprland)
仓库以获得更全面的列表.

## 完全配置Hyprland

前往
[配置Hyprland页](../../Configuring)
了解如何根据自己的喜好配置Hyprland.

## 光标

当你不知道如何设置光标时，设置光标是一种痛苦.
[在FAQ中查看如何更改我的光标](../../FAQ#如何更改我的光标)

如果你的鼠标没有出现,
[在FAQ中查看光标未渲染](../../FAQ#我的光标未渲染)

## 主题

因为Hyprland不是一个成熟的桌面环境, 你需要使用一些工具
比如 `lxappearance` 或 `nwg-look` (推荐) 为 GTK, 以及 `qt5ct` /
`qt6ct` 各自的Qt版本. 一些老的应用程序也可能需要 `qt4ct`.

## 强制应用程序使用Wayland

大部分应用程序默认会使用Wayland. Chromium (以及其它基于此的浏览器, 或Electron) 不会. 你需要通过
`--enable-features=UseOzonePlatform --ozone-platform=wayland` 在可能的情况下来让它们使用
`.conf` 文件. 基于Chromium浏览器也应该有一个切换在 `chrome://flags`. 
搜索 _"ozone"_ 并选择Wayland.

如果你用 NixOS 你可以在配置中设置环境变量 `NIXOS_OZONE_WL=1` .

对于大多数electron应用, 你应该将上述内容放入
`~/.config/electron-flags.conf`. 请注意，已知VSCode**不能**使用它.

[这里](../../Configuring/Environment-variables) 还记录了一些用于强制wayland模式的环境变量.

你可以使用 `hyprctl clients` 检查应用程序是否在xwayland中运行.
