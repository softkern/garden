---
title: 终端新体验：Alacritty 和 Zellij 的高效搭配
description: Alcritty和Zellij的基础体验和配置
date: 2024-12-11
tags:
    - alacritty
    - zellij
    - terminal
---

## 简介
Alacritty是一个高性能、现代化的终端模拟器，使用Rust开发，并利用GPU进行加速，保证流程的输入输出体验；但是Alacritty不提供多标签以及分屏之类的功能，因此需要终端复用器来提供相应功能。

而Zellij就是一个新型终端复用器，也是使用Rust进行开发，并花费了很多心思在性能方面，也同样拥有高性能的特点，与Alacritty堪称绝配。

## 安装
在Mac下的安装非常简单，只需两条命令:
```shell
brew install alacritty
brew install zellij
```

## 配置
本文只介绍一些简单的基础配置，主要包含两者结合使用的配置。

Alacritty的配置:
```toml title="~/.config/alacritty/alacritty.toml"
[general]
import = [
  "~/.config/alacritty/tokyonight_moon.toml",
  #"~/.config/alacritty/catppuccin-mocha.toml"
]
live_config_reload = true

[env]
TERM = "xterm-256color"

[window]
title = "Alacritty"
dimensions = { columns = 0, lines = 0 }
padding = { x = 12, y = 10 }
dynamic_padding = true
opacity = 1

[font]
normal = { family = "CommitMono Nerd Font", style = "Regular" }
bold = { family = "CommitMono Nerd Font", style = "Bold" }
italic = { family = "CommitMono Nerd Font", style = "Italic" }
bold_italic = { family = "CommitMono Nerd Font", style = "Bold Italic" }
size = 14

[terminal]
shell = { program = "/opt/homebrew/bin/zellij", args = ["options", "--default-shell", "/opt/homeb
rew/bin/fish"] }
```

我这里是使用了 [Tokyonight](https://github.com/folke/tokyonight.nvim/blob/main/extras/alacritty/tokyonight_moon.toml) 的主题，下载之后放到 `~/.config/alacritty/`，然后在配置中导入就可以生效。

另外 `[terminal]` 部分是两者结合的关键，这条配置能够在启动Alacritty 的时候自动进入 Zellij 中。



Zellij的配置，只包含了修改的部分:

```kdl title="~/.config/zellij/config.kdl"
theme "tokyo-night"
default_shell "fish"
default_layout "compact"
pane_frames false
```

配置之后效果如下:
![alacritty + zellij](https://img.softkern.com/images/2024/12/2f37bae6e1e96bb7693d8d800452489b.webp)

这里只是简要介绍了基础配置，更多的内容可以查看 [Alacritty](https://alacritty.org/config-alacritty.html) 和 [Zellij](https://zellij.dev/documentation/configuration) 的官方文档。
