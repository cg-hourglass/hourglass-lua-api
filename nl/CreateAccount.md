<!-- Generated. DO NOT EDIT. -->
# CreateAccount

## NL.CreateAccount(Cdkey, Password)

### 函数功能

异步注册一个游戏帐号，结果通过固定名回调函数返回。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 帐号（cdkey），长度必须小于 32 字节。
- Password: [字符串](../appendix/字符串.md) 密码，长度必须小于 16 字节。

### 返回值

返回1表示请求已成功入队，返回0表示未入队（参数超长、队列已满或未接入异步执行器）。这只代表指令发出成功，注册本身的结果要通过 CreateAccountCallback 获取。

## CreateAccountCallback(cdkey, pass, ret)

### 参数说明

- cdkey: [字符串](../appendix/字符串.md) 发起注册时传入的帐号，由引擎传回。
- pass: [字符串](../appendix/字符串.md) 密码位；引擎恒定传入空字符串 ""，不会回传真实密码。
- ret: [数值型](../appendix/数值型.md) 注册结果。1 表示成功，其它值表示失败。由引擎传回。

### 返回值

无返回值，引擎不读取本函数的返回值。

## 参考实例

```lua
NL.CreateAccount("testuser", "testpass");

function CreateAccountCallback(cdkey, pass, ret)
  if(ret == 1)then
    print("帐号"..cdkey.."注册成功");
  else
    print("帐号"..cdkey.."注册失败");
  end
end
```

### 备注

回调函数名是固定的全局名 CreateAccountCallback，需要脚本自行在入口文件里定义；引擎按名字查找，没定义就静默跳过。
主循环每一轮只投递一个异步完成项，所以批量注册时回调会被逐个分批送达。
使用本函数请保证没有改动过 tbl_user 表的结构；如果新增的字段都允许为 NULL，则不影响使用。
回调的第二个参数不是真实密码，引擎恒定传空串。
