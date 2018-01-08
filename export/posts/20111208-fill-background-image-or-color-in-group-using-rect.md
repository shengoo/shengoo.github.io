title: flex中设置背景色或背景图片Fill background image or color in Group using Rect
link: http://www.sheng00.com/168.html
author: admin
description: 
post_id: 168
created: 2011/12/08 14:04:28
created_gmt: 2011/12/08 06:04:28
comment_status: open
post_name: fill-background-image-or-color-in-group-using-rect
status: publish
post_type: post

# flex中设置背景色或背景图片Fill background image or color in Group using Rect

<?xml version="1.0" encoding="utf-8"?>
    <s:Application xmlns:fx="http://ns.adobe.com/mxml/2009" 
                   xmlns:s="library://ns.adobe.com/flex/spark" 
                   xmlns:mx="library://ns.adobe.com/flex/mx" width="400" height="300">
        <fx:Declarations>
            <!-- Place non-visual elements (e.g., services, value objects) here -->
        </fx:Declarations>
        <s:HGroup width="100%" height="100%">
            <s:Group width="50%" height="100%">
                <s:Rect width="100%" height="100%"
                        horizontalCenter="0"
                        verticalCenter="0"
                        topLeftRadiusX="5"
                        topLeftRadiusY="5"
                        topRightRadiusX="5"
                        topRightRadiusY="5"> 
                    <s:fill>
                        <s:BitmapFill fillMode="repeat" source="@Embed(source='flag.png')"/>
                    </s:fill>
                </s:Rect>
            </s:Group>
            <s:Group width="50%" height="100%">
                <s:Rect width="100%" height="100%"
                        horizontalCenter="0"
                        verticalCenter="0"
                        topLeftRadiusX="5"
                        topLeftRadiusY="5"
                        topRightRadiusX="5"
                        topRightRadiusY="5"> 
                    <s:fill>
                        <s:SolidColor alpha="0.5" color="#8811dd"/>
                    </s:fill>
                </s:Rect>
            </s:Group>
        </s:HGroup>
    </s:Application>
    

效果如下： [swfobj src="http://www.sheng00.com/wp-content/uploads/2011/12/BackgroundFill.swf"]