title: automapper list
link: http://www.sheng00.com/50.html
author: admin
description: 
post_id: 50
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: automapper-list
status: publish
post_type: post

# automapper list

Mapper.CreateMap<Source, Destination>();
    
    var sources = new[]
    {
    new Source {Value = 5},
    new Source {Value = 6},
    new Source {Value = 7}
    };
    
    IEnumerable<Destination> ienumerableDest = Mapper.Map<Source[], IEnumerable<Destination>>(sources);
    ICollection<Destination> icollectionDest = Mapper.Map<Source[], ICollection<Destination>>(sources);
    IList<Destination> ilistDest = Mapper.Map<Source[], IList<Destination>>(sources);
    List<Destination> listDest = Mapper.Map<Source[], List<Destination>>(sources);
    Destination[] arrayDest = Mapper.Map<Source[], Destination[]>(sources);
    

如果sources不是数组的话，可以调用`ToArray<Destination>()`转换一下