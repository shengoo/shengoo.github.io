title: Web API:Handling Circular Object References
link: http://www.sheng00.com/909.html
author: admin
description: 
post_id: 909
created: 2013/08/22 09:36:38
created_gmt: 2013/08/22 01:36:38
comment_status: open
post_name: web-apihandling-circular-object-references
status: publish
post_type: post

# Web API:Handling Circular Object References

By default, the JSON and XML formatters write all objects as values. If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice. This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph. Consider the following object models and controller. 
    
    
    public class Employee
    {
        public string Name { get; set; }
        public Department Department { get; set; }
    }
    
    public class Department
    {
        public string Name { get; set; }
        public Employee Manager { get; set; }
    }
    
    public class DepartmentsController : ApiController
    {
        public Department Get(int id)
        {
            Department sales = new Department() { Name = "Sales" };
            Employee alice = new Employee() { Name = "Alice", Department = sales };
            sales.Manager = alice;
            return sales;
        }
    }

Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client. To preserve object references in JSON, add the following code to?**Application_Start**?method in the Global.asax file: 
    
    
    var json = GlobalConfiguration.Configuration.Formatters.JsonFormatter;
    json.SerializerSettings.PreserveReferencesHandling = 
        Newtonsoft.Json.PreserveReferencesHandling.All;

Now the controller action will return JSON that looks like this: 
    
    
    {"$id":"1","Name":"Sales","Manager":{"$id":"2","Name":"Alice","Department":{"$ref":"1"}}}

Notice that the serializer adds an "$id" property to both objects. Also, it detects that the Employee.Department? property creates a loop, so it replaces the value with an object reference: {"$ref":"1"}. Object references are not standard in JSON. Before using this feature, consider whether your clients will be able to parse the results. It might be better simply to remove cycles from the graph. For example, the link from Employee back to Department is not really needed in this example. To preserve object references in XML, you have two options. The simpler option is to add`[DataContract(IsReference=true)]`?to your model class. The?_IsReference_?parameter enables oibject references. Remember that?**DataContract**?makes serialization opt-in, so you will also need to add?**DataMember**?attributes to the properties: 
    
    
    [DataContract(IsReference=true)]
    public class Department
    {
        [DataMember]
        public string Name { get; set; }
        [DataMember]
        public Employee Manager { get; set; }
    }

Now the formatter will produce XML similar to following: 
    
    
    <Department xmlns:i="http://www.w3.org/2001/XMLSchema-instance" z:Id="i1" 
                xmlns:z="http://schemas.microsoft.com/2003/10/Serialization/" 
                xmlns="http://schemas.datacontract.org/2004/07/Models">
      <Manager>
        <Department z:Ref="i1" />
        <Name>Alice</Name>
      </Manager>
      <Name>Sales</Name>
    </Department>

If you want to avoid attributes on your model class, there is another option: Create a new type-specific**DataContractSerializer**?instance and set?_preserveObjectReferences_?to?**true**?in the constructor. Then set this instance as a per-type serializer on the XML media-type formatter. The following code show how to do this: 
    
    
    var xml = GlobalConfiguration.Configuration.Formatters.XmlFormatter;
    var dcs = new DataContractSerializer(typeof(Department), null, int.MaxValue, 
        false, /* preserveObjectReferences: */ true, null);
    xml.SetSerializer<Department>(dcs);

#