# 战斗index

战斗index是本引擎脚本里代表一场战斗对象的整数句柄：

- 战斗对象

战斗index底层是战斗管理器中分配的一个稳定索引。脚本通过它调用 `Battle.*` 接口，读取或修改这场战斗在服务端内存中保存的数据（回合、参战双方、战场属性等），也可以结合其它开放的接口对这场战斗进行操作。[Battle.PVE](../battle/PVE.md)、Battle.PVP、Battle.Encount、Battle.JoinBattle 等创建/加入战斗的接口，成功时返回的就是这个战斗index。
