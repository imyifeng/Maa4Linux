# 参与贡献

先读三份背景材料，再动手：

- [GLOSSARY.md](../GLOSSARY.md)：本项目使用的术语（客户端、引擎、任务链、资源覆盖层……），请沿用而不是发明同义词。
- [docs/adr/](../docs/adr/)：已经做过的、代价较高的决定。改动若与之冲突，请在 issue 里明确指出冲突，而不是默默改掉。
- [docs/v1-spec.md](../docs/v1-spec.md)：v1 的范围、非目标与验收标准。

## 环境准备

- Rust stable（跟随仓库的 `rust-toolchain.toml`）
- GTK4 与 libadwaita 开发文件、`pkg-config`、`blueprint-compiler`
- 可选：系统 `adb`（不装也能用内置 ADB 实现）
- 可选：Waydroid 或 AVD（只有跑真实任务时需要）

引擎二进制与基础资源**不进版本库**，由构建脚本按版本清单拉取并校验；不要手工把它们提交上来。

## 常用命令

```bash
cargo xtask fetch-engine     # 拉取并校验引擎与基础资源
cargo run -p maa4linux-ui    # 启动界面（无需设备）
cargo test --workspace       # 单元测试
cargo xtask test-ui          # 无头合成器下的界面冒烟
cargo xtask test-engine      # 真实引擎的握手测试（无需设备）
cargo xtask appimage         # 打 AppImage
```

## 提交

- 提交信息使用 Conventional Commits（`feat:`、`fix:`、`docs:`、`chore:`……），描述可以用中文或英文。
- 每个提交必须带 DCO 签名：`git commit -s`。本项目不使用 CLA。
- 一个提交只做一件事；格式化与 lint 在提交前跑过（`cargo fmt`、`cargo clippy`）。

## 不能做的事

- 在引擎集成 crate 之外写 `unsafe`。
- 在界面里硬编码引擎、资源或客户端的版本号；版本只从版本清单读取。
- 手写界面文案；文案从上游语言文件生成，键名保持一致。
- 把模板、模型或资源包提交进仓库。
- 修改引擎源码来迁就界面。

## 报问题

在本仓库提 issue，不要提到上游。请附上"关于"页里显示的四个版本（客户端、引擎、基础资源、资源覆盖层）与日志导出。
