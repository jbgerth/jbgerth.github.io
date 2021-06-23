---
layout: post
title: "My terminal setup for Windows"
description: "A proper shell experience on Windows"
categories: [terminal]
tags: [terminal, windows, linux, setup, development, mac]
redirect_from:
  - /2020/05/29/
---

## Introduction

Usually I daily drive a Windows machine. On it is, where I get almost all my personal development work done. Sometimes I worked on Linux machines, but mostly for servers or IoT tasks. After being "forced" to use a Mac Book Pro for work, I explored the for me new eco system and try to take a some lessons to apply on Windows at home.

The first major difference I noticed, is that the terminal experience on MacOS is superb. It feels more like Linux in that regard, which is a good thing. All the commands in the shell work as I would expect them to. Also the default terminal iTerm on Mac supports everything you need and is regularly updated. Lastly the search feels quicker than with Windows 10 start menu, be it with the search bar, to find a program or with `fzf` on the CLI.  

Windows on the other hand always lacked behind in the console experience. It was missing a deeply integrated Linux type shell, a good terminal and a package manager. This changed in recent years. The issues are addressed with a few different tools:

- The **Windows Terminal** as a terminal
- Microsoft **PowerToys** as quality of life improvements
- **Chocolatey** as a package manager
- The **Linux Subsystem for Windows** a.k.a. WSL as a proper linux shell

In this post I want to capture the tools I use to build a better Windows development experience. The installation and usage of the tools can be found on the project pages. Some of the mentioned tools are available for PowerShell or WSL. I choose WSL version, if it is possible, because I am more comfortable with it.

## Windows Tools

### Windows Terminal

