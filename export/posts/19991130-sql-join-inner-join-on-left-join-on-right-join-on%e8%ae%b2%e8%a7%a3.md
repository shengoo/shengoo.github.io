title: sql join inner join on, left join on, right join on讲解
link: http://www.sheng00.com/56.html
author: admin
description: 
post_id: 56
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: sql-join-inner-join-on-left-join-on-right-join-on%e8%ae%b2%e8%a7%a3
status: publish
post_type: post

# sql join inner join on, left join on, right join on讲解

**1.****理论**

    只要两个表的公共字段有匹配值，就将这两个表中的记录组合起来。

    个人理解：以一个共同的字段求两个表中符合要求的交集，并将每个表符合要求的记录以共同的字段为牵引合并起来。

  
**语法**

FROM table1 INNER JOIN table2 ON table1 . field1 compopr table2 . field2

INNER JOIN 操作包含以下部分：

**部分**

**说明**

table1, table2

要组合其中的记录的表的名称。

field1，field2

要联接的字段的名称。如果它们不是数字，则这些字段的数据类型必须相同，并且包含同类数据，但是，它们不必具有相同的名称。

compopr

任何关系比较运算符：“=”、“<”、“>”、“<=”、“>=”或者“<>”。

**  
说明**

    可以在任何 FROM 子句中使用 INNER JOIN 操作。这是最常用的联接类型。只要两个表的公共字段上存在相匹配的值，Inner 联接就会组合这些表中的记录。  
  


    可以将 INNER JOIN 用于 Departments 及 Employees 表，以选择出每个部门的所有雇员。而要选择所有部分（即使某些部门中并没有被分配雇员）或者所有雇员（即使某些雇员没有分配到任何部门），则可以通过 LEFT JOIN 或者 RIGHT JOIN 操作来创建外部联接。如果试图联接包含备注或 OLE 对象数据的字段，将发生错误。  
  


    可以联接任何两个相似类型的数字字段。例如，可以联接自动编号和长整型字段，因为它们均是相似类型。然而，不能联接单精度型和双精度型类型字段。  
  


    下例展示了如何通过 CategoryID 字段联接 Categories 和 Products 表：

SELECT CategoryName, ProductName

FROM Categories INNER JOIN Products

ON Categories.CategoryID = Products.CategoryID;

  
在前面的示例中，CategoryID 是被联接字段，但是它不包含在查询输出中，因为它不包含在 SELECT 语句中。若要包含被联接字段，请在 SELECT 语句中包含该字段名，在本例中是指 Categories.CategoryID。

  
也可以在 JOIN 语句中链接多个 ON 子句，请使用如下语法：

SELECT fields  
FROM table1 INNER JOIN table2  
ON table1.field1 compopr table2.field1 AND  
ON table1.field2 compopr table2.field2) OR  
ON table1.field3 compopr table2.field3)];

  
也可以通过如下语法嵌套 JOIN 语句：

SELECT fields  
FROM table1 INNER JOIN  
(table2 INNER JOIN [( ]table3  
[INNER JOIN [( ]tablex [INNER JOIN ...)]   
ON table3.field3 compopr tablex.fieldx)]  
ON table2.field2 compopr table3.field3)   
ON table1.field1 compopr table2.field2;