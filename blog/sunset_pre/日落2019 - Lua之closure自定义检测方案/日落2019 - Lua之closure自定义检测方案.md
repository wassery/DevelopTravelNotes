## 环境

> 系统：Windows 10
> 引擎：Lua5.3.5

## 目的

> 根据closure的元机制给函数植入自定义检测方案

## 实例

```
testFunc = function ()
	print('testFunc')
end

print('------------before------------')
testFunc()

--[[
此处使用语法糖 local function checkFunc(param)，
相当于先定义checkFunc这个变量，再赋值。
]]
local function checkFunc(param)
	-- 此处为检测方案
	local today = os.date('%d', os.time())
	return today == '01'
end

local oldFunc = testFunc
testFunc = function()
	if checkFunc() then
		oldFunc()
	else
		print('access failed')
	end
end

print('------------after------------')
testFunc()
```

## 结果

上述例子，如果系统时间是本月1日，则

```
------------before------------
testFunc
------------after------------
testFunc
[Finished in 0.1s]
```

如果系统时间是本月9日，则

```
------------before------------
testFunc
------------after------------
access failed
[Finished in 0.1s]
```



以上简单回顾。

## 参考资料：

《Lua程序设计（第二版）》第6.1节与第6.2节