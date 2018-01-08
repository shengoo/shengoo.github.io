title: .net rest api 下载文件代码
link: http://www.sheng00.com/2085.html
author: admin
description: 
post_id: 2085
created: 2015/03/26 11:47:17
created_gmt: 2015/03/26 03:47:17
comment_status: open
post_name: net-rest-api-%e4%b8%8b%e8%bd%bd%e6%96%87%e4%bb%b6%e4%bb%a3%e7%a0%81
status: publish
post_type: post

# .net rest api 下载文件代码

[HttpGet]
    public HttpResponseMessage GetImage()
    {
      //文件路径
      var path = HostingEnvironment.MapPath("~/App_Data/5.jpg");
      FileStream fileStream = new FileStream(path, FileMode.Open, FileAccess.Read);
      Image img = Image.FromStream(fileStream);
      MemoryStream ms = new MemoryStream();
      img.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);
      HttpResponseMessage result = new HttpResponseMessage(HttpStatusCode.OK);
    
      result.Content = new ByteArrayContent(ms.ToArray());
      result.Content.Headers.ContentType = new MediaTypeHeaderValue("image/jpg");
      result.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
      {
          FileName = "5.jpg"//文件名
      };
      return result;
    }