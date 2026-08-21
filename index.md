<!-- Generated. DO NOT EDIT. -->
# hourglass-gmsv Lua 脚本引擎

本文档是 hourglass-gmsv 服务端内置 Lua 5.2.4 脚本引擎的 API 参考手册，面向编写 NPC/事件脚本的开发者。

各库按主题分组：NL/NLG 提供事件注册与通用工具，Char/Battle/Pet/Item/Obj/Map 对应各类游戏对象的读写与操作，Field/Setup/SQL/Protocol/Offline/Debug 则是数据存储、配置、数据库与协议层面的辅助与集成能力。每个函数一页，包含签名、参数说明、返回值与示例；部分函数附带备注，说明需要特别留意的行为细节。完整目录见下方各节；跨函数的通用约定——数值/字符串/布尔/函数/表等参数类型、对象index/道具index/战斗index 等句柄概念、可用的扩展模块——见附录部分。

## NL 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [NL.Charset](nl/Charset.md) | 获取当前 gmsv 运行时使用的文本编码。 |  |
| [NL.CreateAccount](nl/CreateAccount.md) | 异步注册一个游戏帐号，结果通过固定名回调函数返回。 |  |
| [NL.CreateArgNpc](nl/CreateArgNpc.md) | 直接创建 data/npc.txt 支持的各种内建类型 NPC，并传入该类型对应的参数。 |  |
| [NL.CreateCharacter](nl/CreateCharacter.md) | 异步在指定帐号的指定栏位创建一个游戏角色，结果通过固定名回调函数返回。 |  |
| [NL.CreateNpc](nl/CreateNpc.md) | 用 Lua 脚本创建一个 NPC，并执行指定的初始化函数。 |  |
| [NL.DelNpc](nl/DelNpc.md) | 删除一个 NPC。 |  |
| [NL.DeleteCharacter](nl/DeleteCharacter.md) | 异步删除指定帐号指定栏位的角色，结果通过固定名回调函数返回。 |  |
| [NL.GetErrorStr](nl/GetErrorStr.md) | 获取引擎最近一次记录的错误信息。 |  |
| [NL.RegAfterWarpEvent](nl/RegAfterWarpEvent.md) | 注册玩家使用传送点时触发的 Lua 函数，比 RegWarpEvent 多带传送前后的完整坐标。 |  |
| [NL.RegBattleActionEvent](nl/RegBattleActionEvent.md) | 注册玩家在战斗中发出指令时触发的 Lua 函数。 |  |
| [NL.RegBattleExitEvent](nl/RegBattleExitEvent.md) | 注册玩家中途离开战斗时触发的 Lua 函数。 |  |
| [NL.RegBattleGetProfitEvent](nl/RegBattleGetProfitEvent.md) | 注册战斗结算发放奖励时触发的 Lua 函数，可以改写掉落道具或决斗点。 |  |
| [NL.RegBattleNewTurnStartEvent](nl/RegBattleNewTurnStartEvent.md) | 注册战斗新回合开始时触发的 Lua 函数。 |  |
| [NL.RegBattleNextEnemyEvent](nl/RegBattleNextEnemyEvent.md) | 注册通过 Battle.SetNextBattle 设定的连战触发的 Lua 函数，用来提供下一波敌人。 |  |
| [NL.RegBattleOverEvent](nl/RegBattleOverEvent.md) | 注册战斗结束时触发的 Lua 函数。 |  |
| [NL.RegBattlePVPMaxHpEvent](nl/RegBattlePVPMaxHpEvent.md) | 注册 PK 战斗初始化角色最大生命值时触发的 Lua 函数，可以改写该上限。 |  |
| [NL.RegBattleSkillExpEvent](nl/RegBattleSkillExpEvent.md) | 注册对象获得战斗技能经验时触发的 Lua 函数，可以改写实际获得的技能经验。 |  |
| [NL.RegBattleStartEvent](nl/RegBattleStartEvent.md) | 注册战斗开始时触发的 Lua 函数。 |  |
| [NL.RegBattleSurpriseEvent](nl/RegBattleSurpriseEvent.md) | 注册战斗偷袭判定时触发的 Lua 函数，可以改写偷袭结果。 |  |
| [NL.RegCharActionEvent](nl/RegCharActionEvent.md) | 注册玩家做出动作（晕倒、攻击、剪刀石头布等）时触发的 Lua 函数。 |  |
| [NL.RegDamageCalculateEvent](nl/RegDamageCalculateEvent.md) | 注册战斗中计算伤害时触发的 Lua 函数，可以改写最终伤害值。 |  |
| [NL.RegDropEvent](nl/RegDropEvent.md) | 注册玩家掉线时触发的 Lua 函数。 |  |
| [NL.RegEquipmentLevelEvent](nl/RegEquipmentLevelEvent.md) | 注册读取装备使用所需等级时触发的 Lua 函数，可以改写该等级要求。 |  |
| [NL.RegFpConsumeEvent](nl/RegFpConsumeEvent.md) | 注册消耗魔力值（FP）时触发的 Lua 函数，可以改写消耗量。 |  |
| [NL.RegGetExpEvent](nl/RegGetExpEvent.md) | 注册对象获得战斗经验时触发的 Lua 函数，可以改写实际获得的经验值。 |  |
| [NL.RegGetLoginPointEvent](nl/RegGetLoginPointEvent.md) | 注册玩家登入时读取登录点信息触发的 Lua 函数，可用来实现原地登录。 |  |
| [NL.RegGetNextLevelExpEvent](nl/RegGetNextLevelExpEvent.md) | 注册读取升到下一级所需经验时触发的 Lua 函数，可以改写经验曲线。 |  |
| [NL.RegHeadCoverEvent](nl/RegHeadCoverEvent.md) | 注册生成角色头饰效果时触发的 Lua 函数，可以在不装备头饰道具的前提下指定头饰图档。 |  |
| [NL.RegItemDurabilityChangedEvent](nl/RegItemDurabilityChangedEvent.md) | 注册道具耐久度变化时触发的 Lua 函数。 |  |
| [NL.RegItemMaxDurabilityChangedEvent](nl/RegItemMaxDurabilityChangedEvent.md) | 注册道具最大耐久度变化时触发的 Lua 函数。 |  |
| [NL.RegItemOverLapEvent](nl/RegItemOverLapEvent.md) | 注册道具栏内把一个道具拖到另一个道具上时触发的 Lua 函数，可以拦截这次移动。 |  |
| [NL.RegItemString](nl/RegItemString.md) | 注册一个可以在 itemset 中使用的道具效果字段，道具触发该字段时会调用指定的 Lua 函数。 |  |
| [NL.RegLevelUpEvent](nl/RegLevelUpEvent.md) | 注册玩家角色升级时触发的 Lua 函数。 |  |
| [NL.RegLoginEvent](nl/RegLoginEvent.md) | 注册玩家登入游戏时触发的 Lua 函数。 |  |
| [NL.RegLoginGateEvent](nl/RegLoginGateEvent.md) | 注册玩家点击客户端“登出回记录点”时触发的 Lua 函数，可以拦截该操作。 |  |
| [NL.RegLogoutEvent](nl/RegLogoutEvent.md) | 注册玩家主动登出游戏时触发的 Lua 函数。 |  |
| [NL.RegMakeItemStringEvent](nl/RegMakeItemStringEvent.md) | 注册生成道具介绍文字时触发的 Lua 函数，可以改写道具说明文本。 |  |
| [NL.RegMergeItemEvent](nl/RegMergeItemEvent.md) | 注册玩家用生产技能制作道具时触发的 Lua 函数。 |  |
| [NL.RegNpcCreatedEvent](nl/RegNpcCreatedEvent.md) | 注册 NPC 被创建时触发的 Lua 函数。 |  |
| [NL.RegPartyEvent](nl/RegPartyEvent.md) | 注册玩家组队与离队时触发的 Lua 函数，可以拦截该操作。 |  |
| [NL.RegPetEquipCheckEvent](nl/RegPetEquipCheckEvent.md) | 注册宠物装备道具前触发的 Lua 函数，可以禁止本次装备。 |  |
| [NL.RegPetLevelUpEvent](nl/RegPetLevelUpEvent.md) | 注册宠物升级时触发的 Lua 函数。 |  |
| [NL.RegPetRideImageEvent](nl/RegPetRideImageEvent.md) | 注册服务器处理骑宠图档时触发的 Lua 函数，可以改写显示的骑宠图档。 |  |
| [NL.RegProductSkillExpEvent](nl/RegProductSkillExpEvent.md) | 注册对象获得生产技能经验时触发的 Lua 函数，可以改写实际获得的技能经验。 |  |
| [NL.RegRightClickEvent](nl/RegRightClickEvent.md) | 注册玩家右键点击另一名玩家时触发的 Lua 函数。 |  |
| [NL.RegSealEvent](nl/RegSealEvent.md) | 注册玩家封印宠物时触发的 Lua 函数，可以改写封印结果。 |  |
| [NL.RegShutDownEvent](nl/RegShutDownEvent.md) | 注册服务器关闭时触发的 Lua 函数。 |  |
| [NL.RegStallTradeEvent](nl/RegStallTradeEvent.md) | 注册摆摊交易时触发的 Lua 函数，可以自行处理金钱结算或直接拒绝交易。 |  |
| [NL.RegTalkEvent](nl/RegTalkEvent.md) | 注册玩家说话时触发的 Lua 函数，可用来做自定义指令、GM 命令与聊天过滤。 |  |
| [NL.RegTechOptionEvent](nl/RegTechOptionEvent.md) | 注册读取技能附加参数（TECH_OPTION 字段）时触发的 Lua 函数，可以改写字段值。 |  |
| [NL.RegTitleChangedEvent](nl/RegTitleChangedEvent.md) | 注册玩家称号发生变更时触发的 Lua 函数。 |  |
| [NL.RegVSEnemyCreateEvent](nl/RegVSEnemyCreateEvent.md) | 注册玩家遇敌生成敌人队列时触发的 Lua 函数，可以改写遇敌队列和数量。 |  |
| [NL.RegWarpEvent](nl/RegWarpEvent.md) | 注册玩家被传送到指定坐标时触发的 Lua 函数。 |  |
| [NL.SetArgNpc](nl/SetArgNpc.md) | 修改一个 Lua 创建的 NPC 的参数，并让它按新参数重新初始化。 |  |
| [NL.SetRemoteNpc](nl/SetRemoteNpc.md) | 设置 NPC 的远程模式，开启后该 NPC 可以不受距离限制被触发。 |  |
| [NL.Ver](nl/Ver.md) | 获取 Lua 引擎的版本标识。 |  |

