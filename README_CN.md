# Fiddler Everywhere 补丁（自动化版）
指导您在 Windows 系统上自动为 Fiddler Everywhere 打补丁。
> 父仓库：https://github.com/msojocs/fiddler-everywhere-enhance

## 特别说明：您也可以手动打补丁。请访问 [此仓库](https://github.com/sipsuru/fiddler-everywhere-patch-manual)

## 什么是补丁？如何使用？
这是一个适用于 Telerik Fiddler Everywhere 的补丁工具，可以为您提供永不过期的试用期，并解锁所有功能。  
以下是自动应用补丁的操作指南。

![无限试用期](https://github.com/user-attachments/assets/e9c83778-27fa-456a-96e6-07bb0cd7f4ad)

---

### 功能更新
> [!TIP]
> 补丁更新速度更快。
>  - 之前：2分25秒
>  - 现在：1分30秒

> [!TIP]
> 现已支持更改补丁服务器端口（用于解决端口冲突问题）。

> [!TIP]
> 现已支持为前端（FE）更改默认的虚拟用户配置（包括：电子邮箱、名字、姓氏、国家代码、提供商）。

---

> [!IMPORTANT]
> Linux 自动补丁现已支持！

> [!IMPORTANT]
> 现已支持 Mac ARM64 自动补丁。运行任一工作流时请选择 `Mac (arm64)`。

> [!NOTE]
> Windows ARM64 通过系统的 x64 仿真支持。请选择 `Windows (arm64)`；由于目前没有发布原生 ARM64 二进制文件，工作流会使用 x86_64 版本的 Fiddler 和补丁文件。

> [!WARNING]
> 新补丁需要向前端（FE）应用目录内写入文件，因此您需要在 Linux 系统中授予相应的写入权限。更多详情请参阅议题 #27。如果您有任何关于自动化该流程的建议，也欢迎随时提出。

> [!IMPORTANT]
> ### 更新通知：支持同步 Fork 与上游仓库：[阅读更多](#scheduled-syncing-forks-with-upstream-repo)

---

## 快速开始
> [!TIP]
> 您应始终检查您的 Fork 是否是最新的，以避免失败。（我们推荐您启用 [定时上游同步](#scheduled-syncing-forks-with-upstream-repo)）

* 自动化打补丁是如何工作的？
  - 该自动化补丁工具实现了与手动补丁相同的功能：它会下载 Fiddler Everywhere，解压缩、删除、替换、编辑、移动文件，最后生成已打补丁的应用程序。

* Workflow Dispatch 和 Workflow Dispatch Latest 有什么区别？
  - 最新版本 - Workflow Dispatch：补丁最新版本，并作为工作流工件上传。
  - 自定义版本 - Workflow Dispatch：允许您选择一个兼容的版本（5.9.0 及以上）进行补丁，并作为工作流工件上传。

> [!TIP]
> 我们强烈推荐您使用 **最新版本 - Workflow Dispatch**，以补丁最新可用版本。
> **自定义版本 - Workflow Dispatch** 同样支持从 5.9.0 及以上版本选择特定版本。

---

### 使用最新版本 - Workflow Dispatch 
[![](https://github.com/sipsuru/fiddler-everywhere-patch-automated/actions/workflows/cp__latest_dispatch.yml/badge.svg)](https://github.com/sipsuru/fiddler-everywhere-patch-automated/actions/workflows/cp__latest_dispatch.yml)

  - Fork 此仓库。
  - 打开 Actions 标签页，选择 Latest Version - Workflow Dispatch 工作流。
  - 使用 Workflow Dispatch 触发工作流。
  - 触发成功后，下载名为 `Fiddler-Everywhere-VX.X.X-Patched` 的工件。
  - 解压并运行。

  * *以下是操作示例...*

    https://github.com/user-attachments/assets/437c3448-1ea2-4c99-9123-e56b1665a37b

### 使用自定义版本 - Workflow Dispatch 
[![](https://github.com/sipsuru/fiddler-everywhere-patch-automated/actions/workflows/cp_dispatch.yml/badge.svg)](https://github.com/sipsuru/fiddler-everywhere-patch-automated/actions/workflows/cp_dispatch.yml)

  - Fork 此仓库。
  - 打开 Actions 标签页，选择 Custom Version - Workflow Dispatch 工作流。
  - 提供您想要补丁的版本号并触发 Workflow Dispatch。
  - 触发成功后，下载名为 `Fiddler-Everywhere-VX.X.X-Patched` 的工件。
  - 解压并运行。

  > [!WARNING]
  > 请注意，只有版本 5.9.0 及以上版本（5.9.0+）受支持。
  
  > 可在此处找到版本列表 - [版本历史](https://www.telerik.com/support/whats-new/fiddler-everywhere/release-history)

  * *以下是操作示例...*

    https://github.com/user-attachments/assets/1e9fa214-b9c9-469c-83f0-e5ae4527d2f7

---

### 定时同步 Fork 与上游仓库
FE Patch 1.0.8 增加了定时（默认每 6 小时）同步 Fork 与上游仓库的功能。
  > [!NOTE]
  > 感谢：[lobe-chat](https://github.com/lobehub/lobe-chat) & [ous50](https://github.com/ous50)

  > [!IMPORTANT]
  > - 要启用此上游同步操作，您需要启用 [Upstream Sync](.github/workflows/cp_pull_upstream.yml) GitHub Action。
  > - 如果同步失败，此操作会在您的 Fork 中创建一个 Issue。因此，您需要在仓库设置中启用 Issue 功能（设置 --> 常规 --> 功能：Issue）。
  > - 了解更多关于此操作的信息：[lobe-chat 同步功能 Wiki - 英文](https://github.com/lobehub/lobe-chat/wiki/Upstream-Sync) & [lobe-chat 同步功能 Wiki - 中文](https://github.com/lobehub/lobe-chat/wiki/Upstream-Sync.zh-CN)

  > [!TIP]
  > - 您可以通过编辑 [cp_pull_upstream.yml](.github/workflows/cp_pull_upstream.yml) 中的 `cron: '0 */6 * * *'` 更改同步计划。
  > - 了解更多关于 GitHub Actions 的调度计划，请访问 [GitHub 文档 - 调度操作](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows#schedule)

  > [!CAUTION]
  > - 如果您使用其他方法（例如 GitHub App）同步 Fork 与上游仓库（如：[Pull by Wei](https://github.com/wei/pull)），应禁用上游同步操作（操作路径：Actions --> Upstream Sync --> 右上角菜单 [...] --> 禁用工作流）。
  > - 了解更多关于禁用工作流的信息，请访问 [GitHub 文档 - 禁用和启用工作流](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/disabling-and-enabling-a-workflow)

---

> [!NOTE]
> 对于通用 Linux 和 MacOS 的操作说明，请使用 [源仓库](https://github.com/msojocs/fiddler-everywhere-enhance)

> [!CAUTION]
> 请不要将此补丁用于非法目的。如果可以，请支持官方：[支持官方](https://www.telerik.com/purchase/fiddler)
