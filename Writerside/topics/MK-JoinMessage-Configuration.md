# 配置

## 关于配置文件的位置
插件生成的配置文件夹名称与插件名称相同，其内会存有本插件的配置文件

插件的配置形式分为 SQLITE 与 YAML 两种形式，**其中 SQLITE 为默认配置形式**

若插件处于 SQLITE 模式时，你可能会在插件配置文件夹中发现名为 `data.db` 的文件，此为本插件的所有存储信息，**非必要不要对该文件进行修改或删除**

若插件处于 YAML 模式时，你将会在本插件的配置文件夹中发现两个配置文件，分别为 `config.yml` 和 `groups.yml`，**非必要不要删除这些文件**

## 关于配置文件
该栏仅适用于插件配置文件形式处于 YAML 模式状态，SQLITE 仅通过插件内置指令即可实现

<tabs>
    <tab title="config.yml">
        <code-block lang="yaml">
            # 检查更新
            check_update: false
            # 设置配置文件形式，可以更改为 SQLITE 以启用 SQLITE 配置模式
            config_type: YAML
            # 设置消息提示类型: 可选项 > CHAT | ACTIONBAR | BOSSBAR
            show_type: CHAT
            # 
        </code-block>
    </tab>
    <tab title="groups.yml">
        <b>可以设置多个组，但 default 组不要删除</b>
        <code-block lang="yaml">
            groups:
                # 该组为默认组，无法删除
                default:
                    # 优先级，值越大越优先采用
                    priority: 0
                    # 进服处在该组时发出的消息
                    join: "&7[&a+&7] &f{player}"
                    # 退服处在该组时发出的消息
                    exit: "&7[&4-&7] &f{player}"
                customGroup:
                    priority: 1
                    join: "&7[&a+&7] &f{player}"
                    exit: "&7[&4-&7] &f{player}"
                    # 在该组的用户，使用玩家名称存储
                    members: []
        </code-block>
    </tab>
</tabs>
