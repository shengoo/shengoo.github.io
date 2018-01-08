title: android使用ZipInputStream解压缩zip压缩文件
link: http://www.sheng00.com/12.html
author: admin
description: 
post_id: 12
created: 2011/02/28 08:00:00
created_gmt: 2011/02/28 00:00:00
comment_status: open
post_name: android%e4%bd%bf%e7%94%a8zipinputstream%e8%a7%a3%e5%8e%8b%e7%bc%a9zip%e5%8e%8b%e7%bc%a9%e6%96%87%e4%bb%b6
status: publish
post_type: post

# android使用ZipInputStream解压缩zip压缩文件

public class unzip extends Activity {
      /** Called when the activity is first created. */
    
      static final int BUFFER = 2048;
      TextView textView;
    
      @Override
      public void onCreate(Bundle savedInstanceState) {
    
        textView = new TextView(this);
        super.onCreate(savedInstanceState);
        textView.setText(“Main Activity”);
        extractZipfile();
        setContentView(textView);
      }
    
    
    
      private void extractZipfile() {
        String extractDir = getApplicationContext().getFilesDir()
                .getAbsolutePath()
                + “/unzip/”;
        try {
          BufferedOutputStream dest = null;
          ZipInputStream zis = new ZipInputStream(getResources()
                  .openRawResource(R.raw.book));
          ZipEntry entry;
          while ((entry = zis.getNextEntry()) != null) {
            File file = new File(extractDir + entry.getName());
    
    
            if (file.exists()) {
              textView.append(“n” + file.getAbsolutePath() + “texists”);
              continue;
            }
            if (entry.isDirectory()) {
              if (!file.exists())
                file.mkdirs();
              textView.append(“nCreate directory: “
                      + file.getAbsolutePath());
              continue;
            }
            textView.append(“nExtracting:” + entry);
            int count;
            byte data[] = new byte[BUFFER];
            textView.append(” to ” + file.getAbsolutePath());
    
            FileOutputStream fos = new FileOutputStream(file);
            dest = new BufferedOutputStream(fos, BUFFER);
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
              dest.write(data, 0, count);
            }
            dest.flush();
            dest.close();
          }
          zis.close();
        } catch (Exception e) {
            // TODO: handle exception
          e.printStackTrace();
        }
      }
    }