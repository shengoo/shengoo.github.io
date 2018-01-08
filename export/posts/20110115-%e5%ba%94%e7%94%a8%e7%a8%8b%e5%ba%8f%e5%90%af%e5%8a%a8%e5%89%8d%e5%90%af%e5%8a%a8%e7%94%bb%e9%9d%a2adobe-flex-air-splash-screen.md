title: 应用程序启动前启动画面adobe flex air splash screen
link: http://www.sheng00.com/17.html
author: admin
description: 
post_id: 17
created: 2011/01/15 08:00:00
created_gmt: 2011/01/15 00:00:00
comment_status: open
post_name: %e5%ba%94%e7%94%a8%e7%a8%8b%e5%ba%8f%e5%90%af%e5%8a%a8%e5%89%8d%e5%90%af%e5%8a%a8%e7%94%bb%e9%9d%a2adobe-flex-air-splash-screen
status: publish
post_type: post

# 应用程序启动前启动画面adobe flex air splash screen

这是一个应用程序启动前的窗口，可以用在多个方面，比如下载资源、检查更新、初始化控件等等

<?xml version="1.0" encoding="utf-8"?>  
<mx:Window xmlns:fx="http://ns.adobe.com/mxml/2009"   
          xmlns:s="library://ns.adobe.com/flex/spark"   
          xmlns:mx="library://ns.adobe.com/flex/mx" width="265" height="226"  
          systemChrome="none"  
          type="lightweight" showFlexChrome="false" transparent="true"   
          verticalScrollPolicy="off" horizontalScrollPolicy="off" windowComplete="init()">  
    <fx:Declarations>  
        <!-- Place non-visual elements (e.g., services, value objects) here -->  
    </fx:Declarations>  
    <fx:Script>  
        <![CDATA[  
            private function init():void  
            {  
                this.nativeWindow.x = Screen.mainScreen.visibleBounds.width/2 - this.width/2;  
                this.nativeWindow.y = Screen.mainScreen.visibleBounds.height/2 - this.height/2;  
                this.nativeWindow.visible = true;  
                 
                this.dispatchEvent(new Event(Event.COMPLETE));  
                var timer:Timer = new Timer(500,10);  
                timer.addEventListener(TimerEvent.TIMER,onTimer);  
                timer.start();  
            }   
              
            private function onTimer(e:TimerEvent):void  
            {  
                if(lbl.text.length<15)  
                    lbl.text += ".";  
                else  
                    lbl.text = "download";  
            }  
              
            public function showProgress(str:String,num:int):void  
            {  
                if(!pb.visible)  
                    pb.visible = true;  
                pb.label = str;  
                pb.setProgress(num,100);  
            }  
        ]]>  
    </fx:Script>  
    <mx:Canvas width="266" height="227" borderStyle="none">  
        <mx:Image source="@Embed('splash-bg.jpg')" >  
              
        </mx:Image>  
        
        <s:Label id="lbl" y="200" fontSize="14" horizontalCenter="0" color="0xdddddd" text="download...">  
        </s:Label>  
        <mx:ProgressBar id="pb"  y="230" visible="false" chromeColor="white"  
                        minimum="0" maximum="100"  
                        direction="right" mode="manual" width="80%"   
                         horizontalCenter="0">  
              
        </mx:ProgressBar>  
    </mx:Canvas>  
</mx:Window>

 

 

主程序调用：

this.visible = false;//set app invisible.  
splashScreen = new Splash_Window();  
splashScreen.addEventListener(Event.COMPLETE,function():void  
{  
       //闪过之后的处理，splashScreen  
});  
splashScreen.open();//show splash screen.

 

![](/wp-content/uploads/2013/06/4eb0_6f51e2fd4e75c514d7887d03.jpg)