title: Android service 自动重启
link: http://www.sheng00.com/1835.html
author: admin
description: 
post_id: 1835
created: 2014/11/25 16:55:16
created_gmt: 2014/11/25 08:55:16
comment_status: open
post_name: android-service-%e8%87%aa%e5%8a%a8%e9%87%8d%e5%90%af
status: publish
post_type: post

# Android service 自动重启

当Android的service被停止（内存不够、被其他app杀掉）的时候，加入以下代码到你的service里，就可以马上重新启动了。 
    
    
    @Override
    public void onDestroy() {
      super.onDestroy();
      // Restart service in 500 ms
      ((AlarmManager) getSystemService(Context.ALARM_SERVICE))
      .set(AlarmManager.RTC, 
        System.currentTimeMillis() + 500,
        PendingIntent.getService(this, 3, new Intent(this, TaskService.class), 0));
    }