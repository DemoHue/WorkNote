# Claude Code 下载与配置指南

---

## 1. VPN 准备

访问 Claude Code 需要使用 VPN，建议选择**美国节点**。

---

## 2. WSL（Windows Subsystem for Linux）配置

> **说明**：此步骤仅 Windows 用户需要，Mac 用户可跳过。

### 2.1 启用 WSL 功能（仅旧版 Windows 需要）

> **注意**：Windows 10 Build 19041 及以上版本（含 Windows 11）可直接跳到 2.2，`wsl --install` 会自动启用所需功能。

若系统版本较旧，需手动启用：

1. 打开「开始菜单」，搜索「启用或关闭 Windows 功能」
2. 勾选以下两项：
   - 虚拟机平台（Virtual Machine Platform）
   - 适用于 Linux 的 Windows 子系统
3. 点击「确定」后重启系统

### 2.2 安装 WSL

右键点击「开始菜单」→ 打开「Windows PowerShell（管理员）」，执行：

```powershell
wsl --install
```

此命令会自动启用相关功能并安装 Ubuntu（默认使用 WSL 2）。安装完成后重启电脑。

首次启动 Ubuntu 会自动完成初始化（约 1-2 分钟），之后按提示设置 Linux 用户名和密码（密码输入时不显示字符，输完回车确认即可）。

**查看可用发行版列表：**

```powershell
wsl --list --online
```

**安装指定发行版（如 Ubuntu）：**

```powershell
wsl --install -d Ubuntu
```

### 2.3 修改 WSL 网络模式

打开「开始菜单」→ 搜索并打开 **WSL Settings**，将网络模式从 **NAT** 改为 **Mirrored**（镜像模式）。

修改后运行 
```powershell
wsl --shutdown
```

> 镜像模式下 WSL 可以直接共享宿主机的 VPN 网络，无需额外配置代理。

---

## 3. 安装 VSCode 及 Claude Code 插件

前往 [VSCode 官网](https://code.visualstudio.com/) 下载并安装 VSCode，确保 VPN 已开启，然后在 VSCode 扩展市场中搜索并安装 **Claude Code** 插件。

---

## 4. 在 WSL 中安装 Claude Code

> 参考官方文档（如链接失效请在 [docs.anthropic.com](https://docs.anthropic.com) 搜索 Claude Code Quickstart）：
> `https://code.claude.com/docs/en/quickstart#native-install-recommended`

确保 VPN 已开启，打开「开始菜单」启动 WSL，执行以下安装命令（适用于 macOS / Linux / WSL）：

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

安装完成后，在终端输入 `claude`，若出现交互界面则说明安装成功。

---

## 5. Claude Code 配置

### 5.1 进入配置目录

```bash
cd ~/.claude
```

### 5.2 创建配置文件

```bash
touch settings.json
```

> 若文件已存在，此命令不会覆盖原有内容。

### 5.3 在 Windows 文件资源管理器中打开该目录

```bash
explorer.exe .
```

### 5.4 编辑 settings.json

在打开的文件夹中找到 `settings.json`，填入配置内容（具体内容请参考群文件），保存后关闭。

### 5.5 验证安装与基础配置

在 WSL 中输入 `claude` 进入 Claude Code 界面，可使用以下常用命令：

| 命令 | 说明 |
|------|------|
| `/context` | 查看当前会话的上下文 token 分配情况 |
| `/model` | 选择使用的模型及运行模式（如 Max/Normal） |
| `/config` | 修改配置项，例如将界面语言设置为 `中文` |

---

> **提示**：若在任何步骤中遇到网络问题，请确认 VPN 已正常连接并选择了美国节点。
