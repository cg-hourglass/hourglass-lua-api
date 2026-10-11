<!-- Generated. DO NOT EDIT. -->
# RegBattleNextEnemyEvent

## NL.RegBattleNextEnemyEvent(Dofile, FuncName)

### 函数功能

注册通过 Battle.SetNextBattle 设定的连战触发的 Lua 函数，用来提供下一波敌人。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## BattleNextEnemyCallBack(BattleIndex, Flg)

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，由引擎传入。
- Flg: [数值型](../appendix/数值型.md) 连战标记，由 Battle.SetNextBattle 设定并由引擎传回。

### 返回值

返回一个扁平 table，每两项一组：奇数项是 enemy ID，偶数项是基础等级，形如 {id1, lv1, id2, lv2, ...}。最多读取 20 项（即 10 只敌人），多余部分被忽略。返回非 table 则本波没有敌人。

## 参考实例

```lua
NL.RegBattleNextEnemyEvent(nil, "MyBattleNextEnemyEvent");

function MyBattleNextEnemyEvent(BattleIndex, Flg)
  if(Flg == 1)then
    print("第一场连战");
    Battle.SetNextBattle(BattleIndex, 2);
    return {11,200, 11,200, 11,0, 11,0, 11,100};
  end
  if(Flg == 2)then
    print("第二场连战");
    Battle.SetNextBattle(BattleIndex, -1); -- 不再设置连战
    return {11,200, 11,200, 11,0, 11,0, 11,100};
  end
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
只有 Battle.SetNextBattle 设置过连战标记（不等于 -1）时才会触发。
重要：只要 Lua 虚拟机存在，引擎在调用处理函数之前就会无条件清空全部 10 个敌人槽位。所以已注册但处理函数出错、或返回了非 table，本波敌人会被清空而不是保持原样。
奇数项按 enemy ID 传入（引擎内部会转成数组index），每个槽位的 SkillType 一律被置 0。回调的返回值本身会被调用方丢弃，真正生效的是这张表。
