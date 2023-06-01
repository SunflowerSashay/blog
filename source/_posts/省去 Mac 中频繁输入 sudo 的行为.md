---
title: 省去 Mac 中频繁输入 sudo 的行为
date: 2023-06-01 21:30:42
tags: macOS, Mac, sudo, 管理员权限, Keychain, 命令行, 系统管理, 安全性, 工具, 效率
---

在使用 Mac 时，您可能会遇到需要执行管理员权限操作的情况。这时，您可能会频繁地使用 sudo 命令来获取临时的管理员权限。然而，这种频繁输入密码的行为可能会变得繁琐和不便。在本文中，我们将探索一些方法，帮助您省去在 Mac 中总是需要输入 sudo 的行为。

## 使用 visudo

visudo 是一个用于编辑 sudoers 文件的命令。通过编辑该文件，您可以配置允许特定用户执行特定命令时无需输入密码。

```bash
$ sudo visudo
```

在打开的 sudoers 文件中，您可以找到 `%admin ALL=(ALL) ALL` 这样的行，将其替换为：

```bash
%admin ALL=(ALL) NOPASSWD: ALL
```

这样一来，管理员组成员就无需输入密码即可执行任何命令。

## 使用 Keychain

macOS Keychain 是一个密码管理工具，通过将 sudo 密码添加到 Keychain 中，可以省去每次输入密码的麻烦。

```bash
$ sudo visudo
```

在打开的 sudoers 文件中，找到 `%admin ALL=(ALL) ALL` 这样的行，在其下方添加以下内容：

```bash
Defaults        env_keep += "SUDO_ASKPASS"
Defaults:USER   env_keep += "SUDO_ASKPASS"
```

然后，执行以下命令将 `sudo` 密码添加到 `Keychain`：

```bash
$ sudo sh -c 'echo "MyPassword" | sudo -S -v'
```

请将 "MyPassword" 替换为您自己的 `sudo` 密码。

## 结论

通过采用上述方法，您可以轻松省去在 Mac 中频繁输入 sudo 的行为。您可以根据自己的需求选择适合的方法来简化管理员权限操作。无论您选择哪种方法，都应注意确保安全性，避免滥用权限。

希望本文对您有所帮助！如有任何疑问，请随时提出。