## NLG 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [NLG.CanTalk](nlg/CanTalk.md) | 判断玩家当前是否可以与目标 NPC 交谈（在 CheckTalkRange 的几何判定基础上，额外拒绝不可见/停用的 NPC）。 |  |
| [NLG.CharLook](nlg/CharLook.md) | 让对象转向指定方向（只转身，不移动），并触发朝向两格内的对话联动检查。 |  |
| [NLG.CheckInFront](nlg/CheckInFront.md) | 判断目标对象是否位于自身朝向方向、指定距离以内的直线格子上。 |  |
| [NLG.CheckTalkRange](nlg/CheckTalkRange.md) | 检查两个对象是否处于可对话的位置关系（大致等价于“面对面且相距不超过2格”）。 |  |
| [NLG.DischargeParty](nlg/DischargeParty.md) | 解散指定对象所在的队伍。 |  |
| [NLG.DropPlayer](nlg/DropPlayer.md) | 强制断开指定玩家的连接。 |  |
| [NLG.FindNpcByName](nlg/FindNpcByName.md) | 按名字查找 NPC 类对象。 |  |
| [NLG.FindNpcByPos](nlg/FindNpcByPos.md) | 按坐标查找该格子上的第一个 NPC 类对象。 |  |
| [NLG.FindUser](nlg/FindUser.md) | 按帐号（CdKey）查找当前在线玩家的对象index。 |  |
| [NLG.GetFloorPets](nlg/GetFloorPets.md) | 获取指定地图楼层上放置在地面的所有宠物对象。 |  |
| [NLG.GetFrontChar](nlg/GetFrontChar.md) | 获取对象面前一格内、符合指定类型条件的所有对象数量和对象index列表。 |  |
| [NLG.GetGameTime](nlg/GetGameTime.md) | 获取游戏内当前所处的时段。 |  |
| [NLG.GetIp](nlg/GetIp.md) | 获取玩家当前连接的IP地址。 |  |
| [NLG.GetMAC](nlg/GetMAC.md) | 获取玩家登录时上报的MAC地址（本版本已启用MAC地址限制功能）。 |  |
| [NLG.GetMapName](nlg/GetMapName.md) | 获取指定地图楼层当前设置的显示名称。 |  |
| [NLG.GetMapPlayer](nlg/GetMapPlayer.md) | 获取指定地图楼层上所有在线玩家的对象index。 |  |
| [NLG.GetMapPlayerNum](nlg/GetMapPlayerNum.md) | 获取指定地图楼层上在线玩家的数量。 |  |
| [NLG.GetMessage](nlg/GetMessage.md) | 按ID读取旧版 msg.txt 消息表里的一条文字（不是 langmsg 多语言目录）。 |  |
| [NLG.GetOfflineEndTime](nlg/GetOfflineEndTime.md) | 同 Offline.GetOfflineEndTime |  |
| [NLG.GetOfflineStartTime](nlg/GetOfflineStartTime.md) | 同 Offline.GetOfflineStartTime |  |
| [NLG.GetOfflineStatus](nlg/GetOfflineStatus.md) | 同 Offline.GetOfflineStatus |  |
| [NLG.GetOnLinePlayer](nlg/GetOnLinePlayer.md) | 获取当前全服在线玩家总数。 | [NLG.GetPlayerNum](nlg/GetOnLinePlayer.md) |
| [NLG.GetStallItemPrice](nlg/GetStallItemPrice.md) | 获取玩家摆摊道具的定价表。 |  |
| [NLG.GetStallPetPrice](nlg/GetStallPetPrice.md) | 获取玩家摆摊宠物的定价表。 |  |
| [NLG.GetStallStatus](nlg/GetStallStatus.md) | 获取玩家的摆摊状态。 |  |
| [NLG.GetString](nlg/GetString.md) | 以给定分隔符集合切分字符串，取切分结果里第Pos个（从0开始）token。 |  |
| [NLG.MapEffect](nlg/MapEffect.md) | 清除全服玩家的地图特效，或对指定地图楼层设置地图特效；两种调用方式共用同一个函数名。 |  |
| [NLG.MoveItem](nlg/MoveItem.md) | 在玩家的物品栏位之间移动/合并道具。 |  |
| [NLG.Rand](nlg/Rand.md) | 生成一个指定范围内（含两端）的随机整数，使用服务器自身的随机数源。 |  |
| [NLG.SendGraphEvent](nlg/SendGraphEvent.md) | 给对象发送一个白名单内的图形观察事件（如战斗、升级、摆摊等状态图标的显示/隐藏），非玩家对象还会连带更新其内部技能状态。 |  |
| [NLG.SetAction](nlg/SetAction.md) | 设置对象当前的动作状态并向周围广播。 |  |
| [NLG.SetHeadIcon](nlg/SetHeadIcon.md) | 设置对象头顶显示的状态图标（如采集、生产等技能进行中的提示）。 |  |
| [NLG.SetMapName](nlg/SetMapName.md) | 设置指定地图楼层的显示名称，并向当前在该楼层的所有玩家实时广播。 |  |
| [NLG.SetObj](nlg/SetObj.md) | 在指定地图坐标写入一个物件（贴图对象），不改变该坐标的地砖。 |  |
| [NLG.SetOfflinePlayer](nlg/SetOfflinePlayer.md) | 同 Offline.SetOfflinePlayer |  |
| [NLG.SetPal](nlg/SetPal.md) | 改变玩家客户端当前显示的地图调色板。 |  |
| [NLG.SetShowName](nlg/SetShowName.md) | 设置 NPC/宠物/敌人对象是否像玩家一样在头顶显示名字。 |  |
| [NLG.ShowTalked](nlg/ShowTalked.md) | 触发一个对象自身注册的对话模板函数，并把另一个对象当作发起对话的一方传入。 |  |
| [NLG.ShowWindowTalked](nlg/ShowWindowTalked.md) | 生成并向目标对象发送一个对话框封包。 |  |
| [NLG.SortItem](nlg/SortItem.md) | 整理玩家的背包物品。 |  |
| [NLG.SystemMessage](nlg/SystemMessage.md) | 给指定对象发送一条黄色加粗的系统公告消息。 |  |
| [NLG.SystemMessageToMap](nlg/SystemMessageToMap.md) | 给指定地图上的所有在线玩家发送一条黄色加粗的系统公告消息。 |  |
| [NLG.Talk](nlg/Talk.md) | 让指定角色通过完整对话管线说一句话——与玩家客户端发出的对话封包走同一入口，会经过对话事件、连坐指令（聊天魔法）等处理，而不是像 TalkToCli 那样直接下发 TK 封包。 |  |
| [NLG.TalkToCli](nlg/TalkToCli.md) | 让一名角色对指定对象（或全服）说话，走直接 TK 封包通道，不经过对话事件/连坐指令解析。 | [NLG.Say](nlg/TalkToCli.md) |
| [NLG.TalkToFloor](nlg/TalkToFloor.md) | 让一名角色对指定地图+楼层上的所有在线玩家说话，走直接 TK 封包通道。 | [NLG.TalkToMap](nlg/TalkToFloor.md)、[NLG.Say2Map](nlg/TalkToFloor.md) |
| [NLG.Talked](nlg/Talked.md) | 调用引擎内置的银行/窗口治疗师/伤病医生三种 NPC 对话模板之一，是通往这几个legacy系统的桥接函数，不是通用的对话钩子。 |  |
| [NLG.UpChar](nlg/UpChar.md) | 强制刷新一个对象的客户端显示状态，视对象类型触发不同的重发流程。 |  |
| [NLG.Update_Party](nlg/Update_Party.md) | 让指定对象重新向队伍全体成员广播一次队伍参数。 | [NLG.UpdateParty](nlg/Update_Party.md) |
| [NLG.WalkMove](nlg/WalkMove.md) | 让对象朝指定方向走一格（真实位移，不只是转身）。 |  |
| [NLG.Walkable](nlg/Walkable.md) | 检测地图上指定坐标是否可通行。 |  |
| [NLG.WatchBattle](nlg/WatchBattle.md) | 让一名对象进入观战状态，观看另一名对象当前所在的战斗。 | [NLG.WatchEntry](nlg/WatchBattle.md) |
| [NLG.WindowTalked](nlg/WindowTalked.md) | Talked 的窗口交互半区，配合内置银行/窗口治疗师/伤病医生对话框的按钮响应使用。 |  |
| [NLG.c](nlg/c.md) | 将文本按 46 个半角字符宽度居中补空格，常用于 NPC 对话框标题的居中显示。 |  |

