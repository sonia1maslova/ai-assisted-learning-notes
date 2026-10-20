---
ai_assisted: true
review_status: unverified
last_reviewed:
---

# 操作系统与计算机基础术语：Windows、macOS 与 Linux

> 版本：2026-10-21｜语言：简体中文 + 英文原词｜定位：日常使用、计算机基础、科研计算与软件开发的速查笔记
>
> 阅读说明：**术语中文名并非总有唯一标准翻译**，因此以英文原词为检索主线。表中的“含义”是帮助理解的概括，不等同于某一系统特定版本的严格技术规范。不同系统或版本的功能名称、默认值、操作入口可能变化。

## 目录

1. [先建立整体框架](#1-先建立整体框架)
2. [操作系统类型与家族](#2-操作系统类型与家族)
3. [操作系统的基本结构](#3-操作系统的基本结构)
4. [硬件与计算机架构](#4-硬件与计算机架构)
5. [开机、启动、系统安装与双系统](#5-开机启动系统安装与双系统)
6. [图形界面与桌面操作](#6-图形界面与桌面操作)
7. [文件、路径与文件系统](#7-文件路径与文件系统)
8. [硬盘、分区与存储管理](#8-硬盘分区与存储管理)
9. [进程、线程、任务与 CPU 调度](#9-进程线程任务与-cpu-调度)
10. [内存、缓存与系统性能](#10-内存缓存与系统性能)
11. [用户、权限与安全](#11-用户权限与安全)
12. [软件安装、软件包与环境](#12-软件安装软件包与环境)
13. [终端、Shell 与命令行](#13-终端shell-与命令行)
14. [网络、远程访问与文件共享](#14-网络远程访问与文件共享)
15. [虚拟机、容器与跨系统使用](#15-虚拟机容器与跨系统使用)
16. [科研计算、开发与服务器常见术语](#16-科研计算开发与服务器常见术语)
17. [系统维护、更新、故障排除与备份](#17-系统维护更新故障排除与备份)
18. [Windows、macOS、Linux 对照表](#18-windowsmacoslinux-对照表)
19. [容易混淆的概念：逐组辨析](#19-容易混淆的概念逐组辨析)
20. [最实用的命令与路径速查](#20-最实用的命令与路径速查)
21. [推荐学习路线与官方资料](#21-推荐学习路线与官方资料)

---

## 1. 先建立整体框架

理解操作系统，最好先区分 **硬件—固件—操作系统内核—系统服务—应用程序—用户界面** 六个层次：

```text
人（用户）
  │ 图形界面 GUI / 命令行 CLI
应用程序（浏览器、Office、Python、MATLAB 等）
  │ 系统调用 / 系统提供的 API
系统服务与运行库（网络、登录、文件共享、图形服务等）
  │
操作系统内核 Kernel（进程调度、内存管理、设备驱动、文件系统等）
  │
固件 Firmware（UEFI / 传统 BIOS 等）
  │
硬件 Hardware（CPU、RAM、SSD、GPU、网卡等）
```

这是一张**便于学习的简化图**，并不代表全部服务都位于内核之上，也不代表所有驱动都在内核中。固件主要在启动及特定硬件管理阶段发挥作用，并非每次应用系统调用都要经过固件。

**一个直观的例子**：在 Windows 上双击 Python 脚本的快捷方式，图形界面响应操作，系统按文件关联启动某个 Python 解释器，内核为它提供进程和内存资源，解释器再读取脚本及相关文件。你看到的是一个动作，底层则涉及多个层次。

---

## 2. 操作系统类型与家族

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 操作系统 | Operating System（OS） | 管理计算机硬件资源并为应用提供运行环境的软件系统。 |
| 桌面操作系统 | Desktop OS | 面向个人电脑和交互式桌面应用的系统，如 Windows、macOS、Ubuntu Desktop。 |
| 服务器操作系统 | Server OS | 面向长期运行的网络服务、多用户管理和远程管理的系统，如 Windows Server、Ubuntu Server。 |
| 移动操作系统 | Mobile OS | 面向手机、平板等移动终端的系统，如 Android、iOS。 |
| 嵌入式操作系统 | Embedded OS | 用于专用设备或资源受限设备，如仪器、路由器、工控设备。 |
| 实时操作系统 | Real-Time Operating System（RTOS） | 侧重任务响应时间的可预测性；“实时”不简单等于“速度快”。 |
| Windows | Microsoft Windows | 微软的操作系统家族，个人电脑主要使用 Windows 10/11 等版本。 |
| Windows Server | Windows Server | 微软面向服务器的操作系统产品家族。 |
| macOS | macOS | 苹果 Mac 电脑使用的桌面操作系统；基于 Darwin，拥有 Unix 技术基础。 |
| Mac OS X / OS X | Mac OS X / OS X | macOS 在历史上的产品名称，不是与 macOS 完全独立的新系统家族。 |
| Linux 内核 | Linux kernel | Linux 严格意义上是内核；日常“Linux 系统”通常是由内核和大量工具软件组成的发行版。 |
| GNU/Linux | GNU/Linux | 强调 GNU 用户空间工具与 Linux 内核共同构成系统的一种称呼；不同发行版组件并不完全相同。 |
| Linux 发行版 | Linux distribution（distro） | 把 Linux 内核、软件包管理器、系统工具等集成并维护成可安装的系统。 |
| Ubuntu | Ubuntu | 广泛使用的 Linux 发行版，基于 Debian。 |
| Debian | Debian | 注重社区维护与软件包管理的 Linux 发行版；许多其他发行版以其为基础。 |
| Fedora | Fedora | 由社区支持、与 Red Hat 生态相关的 Linux 发行版。 |
| Red Hat Enterprise Linux | RHEL | 面向企业的商业 Linux 发行版。 |
| Arch Linux | Arch Linux | 以滚动更新、较高可配置性为特点的发行版。 |
| Unix | UNIX / Unix | 一类历史悠久的操作系统传统；大写 UNIX 还可作为经认证的商标名称。 |
| 类 Unix 系统 | Unix-like OS | 在接口、工具和设计思想上类似 Unix 的系统，Linux 和 macOS 都常被这样归类。 |
| BSD | Berkeley Software Distribution（BSD） | 源于 Berkeley Unix 的系统及代码传统，FreeBSD、OpenBSD 等是相关系统。 |
| Darwin | Darwin | 支撑 macOS 等苹果系统的开源基础层，包含 XNU 内核和部分系统组件。 |
| XNU | X is Not Unix（XNU） | Apple 的内核名称，采用 Mach、BSD 等技术。 |
| Android | Android | 以 Linux 内核为基础的移动平台，用户空间、应用生态与常见桌面 Linux 发行版不同。 |
| ChromeOS | ChromeOS | Google 的操作系统，重点面向 Chromebook 及 Web 应用场景。 |
| 开源软件 | Open-source software | 源代码依相应许可证公开，允许规定范围内的使用、研究、修改和分发；不等同于“没有版权”。 |
| 专有软件 | Proprietary software | 使用、修改和传播通常受到软件所有者许可证限制。 |
| 长期支持版本 | Long-Term Support（LTS） | 提供较长周期维护支持的发布类型；具体年限依厂商或发行版而定。 |
| 滚动更新 | Rolling release | 不以很长间隔的完整大版本升级为主，而持续发布软件和系统更新。 |

**提示**：*Linux ≠ Ubuntu*，正如“操作系统”不等于“Windows”。Linux 是内核，Ubuntu 是包含内核与其他软件的完整发行版。

## 3. 操作系统的基本结构

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 内核 | Kernel | 操作系统核心部分，负责资源协调、进程、内存和硬件交互等。 |
| 用户空间 | User space | 普通应用和部分系统服务运行的隔离环境。 |
| 内核空间 | Kernel space | 内核代码和内核数据所在的特权执行环境；具体地址空间安排依操作系统。 |
| 用户态 | User mode | 处理器运行较低特权代码的一种状态，不能直接执行所有特权操作。 |
| 内核态 | Kernel mode | 处理器运行高特权内核代码的状态；内核缺陷影响范围往往更大。 |
| 系统调用 | System call（syscall） | 应用请求内核完成操作的接口，如打开文件、创建进程。 |
| 应用程序编程接口 | Application Programming Interface（API） | 程序间约定的功能接口，范围比“系统调用”更广。 |
| 应用二进制接口 | Application Binary Interface（ABI） | 约定已编译程序如何与操作系统和其他二进制组件交互。 |
| 驱动程序 | Device driver | 使操作系统能够控制和访问显卡、网卡、打印机等硬件的软件。 |
| 系统服务 | System service | 在后台执行某类系统功能，如网络、日志、打印、更新。 |
| 守护进程 | Daemon | Unix/Linux 中长期运行的后台进程，常用于提供网络和系统服务。 |
| 初始化进程 | Init process / init system | 系统启动时负责初始化并启动其他服务的核心用户空间组件，如 systemd。 |
| systemd | systemd | 许多 Linux 发行版使用的系统与服务管理组件，不是所有 Linux 系统都使用它。 |
| launchd | launchd | macOS 用于启动、调度与管理多类后台作业的系统组件。 |
| 服务控制管理器 | Service Control Manager（SCM） | Windows 管理服务启动、停止及服务配置的系统组件。 |
| 注册表 | Windows Registry | Windows 的分层配置数据库，存放系统及许多应用的设置信息。 |
| 环境变量 | Environment variable | 向程序提供运行环境信息的键值，如 `PATH`、`HOME`。 |
| 内核模块 | Kernel module | 可按系统机制加载的内核功能组件，在 Linux 中常以模块形式提供驱动。 |
| 单体内核 | Monolithic kernel | 大量核心服务运行于内核空间的设计；Linux 通常归于这一类别。 |
| 微内核 | Microkernel | 尽量把部分服务移到用户空间、保留较小内核核心的设计思路。 |
| 混合内核 | Hybrid kernel | 吸收不同内核设计特征的统称，Windows NT、XNU 常被描述为此类。 |
| Windows NT | Windows NT architecture | 现代 Windows 系列所依托的内核与系统架构；不是当前消费者必须安装的独立产品。 |
| 权限边界 | Privilege boundary | 限制不同权限级别代码访问资源的边界，是系统安全的基本概念。 |

参考：[Microsoft：用户态和内核态](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)、[Microsoft：注册表结构](https://learn.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry/)。

## 4. 硬件与计算机架构

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 中央处理器 | Central Processing Unit（CPU） | 负责执行程序指令的主要处理器。 |
| 图形处理器 | Graphics Processing Unit（GPU） | 擅长图形计算和大规模并行计算，常用于 AI、科学计算。 |
| 处理器架构 | Instruction Set Architecture（ISA） | 处理器对外提供的指令与执行规则，如 x86-64、ARM64。 |
| x86 | x86 | 源于 Intel 8086 的处理器架构家族，常用来泛指 PC 体系架构。 |
| x64 / x86-64 | x86-64 / AMD64 | 广泛使用的 64 位 x86 指令集架构。 |
| ARM64 | AArch64 / ARM64 | ARM 的 64 位指令集架构，Apple silicon 和许多移动芯片使用。 |
| Apple 芯片 | Apple silicon | Apple 自研的 ARM 架构 Mac 处理器系列，与旧 Intel Mac 架构不同。 |
| Intel Mac | Intel-based Mac | 使用 Intel x86-64 处理器的 Mac。 |
| 位数 | 32-bit / 64-bit | 常见用于描述处理器、操作系统及程序的位宽，影响指针、寻址能力等。 |
| 指令集兼容性 | ISA compatibility | 某个已编译程序能否在目标处理器架构上直接执行。 |
| 模拟 | Emulation | 模拟另一种硬件或软件平台的行为，通常有额外开销。 |
| 二进制翻译 | Binary translation | 把一种指令格式转换为另一种可执行指令，Rosetta 2 属于相关技术。 |
| 处理器核心 | CPU core | CPU 内能够执行指令流的处理单元。 |
| 逻辑处理器 | Logical processor | 操作系统可调度的处理器执行单元，可能来自 SMT/超线程。 |
| 超线程 | Hyper-Threading / SMT | 让一个物理核心暴露多个逻辑处理器的技术；Hyper-Threading 是 Intel 的品牌名称。 |
| 随机存取存储器 | Random Access Memory（RAM） | 程序运行时主要使用的易失性内存，关机后通常不保留其中内容。 |
| 只读存储器 | Read-Only Memory（ROM） | 泛指某些主要用于存储固件等内容的非易失性存储技术；现代固件常在 Flash 中。 |
| 固态硬盘 | Solid-State Drive（SSD） | 使用闪存等固态器件保存数据的存储设备。 |
| 机械硬盘 | Hard Disk Drive（HDD） | 以旋转磁盘保存数据的存储设备。 |
| NVMe | Non-Volatile Memory Express（NVMe） | 面向非易失性存储、通常运行于 PCIe 上的通信协议；不等于 SSD 本身。 |
| SATA | Serial ATA | 一种常见存储设备连接接口/协议。 |
| PCIe | Peripheral Component Interconnect Express | 高速内部扩展互连总线，显卡及部分 SSD 常使用。 |
| 驱动兼容性 | Driver compatibility | 硬件是否有适配当前操作系统和架构的驱动支持。 |
| 外设 | Peripheral device | 键盘、鼠标、外接硬盘、打印机等外围设备。 |

## 5. 开机、启动、系统安装与双系统

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 开机 / 启动 | Boot / Booting | 从硬件初始化到操作系统可用的一系列过程。 |
| 冷启动 | Cold boot | 从关机状态上电启动。 |
| 热启动 / 重新启动 | Warm boot / Restart / Reboot | 在系统运行后重新开始启动过程。 |
| 固件 | Firmware | 存储在硬件设备上的底层控制程序，如主板固件。 |
| BIOS | Basic Input/Output System | 传统 PC 固件接口；日常口语有时也泛指 UEFI 设置界面。 |
| UEFI | Unified Extensible Firmware Interface | 现代系统固件接口规范，广泛替代传统 BIOS 启动方式。 |
| 启动顺序 | Boot order | 决定从哪个设备或启动项优先加载系统。 |
| 启动项 | Boot entry | 固件或启动管理器中可选的启动目标。 |
| 引导加载程序 | Bootloader / Boot loader | 加载操作系统内核或后续启动阶段的程序。 |
| 启动管理器 | Boot manager | 选择或管理要启动哪个系统的组件，如 Windows Boot Manager、GRUB。 |
| GRUB | GNU GRand Unified Bootloader | 多见于 Linux 的启动管理器，可支持多系统菜单。 |
| EFI 系统分区 | EFI System Partition（ESP） | UEFI 启动时存放引导程序等文件的专用分区。 |
| 安全启动 | Secure Boot | UEFI 体系下验证启动软件可信性的机制；与用户登录密码无关。 |
| 可信平台模块 | Trusted Platform Module（TPM） | 提供密钥保护、平台度量等功能的安全硬件或固件实现。 |
| 系统镜像 | OS image / System image | 操作系统安装或部署用的磁盘映像；某些语境指完整备份。 |
| ISO 镜像 | ISO image | 常见的光盘映像文件格式，系统安装介质常以 `.iso` 提供。 |
| 可启动 U 盘 | Bootable USB drive | 制作了可用引导结构和安装/维护内容的 USB 设备。 |
| 纯净安装 | Clean installation | 重新部署操作系统，通常不保留旧系统环境；应先备份。 |
| 就地升级 | In-place upgrade | 在已有系统环境中升级操作系统，是否保留应用及设置取决于具体流程。 |
| 双系统 | Dual boot | 同一电脑安装两个可分别启动的操作系统，通常开机时选择其中一个。 |
| 多重启动 | Multiboot | 一台电脑可从多个操作系统/环境中选择启动。 |
| 预装系统 | Preinstalled OS | 厂商出厂时已在设备中安装的操作系统。 |
| OEM | Original Equipment Manufacturer | 原始设备制造商；在系统授权中常指随设备提供的 OEM 许可证。 |
| 驱动安装 | Driver installation | 安装或更新操作系统所需的硬件驱动。 |
| 系统恢复环境 | Recovery environment | 独立于正常桌面、用于修复或重装系统的特殊运行环境。 |
| WinRE | Windows Recovery Environment | Windows 提供的恢复环境，可进行启动修复、重置等操作。 |
| macOS 恢复 | macOS Recovery | Mac 的系统恢复工具环境，可执行磁盘工具、重装系统等操作。 |
| Live USB | Live USB | 直接从 USB 启动的临时操作系统环境，可用于体验或维护 Linux。 |
| 安全模式 | Safe Mode | 用较精简的启动配置排除驱动和服务问题；各平台实现不同。 |

**双系统不等于同时运行两个系统**：典型双系统需要重启切换；若希望 Windows 中同时运行 Linux，应了解 WSL 2 或虚拟机（见第 15 节）。参考：[Microsoft：Secure Boot](https://learn.microsoft.com/en-us/windows-hardware/drivers/bringup/secure-boot)、[Microsoft：WinRE](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference?view=windows-11)。

## 6. 图形界面与桌面操作

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 图形用户界面 | Graphical User Interface（GUI） | 用窗口、图标、菜单、鼠标等交互的界面。 |
| 命令行界面 | Command-Line Interface（CLI） | 输入文本命令来操作系统或应用的交互方式。 |
| 桌面环境 | Desktop environment（DE） | 桌面、面板、窗口、文件管理器等组件的集合；Linux 可选 GNOME/KDE 等。 |
| 窗口管理器 | Window manager（WM） | 管理窗口位置、尺寸、焦点及装饰的组件。 |
| 显示服务器 | Display server | 处理图形输出和输入事件的相关服务层，如 X.Org；Wayland 使用不同架构的协议和合成器。 |
| X11 / X Window System | X11 / X Window System | Unix/Linux 常见的历史悠久的图形窗口系统协议。 |
| Wayland | Wayland | 现代 Linux 图形显示协议及生态，不是一个完整桌面环境。 |
| 合成器 | Compositor | 组合各窗口绘制结果并输出最终桌面画面的组件。 |
| 文件资源管理器 | File Explorer | Windows 查看文件、文件夹和磁盘的图形工具。 |
| 访达 | Finder | macOS 文件管理器。 |
| Windows 桌面 | Desktop | Windows 的主要图形工作区域，也对应用户的桌面文件夹。 |
| 任务栏 | Taskbar | Windows 显示打开/固定应用及系统状态的条带。 |
| 开始菜单 | Start menu | Windows 用来启动应用、查找设置等的入口。 |
| 系统托盘 / 通知区域 | System tray / Notification area | Windows 任务栏显示后台应用和系统状态图标的区域。 |
| Dock 程序坞 | Dock | macOS 快速启动/切换应用及访问常用位置的界面元素。 |
| 菜单栏 | Menu bar | macOS 屏幕顶端显示应用菜单与部分系统状态的区域。 |
| Spotlight 聚焦搜索 | Spotlight | macOS 的系统级搜索功能，可检索应用、文件和设置等。 |
| Mission Control 调度中心 | Mission Control | macOS 总览当前打开窗口和桌面空间的界面。 |
| Stage Manager 台前调度 | Stage Manager | macOS 用于组织窗口与工作空间的功能。 |
| 虚拟桌面 | Virtual desktop / Workspace | 在同一操作系统会话中建立多个桌面工作区，并非安装多个系统。 |
| 活动监视器 | Activity Monitor | macOS 查看 CPU、内存、能耗及进程的工具。 |
| 任务管理器 | Task Manager | Windows 查看任务、性能、启动应用及部分系统信息的工具。 |
| 系统设置 | System Settings | macOS 统一配置系统功能的主要入口。 |
| 设置 | Settings | Windows 现代设置应用；部分传统功能仍在控制面板或其他工具。 |
| 控制面板 | Control Panel | Windows 较传统的系统设置界面。 |
| 设备管理器 | Device Manager | Windows 查看硬件及驱动状态、调整相关配置的工具。 |

参考：[Apple：Finder](https://support.apple.com/guide/mac-help/organize-your-files-in-the-finder-mchle9f0a1b2/mac)、[Apple：Desktop & Dock](https://support.apple.com/en-ke/guide/mac-help/mchlp1119/mac)。

## 7. 文件、路径与文件系统

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 文件 | File | 有名称、内容及元数据的数据对象。 |
| 文件夹 / 目录 | Folder / Directory | 用于分层组织文件和子目录的结构。 |
| 路径 | Path | 指向文件或目录位置的字符串，如 `C:\Users\Alice` 或 `/home/alice`。 |
| 绝对路径 | Absolute path | 从文件系统根目录或某个明确根位置描述的完整路径。 |
| 相对路径 | Relative path | 相对于当前工作目录或指定基准的路径，如 `./data/file.csv`。 |
| 根目录 | Root directory | 文件系统层级的起点；Unix 系常写作 `/`，Windows 卷可见如 `C:\`。 |
| 主目录 / 用户目录 | Home directory | 当前用户的个人目录；macOS 多为 `/Users/姓名`，Linux 多为 `/home/姓名`。 |
| 当前工作目录 | Current working directory（CWD） | 程序在解析相对路径时所使用的基准目录。 |
| 父目录 | Parent directory | 当前目录的上一级，常记为 `..`。 |
| 文件扩展名 | File extension | 文件名末尾的后缀，如 `.txt`、`.pdf`、`.exe`；不总能准确反映实际格式。 |
| 隐藏文件 | Hidden file | 文件管理器通常不默认展示的文件；Unix 系常用以 `.` 开头的文件名。 |
| 元数据 | Metadata | 文件的大小、时间戳、权限、所有者等附加信息。 |
| 文件系统 | File system | 组织、保存和访问磁盘上文件的数据结构与规则，如 NTFS、APFS、ext4。 |
| NTFS | New Technology File System | 现代 Windows 系统盘常用文件系统，支持权限、日志等功能。 |
| FAT32 | File Allocation Table 32 | 兼容性广的较旧文件系统；单个文件通常不能达到 4 GiB。 |
| exFAT | Extended File Allocation Table | 面向闪存/跨平台存储常见的文件系统，支持大文件。 |
| APFS | Apple File System | 现代 macOS 使用的默认文件系统，支持快照、克隆等功能。 |
| HFS+ | Hierarchical File System Plus | 旧式 macOS 常用文件系统，也叫 Mac OS Extended。 |
| ext4 | Fourth Extended Filesystem | Linux 常用的日志型文件系统。 |
| XFS | XFS | Linux 等平台可用的高性能日志型文件系统。 |
| Btrfs | B-tree File System | 支持写时复制、快照和校验等功能的 Linux 文件系统。 |
| 符号链接 | Symbolic link（symlink） | 保存目标路径的链接对象，可以指向文件或目录。 |
| 硬链接 | Hard link | 让多个文件名指向同一文件对象（同一文件系统内）；与符号链接不同。 |
| Windows 快捷方式 | Shortcut（`.lnk`） | Windows Shell 级的快捷入口；不等于文件系统符号链接。 |
| 挂载 | Mount | 将文件系统接入可访问目录树的过程。 |
| 挂载点 | Mount point | 文件系统被接入时对应的目录位置，如 `/mnt/data`。 |
| 盘符 | Drive letter | Windows 常见的卷标识形式，如 `C:`、`D:`，不一定代表不同物理硬盘。 |
| UNC 路径 | Universal Naming Convention（UNC） | Windows 常见的网络资源路径，如 `\\server\share`。 |
| 网络共享 | Network share | 通过网络暴露的文件夹或存储位置。 |
| 大小写敏感 | Case sensitivity | 区分 `data.txt` 和 `Data.txt`；依文件系统配置而变，不只取决于 OS 名称。 |
| 文件权限 | File permissions | 控制谁可以查看、修改或执行文件及进入目录。 |
| 日志型文件系统 | Journaling file system | 通过记录元数据等变更帮助故障恢复的文件系统；不等于文件自动备份。 |
| 写时复制 | Copy-on-Write（CoW） | 修改时先保留旧数据、写入新数据块的机制，常用于快照等。 |

**路径的三个例子**：

```text
Windows: C:\Users\Alice\Documents\report.docx
macOS:   /Users/alice/Documents/report.docx
Linux:   /home/alice/Documents/report.docx
```

三种系统路径格式的差异很重要；但 macOS 与 Linux 的目录习惯也不完全相同。参考：[Microsoft：NTFS](https://learn.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview)、[Apple：APFS 与磁盘工具](https://support.apple.com/guide/disk-utility/welcome/mac)。

## 8. 硬盘、分区与存储管理

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 物理磁盘 | Physical disk | 实际 SSD/HDD 设备，一块物理磁盘可以有多个分区。 |
| 分区 | Partition | 把磁盘地址空间划分为逻辑区域的结构。 |
| 卷 | Volume | 由操作系统管理并供文件系统使用的存储逻辑单元；可能跨分区或磁盘。 |
| 格式化 | Format | 初始化某个卷上的文件系统结构；执行前应明确数据保留风险。 |
| 分区表 | Partition table | 记录磁盘分区布局的元数据。 |
| GPT 分区表 | GUID Partition Table（GPT） | 现代分区表格式，常与 UEFI 启动配合使用。 |
| MBR | Master Boot Record（MBR） | 传统磁盘启动记录及分区结构；也可专指首扇区记录。 |
| 磁盘管理 | Disk Management | Windows 内置的磁盘、分区、卷管理工具。 |
| 磁盘工具 | Disk Utility | macOS 用于查看、抹掉、分区、修复磁盘的图形工具。 |
| 逻辑卷管理 | Logical Volume Management（LVM） | Linux 常见的灵活管理物理卷、卷组与逻辑卷的方法。 |
| RAID | Redundant Array of Independent Disks | 组合多个磁盘获得冗余或性能等特性；RAID 不等于备份。 |
| NAS | Network-Attached Storage | 通过网络提供文件存储访问的设备或服务。 |
| SAN | Storage Area Network | 面向块存储的专用存储网络架构。 |
| 读写速度 | Read/write throughput | 单位时间内传输的数据量，常用 MB/s 表示。 |
| IOPS | Input/Output Operations Per Second | 每秒完成的存储 I/O 操作数。 |
| 延迟 | Latency | 一次操作等待完成的时间，磁盘读取和网络访问都有延迟。 |
| 块设备 | Block device | 按可寻址数据块访问的设备，如磁盘。 |
| 文件句柄 | File handle | 进程访问已打开文件时使用的操作系统标识/引用。 |
| 文件描述符 | File descriptor（FD） | Unix/Linux 中表示打开文件及其他 I/O 对象的整数编号。 |
| 磁盘配额 | Disk quota | 限制用户或应用可以使用的存储容量。 |
| TRIM | TRIM | 操作系统向 SSD 通知哪些逻辑块已不再使用的机制。 |
| 磁盘碎片整理 | Defragmentation | 调整文件在存储介质上的布局以降低碎片影响；对 SSD 不应简单照搬机械硬盘做法。 |
| 稀疏文件 | Sparse file | 未实际写入的数据区域不必占用对应大小的物理空间。 |
| 快照 | Snapshot | 记录文件系统/卷某一时间点状态的机制；不是天然独立的异地备份。 |

---
## 9. 进程、线程、任务与 CPU 调度

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 程序 | Program | 存储在磁盘上的指令和数据；尚不意味着正在运行。 |
| 进程 | Process | 一个正在执行的程序实例，具有自己的资源、地址空间及运行状态等。 |
| 进程标识符 | Process ID（PID） | 操作系统用来标识进程的编号。 |
| 线程 | Thread | 进程内部可被调度的执行流；一个进程可以有多个线程。 |
| 多线程 | Multithreading | 在一个进程中使用多个线程执行任务。 |
| 多进程 | Multiprocessing | 利用多个进程执行工作；与多个 CPU 核心不是同一概念。 |
| 并发 | Concurrency | 多个任务在一段时间内交错推进，不要求同一瞬间真正在不同核心上执行。 |
| 并行 | Parallelism | 多个任务在同一时间真正执行，例如分布于多个 CPU 核心。 |
| 多任务 | Multitasking | 操作系统允许多个任务交替或并行执行的能力。 |
| 上下文切换 | Context switch | CPU 从一个执行上下文切换到另一个执行上下文的过程。 |
| 调度器 | Scheduler | 决定哪些任务或线程何时获得 CPU 的系统组件。 |
| 时间片 | Time slice | 任务在某些调度策略下获得的一段 CPU 运行时间。 |
| 优先级 | Priority | 影响操作系统调度顺序或资源分配的参数。 |
| 前台进程 | Foreground process | 与当前交互或作业控制前台相关的进程；GUI 与 Shell 语境稍有不同。 |
| 后台进程 | Background process | 无需始终占据交互界面也能运行的进程。 |
| 子进程 | Child process | 由其他进程创建的进程。 |
| 父进程 | Parent process | 创建另一个进程的进程。 |
| 进程间通信 | Inter-Process Communication（IPC） | 不同进程交换数据或同步的方式，如管道、共享内存、Socket。 |
| 标准输入 | Standard input（stdin） | 进程默认输入流，Unix 中对应文件描述符 0。 |
| 标准输出 | Standard output（stdout） | 进程默认正常输出流，Unix 中通常对应文件描述符 1。 |
| 标准错误 | Standard error（stderr） | 进程默认错误/诊断输出流，Unix 中通常对应文件描述符 2。 |
| 退出码 | Exit code / Exit status | 程序结束时提供的状态值；Unix 传统上 0 常表示成功，但具体约定依程序。 |
| 终止进程 | Terminate / Kill process | 要求或强制结束一个进程，可能导致未保存的数据丢失。 |
| 信号 | Signal | Unix/Linux 向进程通知事件或请求动作的机制，如 `SIGTERM`、`SIGKILL`。 |
| 僵尸进程 | Zombie process | Unix 中已经结束但退出状态还未被父进程回收的进程。 |
| 孤儿进程 | Orphan process | 父进程已结束、但自身仍存在的进程，之后会被系统接管。 |
| 进程树 | Process tree | 按父子关系组织的进程层级。 |
| CPU 使用率 | CPU usage / Utilization | 衡量处理器活动的指标；多核心系统中不同工具的百分比口径可能不同。 |
| 负载平均值 | Load average | Unix/Linux 中反映可运行任务和部分不可中断等待任务负载的指标，不等于 CPU 百分比。 |

**核心区分**：程序是“可供执行的代码”，进程是“运行中的实例”，线程是“进程内部的执行流”。

## 10. 内存、缓存与系统性能

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 内存 | Memory / RAM | 程序执行时使用的高速主存，常说的“16GB 内存”一般指 RAM 容量。 |
| 虚拟内存 | Virtual memory | 让进程使用虚拟地址空间，并由操作系统/硬件映射到物理内存等资源的机制。 |
| 虚拟地址 | Virtual address | 程序使用的地址，由系统与处理器翻译成实际映射位置。 |
| 物理地址 | Physical address | 与物理内存寻址体系关联的地址。 |
| 页 | Memory page | 虚拟内存管理中常用的固定大小单位。 |
| 页表 | Page table | 用于虚拟地址与物理地址映射的数据结构。 |
| 内存管理单元 | Memory Management Unit（MMU） | 处理器中用于地址转换和相关访问控制的硬件。 |
| 换页 | Paging | 以页面为单位管理虚拟内存和物理内存的机制。 |
| 交换空间 | Swap space | Linux 等系统把部分内存页换出到磁盘时使用的空间或文件。 |
| 页面文件 | Pagefile / `pagefile.sys` | Windows 虚拟内存管理中可能用于分页等用途的磁盘文件。 |
| 交换文件 | Swapfile | 作为交换空间的文件；macOS、Linux 等平台有相应实现。 |
| 内存压力 | Memory pressure | 表示系统内存资源是否紧张、是否需要回收或压缩内存的指标。 |
| 内存压缩 | Memory compression | 将部分较少使用的内存数据压缩保存，以减少物理内存占用。 |
| 缓存 | Cache | 保存近期或经常访问的数据，加快后续操作；存在 CPU 缓存、文件缓存等不同层级。 |
| CPU 缓存 | CPU cache（L1/L2/L3） | 处理器附近的高速小容量存储，用于降低访问数据的成本。 |
| 页缓存 | Page cache | 操作系统用空闲 RAM 缓存文件数据，以减少重复磁盘访问。 |
| 缓冲区 | Buffer | 用于暂时存储传输或处理中的数据的区域；不完全等同于缓存。 |
| 内存泄漏 | Memory leak | 程序不再需要某些已占用内存，却持续未释放/无法回收，可能导致占用增长。 |
| 内存溢出 | Out of Memory（OOM） | 申请内存不能满足时的异常情形；Linux 可能由 OOM Killer 终止进程。 |
| 内存分配 | Memory allocation | 为程序或对象提供可使用内存的过程。 |
| 堆 | Heap | 程序常用于动态分配对象的内存区域/数据结构，具体由语言运行时管理。 |
| 栈 | Stack | 用于函数调用记录、局部状态等的后进先出结构；程序中的调用栈是典型实例。 |
| 硬缺页 | Hard page fault | 所需页面不在物理内存，需要从磁盘等后备存储读取；不表示硬件损坏。 |
| 内存映射文件 | Memory-mapped file | 使文件内容通过进程虚拟地址空间访问的机制。 |
| 吞吐量 | Throughput | 单位时间完成的工作量。 |
| 瓶颈 | Bottleneck | 限制整体速度的关键资源或环节，如 CPU、磁盘 I/O、网络。 |
| 基准测试 | Benchmark | 使用可重复工作负载比较系统或软硬件性能的测量方法。 |

**特别注意**：虚拟内存并不等于“硬盘划出来的内存”。它首先是一种**地址空间抽象与管理机制**，交换文件/交换分区只是其中可能使用的后备存储手段。

## 11. 用户、权限与安全

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 用户账户 | User account | 识别用户身份并关联设置、文件和权限的账户。 |
| 用户名 | Username | 操作系统用于识别账户的名称，不一定等于显示昵称。 |
| 本地账户 | Local account | 主要在当前设备本地管理的账户。 |
| Microsoft 账户 | Microsoft account | 用于微软在线服务及部分 Windows 登录场景的账户。 |
| Apple 账户 | Apple Account | 苹果在线服务身份；旧资料常称 Apple ID。 |
| 管理员 | Administrator / Admin | 拥有执行系统管理操作权限的账户或角色。 |
| 标准用户 | Standard user | 默认不拥有所有系统管理权限的普通账户。 |
| root 用户 | root / Superuser | Unix/Linux 中具有极高管理权限的账户名称。 |
| sudo | Substitute User Do / `sudo` | Unix/Linux/macOS 常用工具，可按策略以其他身份（通常是 root）运行命令。 |
| UAC | User Account Control | Windows 用户账户控制，运行特权操作时进行权限提升提示等。 |
| UID / GID | User ID / Group ID | Unix/Linux 用户及用户组的数字标识。 |
| 用户组 | User group | 便于批量分配权限和管理账户的集合。 |
| 访问控制列表 | Access Control List（ACL） | 对特定用户/组或主体定义资源访问权限的规则集合。 |
| 读取权限 | Read permission | 允许读取对象；对目录的具体含义依文件系统规则。 |
| 写入权限 | Write permission | 允许修改对象或在有适当目录权限时创建/删除目录项。 |
| 执行权限 | Execute permission | 允许执行程序；在 Unix 目录上常意味着允许穿越/进入目录。 |
| 身份验证 | Authentication | 确认“你是谁”，如密码、指纹、硬件密钥。 |
| 授权 | Authorization | 身份得到确认后，决定“你能做什么”。 |
| 最小权限原则 | Principle of Least Privilege | 仅授予完成任务所需的权限，降低误操作和攻击风险。 |
| 权限提升 | Privilege escalation / Elevation | 从较低权限变为更高权限；可能是合法管理员操作，也可能是漏洞攻击。 |
| 沙盒 | Sandbox | 隔离程序可访问的资源，以限制潜在影响范围的机制。 |
| 防火墙 | Firewall | 根据规则允许或拦截网络通信的软件或设备。 |
| 反恶意软件 | Anti-malware | 检测、阻止或处理恶意软件的工具或系统机制。 |
| Defender | Microsoft Defender Antivirus | Windows 中的微软反病毒保护组件；与其他同名企业安全产品需区分。 |
| Gatekeeper | Gatekeeper | macOS 对下载软件的来源、签名和公证状态等进行检查的安全机制。 |
| SIP | System Integrity Protection | macOS 系统完整性保护，限制对关键系统部分的修改。 |
| FileVault | FileVault | macOS 的磁盘/卷数据加密功能。 |
| BitLocker | BitLocker Drive Encryption | Windows 提供的卷加密技术，部分功能/管理方式取决于系统版本。 |
| 全盘加密 | Full-disk encryption（FDE） | 对设备磁盘数据进行加密的统称；实际产品常以卷为加密单位。 |
| 安全隔区 | Secure Enclave | Apple 部分设备中的硬件隔离安全子系统，用于保护敏感密钥等。 |
| 哈希 | Cryptographic hash | 把数据计算为固定长度摘要的密码学技术；哈希不是可直接“解密”的加密。 |
| 数字签名 | Digital signature | 用私钥签名、借助公钥验证来源及完整性的一种技术。 |
| 证书 | Digital certificate | 用签名绑定公钥与身份等信息的电子凭据。 |
| 多因素认证 | Multi-Factor Authentication（MFA） | 使用不同类别的身份因素进行认证。 |
| VPN | Virtual Private Network | 利用隧道等技术建立受保护的网络连接；不等同于绝对匿名。 |
| 安全补丁 | Security patch | 修复已知安全漏洞的更新。 |
| CVE | Common Vulnerabilities and Exposures | 公开漏洞编号体系，用于统一标识已知安全问题。 |

**关键区别**：管理员/root 是权限身份，`sudo` 是按策略执行特权命令的工具，UAC 是 Windows 的权限控制提示机制。**不要因为碰到“权限不足”，就直接关闭安全保护。**

参考：[Microsoft：UAC](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works)、[Microsoft：TPM 与 BitLocker](https://learn.microsoft.com/en-us/windows/security/hardware-security/tpm/how-windows-uses-the-tpm)、[Apple：Gatekeeper](https://support.apple.com/guide/security/gatekeeper-and-runtime-protection-sec5599b66df/web)、[Apple：SIP](https://developer.apple.com/documentation/security/disabling-and-enabling-system-integrity-protection)。

## 12. 软件安装、软件包与环境

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 应用程序 | Application / App | 面向具体任务的软件，如浏览器、MATLAB、文本编辑器。 |
| 可执行文件 | Executable | 操作系统可加载执行的程序文件；不同系统使用不同格式。 |
| EXE | `.exe` executable | Windows 常见的可执行程序文件格式/扩展名。 |
| MSI | Microsoft Installer package（`.msi`） | Windows Installer 使用的常见软件安装包格式。 |
| macOS App 包 | Application bundle（`.app`） | macOS 以目录包形式组织应用程序及资源的常见形式。 |
| DMG | Disk image（`.dmg`） | macOS 常见磁盘映像格式，常用于分发应用安装内容。 |
| PKG | Installer package（`.pkg`） | macOS 常见的软件安装程序包。 |
| DEB | Debian package（`.deb`） | Debian/Ubuntu 生态常见的软件包文件格式。 |
| RPM | RPM Package Manager（`.rpm`） | Fedora/RHEL 等生态使用的软件包格式及管理体系。 |
| 包管理器 | Package manager | 安装、升级、卸载软件并管理其依赖的工具。 |
| APT | Advanced Package Tool（`apt`） | Debian/Ubuntu 常用包管理工具。 |
| DNF | Dandified YUM（`dnf`） | Fedora/RHEL 家族常见包管理工具。 |
| Homebrew | Homebrew（`brew`） | macOS 常用第三方包管理器，也支持部分 Linux 环境。 |
| WinGet | Windows Package Manager（`winget`） | Windows 的命令行应用包管理工具。 |
| App Store | App Store | 苹果的软件分发平台，Mac 有对应的应用商店。 |
| Microsoft Store | Microsoft Store | Windows 的应用与内容分发平台。 |
| 软件源 | Software repository | 提供软件包及元数据的仓库或服务器。 |
| 软件依赖 | Dependency | 软件运行或安装时必须使用的其他组件、库或版本。 |
| 依赖冲突 | Dependency conflict | 多个软件要求不兼容的依赖版本或配置。 |
| 动态链接库 | Dynamic-link library（DLL） | Windows 常见可由程序在运行时加载的共享代码与资源文件。 |
| 共享库 | Shared library（`.so`） | Linux/Unix 常见共享库文件。 |
| 动态库 | Dynamic library（`.dylib`） | macOS 常见动态库文件形式之一。 |
| 运行时 | Runtime | 程序执行依赖的环境或组件，如 Java Runtime、.NET Runtime。 |
| 编译器 | Compiler | 把源代码转换成机器码或其他目标表示的工具。 |
| 解释器 | Interpreter | 解释或执行程序语言代码的运行程序；Python 常用 CPython 解释器。 |
| SDK | Software Development Kit | 为某个平台开发软件的工具、库、文档等集合。 |
| PATH | `PATH` environment variable | Shell 搜索可执行命令时使用的一组目录；不同系统的路径分隔规则不同。 |
| 环境隔离 | Environment isolation | 为不同软件建立相对独立的包/版本配置，以减少冲突。 |
| 虚拟环境 | Virtual environment | 如 Python `venv`，隔离某个项目的 Python 包环境；不是虚拟机。 |
| Conda 环境 | Conda environment | 使用 Conda 管理的相对隔离的包及运行环境，可包含 Python 和非 Python 依赖。 |
| 版本管理器 | Version manager | 管理多个软件版本并切换使用，如 pyenv、nvm。 |
| 便携软件 | Portable application | 相对少依赖传统安装过程、可在特定环境直接运行的软件。 |
| 软件许可证 | Software license | 规定软件使用、复制、修改、分发等权利和条件的条款。 |

### 一个科研场景

- 操作系统是 Windows 或 Ubuntu；
- **Python** 是编程语言，**CPython** 是其常见解释器；
- `conda create` 建立的是 **软件环境**，不是新操作系统；
- Jupyter Notebook/JupyterLab 是交互式工作界面，内核（Jupyter kernel）负责执行代码，但这里的 **Jupyter kernel 与操作系统内核不是一个概念**；
- 即使两个项目都叫 `python`，依赖版本不同也可能出现不同结果。

## 13. 终端、Shell 与命令行

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 终端 | Terminal | 用于输入命令和显示输出的交互界面；现代通常指终端模拟器。 |
| 终端模拟器 | Terminal emulator | 提供终端窗口的软件，如 Windows Terminal、macOS Terminal、iTerm2、GNOME Terminal。 |
| Shell | Shell / Command shell | 接收、解析并执行命令的程序，是操作系统交互层之一。 |
| Bash | Bourne Again SHell（Bash） | Linux 等系统常见的 Shell 与脚本语言。 |
| Zsh | Z shell（zsh） | macOS 现代版本默认的交互式 Shell，Linux 也能使用。 |
| PowerShell | PowerShell | 微软的跨平台 Shell、脚本与自动化工具，管道可传递结构化对象。 |
| CMD | Command Prompt / `cmd.exe` | Windows 传统命令解释器，与 PowerShell 不是同一种语言。 |
| Windows Terminal | Windows Terminal | 微软的终端应用，可以承载 PowerShell、CMD、WSL 的 Shell 等。 |
| 提示符 | Prompt | 终端显示并等待输入命令的部分，如 `$` 或 `PS C:\>`。 |
| 命令 | Command | 在 Shell 中调用的操作、程序或内建指令，如 `ls`、`cd`。 |
| 参数 | Argument | 提供给命令的输入内容，如文件名和目标路径。 |
| 选项 | Option / Flag | 改变命令行为的标记，如 `-l`、`--help`。 |
| 标准流重定向 | Redirection | 将命令输入/输出接到文件或其他流的机制。 |
| 管道 | Pipe / Pipeline | 把一个命令的输出连接给另一个命令；Unix 常传文本字节流，PowerShell 可传对象。 |
| 通配符 | Wildcard / Glob | 使用 `*`、`?` 等表达文件名匹配规则，具体行为依 Shell。 |
| 变量展开 | Variable expansion | 把 Shell 变量替换为对应值，如 Bash 中的 `$HOME`。 |
| 命令历史 | Command history | Shell 保存的先前输入命令记录。 |
| 自动补全 | Autocompletion | 输入命令、路径时自动补全，例如按 Tab 键。 |
| 别名 | Alias | 为命令或命令片段定义简短名称。 |
| Shell 脚本 | Shell script | 把一组 Shell 命令写成文件，用于批量或自动化操作。 |
| Bash 脚本 | Bash script（`.sh`） | 通常以 Bash 语法执行的脚本；`.sh` 扩展名本身不能保证解释器一定是 Bash。 |
| 批处理文件 | Batch file（`.bat` / `.cmd`） | Windows CMD 命令脚本格式。 |
| PowerShell 脚本 | PowerShell script（`.ps1`） | PowerShell 命令脚本。 |
| Shebang | Shebang（`#!`） | Unix 脚本文件首行用来指定解释器的特殊标记，如 `#!/usr/bin/env bash`。 |
| SSH | Secure Shell | 加密的远程登录与命令执行协议/工具，也支持隧道等。 |
| 伪终端 | Pseudo-terminal（PTY） | 软件模拟终端设备接口，常见于终端窗口或 SSH 会话。 |
| 手册页 | Manual page（man page） | Unix/Linux 软件命令与系统接口的传统使用说明。 |
| 帮助选项 | `--help` / `-h` | 很多命令提供的帮助参数，但不是所有命令都一致。 |
| 退出命令 | `exit` | 退出当前 Shell 或相关程序/会话，依具体上下文而定。 |
| 超级终端用户 | Superuser / root shell | 具有提升权限的 Shell 会话，任何命令都可能影响系统重要文件。 |

**四个最容易搞错的名字**：

```text
Windows Terminal ＝ 终端窗口程序
PowerShell       ＝ 可以运行在终端中的 Shell
CMD              ＝ 另一种 Windows Shell
WSL              ＝ Windows 中运行 Linux 环境的功能
```

这四者可以互相配合，但不能互换。参考：[Microsoft：Windows 命令行](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)、[Microsoft：PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/overview)、[Ubuntu：命令行入门](https://ubuntu.com/tutorials/command-line-for-beginners)。

## 14. 网络、远程访问与文件共享

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 计算机网络 | Computer network | 通过通信链路互相连接、交换信息的设备集合。 |
| 局域网 | Local Area Network（LAN） | 家庭、办公室或校园局部范围的网络。 |
| 广域网 | Wide Area Network（WAN） | 连接更广地理区域的网络。 |
| 互联网 | Internet | 基于 TCP/IP 等协议的全球互联网络。 |
| 内网 | Private network / Intranet | 组织内部或未直接向互联网公开的网络环境，概念取决于语境。 |
| 公网 | Public network / Public Internet | 对外可访问的互联网连接或地址空间；“公网 IP”更具体。 |
| IP 地址 | Internet Protocol address | IP 网络中标识接口/通信端点的地址。 |
| IPv4 / IPv6 | Internet Protocol version 4 / 6 | 两种主要 IP 协议版本，地址长度分别为 32 位和 128 位。 |
| 子网掩码 | Subnet mask | IPv4 中用于表达网络前缀范围的掩码。 |
| CIDR | Classless Inter-Domain Routing | 使用如 `/24`、`/64` 的前缀长度表示网络范围的方式。 |
| 默认网关 | Default gateway | 访问非本地网络时通常转发到的路由设备/下一跳。 |
| 路由器 | Router | 在不同 IP 网络之间转发数据包的设备或程序。 |
| 交换机 | Network switch | 主要在局域网络中转发以太网帧的网络设备。 |
| DNS | Domain Name System | 把域名解析为 IP 地址等记录的分布式命名系统。 |
| DHCP | Dynamic Host Configuration Protocol | 自动分配 IP 地址及其他网络配置的协议。 |
| MAC 地址 | Media Access Control address | 网络接口链路层使用的硬件/逻辑地址；与苹果的 Mac 电脑不是一回事。 |
| TCP | Transmission Control Protocol | 面向连接、提供可靠字节流服务的传输层协议。 |
| UDP | User Datagram Protocol | 无连接的数据报传输协议，通常不保证交付或顺序。 |
| 端口 | Port | TCP/UDP 等传输协议用于区分服务/会话的数字标识，如 22、80、443。 |
| HTTP / HTTPS | Hypertext Transfer Protocol / HTTP Secure | Web 请求协议；HTTPS 表示通过 TLS 等机制保护 HTTP 传输。 |
| TLS | Transport Layer Security | 保护网络通信的加密协议，HTTPS 常依赖它。 |
| 主机名 | Hostname | 计算机在某个网络/系统上下文中的名称。 |
| 域名 | Domain name | DNS 命名体系中的名称，如 `example.org`。 |
| 回环地址 | Loopback address | 指向本机网络协议栈的地址，常见 `127.0.0.1`、`::1`。 |
| localhost | localhost | 通常解析到本机回环地址的主机名。 |
| NAT | Network Address Translation | 转换网络地址的机制，常见于家庭路由器。 |
| 代理服务器 | Proxy server | 代替客户端或服务端转发请求的中间服务。 |
| 系统代理 | System proxy | 操作系统配置的代理参数；不是所有应用都会自动遵循。 |
| VPN 隧道 | VPN tunnel | 通过加密或封装等方法建立的逻辑网络通道。 |
| 远程桌面 | Remote desktop | 在一台设备上访问另一台计算机的图形桌面。 |
| RDP | Remote Desktop Protocol | 微软远程桌面常用协议。 |
| VNC | Virtual Network Computing | 基于远程帧缓冲等机制共享图形桌面的技术家族。 |
| SSH 登录 | SSH login | 通过 SSH 连接远程主机，常用于服务器终端操作。 |
| SFTP | SSH File Transfer Protocol | 基于 SSH 的文件传输协议；不是 FTP 的简单“加密开关”。 |
| SCP | Secure copy（scp） | 经 SSH 相关协议复制文件的工具/方式；现代实现可能使用 SFTP。 |
| SMB | Server Message Block | Windows 常见、macOS/Linux 也支持的网络文件共享协议。 |
| NFS | Network File System | Unix/Linux 服务器和科研集群常见的网络文件系统协议。 |
| 挂载网络盘 | Mount network share | 将 SMB/NFS 等网络共享接入本机文件访问树。 |
| 带宽 | Bandwidth | 网络链路单位时间可承载的数据量，常用 Mbps 或 Gbps。 |
| 往返时延 | Round-Trip Time（RTT） | 数据从发送端到对方再返回的往返时间。 |
| 丢包 | Packet loss | 传输中某些网络数据包未成功送达的现象。 |
| Ping | `ping` / ICMP echo | 常用的网络连通性/延迟测试方式；部分设备会限制 ICMP。 |

### 科研服务器里的两个常见词

- `ssh username@server.example.org`：通过 SSH 登录远程服务器，后面的命令通常在**远程主机**上执行。
- `/nfs/xxx/project`：常表示已挂载到本机目录树的 NFS 网络文件存储路径。**路径中出现 `/nfs` 不足以单独证明它一定是 NFS 挂载**，应结合 `mount`、`findmnt` 等查询。

## 15. 虚拟机、容器与跨系统使用

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 虚拟化 | Virtualization | 将硬件或系统资源抽象为相对独立的运行环境的技术。 |
| 虚拟机 | Virtual Machine（VM） | 模拟/虚拟一台计算机所需资源，通常运行独立来宾操作系统。 |
| 虚拟机监控程序 | Hypervisor | 创建和管理虚拟机执行环境的核心软件层。 |
| 宿主机 | Host machine / Host OS | 提供物理资源并承载虚拟化平台的机器/系统。 |
| 客户机 / 来宾系统 | Guest OS | 运行在虚拟机内部的操作系统。 |
| Type 1 虚拟机监控程序 | Type-1 / Bare-metal hypervisor | 直接在硬件层之上提供虚拟化的软件，如 Hyper-V 属此类架构。 |
| Type 2 虚拟机监控程序 | Type-2 / Hosted hypervisor | 在宿主操作系统上运行的虚拟化应用形式。 |
| Hyper-V | Microsoft Hyper-V | 微软的硬件虚拟化平台，可以运行 Windows/Linux 等来宾系统。 |
| VirtualBox | Oracle VM VirtualBox | 常用的跨平台桌面虚拟化软件。 |
| VMware | VMware virtualization products | 一系列虚拟化产品/技术名称，应区分具体产品。 |
| Parallels Desktop | Parallels Desktop | Mac 上用于运行虚拟机的商业桌面软件。 |
| WSL | Windows Subsystem for Linux | Windows 上运行 Linux 环境的功能；WSL 2 使用轻量虚拟机中的 Linux 内核。 |
| WSL 1 | Windows Subsystem for Linux 1 | 使用系统调用转换方式实现 Linux 兼容环境的较早架构。 |
| WSL 2 | Windows Subsystem for Linux 2 | 利用虚拟化运行真实 Linux 内核的架构，与 WSL 1 实现不同。 |
| Docker | Docker | 提供构建、分发、运行容器的软件与生态。 |
| 容器 | Container | 使用宿主内核提供隔离的进程运行环境，通常比完整虚拟机轻量。 |
| 容器镜像 | Container image | 打包程序、依赖和配置等的只读分层模板，用于创建容器。 |
| Dockerfile | Dockerfile | 描述如何构建容器镜像的文本文件。 |
| 镜像仓库 | Container registry | 存储和分发容器镜像的服务，如 Docker Hub。 |
| 命名空间 | Linux namespace | 为进程隔离部分系统资源视图的 Linux 内核机制。 |
| 控制组 | Control groups（cgroups） | Linux 用于组织进程、核算与限制 CPU/内存等资源的机制。 |
| Kubernetes | Kubernetes（K8s） | 用于编排、部署和管理容器化工作负载的平台。 |
| 端口映射 | Port mapping | 把宿主机端口和虚拟机/容器内服务端口关联起来的配置。 |
| 桥接网络 | Bridged networking | 让虚拟环境连接到宿主所在网络的一类联网方式。 |
| NAT 网络 | NAT networking | 虚拟化环境通过地址转换访问外部网络的方式。 |
| 共享文件夹 | Shared folder | 让宿主系统与虚拟系统交换文件的机制。 |
| 虚拟机快照 | VM snapshot | 保存虚拟机某一时刻状态的技术；通常不替代独立备份。 |
| 嵌套虚拟化 | Nested virtualization | 在虚拟机内再次使用虚拟化能力。 |

### 四种“我想在 Windows 上使用 Linux”方案

| 方案 | Linux 是否独立启动 | 能否与 Windows 同时运行 | 典型用途 | 需要注意 |
|---|---|---|---|---|
| 双系统（Dual boot） | 是 | 通常不能；须重启切换 | 希望完整独立使用 Linux | 改分区、引导项有数据风险 |
| WSL 2 | 由 Windows 管理 Linux 环境 | 能 | 命令行开发、Python、科研软件 | 并非完整普通 PC 启动方式，硬件/桌面体验有差异 |
| 虚拟机（VM） | 虚拟机中独立启动 | 能 | 系统实验、隔离软件和服务 | 额外占用 CPU、内存和存储 |
| 远程 Linux 服务器（SSH） | Linux 在远程主机启动 | 能 | GPU 计算、集群科研、长期任务 | 依赖网络、权限和远程资源 |

**为什么容器不等于虚拟机？** 虚拟机通常有自己的内核；Linux 容器共享底层 Linux 内核。Windows/macOS 上的 Linux 容器通常借助 Linux 虚拟化环境实现，不能仅凭“Docker 运行在 macOS 上”就推断容器直接共享 macOS 内核。

参考：[Microsoft：WSL 架构](https://learn.microsoft.com/zh-cn/windows/wsl/about)、[Microsoft：Hyper-V](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/overview)、[Docker：容器与虚拟机](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)、[Linux Kernel：cgroups](https://docs.kernel.org/admin-guide/cgroup-v2.html)。

## 16. 科研计算、开发与服务器常见术语

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 本地计算机 | Local machine | 当前用户直接操作的计算机。 |
| 远程主机 | Remote host | 通过网络连接并执行工作的另一台机器。 |
| 工作站 | Workstation | 为开发、科学计算或图形处理配置的个人/小型专业计算机。 |
| 计算节点 | Compute node | 集群中主要执行计算任务的主机。 |
| 登录节点 | Login node | HPC 集群中供用户登录、编辑与提交任务的节点，通常不适合重负载计算。 |
| 高性能计算 | High-Performance Computing（HPC） | 使用集群、并行硬件和调度系统执行较大规模计算。 |
| 集群 | Cluster | 多台互联计算机协同提供计算或服务能力的系统。 |
| 作业调度器 | Job scheduler | 管理集群作业队列和资源分配的组件。 |
| SLURM | Slurm Workload Manager | HPC 常见的批作业与资源调度系统。 |
| 作业 | Job | 提交到调度系统运行的一项计算任务。 |
| 队列 / 分区 | Queue / Partition | 调度系统分配任务资源的逻辑类别；具体术语依调度器。 |
| 批处理脚本 | Batch script | 描述作业命令、资源需求等的脚本。 |
| 交互式作业 | Interactive job | 让用户实时与分配的计算资源交互的作业。 |
| 核心数 | CPU core count | 任务可使用的 CPU 核心或调度单位数；需核对实际资源规则。 |
| GPU 显存 | Video RAM（VRAM） | 图形处理器使用的存储资源，不等于系统 RAM。 |
| CUDA | Compute Unified Device Architecture | NVIDIA 的 GPU 并行计算平台及相关工具生态。 |
| 驱动版本 | Driver version | GPU 等设备驱动的软件版本，可能影响计算程序兼容性。 |
| CUDA Toolkit | CUDA Toolkit | CUDA 编译器、库、工具等开发组件，不等于全部 GPU 驱动。 |
| Python 内核 | Jupyter kernel | 在 Notebook 中执行代码的后端进程/协议角色，不是 OS 内核。 |
| Git | Git | 分布式版本控制系统，记录代码和文本等文件的修订。 |
| 仓库 | Repository（repo） | 用于版本控制的项目数据和历史记录集合。 |
| SSH 密钥 | SSH key pair | 远程登录常用的一对公钥、私钥，私钥需安全保存。 |
| 端口转发 | Port forwarding / SSH tunneling | 将一端的网络端口连接到另一端，使远程服务可从本地访问。 |
| 长时间会话管理 | `tmux` / `screen` | 允许在终端断开后保持会话/程序运行的工具；前提是主机和任务未被外部终止。 |
| 后台服务管理 | `systemctl` | 在采用 systemd 的 Linux 系统中管理服务和检查状态的工具。 |
| 配置文件 | Configuration file | 保存程序行为、路径和参数的文件，如 YAML、TOML、INI 等。 |
| 日志文件 | Log file | 程序或系统记录运行事件、错误信息的文件。 |
| 工作目录 | Working directory | 运行脚本时解析相对路径的目录，应与脚本存放目录区分。 |
| 绝对路径可复现性 | Absolute-path portability | 绝对路径往往只在特定机器成立；跨平台项目更宜用配置或项目相对路径。 |

**科研实践中的层级**：Windows 笔记本 → SSH → Linux 登录节点 → 提交 Slurm 作业 → Linux 计算节点 → 挂载共享数据目录。这五个层次分别涉及本地系统、网络连接、账号、作业调度与存储权限，不宜混为一谈。

## 17. 系统维护、更新、故障排除与备份

| 中文名称 | 英文名称／缩写 | 含义与区别 |
|---|---|---|
| 操作系统更新 | OS update | 修复错误、安全漏洞及更新系统组件。 |
| 功能更新 | Feature update | 增加或改动产品功能的更新；具体发布策略依系统。 |
| 安全更新 | Security update | 主要用于修补漏洞或强化安全的更新。 |
| 驱动更新 | Driver update | 更新硬件适配程序，可能修复兼容性或性能问题。 |
| 补丁 | Patch | 修复特定问题的代码更改或软件更新包。 |
| 升级 | Upgrade | 通常指较大版本或功能层面的更新，如 Windows 大版本升级。 |
| 更新回滚 | Rollback | 恢复到较早版本或状态的操作，不总保证能完整还原个人数据。 |
| 系统还原 | System Restore | Windows 一类系统状态恢复功能，并非完整个人文件备份。 |
| 恢复点 | Restore point | 用于将某些系统配置恢复到此前状态的记录。 |
| 重置此电脑 | Reset this PC | Windows 重新安装/重置系统的恢复选项；保留文件与否依用户所选流程。 |
| 启动修复 | Startup Repair | 检测并尝试解决特定启动故障的恢复工具。 |
| 系统备份 | System backup | 将操作系统或相关数据复制保存，用于后续恢复。 |
| 文件备份 | File backup | 复制保存指定文档、项目和个人文件。 |
| 增量备份 | Incremental backup | 只备份相对上一次备份新增或变化的数据。 |
| 差异备份 | Differential backup | 备份相对于某次完整备份以来变化的数据。 |
| Time Machine 时间机器 | Time Machine | macOS 的备份系统，可按时间恢复文件和部分环境。 |
| 恢复密钥 | Recovery key | 找回加密磁盘/账户访问能力时使用的密钥或凭据，丢失可能导致无法恢复。 |
| 事件查看器 | Event Viewer | Windows 查看系统及应用事件日志的工具。 |
| Windows 事件日志 | Windows Event Log | Windows 记录安全、系统及应用事件的日志体系。 |
| Console 控制台 | Console app | macOS 查看系统及应用日志等的工具；这里不是命令行 Shell。 |
| 系统日志 | System log / Journal | 记录系统服务、内核及应用运行状态的日志集合。 |
| journalctl | `journalctl` | systemd 系统上查询 journal 日志的命令。 |
| 崩溃报告 | Crash report | 记录程序崩溃时的异常和调用信息。 |
| 蓝屏 | Blue Screen of Death（BSOD） | Windows 严重错误时显示的系统停止错误界面（俗称）。 |
| 内核恐慌 | Kernel panic | 内核遭遇无法安全继续运行的严重错误时采取的停止机制。 |
| 磁盘检查 | Disk check / File system check | 检查文件系统结构和部分磁盘问题的工具或过程。 |
| 恢复分区 | Recovery partition | 存放系统恢复组件的分区，不等于完整数据备份。 |
| 出厂重置 | Factory reset | 将设备还原为出厂或近似初始软件状态的操作，可能清除个人数据。 |

**维护原则**：更新前确认兼容性，改分区前进行独立备份，运行未知 `sudo`/管理员命令前看懂命令用途。参考：[Microsoft：Windows 恢复环境](https://support.microsoft.com/en-us/windows/experience/backup-recovery/windows-recovery-environment)、[Apple：Time Machine](https://support.apple.com/en-lamr/guide/mac-help/mh35860/27/mac/27)。

---
## 18. Windows、macOS、Linux 对照表

下表使用 **Windows 11、现代 macOS、Ubuntu / 常见 Linux 发行版** 作为理解示例。Linux 各发行版高度可定制，因此右列不是全部 Linux 系统的统一默认配置。

| 具体功能或概念 | Windows（常见） | macOS（常见） | Linux（以 Ubuntu 等为例） |
|---|---|---|---|
| 图形文件管理 | File Explorer（文件资源管理器） | Finder（访达） | Files / Nautilus、Dolphin 等 |
| 系统设置 | Settings、Control Panel | System Settings | GNOME Settings、KDE System Settings 等 |
| 任务 / 资源监控 | Task Manager | Activity Monitor | System Monitor、`top`、`htop` |
| 系统进程与服务 | Windows services、Service Control Manager | `launchd` | `systemd`（许多发行版） |
| 默认桌面 Shell / CLI | PowerShell、CMD 可选 | 默认交互 Shell 通常为 zsh | 很多发行版默认使用 Bash |
| 终端窗口 | Windows Terminal 等 | Terminal、iTerm2（第三方） | GNOME Terminal、Konsole 等 |
| 常见个人目录 | `C:\Users\用户名` | `/Users/用户名` | `/home/用户名` |
| 文件路径分隔符 | 通常 `\` | `/` | `/` |
| 系统卷 / 根位置 | 常见为 `C:\` | Unix 根目录 `/`，系统卷由 APFS 等组织 | 根目录 `/`，可独立挂载多个卷 |
| 典型文件系统 | NTFS | APFS | ext4、Btrfs、XFS 等 |
| 应用分发形式 | `.exe`、`.msi`、Store | `.app`、`.dmg`、`.pkg`、App Store | `.deb`、`.rpm`、软件仓库、Flatpak 等 |
| 命令行软件管理 | `winget` | `brew`（第三方） | `apt`、`dnf`、`pacman` 等 |
| 管理员操作 | “以管理员身份运行”、UAC | `sudo`、系统授权 | `sudo` / root（依配置） |
| 典型共享库文件 | `.dll` | `.dylib` | `.so` |
| 网络共享 | SMB | SMB 等 | SMB、NFS 等 |
| 系统自带日志界面 | Event Viewer | Console | `journalctl`、日志查看工具 |
| 全盘/卷加密 | BitLocker / 设备加密 | FileVault | LUKS/dm-crypt 等 |
| 防火墙 | Microsoft Defender Firewall | macOS 应用防火墙及其他底层机制 | `nftables` / `ufw` 等 |
| 系统备份 | Windows Backup、文件历史记录及其他备份方式 | Time Machine | 依发行版/工具，如 Déjà Dup、Borg 等 |
| 系统恢复 | WinRE | macOS Recovery | 恢复模式、Live USB、快照等 |
| 在本机运行 Linux | WSL 2、虚拟机、双系统 | 虚拟机、双系统（受硬件架构限制） | 本身已运行 Linux，也可用虚拟机或容器 |
| 查当前目录 | PowerShell `Get-Location` | `pwd` | `pwd` |
| 列出目录 | PowerShell `Get-ChildItem` | `ls` | `ls` |
| 查看进程 | `Get-Process`、Task Manager | `ps`、Activity Monitor | `ps`、`top`、`htop` |
| 当前用户 | `whoami` | `whoami` | `whoami` |

**避免机械类比**：Windows 的 `C:` 不完全等同于 Unix 的 `/`；macOS 的 Finder 与 Linux 的 GNOME Files 属于功能类似但不同实现；PowerShell 中 `ls` 可能是 `Get-ChildItem` 的别名，语法与 GNU `ls` 不一定一致。

## 19. 容易混淆的概念：逐组辨析

### 19.1 操作系统 vs 内核 vs 发行版

- **OS** 是完整运行平台；**Kernel** 是操作系统核心；**Linux distro** 是组合 Linux 内核和工具软件的一套系统。
- Windows 和 macOS 都不只是“一个内核”；Ubuntu 不只是“Linux 内核换了名字”。

### 19.2 Windows vs Windows NT vs Windows Server

- **Windows** 是产品家族；**Windows NT** 既有历史产品含义，也指现代 Windows 所继承的架构；**Windows Server** 是针对服务器设计和授权的产品线。

### 19.3 Mac vs macOS vs Macintosh

- **Mac** 是电脑产品家族；**macOS** 是运行在 Mac 上的操作系统；**Macintosh** 是该电脑家族的历史全名。

### 19.4 “系统盘” vs “分区” vs “硬盘”

- “**系统盘**”是日常用法，在 Windows 经常泛指 C 盘，但严格而言系统启动涉及启动分区、系统卷等不同结构。
- 一块**物理硬盘**可以有多个**分区**，一个文件系统**卷**也并非总与一个分区严格一一对应。

### 19.5 BIOS vs UEFI

- BIOS 是传统 PC 固件启动体系；UEFI 是现代固件接口规范。日常说“进 BIOS”通常也可能指打开 UEFI 固件设置。

### 19.6 MBR vs GPT

- MBR/GPT 主要谈的是**磁盘分区结构**，而 BIOS/UEFI 谈的是**固件启动接口**；它们经常配对出现，但属于不同维度。

### 19.7 双系统 vs 虚拟机 vs WSL vs 远程服务器

- **双系统**：两个系统都安装在本机，选择启动其中一个。
- **虚拟机**：在现有系统内启动一个模拟的独立系统环境。
- **WSL 2**：Windows 管理的 Linux 运行环境，底层利用轻量虚拟化。
- **远程服务器**：Linux 实际运行在另一台机器上，本机只是通过网络访问它。

### 19.8 虚拟桌面 vs 虚拟机

- **虚拟桌面**是同一个系统会话中增加多个窗口工作空间；**虚拟机**运行另一套操作系统环境。这两者完全不同。

### 19.9 Terminal vs Shell vs 命令行

- **Terminal** 是显示与输入界面；**Shell** 是解析并执行命令的程序；**CLI** 是文本交互方式。
- 你在 Windows Terminal 中可以打开 PowerShell、CMD、WSL 的 Bash，它们不是同一个东西。

### 19.10 CMD vs PowerShell vs Bash

- 三者是不同的 Shell 及脚本语言；命令名相似不代表语法或输出一样。PowerShell 的管道可以传递对象，Bash/Unix 工具管道传统上主要传递字节文本流。

### 19.11 管理员 vs root vs sudo

- **Administrator** 常指 Windows 管理角色；**root** 是 Unix/Linux 的超级用户；**sudo** 是按照配置临时以目标身份执行命令的工具。

### 19.12 文件格式 vs 文件扩展名

- `.csv`、`.pdf` 是文件名后缀。文件内部格式必须符合对应规范；直接改后缀一般不会转换文件内容。

### 19.13 文件快捷方式 vs 符号链接 vs 硬链接

- Windows `.lnk` 是 Shell 快捷方式；符号链接保存指向目标的路径；硬链接为同一个底层文件对象提供另一个目录项。删除其中一种“入口”后的行为并不完全相同。

### 19.14 磁盘格式化 vs 重新分区 vs 重装系统

- **格式化**处理文件系统；**重新分区**改变存储布局；**重装系统**重新部署操作系统。三者有时在安装向导中连续发生，但并不是一个动作。

### 19.15 删除文件 vs 清空回收站 vs 安全擦除

- 删除和清空回收站通常只改变文件系统中可见性/空间分配等信息，不保证底层数据立即不可恢复；SSD 上的数据清除与加密擦除又涉及其他机制。

### 19.16 休眠 vs 睡眠 vs 关机

- **Sleep（睡眠）**：保持部分系统状态并低功耗等待唤醒；**Hibernate（休眠）**：将系统状态写入非易失性存储后进入更低功耗状态；**Shutdown（关机）**：结束或部分终止运行状态。具体 Windows/macOS 实现与硬件策略可能不同。

### 19.17 RAM vs ROM vs SSD

- **RAM** 主要供程序运行，通常易失；**ROM/Flash 固件存储**可在断电后保留内容；**SSD** 是长期存储文件和系统的设备。

### 19.18 内存缓存 vs 磁盘缓存 vs 虚拟内存

- **缓存**是为了减少重复访问开销；**虚拟内存**是一套地址管理抽象；**Swap/Pagefile** 是可能辅助虚拟内存工作的磁盘后备空间。三者不能互相替换。

### 19.19 虚拟环境（venv/Conda）vs 虚拟机 vs 容器

- **venv/Conda**：隔离软件包与运行时环境；**容器**：隔离进程和部分系统资源，常共享内核；**虚拟机**：通常运行独立来宾内核。

### 19.20 源代码 vs 编译文件 vs 可执行文件

- **源代码**是供程序员或工具阅读/处理的代码；**编译产物**是工具转换后的结果；**可执行文件**是能够被运行环境加载执行的程序格式。并非所有语言都必须先编译成本机机器码。

### 19.21 macOS 的“应用内核” vs 操作系统内核

- **Jupyter kernel**、某些软件所说的 kernel，通常是“执行引擎”或技术模块；**OS kernel** 则是操作系统管理资源的核心。务必根据上下文判断。

### 19.22 备份 vs 同步 vs 快照

- **备份**用于恢复历史数据；**同步**保持多个位置状态一致（误删也可能同步扩散）；**快照**记录某时刻存储状态，可能与原始存储共享底层资源。**同步盘不天然等于备份**。

### 19.23 下载速度 Mbps vs 文件大小 MB

- `Mb` 表示 megabit，`MB` 表示 megabyte（字节）；通常 8 bit = 1 byte。网络标称 `100 Mbps` 并不表示每秒直接下载 `100 MB`，协议开销和实际网络状况还会影响速度。

### 19.24 “浏览器代理” vs “系统代理” vs “全局代理”

- **浏览器代理**只影响遵循浏览器代理配置的流量；**系统代理**影响遵循系统代理配置的应用；**全局代理**是部分代理软件的运行模式名称，具体范围取决于软件是否实现了系统级流量接管，不能假设所有流量都一定被代理。

---

## 20. 最实用的命令与路径速查

> 下列命令用于帮助认识术语；在不同 Shell 上不能机械照抄。凡是涉及删除、格式化、权限提升、服务停止的操作，都要先确认作用对象。

### 20.1 Linux / macOS 常见命令

| 命令 | 英文含义／用途 | 例子或补充 |
|---|---|---|
| `pwd` | Print working directory，显示当前工作目录 | `pwd` |
| `ls` | List，列出目录内容 | `ls -la`（选项可因系统不同而差异） |
| `cd` | Change directory，切换目录 | `cd ~/Documents` |
| `mkdir` | Make directory，建立文件夹 | `mkdir results` |
| `cp` | Copy，复制 | `cp source.txt backup.txt` |
| `mv` | Move，移动或改名 | `mv old.txt new.txt` |
| `rm` | Remove，删除 | **谨慎**，直接删除可能不经过回收站 |
| `cat` | Concatenate，显示/拼接文件内容 | `cat notes.txt` |
| `less` | 分页查看文本内容 | `less logfile.log` |
| `grep` | 搜索符合文本模式的行 | `grep 'ERROR' logfile.log` |
| `find` | 遍历目录并查找文件 | `find . -name '*.txt'` |
| `which` / `command -v` | 查看命令位置/解析结果 | `command -v python` |
| `echo` | 输出文本或变量值 | `echo "$HOME"` |
| `env` | 查看/设置命令环境 | `env` |
| `ps` | Process status，显示进程 | `ps aux` |
| `top` | 动态查看进程和系统负载 | `top` |
| `df` | Disk free，查看文件系统使用率 | `df -h` |
| `du` | Disk usage，查看目录占用 | `du -sh .` |
| `uname` | 查看系统/内核信息 | `uname -a` |
| `whoami` | 查看当前账户 | `whoami` |
| `chmod` | Change mode，更改 Unix 权限位 | `chmod u+x script.sh` |
| `chown` | Change owner，更改文件所有者 | 通常需要额外权限 |
| `sudo` | 临时以授权身份执行命令 | 不要执行来源不明的管理员命令 |
| `ssh` | Secure Shell，远程登录 | `ssh user@host` |
| `scp` / `sftp` | 安全文件传输工具 | 用于服务器文件复制/交互传输 |
| `man` | Manual，查看命令手册 | `man ls` |
| `systemctl` | systemd 服务控制 | 仅适用采用 systemd 的系统 |
| `journalctl` | systemd 日志查询 | `journalctl -b` |
| `nvidia-smi` | NVIDIA GPU 状态查看工具 | 需要适用的 NVIDIA 驱动/环境 |

### 20.2 Windows PowerShell 常见命令

| 命令 | 英文含义／用途 | 例子或补充 |
|---|---|---|
| `Get-Location` | 获取当前目录 | 类似 Unix 的 `pwd` |
| `Get-ChildItem` | 枚举目录内容 | `Get-ChildItem`；常见别名 `ls`、`dir` |
| `Set-Location` | 切换工作目录 | `Set-Location C:\Users`；别名 `cd` |
| `New-Item` | 创建文件或目录等对象 | `New-Item -ItemType Directory -Name results` |
| `Copy-Item` | 复制文件或目录 | `Copy-Item a.txt b.txt` |
| `Move-Item` | 移动文件或目录 | `Move-Item a.txt archive\` |
| `Remove-Item` | 删除对象 | **谨慎**，可能直接删除重要文件 |
| `Get-Content` | 读取文件内容 | `Get-Content notes.txt` |
| `Select-String` | 在文本中检索字符串/模式 | `Select-String -Path a.txt -Pattern 'ERROR'` |
| `Get-Process` | 查看进程 | `Get-Process` |
| `Get-Service` | 查看 Windows 服务 | `Get-Service` |
| `Get-Command` | 查看命令来源与类型 | `Get-Command python` |
| `Get-Help` | 查看命令帮助 | `Get-Help Get-Process` |
| `Get-ComputerInfo` | 查看计算机及系统信息 | `Get-ComputerInfo` |
| `Get-NetIPAddress` | 查看本机网络地址 | 部分系统环境中可用 |
| `Test-Connection` | 测试网络连接 | `Test-Connection example.org` |
| `winget` | Windows 包管理器 | `winget list`（是否可用依安装配置） |
| `wsl` | Windows 上管理 WSL | `wsl --list --verbose` |

### 20.3 常见路径和特殊记号

| 路径或记号 | 典型含义 | 平台/提醒 |
|---|---|---|
| `C:\` | Windows 中一个磁盘卷的根位置 | 不必然代表整块物理硬盘 |
| `C:\Users\用户名` | Windows 用户配置和个人文件目录 | 可因配置而异 |
| `%USERPROFILE%` | Windows CMD 风格的用户配置目录环境变量 | 例如 `C:\Users\Alice` |
| `$env:USERPROFILE` | PowerShell 读取用户目录环境变量 | PowerShell 语法，不是 Bash 语法 |
| `%APPDATA%` | Windows 用户漫游应用数据目录环境变量 | 用于许多软件配置 |
| `C:\Windows` | Windows 常见系统目录 | 不应随意修改 |
| `C:\Program Files` | Windows 常见 64 位程序安装目录 | 可能依设备配置而异 |
| `/` | Unix/Linux/macOS 文件树的根 | 不等于 Windows 的 `C:` |
| `~` | Shell 中当前用户主目录的常见缩写 | 在 Bash/Zsh 中常用 |
| `.` | 当前目录 | 常见于 Unix Shell 等环境 |
| `..` | 上一级目录 | 常见于多平台 |
| `/home/用户名` | Linux 常见普通用户主目录 | 依系统配置而异 |
| `/Users/用户名` | macOS 常见用户主目录 | 依系统配置而异 |
| `/etc` | Unix/Linux 系统中常见全局配置目录 | macOS 也有相应路径/链接 |
| `/usr` | Unix 系统中重要的程序、库和共享资源目录 | 并不是普通用户自己的主目录 |
| `/var` | Unix 系统中可变数据目录 | 如日志、缓存、服务数据 |
| `/tmp` | 临时文件常用目录 | 通常不能假设会长期保留 |
| `/mnt` | Linux 中常见的临时/手工挂载点父目录 | 目录名本身不能证明存储类型 |
| `/media` | Linux 中常见可移动介质挂载位置 | 具体依桌面及发行版 |
| `/Volumes` | macOS 常见挂载卷位置 | 例如外接磁盘 |
| `/Applications` | macOS 常见应用安装位置 | 特定软件也可能不在此处 |
| `/Library` | macOS 机器级共享的配置和支持数据位置 | 与个人 `~/Library` 不同 |
| `~/Library` | macOS 用户级配置、应用支持等目录 | 默认常不直接显示 |
| `/dev` | Unix 系设备接口文件目录 | 包含很多虚拟/设备节点 |
| `/proc` | Linux 常见的进程与内核信息虚拟文件系统 | macOS 通常没有相同的标准 `/proc` 布局 |

### 20.4 用什么工具检查什么问题？

| 想知道的问题 | Windows 常用做法 | macOS 常用做法 | Linux 常用做法 |
|---|---|---|---|
| 系统当前占用多少 RAM？ | 任务管理器 → 性能 → 内存 | 活动监视器 → 内存 | `free -h`、`top` |
| 谁占用 CPU？ | 任务管理器 → 进程 | 活动监视器 → CPU | `top` / `htop` |
| 系统版本是什么？ | 设置 → 系统 → 系统信息，或 `winver` | Apple 菜单 → 关于本机 | `cat /etc/os-release`、`uname -r` |
| 程序装在什么位置？ | `Get-Command`、应用属性 | Finder、`command -v` | `command -v`、包管理器查询 |
| 磁盘还有多少空间？ | 文件资源管理器、磁盘管理 | Finder、磁盘工具 | `df -h` |
| 网络是否能访问目标？ | `Test-Connection` / `ping` | `ping` | `ping` |
| 服务器能否连上？ | PowerShell 的 `ssh` | Terminal 的 `ssh` | `ssh` |
| 文件或目录权限是什么？ | 文件属性 → 安全 | Finder → 显示简介，或 `ls -l` | `ls -l`、`stat`、`getfacl`（若已安装） |
| 开机服务为什么失败？ | 事件查看器、服务管理 | Console、`launchctl` | `systemctl status`、`journalctl` |

---

## 21. 推荐学习路线与官方资料

### 21.1 建议学习顺序

1. **先认识三大系统**：Windows/macOS/Linux 的关系，内核、发行版、桌面系统与服务器系统。
2. **理解存储**：磁盘、分区、卷、文件系统、路径、权限；这是日常装机与科研文件操作最常见的困惑来源。
3. **理解程序怎么运行**：程序、进程、线程、CPU、RAM、虚拟内存、后台服务。
4. **再学终端**：终端、Shell、CMD/PowerShell/Bash、环境变量、`PATH`、绝对路径和相对路径。
5. **最后掌握跨系统工作**：SSH、WSL 2、虚拟机、容器、远程集群及备份/恢复。

### 21.2 官方及高可信资料（检索时间：2026-10-21）

| 资料 | 机构 | 适合学习什么 |
|---|---|---|
| [Windows：用户态与内核态](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) | Microsoft Learn | 内核、权限与运行隔离 |
| [Windows 注册表结构](https://learn.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry/) | Microsoft Learn | 注册表及配置管理 |
| [Windows 命令行参考](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands) | Microsoft Learn | CMD、PowerShell 和 Windows 命令 |
| [PowerShell 概述](https://learn.microsoft.com/en-us/powershell/scripting/overview) | Microsoft Learn | Shell、脚本、对象管道 |
| [WSL 介绍](https://learn.microsoft.com/zh-cn/windows/wsl/about) | Microsoft Learn | Windows 与 Linux 共用环境、WSL 1/2 |
| [Hyper-V 虚拟化](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/overview) | Microsoft Learn | 虚拟机、宿主与客户机 |
| [UEFI Secure Boot](https://learn.microsoft.com/en-us/windows-hardware/drivers/bringup/secure-boot) | Microsoft Learn | 启动安全与固件 |
| [NTFS 概述](https://learn.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview) | Microsoft Learn | Windows 文件系统 |
| [Apple：Finder 使用指南](https://support.apple.com/guide/mac-help/organize-your-files-in-the-finder-mchle9f0a1b2/mac) | Apple Support | macOS 文件管理 |
| [Apple：磁盘工具和 APFS](https://support.apple.com/guide/disk-utility/welcome/mac) | Apple Support | macOS 存储、卷、分区 |
| [Apple：Gatekeeper](https://support.apple.com/guide/security/gatekeeper-and-runtime-protection-sec5599b66df/web) | Apple Platform Security | Mac 软件安全 |
| [Apple：Time Machine](https://support.apple.com/en-lamr/guide/mac-help/mh35860/27/mac/27) | Apple Support | 备份与恢复 |
| [Ubuntu 命令行入门](https://ubuntu.com/tutorials/command-line-for-beginners) | Canonical / Ubuntu | Linux 初学者命令 |
| [Linux 内核文档主页](https://docs.kernel.org/) | Linux Kernel Documentation | 内核结构、驱动、文件系统等 |
| [Linux：控制组 cgroups v2](https://docs.kernel.org/admin-guide/cgroup-v2.html) | Linux Kernel Documentation | Linux 容器资源管理 |
| [Docker：什么是容器](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/) | Docker Docs | 容器与虚拟机的区别 |
| [Docker：什么是镜像](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/) | Docker Docs | 容器软件分发机制 |

### 21.3 本手册的使用边界

- 重点是**建立术语知识地图**，不等于操作系统教材中的全部数学、内核源码和协议细节。
- 特定功能是否可用，取决于操作系统版本、家庭版/专业版、芯片架构、软件安装状况和管理员政策。
- 命令示例主要用于概念理解，执行会改变系统状态的命令前，应先确认当前路径、账号权限、文件备份和目标主机。
- 技术术语并非始终一一对应，例如 *drive / disk / volume* 的中文都可能被口语称为“盘”，必须结合上下文区分。

---

**最简总结**：硬件提供计算与存储资源；固件帮助完成机器初始化和系统启动；内核负责核心资源管理；操作系统提供完整运行平台；桌面与终端提供人机交互方式；虚拟机、容器、WSL、SSH 则使我们能够跨机器、跨环境或跨系统工作。
