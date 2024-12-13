---
weight: 1
title: 安装
---

{{< callout type=warning >}}

Hyprland不适合初学者! 它需要你阅读本WIKI, 理解Linux如何工作以及有能力在线搜索并解决问题

如果你是Linux初学者, 可以考虑阅读**所有**内容以及它引用的所有其他页面, 否则你很难得到一个可用的桌面.

在线社区(比如Reddit)应作为最后的手段, 大多数信息可以在本WIKI中找到同时它保证是*最新和准确的*, 这不同于大多数在线"提示和技巧".

除非你知道你在做什么! 否则从**从头到尾**跟着[大师教程](../Master-Tutorial)

{{< /callout >}}

{{< callout type=warning >}}

由于专利性质, Nvidia显卡对Hyprland的兼容性有限.
如果你想试着在Nvidia上用Hyprland(很多人反馈成功), 请在安装Hyprland后跟着[Nvidia页面](../../Nvidia)操作

{{< /callout >}}

## 发行版

Arch, NixOS和openSUSE滚动发行版有很好的支持. 对于其他发行版(不基于Arch/Nix/openSUSE)你能得到不同程度的成功. 然而,因为Hyprland非常前沿, 一些发行版, 比如Pop!\_OS, Ubuntu等.可能在运行Hyprland时有**大**问题.

## 安装

安装Hyprland很简单.只需用你的包管理器就能安装(如果可用)亦或自行安装/构建.

{{< callout >}}
这个项目还在开发中并且不断变化. 如果你想了解最新变动,请考虑用`yay -Syu --devel`更新你的包,或其它你喜欢的包管理器

{{< /callout >}}

### 包

**警告:** 我不维护任何包.如果它们奔溃了,试着从源代码构建.

{{% details title="Arch" closed="true" %}}

从编译安装最新源代码的AUR安装:

```shell
yay -S hyprland-git
```

或者arch软件包的标记版本:

```shell
sudo pacman -S hyprland
```

或者，安装"hyprland meta"包，以自动获取和编译hypr*生态系统中所有组件的最新git版本.

