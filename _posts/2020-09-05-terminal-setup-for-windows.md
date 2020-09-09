---
layout: post
title: "My terminal setup for Windows"
description: "Seeing how it is done on Mac and bringing it home to my Windows machine"
categories: [terminal]
tags: [terminal, windows, linux, setup, development, mac]
lastmod: 2020-09-09
redirect_from:
  - /2020/05/29/
---

## Introduction

Usually I always used Windows for most things, including almost all my development work. Sometimes I worked on Linux machines, but mostly for servers or IoT tasks. After being "forced" to used a Mac Book Pro for work, I could explore using a proper terminal during development. The terminal experience on MacOS is superb. Everything runs super fast. No GUI is in your way.

Windows on the other hand always lacked behind in the console experience. It was missing a Linux type terminal. This changed in the last years. Some of the notable changes, that led me to write this post and change my setup, are:

- The **Linux Subsystem for Windows** a.k.a. WSL was introduced and almost perfected in WSL 2
- Microsoft brought **PowerToys** back
- There is a new fancy **Windows Terminal** available
- The PowerShell got a package manager with **chocolatry**
- Linux CLI tools can be directly called from Windows using a combination WSL and Powershell

In this post I want to capture the tools I use to build a better Windows CLI experience. The installation and usage of the tools can be found on the project pages. Some of the mentioned tools are available for PowerShell or WSL. I choose WSL version, if it is possible, because I am more comfortable with it. The PowerShell commands feel often very long and not intuitive from a UNIX perspective.

## WSL 2

Since Windows 10 Version 2004, Build 19041 Microsoft improved the performance of the build in Linux distributions by a lot. [WSL 2](https://docs.microsoft.com/de-de/windows/wsl/wsl2-index) is almost as fast as native linux as it runs directly on the kernel without emulation or for example the previous file limit from WSL 1. The speed enables WSL 2 to be used instead of any VMs and provides developers with most needed tools, that are usually hard to come by on Windows.

## Windows Tools

### Windows Terminal

Better [Terminal](https://github.com/microsoft/terminal) than the default Powershell from Windows or other available CLIs. It runs fast and looks nice. Additionally it supports multiple tabs. In each tab another shell can be launched. That way multiply shells can be used at the same time, e.g. one for Powershell with chocolatry and a second one for WSL to run code.

### Windows PowerToys

A selection of tools developed by Microsoft employees, which provides productivity tools for power users. Most notably are the quick search bar (PowerToys Run), a tile manager (Fancy Zones) and a shortcut Guide.

All of those are non essential, but nice to have. In the future Microsoft hinted, that they will be adding more tools.

### Chocolatry

[Chocolatry](https://chocolatey.org) is a package manager for Windows. It works quite well. A lot of application such as VS code, Spotify or nvim to name a few can be installed using 'choco install [name]'.

It has a few caveats thought. First it needs to be run in administrator mode, to install anything. This is not a problem, but it does disrupt the workflow compared to calling "sudo" like on most other non Windows machines.

One other limitation is, that some features are looked away behind a paywall. Those feature are not needed in day to day use, but I missed them sometimes.

## Classic Terminal Tools

The following tools can be used on either Powershell or WSL.

### NVIM

[NVIM](https://neovim.io)  is a modern implementation of VIM. I have no particular reason to use this over VIM. In general it is a fast editor for editing files in the CLI, it is highly customizable and is super fast once the hot keys are learned.

I used [vim-plug](https://github.com/junegunn/vim-plug), to install the following plugins:

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

### tmux

The terminal multiplexer a.k.a. [tmux](https://github.com/tmux/tmux) is an old school Linux tool. It enables users running multiple CLIs in one terminal window or keep programs running after a CLI session closes. For both cases tmux comes in very handy. It has a bunch of option further and configs, which are worth getting into.  

### Git

[Git](https://git-scm.com) became almost the default version control system for software project. It is available as plugins for almost any IDE, but the CLI version provides some easy general access, which changes between IDEs.

### fzf

Finding past commands in a very quick fashion. Fuzzy find matches better than the default search with `<CTRL> + r`. It shows many options, if there are multiple matches. This feels better and brings the correct command faster.

### Zsh

Zsh or Z shell is a different competitor to bash. Zsh provides a lot of options and extensions to configure the shell experience. The extensions enable a faster workflow, with for example better tab completion for various tools, nicer themes or a git line. oh-my-zsh provides a good starting point with sensible defaults. Below is my current configuration of zsh. It requirers oh-my-zsh, zsh-autosuggestions and zsh-syntax-highlighting to be installed separately.

#### ~/.zshrc

```bash
# Oh my zsh config location
export ZSH="/home/[user]/.oh-my-zsh"

# Theme
ZSH_THEME="fishy"

# Timestamp format
HIST_STAMPS="yyyy-mm-dd"

# Plugins
plugins=(
	kubectl
	git
	ubuntu
	python
	golang
	scala
	sbt
	docker
	fzf
	sudo
	ls
	tmux
	zsh-autosuggestions
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
```
