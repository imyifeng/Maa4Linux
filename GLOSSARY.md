# Maa4Linux

MaaAssistantArknights 的 Linux 原生桌面客户端：用 Rust 与 GTK4 重写用户界面，把自动化引擎作为外部依赖驱动。本文件只放术语，不放实现细节或计划。

## Language

### 组件与来源

**Engine**（引擎）:
无界面的自动化运行时（MaaCore），负责识别与控制。在本项目中是外部依赖，通过冻结的 C 接口使用。
_Avoid_: core、后端、服务端

**Client**（客户端）:
本项目交付的桌面应用。它驱动引擎并呈现其状态，自身不含任何自动化逻辑。
_Avoid_: GUI、前端、外壳、包装

**Controlled device**（受控端）:
被自动化的 Android 实例：模拟器、Waydroid 或 redroid 这类容器，或通过 ADB 访问的真机。
_Avoid_: 目标机、模拟器、手机

**Resource**（资源）:
游戏侧数据资产：关卡与干员物品数据、模板图、ONNX 模型、任务图。
_Avoid_: 素材、资源包、数据文件

**Resource overlay**（资源覆盖层）:
独立于任何客户端版本发布的资源增量，只包含跟随游戏变化、与引擎版本无关的数据。它叠加在 Resource 之上。
_Avoid_: 补丁、热更新包、更新包

**Region**（区服）:
玩家所在的游戏服务器（Official、Bilibili、YoStarEN、YoStarJP、YoStarKR、txwy）。它决定加载哪一层区服资源。
_Avoid_: client type、服务器、区域

### 执行模型

**Task type**（任务类型）:
引擎接受的任务种类，用固定字符串标识，例如 `Fight`、`Roguelike`。
_Avoid_: 任务名、模式、作业

**Task chain**（任务链）:
提交给引擎的一个完整单元，执行完才轮到下一个。
_Avoid_: 任务、批次

**Task queue**（任务队列）:
用户排好序、由客户端逐条下发的任务卡序列。
_Avoid_: 任务列表、计划、日程

**Task card**（任务卡）:
任务队列中的一张卡片，对应一个任务类型及其参数。
_Avoid_: 任务项、任务块

**Tool task**（工具任务）:
只在客户端存在的伪任务（公招识别、仓库识别、抽卡统计等），引擎没有对应的任务类型。
_Avoid_: 工具、小工具、辅助任务

**Connection**（连接）:
到达受控端所需的配置：ADB 实现、ADB 路径、地址、连接预设。
_Avoid_: 设备、模拟器、目标

**Connection preset**（连接预设）:
上游 `config.json` 里的一组 ADB 命令模板，例如 Waydroid、AVD。
_Avoid_: 配置模板、连接方案

**Engine event**（引擎事件）:
引擎推给客户端的一条 JSON 消息，由消息编号与 `what` 字符串标识。
_Avoid_: 通知、日志、信号、回调

**Profile**（配置档）:
一整套用户配置：一条任务队列加一组设置。
_Avoid_: 配置、方案、账号
