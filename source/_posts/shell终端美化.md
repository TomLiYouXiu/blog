---
title: shell终端美化
date: 2024-05-08 15:51:37
tags: 教程
categories: shell
thumbnail: "https://pic.imgdb.cn/item/663c472f0ea9cb1403e4c285.png"
---

# 打造酷帅的最强shell终端，效率直接快100倍！！！

## 什么是shell？

​		Shell 终端，也被称为命令行接口或控制台，是一种交互式用户界面，允许用户通过键入命令来与操作系统进行交互。

​		在 Shell 终端中，用户可以执行各种各样的操作，例如管理文件和目录，运行程序，监控系统状态，配置系统设置，等等。这些操作都是通过键入特定的命令来实现的。

​		Shell 终端的名称来源于 "shell"，这是一个用于描述用户和操作系统内核之间的接口的术语。Shell 提供了一个解释和执行用户命令的环境，而终端则是用户与 shell 交互的界面。

​		在 Unix 和类 Unix 系统（如 Linux）中，常见的 shell 包括 Bourne shell（sh）、Bourne Again shell（bash）、C shell（csh）、Korn shell（ksh）等。在 Windows 系统中，常见的 shell 包括命令提示符（cmd）和 PowerShell。

​		总的来说，Shell 终端是进行系统管理和开发工作的重要工具，对于理解操作系统的工作原理和进行高效的工作都非常有帮助。

## 前期准备

​		一个支持全彩的终端，我使用的是Windows terminal

### Windows terminal

​		Windows Terminal 是微软开发的一个新的、现代的、功能丰富的、开源的终端应用程序，用于访问命令行工具和 shell，如 Command Prompt、PowerShell 和 WSL (Windows Subsystem for Linux)。它于 2019 年首次发布，旨在提供一个集中的位置，用户可以访问多种命令行接口。

以下是 Windows Terminal 的一些主要特性：

1. **多标签界面**：Windows Terminal 允许用户在一个窗口中打开多个标签，每个标签可以运行不同的命令行工具或 shell。
2. **丰富的可定制选项**：用户可以通过修改一个 JSON 文件来定制 Windows Terminal 的许多方面，包括字体、颜色方案、背景图片、透明度等。
3. **GPU 加速文本渲染**：Windows Terminal 使用 GPU 进行文本渲染，提供流畅且高效的用户体验。
4. **Unicode 和 UTF-8 字符支持**：Windows Terminal 支持显示各种 Unicode 字符和表情符号。
5. **支持 PowerShell、命令提示符和 WSL**：Windows Terminal 可以访问 Windows 系统中的各种命令行工具和 shell，包括 PowerShell、命令提示符和 WSL。

### 字体

根据你安装的主题可能需要一个字体，来做适配，可以看你使用的主题的说明

### 其他准备

**安装git**

## zsh

~~~
apt-get update

# 安装
sudo apt install zsh

# 将 zsh 设置为默认 shell
chsh -s /bin/zsh

# 检查
echo $SHELL
# 返回 /usr/bin/zsh 即表示成功；若没成功，重启试试看
~~~

1. **在 Ubuntu 或其他基于 Debian 的 Linux 系统上**：

   首先，打开终端，然后使用 apt-get 命令安装 Zsh：

   ```
   sudo apt-get update
   sudo apt-get install zsh
   ```

   安装完成后，你可以使用 `chsh` 命令来更改默认的 shell：

   ```
   chsh -s $(which zsh)
   ```

   然后，重新登录或重启你的计算机。

2. **在 Fedora 或其他基于 RPM 的 Linux 系统上**：

   打开终端，然后使用 dnf 命令安装 Zsh：

   ```
   sudo dnf install zsh
   ```

   同样，你可以使用 `chsh` 命令来更改默认的 shell：

   ```
   chsh -s $(which zsh)
   ```

   然后，重新登录或重启你的计算机。

3. **在 macOS 上**：

   macOS Catalina（10.15）及更高版本默认使用 Zsh。如果你使用的是早期版本的 macOS，你可能需要手动安装 Zsh。你可以使用 Homebrew 来安装 Zsh：

   ```
   brew install zsh
   ```

   然后，你可以使用 `chsh` 命令来更改默认的 shell：

   ```
   chsh -s $(which zsh)
   ```

   然后，重新登录或重启你的计算机

   ### 配置文件地址

   默认在~/.zshrc

   没有的话可以新建一个

## oh my zsh

`Oh My Zsh` 是一个开源的、社区驱动的框架，用于管理 Zsh 配置。它拥有大量的插件和主题，可以帮助用户定制他们的 Zsh 环境，使得命令行操作更加高效、友好。

以下是如何在已经安装了 Zsh 的系统上安装 "Oh My Zsh"：

1. 首先，确保你的系统上已经安装了 `curl` 或 `wget`。如果没有，你可以使用你的包管理器（如 `apt` 或 `brew`）来安装。

2. 然后，你可以使用 "Oh My Zsh" 的安装脚本来安装。你可以通过 `curl` 或 `wget` 来运行这个脚本：

   使用 `curl`：

   ```bash
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

   或使用 `wget`：

   ```bash
   sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
   ```

   这个脚本将会自动下载并安装 "Oh My Zsh"，并且将你的默认 shell 设置为 Zsh。

3. 安装完成后，你可以通过编辑 `~/.zshrc` 文件来定制你的 Zsh 环境。例如，你可以在这个文件中启用插件或更改主题]

   上面是官方的教程大概是这个意思，但是国内的话安装是有一点问题的

   

   oh_my_zsh 国内安装修改镜像 直连gitee官方源

   #### 安装教程

   ##### Install oh-my-zsh via curl

   ```
   sh -c "$(curl -fsSL https://gitee.com/Devkings/oh_my_zsh_install/raw/master/install.sh)"
   ```

   ##### Install oh-my-zsh via wget

   ```
   sh -c "$(wget https://gitee.com/Devkings/oh_my_zsh_install/raw/master/install.sh 
   ```

## powerlevel10k

官方地址： [romkatv/powerlevel10k: A Zsh theme (github.com)](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#oh-my-zsh)

~~~bash
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
~~~

主题的设置：Set `ZSH_THEME="powerlevel10k/powerlevel10k"` in `~/.zshrc`.