## Char 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Char.AddGold](char/AddGold.md) | 为目标对象增减金钱。 |  |
| [Char.AddPet](char/AddPet.md) | 按敌人模板 ID 为对象制作一只 1 级宠物并加入宠物栏，成长档随机。 |  |
| [Char.AddSkill](char/AddSkill.md) | 为玩家增加指定技能，可同时播种初始经验。 |  |
| [Char.CheckTitle](char/CheckTitle.md) | 重新检定玩家的全部称号解锁条件。 |  |
| [Char.ClrClrEvt](char/ClrClrEvt.md) | 批量同时清除对象的 NowEvent 与 EndEvent 任务旗标。 |  |
| [Char.ClrEvtEnd](char/ClrEvtEnd.md) | 批量清除对象的 EndEvent 任务旗标。 |  |
| [Char.ClrEvtNow](char/ClrEvtNow.md) | 批量清除对象的 NowEvent 任务旗标。 |  |
| [Char.DelItem](char/DelItem.md) | 删除目标对象身上指定 ID 的道具。 |  |
| [Char.DelPet](char/DelPet.md) | 删除对象身上第一只满足条件的宠物。 |  |
| [Char.DelSkill](char/DelSkill.md) | 删除玩家的指定技能。 |  |
| [Char.DelSlotPet](char/DelSlotPet.md) | 删除对象指定宠物栏位上的宠物。 |  |
| [Char.DischargeParty](char/DischargeParty.md) | 解散对象所在的队伍。 |  |
| [Char.DropPet](char/DropPet.md) | 把对象指定宠物栏位上的宠物丢到地面上。 |  |
| [Char.EndEvent](char/EndEvent.md) | 读取或设置对象的 EndEvent 任务旗标。 |  |
| [Char.FeverStart](char/FeverStart.md) | 让玩家进入打卡（Fever）状态。 |  |
| [Char.FeverStop](char/FeverStop.md) | 结束玩家的打卡（Fever）状态。 |  |
| [Char.FindItemId](char/FindItemId.md) | 查找对象身上第一个指定 ID 道具所在的道具栏位置。 |  |
| [Char.FindTitleIndex](char/FindTitleIndex.md) | 查找玩家是否拥有指定 ID 的称号，并返回其称号栏位置。 |  |
| [Char.GetBattleIndex](char/GetBattleIndex.md) | 获取玩家当前所在战斗的战斗index。 |  |
| [Char.GetCharPointer](char/GetCharPointer.md) | 获取对象的稳定标识。 |  |
| [Char.GetCurrentBattleActionCount](char/GetCurrentBattleActionCount.md) | 获取玩家在当前战斗回合内已提交的战斗指令数量。 |  |
| [Char.GetCurrentBattleTechActionCount](char/GetCurrentBattleTechActionCount.md) | 获取玩家在当前战斗回合内已提交的技能指令数量。 |  |
| [Char.GetData](char/GetData.md) | 读取对象index的指定信息栏位。 |  |
| [Char.GetGuildID](char/GetGuildID.md) | 获取玩家所属家族的 ID。 |  |
| [Char.GetGuildTitleID](char/GetGuildTitleID.md) | 获取玩家在家族中的称号 ID。 |  |
| [Char.GetHouseItem](char/GetHouseItem.md) | 获取玩家出租屋中指定位置的道具index。 |  |
| [Char.GetHousePet](char/GetHousePet.md) | 获取玩家出租屋中指定位置的宠物对象index。 |  |
| [Char.GetItemIndex](char/GetItemIndex.md) | 读取对象指定道具栏位上的道具index。 |  |
| [Char.GetPartyMember](char/GetPartyMember.md) | 获取对象所在队伍中指定位置的成员。 |  |
| [Char.GetPartyMode](char/GetPartyMode.md) | 获取对象当前的组队状态。 |  |
| [Char.GetPet](char/GetPet.md) | 获取对象指定宠物栏位上的宠物对象index。 |  |
| [Char.GetPoolItem](char/GetPoolItem.md) | 获取玩家银行中指定位置的道具index。 |  |
| [Char.GetPoolPet](char/GetPoolPet.md) | 获取玩家银行中指定位置的宠物对象index。 |  |
| [Char.GetSkillExp](char/GetSkillExp.md) | 获取玩家指定技能栏位置上的技能经验。 |  |
| [Char.GetSkillID](char/GetSkillID.md) | 获取玩家指定技能栏位置上的技能 ID。 |  |
| [Char.GetSkillLevel](char/GetSkillLevel.md) | 获取玩家指定技能栏位置上的技能等级。 |  |
| [Char.GetSkillMaxLevel](char/GetSkillMaxLevel.md) | 获取玩家指定技能栏位置上的技能在当前职业下的等级上限。 |  |
| [Char.GetTechId](char/GetTechId.md) | 获取对象某个技能栏位置下指定招式位置的招式 ID。 |  |
| [Char.GetTitle](char/GetTitle.md) | 获取玩家当前装备的称号 ID。 |  |
| [Char.GiveItem](char/GiveItem.md) | 给予目标对象指定 ID 的道具。 |  |
| [Char.GiveItemWithPos](char/GiveItemWithPos.md) | 在指定道具栏位上给予目标对象道具。 |  |
| [Char.GivePet](char/GivePet.md) | 按敌人模板 ID 为对象制作一只 1 级宠物，可指定是否满档。 |  |
| [Char.GiveRecipe](char/GiveRecipe.md) | 为玩家增加指定 ID 的配方。 |  |
| [Char.HasGuild](char/HasGuild.md) | 检测对象是否已经加入家族。 | [Char.HaveGuild](char/HasGuild.md) |
| [Char.HaveItem](char/HaveItem.md) | 检测对象身上是否有指定 ID 的道具，并返回该道具index。 |  |
| [Char.HavePet](char/HavePet.md) | 检测对象身上是否有指定 ID 的宠物，并返回其宠物栏位置。 |  |
| [Char.HaveSkill](char/HaveSkill.md) | 获取玩家指定技能所在的技能栏位置。 |  |
| [Char.IsEventEnd](char/IsEventEnd.md) | 检测对象的指定 EndEvent 任务旗标是否已经置位。 |  |
| [Char.IsEventNow](char/IsEventNow.md) | 检测对象的指定 NowEvent 任务旗标是否已经置位。 |  |
| [Char.IsFeverTime](char/IsFeverTime.md) | 检测玩家是否处于打卡（Fever）状态。 |  |
| [Char.ItemNum](char/ItemNum.md) | 统计对象身上指定 ID 道具的总数量。 | [Char.HaveItemNum](char/ItemNum.md) |
| [Char.ItemSlot](char/ItemSlot.md) | 统计对象道具栏中已被占用的栏位数量。 |  |
| [Char.JoinParty](char/JoinParty.md) | 让对象加入指定目标所在的队伍。 |  |
| [Char.LevelExp](char/LevelExp.md) | 获取对象当前等级对应的升级经验门槛。 |  |
| [Char.NowEvent](char/NowEvent.md) | 读取或设置对象的 NowEvent 任务旗标。 |  |
| [Char.PartyNum](char/PartyNum.md) | 获取对象所在队伍的成员人数。 |  |
| [Char.PetNum](char/PetNum.md) | 统计对象携带的宠物数量。 |  |
| [Char.SelectTitle](char/SelectTitle.md) | 为玩家装备指定栏位上的称号。 |  |
| [Char.SetBonusEncountRate](char/SetBonusEncountRate.md) | 设置玩家的遇敌率修正值。 |  |
| [Char.SetData](char/SetData.md) | 写入对象index的指定信息栏位。 |  |
| [Char.SetEvtEnd](char/SetEvtEnd.md) | 批量置位对象的 EndEvent 任务旗标。 |  |
| [Char.SetEvtNow](char/SetEvtNow.md) | 批量置位对象的 NowEvent 任务旗标。 |  |
| [Char.SetItemPutEvent](char/SetItemPutEvent.md) | 为对象index登记“有道具被丢在附近”事件的 Lua 回调函数。 |  |
| [Char.SetLoopEvent](char/SetLoopEvent.md) | 为对象index登记循环事件的 Lua 回调函数，每隔指定间隔触发一次。 |  |
| [Char.SetPartyNPC](char/SetPartyNPC.md) | 把 NPC 设为可组队的随行 NPC。 |  |
| [Char.SetPostOverEvent](char/SetPostOverEvent.md) | 为对象index登记“覆盖其他对象后”事件的 Lua 回调函数。 |  |
| [Char.SetPreOverEvent](char/SetPreOverEvent.md) | 为对象index登记“覆盖其他对象前”事件的 Lua 回调函数。 |  |
| [Char.SetSkillExp](char/SetSkillExp.md) | 设置玩家指定技能栏位置上的技能经验。 |  |
| [Char.SetSkillLevel](char/SetSkillLevel.md) | 设置玩家指定技能栏位置上的技能等级。 |  |
| [Char.SetTalkedEvent](char/SetTalkedEvent.md) | 为对象index登记“被搭话”事件的 Lua 回调函数。 |  |
| [Char.SetWalkPostEvent](char/SetWalkPostEvent.md) | 为对象index登记“行走后”事件的 Lua 回调函数。 |  |
| [Char.SetWalkPreEvent](char/SetWalkPreEvent.md) | 为对象index登记“行走前”事件的 Lua 回调函数。 |  |
| [Char.SetWindowTalkedEvent](char/SetWindowTalkedEvent.md) | 为对象index登记“对话框交互”事件的 Lua 回调函数。 |  |
| [Char.Warp](char/Warp.md) | 将对象连同其队伍传送到指定地图坐标。 |  |

