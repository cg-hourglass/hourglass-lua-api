# 演示

```lua
--  ***************************************************************************************************** --
--  地图库 Map 示范脚本
--                   #基本设置#
--  定义 Lua 地图的 MAPID，不可修改
local LUAMAPID = %地图类型_LUAMAP%;

--                   #使用说明#
--  在游戏中对着自己发送（本地聊天）以下文本即可触发对应的演示：
--
--  copymap,地图类型,地图ID                --> 复制指定地图
--  mazemap,x坐标范围,y坐标范围,地图名      --> 制作指定大小的随机地图
--  delmap,地图ID                          --> 删除指定 Lua 地图
--  getpos,地图ID                          --> 获取指定 Lua 生成的随机地图中的随机可用坐标点
--  getimage                               --> 获取当前人物坐标的地板图档号和物件图档号
--  setimage,图档号                        --> 设置当前人物坐标的地板/物件图档号
--  dumpmap,路径,地图ID,写入ID             --> 将指定 Lua 地图导出成地图文件保存在指定路径中
--  mapsize,地图类型,地图ID                --> 获取指定地图的尺寸
--  dungeontime,地图ID                     --> 获取指定随机地图距离重制还剩的秒数
--
--                   #注意事项#
--  生成随机地图时，实际的房间/墙壁生成在后台异步完成；如果随机地图设置过大，
--  可能需要一段时间才能生成好，请自行测试，不要在回调触发前假设地图已可用。
--  本脚本只依赖 Map/NL/NLG/Char 几个原生库，没有引入额外的框架依赖，
--  便于单独复制出来验证 Map 库的每一个函数。
--  ***************************************************************************************************** --

-- 按分隔符切分字符串的小工具（标准库不带 split，这里用 gmatch 自己实现）
local function splitToken(str, sep)
  local result = {};
  for token in string.gmatch(str, "([^"..sep.."]+)") do
    table.insert(result, token);
  end
  return result;
end

--  创建复制地图
--  参数定义  index: 玩家对象
--            c_mapid: 要复制的地图的 Map ID
--            c_floor: 要复制的地图的 Floor ID
function makeCopyMap(index, c_mapid, c_floor)
  local newFloorID = Map.MakeCopyMap(c_mapid, c_floor);
  if (newFloorID == -1) then
    NLG.SystemMessage(index, "地图复制失败。");
  else
    NLG.SystemMessage(index, "地图"..c_mapid..","..c_floor.."已经成功复制到"..LUAMAPID..","..newFloorID);
    NLG.SystemMessage(index, "使用GM命令[warp "..LUAMAPID.." "..newFloorID.." x坐标 y坐标] 可以移动过去看看哦");
  end
  return;
end

--  创建随机地图
--  参数定义  index: 玩家对象
--            xsiz: 要生成的地图的 x 坐标范围
--            ysiz: 要生成的地图的 y 坐标范围
--            mapName: 地图名
--  函数说明：MakeMazeMap 是需要定义回调函数的，当后台生成完毕后，会触发定义
--  的回调函数，通知生成是否成功。
function makeMazeMap(index, xsiz, ysiz, mapName)
  -- Map.MakeMazeMap 参数简要说明（详见 Map.MakeMazeMap 函数页）
  --[[
    ----------------------------
    回调函数所在文件（这里传 nil，因为回调函数就定义在当前脚本）
    回调函数名
    地图x坐标最大值
    地图y坐标最大值
    地图名
    ---------------------------- 可选参数组：定义调色板号（要么给，要么不给）
    调色板ID
    ---------------------------- 可选参数组：随机生成地图的房间变量（5个要么全给，要么全不给）
    随机地图块大小
    随机地图块x坐标最小值
    随机地图块y坐标最小值
    随机地图块x坐标最大值
    随机地图块y坐标最大值
    ---------------------------- 可选参数组：地图图档信息（3个要么全给，要么全不给）
    地图地板图档编号
    地图其他图档编号
    地图其他物件编号
    ---------------------------- 可选参数组：地图墙面（5个要么全给，要么全不给；只给一部分等于全部不给）
    墙横向图档编号
    墙横向反向图档编号
    墙纵向图档编号
    墙纵向反向图档编号
    墙相交图档编号
    ----------------------------
  --]]
  local newFloorID = Map.MakeMazeMap(nil, "mazeMapDoneCall", xsiz, ysiz, mapName, 0, 30, 30, 30, 30, 30, 9491, 100, 0, 0, 0, 0, 0, 0);
  if (newFloorID == -1) then
    NLG.SystemMessage(index, "地图生成失败。");
  else
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..newFloorID.."已经开始生成了...请稍后");
  end
  return;
end

--  创建随机地图的回调函数
--  参数定义  floorID: 生成的地图的 Floor ID
--            doneflg: 生成结果，1 成功，0 失败
function mazeMapDoneCall(floorID, doneflg)
  if (doneflg == 1) then
    NLG.SystemMessage(-1, "生成地图"..LUAMAPID..","..floorID.."成功！");
    NLG.SystemMessage(-1, "可以通过使用 getpos,"..floorID.." 来获取一个合法的坐标点");
  else
    NLG.SystemMessage(-1, "生成地图"..LUAMAPID..","..floorID.."失败！");
  end
end

--  获取随机地图可用的坐标
--  参数定义  index: 玩家对象
--            floorID: 随机地图的 Floor ID
function getPosition(index, floorID)
  local mapx, mapy = Map.GetAvailablePos(floorID);
  if (mapx == 0 and mapy == 0) then
    NLG.SystemMessage(index, "获取地图可用坐标失败，请重试");
  else
    NLG.SystemMessage(index, "获取地图"..LUAMAPID..","..floorID.."可用坐标"..mapx..","..mapy);
    NLG.SystemMessage(index, "使用GM命令[warp "..LUAMAPID.." "..floorID.." "..mapx.." "..mapy.."] 可以移动过去看看哦");
  end
  return;
end

--  获取当前玩家坐标的地板图档号与物件（obj）图档号
--  参数定义  index: 玩家对象
function getTileandObj(index)
  local nowMap = Char.GetData(index, %对象_MAP%);
  local nowFloor = Char.GetData(index, %对象_地图%);
  local nowXpos = Char.GetData(index, %对象_X%);
  local nowYpos = Char.GetData(index, %对象_Y%);
  local tile, obj = Map.GetImage(nowMap, nowFloor, nowXpos, nowYpos);
  if (tile == nil and obj == nil) then
    -- MapId 越界或该 Floor 查无时，Map.GetImage 只回传单个 0，第二个接收变量会是 nil
    NLG.SystemMessage(index, "获取地图元素失败：地图或楼层不存在。");
    return;
  end
  NLG.SystemMessage(index, "获取地图"..nowMap..","..nowFloor..","..nowXpos..","..nowYpos.."的地图元素[地板:"..tile.."],[物件:"..obj.."]");
  return;
end

--  设置当前玩家坐标的地板图档号与物件（obj）图档号，函数会自动判定图档属于地板还是物件
--  参数定义  index: 玩家对象
--            image: 图档号
function setTileandObj(index, image)
  local nowMap = Char.GetData(index, %对象_MAP%);
  local nowFloor = Char.GetData(index, %对象_地图%);
  local nowXpos = Char.GetData(index, %对象_X%);
  local nowYpos = Char.GetData(index, %对象_Y%);
  local ori_tile, ori_obj = Map.GetImage(nowMap, nowFloor, nowXpos, nowYpos);
  local ret = Map.SetImage(nowMap, nowFloor, nowXpos, nowYpos, image);
  if (ret == 0) then
    NLG.SystemMessage(index, "设置地图元素失败。");
    return;
  end
  local now_tile, now_obj = Map.GetImage(nowMap, nowFloor, nowXpos, nowYpos);
  NLG.SystemMessage(index, "地图"..nowMap..","..nowFloor..","..nowXpos..","..nowYpos.."的地图元素变更[地板:"..ori_tile.."->"..now_tile.."],[物件:"..ori_obj.."->"..now_obj.."]");
  return;
end

--  输出地图文件到本地路径中
--  参数定义  index: 玩家对象
--            path: 本地路径，不包含文件名，文件夹以 "\" 结尾
--            floorID: Lua 地图的 Floor 号
--            writeAsFloor: 写出文件中定义的地图编号
function dumpMapFile(index, path, floorID, writeAsFloor)
  local ret = Map.DumpLuaMap(path, floorID, writeAsFloor);
  if (ret == 0) then
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."输出至文件失败！");
  else
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."已经输出至文件:["..path..LUAMAPID.."_"..floorID.."]");
  end
  return;
end

--  删除 Lua 生成的地图，释放地图编号
--  参数定义  index: 玩家对象
--            floorID: Lua 地图的 Floor 编号
function deleteLuaMap(index, floorID)
  local ret = Map.DelLuaMap(floorID);
  if (ret == 0) then
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."删除失败！");
  else
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."已经成功删除！");
  end
  return;
end

--  获取地图尺寸
--  参数定义  index: 玩家对象
--            mapid: 要查询的地图 Map ID
--            floorID: 要查询的地图 Floor ID
function getMapSizeInfo(index, mapid, floorID)
  local xsize, ysize = Map.GetMapSize(mapid, floorID);
  if (xsize == -1 and ysize == -1) then
    NLG.SystemMessage(index, "地图"..mapid..","..floorID.."不存在。");
  else
    NLG.SystemMessage(index, "地图"..mapid..","..floorID.."的尺寸为 "..xsize.."x"..ysize);
  end
  return;
end

--  获取随机地图距离重置还剩的秒数
--  参数定义  index: 玩家对象
--            floorID: 要查询的地图 Floor ID
function getDungeonExpire(index, floorID)
  local remainSec = Map.GetDungeonExpireTime(floorID);
  if (remainSec == -1) then
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."不是被追踪的活跃地城。");
  else
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."距离重置还剩 "..remainSec.." 秒。");
  end
  return;
end

--  本地聊天命令分发：把玩家发出的一句本地聊天当作调试命令解析并执行
--  参数定义  index: 说话的玩家对象，msg: 聊天内容，col/range/size: 引擎附带的显示参数
function MapProc_TalkEvent(index, msg, col, range, size)
  local token = splitToken(msg, ",");
  if (token[1] == "copymap") then
    local m = tonumber(token[2]);
    local f = tonumber(token[3]);
    makeCopyMap(index, m, f);
    return 1;
  end
  if (token[1] == "mazemap") then
    local xsiz = tonumber(token[2]);
    local ysiz = tonumber(token[3]);
    local MapName = token[4];
    makeMazeMap(index, xsiz, ysiz, MapName);
    return 1;
  end
  if (token[1] == "delmap") then
    local f = tonumber(token[2]);
    deleteLuaMap(index, f);
    return 1;
  end
  if (token[1] == "getpos") then
    local f = tonumber(token[2]);
    getPosition(index, f);
    return 1;
  end
  if (msg == "getimage") then
    getTileandObj(index);
    return 1;
  end
  if (token[1] == "setimage") then
    local image = tonumber(token[2]);
    setTileandObj(index, image);
    return 1;
  end
  if (token[1] == "dumpmap") then
    local path = token[2];
    local floorID = tonumber(token[3]);
    local writeAsFloor = tonumber(token[4]);
    dumpMapFile(index, path, floorID, writeAsFloor);
    return 1;
  end
  if (token[1] == "mapsize") then
    local m = tonumber(token[2]);
    local f = tonumber(token[3]);
    getMapSizeInfo(index, m, f);
    return 1;
  end
  if (token[1] == "dungeontime") then
    local f = tonumber(token[2]);
    getDungeonExpire(index, f);
    return 1;
  end
  -- 不是本脚本认识的命令：不拦截，正常显示聊天内容
  return 1;
end

-- 注册本地聊天事件：把当前脚本文件里定义的 MapProc_TalkEvent 挂到 EVENT_TALK 上
NL.RegTalkEvent(nil, "MapProc_TalkEvent");

```
