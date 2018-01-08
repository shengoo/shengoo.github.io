title: NHibernate ICriteria多表一对多关联查询
link: http://www.sheng00.com/58.html
author: admin
description: 
post_id: 58
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: nhibernate-icriteria%e5%a4%9a%e8%a1%a8%e4%b8%80%e5%af%b9%e5%a4%9a%e5%85%b3%e8%81%94%e6%9f%a5%e8%af%a2
status: publish
post_type: post

# NHibernate ICriteria多表一对多关联查询

## 配置文件

### Customer.hbm.xml
    
    
    <?xml version="1.0" encoding="utf-8" ?>
    <hibernate-mapping xmlns="urn:nhibernate-mapping-2.2">
      <class name="Entity.CustomerEntity, Entity" table="Customer" lazy="false" >
        <id name="CustomerID" column="CustomerID" type="Int32">
          <generator class="identity" />
        </id>
        <property name="CustomerName" column="CustomerName" type="String" length="10" />
    
        <bag name="Files" table="File" cascade="all">
          <key column="FileID" foreign-key="FileID"></key>
          <one-to-many class="Entity.FileEntity, Entity"/>
        </bag>
      </class>
    </hibernate-mapping>
    

### File.hbm.xml
    
    
    <?xml version="1.0" encoding="utf-8" ?>
    <hibernate-mapping xmlns="urn:nhibernate-mapping-2.2">
      <class name="Entity.FileEntity, Entity" table="File1"  lazy="false">
        <id name="FileID" column="FileID" type="Int32">
          <generator class="identity" />
        </id>
        <property name="FileSize" column="FileSize" type="Int32" length="4" />
        <property name="CustomerID" column="CustomerID" type="Int32" length="4" />
        <many-to-one name="Customer" column="CustomerID" class="Entity.CustomerEntity, Entity" insert="false"/>
        <bag name="DownloadLogs" table="DownloadLog" cascade="all">
          <key column="FileID"/>
          <one-to-many class="Entity.DownloadLogEntity, Entity" />
        </bag>
      </class>
    </hibernate-mapping>
    

### DownloadLog.hbm.xml
    
    
    <?xml version="1.0" encoding="utf-8" ?>
    <hibernate-mapping xmlns="urn:nhibernate-mapping-2.2">
      <class name="Entity.DownloadLogEntity, Entity" table="DownloadLog" lazy="false" >
        <id name="DownloadLogID" column="DownloadLogID" type="Int32">
          <generator class="identity" />
        </id>
        <property name="FileID" column="FileID" type="Int32" length="4" />
        <property name="Times" column="Times" type="Int32" length="4" />
        <many-to-one name="File" column="FileID" class="Entity.FileEntity, Entity" insert="false"/>
      </class>
    </hibernate-mapping>
    

从配置文件上可以看出 每个customer对应多个file，每个file对应多个downloadlog 如果使用icriteria查询customer对应的downloadlog 可以这样写： 
    
    
    public IList<DownloadLogEntity> GetByCustomerID(int customerID)
    {
      ICriteria criteria = NHibernateSession.CreateCriteria(typeof(DownloadLogEntity));
      criteria.CreateAlias("File", "file");
      criteria.CreateAlias("file.Customer", "customer");
      criteria.Add(Expression.Eq("customer.CustomerID",customerID));
      return criteria.List<DownloadLogEntity>();
    }