## Battle 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Battle.ActionSelect](battle/ActionSelect.md) | 让对象执行一次指定的战斗指令，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。 |  |
| [Battle.DelDefaultWinEvent](battle/DelDefaultWinEvent.md) | 删除指定战斗的引擎内建胜利事件。 |  |
| [Battle.Encount](battle/Encount.md) | 触发一场遇敌战斗；两参数形式为原地遇敌，三参数形式把 NPC 重新初始化为立敌（stand enemy）后发起战斗。 |  |
| [Battle.ExitBattle](battle/ExitBattle.md) | 强制让指定对象退出当前所在的战斗。 |  |
| [Battle.FinishPlayerBattle](battle/FinishPlayerBattle.md) | 让角色直接脱离当前战斗并结束战斗流程。 |  |
| [Battle.GetBattleCharacterStatus](battle/GetBattleCharacterStatus.md) | 获取对象当前的某一项战斗状态（战斗中的临时增益、异常状态与回合计数）。 |  |
| [Battle.GetBattleFieldAttribute](battle/GetBattleFieldAttribute.md) | 获取当前战斗的战场魔法效果，如属性翻转、魔法封印。 |  |
| [Battle.GetBattleMode](battle/GetBattleMode.md) | 获取对象当前的战斗状态。 |  |
| [Battle.GetCurrentBattle](battle/GetCurrentBattle.md) | 获取指定对象当前所处战斗的战斗index。 |  |
| [Battle.GetEntryPosition](battle/GetEntryPosition.md) | 获取对象在战场中的位置编号。 |  |
| [Battle.GetGainMode](battle/GetGainMode.md) | 获取战斗奖励模式，如奖励经验、奖励 DP。 |  |
| [Battle.GetMod](battle/GetMod.md) | 获取战斗的运行模式（战斗流程状态机所处的阶段）。 |  |
| [Battle.GetNextBattle](battle/GetNextBattle.md) | 获取连战设置。 |  |
| [Battle.GetNoRisk](battle/GetNoRisk.md) | 获取战斗的 NoRisk（无风险）标志。 |  |
| [Battle.GetPlayIndex](battle/GetPlayIndex.md) | 获取战斗队列中指定位置上对象实例的对象index。 | [Battle.GetPlayer](battle/GetPlayIndex.md) |
| [Battle.GetTargetSelect](battle/GetTargetSelect.md) | 根据进攻者与目标在战场中的位置，换算出可直接用于战斗指令的目标参数。 |  |
| [Battle.GetTurn](battle/GetTurn.md) | 获取战斗当前的回合数。 |  |
| [Battle.GetType](battle/GetType.md) | 获取战斗类型，如普通战、PVP 战等。 |  |
| [Battle.GetUseFpByTechId](battle/GetUseFpByTechId.md) | 查询指定对象施放某个战斗技能所需的 FP 消耗。 |  |
| [Battle.GetWinSide](battle/GetWinSide.md) | 获取战斗胜利方所在的队列。 |  |
| [Battle.IsBattleSurprise](battle/IsBattleSurprise.md) | 判断战斗是否存在先制（偷袭）方。 |  |
| [Battle.IsBossBattle](battle/IsBossBattle.md) | 判断战斗是否是 BOSS 战。 |  |
| [Battle.IsUsing](battle/IsUsing.md) | 判断指定战斗槽是否正在使用中。 |  |
| [Battle.IsWaitingCommand](battle/IsWaitingCommand.md) | 判断对象是否正处于战斗中的等待输入指令状态。 |  |
| [Battle.JoinBattle](battle/JoinBattle.md) | 让一个不在战斗中的玩家加入另一个玩家的战斗（战斗中途救援参战）。 |  |
| [Battle.PVE](battle/PVE.md) | 用 Lua 脚本直接创建一场对怪物的战斗，战斗初始化完成后可回调指定的 Lua 函数。 |  |
| [Battle.PVP](battle/PVP.md) | 在两个玩家之间创建一场 PK 战斗。 |  |
| [Battle.PetActionSelect](battle/PetActionSelect.md) | 让玩家的出战宠物执行一次战斗指令，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。 |  |
| [Battle.SetBattleCharacterStatus](battle/SetBattleCharacterStatus.md) | 设置对象当前的某一项战斗状态。 |  |
| [Battle.SetBattleFieldAttribute](battle/SetBattleFieldAttribute.md) | 设置当前战斗的战场魔法效果，如属性翻转、魔法封印。 |  |
| [Battle.SetGainMode](battle/SetGainMode.md) | 设置战斗奖励模式，如奖励经验、奖励 DP。 |  |
| [Battle.SetMod](battle/SetMod.md) | 设置战斗的运行模式（战斗流程状态机所处的阶段）。 |  |
| [Battle.SetNextBattle](battle/SetNextBattle.md) | 设置连战（本场战斗结束后接续下一场）。 |  |
| [Battle.SetNoRisk](battle/SetNoRisk.md) | 设置战斗的 NoRisk（无风险）标志。 |  |
| [Battle.SetType](battle/SetType.md) | 设置战斗类型，如普通战、PVP 战等。 |  |
| [Battle.SetWinEvent](battle/SetWinEvent.md) | 为战斗设置胜利事件的 Lua 回调函数，战斗结束时由引擎回调。 | [Battle.SetPVPWinEvent](battle/SetWinEvent.md) |
| [Battle.UseTech](battle/UseTech.md) | 让对象按技能栏位置施放战斗技能，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。 |  |
| [Battle.UseTechById](battle/UseTechById.md) | 让对象直接按 tech id 施放战斗技能，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。 |  |