The Windows Terminal is better [Terminal](https://github.com/microsoft/terminal) than the default Powershell from Windows. It runs fast and looks nice. Additionally it supports multiple tabs. In each tab a different shell can be launched. That way multiply shells can be used at the same time, e.g. one for Powershell and a second one for WSL, without the need of closing a session or opening another window.

Compared to the normal Command Prompt, the Terminal allows for different fonts. Other fonts enable more shell integrations. For example, if a font such as `Fira Code` is used, power line integrations can be shown.

### Windows PowerToys

[PowerToys](https://docs.microsoft.com/de-de/windows/powertoys/) is a selection of tools developed by Microsoft employees, which provides productivity tools for power users. They provide some of the functionality exclusive to Mac OS.

Most notably is the quick search bar [PowerToys Run](https://docs.microsoft.com/de-de/windows/powertoys/run). It works the same as the serach in Mac OS and can be accessed by hitting `<ALT> + <SPACE>`. In the settings it can be configured, what it is searching in, e.g. programms, files, directories etc..
It also does simple math operation and can even run shell commands.
![Run in action](/assets/img/2020-09-05/pt-powerrun-demo.gif)

Also included is the tile manager [FancyZones](https://docs.microsoft.com/de-de/windows/powertoys/fancyzones), to order all windows in preset zones. These zones go beyond Windows normal ability of having two windows on the same screen. It is possible to have one main window in the middle with two smaller one on the sides. I do not use it as often, but it comes in handy sometimes.
![Possible FancyZones](/assets/img/2020-09-05/pt-fancyzones-multimon.png "titel")

Two other cool features are the Markdown preview for the explorer and a shortcut Guide, that is displayed when holding down the windows key.

### Chocolatey

[Chocolatey](https://chocolatey.org) is a package manager for Windows. It works quite well. A lot of application such as VS code, Spotify or NVIM, to name a few, can be installed by running `choco install [name]`.

It has a few caveats thought. First it needs to be run in administrator mode, to install anything. Therefore the terminal itself needs to be launched as an administrator. This is not a problem, but it does disrupt the workflow, especially compared to calling `sudo`.

One other limitation is, that some features are looked away behind a paywall. Those feature are not needed in day to day use, but I missed them sometimes. For example the freedom to choose the installation directory.

## WSL 2

Since Windows 10 Version 2004, Build 19041 Microsoft improved the performance of the build in Linux distributions by a lot. [WSL 2](https://docs.microsoft.com/de-de/windows/wsl/wsl2-index) is almost as fast as native linux as it runs directly on the kernel without emulation or for example the previous file limit from WSL 1. The speed enables WSL 2 to be used instead of any VMs and provides developers with most needed tools, that are usually hard to come by on Windows.

## Classic Terminal Tools

The following tools can be used on either Powershell or WSL. When in doubt I do prefer WSL, because I am more used to the commands. The tools are only mentioned very briefly. All of them can be a huge time sink with a lot optimization and customization to do.

### NVIM

[NVIM](https://neovim.io)  is a modern implementation of VIM. I have no particular reason to use this over VIM. In general it is a fast editor for editing files in the CLI, it is highly customizable and is super fast once the hot keys are learned. I use it mostly for smaller edits and if I am working on a server. Most of the time I do prefer a full IDE such as VS code.

I use NVIM together [vim-plug](https://github.com/junegunn/vim-plug), to install the following plugins:

#### ~/.config/nvim/init.vim

```vim
call plug#begin('~/.vim/plugged')

Plug 'airblade/vim-gitgutter'
Plug 'editorconfig/editorconfig-vim'
Plug 'itchyny/lightline.vim'
Plug 'junegunn/fzf'
Plug 'junegunn/fzf.vim'
Plug 'mattn/emmet-vim'
Plug 'scrooloose/nerdtree'
Plug 'terryma/vim-multiple-cursors'
Plug 'tpope/vim-eunuch'
Plug 'tpope/vim-surround'
Plug 'w0rp/ale'
Plug 'vim-airline/vim-airline-themes'
Plug 'valloric/youcompleteme'

call plug#end()
```

To enable `vim-plug` for WSL call:

```sh
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

Other install options for different distributions can be found on the Github page. The plugins improve the general feel and quality of life things. For example it adds fuzzy find, auto complete and a git power line.

### tmux

The terminal multiplexer a.k.a. [tmux](https://github.com/tmux/tmux) is an old school Linux tool. It enables users running multiple shell sessions in one terminal window and keeps programs running after the CLI session closes. For both cases tmux comes in very handy. It has a bunch of option further and configs, which are worth getting into.  

### Git

[Git](https://git-scm.com) became almost the default version control system for software project. It is available as plugins for almost any IDE, but the CLI version provides some easy general access, which changes between IDEs.

Like for this very websites, I use it for any more complex project.

### fzf

[fzf](https://github.com/junegunn/fzf)  is for finding past commands in a very quick fashion. Fuzzy finder matches better than the default search with `<CTRL> + r`. It shows many options, if there are multiple matches. Those results can be navigated with the error keys or `h j k l` for those, who like VIM.

### Zsh

[Zsh](https://www.zsh.org) or Zshell is a competitor to bash. Zsh provides a lot of options and extensions to configure the shell experience. The extensions enable a faster workflow, with for example better tab completion for various tools, nicer themes or a git power line. A good starting point is [oh-my-zsh](https://ohmyz.sh) with sensible defaults.

Below is my current configuration of zsh. It requirers oh-my-zsh, zsh-autosuggestions and zsh-syntax-highlighting to be installed separately. See the comments in the config on how to install them.

#### ~/.zshrc

```bash
# Oh my zsh config location
export ZSH="/home/[user]/.oh-my-zsh"

# Theme
ZSH_THEME="spaceship"

# Timestamp format
HIST_STAMPS="yyyy-mm-dd"

# Plugins
plugins=(
        git
        node
        npm
        python
        ubuntu
        docker
        tmux
        fzf
# sudo git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
        zsh-autosuggestions
# sudo git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
        zsh-syntax-highlighting
        history-substring-search
        colored-man-pages
)

# Source oh my zsh
source $ZSH/oh-my-zsh.sh

# Default editor for SSH sessions
if [[ -n $SSH_CONNECTION ]]; then
   export EDITOR='vim'
else
   export EDITOR='nvim'
fi

# Set to use neo vim instead of vim
alias vim=nvim
alias vi=vim
```

The pictures are taken from the Microsoft pages.
