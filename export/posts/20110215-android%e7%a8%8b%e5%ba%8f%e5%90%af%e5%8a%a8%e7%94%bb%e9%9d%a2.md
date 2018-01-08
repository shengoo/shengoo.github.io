title: Android程序启动画面
link: http://www.sheng00.com/13.html
author: admin
description: 
post_id: 13
created: 2011/02/15 08:00:00
created_gmt: 2011/02/15 00:00:00
comment_status: open
post_name: android%e7%a8%8b%e5%ba%8f%e5%90%af%e5%8a%a8%e7%94%bb%e9%9d%a2
status: publish
post_type: post

# Android程序启动画面

public class SplashScreenTest extends Activity {
      /** Called when the activity is first created. */
      @Override
      public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.splash);
        /** set time to splash out */
        final int welcomeScreenDisplay = 3000;
    
    
        new Handler().postDelayed(new Runnable(){  
           @Override  
           public void run() {  
               Intent mainIntent = new Intent(SplashScreenTest.this,MainActivity.class);  
               startActivity(mainIntent);  
               finish();  
           }  
          }, welcomeScreenDisplay); 
    
        }
    }
    
    
    public class MainActivity extends Activity {
      @Override
      public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        TextView textView = new TextView(this);
        textView.setText(“Main Activity”);
        setContentView(textView);
      }
    }
    

svn checkout https://myandroidcode.googlecode.com/svn/trunk/SplashScreenTest

源代码 <http://code.google.com/p/myandroidcode/source/browse/trunk/SplashScreenTest>