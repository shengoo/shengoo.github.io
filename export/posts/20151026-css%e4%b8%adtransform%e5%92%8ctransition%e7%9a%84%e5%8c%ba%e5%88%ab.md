title: CSS中Transform和Transition的区别
link: http://www.sheng00.com/2144.html
author: admin
description: 
post_id: 2144
created: 2015/10/26 22:41:40
created_gmt: 2015/10/26 14:41:40
comment_status: closed
post_name: css%e4%b8%adtransform%e5%92%8ctransition%e7%9a%84%e5%8c%ba%e5%88%ab
status: publish
post_type: post

# CSS中Transform和Transition的区别

## Transform

`Transform`意思是变形，指的是变成什么样子，虽然经常在动画里用到这个属性，但是Transform本事是静态的，跟动画没什么关系。 

## Transition

`Transition`意思是过渡，指的是怎么变，这个是可以做到动画的。 

### Transition配合一般属性
    
    
    div
    {
    width:100px;
    height:100px;
    background:blue;
    transition:width 2s;
    -moz-transition:width 2s; /* Firefox 4 */
    -webkit-transition:width 2s; /* Safari and Chrome */
    -o-transition:width 2s; /* Opera */
    }
    
    div:hover
    {
    width:300px;
    }
    

请把鼠标指针移动到蓝色的 div 元素上，就可以看到过渡效果。 **注释：**本例在 Internet Explorer 中无效。