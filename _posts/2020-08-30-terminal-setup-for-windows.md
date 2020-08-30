---
layout: post
title: "My terminal setup for Windows"
description: "Seeing how it is done on Mac and bringing it home to my Windows machine"
categories: [terminal]
tags: [terminal, windows, linux, setup, development]
redirect_from:
  - /2020/05/29/
---

## Introduction

Usually I always used Windows for most things. Sometimes I worked on Linux machines, but mostly for servers. After being "forced" to used a Mac Book Pro for work, I could explore using a proper terminal during development. The terminal experience on MacOS is superb. Everything runs super fast. No GUI is in your way.

Windows on the other hand always lacked behind in the console experience. It was missing a Linux type terminal available. This changed in the last years. Some of the notable changes, that led me to write this post, are:

- The **Linux Subsystem for Windows** a.k.a. WSL was introduced.
- Microsoft brought **PowerToys** back
- There is a new fancy **Windows Terminal** available
- The PowerShell got a package manager with **chocolatry**
- Linux tools can be directly called from Windows

Over the past few weeks I try to achieve the same fluidity from Mac in Windows, because all in all I still prefer Windows over Mac.

## WSL 2

Since Windows 10 Version 2004, Build 19041 Microsoft improved the performance of the build in Linux distributions by a lot. [WSL 2](https://docs.microsoft.com/de-de/windows/wsl/wsl2-index) is almost as fast as native linux as it runs directly on the kernel without emulation or for example the previous file limit from WSL 1. The speed enables WSL 2 to be used instead of any VMs and provides developers with most needed tools, that are usually hard to come by on Windows.

## Windows Tools

### Windows Terminal

Better [Terminal](https://github.com/microsoft/terminal) than the default Powershell from Windows or other available CLIs. It runs fast and looks nice. Additionally it supports multiple tabs. In each tab another shell can be launched. That way multiply shells can be used at the same time, e.g. one for Powershell with chocolatry and a second one for WSL to run code.

### Windows PowerToys

A selection of tools developed by Microsoft employees, which provides productivity tools for power users. Most notably are the quick search bar (PowerToys Run), a tile manager (Fancy Zones) and a shortcut Guide.

All of those are non essential, but nice to have. In the future there should be even more tools added.

### Chocolatry

A package manager for Windows. It works quite well. A lot of application such as VS code, Spotify or nvim to name a few can be installed using 'choco install "name"'.

It has a few caveats thought. First it needs to be run in administrator mode, to install anything. This is not a problem, but it does disrupt the workflow compared to calling "sudo" like on most other non Windows machines.

One other limitation is, that some features are looked away behind a paywall.

## Classic Console Tools

The following tools can be used on either Powershell or WSL.

### NVIM

### TMUX

### Git

## Special shell setups

### POSH

### oh-my-zsh
