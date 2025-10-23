# MiniTB - ThingsBoard核心数据流学习项目

## 📚 项目说明

`minitb` 是ThingsBoard核心数据流的简化教学实现，已作为Git Submodule集成到本项目中。

## 🔗 仓库信息

- **独立仓库**: https://github.com/caochun/minitb
- **本地路径**: `thingsboard/minitb/`
- **提交ID**: `3a91845`

## 🎯 核心数据流

```
设备 → MQTT传输层 → TransportService → TbMsg → Rule Engine → 数据存储
```

**代码对比：**
- MiniTB: ~1000行 (16个Java文件)
- ThingsBoard: ~100,000行 (数千个文件)

## 📂 快速开始

### 查看MiniTB代码
```bash
cd minitb
cat README.md
```

### 文件结构
```bash
cd minitb
tree -L 3
```

### 核心文件对比

| MiniTB | ThingsBoard | 说明 |
|--------|-------------|------|
| `minitb/src/main/java/com/minitb/common/msg/TbMsg.java` | `common/message/src/main/java/org/thingsboard/server/common/msg/TbMsg.java` | 核心消息对象 |
| `minitb/src/main/java/com/minitb/transport/service/TransportService.java` | `common/transport/transport-api/src/main/java/org/thingsboard/server/common/transport/service/DefaultTransportService.java` | 传输服务 |
| `minitb/src/main/java/com/minitb/ruleengine/RuleEngineService.java` | `application/src/main/java/org/thingsboard/server/actors/ruleChain/RuleChainActorMessageProcessor.java` | 规则引擎 |
| `minitb/src/main/java/com/minitb/transport/mqtt/MqttTransportHandler.java` | `common/transport/mqtt/src/main/java/org/thingsboard/server/transport/mqtt/MqttTransportHandler.java` | MQTT处理器 |

## 🎓 学习路径

### 第1步：理解简化版 (MiniTB)
```bash
cd minitb
# 阅读文档
cat README.md
cat FLOW.txt

# 查看核心代码
cat src/main/java/com/minitb/common/msg/TbMsg.java
cat src/main/java/com/minitb/transport/service/TransportService.java
```

### 第2步：对比完整版 (ThingsBoard)
```bash
cd ..
# 对比核心消息对象
diff minitb/src/main/java/com/minitb/common/msg/TbMsg.java \
     common/message/src/main/java/org/thingsboard/server/common/msg/TbMsg.java

# 对比传输服务
diff minitb/src/main/java/com/minitb/transport/service/TransportService.java \
     common/transport/transport-api/src/main/java/org/thingsboard/server/common/transport/service/DefaultTransportService.java
```

### 第3步：深入理解
- 理解为什么ThingsBoard使用Actor模型
- 理解为什么需要消息队列(Kafka)
- 理解分布式架构的设计

## 🔄 Git Submodule 管理

### 克隆ThingsBoard（包含MiniTB）
```bash
git clone --recursive git@github.com:thingsboard/thingsboard.git
```

### 单独更新MiniTB
```bash
cd thingsboard/minitb
git pull origin main
```

### 在ThingsBoard中提交MiniTB的更新
```bash
cd thingsboard
git add minitb
git commit -m "Update minitb submodule"
```

## 📊 核心概念对比

| 概念 | MiniTB实现 | ThingsBoard实现 |
|------|-----------|----------------|
| **消息传递** | 直接方法调用 | Kafka消息队列 |
| **并发处理** | ExecutorService线程池 | Actor模型 (TenantActor → RuleChainActor) |
| **规则链路由** | if-else选择 | 基于关系类型路由 (Success/Failure/Other) |
| **数据存储** | 内存Map + 文件 | Cassandra/PostgreSQL + Redis缓存 |
| **集群支持** | 单机 | 分布式集群，水平扩展 |

## 💡 关键收获

通过MiniTB学习，您将理解：

1. ✅ **物联网平台的核心数据流**是如何工作的
2. ✅ **TbMsg消息对象**是整个系统的血液
3. ✅ **规则引擎**提供了灵活的业务逻辑处理能力
4. ✅ **分层架构**使系统易于维护和扩展
5. ✅ **为什么生产环境需要Actor模型和消息队列**

## 📖 相关资源

- [MiniTB仓库](https://github.com/caochun/minitb)
- [ThingsBoard官方文档](https://thingsboard.io/docs/)
- [ThingsBoard GitHub](https://github.com/thingsboard/thingsboard)

---

**从简单到复杂，从原理到实践，MiniTB是理解ThingsBoard的最佳起点！**


