# MuPacket API

**在 MK-ServerLauncher 中，HTTP 和 WebSocket 中传输的消息皆为由 MuPacket API & MuPacketAPI4TS 转换而来的 JSON 消息**

**在 MuPacketAPI 中，其本质为 `MuPacket` 及其子类，由 `JsonObject` 为信息载体**

## 消息结构

### 示例
```JSON5
{
  "MP_ID": "x.x:x",
  "MP_DATA": {
    // 动态内容, 根据不同 MP_ID 提供不同内容
  },
  "TSS": 1145141919810 // 是一个 Long 类型时间戳，用于标记创建时间（注意是创建时间）
}
```

### MuPacket ID {id="mupacket-id_1"}

MuPacket ID 由类ID与操作名组合而来，形如 `类ID:操作名`

#### MuPacket ID 目录

| MuPacket ID                       | Description                                                |
|-----------------------------------|------------------------------------------------------------|
| mucore.internal:overiview         | Overview 包，用于提供 MuCore 提供者信息，CPU & MEM 仪表数据及 MuServer 统计数据 |
| mucore.internal:msg               | 带状态的消息包（由 MuCore 发送的）                                      |
| mucore.internal:status            | 状态包，仅传送一个状态（INFO, OK, WARN, ERROR, TIP）                    |
| mucore.config:all                 | 返回 MuCore 设置项的包                                            |
| mucore.muserver:status            | 状态包，传送服务器的当前状态                                             |
| mucore.muserver.console:log       | 日志包，传送目标服务器日志                                              |
| mucore.muserver:playerlist        | 用于返回指定 MuServer 中的玩家列表                                     |
| mucore.muserver.config:list       | 用于返回指定 MuServer 中的设置                                       |
| muview.muserver.config:modify     | 在 MuView 中修改指定 MuServer 中的设置时传送的包                          |
| muview.muserver.config:add        | 在 MuView 中添加指定 MuServer 中的设置时传送的包                          |
| muview.muserver.config:del        | 在 MuView 中删除指定 MuServer 中的设置时传送的包                          |
| muview.muserver:create            | 在 MuView 中创建 MuServer 时传送的包                                |
| muview.muserver:modify            | 在 MuView 中更改 MuServer 设置时传送的包                              |
| muview.muserver:remove            | 在 MuView 中删除 MuServer 时传送的包                                |
| muview.muserver:start             | 在 MuView 中启动指定的 MuServer 时传送的包                             |
| muview.muserver:restart           | 在 MuView 中重启指定的 MuServer 时传送的包                             |
| muview.muserver:stop              | 在 MuView 中停止指定的 MuServer 时传送的包                             |
| muview.muserver.console:send      | 在 MuView 中向指定 MuServer 发送指令                                |
| muview.muserver.console:kick      | 在 MuView 中向指定 MuServer 快速踢出指定玩家                            |
| muview.muserver.console:msg       | 在 MuView 中向指定 MuServer 快速发送消息给指定玩家                         |
| muview.muserver.console:broadcast | 在 MuView 中向指定 MuServer 快速发送广播消息                            |
| muview.muenv:create               | 在 MuView 中创建 MuEnv 时传送的包                                   |
| muview.muenv:remove               | 在 MuView 中移除 MuEnv 时传送的包                                   |
| muview.config:modify              | 在 MuView 中更改 MuCore 设置项时传送的包                               |

### MuPacket Data {id="mupacket-data_1"}

MuPacket Data 是由 MuPacket 实现者自行约定的结构，无论结构如何变化，其本质仍是一个 `JsonObject`(MuPacket API) 和 `object/{}`(MuPacketAPI4TS)

#### MuPacket Data 结构一览表

***以 [MuPacket ID 目录](#mupacket-id_1) 顺序排列***