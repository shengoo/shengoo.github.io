title: nhibernate cascade delete
link: http://www.sheng00.com/374.html
author: admin
description: 
post_id: 374
created: 2012/06/05 14:34:54
created_gmt: 2012/06/05 06:34:54
comment_status: open
post_name: nhibernate-cascade-delete
status: publish
post_type: post

# nhibernate cascade delete

<bag name="FileTagRelations" table="FileTagRelation"  inverse="true" cascade="delete"> 
      <key column="FileID"  foreign-key="FileID" /> 
      <one-to-many class="Entity.FileTagRelationEntity, Entity"/> 
    </bag>