title: DataTableSerializer datatable序列化成对象 datatable to entity serialization
link: http://www.sheng00.com/1156.html
author: admin
description: 
post_id: 1156
created: 2014/07/01 10:21:35
created_gmt: 2014/07/01 02:21:35
comment_status: open
post_name: datatableserializer-datatable%e5%ba%8f%e5%88%97%e5%8c%96%e6%88%90%e5%af%b9%e8%b1%a1-datatable-to-entity-serialization
status: publish
post_type: post

# DataTableSerializer datatable序列化成对象 datatable to entity serialization

public class DataTableSerializer
    {
      public static List ToList(DataTable dt)
      {
        var list = new List();
        if (dt == null || dt.Rows.Count == 0)
          return list;//return empty list instead of null object
        list.AddRange(from DataRow row in dt.Rows select ToEntity(row));
        return list;
      }
    
      public static T ToEntity( DataRow row)
      {
        var objType = typeof(T);
        var obj = Activator.CreateInstance();
    
        foreach (DataColumn column in row.Table.Columns)
        {
          var property = objType.GetProperty(column.ColumnName,
              BindingFlags.Public | BindingFlags.Instance | BindingFlags.IgnoreCase);
          if (property == null || !property.CanWrite)
          {
            continue;
          }
          var value = row[column.ColumnName];
          if (value == DBNull.Value)
          {
            value = null;
          }
          else
          {
            //add what you need.
            //if (column.DataType == typeof (DateTime))
            //{
            //    value = ((DateTime)value).ToString("yyyy-MM-dd");
            //}
          }
    
          property.SetValue(obj, value, null);
    
        }
        return obj;
      }
    }