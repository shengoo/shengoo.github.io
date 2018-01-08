title: LINQ中.AsEnumerable() 和 .ToList() 的区别：
link: http://www.sheng00.com/1031.html
author: admin
description: 
post_id: 1031
created: 2013/12/30 11:19:08
created_gmt: 2013/12/30 03:19:08
comment_status: open
post_name: linq%e4%b8%ad-asenumerable-%e5%92%8c-tolist-%e7%9a%84%e5%8c%ba%e5%88%ab%ef%bc%9a
status: publish
post_type: post

# LINQ中.AsEnumerable() 和 .ToList() 的区别：

* `.AsEnumerable()`延迟执行，不会立即执行。当你调用`.AsEnumerable()`的时候，实际上什么都没有发生。
  * `.ToList()`立即执行
  * 当你需要操作结果的时候，用`.ToList()`，否则，如果仅仅是用来查询不需要进一步使用结果集，并可以延迟执行，就用`.AsEnumerable()`/`IEnumerable` /`IQueryable`
  * .AsEnumerable()虽然延迟执行，但还是访问数据库，而.ToList()直接取得结果放在内存中。比如我们需要显示两个部门的员工时，部门可以先取出放置在List中，然后再依次取出各个部门的员工，这时访问的效率要高一些，因为不需要每次都访问数据库去取出部门。
  * `IQueryable`实现了`IEnumberable`接口。但`IEnumerable` 换成`IQueryable`后速度提高很多。原因： `IQueryable`接口与`IEnumberable`接口的区别： `IEnumerable` 泛型类在调用自己的SKip 和 Take 等扩展方法之前数据就已经加载在本地内存里了，而`IQueryable` 是将`Skip ,take` 这些方法表达式翻译成T-SQL语句之后再向SQL服务器发送命令，它并不是把所有数据都加载到内存里来才进行条件过滤。
  * `IEnumerable`跑的是Linq to Object，强制从数据库中读取所有数据到内存先。