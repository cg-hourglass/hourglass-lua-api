<!-- Generated. DO NOT EDIT. -->
# RegVSEnemyCreateEvent

## NL.RegVSEnemyCreateEvent(Dofile, FuncName)

### 函数功能

注册玩家遇敌生成敌人队列时触发的 Lua 函数，可以改写遇敌队列和数量。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## VSEnemyCreateCallBack(CharIndex, GroupIndex, EnemyNum, EnemyList)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 触发遇敌的玩家对象index，由引擎传入。
- GroupIndex: [数值型](../appendix/数值型.md) 本次遇敌的 group ID，由引擎传入。
- EnemyNum: [数值型](../appendix/数值型.md) 服务器算出的遇敌数量，由引擎传入。
- EnemyList: [数值型](../appendix/数值型.md)[数组] 遇敌队列，长度 16 的一维表（EnemyList[1] ~ EnemyList[16]），每项是 enemy 的数组index（可用 Data.EnemyGetIndex 取得），空位为 -1。由引擎传入。

### 返回值

返回一个 table 作为新的遇敌队列，引擎会读回其 1~16 项并把遇敌数量重算为“不等于 -1 的项数”。返回任何非 table 的值都会丢弃全部改动并沿用传入的 EnemyNum。

## 参考实例

```lua
NL.RegVSEnemyCreateEvent(nil, "MyVSEnemyCreateEvent");

function MyVSEnemyCreateEvent(CharIndex, GroupIndex, EnemyNum, EnemyList)
  local EnemyIndex = Data.EnemyGetIndex(1); -- 取得虎人的 EnemyIndex
  local NewEnemyList = {};
  for i = 1, 16, 1 do
    if i <= 10 then
      NewEnemyList[i] = EnemyIndex; -- 10 只虎人
    else
      NewEnemyList[i] = -1;         -- 其余无效
    end
  end
  return NewEnemyList;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
传入的 EnemyList 是每次现做的新表、下标从 1 开始；惯用写法是就地修改它再返回它。
引擎读回时不走元方法：缺项或非数值一律按 -1（空位）处理。
旧版在这里会把缺项读成 0（即一只有效敌人）并可能触发 __index 元方法，本服务端刻意采用了更安全的语义。
触发点在遇敌队列生成处；如果改写后有效项数为 0，本次遇敌会被取消。
