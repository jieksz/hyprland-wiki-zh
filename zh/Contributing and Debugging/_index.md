---
weight: 13
title: 贡献和调试
---

# 贡献指导

PR, 代码风格和代码 FAQs 在 [这](./PR-Guidelines)

对于问题, 请见
[指导](https://github.com/hyprwm/Hyprland/blob/main/docs/ISSUE_GUIDELINES.md)

## 在调试模式构建

### 依赖包

见 [手动构建](https://wiki.hyprland.org/Getting-Started/Installation/#manual-manual-build) 中所述依赖.

### 推荐, CMake

安装 VSCode C/C++ 和 CMake 工具插件并使用.

我附上一份
[example/launch.json](https://github.com/hyprwm/Hyprland/blob/main/example/launch.json)
你可复制到你的项目根目录的 .vscode/ 目录.

这样, 你就可以在调试中构建, 转到调试选项卡并点击
`(gdb) Launch`.

_note:_ 你也许想在你配置的 debug {} 部分设置 `watchdog_timeout = 0`.
否则 Hyprland 将在遇到断点时注意到它挂起并在你继续后退出崩溃.

### 自定义, CLI

`make debug`

以你喜欢的方式附上配置文件

### Meson

```console
meson setup build -Dbuildtype=debug
ninja -C build
```

### Nix

为在调试模式构建包你需要像这样重写它:

```nix
hyprland.override {
  debug = true;
};
```

此代码可以放在 NixOS/Home Manager模块的 `package`属性中.

## 运行
当 Hyprland 运行在调试模式时, 配置为
`~/.config/hypr/hyprlandd.conf` 日志可在以下位置
`$XDG_RUNTIME_DIR/hypr/[INSTANCE SIGNATURE]/hyprlandd.log` 找到.

## 嵌套 Hyprland


Hyprland 可被嵌套运行在窗口. 为此, 确保你做了以下几点:

- 调试模式构建
- 从你的调试配置(`hyprlandd.conf`)中删除所有 `exec=` 和 `exec-once=` 关键字
- 确保没有键绑定冲突 (为你的键绑定不同的 mod) 

## LSP 和格式化

如果你想在一个不会自动设置 LSP 的编辑器中获得适当的 LSP 支持, 请使用 cland.
你可能会注意到, 由于我们还没有生成编译命令, 因此会出现一堆警告, 要执行此操作, 请运行:

```sh
cmake -S . -B build/ -G Ninja -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
```

此为, 在提交 PR 前请使用 clang-format 进行格式化,
要仅对于你的更改进行操作, 请在项目根目录运行 `git-clang-format`.

## 日志, 转储, 等等

你可使用日志和 GDB 调试器, 但将 Hyprland 作为驱动程序在调试编译中运行并使用一段时间可能会对更多随机错误有更深的了解.

当 Hyprland 奔溃, 同时使用 `coredumpctl` 和 `coredumpctl info PID` 查看转储.
有关 `coredumpctl` 的更多信息, 请参考下面的说明.

你可使用以下命令

```sh
watch -n 0.1 "grep -v \"arranged\" $XDG_RUNTIME_DIR/hypr/$HYPRLAND_INSTANCE_SIGNATURE/hyprland.log | tail -n 40"
```

用于实时日志. (在调试构建中将 `hyprland` 替换为 `hyprlandd`)

### 我该如何获得 coredump?

见
[`ISSUE_GUIDELINES.md`](https://github.com/hyprwm/Hyprland/blob/main/docs/ISSUE_GUIDELINES.md).
