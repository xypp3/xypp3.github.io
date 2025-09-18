---
title: 'tmux; Windows for SSH'
pubDate: 2025-09-18 12:31
description: 'TLDR; very basics of tmux to make your server ssh experience a bajillion times smoother'
author: 'xypp3'
tags: ['linux', 'tools', 'tmux']
---

Before you rage that tmux isn't just used when connecting to servers, I know. It's just where I find it most useful and where I recommend people get started with it cause it has the highest bang for buck.

## $ whatis tmux
tmux is a [terminal multiplexer](https://github.com/tmux/tmux/wiki/Getting-Started). Done, everyone pack your bags, you know it all. Big word aside it essentially is a way to manage terminal sessions/windows/panes and more! Why would this be useful in a remote server environment?
1. Allows you to have multiple windows at once. (e.g. editing file 1, while compiling, while reading document, while remote copying files, while editing file 2, while having `htop` open, while editing file 1, et cetera)
2. Allow you to "detach" from your remote "session" so that you can leave jobs running without being directly connected to the server

These two uses are what I gain most from tmux and what I think most people would gain from it as well.

## $ tldr tmux
For me tmux has 2 key concepts: sessions and windows. A "session" is a the outer layer of the tmux wrapper. Most things live in your session like windows (and panes but I don't use em so if you wanna go read up on it). Once you're in a tmux session life is good and you can start gaining the benefits above. Second concept is "windows", where each window is like new browser tab that you can do anything in (ala long list above). And this is it. These are the basics that let you get the two big boons of the terminal multiplexer in remote connections.

You will use commands/bindings/hotkeys to move around in tmux. The operations are:
- in terminal session
    - type `tmux` in your terminal to start a tmux session
    - type `tmux new-session -A`, to re enter a previous tmux session (will pick one at random if you have multiple but is fine)
- in tmux session
    - `ctrl+B C`, to create a window (notice how every window you create appears at the bottom with a name and number)
    - `ctrl+B n`, (where n is a number) moves you to that numbered window
    - `ctrl+B &`, closes the current tmux window
    - `ctrl+B D`, detaches you from your tmux session (in remote context tmux is staying alive while your local device disconnects from the ssh)
    - `ctrl+D` to disconnect tmux from ssh i.e. fully leaving the server

## Additional goodies
Some small tweaks that improve my tmux life:

### In ssh config
To have tmux autolaunch on ssh, I add this line to my ssh config for that specific host:
`RemoteCommand tmux new-session -A`

I found this in a blog post somewhere and can't go back.

### In tmux config
Some downsides of tmux is that you don't have mouse access by default but that can be enabled. In the server create a `.tmux.conf` file for small tmux configs
- `set -g mouse on` to turn mouse on

Another thing you can add to your config file is making the default pane 1 instead of 0 to make toggling back and forth a bit easier:
```
set -g base-index 1
setw -g pane-base-index 1 
```

Last thing that I usually have is a way to copy things from the server to my device and back. Cause your clipboard is no longer shared. I recommend the plugin `tmux-yank` or also a terminal shortcut which is to hold shift as you are highlighting and copying.

## Final thoughts
If you love tmux and want to explore every nook and cranny go for it. This is what I gain from it and for now my exploration of it ends here. Same with customizing it. You could go ham and customise the keybindings and all to the max. But I find that the defaults are "good enough" and so live with them. However, even just the very basics are absolutely huge for me. Anywho, hope you enjoyzed and have a good day. Byeeeeee
