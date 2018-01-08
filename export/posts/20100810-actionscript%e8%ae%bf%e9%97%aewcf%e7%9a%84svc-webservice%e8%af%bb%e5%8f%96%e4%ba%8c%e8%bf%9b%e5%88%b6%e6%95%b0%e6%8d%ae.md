title: ActionScript访问WCF的svc WebService读取二进制数据
link: http://www.sheng00.com/23.html
author: admin
description: 
post_id: 23
created: 2010/08/10 08:00:00
created_gmt: 2010/08/10 00:00:00
comment_status: open
post_name: actionscript%e8%ae%bf%e9%97%aewcf%e7%9a%84svc-webservice%e8%af%bb%e5%8f%96%e4%ba%8c%e8%bf%9b%e5%88%b6%e6%95%b0%e6%8d%ae
status: publish
post_type: post

# ActionScript访问WCF的svc WebService读取二进制数据

先写个wcf的svc服务  
有个方法叫TestImage，返回一个图片的二进制数据   
写好服务能用之后开始ActionScript的实现   
  
先在build path里加入fiber.swc   
我的fiber.swc路径是C:Program FilesAdobeAdobe Flash Builder 4pluginscom.adobe.flexbuilder.dcrad_4.0.0.272416dcradSwcs4.0libsfiber.swc   
  
然后是代码   

    
    
    package WebService  
    
    {
    import com.adobe.fiber.core.model_internal;
    import com.adobe.fiber.services.wrapper.WebServiceWrapper;
    
    import flash.events.Event;
    import flash.events.IOErrorEvent;
    import flash.filesystem.File;
    import flash.filesystem.FileMode;
    import flash.filesystem.FileStream;
    import flash.net.URLLoader;
    import flash.net.URLRequest;
    import flash.net.URLRequestMethod;
    import flash.net.URLVariables;
    import flash.utils.ByteArray;
    
    import mx.rpc.AbstractOperation;
    import mx.rpc.AsyncToken;
    import mx.rpc.events.ResultEvent;
    import mx.rpc.soap.mxml.WebService;
    
    
    public class ImageTest extends WebServiceWrapper
    {
    
      public function ImageTest()
      {
        _serviceControl = new WebService();
        //load wsdl
        _serviceControl.loadWSDL("http://192.168.0.2:8080/EpubService/Service1.svc?wsdl");
        model_internal::initialize();
        getImage();
      }
    
    
      public function getImage():void
      {
        var operation:AbstractOperation = _serviceControl.getOperation("TestImage");
        operation.addEventListener(ResultEvent.RESULT,onresult);
        operation.send();
      }
    
      private function onresult(e:ResultEvent):void
      {
        var imgByte:ByteArray = e.result as ByteArray;
        var f:File = File.documentsDirectory.resolvePath("test.jpg");
        var fs:FileStream = new FileStream();
        try
        {
          //open file in write mode
          fs.open(f,FileMode.WRITE);
          //write bytes from the byte array
          fs.writeBytes(imgByte);
          trace("create file: "+f.nativePath);
        }
        catch(e:Error)
        {
          trace(e.message);
        }
        finally
        {
          //close the file
          fs.close();
        }
        }
      }
    }
    

输出：  

    
    
    create file: C:UsersQingDocumentstest.jpg