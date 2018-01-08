title: 编译源代码修改jwplayer  Build jwplayer source code
link: http://www.sheng00.com/449.html
author: admin
description: 
post_id: 449
created: 2012/09/14 23:32:55
created_gmt: 2012/09/14 15:32:55
comment_status: open
post_name: %e7%bc%96%e8%af%91%e6%ba%90%e4%bb%a3%e7%a0%81%e4%bf%ae%e6%94%b9jwplayer-build-jwplayer-source-code
status: publish
post_type: post

# 编译源代码修改jwplayer  Build jwplayer source code

首先checkout jwplayer的源代码 地址：http://developer.longtailvideo.com/svn/trunk/fl5 编译jwplayer需要以下程序 * Flex SDK 4.1: http://sourceforge.net/adobe/flexsdk/wiki/Downloads/ * Ant 1.7.0: http://ant.apache.org/bindownload.cgi * FlexUnit 4: http://opensource.adobe.com/wiki/display/flexunit/FlexUnit (for testing the player) 环境配置好之后需要修改配置文件 flexsdk = C:/Program Files/Adobe/Adobe Flash Builder 4.5/sdks/4.5.1 windows环境下需要更改execextension execextension = .exe 根据flash player版本更改flexsdk.target C:Program FilesAdobeAdobe Flash Builder 4.5sdks4.5.1frameworkslibsplayer10.2 这个是本机的player版本，所以 flexsdk.target = 10.2.0 配置文件修改完成之后就可以用ant来build了 控制台切换到build文件夹运行：ant -buildfile buildbuild.xml 输出： Buildfile: E:Developmentjwplayersourcebuildbuild.xml check-properties: clean-release: build-release-player: release-swf: build-swf: [exec] ????????????????C:Program FilesAdobeAdobe Flash Builder 4.5sdks4.5.1frameworksflex-config.xml?? [exec] E:Developmentjwplayersourceplayer.swf??112357 ???? BUILD SUCCESSFUL Total time: 4 seconds 如果你的电脑上装的是64位的java sdk的话，可能会报错 现在开始修改源代码 1、去掉左下角的jwplayer水印 找到com.longtailvideo.jwplayer.view里的View.as 找到protected function setupComponents()里的setupComponent(_logo, n++);注释掉即可 2、修改右键about的菜单项 找到com.longtailvideo.jwplayer.view里的RightclickMenu.as 修改function setAboutText()函数 about = new ContextMenuItem('About Sheng00 ...'); 修改function aboutHandler(evt:ContextMenuEvent)函数 navigateToURL(new URLRequest('http://www.sheng00.com'), '_blank');   然后ant -buildfile buildbuild.xml 生成的就是修改过的player了 以下是效果：  

JW Player goes here