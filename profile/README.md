<div align="center">
<img src="https://avatars.githubusercontent.com/u/245985800?s=200&v=4" style="width:100px;" width="100"/>
<h2>FasterEdge：对称、可靠、安全的多场景边缘计算框架</h2>
</div>

### 概念
- 这是一个灵活且对称的云边合作库，各端（当然可以不分云边）运行时可具备的Ability与Data由您指定
- 对称性决定了系统的简单性和易于理解性，这将会方便您快速入门或投入应用，更是为了降低您评估的门槛
- 一般将支持常规指令集架构下的一切操作系统（主语言为Golang），对于单片机等设备会有专用版进行兼容
- 本项目也将不断兼容其他云边合作框架和基本设施，实现统一操作流程或作为拓展使用
- 此体系下的算法将支持原生运行、进程管理器高可用运行、容器运行、pod监管运行等

### Ability
> Ability即是当前节点具备的能力，需要以BaseAbility作为“模板约束”实现，当然用户也可以根据“模板约束”去设计任何自己想要的能力，有些Ability需要具备前提条件，前提可以为Data或Ability
- BaseAbility（Ability模板约束）【未公开】
- NetMapAbility（网络拓扑能力）【未公开】
- OneKeyAbility（节点加密访问能力）【未公开】
- RoleAbility（节点角色能力）【未公开】
- CloudRoleAbility（云侧节点能力）【未公开】
- EdgeRoleAbility（边策节点能力）【未公开】
- CmdAbility（Cmd终端能力）【未公开】
- ShAbility （SH终端能力）【未公开】
- BashAbility（Bash终端能力）【未公开】
- DockerAbility（非侵入式Docker控制能力）【未公开】
- KubernetesAbility（非侵入式k8s控制能力）【未公开】
- DontCrackAbility（DontCrack进程管理器控制能力）【未公开】
- MQTTAbility（连接与监听MQTT Broker的能力）【未公开】
- EKuiperAbility（与eKuiper交互的能力）【未公开】
- InfluxDBAbility（与InfluxDB交互的能力）【未公开】
- SerialAbility（常规串口通信的能力）【未公开】
- ModbusAbility（直接接入Modbus的能力）【未公开】
- TSNAbility（软TSN网络加速的能力）【未公开】
- FileTransferAbility（文件传输能力）【未公开】
- ConfigFileAbility（配置文件管理能力）【未公开】

### Data
> Data即是当前节点存储的数据，需要以BaseData作为“模板约束”实现，当然用户也可以根据“模板约束”去设计任何自己想要的数据，有些Data需要具备前提条件，前提可以为Data或Ability
- BaseData（Data模板约束）【未公开】
- SelfNetData（自我网络状态数据）【未公开】
- AddressTableData（寻址表数据）【未公开】
- TreeMapData（树状拓扑数据）【未公开】
- TagData（节点标签数据）【未公开】

### 组件群（外置可选项）
> 这些是作为外部配套组件存在的程序，您可以在FasterEdge选用他们，也可以单独使用
- DontCrack进程管理器（进程可用性保证组件）【[OpenHarmony版](https://github.com/FasterEdge/DontCrack4OpenHarmonyLinuxKernelSide)】
- SimpleWebShell（加密WebShell）【未公开】

### 灵活使用
> 此体系使用方式十分灵活，您习惯或者方面怎么做都可以，各种方式也可以顺利组合
- 终端Ability + 直接可执行程序：算法下发原生运行时，发挥系统原生性能与板载驱动
- 终端Ability + 进程管理器：发挥系统原生性能与板载驱动同时直接支持自动重启和自我检查
- DockerAbility：容器化便捷打包部署
- KubernetesAbility：容器化且在K8s集群中打包部署
- 只用Ability：使用Ability自带功能实现状态与信息上报

### 设计与编译
```
We are building...
```

### 其他说明
- 我们将使用简体中文作为系统的主操作语言，同时我们希望为国产云边合作技术体系出一份微薄之力
- 系统将提供AI易于阅读和理解的文档和示例（知识库）以便用户进一步降低理解和使用难度
- 本项目由大连理工大学“泛在网络与智能感知实验室”孵化支持
- 开源项目天然具备用户对代码知根知底的底色，如果您希望将此框架使用在重要场合，可先对代码进行评审
- 您如果想关注此项目，可以在项目的Github主页或Gitee主页点击订阅按钮，这是对我们最好的支持
