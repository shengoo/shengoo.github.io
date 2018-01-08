title: flex（air） image button
link: http://www.sheng00.com/16.html
author: admin
description: 
post_id: 16
created: 2011/01/28 08:00:00
created_gmt: 2011/01/28 00:00:00
comment_status: open
post_name: flex%ef%bc%88air%ef%bc%89-image-button
status: publish
post_type: post

# flex（air） image button

package buttons  
{  
    import mx.controls.Button;  
      
    public class ImageButton extends Button  
    {  
        [Embed(source="assets/image/delete-16.png")]   
        private var icon:Class;  
        [Embed(source="assets/image/deleteover.png")]   
        private var overIcon:Class;  
        [Embed(source="assets/image/deletedown.png")]   
        private var downIcon:Class;  
        public function ImageButton()  
        {  
            super();  
            this.label = "";  
            this.width = 16;  
            this.height = 16;  
            this.setStyle("cornerRadius",8);  
            this.setStyle("icon",icon);  
            this.setStyle("downIcon",downIcon);  
            this.setStyle("overIcon",overIcon);  
            this.setStyle("upIcon",icon);  
        }  
    }  
}

![](/wp-content/uploads/2013/06/e239_10ae7d60b528068e8cb10d15.jpg)

![](/wp-content/uploads/2013/06/a00c_32ce2eb3c3a71af6d8335a10.jpg)

![](/wp-content/uploads/2013/06/d736_01d4f013a074da535baf5311.jpg)

![](/wp-content/uploads/2013/06/6ded_fef9f116caa1f349962b4312.jpg)