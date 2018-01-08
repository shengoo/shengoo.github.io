title: JavaScript类型转换 type conversions
link: http://www.sheng00.com/1198.html
author: admin
description: 
post_id: 1198
created: 2014/07/16 13:12:22
created_gmt: 2014/07/16 05:12:22
comment_status: open
post_name: javascript%e7%b1%bb%e5%9e%8b%e8%bd%ac%e6%8d%a2-type-conversions
status: publish
post_type: post

# JavaScript类型转换 type conversions

var a = new Boolean(false);
    console.log(a);//{}
    console.log(a == false)//true
    console.log(a === false)//false
    if(a){
        console.log("new Boolean(false) is true")//new Boolean(false) is true
    }else{
        console.log("new Boolean(false) is false")
    }

这里a转换为true，因为a是一个Boolean的object，而object如果不是null或者undefined，就会被转换为true 这里主要需要分清楚值类型（primitive）和对象类型（object） 下面是JavaScript类型转换 

JavaScript type conversions

值 转换为:

String Number Boolean Object

`undefined`
`"undefined"`
`NaN`
`false`
throws TypeError

`null`
`"null"`
`0`
`false`
throws TypeError

`true`
`"true"`
`1`

`new Boolean(true)`

`false`

`"false"`

`0`

`new Boolean(false)`

`""`?(empty string)

`0`

`false`

`new String("")`

`"1.2"`?(nonempty, numeric)

`1.2`

`true`

`new String("1.2")`

`"one"`?(nonempty, non-numeric)

`NaN`

`true`

`new String("one")`

`0`

`"0"`

`false`

`new Number(0)`

`-0`

`"0"`

`false`

`new Number(-0)`

`NaN`

`"NaN"`

`false`

`new Number(NaN)`

`Infinity`

`"Infinity"`

`true`

`new Number(Infinity)`

`-Infinity`

`"-Infinity"`

`true`

`new Number(-Infinity)`

`1`?(finite, non-zero)

`"1"`

`true`

`new Number(1)`

`{}`?(any object)

`true`

`[]`?(empty array)

`""`

`0`

`true`

`[9]`?(1 numeric elt)

`"9"`

`9`

`true`

`['a']`?(any other array)