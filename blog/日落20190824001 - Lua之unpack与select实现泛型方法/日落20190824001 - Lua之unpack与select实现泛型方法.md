## 环境
> 系统：Windows 10
> 引擎：Lua5.3.5

## 目的
> 通过实例使用unpack与select函数，了解lua的多重返回值和变长参数，以实现泛型方法。

## 实例
（1）使用unpack函数可以返回多个值。

```
function aaa()
	local a = {"hello kitty","tt"}
	print(string.find(unpack(a)))
end

aaa()
```



（2）但在lua5.3.5版本，用上面的代码，就会报错：

> ...... attempt to call a nil value (global 'unpack')



（3）因为lua5.3.5的公共函数库里没有unpack，所以需要手动来一个。

```
function unpack(t, i)
	i = i or 1
	if t[i] then
		return t[i], unpack(t, i + 1)
	end
end

function aaa()
	local a = {"hello kitty","tt"}
	print(string.find(unpack(a)))
end

aaa()
```



（4）加入select的运用，可以通过变长参数的机制，实现泛型方法。

```
function unpack(t, i)
	i = i or 1
	if t[i] then
		return t[i], unpack(t, i + 1)
	end
end

function aaa(...)
	local f = select(1, ...) -- 即select(1, ...)第一个参数：string.find
	local a
	for i = 2, select('#', ...) do -- select('#', ...)即变长参数的数量
		a = select(i, ...) -- 从变长参数第i个开始
	end
	print(f(unpack(a)))
end

aaa(string.find, {"hello kitty","tt"})
```



（5）稍微改变一下，把入参从table类型切分开，个人觉得比较好看。

```
function unpack(t, i)
	i = i or 1
	if t[i] then
		return t[i], unpack(t, i + 1)
	end
end

function aaa(...)
	local f = select(1, ...) -- 即select(1, ...)第一个参数：string.find
	local a = {}
	for i = 2, select('#', ...) do -- select('#', ...)即变长参数的数量
		a[#a+1] = select(i, ...) -- 从变长参数第i个开始
	end
	print(f(unpack(a)))
end

aaa(string.find, "hello kitty", "tt")
```



以上结果均为：

```
9	10
[Finished in 0.1s]
```



以上简单回顾。

## 参考资料：

《Lua程序设计（第二版）》第5.1节与第5.2节