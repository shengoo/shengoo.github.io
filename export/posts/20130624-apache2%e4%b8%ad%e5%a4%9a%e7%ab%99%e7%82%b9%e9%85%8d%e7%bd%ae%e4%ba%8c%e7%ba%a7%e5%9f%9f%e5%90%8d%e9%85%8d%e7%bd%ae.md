title: apache2中多站点配置,二级域名配置
link: http://www.sheng00.com/796.html
author: admin
description: 
post_id: 796
created: 2013/06/24 12:02:15
created_gmt: 2013/06/24 04:02:15
comment_status: open
post_name: apache2%e4%b8%ad%e5%a4%9a%e7%ab%99%e7%82%b9%e9%85%8d%e7%bd%ae%e4%ba%8c%e7%ba%a7%e5%9f%9f%e5%90%8d%e9%85%8d%e7%bd%ae
status: publish
post_type: post

# apache2中多站点配置,二级域名配置

1. 增加站点 
    
        sudo cp /etc/apache2/sites-available/default /etc/apache2/sites-available/mynewsite
    

  2. 配置站点 
    
        sudo vi /etc/apache2/sites-available/mynewsite
    
    
        ServerAlias *.sheng00.com
    

  3. 开启站点 
    
        sudo a2ensite mynewsite
    sudo service apache2 restart
    

  4. 关闭站点
    
        sudo a2dissite mynewsite
    sudo service apache2 restart
    

站点配置中，如果想配置二级域名的站点，ServerAlias 要写成二级域名，比如xx.sheng00.com