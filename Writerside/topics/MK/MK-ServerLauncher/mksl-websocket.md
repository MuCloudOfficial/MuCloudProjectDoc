# MuPacket API

在 MK-ServerLauncher 中，HTTP 和 WebSocket 中传输的消息皆为由 MuPacket API & MuPacketAPI4TS 转换而来的 JSON 消息

**在 MuPacketAPI 中，其本质为 `MuPacket` 及其子类，由 JSON 为信息载体**

## 消息结构

### 示例
```JSON5
{
  "MP_ID": "x.x:x", // MuPacket ID
  "MP_DATA": {
    // 动态内容, 根据不同 MP_ID 提供不同内容
  },
  "CID": 1145141919810 // 是一个 Long 类型长数字，这指代了该 MuPacket 的唯一标识
}
```

### MuPacket ID {id="mupacket-id_1"}

MuPacket ID 由类ID与操作名组合而来，形如 `类ID:操作名`

### MuPacket Data {id="mupacket-data_1"}

MuPacket Data 是由 MuPacket 实现者自行约定的结构  
无论结构如何变化，其本质仍是一个 `JsonObject`(MuPacket API) 或 `object`(MuPacketAPI4TS)

## MuPacket ID 目录 (MuCore)

| MuPacket ID                | Description                                                                   |
|----------------------------|-------------------------------------------------------------------------------|
| mucore.internal:msg        | 带状态的消息包                                                                |
| mucore.internal.config:all | 带有 MuCore 所有设置项的包                                                    |
| mucore.muserver:info       | 带有指定 MS_ID 的服务器信息（MuServerInfo）和服务器状态（MuServerStatus）的包 |
| mucore.muserver:list       | 用于返回所有服务器                                                            |
| mucore.muserver:status     | 状态包，传送服务器的当前状态                                                  |
| mucore.muenv:info          | 带有环境信息的包                                                              |
| mucore.muenv:list          | 用于返回所有的环境                                                            |


## MuPacket ID 目录 (MuView)

| MuPacket ID            | Description                       |
|------------------------|-----------------------------------|
| muview.muserver:create | 用于传送创建服务器请求的包        |
| muview.muserver:import | 用于传送引入服务器请求的包        |
| muview.muenv:create    | 在 MuView 中创建 MuEnv 时传送的包 |


## MuPacket Data 结构一览表

***以 [MuPacket ID 目录](#mupacket-id_1) 顺序排列***

### mucore.internal:msg
```TYPESCRIPT
{
    // 该消息的类型，这会影响在 MuView-FrontView 中 Toast 消息的表现
    type: "OK" | "TIP" | "WARN" | "ERR" | "INFO"
    
    // 消息文本
    msg: string
}
```

### mucore.internal.config:all
```TYPESCRIPT
{
    // 尚未实现
}
```

### mucore.muserver:info
```typescript
{
    // 服务器 ID，这通常是一个 8 位字符串
    // 如非特别指定，这通常是以符合该正则 [A-Z0-9]{,8} 生成的随机字符串
    // 这通常是唯一值
    MS_ID: string
    MS_OP: {
        // 服务器名称（请注意这与服务器 ID 不是同一概念）
        name: string
        // 服务器的描述
        desc: string
        // 服务器的版本（是指该服务器的 Minecraft 版本）
        version: string
        // 服务器的类型（例如该服务器是 Paper 核心，那么服务器的类型即为 "paper"）
        type: string
        // 服务器所使用的环境名
        env: string
        // 服务器当前的状态，以数字标识
        // 0 -> 正在创建
        // 1 -> 已停止
        // 2 -> 服务器正在执行启动前任务（MuTask）中
        // 3 -> 正在运行
        // 4 -> 正在停止
        // 5 -> 重新启动中
        // 6 -> 遇错重启中
        // 7 -> 服务器连续报告了错误，被强行停止
        status: number
    }
}
```

### mucore.muserver:list
```TypeScript
[
    {
        // 服务器名称（请注意这与服务器 ID 不是同一概念）
        name: string,
        // 服务器的描述
        desc: string,
        // 服务器的版本（是指该服务器的 Minecraft 版本）
        version: string,
        // 服务器的类型（例如该服务器是 Paper 核心，那么服务器的类型即为 "paper"）
        type: string,
        // 服务器所使用的环境名
        env: string,
        // 服务器当前的状态，以数字标识
        // 0 -> 正在创建
        // 1 -> 已停止
        // 2 -> 服务器正在执行启动前任务（MuTask）中
        // 3 -> 正在运行
        // 4 -> 正在停止
        // 5 -> 重新启动中
        // 6 -> 遇错重启中
        // 7 -> 服务器连续报告了错误，被强行停止
        status: number
    }
]
```

### mucore.muserver:status
```TypeScript
{
    // 服务器 ID，这通常是一个 8 位字符串
    // 如非特别指定，这通常是以符合该正则 [A-Z0-9]{,8} 生成的随机字符串
    // 这通常是唯一值
    MS_ID: string

    // 服务器当前的状态，以数字标识
    // 0 -> 正在创建
    // 1 -> 已停止
    // 2 -> 服务器正在执行启动前任务（MuTask）中
    // 3 -> 正在运行
    // 4 -> 正在停止
    // 5 -> 重新启动中
    // 6 -> 遇错重启中
    // 7 -> 服务器连续报告了错误，被强行停止
    MS_OP: number
}
```