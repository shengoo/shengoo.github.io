title: The text, ntext, and image data types cannot be compared or sorted, except when using IS NULL or LIKE operator.
link: http://www.sheng00.com/1065.html
author: admin
description: 
post_id: 1065
created: 2014/02/13 14:37:52
created_gmt: 2014/02/13 06:37:52
comment_status: open
post_name: the-text-ntext-and-image-data-types-cannot-be-compared-or-sorted-except-when-using-is-null-or-like-operator
status: publish
post_type: post

# The text, ntext, and image data types cannot be compared or sorted, except when using IS NULL or LIKE operator.

SQL Server Error Messages - Msg 306

Error Message
    
    
    Server: Msg 306, Level 16, State 1, Line 1
    The text, ntext, and image data types cannot be compared
    or sorted, except when using IS NULL or LIKE operator.

Causes

NTEXT data types are used for variable-length of Unicode data, TEXT data types are used for variable-length non-Unicode data while IMAGE data types are used for variable-length binary data.

One way of getting this error is when including a column of TEXT, NTEXT or IMAGE data type in the ORDER BY clause. To illustrate, here’s a script that will generate this error message:
    
    
    CREATE TABLE [dbo].[BookSummary] (
        [BookSummaryID]     INT NOT NULL IDENTITY(1, 1),
        [BookName]          NVARCHAR(200),
        [Author]            NVARCHAR(100),
        [Summary]           NTEXT
    )
    
    SELECT * FROM [dbo].[BookSummary]
    ORDER BY [Summary]
    
    Msg 306, Level 16, State 2, Line 2
    The text, ntext, and image data types cannot be compared or sorted,
    except when using IS NULL or LIKE operator.

Another way of getting this error is including a column of TEXT, NTEXT or IMAGE data type as part of a GROUP BY clause, as can be seen in the following script:
    
    
    SELECT [Summary], COUNT(*)
    FROM [dbo].[BookSummary]
    GROUP BY [Summary]
    
    Msg 306, Level 16, State 2, Line 3
    The text, ntext, and image data types cannot be compared or sorted,
    except when using IS NULL or LIKE operator.

Note that ntext, text and image data types will be removed in a future version of SQL Server and usage of these data types should be avoided. When using SQL Server 2005 or later, use nvarchar(max), varchar(max) and varbinary(max), respectively, instead.

Solution / Workaround:

To work around this error, the TEXT or NEXT column needs to be converted to VARCHAR or NVARCHAR when used in either the ORDER BY clause or the GROUP BY clause of a SELECT statement.

In the first example, using SQL Server 2000, the NTEXT column can be converted to NVARCHAR(4000) in the ORDER BY clause to avoid the error and generate the result desired:
    
    
    SELECT * FROM [dbo].[BookSummary]
    ORDER BY CAST([Summary] AS NVARCHAR(4000))

Using SQL Server 2005 or SQL Server 2008 (or later), instead of NVARCHAR(4000), the NTEXT column can be converted to NVARCHAR(MAX):
    
    
    SELECT * FROM [dbo].[BookSummary]
    ORDER BY CAST([Summary] AS NVARCHAR(MAX))

As for the second example, using SQL Server 2000, the same can be done with the NTEXT column in the GROUP BY clause to avoid the error:
    
    
    SELECT CAST([Summary] AS NVARCHAR(4000)) AS [Summary], COUNT(*)
    FROM [dbo].[BookSummary]
    GROUP BY CAST([Summary] AS NVARCHAR(4000))

Using SQL Server 2005 or SQL Server 2008 (or later), instead of NVARCHAR(4000), the NTEXT column can be converted to NVARCHAR(MAX):
    
    
    SELECT CAST([Summary] AS NVARCHAR(MAX)) AS [Summary], COUNT(*)
    FROM [dbo].[BookSummary]
    GROUP BY CAST([Summary] AS NVARCHAR(MAX))

To totally avoid getting this error message, if using SQL Server 2005 or SQL Server 2008, it is suggested that any TEXT, NTEXT or IMAGE data types be converted to VARCHAR(MAX), NVARCHAR(MAX) and VARBINARY(MAX), respectively.