title: NHibernate查询语言(HQL)
link: http://www.sheng00.com/70.html
author: admin
description: 
post_id: 70
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: nhibernate%e6%9f%a5%e8%af%a2%e8%af%ad%e8%a8%80hql
status: publish
post_type: post

# NHibernate查询语言(HQL)

## NHibernate中的查询方法

在NHibernate中提供了三种查询方式给我们选择：NHibernate查询语言(HQL，NHibernate Query Language)、条件查询(Criteria API，Query By Example(QBE)是Criteria API的一种特殊情况)、原生SQL(Literal SQL，T-SQL、PL/SQL)。每个人有不同的喜好和特长，可以根据自己的情况选择使用其中的一种或几种。这一节我们介绍NHibernate查询 语言(HQL，NHibernate Query Language)。 

## NHibernate查询语言(HQL)

NHibernate查询语言(HQL，NHibernate Query Language)是NHibernate特有的基于面向对象的SQL查询语言，它具有继承、多态和关联等特性。实际上是用OOP中的对象和属性映射了数据库中的表和列。 例如这一句：select c.Firstname from Customer c Customer是数据库表，Firstname是列；而对于HQL：Customer是一个对象，Firstname是Customer对象的属性。相比之下SQL语句非常灵活，但是没有编译时语法验证支持。 本节介绍基础语法：from子句，select子句，where子句，order by子句，group by子句并分别举出可以运行的实例。至于关联和连接，多态(polymorphism)查询，子查询在以后具体实例中学习。注意：HQL不区分大小写。 注意：由于篇幅有限，我在这里仅仅贴出了数据访问层的代码，就是在业务逻辑层可以直接调用的方法。测试这些方法的代码就没有贴出来了，你可以下载本 系列的 源代码仔细看看测试这些方法的代码。这节，我们在上一节源代码的基础上，在数据访问层中新建QueryHQL.cs类用于编写HQL查询方法，在数据访问 的测试层新建一QueryHQLFixture.cs类用于测试。 

### 1.from子句

顾名思义，同SQL语句类似： 1.简单用法：返回表中所有数据。 
    
    
    public IList From()
    {
     //返回所有Customer类的实例
     return _session.CreateQuery("from Customer")
            .List();
    }

2.使用别名：使用as来赋予表的别名，as可以省略。 
    
    
    public IList FromAlias()
    {
      //返回所有Customer类的实例，Customer赋予了别名customer
      return _session.CreateQuery("from Customer as customer")
      .List();
    }
    

3.笛卡尔积：出现多个类，或者分别使用别名，返回笛卡尔积或者称为“交叉”连接。 

### 2.select子句

1.简单用法：在结果集中返回指定的对象和属性。 
    
    
    public IList Select()
    {
      //返回所有Customer的CustomerId
      return _session
        .CreateQuery("select c.CustomerId from Customer c")
        .List();
    }
    

2.数组：用Object[]的数组返回多个对象和/或多个属性，或者使用特殊的elements功能，注意一般要结合group by使用。 
    
    
    public IList SelectObject()
    {
      return _session
        .CreateQuery("select c.Firstname, count(c.Firstname) from Customer c group by c.Firstname")
        .List();
    }
    

或者使用类型安全的.NET对象，以后在实例中说明。 3.统计函数：用Object[]的数组返回属性的统计函数的结果，注意统计函数的变量也可以是集合`count(elements(c.CustomerId) )`
    
    
    public IList AggregateFunction()
    {
      return _session
        .CreateQuery("select avg(c.CustomerId),sum(c.CustomerId),count(c) from Customer c")
        .List();
    }
    

4.Distinct用法：distinct和all关键字的用法和语义与SQL相同。实例：获取不同Customer的FirstName。 
    
    
    public IList Distinct()
    {
      return _session
        .CreateQuery("select distinct c.Firstname from Customer c")
        .List();
    }
    

### 3.where子句

where子句让你缩小你要返回的实例的列表范围。 
    
    
    public IList Where()
    {
      return _session
        .CreateQuery("select from Customer c where c.Firstname='YJing'")
        .List();
    }
    

where子句允许出现的表达式包括了在SQL中的大多数情况： 

  * 数学操作符：+, -, *, /
  * 真假比较操作符：=, >=, <=, <>, !=, like
  * 逻辑操作符：and, or, not
  * 字符串连接操作符：||
  * SQL标量函数：upper(),lower()
  * 没有前缀的( )：表示分组
  * in, between, is null
  * 位置参数：?
  * 命名参数：:name, :start_date, :x1
  * SQL文字：'foo', 69, '1970-01-01 10:00:01.0'
  * 枚举值或常量：Color.Tabby

### 4.order by子句

按照任何返回的类或者组件的属性排序：asc升序、desc降序。 
    
    
    public IList Orderby()
    {
      return _session
        .CreateQuery("select from Customer c order by c.Firstname asc,c.Lastname desc")
        .List();
    }
    

### 5.group by子句

按照任何返回的类或者组件的属性进行分组。 
    
    
    public IList Groupby()
    {
      return _session
        .CreateQuery("select c.Firstname, count(c.Firstname) from Customer c group by c.Firstname")
        .List();
    }
    

## 实例分析

好的，以上基本的查询的确非常简单，我们还是参考一下实例，分析一下我们如何写HQL查询吧！ 实例1：按照FirstName查询顾客： 
    
    
    public IList GetCustomersByFirstname(string firstname)
    {
      //写法1
      //return _session
      // .CreateQuery("select from Customer c where c.Firstname='" + firstname + "'")
      // .List();
      //写法2:位置型参数
      //return _session
      // .CreateQuery("select from Customer c where c.Firstname=?")
      // .SetString(0, firstname)
      // .List();
    
      //写法3:命名型参数(推荐)
      return _session
        .CreateQuery("select from Customer c where c.Firstname=:fn")
        .SetString("fn", firstname)
        .List();
    }
    

书写HQL参数有四种写法： 

  * 写法1：可能会引起SQL注入，不要使用。
  * 写法2：ADO.NET风格的?参数，NHibernate的参数从0开始计数。
  * 写法3：命名参数用:name的形式在查询字符串中表示，这时IQuery接口把实际参数绑定到命名参数。
  * 写法4：命名的参数列表，把一些参数添加到一个集合列表中的形式，比如可以查询数据是否在这个集合列表中。
使用命名参数有一些好处：命名参数不依赖于它们在查询字符串中出现的顺序；在同一个查询中可以使用多次；它们的可读性好。所以在书写HQL使用参数的时候推荐命名型参数形式。 测试一下这个方法吧：看看数据库中Firstname为“YJingLee”的记录个数是否是1条，并可以判断查询出来的数据的FirstName属性是不是“YJingLee”。 
    
    
    [Test]
    public void GetCustomerByFirstnameTest()
    {
      IList customers = _queryHQL.GetCustomersByFirstname("YJingLee");
      Assert.AreEqual(1, customers.Count);
      foreach (var c in customers)
      {
        Assert.AreEqual("YJingLee", c.Firstname);
      }
    }
    

实例2：获取顾客ID大于CustomerId的顾客： 
    
    
    public IList GetCustomersWithCustomerIdGreaterThan(int customerId)
    {
      return _session
        .CreateQuery("select from Customer c where c.CustomerId > :cid")
        .SetInt32("cid", customerId)
        .List();
    }