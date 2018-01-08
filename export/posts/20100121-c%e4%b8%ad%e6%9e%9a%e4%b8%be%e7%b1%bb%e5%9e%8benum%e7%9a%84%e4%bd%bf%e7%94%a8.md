title: C#中枚举类型enum的使用
link: http://www.sheng00.com/29.html
author: admin
description: 
post_id: 29
created: 2010/01/21 08:00:00
created_gmt: 2010/01/21 00:00:00
comment_status: open
post_name: c%e4%b8%ad%e6%9e%9a%e4%b8%be%e7%b1%bb%e5%9e%8benum%e7%9a%84%e4%bd%bf%e7%94%a8
status: publish
post_type: post

# C#中枚举类型enum的使用

### 1、关于enum的定义
    
    
    enum Fabric
    {
      Cotton = 1,
      Silk = 2,
      Wool = 4,
      Rayon = 8,
      Other = 128
    }
    

### 2、符号名和常数值的互相转换
    
    
    Fabric fab = Fabric.Cotton;
    int fabNum = (int)fab;//转换为常数值。必须使用强制转换。
    Fabric fabString = (Fabric)1;//常数值转换成符号名。如果使用ToString()，则是（（Fabric）1）.ToString()，注意必须有括号。
    string fabType = fab.ToString();//显示符号名
    string fabVal = fab.ToString ("D");//显示常数值
    

### 3、获得所有符号名的方法（具体参见Enum类）
    
    
    public enum MyFamily
    {
      YANGZHIPING = 1,
      GUANGUIQIN = 2,
      YANGHAORAN = 4,
      LIWEI = 8,
      GUANGUIZHI = 16,
      LISIWEN = 32, 
      LISIHUA = 64,
    }
    foreach (string s in Enum.GetNames(typeof(MyFamily)))
    {
      Console.WriteLine(s);
    }
    

### 4、将枚举作为位标志来处理

根据下面的两个例子，粗略地说，一方面，设置标志[Flags]或者[FlagsAttribute]，则表明要将符号名列举出来；另一方面，可以通过强制转换，将数字转换为**符号名**。说不准确。看下面的例子体会吧。注意： 

  * 例一：
    
    
    Fabric fab = Fabric.Cotton | Fabric.Rayon | Fabric.Silk;
    Console.WriteLine("MyFabric = {0}", fab);//输出：Fabric.Cotton | Fabric.Rayon | Fabric.Silk;
    

  * 例二：
    
    
    class FlagsAttributeDemo
    {
      // Define an Enum without FlagsAttribute.
      enum SingleHue : short
      {
        Black = 0,
        Red = 1,
        Green = 2,
        Blue = 4
      };
    
      // Define an Enum with FlagsAttribute.
      [FlagsAttribute] 
      enum MultiHue : short
      {
        Black = 0,
        Red = 1,
        Green = 2,
        Blue = 4
      };
      static void Main( ) 
      {
        Console.WriteLine( 
        "This example of the FlagsAttribute attribute n" +
        "generates the following output." );
        Console.WriteLine( 
        "nAll possible combinations of values of an n" + 
        "Enum without FlagsAttribute:n" );
        // Display all possible combinations of values.
        for( int val = 0; val <= 8; val++ )
        Console.WriteLine( "{0,3} – {1}",  val, ( (SingleHue)val ).ToString( ) );
    
        Console.WriteLine(  "nAll possible combinations of values of an n" + "Enum with FlagsAttribute:n" );
        // Display all possible combinations of values.
        // Also display an invalid value.
        for( int val = 0; val <= 8; val++ )
        Console.WriteLine ( "{0,3} – {1}",  val, ( (MultiHue)val ).ToString( ) );
      } 
    }
    /*
    This example of the FlagsAttribute attribute
    generates the following output.
    All possible combinations of values of an 
    Enum without FlagsAttribute:
    0 – Black
    1 – Red
    2 – Green
    3 – 3
    4 – Blue
    5 – 5
    6 – 6
    7 – 7
    8 – 8
    All possible combinations of values of an
    Enum with FlagsAttribute:
    0 – Black
    1 – Red
    2 – Green
    3 – Red, Green
    4 – Blue
    5 – Red, Blue
    6 – Green, Blue
    7 – Red, Green, Blue
    8 – 8
    */
    

### 5、枚举作为函数参数。经常和switch结合起来使用。下面举例
    
    
    public static double GetPrice(Fabric fab)
    {
      switch (fab)
      {
        case Fabric.Cotton: 
          return (3.55);
        case Fabric.Silk: 
          return (5.65);
        case Fabric.Wool: 
          return (4.05);
        case Fabric.Rayon: 
          return (3.20);
        case Fabric.Other: 
          return (2.50);
        default: 
          return (0.0);
      }
    }
    

### 6、上面三点一个完整的例子
    
    
    //enum的定义
    public enum Fabric : short
    {
      Cotton = 1,
      Silk = 2,
      Wool = 3,
      Rayon = 8,
      Other = 128
    }
    //将枚举作为参数传递
    public static double GetPrice(Fabric fab)
    {
      switch (fab)
      {
        case Fabric.Cotton: return (3.55);
        case Fabric.Silk : return (5.65);
        case Fabric.Wool: return (4.05);
        case Fabric.Rayon: return (3.20);
        case Fabric.Other: return (2.50);
        default: return (0.0);
      } 
    }
    
    public static void Main()
    {
      Fabric fab = Fabric.Cotton;
      int fabNum = (int)fab;
      string fabType = fab.ToString();
      string fabVal = fab.ToString ("D");
      double cost = GetPrice(fab);
      Console.WriteLine("fabNum = {0}nfabType = {1}nfabVal = {2}n", fabNum, fabType, fabVal);
      Console.WriteLine("cost = {0}", cost); 
    }
    

### 7、Enum类的使用

`Enum.IsDefinde`、`Enum.Parse`两种方法经常一起使用，来确定一个值或符号是否是一个枚举的成员，然后创建一个实例。`Enum.GetName`打印出一个成员的值；`Enum.GetNames`打印出所有成员的值。其中注意**```typeof```**的使用。这一点很重要。 
    
    
    public enum MyFamily
    {
      YANGZHIPING = 1,
      GUANGUIQIN = 2,
      YANGHAORAN = 4,
      LIWEI = 8,
      GUANGUIZHI = 16,
      LISIWEN = 32, 
      LISIHUA = 64,
    }
    
    string s = "YANGHAORAN";
    if (Enum.IsDefined(typeof(MyFamily), s))
    {
      MyFamily f = (MyFamily)Enum.Parse(typeof(MyFamily), s);
      GetMyFamily(f);
      Console.WriteLine("The name is:" + Enum. GetName(typeof(MyFamily), 2));
      string[] sa = Enum.GetNames(typeof(MyFamily)); 
      foreach (string ss in sa)
      {
        Console.WriteLine(ss);
      }
    }