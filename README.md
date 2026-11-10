# TimeScheduler

Windows 定时任务调度器的版本发布仓库。

> **这不是源码仓库。** 本仓库只存放编译好的可执行文件和自动更新所需的元数据。源码维护在独立的开发仓库中，不在此处。

---

## 关于

TimeScheduler 是一个便携式的 Windows 定时任务调度器：常驻托盘、按周/日/月/间隔等条件触发指定程序、记录调用历史、支持自动更新与版本回退。

本仓库承担两件事：

- **手动下载**：用户在这里取到任意历史版本的 `TimeScheduler.exe`
- **自动更新**：程序内置的更新器从这里拉取 `update.json` / `versions.json` / `version.json`，完成升级或降级

---

## 下载

### 方式一：直接下载（推荐给新用户）

进入 `time-scheduler/updates/stable/` 下对应版本目录，下载 `TimeScheduler.exe`。

最新稳定版通常是最高的版本号目录。下载后放到任意文件夹，双击运行即可，**无需安装、不写注册表**。

### 方式二：程序内自动更新（推荐给已安装用户）

已运行的 TimeScheduler 会按设置页配置的通道自动检查更新。也可以手动在「设置 → 软件更新」中：

- 点「检查更新」看是否有新版本
- 点「刷新版本列表」选择任意可用版本
- 点「安装所选版本」升级或降级

安装过程是事务性的：下载 → SHA256 校验 → 备份旧 exe 和配置 → 替换 → 启动新版本。任一步失败自动回滚，不会让程序变成打不开的状态。

---

## 仓库结构

```
time-scheduler/
└── updates/
    ├── stable/
    │   ├── update.json               # 指向当前最新稳定版
    │   ├── versions.json             # 列出所有可用稳定版
    │   └── v1.3.0/
    │       ├── version.json          # 该版本的元信息（sha256 / 下载地址 / 说明）
    │       └── TimeScheduler.exe     # 该版本的可执行文件
    └── beta/
        ├── update.json
        ├── versions.json
        └── v1.4.0-beta1/
            ├── version.json
            └── TimeScheduler.exe
```

| 文件 | 作用 |
|---|---|
| `update.json` | 启动时自动检查用，告诉客户端「最新版本是哪个」 |
| `versions.json` | 手动安装用，列出所有可选版本 |
| `version.json` | 每个版本的元信息：版本号、配置格式版本、SHA256、下载地址、更新说明 |
| `TimeScheduler.exe` | 该版本的可执行文件 |

`stable` 和 `beta` 是两个独立通道。客户端在设置页切换通道后，会请求对应目录下的文件。

---

## 版本说明

- **stable**：面向日常使用的正式版。字段稳定，不引入未验证的新功能。
- **beta**：预发布版，用于在新功能正式发布前试运行。可能有 bug，版本号带 `-betaN` 后缀（如 `1.4.0-beta1`）。

程序内置的版本号比较规则：`1.4.0-beta1 < 1.4.0-beta2 < 1.4.0`。beta 用户不会因为切回 stable 而被强制降级，stable 用户也不会误收到 beta 版本。

---

## 版本历史

每个 `v{version}/version.json` 里有一条 `notes` 字段，记录该版本最值得说的 1–3 条变更，程序内「软件更新」卡片会显示这段文字。

完整变更记录维护在开发仓库的 `CHANGELOG.md` 中，不在此仓库重复。

---

## 源码

源码维护在独立的开发仓库，不在此处公开。

本仓库只接收构建产物，不接受 Pull Request。

---

## 许可

本项目采用 Apache License 2.0，详见 [LICENSE](LICENSE)。
