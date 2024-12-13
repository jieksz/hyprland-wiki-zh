---
weight: 11
title: FAQ
---

### 我的应用很模糊

这只是意味着它们在 XWayland 中运行, 而 XWayland 无法在物理上按分数缩放.

强制它们运行在原生 Wayland 模式, 查看
[大师教程](../Getting-Started/Master-Tutorial/#强制应用程序使用Wayland).

如果它们不能, 查看 [XWayland 页面](../Configuring/XWayland).

### 未渲染 / 白屏 / 首次打开应用时奔溃

可能的原因:

> 你的主题未正确设置, 导致应用奔溃.

使用类似于 `qt6ct` (Qt) 和 `nwg-look` (GTK) (\*对于 GTK 你可以使用 envvars 设置主题) 来设置你的主题.

> 你的电脑非常, _非常_ 旧.

这种情况, 查看 [安装页](../Getting-Started/Installation)
并试图使用旧版渲染器进行编译

_了解更多关于错误和奔溃, 查看_
_[wiki 页](../Crashes-and-Bugs)_

### 我的外部显示器显示空白 / 未渲染 / 未接收到信号 (笔记本电脑)

对于 Nvidia 显卡 - 使用 Nvidia 驱动程序 525.60.11 或更高版本时, 此问题似乎已得到解决, 
但对于较旧的驱动程序, 此问题可能会持续存在.

对于硬件有限的系统 (Ex. iGPU, USB-C, USB Hubs) - 在你的配置中设置 `env = AQ_NO_MODIFIERS,1` .
要诊断是否有上述确切问题, 你可以获取 [DRM 日志](https://wiki.hyprland.org/Crashes-and-Bugs/#debugging-drm-issues) 并查找

```plain
Requested display configuration exceeds system DDB limitations
```

除此之外, 还有一种方法_可能_对你有效:

**方法 1:** _只_使用外部显示器

通过使用 `AQ_DRM_DEVICES=/dev/dri/card1` (或 `card0`) 环境变量你可以强制 Hyprland
只使用你的 dGPU, 这意味着你的笔记本电脑的屏幕将消失, 但你的外部屏幕可以工作.

**方法 2:** 使用所有输出, 以电池寿命为代价.

通过将笔记本电脑切换为仅使用BIOS中的dGPU, 你_可以_以高电池使用率为代价, 让一切正常工作.

_请注意, 这些是高度取决于机型的, 可能会也可能不会奏效. 如果它们不起作用, 很遗憾你运气不佳_

你可以试试 USB-C to HDMI 适配器, 也许这可以通过iGPU路由到外部监视器.

### 如何截屏?

**方法 1:** 安装 `grim` 和 `slurp`.

使用绑定的键 (或执行) `grim -g "$(slurp)"`, 并选择区域. 
一张截图将输出到你的 `~/Pictures/` (你可以配置 grim 和 slurp, 查看它们的 GitHub 页面).

如果你想让这些截图直接到你的剪贴板, 
考虑使用 [`wl-clipboard`](https://github.com/bugaevc/wl-clipboard) 中的 `wl-copy`.
这是绑定示例:
`bind = , Print, exec, grim -g "$(slurp -d)" - | wl-copy` 为了获得更完整的实用程序, 
尝试我门自己的截图工具:
[Grimblast](https://github.com/hyprwm/contrib).

**方法 2:** 你也可以使用 hyprshot, [更多信息](https://github.com/Gustash/Hyprshot).

**方法 3:** 安装 `flameshot`.

Flameshot 有很多内置功能, 比如运行你用画笔画画, 添加线条, 添加形状等. 

Flameshot 最初是为 X 构建的, **它在Wayland上有很多问题**, 
使用HiDPI和多显示器设置的用户对 Flameshot 的体验喜忧参半. 
上面的方法更好, 更适合Wayland. 如果你仍然想使用 Flameshot, 这里有一些已经找到解决方法的用户的配置建议. 

```ini
# noanim不是必需的, 但有这些规则的动画可能看起来很糟糕, 自行决定使用. 
windowrulev2 = noanim, class:^(flameshot)$
windowrulev2 = float, class:^(flameshot)$
windowrulev2 = move 0 0, class:^(flameshot)$
windowrulev2 = pin, class:^(flameshot)$
# 将其设置为最左侧显示器的id, 否则在执行 flameshot 之前你必须将你的光标移动的最左侧显示器
windowrulev2 = monitor 1, class:^(flameshot)$

# ctrl-c 从 flameshot gui 复制时有时会产生扭曲的图像, 但设置 env 可以修复它
bind = ..., exec, XDG_CURRENT_DESKTOP=sway flameshot gui
```

对于录制视频, [wf-recorder](https://github.com/ammen99/wf-recorder),
[wl-screenrec](https://github.com/russelltg/wl-screenrec) or
[OBS Studio](https://obsproject.com/) could be used.

### 屏幕共享 / OBS 不工作

查看 [屏幕共享](../Useful-Utilities/Screen-Sharing).

如果你计划使用 obs 也可以安装 `qt6-wayland`.

### 如何改变壁纸?

查看 [壁纸](../Useful-Utilities/Wallpapers).

### 它有多大?

不比 Xorg 大多少. 如果你想获得最佳性能, 可以考虑关闭模糊和动画. 

### 我的显示器不工作

尝试在你的配置中改变模式. 如果你的首选并不工作, 试试低一点的. 
列出所有模式的一个好方法是获取 `wlr-randr` 并执行 `wlr-randr --dryrun`

### 打开VRR时, 我的显示器亮度闪烁

改变 VRR 选项为 `2` (全屏), 所有它只使用于游戏.
这是因为某些显示器的亮度可能取决于刷新率, 而快速变化的刷新率 ( 例如按下按键后屏幕瞬间更新时 ) 会导致亮度快速变化. 

### 如何更新?

在你克隆的仓库打开终端.

```bash
git pull
make all && sudo make install
```

如果你使用 AUR (hyprland-git) 包, 你需要 cleanbuild 来更新包, Paru之前更新有问题, 请使用Yay. 

### 如何锁屏?

使用 WLR 协议的 Wayland 兼容锁定实用程序, 例如 `swaylock`. 
请注意, 它们不会阻止使用Ctrl-Alt-F1...F7更改tty. 

### 如何更改我的光标?

查看 [hyprcursor](../Hypr-Ecosystem/hyprcursor)

1. 使用 [nwg-look](https://github.com/nwg-piotr/nwg-look) 设置 GTK 光标.
2. 添加 `exec-once=hyprctl setcursor [THEME] [SIZE]` 到你的配置并重启 Hyprland.

如果使用 flatpak, 运行 `flatpak override --filesystem=~/.themes:ro --filesystem=~/.icons:ro --user` 
并将你的主题都放到 `/usr/share/themes` 和 `~/.themes`, 并将你的 icons 和 cursors 都放到 `/usr/share/icons` 和 `~/.icons`.

对于 Qt 应用程序, Hyprland 默认将 XCURSOR_SIZE 导出设置为24.
你可以通过使用 `env` 将 XCURSOR_SIZE 导出设置为其他值来覆盖此内容.

你也可以试着运行 `gsettings set org.gnome.desktop.interface cursor-theme 'theme-name'` 或者在你的配置中添加到 `exec-once=` 之后.

如果你不想安装 GTK 设置编辑器, 请根据
[XDG specification (Arch Wiki link)](https://wiki.archlinux.org/title/Cursor_themes#Configuration)
更改配置文件.
请确保同时编辑 `~/.config/gtk-4.0/settings.ini` 和 `~/.gtkrc-2.0` 如果_不_使用工具(如 `nwg-look`).

### GTK Settings no work / whatever

[https://github.com/swaywm/sway/wiki/GTK-3-settings-on-Wayland](https://github.com/swaywm/sway/wiki/GTK-3-settings-on-Wayland)

### My \[program name\] is freezing

Make sure you have a notification daemon running, for example `dunst`. Autostart
it with the `exec-once` keyword.

### Waybar workspaces no worky???

Waybar has a set of caveats or settings that you need to be aware of. See
[Status bars](../Useful-Utilities/Status-Bars) for solutions.

### How do I autostart my favorite apps?

Using the window rules to assign apps to workspaces, you can open a bunch of
applications on various workspaces. The following method will start these apps
silently (i.e. without the flickering from workspace to workspace).

Put the following in your `hyprland.conf`: (example)

```ini
exec-once = [workspace 1 silent] kitty
exec-once = [workspace 1 silent] subl
exec-once = [workspace 3 silent] mailspring
exec-once = [workspace 4 silent] firefox
```

### How do I move my favorite workspaces to a new monitor when I plug it in?

If you want workspaces to automatically go to a monitor upon connection, use the
following:

In hyprland.conf:

```ini
exec-once = handle_monitor_connect.sh
```

where `handle_monitor_connect.sh` is: (example)

```sh {filename="handle_monitor_connect.sh"}
#!/bin/sh

handle() {
  case $1 in monitoradded*)
    hyprctl dispatch moveworkspacetomonitor "1 1"
    hyprctl dispatch moveworkspacetomonitor "2 1"
    hyprctl dispatch moveworkspacetomonitor "4 1"
    hyprctl dispatch moveworkspacetomonitor "5 1"
  esac
}

socat - "UNIX-CONNECT:$XDG_RUNTIME_DIR/hypr/${HYPRLAND_INSTANCE_SIGNATURE}/.socket2.sock" | while read -r line; do handle "$line"; done
```

This makes workspaces 1, 2, 4, and 5 go to monitor 1 when connecting it.

Please note this requires `socat` to be installed.

### My tablet no worky??

Use [Open Tablet Driver](https://github.com/OpenTabletDriver/OpenTabletDriver)
to configure your tablet. In the future it will be supported in the config.
Until then, OTD is the way to go.

### Some of my apps take a really long time to open...?

```ini {filename="~/.config/hypr/hyprland.conf"}
exec-once = dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP
```

Make sure that your portals launch _after_ this gets executed. For some people,
they might launch before that has happened.

In such cases, a script like this:

```bash
#!/usr/bin/env bash
sleep 4
killall -e xdg-desktop-portal-wlr
killall xdg-desktop-portal
/usr/lib/xdg-desktop-portal-wlr &
sleep 4
/usr/lib/xdg-desktop-portal &
```

launched with `exec-once` should fix all issues. Adjust the sleep durations to
taste.

### How do I export envvars for Hyprland?

See [Environment Variables](../Configuring/Environment-variables)

The `env` keyword is used for this purpose. For example:

```ini
env = XDG_CURRENT_DESKTOP,Hyprland
```

### How to disable middle-click paste?

Setting `misc:middle_click_paste` to `false` disables the feature altogether with the exception of some browsers (notably firefox) having a separate built-in way of emulating that feature which has to be disabled within the browser's settings.

### How do I make Hyprland draw as little power as possible on my laptop?

**_Useful Optimizations_**:

- `decoration:blur:enabled = false` and `decoration:shadow:enabled = false` to disable
  fancy but battery hungry effects.

- `misc:vfr = true`, since it'll lower the amount of sent frames when nothing is
  happening on-screen.

### My apps take a long time to start / can't screenshare

See [The XDPH Page](../Hypr-Ecosystem/xdg-desktop-portal-hyprland/#debugging).

You most likely have multiple portal impls / an impl is failing to launch.

### My screenshot utilities won't work with multiple screens

Some programs like Flameshot (currently) have limited Wayland support, so on most
Wayland compositors, you will have to do a few tweaks. For Hyprland, you can add
these window rules to your config to make these programs work with both of your
screens.

```ini
windowrulev2 = float,title:^(flameshot)
windowrulev2 = move 0 0,title:^(flameshot)
windowrulev2 = suppressevent fullscreen,title:^(flameshot)
```

### I cannot bind SUPER as my mod key on my laptop

Many laptops have a built-in function to toggle `SUPER` between single key press
mode and hold mode. This is usually indicated by a padlock on the `SUPER` key.

First, install and run `wev`, then press `SUPER`. If you see a key press event
followed by an instant key release event, then it's likely your `SUPER` key is
set to single press mode.

On most laptops, this can be fixed by pressing `FN+SUPER` and verified in `wev`.
You should be able to hold `SUPER` and not see an instant release event. In case
`FN+SUPER` doesn't work, consult your laptop's manual.

### My VM doesn't receive keybinds I have set in Hyprland

This is expected, as Hyprland takes precedence.

A simple fix is to create an empty "passthrough" submap:

```ini
bind = MOD,KEY,submap,passthru
submap = passthru
bind = SUPER,Escape,submap,reset
submap = reset
```

Set `MOD` and `KEY` to desired values.

By pressing the selected combo, you will enter a mode where Hyprland ignores your
keybinds and passes them on to the VM. Pressing `SUPER + Escape` will leave that mode.

### Some of my drop-down/pop-up windows in apps disappear/don't open at cursor position

In some apps like Steam or VSCode, the drop-down windows may disappear if you
hover over them. This can be fixed with window rules.

First, find the title and class of the pop-up window with `hyprctl clients`. You
can try something like `sleep 3 && hyprctl clients` so you have time to open the
pop-up. It should look something like this:

```bash
Window 55d794495400 -> :
  ...
  class: [CLASS here]
  title: [TITLE here]
  ...
```

If the pop-up disappears as you hover over it, you can add to your config:

```ini
windowrulev2 = stayfocused, title:^(TITLE)$, class:^(CLASS)$
```

This has a downside of not being able to click on anything in the main UI until
you've interacted with the pop-up.

If the pop-up disappears immediately, you can use:

```ini
windowrulev2 = minsize 1 1, title:^(TITLE)$, class:^(CLASS)$
```

If the pop-up doesn't open at the cursor position, try the following:

```ini
windowrulev2 = move onscreen cursor, title:^(TITLE)$, class:^(CLASS)$
```

This is required for apps running under xwayland only and there is usually no need
to use the first solution if opening at the cursor position.

### Steam's file picker no worky

On instances where you have a Steam library on another drive that you have to
add, Hyprland's file picker would not normally appear when selecting a directory
from Steam.

Steam has its own file picker, however, it's not functional. Install
`xdg-desktop-portal-gtk` to show the desktop's file picker.

### Workspaces or clients are disappearing or monitor related dispatchers cause crashes

It seems there is a Kernel bug making the system think there is an extra
phantom monitor, that causes all sorts of issues, crashes and weird behaviors
like disapearing workspaces or clients when adding or removing an external
monitor.

First check the list of monitors detected by Hyprland by running:

```ini
hyprctl monitors
```

If you see a monitor that should not be there (usually named `Unknown-1`), you
can work around the issue by adding in your `hyprland.conf`:

```ini
monitor = Unknown-1,disabled
```

### I get a .so file missing error on launch

If you are using a -git package, this is a common occurrence when ABI-breaking updates are done.

_**Do not**_ symlink different .so versions, this will cause crashes!!!

Instead, find all hypr* packages with `-git` you have installed, remove them (possibly remove dependencies of them, too)
and simply install them again.

If using yay, make sure to `CleanBuild` every package. If using paru, manually remove the cache of hypr* packages in `~/.cache/paru`.

If you are not using any -git packages, this is a mistake in your distro's packaging and should be solved there.

### My cursor is a hyprland icon?

This means you have no hyprcursor theme installed, and hyprland failed to find an XCursor theme as well. Install a cursor theme.

### Smart gaps please?

[Here](../Configuring/Workspace-Rules/#smart-gaps).

### Hyprwinwrap is not visible through blurred windows

This is a side effect of the [decoration:blur:new_optimizations](../Configuring/Variables/#blur).
You have two options to resolve it.
1. Set `decoration:blur:new_optimizations` to `false` - This will preserve the exact same appearance, but may have a slight performance cost.
2. Set `decoration:blur:ignore_opacity` to `false` - This will drastically affect the appearance, but should maintain the original performance.