## Pet 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Pet.AddSkill](pet/AddSkill.md) | 给宠物增加一个新技能，宠物技能栏未满时生效。 |  |
| [Pet.ArtRank](pet/ArtRank.md) | 获取指定宠物某项属性的当前成长值（档数）。 | [Pet.GetArtRank](pet/ArtRank.md) |
| [Pet.DelSkill](pet/DelSkill.md) | 删除宠物指定位置上的技能。 |  |
| [Pet.FullArtRank](pet/FullArtRank.md) | 获取指定宠物某项属性的满档成长值。 |  |
| [Pet.GetGetableItemList](pet/GetGetableItemList.md) | 获取战斗中敌方怪物身上的可掉落道具对象列表。 |  |
| [Pet.GetOwner](pet/GetOwner.md) | 获取宠物的拥有者对象index。 |  |
| [Pet.GetRider](pet/GetRider.md) | 获取骑乘该宠物的玩家对象index。 |  |
| [Pet.GetSkill](pet/GetSkill.md) | 获取宠物指定位置上的技能 ID。 |  |
| [Pet.GetStatus](pet/GetStatus.md) | 获取玩家指定宠物栏位上宠物的出战状态。 |  |
| [Pet.GetStealableItem](pet/GetStealableItem.md) | 获取战斗中敌方怪物身上的可偷窃道具对象。 |  |
| [Pet.GetUUID](pet/GetUUID.md) | 获取宠物对象的全局唯一标识。 |  |
| [Pet.IsPet](pet/IsPet.md) | 判断对象是否为宠物。 |  |
| [Pet.Kill](pet/Kill.md) | 从指定玩家身上删除指定宠物，宠物对象随之销毁。 |  |
| [Pet.LevelUp](pet/LevelUp.md) | 让玩家指定宠物栏位上的宠物提升 1 级。 |  |
| [Pet.ReBirth](pet/ReBirth.md) | 回炉指定宠物，让宠物回到 1 级并按当前档数重新分配基础属性。 |  |
| [Pet.SetArtRank](pet/SetArtRank.md) | 设置指定宠物某项属性的成长值（档数）。 |  |
| [Pet.SetGetableItemList](pet/SetGetableItemList.md) | 设置战斗中敌方怪物身上的可掉落道具对象。 |  |
| [Pet.SetStatus](pet/SetStatus.md) | 设置玩家指定宠物栏位上宠物的出战状态。 |  |
| [Pet.SetStealableItem](pet/SetStealableItem.md) | 设置战斗中敌方怪物身上的可偷窃道具对象。 |  |
| [Pet.TradePet](pet/TradePet.md) | 把玩家指定宠物栏位上的宠物转移给另一个玩家。 |  |
| [Pet.UpPet](pet/UpPet.md) | 结算宠物所有待处理的升级，并把宠物的最新状态封包发给客户端。 |  |

