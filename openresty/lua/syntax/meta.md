# 元表

Lua语言中的每个类型的值都有一套可预见的操作集合。例如数值类型可以做加减乘除，也可以和字符串拼接。

元表可以修改一个值在面对一个未知操作时的行为。

Lua语言中每一个值都可以有元表。每一个表和用户数据类型都有各自独立的元表，而其他类型的值则共享对应类型所属的同一个元表。

元表的设置与获取API

```lua
-- 设置元表，返回值为第一个参数 table
setmetatable(table, metatable)

-- 获取元表（的地址），返回的是元表的地址
getmetatable(object)
```



查找元方法的顺序：如果第一个值有元表且元表中存在所需的元方法，那么就是使用这个元方法；如果第二个值有元表且元表中存在所需的元方法，则使用这个元方法；否则Lua会抛出异常。
