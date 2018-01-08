title: 帝国CMS当前栏目高亮显示
link: http://www.sheng00.com/518.html
author: admin
description: 
post_id: 518
created: 2013/03/23 14:11:51
created_gmt: 2013/03/23 06:11:51
comment_status: open
post_name: %e5%b8%9d%e5%9b%bdcms%e5%bd%93%e5%89%8d%e6%a0%8f%e7%9b%ae%e9%ab%98%e4%ba%ae%e6%98%be%e7%a4%ba
status: publish
post_type: post

# 帝国CMS当前栏目高亮显示

找到e/class/userfun.php，加入下面代码 
    
    
    function currentPage($classid,$thisid){
            global $class_r;
            $fr=explode('|',$class_r[$classid][featherclass]);
            $topbclassid=$fr[1]?$fr[1]:$classid;//取得第一级栏目id
            if ($topbclassid==$thisid) {
                      echo "menuon";
                    }
                    else {
                    }
    }
    

menuon是CSS样式名，可自己定义 导航这样写 
    
    
    ?[e:loop={'select classid,classname,classpath from [!db.pre!]enewsclass where bclassid=0 and showclass=0 order by myorder',0,24,0}]
    <li id="cid<?=$bqr[classid]?>" class="<?=currentPage($GLOBALS[navclassid],$bqr[classid])?>">
    <a href="&lt;?=$public_r[newsurl]?&gt;&lt;?=$bqr[classpath]?&gt;" title="<?=$bqr[classname]?>" target="_self"><?=$bqr[classname]?></a>
    </li>
    [/e:loop]

_OK了_