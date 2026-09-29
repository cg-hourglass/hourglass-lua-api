<!-- Generated. DO NOT EDIT. -->
# Query

## SQL.Query(QueryString)

### 函数功能

执行一条SQL语句（同步阻塞，直到拿到结果或超时）；SQL.Run是同一实现的别名。

### 函数别名

- `SQL.Run(QueryString)`

### 参数说明

- QueryString: [字符串](../appendix/字符串.md) 要执行的SQL查询/语句文本。

### 返回值

单个数值或一张结果表：
- `-1001`：Lua专用连接池已耗尽（本引擎为 SQL.* 单独准备了一个有界连接池；池满时立即返回，不排队等待）。
- `-1`：语句执行失败（SQL语法错误、连接异常等），或本次查询超过配置的超时时间。
- `0`：语句执行成功但没有可用结果集——INSERT/UPDATE/DELETE 成功、SELECT 结果为空、或结果集在读取阶段中途失败（这种失败按成功且零行处理，不会额外报错）。
- 非空结果集时返回一张 table：键为字符串 `"行号_列号"`（均从0开始计数，且最多保留14个可见字符，超长时按固定规则截断，极端的行/列号可能因此共享同一个截断后的键），值统一是字符串；某单元格为SQL NULL时，对应键在表中不存在（不会出现值为nil的键）。

## 参考实例

```lua
local query = "UPDATE tbl_globalregvalue SET value = '1000' WHERE account_id='freefs' and str='#dianjuan2'";
local resset = SQL.Run(query);
print(resset); -- 输出 0

local query2 = "SELECT * from tbl_character WHERE cdkey='free'";
local resset2 = SQL.Query(query2);
if type(resset2) == "table" then
  print(resset2["0_1"]); -- 第一行第二列的值
  print(resset2["1_2"]); -- 第二行第三列的值
end
```

### 备注

- 结果表的下标是字符串（如 `resset["0_1"]`）；下划线连接的裸标识符不是合法的 Lua 表下标写法，注意不要误写成 `resset[0_1]`。
- SQL.Query 与 SQL.Run 是同一个实现的两个名字，不存在“Run 返回受影响行数”这回事——不论是SELECT、UPDATE还是DELETE，成功且无结果集一律返回0，不要用 Run 的返回值判断“改了几行”。
- SQL.* 使用本引擎单独准备的一个有界连接池（默认4个连接、5秒超时，均可配置），与引擎自身存取角色/道具等数据使用的连接池完全独立，互不挤占。
- SQL.Query 是本引擎“游戏回调中禁止阻塞”这条总规则的一个显式例外：调用会阻塞发起调用的处理流程，直到数据库应答或超时为止（脚本写 `local r = SQL.Query(...)` 后紧接着在下一行使用 r 是安全的）；查询超时时长可配置，避免无限阻塞。
- 查询语句与结果全程按脚本自身的传统编码（GBK/Big5，与数据库连接的 charset 一致）原样透传，不经过引擎的 UTF-8 转码层，这样才能保证结果单元格里任意二进制内容（含BLOB）原样往返。