## Item 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Item.GetData](item/GetData.md) | 获取道具实例的指定信息栏位。 |  |
| [Item.Kill](item/Kill.md) | 删除玩家指定槽位上的道具实例，并向该玩家发送系统提示与客户端刷新。 |  |
| [Item.KillByIndex](item/KillByIndex.md) | 仅凭道具 index 销毁一个道具实例（自动在持有者的 28 个背包槽位中定位）。 |  |
| [Item.MakeItemAndRegist](item/MakeItemAndRegist.md) | 创建一个未挂靠任何角色的游离道具实例，并返回其 ItemIndex。 |  |
| [Item.SetData](item/SetData.md) | 设置道具实例的指定信息栏位。 |  |
| [Item.SetTimeLimit](item/SetTimeLimit.md) | 设置或清除道具实例的时限属性。 |  |
| [Item.TradeItem](item/TradeItem.md) | 将一个玩家的道具实例转移给另一个玩家的背包（不弹交易窗口，直接转移）。 |  |
| [Item.UpItem](item/UpItem.md) | 向该角色关联的客户端发送指定道具槽位的数据封包，强制刷新道具栏显示。 |  |

## Obj 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Obj.GetCharIndex](obj/GetCharIndex.md) | 获取指定 Object Index 关联的 Index 栏位。 |  |
| [Obj.GetDelTime](obj/GetDelTime.md) | 获取指定 Object 的删除时间。 |  |
| [Obj.GetFloor](obj/GetFloor.md) | 获取指定 Object Index 的 Floor ID。 |  |
| [Obj.GetMap](obj/GetMap.md) | 获取指定 Object Index 的 Map ID。 |  |
| [Obj.GetObject](obj/GetObject.md) | 获取指定地图坐标上的 Object Index 列表。 |  |
| [Obj.GetType](obj/GetType.md) | 获取指定 Object Index 的 Object 类型。 |  |
| [Obj.GetX](obj/GetX.md) | 获取指定 Object Index 的 X 坐标。 |  |
| [Obj.GetY](obj/GetY.md) | 获取指定 Object Index 的 Y 坐标。 |  |
| [Obj.SetDelTime](obj/SetDelTime.md) | 设置指定 Object 的删除时间。 |  |
| [Obj.SetFloor](obj/SetFloor.md) | 设置指定 Object Index 的 Floor ID。 |  |
| [Obj.SetMap](obj/SetMap.md) | 设置指定 Object Index 的 Map ID。 |  |
| [Obj.SetType](obj/SetType.md) | 设置指定 Object Index 的 Object 类型。 |  |
| [Obj.SetX](obj/SetX.md) | 设置指定 Object Index 的 X 坐标。 |  |
| [Obj.SetY](obj/SetY.md) | 设置指定 Object Index 的 Y 坐标。 |  |

