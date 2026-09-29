<!-- Generated. DO NOT EDIT. -->
# DeleteCharacter

## NL.DeleteCharacter(Cdkey, DataplaceNum)

### 函数功能

异步删除指定帐号指定栏位的角色，结果通过固定名回调函数返回。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 帐号（cdkey），长度必须小于 32 字节。
- DataplaceNum: [数值型](../appendix/数值型.md) 角色栏位，0 表示左边，1 表示右边。

### 返回值

返回1表示请求已成功入队，返回0表示未入队（帐号超长、队列已满或未接入异步执行器）。这只代表指令发出成功，删除结果要通过 DeleteCharacterCallback 获取。

## DeleteCharacterCallback(cdkey, dataplace, regist, ret)

### 参数说明

- cdkey: [字符串](../appendix/字符串.md) 发起删除时传入的帐号，由引擎传回。
- dataplace: [数值型](../appendix/数值型.md) 角色栏位，由引擎传回。
- regist: [数值型](../appendix/数值型.md) 角色的 regist number，由引擎传回。
- ret: [数值型](../appendix/数值型.md) 删除结果。1 表示成功，其它值表示失败。由引擎传回。

### 返回值

无返回值，引擎不读取本函数的返回值。

## 参考实例

```lua
NL.DeleteCharacter("testuser", 0);

function DeleteCharacterCallback(cdkey, dataplace, regist, ret)
  if(ret == 1)then
    print("帐号"..cdkey.."的第"..dataplace.."个角色已删除");
  end
end
```

### 备注

回调函数名是固定的全局名 DeleteCharacterCallback，需要脚本自行在入口文件里定义；引擎按名字查找，没定义就静默跳过。
删除级联在后台完成，主循环每一轮只投递一个异步完成项。
