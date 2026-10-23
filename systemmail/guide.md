# 系统奖励邮件

系统邮件不占用好友名片槽。奖励支持金币与最多二十条拆分后的道具附件，整封领取，
每条附件需要一个新背包空格，不自动合并到已有堆叠。通知可以没有任何奖励。
发送、阅读、呼叫与实际发放是不同动作；打开界面、播放动画都不代表已经领取。

所有失败统一返回 `nil, code, detail`；Configure 和 MarkRead 成功为 `1`，
其余成功为表。常见错误有 BAD_ARGS、TEXT、LIMIT、TOO_BIG、INVALID_ITEM、
KEY_CONFLICT、NOT_FOUND、NO_REWARD、EXPIRED、STATE、MAP、BUSY、BAG_SPACE、
GOLD_LIMIT、DB、FORBIDDEN、OWNER_SERVER、CONFLICT。BAG_SPACE 的 detail 为
`{required_slots,free_slots}`；OWNER_SERVER 的 detail 为 `{dispatch_server_number}`。

## 发送与查询

```lua
assert(SystemMail.Configure{name='System',title='Rewards',graphic=0,
  courier_graphic=101000,courier_effect=0,audience_fields={}})
local result,code,detail=SystemMail.Send(
  {cdkey=account,regist_number=regist},
  {key='maintenance:2026-10-19',title='Maintenance reward',body='Thank you.',
   items={{item_id=item_template,amount=5}},gold=1000})
```

图号与道具模板必须取目标服务器实际可用资源；示例不能替代资源核验。
title 最长48个运行编码字节，body 最长1024个字节，不截断或替换不可表示文字。
key 为1..128个可打印ASCII字节，在同一系统发件人与确切收件角色内去重。
相同规范化参数返回原 id 和 existing=true，内容冲突 KEY_CONFLICT；过期或已撤回
也不会重新生成奖励。删除角色后的邮件保留原业务键，发送同键不会重新开放奖励。

Summary 的定位字段为 latest_unread_id/latest_pending_id。List 的 anchor_id 必须
属于本人且可见，与 cursor 互斥，从定位项开始有界返回，不自动标记已读。
Get 的 opts 为 `{attachment_page=1}`，一页最多10条摘要；Preview 返回
`{id,index,tooltip}`，不会返回完整奖励存档，也不占假背包槽。

## 投递与通知

player/actor 是当前真人角色的整数索引；handle 是仅服务器持有的不透明字符串。
BeginDelivery/DeliveryState 返回 `{id,handle,state,ready_at,depart_at,expires_at}`，
均为服务器 Unix 秒。这里 expires_at 是表现资源 TTL；奖励期限另用 mail_expires_at。
实际完成后 depart_at 从实际成功时间加 depart_seconds 计算，并限制在资源 TTL 内。

受信任 Lua 服务实现 CallCourier，调用 BeginDelivery、ShowCourier，并在共享
事件分发器的有界 tick 中读取 DeliveryState，到 ready_at 才 CompleteDelivery，
到 depart_at 再 EndDelivery。没有自动发奖循环。脚本重载以 ActiveDeliveries
接续原 handle，不重新 Begin；资源过期或角色失效会安全清理，不因清理发奖。
原生玩家单附件宠邮、技能要求、宠物栏和 Loop 不参与系统奖励。

DrainChanges 返回 `{entries}`，每项 `{char_index,reason}`，按具体真人会话合并；
由 Lua 通过现有推送发送 changed。它只是有界内存失效提示，角色复用不继承旧事件，
不保证跨进程可靠通知；界面仍应低频只读核实。

## 公告与管理员

selector 明确 source=saved 或 online_local；saved 使用已保存值，支持离线；
online_local 仅代表本服当前真人。recipient_unit 为 character（默认）或 account；
account 固定该账号所有命中角色中 RegistNumber 最小者。where 支持 all/any/not、
eq/ne/lt/lte/gt/gte/in/exists，最多4层、32个叶子、每个in最多100值。
未知字段与类型拒绝，缺失值不当0，ne也不匹配缺失值。全量必须显式 match_all=true。
扩展字段只接受启动配置的 `{alias,scope,key,value_type}`，scope 为 account/character，
value_type 为 integer/string；账号键由服务增加 #。离线字段从已保存记录读取。

```lua
local selector={source='saved',recipient_unit='character',
  where={field='character.level',op='gte',value=20}}
local draft=assert(SystemMail.CreateDraft(gm,{key='gm:notice:1',title='Notice',
  body='Maintenance at 22:00.',selector=selector}))
assert(SystemMail.PrepareDraft(gm,draft.id))
-- Trusted bounded tick: StepAnnouncement(draft.id,{limit=100}) until ready.
-- After reviewing the fixed recipient count:
assert(SystemMail.PublishAnnouncement(draft.id))
```

管理员逐请求校验真人会话与管理员字段；客户端隐藏按钮不承担权限控制。
CreateDraft/SaveDraft 使用扁平 `{key,title,body,selector,items,gold,expires_at}`，
PrepareAnnouncement 使用 `{key,selector,mail}`。GetAnnouncement 返回原始 mail
模板与当前展示文案 current_title/current_body；发布后仅文案可改，不重置已读，
后续发送仍使用原始模板。名单 ready 后不因升级、下线或字段变化重算。

创建、保存和更正文案在写入前校验最终详情的单帧编码预算，并为后续计数、版本、
时间和最长撤回原因预留空间。纯文本的字节上限仍为1024，编码转义使最终回包超限
时返回 TOO_BIG，不先写入无法读取的草稿，不截断内容。列表每项仅含 id、key、state、
current_title、dispatch_server_number、source、updated_at、recipient_count、counts，
不含正文、奖励或 selector；实际条数还受整页编码预算限制，以 next_cursor 续查。
原始 mail 模板和当前正文分别保留在单封任务详情里。

任务只由 dispatch_server_number 对应服务器写入；OWNER_SERVER 提示切服，
不自动接管。ListAnnouncementJobs 默认本服活动任务；管理员可显式 scope=all
分页浏览。counts 包含 total、pending、sent、skipped、error、withdraw_pending，
及 withdrawn_count、retained_read_count、retained_claimed_count、already_withdrawn_count。
withdrawn 表示处理结束，可以同时存在已读/已领取的保留邮件。

撤回严格为未读 AND 未领取；已读未领取仍可领，已发放奖励不扣回。判定使用当前
角色所属服务器已处理的状态；未知持有服保持待处理。已生成邮件随确切角色转移，
原名单保留选择身份，撤回以 mail_id 指向的当前收件身份判定；未发送部分不重定向。
发信结果未知时，撤回先用固定业务键核实已经生成的邮件并保存名单引用，不能把
尚未链接的已生成邮件当成未发送。登录和摘要同步也会处理这种情况。

条件组合保留比较字段是否存在这一信息：普通 ANY 可由已知分支匹配，NOT 只有在
整个子树的比较依赖都存在时才可取反，包括双重 NOT；条件重排不会改变这一规则。
显式 exists 本身始终有定义，可以用于明确匹配字段存在或缺失。

奖励完成内存发放后，即使普通保存报错仍为 claimed，正常后续保存可再次写回。
保存中途退出、部分写入或人工回档不具备跨表回滚或绝对一次保证。角色删除成功后
邮件保留并标记收件人删除，全部玩家入口拒绝，备份恢复不会自动清标记或重开领取。
维护时必须按确切角色同时核对邮件数据。离线检查之后的并发登录仍属于既有维护边界。