## Map 库

- [库说明](map/guide.md)
- [demo](map/demo.md)

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Map.DelLuaMap](map/DelLuaMap.md) | 删除一张 Lua 生成的地图，释放其 Floor 编号，并将该地图上的所有实体清场。 |  |
| [Map.DumpLuaMap](map/DumpLuaMap.md) | 把一张 Lua 地图导出为本地地图文件（可当作简易地图编辑器使用）。 |  |
| [Map.GetAvailablePos](map/GetAvailablePos.md) | 在一张随机（迷宫）地图上获取一个可通行的空地坐标。 |  |
| [Map.GetDungeonExpireTime](map/GetDungeonExpireTime.md) | 获取一张（经典随机地城系统的）地图距离重置还剩的秒数。 |  |
| [Map.GetImage](map/GetImage.md) | 获取地图指定坐标的地板（底层）图档编号与物件（顶层）图档编号。 |  |
| [Map.GetMapSize](map/GetMapSize.md) | 获取地图的尺寸。 |  |
| [Map.MakeCopyMap](map/MakeCopyMap.md) | 复制一张已存在的地图（原样拷贝地板/物件/遭遇等信息）到 Lua 地图区块中的一个新 Floor。 |  |
| [Map.MakeMazeMap](map/MakeMazeMap.md) | 异步生成一张随机（迷宫）地图；调用立即返回预留的 FloorId，实际生成在后台完成后通过回调函数通知结果。 |  |
| [Map.SetImage](map/SetImage.md) | 设置地图指定坐标的地板或物件图档编号（系统自动判定该图档属于地板层还是物件层）。 |  |

## Field 库

- [库说明](field/guide.md)

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Field.Get](field/Get.md) | 读取指定 Field 的值。Field 名称首字符决定归属层级：不带前缀绑定当前角色，"#"前缀绑定所在账号，"@"前缀绑定整个服务器。 |  |
| [Field.Set](field/Set.md) | 设置指定 Field 的值；名称首字符前缀规则与 Field.Get 相同。 |  |

