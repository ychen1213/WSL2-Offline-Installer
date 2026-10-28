# WSL 2 离线安装包（Windows x64）

下载微软官方 WSL 安装程序后，将未经修改的 MSI、中文说明、来源记录和校验文件打包为 ZIP，便于下载和传输。

- **WSL 应用版本：3.0.3（稳定版）**，支持 WSL 2。应用版本号与 WSL 1 / WSL 2 的运行模式是两回事。
- **架构：x64 / AMD64**，适合 Intel / AMD 64 位 Windows 电脑；不适用于 ARM64 电脑。
- 官方发布时间：2026-10-09；本包核验日期：2026-10-28。
- 安装程序：`wsl.3.0.3.0.x64.msi`（367,575,040 字节）。
- 微软数字签名已验证有效，签名者为 Microsoft Corporation。

## 下载

- [下载 WSL2-3.0.3-x64.zip](https://github.com/ychen1213/WSL2-Offline-Installer/releases/download/wsl-3.0.3-x64/WSL2-3.0.3-x64.zip)
- [下载 ZIP 的 SHA-256 校验文件](https://github.com/ychen1213/WSL2-Offline-Installer/releases/download/wsl-3.0.3-x64/WSL2-3.0.3-x64.zip.sha256)
- [查看本仓库 Releases](https://github.com/ychen1213/WSL2-Offline-Installer/releases)
- [微软原始发布页](https://github.com/microsoft/WSL/releases/tag/3.0.3)

## 安装步骤

以下步骤适用于 Windows 11 x64。电脑需要支持虚拟化，并在 BIOS / UEFI 中启用硬件虚拟化。

1. 解压 ZIP，进入 `WSL2-3.0.3-x64` 文件夹，双击 `wsl.3.0.3.0.x64.msi`，按安装向导完成安装。
2. 以管理员身份打开 PowerShell，启用虚拟机平台：

   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

3. 重启 Windows，然后在 PowerShell 中执行：

   ```powershell
   wsl --set-default-version 2
   wsl --version
   wsl --status
   ```

4. 如需安装 Ubuntu，联网后运行：

   ```powershell
   wsl --install -d Ubuntu
   ```

5. 安装 Linux 发行版后，可通过以下命令确认其 `VERSION` 为 `2`：

   ```powershell
   wsl --list --verbose
   ```

**本 ZIP 包含 WSL 运行环境安装程序，不包含 Ubuntu 等 Linux 发行版。** 因此它可以离线安装 WSL 本身；完整离线部署 Linux 环境还需要单独准备对应发行版文件。现有发行版不会因设置默认版本而自动转换；需要时可按微软文档使用 `wsl --set-version <发行版名称> 2`。

## 校验

微软原始 MSI 的 SHA-256：

```text
ae977286974255bd26bf925f00f40f5692c6b2084155cbc0563c09aea091f211
```

在解压目录中运行：

```powershell
Get-FileHash .\wsl.3.0.3.0.x64.msi -Algorithm SHA256
Get-AuthenticodeSignature .\wsl.3.0.3.0.x64.msi | Format-List Status,SignerCertificate
```

ZIP 本身的 SHA-256 见同名 `.zip.sha256` 附件；包内 `SHA256SUMS.txt` 提供各文件的 SHA-256。`SOURCES.json` 记录原始下载地址、官方摘要、文件大小及签名验证结果。

## 来源与许可

- [微软 WSL 安装说明及离线安装步骤](https://learn.microsoft.com/windows/wsl/install#offline-install)
- [微软 WSL 3.0.3 官方发布页](https://github.com/microsoft/WSL/releases/tag/3.0.3)
- [微软官方 x64 MSI 下载地址](https://github.com/microsoft/WSL/releases/download/3.0.3/wsl.3.0.3.0.x64.msi)
- [微软 WSL 项目](https://github.com/microsoft/WSL)

本仓库由用户维护，提供微软原始安装程序的打包镜像。安装程序未经修改，相关版权及使用条款以微软安装程序及上游项目随附条款为准；包内保留上游 3.0.3 版本的 `MICROSOFT-WSL-LICENSE.txt` 和第三方声明 `MICROSOFT-WSL-NOTICE.txt`。
