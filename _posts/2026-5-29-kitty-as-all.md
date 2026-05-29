---
title: kitty as all -- to replace tmux and zellij
date: 2026-05-29 17:00:00 +0800
categories: [tools, terminal, productivity]
tags: [kitty, tmux, zellij]
---

Ok, like most people, i use tmux/zellij these multiplexer for a long time, and it did magic for me before.

I still remember, when i was young, eager and foolish, i searched across all the internet for any tips that may suit my taste, i spend a lot of time on how to arm my linux.

So i first tried out tmux, i didn't even know what problem it would solve, but it did magic to me that time, before that, if i want to multitask, i may run kitty then run another terminal emulator side by side like ghostty. At first i just port some up's config from bilibili, and i only modified it a bit using codex. And it works great for me.

Then i know zellij, since i kept learning rust again and again, i transfer my setup to zellij very fast.It is great, but has some small issues compared to tmux, it is more visually heavy and its session switch is not as convenient as tmux's.But i love it for its draggable window and its customized key to pop out some window, i could use that to run some common commmands like fastfetch and btop.

But in all both of them have some small issues, i could not preview images using yazi, some keybinding fighting some apps keybinding, i do care about simplicity. After some thought, i realized that i could use kitty's embedding functions to achieve everything i used to with tmux and zellij except persistence.

Yeah, so if you are just like me, running codex on a host machine and connect use a portable machine, if you need it to work while you close your lid, tmux is still a must, but at the remaining time, kitty is good enough.

## my configuration

Now please allow me to introduce my kitty.conf, and explain a little why and how.

```kitty.conf
font_family Maple Mono NF CN
font_size 14.0
background_opacity 0.8
hide_window_decorations yes
```

Choose my font and size and opacity, i hide window decorations for beauty.

```kitty.conf
# Cursor trail - animated trail following cursor jumps
cursor_trail 3
cursor_trail_decay 0.05 0.3
cursor_trail_start_threshold 2
# Cursor polish
cursor_blink_interval 0.75
cursor_stop_blinking_after 8.0
cursor_trail_color #f4efe7
```

Some cool cursor animation, and not very eye-catching, pleasant.

```kitty.conf
# Signature watermark
window_logo_path nastem-signature.png
window_logo_position top-right
window_logo_alpha 0.14
window_logo_scale 10
```

I add a customized image, my logo.

```kitty.conf
# --- 标签页管理 (Tabs) ---
map alt+o       new_tab
map alt+w       close_tab
map alt+right   next_tab
map alt+left    previous_tab
map alt+1       goto_tab 1
map alt+2       goto_tab 2
map alt+3       goto_tab 3
map alt+4       goto_tab 4
map alt+5       goto_tab 5
map alt+6       goto_tab 6
map alt+7       goto_tab 7
map alt+8       goto_tab 8
map alt+9       goto_tab 9
```

Some keymaps for changing tabs.

```kitty.conf
# --- 分屏管理 (Windows/Splits) ---
# 垂直分屏（左右）
map alt+v       launch --location=vsplit
# 水平分屏（上下）
map alt+s       launch --location=hsplit
# 关闭当前分屏
map alt+x       close_window

# --- 分屏间导航 ---
map alt+h       neighboring_window left
map alt+l       neighboring_window right
map alt+k       neighboring_window up
map alt+j       neighboring_window down

# --- 调整分屏大小 ---
map alt+shift+h resize_window narrower 3
map alt+shift+l resize_window wider 3
map alt+shift+k resize_window taller 3
map alt+shift+j resize_window shorter 3
```

Some keymaps for pane switch and creation.

```kitty.conf
# 一键最大化/恢复当前分屏（优雅替代 Tmux 的 Zoom 功能）
map alt+z toggle_layout stack
```

Useful if i want to zoom a pane.

```kitty.conf
tab_bar_style        powerline
tab_powerline_style round
tab_bar_edge top
```

I am used to the tab bar on the top and powerline is better looking for me compared to the default one.

```kitty.conf
# 允许远程控制
allow_remote_control yes
```

Useful so you could ask your agents to work with kitty.