## Foreach 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Foreach.Enemy](foreach/Enemy.md) | 对当前地图上所有敌人（战斗单位）角色依次执行指定的回调函数。 |  |
| [Foreach.Item](foreach/Item.md) | 对所有已使用且状态可用的道具实例依次执行指定的回调函数。 |  |
| [Foreach.Npc](foreach/Npc.md) | 对当前地图上所有 NPC 类角色依次执行指定的回调函数（不含玩家/宠物/敌人/传送点）。 |  |
| [Foreach.Object](foreach/Object.md) | 对世界对象表中所有已使用（非 NOUSE）的 Object 依次执行指定的回调函数。 |  |
| [Foreach.Pet](foreach/Pet.md) | 对当前所有在线宠物依次执行指定的回调函数。 |  |
| [Foreach.Player](foreach/Player.md) | 对当前所有在线玩家依次执行指定的回调函数。 |  |
| [Foreach.Warp](foreach/Warp.md) | 对当前所有可用的 Warp 传送点角色依次执行指定的回调函数。 |  |

## Data 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Data.EnemyGetData](data/EnemyGetData.md) | 获取指定索引的怪物出场表条目（enemy.txt）在某个信息栏位上的值。 |  |
| [Data.EnemyGetIndex](data/EnemyGetIndex.md) | 通过 Enemy ID 获取该 Enemy 在 enemy.txt（怪物出场表）中的索引。 |  |
| [Data.EnemyTempGetData](data/EnemyTempGetData.md) | 获取指定索引的怪物基础模板（enemybase.txt）在某个信息栏位上的值。 |  |
| [Data.EnemyTempGetIndex](data/EnemyTempGetIndex.md) | 通过 Enemy ID 获取该 Enemy 在 enemybase.txt（怪物基础模板表）中的索引。 |  |
| [Data.ItemsetGetData](data/ItemsetGetData.md) | 获取指定索引的道具模板在某个信息栏位上的值。 |  |
| [Data.ItemsetGetIndex](data/ItemsetGetIndex.md) | 通过道具 ID 获取该道具在 ITEMSET.txt（道具模板表）中的索引。 |  |
| [Data.ItemsetGetRandomIntData](data/ItemsetGetRandomIntData.md) | 获取指定索引的道具模板在某个整数栏位上的随机浮动区间宽度。 |  |

## Setup 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Setup.Get](setup/Get.md) | 按配置项名称读取服务端当前生效的设置值。 |  |
| [Setup.Set](setup/Set.md) | 修改服务端当前进程内某配置项在内存中的数值；不改写配置文件本身，重启后修改效果消失。 |  |

## SQL 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [SQL.Query](sql/Query.md) | 执行一条SQL语句（同步阻塞，直到拿到结果或超时）；SQL.Run是同一实现的别名。 | [SQL.Run](sql/Query.md) |

## Protocol 库

- [库说明](protocol/guide.md)

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Protocol.AddPacket](protocol/AddPacket.md) | 注册一对脚本自定义的封包头（接收/发送标识），用于承载脚本自己扩展的协议。 |  |
| [Protocol.GetCharByFd](protocol/GetCharByFd.md) | 根据网络连接套接字ID获取对应的玩家对象index。 |  |
| [Protocol.OnRecv](protocol/OnRecv.md) | 为指定封包ID注册一个接收回调，可以过滤/拦截该封包在服务端的后续派发。 |  |
| [Protocol.RawSend](protocol/RawSend.md) | 向指定对象发送一段未经封包头封装的原始数据。 |  |
| [Protocol.Send](protocol/Send.md) | 向指定对象发送一个自定义内容的封包。 |  |
| [Protocol.SendLuaCustomPacket](protocol/SendLuaCustomPacket.md) | 发送Lua自定义封包，固定走服务端的自定义封包通道。 |  |

## Offline 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Offline.GetOfflineEndTime](offline/GetOfflineEndTime.md) | 获取指定玩家离线挂机的结束时间。 |  |
| [Offline.GetOfflineStartTime](offline/GetOfflineStartTime.md) | 获取指定玩家离线挂机的开始时间。 |  |
| [Offline.GetOfflineStatus](offline/GetOfflineStatus.md) | 获取指定玩家当前是否处于离线挂机状态。 |  |
| [Offline.OfflineLogin](offline/OfflineLogin.md) | 以离线模式登录指定帐号的角色（不建立客户端连线），默认离线挂机时长按登录流程另行设定。 |  |
| [Offline.OfflineLogout](offline/OfflineLogout.md) | 强制结束当前离线挂机角色的登录状态（立即登出）。 |  |
| [Offline.SetOfflineEndTime](offline/SetOfflineEndTime.md) | 重新设置离线挂机角色的结束时间（从当前时间起续期）。 |  |
| [Offline.SetOfflineLoopEvent](offline/SetOfflineLoopEvent.md) | 为指定对象设置离线循环事件回调，每隔 Interval 毫秒触发一次，直到被清除或对象登出。 |  |
| [Offline.SetOfflinePlayer](offline/SetOfflinePlayer.md) | 设置指定玩家进入离线挂机状态，并保持指定时长。 |  |

## Debug 库

| 函数 | 功能简述 | 别名 |
| --- | --- | --- |
| [Debug.OfflineLogin](debug/OfflineLogin.md) | 同 Offline.OfflineLogin |  |
| [Debug.Snapshot](debug/Snapshot.md) | 生成当前 Lua 状态的内存快照（本版本为占位实现），供内存诊断参考。 |  |

## 附录

- [数值型](appendix/数值型.md)
- [字符串](appendix/字符串.md)
- [布尔型](appendix/布尔型.md)
- [函数型](appendix/函数型.md)
- [表](appendix/表.md)
- [对象index](appendix/对象index.md)
- [道具index](appendix/道具index.md)
- [战斗index](appendix/战斗index.md)
- [扩展模块](appendix/扩展模块.md)
- [事件总表](appendix/事件总表.md)
- [setup配置键](appendix/setup配置键.md)
- [常量](appendix/常量.md)
- [常量-big5](appendix/常量-big5.md)

## 待补充

无：所有函数都已有中文说明。

## 全局函数

- `gadofile(FileName)`：不属于任何库的全局函数，加载并执行指定的 Lua 脚本文件，无论成功与否都返回 1。
