# IDM Activation Script (IAS)

一个开源工具，用于冻结 [Internet Download Manager](https://www.internetdownloadmanager.com/) 的 30 天试用期，实现终身使用。

> **注意：** 脚本界面为英文，但本文档详细解释了每一项的含义，对照操作即可。

---

## 免责声明

本项目仅供学习和研究使用。请支持正版软件，如果您喜欢 IDM 并经常使用，建议购买正版授权。

---

## 快速使用（推荐）

右键点击 Windows 开始菜单，选择 **PowerShell** 或 **终端**（不是 CMD），复制以下命令并回车：

```powershell
iex(irm https://raw.githubusercontent.com/UselessWater/IDM-Activation-Script/master/IAS.ps1)
```

脚本会自动下载并运行，按照屏幕提示操作即可。

---

## 手动下载使用

1. 从 [GitHub](https://github.com/UselessWater/IDM-Activation-Script/archive/refs/heads/main.zip) 下载 ZIP 文件
2. 解压到文件夹（**不要直接在压缩包内运行**）
3. 右键点击 `IAS.cmd`，选择 **以管理员身份运行**
4. 按屏幕提示选择对应选项

---

## 脚本菜单说明

运行脚本后，会显示以下英文菜单：

| 选项 | 英文 | 中文说明 |
|------|------|----------|
| [1] | Activate | **激活** — 通过注册表锁定方式激活 IDM。部分用户可能无效，会出现假序列号弹窗 |
| [2] | Freeze Trial | **冻结试用（推荐）** — 将 30 天试用期锁定为永久，更新 IDM 后依然有效 |
| [3] | Reset Activation / Trial Status | **重置激活/试用状态** — 清空所有激活信息，恢复到未激活状态 |
| [4] | Download IDM | **下载 IDM** — 打开 IDM 官方下载页面 |
| [5] | Homepage | **项目主页** — 打开本项目 GitHub 页面 |
| [0] | Exit | **退出** — 关闭脚本 |

选择方式：直接按键盘上对应的数字键。

---

## 操作过程中常见的英文提示

| 脚本显示 | 中文含义 |
|----------|----------|
| `Initializing...` | 正在初始化，等待检测完成 |
| `Checking Info - [...]` | 显示当前系统信息（Windows 版本 / 架构 / IDM 版本） |
| `Backing up registry to ...` | 正在备份注册表，以防出现问题可恢复 |
| `Deleting IDM registry info...` | 正在清理旧的注册信息 |
| `Adding registry keys...` | 正在写入新的注册表项 |
| `Scanning IDM CLSID registry keys in ...` | 正在扫描 IDM 相关的注册表项 |
| `Locking IDM CLSID registry keys...` | 正在锁定注册表，使 IDM 无法修改 |
| `Deleting IDM CLSID registry keys...` | 正在删除被检测到的注册表项 |
| `Generating registration info...` | 正在生成随机的注册信息（仅激活模式） |
| `Triggering downloads ... please wait...` | 正在触发 IDM 下载以创建必要的注册表项 |
| `IDM has been successfully activated.` | ✅ IDM 已成功激活 |
| `Successfully froze IDM 30-day trial period.` | ✅ 已成功冻结 30 天试用期 |
| `IDM activation/trial has been reset.` | ✅ 激活/试用状态已重置 |
| `IDM [Internet Download Manager] is not installed.` | ❌ 未检测到 IDM 安装 |
| `Press 0 to go back...` / `Press any key to go back...` | 按 0 或其他键返回主菜单 |
| `Press 0 to exit...` / `Press any key to exit...` | 按 0 或其他键退出脚本 |

---

## 三种模式说明

### 冻结试用（推荐 — 选项 [2]）

- IDM 提供 30 天试用期，此选项将其锁定为永不过期
- 需要网络连接（用于触发 IDM 下载以创建注册表项）
- IDM 更新后无需重新操作
- **推荐大多数用户使用此选项**

### 激活（选项 [1]）

- 通过注册表锁定方式激活 IDM
- 需要网络连接
- 部分用户可能无效，会出现假序列号弹窗
- 如遇假序列号弹窗，请改用 **冻结试用** 选项

### 重置（选项 [3]）

- 清空所有激活/试用信息
- 当 IDM 提示假序列号或其他错误时可以使用
- 重置后可重新选择激活或冻结

---

## 无人值守模式（高级）

可通过命令行参数静默运行，不显示菜单：

| 参数 | 作用 |
|------|------|
| `/act` | 静默激活 |
| `/frz` | 静默冻结试用 |
| `/res` | 静默重置 |
| `-el` | 请求管理员权限 |
| `-qedit` | 禁用快速编辑模式 |

示例：`IAS.cmd /frz -el` 将以管理员权限静默冻结试用。

---

## 系统要求

- Windows 7 / 8 / 8.1 / 10 / 11 及对应的服务器版本
- PowerShell（系统自带即可）

---

## 常见问题

**Q: 运行脚本后没有任何反应？**  
A: 请右键点击 `IAS.cmd`，选择"以管理员身份运行"。

**Q: 提示 `Null service is not running`？**  
A: Windows 的 Null 服务未运行，按脚本提示访问帮助页面排查。

**Q: 提示 `PowerShell is not running in FullLanguage mode`？**  
A: PowerShell 被限制，请检查是否应用了 PowerShell 约束策略。

**Q: 更新 IDM 后需要重新操作吗？**  
A: 使用冻结试用模式一般不需要。如果出现弹窗，重新运行脚本即可。

**Q: 提示 `Unable to download files using IDM`？**  
A: 网络连接问题，请检查能否访问 `internetdownloadmanager.com`。

---

## 工作原理

IDM 在注册表中存储试用和激活相关的数据，部分键被系统锁定防止篡改。本脚本通过以下步骤实现：

1. 触发 IDM 下载，在注册表中生成必要的 CLSID 条目
2. 扫描并识别这些与激活/试用相关的注册表项
3. 获取权限并锁定这些键，使 IDM 无法读取和修改
4. IDM 因此无法判断试用是否过期，从而实现永久使用

---

## 许可证

MIT License — 详见 [LICENSE](LICENSE) 文件。