```shell
yay -S hyprland-meta-git
```
如果你选择使用AUR中的`git`版本, 你可以使用 [Chaotic Aur](https://aur.chaotic.cx/)获取预构建的二进制文件.

如果出现错误你可以使用[downgrade](https://github.com/archlinux-downgrade/downgrade)来降级.

{{% /details %}}

{{% details title="Nix" closed="true" %}}

在你的NixOS配置中启用Hyprland:

```nix
programs.hyprland.enable = true;
```

获取详情, 读[Nix页面](../../Nix).

{{% /details %}}

{{% details title="openSUSE*" closed="true" %}}

Hyprland是factory的一部分,从快照20230411开始.安装它只需使用zypper

```sh
sudo zypper in hyprland
```
或者通过YaST2软件安装"hyprland"包.

为了使`hyprpm`识别其依赖关系, 你还需要安装 `hyprland-devel`:

```sh
sudo zypper in hyprland-devel
```

或者, 跟随如下说明["手册(手动构建)"](#manual-manual-build)来自行构建Hyprland.

注意: _Hyprland不适用于Leap, 因为Hyprland需要的大多数库(和编译器)都太老了._

{{% /details %}}

{{% details title="Fedora*" closed="true" %}}

在 Fedora 39+, 运行:

```sh
sudo dnf install hyprland
sudo dnf install hyprland-devel # 如果你想用构建插件 (使用 hyprpm)
```

更快的更新和额外的软件包可在
[solopasha/hyprland](https://copr.fedorainfracloud.org/coprs/solopasha/hyprland)
Copr仓库获得.

如果你在使用老版本的 Fedora,你也可以按照
[这个](https://github.com/hyprwm/Hyprland/discussions/284)
说明自行编译

{{% /details %}}
{{% details title="Debian*" closed="true" %}}

Hyprland 最近被纳入 SID 和 trixie 仓库, 可使用以下命令安装

```sh
sudo apt install hyprland
```

注意: 即使Hyprland 以被纳入 trixie 仓库, 仍推荐从 SID 安装, 因为 trixie 仓库中某些依赖已过时.

或者, 你也可以按照
["手册 (手动构建)"](#manual-manual-build) 来自行构建Hyprland.

{{< callout type=info >}}

Hyprland 不适用于 Bookworm 因为他的软件包太旧.

{{< /callout >}}

{{% /details %}}

{{% details title="Gentoo*" closed="true" %}}

hyprland 包在 main tree 中可用:

```sh
emerge --ask gui-wm/hyprland
```

其它软件包, 如 hyprlock, hypridle, xdg-desktop-portal-hyprland,
hyprland-plugins, hyprpaper 和 hyprpicker 在
[GURU](https://wiki.gentoo.org/wiki/Project:GURU) overlay 中可用.
作为 hyprland-contrib 包的一部分, GURU中也提供了社区贡献的脚本.

```sh
eselect repository enable guru
emaint sync -r guru

emerge --ask gui-apps/hyprlock
emerge --ask gui-apps/hypridle
emerge --ask gui-libs/xdg-desktop-portal-hyprland
emerge --ask gui-apps/hyprland-plugins
emerge --ask gui-apps/hyprpaper
emerge --ask gui-apps/hyprpicker
emerge --ask gui-wm/hyprland-contrib
```

有关 USE flags 和更多详细信息, 请参阅
[Gentoo wiki page](https://wiki.gentoo.org/wiki/Hyprland) 中有关Hyprland的部分.

{{% /details %}}

{{% details title="FreeBSD*" closed="true" %}}

Hyprland 及其相关已被纳入默认仓库:

- [hyprland](https://www.freshports.org/x11-wm/hyprland)
- [hyprpaper](https://www.freshports.org/x11/hyprpaper)
- [hyprpicker](https://www.freshports.org/x11/hyprpicker)
- [xdg-desktop-portal-hyprland](https://www.freshports.org/x11/xdg-desktop-portal-hyprland)
- [Other Wayland stuff](https://www.freshports.org/wayland/)

{{% /details %}}

{{% details title="Ubuntu*" closed="true" %}}

Hyprland 已被纳入 Ubuntu 24.10 Oracular Oriole universe 仓库, 可使用以下方式安装

```bash
sudo add-apt-repository universe && sudo apt-get update && sudo apt-get install -y hyprland
```

{{< callout type=info >}}

注意: 以上是 Ubuntu 24.10 (Unreleased) 版本

{{< /callout >}}

从 Source 中安装 Hyprland, 首先安装以下依赖:

```bash
sudo apt-get install -y meson wget build-essential ninja-build cmake-extras cmake gettext gettext-base fontconfig libfontconfig-dev libffi-dev libxml2-dev libdrm-dev libxkbcommon-x11-dev libxkbregistry-dev libxkbcommon-dev libpixman-1-dev libudev-dev libseat-dev seatd libxcb-dri3-dev libegl-dev libgles2 libegl1-mesa-dev glslang-tools libinput-bin libinput-dev libxcb-composite0-dev libavutil-dev libavcodec-dev libavformat-dev libxcb-ewmh2 libxcb-ewmh-dev libxcb-present-dev libxcb-icccm4-dev libxcb-render-util0-dev libxcb-res0-dev libxcb-xinput-dev libtomlplusplus3
```

你还需要从 Source 构建最新 wayland, wayland-protocols, 和
libdisplay-info 的标记版本.

你也可以安装 `xdg-desktop-portal-wlr` 或 `xdg-desktop-portal-hyprland` , 用于屏幕共享

```bash
sudo apt-get install -y xdg-desktop-portal-wlr
```

_不幸的是, `xdg-desktop-portal-hyprland` 仍未纳入 Ubuntu 仓库 所以你必须从 source 中构建它_

查看
[The xdph GitHub repo's readme](https://github.com/hyprwm/xdg-desktop-portal-hyprland). 参考
[XDPH](../../Hypr-Ecosystem/xdg-desktop-portal-hyprland) 和
[Ubuntu Guide For Installing And Building Hyprland Gist](https://gist.github.com/Vertecedoc4545/3b077301299c20c5b9b4db00f4ca6000)
了解更多信息.

{{< callout type=warning >}}

请注意, 由于Ubuntu通常落后于依赖项, 因此无法保证构建过程能够正常工作.
即使是这样, 它也有可能在未来的某个时候奔溃.

{{< /callout >}}

{{< callout >}}

始终使用最新版本的 Ubuntu 作为最新的依赖.

注意: 因人而异, 因为 GDM 在 Hyprland 上有一些错误. 查看 [大师教程](../Master-Tutorial) 了解更多信息.

如果有什么问题, 请参考要点.

<!-- For some reason uncommenting the line below creates an unwanted <pre><div></pre> in the page. -->
<!-- {{< /callout >}} -->

{{% /details %}}

{{% details title="Void Linux*" closed="true" %}}

Hyprland 不适用于 Void Linux's 官方仓库
[由于包装理念的冲突](https://github.com/void-linux/void-packages/issues/37544).
但是, [第三方仓库](https://github.com/Makrennel/hyprland-void)
可以使用 GitHub Actions 在 CI 中构建的
[二进制包](https://github.com/Makrennel/hyprland-void/tree/repository-x86_64-glibc)
.

你可以通过创建包含以下内容的
`/etc/xbps.d/hyprland-void.conf` 文件来添加此仓库:

```plain {filename="/etc/xbps.d/hyprland-void.conf"}
repository=https://raw.githubusercontent.com/Makrennel/hyprland-void/repository-x86_64-glibc
```

然后你可以像安装其他软件包一样安装这些软件包:

```sh
sudo xbps-install -S hyprland
sudo xbps-install -S hyprland-devel # 如果你想用插件
sudo xbps-install -S xdg-desktop-portal-hyprland

xbps-query -Rs hypr # 这将要求你已经使用 xbps-install -S 接受了仓库的指纹
```

更多信息, 请参阅
[hyprland-void README](https://github.com/Makrennel/hyprland-void/blob/master/README.md),
包括如何使用提供的模板
[手动构建](https://github.com/Makrennel/hyprland-void?tab=readme-ov-file#manually-building)
适用于 Void Linux 的 Hyprland 信息.

{{% /details %}}

{{% details title="Slackware*" closed="true" %}}

```plain
hyprland-bin (SlackBuilds) - Slackware的预构建版本以准备好安装
```

默认情况下, 当前版本的Slackware上未安装Hyprland.

有关安装此版本的详细说明, 请参阅 [此处](https://slackbuilds.org/repository/15.0/desktop/hyprland-bin/)

{{% /details %}}

{{% details title="Alpine*" closed="true" %}}

Hyprland在 Alpine [测试仓库](https://wiki.alpinelinux.org/wiki/Repositories#Testing) 中可用, 通过添加以下内容在 `/etc/apk/repositories` 中启用

```plain {filename="/etc/apk/repositories"}
http://dl-cdn.alpinelinux.org/alpine/edge/testing
```

这仅适用于 Alpine linux edge, 不适用于任何稳定版本. 如需在稳定版本上使用, 请参阅 [Alpine wiki](https://wiki.alpinelinux.org/wiki/Repositories#Using_the_testing_repository_on_stable_branches)

在启用仓库之后, 以下命令将安装 hyprland 及其依赖.


```plain
apk add hyprland
```

{{% /details %}}

{{% details title="Ximper*" closed="true" %}}

从Sisyphus安装:

```bash
epmi hyprland
epmi hyprland-devel # 如果你想使用插件
```

或者旧版渲染器版本:

```bash
epmi hyprland-legacyrenderer
```

生态系统:

```bash
epmi xdg-desktop-portal-hyprland
epmi hypridle
epmi hyprpaper
epmi hyprpicker
```

{{% /details %}}

{{% details title="Solus*" closed="true" %}}

为Solus, 运行:

```bash
sudo eopkg install hyprland
```

{{% /details %}}

_**\* 非官方, 没有官方支持提供. 这些说明由社区驱动, 并且不保证其有效性.**_

### 手册 (Releases, 仅Linux)

1. 下载最新 release.
2. 复制二进制文件 (Hyprland, hyprctl, hyprpm) 到 `/usr/bin/`.
3. 复制 desktop entry (`example/hyprland.desktop`) 到
   `/usr/share/wayland-sessions/`

示例配置在 `example/hyprland.conf`.

为了以后更新, 你可以覆盖二进制文件 (Hyprland, hyprctl,
hyprpm) . 你不需要更新其他任何内容.

### 手册 (手动构建)

依赖:

{{< callout type=info >}}

请注意 Hyprland 使用 C++26 标准, 所以你的编译器和 C++ 标准库都必须支持 (`gcc>=14` 或 `clang>=18`).

{{< /callout >}}

{{% details title="Arch" closed="true" %}}

```plain
yay -S ninja gcc cmake meson libxcb xcb-proto xcb-util xcb-util-keysyms libxfixes libx11 libxcomposite libxrender pixman wayland-protocols cairo pango seatd libxkbcommon xcb-util-wm xorg-xwayland libinput libliftoff libdisplay-info cpio tomlplusplus hyprlang-git hyprcursor-git hyprwayland-scanner-git xcb-util-errors hyprutils-git hyprgraphics-git
```

_(如果列表中缺少任何包, 请提交一个pr或打开issue)_

{{% /details %}}

{{% details title="OpenSuse" closed="true" %}}

```sh
zypper in gcc-c++ git meson cmake "pkgconfig(cairo)" "pkgconfig(egl)" "pkgconfig(gbm)" "pkgconfig(gl)" "pkgconfig(glesv2)" "pkgconfig(libdrm)" "pkgconfig(libinput)" "pkgconfig(libseat)" "pkgconfig(libudev)" "pkgconfig(pango)" "pkgconfig(pangocairo)" "pkgconfig(pixman-1)" "pkgconfig(vulkan)" "pkgconfig(wayland-client)" "pkgconfig(wayland-protocols)" "pkgconfig(wayland-scanner)" "pkgconfig(wayland-server)" "pkgconfig(xcb)" "pkgconfig(xcb-icccm)" "pkgconfig(xcb-renderutil)" "pkgconfig(xkbcommon)" "pkgconfig(xwayland)" "pkgconfig(xcb-errors)" glslang-devel Mesa-libGLESv3-devel tomlplusplus-devel
```

(如果你删除 `Mesa-libGLESv3-devel` 和 `pkgconfig(xcb-errors)` 这也应该适用于 RHEL/Fedora)

{{% /details %}}

{{% details title="FreeBSD" closed="true" %}}

```sh
pkg install git pkgconf gmake gcc evdev-proto cmake wayland-protocols wayland libglvnd libxkbcommon libinput cairo pango pixman libxcb
pkg install meson jq hwdata libdisplay-info libliftoff
export CC=gcc CXX=g++ LDFLAGS="-static-libstdc++ -static-libgcc"
```

{{% /details %}}

{{% details title="Ubuntu" closed="true" %}}

请参考上面的 Ubuntu 选项卡

{{% /details %}}

{{< callout type=warning >}}

除此之外, 您还需要一些 hypr\* 依赖项，这些依赖项可能会也可能不会为你选择的发行版打包:

- aquamarine
- hyprlang
- hyprcursor
- hyprutils
- hyprgraphics
- hyprwayland-scanner (仅构建)

{{< /callout >}}

### CMake (推荐)

```sh
git clone --recursive https://github.com/hyprwm/Hyprland
cd Hyprland
make all && sudo make install
```

_总是建议使用CMake, 因为这是Hyprland的预期安装方式._

### Meson

```sh
meson subprojects update --reset
meson setup build
ninja -C build
ninja -C build install --tags runtime,man
```

请参考 [调试](../../Contributing-and-Debugging) 以了解如何构建和调试.

## 启动时奔溃

查看 [奔溃和错误](../../Crashes-and-Bugs).

## 自定义安装 (旧版渲染器, 等)

1. cd 进入 hyprland 仓库.
2. 对于旧版渲染器:

```bash
make legacyrenderer
sudo make install
```

{{< callout type=info >}}

_请注意旧版渲染器也许不支持一些图形功能._

{{< /callout >}}

3. 其他配置: (在你的预设中替换 `<PRESET>` : `release`, `debug`,
   `legacyrenderer`, `legacyrendererdebug`)

```bash
make <PRESET> && sudo cp ./build/Hyprland /usr/bin && sudo cp ./example/hyprland.desktop /usr/share/wayland-sessions
```

## 自定义构建标志

为应用自定义构建标志 你必须要放弃make.

以支持的自定义构建标志:

```bash
LEGACY_RENDERER - 编译带有旧版渲染器 (见上文)
NO_XWAYLAND - 移除 XWayland 支持
NO_SYSTEMD - 移除 systemd 依赖
```

标志可以这样传递给CMake:

```bash
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -D<FLAG>:STRING=true -B build -G Ninja
```

将 `<FLAG>` 更改为自定义构建标志之一. 可同时使用多个标志, 通过添加更多 `-D<FLAG_2>:STRING=true`.

`BUILD_TYPE` 也可以更改为 `Debug`.

构建, 运行:

```bash
cmake --build ./build --config Release --target all
```

如果在 `Debug` 中配置, 也修改 `--config` 为 `Debug` .

安装, 运行:

```bash
sudo cmake --install ./build
```

## 运行在虚拟机中

_因人而异, 这不受官方支持._

浏览 [libvirt Arch wiki page](https://wiki.archlinux.org/title/Libvirt) 获得
`libvirt`, `virsh`, 以及 `virt-viewer` 设置并安装.

```bash
# 安装 libvirt 和 qemu .
sudo pacman -S libvirt virt-viewer qemu-common
# 将你自己添加到 libvirt 组.
sudo usermod -a -G libvirt USER # Replace 'USER' with your username.
# 启用并启动 libvirtd.
systemctl enable --now libvirtd
```

跳转至
[arch-boxes gitlab](https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages)
并下载最新版 arch qemu 基础镜像. 你可以通过任意 arch 镜像源来下载.

```bash
curl https://geo.mirror.pkgbuild.com/images/latest/Arch-Linux-x86_64-basic.qcow2 \
  -o ~/Downloads/arch-qemu.qcow2 # 或其他你想下载到的地方.
```

使用 virsh 创建虚拟机.

```bash
# 使用 virt-install (已包含在 libvirt) 从镜像安装虚拟机.
virt-install \
  --graphics spice,listen=none,gl.enable=yes,rendernode=/dev/dri/renderD128 \
  --name hypr-vm \
  --os-variant archlinux \
  --memory 2048 \
  --disk ~/Downloads/arch-qemu.qcow2 \
  --import
```

使用 `virt-viewer` 连接, 这将在tty打开 `virt-viewer` 图形会话. 
默认登陆用户为 'arch' 密码为 'arch' .

{{< callout >}}

确保 --attach 标志被使用, 启用 virgl 使我们不得不禁用监听.
这意味着我们无法与远程显示器建立直接的　TCP/UNIX　套接字连接. 
--attach要求libvirt为显示器提供一个预连接的套接字.\*

{{</ callout >}}

```sh
virt-viewer --attach hypr-vm
```

最后, 请按照上述说明进行以下任一操作
[从 aur 安装 hyprland-git](#installation) 或
[手动构建](#manual-manual-build).
{{< callout >}}

确保你安装了 `mesa` 作为 OpenGL 驱动. virgl 驱动以包含在 `mesa`.

{{</ callout >}}
