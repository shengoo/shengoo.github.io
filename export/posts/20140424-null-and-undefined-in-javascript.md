title: null and undefined in javascript
link: http://www.sheng00.com/1119.html
author: admin
description: 
post_id: 1119
created: 2014/04/24 11:59:59
created_gmt: 2014/04/24 03:59:59
comment_status: open
post_name: null-and-undefined-in-javascript
status: publish
post_type: post

# null and undefined in javascript

> var un;
    > console.log(un);
    undefined
    > var nu = null;
    > console.log(nu);
    null
    > typeof un
    'undefined'
    > typeof nu
    'object'
    > un == nu
    true
    > un === nu
    false
    > Number(undefined)
    NaN
    > Number(null)
    0
    

undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是： （1）变量被声明了，但没有赋值时，就等于undefined。 （2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。 （3）对象没有赋值的属性，该属性的值为undefined。 （4）函数没有返回值时，默认返回undefined。