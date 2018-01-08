title: how to catch NULL values using case statement
link: http://www.sheng00.com/995.html
author: admin
description: 
post_id: 995
created: 2013/10/29 17:15:56
created_gmt: 2013/10/29 09:15:56
comment_status: open
post_name: how-to-catch-null-values-using-case-statement
status: publish
post_type: post

# how to catch NULL values using case statement

select contactid,Title,FirstName,MiddleName,
    case ISNULL(MiddleName, 'NULLVALUE')
    when 'R.' then 'Robert'
    when 'B.' then 'Bids'
    when 'J.' then 'John'
    when 'NULLVALUE' then 'New Name'
    else 'No Name'
    end, LastName from Person.Contact