title: JavaScript:工厂模式
link: http://www.sheng00.com/1433.html
author: admin
description: 
post_id: 1433
created: 2014/09/07 14:26:09
created_gmt: 2014/09/07 06:26:09
comment_status: open
post_name: javascript%e5%b7%a5%e5%8e%82%e6%a8%a1%e5%bc%8f
status: publish
post_type: post

# JavaScript:工厂模式

> 工厂模式定义：实例化对象，用工厂方法代替new操作。
    
    
    function CarMaker () {
      
    }
    CarMaker.prototype.drive = function () {
      console.log("Vroom, I have " + this.doors + " doors");
    }
    CarMaker.factory = function (type) {
      var constr = type,
      newcar;
      if(typeof CarMaker[constr] !== "function"){
        throw{
          name:"Error",
          message: constr + " doesn't exist"
        };
      }
      if(typeof CarMaker[constr].prototype.drive !=="function"){
        CarMaker[constr].prototype = new CarMaker();
      }
      newcar = new CarMaker[constr]();
      return newcar;
    }
    
    CarMaker.Compact = function(){
      this.doors = 4;
    }
    CarMaker.Convertible = function(){
      this.doors = 2;
    }
    CarMaker.SUV = function(){
      this.doors = 3;
    }
    
    
    var corolla = CarMaker.factory('Compact');
    var solstice = CarMaker.factory('Convertible');
    var cherokee = CarMaker.factory('SUV');
    corolla.drive();
    solstice.drive();
    cherokee.drive();
    

> 内置的Object也表现了工厂的行为：
    
    
    var o = new Object(),
        n = new Object(1),
        s = Object("s"),
        b = Object(true);
    
    
    console.log(o.constructor);
    console.log(n.constructor);
    console.log(s.constructor);
    console.log(b.constructor);