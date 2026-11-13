# Maa4Linux

MaaAssistantArknights 的 Linux 原生桌面客户端。用 Rust + GTK4 + libadwaita 重写用户界面，直接驱动上游的自动化引擎，不包含任何游戏逻辑。

> **状态：v1 规格已确认，尚未实现。** 现在克隆下来还没有可运行的程序。

## 它是什么

- 一个**客户端**：调用上游引擎的冻结 C 接口，把它的状态与截图渲染成原生界面。
- **行为对齐**上游 `v6.22.0` 的 WPF GUI：任务队列（13 张任务卡）、自动战斗、设置、日志与截图。
- **资源跟随游戏**：引擎与客户端钉在 `v6.22.0`，游戏数据可以独立更新到最新，新活动当天就能用。

## 它不是什么

- 不是引擎的重写，也不是上游的分支。
- 不是 Wine 包装，不需要 .NET 运行时。
- 不包含 Windows 专属功能（窗口捕获、模拟器外部渲染器、注册表自启动等）。

## 文档

- [v1 规格](docs/v1-spec.md)：范围、非目标、实现决定、验收标准
- [术语表](GLOSSARY.md)
- [架构决定](docs/adr/)
- [与上游的关系](docs/upstream.md)
- [参与贡献](CONTRIBUTING.md)

## 许可

AGPL-3.0，与上游一致。引擎与游戏资源的版权归上游及其贡献者。

---

## English

A native Linux desktop client for MaaAssistantArknights, written in Rust with GTK4 and libadwaita. It reimplements the user-facing client only: the automation engine stays an external, pinned dependency, and game resources are updated independently of the client.

Status: v1 spec agreed, implementation not started. See [docs/v1-spec.md](docs/v1-spec.md).
