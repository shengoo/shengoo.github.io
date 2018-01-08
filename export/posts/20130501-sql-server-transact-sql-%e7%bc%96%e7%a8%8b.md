title: SQL Server Transact-SQL 编程
link: http://www.sheng00.com/530.html
author: admin
description: 
post_id: 530
created: 2013/05/01 17:21:38
created_gmt: 2013/05/01 09:21:38
comment_status: open
post_name: sql-server-transact-sql-%e7%bc%96%e7%a8%8b
status: publish
post_type: post

# SQL Server Transact-SQL 编程

T-SQL语句用于管理SQL Server数据库引擎实例，创建和管理数据库对象，以及查询、插入、修改和删除数据。 ? 变量 1、 局部变量（Local Variable） 局部变量是用户可以自定义的变量，它的作用范围是仅在程序内部，在程序中通常用来储存从表中查询到的数据或当做程序执行过程中的暂存变量。使用局部变量必须以@开头，而且必须用declare命令后才能使用。 基本语法： 声明变量 
    
    
    declare @变量名 变量类型 [@变量名 变量类型]

为变量赋值 
    
    
    set @变量名 = 变量值;
    select @变量名 = 变量值;

示例： \--局部变量 
    
    
    declare @id char(10)--声明一个长度的变量id
    declare @age int --声明一个int类型变量age
    select @id = 22 --赋值操作
    set @age = 55 --赋值操作
    print convert(char(10), @age) + '#' + @id
    select @age, @id
    go

简单hello world示例 
    
    
    declare @name varchar(20);
    declare @result varchar(200);
    set @name = 'jack';
    set @result = @name + ' say: hello world!';
    select @result;

查询数据示例 
    
    
    declare @id int, @name varchar(20);
    set @id = 1;
    select @name = name from student where id = @id;
    select @name;

select赋值 
    
    
    declare @name varchar(20);
    select @name = 'jack';
    select * from student where name = @name;

从上面的示例可以看出，局部变量可用于程序中保存临时数据、传递数据。Set赋值一般用于赋值指定的常量个变量。而select多用于查询的结果进行赋值，当然select也可以将常量赋值给变量。 注意：在使用select进行赋值的时候，如果查询的结果是多条的情况下，会利用最后一条数据进行赋值，前面的赋值结果将会被覆盖。 2、 全局变量（Global Variable） 全局变量是系统内部使用的变量，其作用范围并不局限于某一程序而是任何程序均可随时调用的。全局变量一般存储一些系统的配置设定值、统计数据。 全局变量 
    
    
    select @@identity;--最后一次自增的值
    select identity(int, 1, 1) as id into tab from student;--将studeng表的烈属，以/1自增形式创建一个tab
    select * from tab;
    select @@rowcount;--影响行数
    select @@cursor_rows;--返回连接上打开的游标的当前限定行的数目
    select @@error;--T-SQL的错误号
    select @@procid;

\--配置函数 
    
    
    set datefirst 7;--设置每周的第一天，表示周日
    select @@datefirst as '星期的第一天', datepart(dw, getDate()) AS '今天是星期';
    select @@dbts;--返回当前数据库唯一时间戳
    set language 'Italian';
    select @@langId as 'Language ID';--返回语言id
    select @@language as 'Language Name';--返回当前语言名称
    select @@lock_timeout;--返回当前会话的当前锁定超时设置（毫秒）
    select @@max_connections;--返回SQL Server 实例允许同时进行的最大用户连接数
    select @@MAX_PRECISION AS 'Max Precision';--返回decimal 和numeric 数据类型所用的精度级别
    select @@SERVERNAME;--SQL Server 的本地服务器的名称
    select @@SERVICENAME;--服务名
    select @@SPID;--当前会话进程id
    select @@textSize;
    select @@version;--当前数据库版本信息

\--系统统计函数 
    
    
    select @@CONNECTIONS;--连接数
    select @@PACK_RECEIVED;
    select @@CPU_BUSY;
    select @@PACK_SENT;
    select @@TIMETICKS;
    select @@IDLE;
    select @@TOTAL_ERRORS;
    select @@IO_BUSY;
    select @@TOTAL_READ;--读取磁盘次数
    select @@PACKET_ERRORS;--发生的网络数据包错误数
    select @@TOTAL_WRITE;--sqlserver执行的磁盘写入次数

? 输出语句 T-SQL支持输出语句，用于显示结果。常用输出语句有两种： 基本语法 
    
    
    print 变量或表达式
    select 变量或表达式

示例 
    
    
    select 1 + 2;
    select @@language;
    select user_name();
    
    print 1 + 2;
    print @@language;
    print user_name();

print在输出值不少字符串的情况下，需要用convert转换成字符串才能正常输出，而且字符串的长度在超过8000的字符以后，后面的将不会显示。 ? 逻辑控制语句 1、 if-else判断语句 语法 
    
    
    if <表达式>
    <命令行或程序块>
    else if <表达式>
    <命令行或程序块>
    else
    <命令行或程序块>

示例 if简单示例 
    
    
    if 2 > 3
    print '2 > 3';
    else
    print '2 < 3'; if (2 < 3)
    print '2 > 3';
    else if (3 > 2)
    print '3 > 2';
    else
    print 'other';

简单查询判断 
    
    
    declare @id char(10),
    @pid char(20),
    @name varchar(20);
    set @name = '广州';
    select @id = id from ab_area where areaName = @name;
    select @pid = pid from ab_area where id = @id;
    print @id + '#' + @pid;
    
    
    if @pid > @id
    begin
    print @id + '%';
    select * from ab_area where pid like @id + '%';
    end
    else
    begin
    print @id + '%';
    print @id + '#' + @pid;
    select * from ab_area where pid = @pid;
    end
    go

2、 while…continue…break循环语句 基本语法 
    
    
    while <表达式>
    begin
    <命令行或程序块>
    [break]
    [continue]
    <命令行或程序块>
    end

示例 \--while循环输出到 
    
    
    declare @i int;
    set @i = 1;
    while (@i < 11)
    begin
    print @i;
    set @i = @i + 1;
    end
    go

\--while continue 输出到 
    
    
    declare @i int;
    set @i = 1;
    while (@i < 11)
    begin
    if (@i < 5) begin set @i = @i + 1; continue; end print @i; set @i = @i + 1; end go --while break 输出到 declare @i int; set @i = 1; while (1 = 1) begin print @i; if (@i >= 5)
    begin
    set @i = @i + 1;
    break;
    end
    set @i = @i + 1;
    end
    go

3、 case 基本语法 
    
    
    case
    when <条件表达式> then <运算式>
    when <条件表达式> then <运算式>
    when <条件表达式> then <运算式>
    [else <运算式>]
    end

示例 
    
    
    select *,
    case sex
    when 1 then '男'
    when 0 then '女'
    else '火星人'
    end as '性别'
    from student;
    
    select areaName, '区域类型' = case
    when areaType = '省' then areaName + areaType
    when areaType = '市' then 'city'
    when areaType = '区' then 'area'
    else 'other'
    end
    from ab_area;

4、 其他语句 批处理语句go 
    
    
    Use master
    Go

延时执行，类似于定时器、休眠等 
    
    
    waitfor delay '00:00:03';--定时三秒后执行
    print '定时三秒后执行';