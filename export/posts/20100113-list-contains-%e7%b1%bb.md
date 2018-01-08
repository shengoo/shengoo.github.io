title: list contains 类
link: http://www.sheng00.com/30.html
author: admin
description: 
post_id: 30
created: 2010/01/13 08:00:00
created_gmt: 2010/01/13 00:00:00
comment_status: open
post_name: list-contains-%e7%b1%bb
status: publish
post_type: post

# list contains 类

Subscription sub = new Subscription();
    sub.Appname = subName;
    if (this.Subscriptions.Contains(sub,new SubcriptionComparer<Subscription>()))
      return true;
    else
      return false;
    
    class SubcriptionComparer<T> : IEqualityComparer<T>
    where T : Subscription
    {
    
      public int GetHashCode(T obj)
      {
        return obj.GetHashCode();
      }
    
      public bool Equals(T t1, T t2)
      {
        return t1.Appname == t2.Appname;
      }
    }