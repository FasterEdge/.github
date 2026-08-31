<div align="center">
<img src="https://avatars.githubusercontent.com/u/245985800?s=200&v=4" style="width:100px;" width="100"/>
<h2>FasterEdge：对称、可靠、安全的多场景边缘计算框架</h2>
</div>

<div align="center">
<img src="../images/concept.png" style="width:96%;" width="100"/>
</div>

### 概念
- 这是一个灵活且对称的云边合作库，各端（当然可以不分云边）运行时可具备的 Ability 与 Data 由您指定
- 对称性决定了系统的简单性和易于理解性，这将会方便您快速入门或投入应用，更是为了降低您评估的门槛
- 一般将支持常规指令集架构下的一切操作系统（主语言为 Golang），对于单片机等设备会有专用版进行兼容
- 本项目也将不断兼容其他云边合作框架和基本设施，实现统一操作流程或作为拓展使用
- 此体系下的算法将支持原生运行、进程管理器高可用运行、容器运行、pod 监管运行等

### 当前版本快照
- 文档与近期 MCU / FPGA / RelayNode 工程快照：`1.0.20260831`
- 各软件组件的运行版本以对应源码仓库中的版本常量和发布标签为准

### 核心仓库
- **[FasterEdge](https://github.com/FasterEdge/FasterEdge)**：框架主仓库，Atom / Ability / Data / Command / Transport 模型，完整 Go 单测覆盖，`go test ./...` 通过
- **[FasterEdge/B2C](https://github.com/FasterEdge/B2C)**：超轻量物联网边缘流式分析引擎（LF Edge eKuiper 增强分支），SQL/Graph 规则、REST/CLI/K8s 管理、Golang/Python 扩展、MQTT v5 请求响应闭环
- **[FasterEdge/DontCrack4OpenHarmonyLinuxKernelSide](https://github.com/FasterEdge/DontCrack4OpenHarmonyLinuxKernelSide)**：开源鸿蒙 Linux 内核侧进程管理器
- **[FasterEdge/DontCrack4AndroidLinuxKernelSide](https://github.com/FasterEdge/DontCrack4AndroidLinuxKernelSide)**：Android adb ELF 进程管理器
- **[FasterEdge/DontCrack4ManyLinux](https://github.com/FasterEdge/DontCrack4ManyLinux)**：通用 Linux 进程管理器（含 `/healthz` `/metrics` Prometheus 端点）
- **[FasterEdge/DontCrack4Windows](https://github.com/FasterEdge/DontCrack4Windows)**：Windows PE 进程管理器（含 Web UI 控制台）

### Ability（已实现）
| 名称 | 类别 | 关键命令 |
|---|---|---|
| `BaseAbility` | 基础 | `list_data_names` / `list_ability_names` |
| `RoleAbility` | 基础 | `describe` / `set_role` / `get_role` |
| `TimeAbility` | 基础 | `sync_manual` / `sync_system` / `sync_net` / `sync_ntp` / `get_time` / `configure_run` |
| `NetMapAbility` | 基础 | `register_peer` / `unregister_peer` / `update_peer` / `list_peers` / `lookup_peer` / `get_topology` |
| `OneKeyAbility` | 基础 | `issue_token` / `verify_token` / `revoke_token` / `revoke_all` / `list_tokens` / `status` / `rotate`（HMAC-SHA256）|
| `CloudRoleAbility` | 基础 | `describe` / `set_controller` / `register_service` / `set_status` / `heartbeat` |
| `EdgeRoleAbility` | 基础 | `describe` / `set_zone` / `add_capability` / `record_latency` / `get_metrics` / `set_online` |
| `CmdAbility` | 终端 | `run` / `start` / `wait` / `kill` / `list` / `set_allowlist` |
| `ShAbility` | 终端 | `run` / `start` / `wait` / `kill` / `list`（`sh -c` 形式）|
| `BashAbility` | 终端 | `run` / `start` / `wait` / `kill` / `list`（`bash --noprofile --norc -c` 形式）|
| `ConfigFileAbility` | 文件/配置 | `set_path` / `load` / `save` / `exists` |
| `FileTransferAbility` | 文件/配置 | `set_target` / `upload` / `download` / `list` / `get_transfer` / `cancel` |
| `AlgorithmDistributionAbility` | 文件/配置 | `register_algorithm` / `unregister_algorithm` / `distribute` / `list_distributions` / `cancel` |
| `ModbusAbility` | 工业协议 | `set_endpoint` / `set_unit_id` / `read_*` / `write_*` |
| `SerialAbility` | 工业协议 | `open` / `close` / `read` / `write` / `set_config` / `list_ports` |
| `TSNAbility` | 工业协议 | `set_interface` / `register_talker` / `register_listener` / `unregister` / `set_priority_map` |
| `MQTTAbility` | 数据交互 | `set_broker` / `connect` / `disconnect` / `publish` / `subscribe` / `drain` / `list_subscriptions` |
| `InfluxDBAbility` | 数据交互 | `set_endpoint` / `set_token` / `set_org` / `set_bucket` / `ping` / `write` / `query` / `list_series` |
| `EKuiperAbility` | 数据交互 | `set_endpoint` / `create_stream` / `drop_stream` / `create_rule` / `start_rule` / `stop_rule` |
| `DockerAbility` | 容器编排 | `set_endpoint` / `list_containers` / `start` / `stop` / `restart` / `remove` / `pull_image` / `inspect` / `get_logs` / `create` |
| `KubernetesAbility` | 容器编排 | `set_context` / `apply` / `delete` / `list` / `get` / `scale` / `get_logs` |

依赖外部网络/进程的能力（FileTransfer / Modbus / Serial / MQTT / InfluxDB / EKuiper / Docker / Kubernetes）均通过 `SetXxxTransport(...)` 注入，框架本身只管理元数据与生命周期。

### Data（已实现）
| 名称 | 功能 | 关键命令 |
|---|---|---|
| `BaseData` | 框架元信息（logo、版本）| `logo` / `info` |
| `NetMapData` | 本节点网络拓扑 | `info` / `set_node_name` / `interfaces` / `set_default_iface` |
| `KeyringData` | 共享密钥与令牌表 | `status` / `set_secret` / `rotate` / `issue_token` / `revoke_*` |
| `ConfigData` | 扁平点号路径 KV 配置 | `get` / `set` / `delete` / `list` / `snapshot` |

### 组件群（外置可选项）
| 名称 | 仓库 |
|---|---|
| **DontCrack 进程管理器**（进程可用性保证，含自动重启、健康探针、`/healthz` `/metrics` Prometheus 端点、Web UI 控制台）| [OpenHarmony 版](https://github.com/FasterEdge/DontCrack4OpenHarmonyLinuxKernelSide) · [Android 版](https://github.com/FasterEdge/DontCrack4AndroidLinuxKernelSide) · [manylinux 版](https://github.com/FasterEdge/DontCrack4ManyLinux) · [Windows 版](https://github.com/FasterEdge/DontCrack4Windows) |
| **MqttBroker**（轻量级 MQTT 服务，MQTT 3.1.1/5.0、QoS 0/1/2、内置 WebUI，管理端口 11883）| [MqttBroker](https://github.com/FasterEdge/MqttBroker) · [MqttBrokerCore](https://github.com/FasterEdge/MqttBrokerCore) |
| **SimpleWebShell**（加密 WebShell）| [仓库](https://github.com/FasterEdge/SimpleWebShell) |
| **SimpleTimeService**（轻量 NTP 时间服务）| [仓库](https://github.com/FasterEdge/SimpleTimeService) |
| **TsnHub**（软 TSN 网络加速中枢）| [仓库](https://github.com/FasterEdge/TsnHub) |
| **NetMap**（网络拓扑管理器，Web 前端实时渲染 FasterEdge 节点拓扑）| [仓库](https://github.com/FasterEdge/NetMap) |
| **ProxyArea**（纯 Go 标准库 REST 兼容 HTTP 转发器）| [仓库](https://github.com/FasterEdge/ProxyArea) |
| **ModelTranslator**（多格式模型转换工具，uv 环境 + 依赖按需拉取）| [仓库](https://github.com/FasterEdge/ModelTranslator) |
| **ModelRunntime**（多语言多格式模型推理运行时示例集）| [仓库](https://github.com/FasterEdge/ModelRunntime) |
| **Archs**（FasterEdge 组件平台/处理器架构兼容性说明）| [仓库](https://github.com/FasterEdge/Archs) |
| **FasterEdgeDoctor**（本地/远程仓库和运行状态诊断，支持只读 HTTP 与 OneKey 检查）| [仓库](https://github.com/FasterEdge/FasterEdgeDoctor) |
| **MCU / FPGA 移植**（Arduino、PlatformIO、Keil、MounRiver、Vivado、MicroBlaze、Vitis HLS 等）| [组织仓库](https://github.com/FasterEdge) |
| **RelayNode**（SW2MQTT、SW2USB 硬件节点与 EDA 工程）| [组织仓库](https://github.com/FasterEdge) |
| **Example**（跨能力组合示例集合）| [仓库](https://github.com/FasterEdge/Example) |

### 灵活使用
> 此体系使用方式十分灵活，您习惯或者方便怎么做都可以，各种方式也可以顺利组合
- 终端 Ability + 直接可执行程序：算法下发原生运行时，发挥系统原生性能与板载驱动
- 终端 Ability + **DontCrack 进程管理器**：发挥系统原生性能与板载驱动同时直接支持自动重启和自我检查
- DockerAbility：容器化便捷打包部署
- KubernetesAbility：容器化且在 K8s 集群中打包部署
- 只用 Ability：使用 Ability 自带功能实现状态与信息上报

### 设计哲学
- 依赖抽象而不依赖具体（Depend on Abstractions, Not on Concrete Implementations.）
- 遵循策略模式（Strategy Pattern）、命令模式（Command Pattern）、组合模式（Composite Pattern）
- 所有命令参数为严格类型，任何 nil / 类型不匹配 / 空白值都会返回 `types.ErrInvalidArguments`
- 内部状态全部受 `sync.RWMutex` / `atomic` 保护，`-race` 干净
- 涉及外部网络的 Ability 默认拒绝 `localhost` / `127.0.0.1` / `0.0.0.0` / `::1`，降低 SSRF 风险

### 其他说明
- 我们将使用简体中文作为系统的主操作语言，同时我们希望为国产云边合作技术体系出一份微薄之力
- 系统将提供 AI 易于阅读和理解的文档和示例（知识库）以便用户进一步降低理解和使用难度
- 本项目由大连理工大学"泛在网络与智能感知实验室"孵化支持
- 开源项目天然具备用户对代码知根知底的底色，如果您希望将此框架使用在重要场合，可先对代码进行评审
- 您如果想关注此项目，可以在项目的 Github 主页或 Gitee 主页点击订阅按钮，这是对我们最好的支持
