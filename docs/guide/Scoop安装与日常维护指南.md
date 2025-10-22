---
title: 🚀Scoop 安装与日常维护指南
---
Scoop 是 Windows 上最简洁优雅的软件包管理器之一。通过命令行即可快速安装、更新、清理各类开发工具，体验接近 macOS 的 Homebrew。

---
## 一、启用脚本执行权限

Windows 默认禁止执行脚本，需要手动放开权限（仅限当前用户）：

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

这条命令的含义：

- **RemoteSigned**：只允许运行本地脚本或来自可信签名的远程脚本；
- **Scope CurrentUser**：只对当前用户生效；
- **Force**：跳过确认提示。
---
## 二、安装 Scoop

从官方安装脚本下载安装：

```
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

验证安装是否成功：

```
scoop --version
```
---
## 三、如果安装后命令无效

有时由于网络或权限问题，Scoop 目录未初始化，可以手动修复：

```
cd ~\scoop
git init
scoop update
```
---
## 四、添加常用软件源（Buckets）

Scoop 的软件仓库称为 **bucket**，类似于 Homebrew 的 tap。  
建议添加以下常用仓库：

```
scoop bucket add extras
scoop bucket add nerd-fonts
```

---
## 五、日常维护命令

```
scoop update              # 更新 Scoop 本身和所有 buckets
scoop list                # 查看已安装软件
scoop status              # 查看哪些软件可更新
scoop update *            # 一键升级所有软件
scoop cleanup *           # 清理旧版本释放空间
scoop cache rm *          # 清空下载缓存
scoop bucket list         # 查看已添加的仓库
```

---
## 六、一键维护脚本（推荐）

常用维护组合命令：

```
scoop update * && scoop cleanup * && scoop cache rm *
```

此命令会：

1. 更新所有包；
2. 清理旧版本；
3. 清空缓存文件。

---
## 七、网络加速建议

⚠️ Scoop 依赖 GitHub 资源，国内网络环境下安装和更新常会超时。建议在代理 **Tun 模式** 下运行 Scoop 命令（如 Clash Tun、Clash Verge Tun）。

---

## 八、总结

|   |   |
|---|---|
|操作|命令|
|安装 Scoop|`Invoke-RestMethod -Uri [https://get.scoop.sh](https://get.scoop.sh/)`|
|更新全部软件|`scoop update *`|
|清理旧版本|`scoop cleanup *`|
|清理缓存|`scoop cache rm *`|
|添加 extras 仓库|`scoop bucket add extras`|
|一键维护|`scoop update * && scoop cleanup * && scoop cache rm *`|

---

💡 建议：在 PowerShell 中添加别名函数，如：

```
function scoopup { scoop update *; scoop cleanup *; scoop cache rm * }
```

以后只需执行 `scoopup` 即可完成全部维护。

[^1]: 
