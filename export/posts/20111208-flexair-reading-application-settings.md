title: Flex/Air Reading application settings
link: http://www.sheng00.com/167.html
author: admin
description: 
post_id: 167
created: 2011/12/08 13:54:34
created_gmt: 2011/12/08 05:54:34
comment_status: open
post_name: flexair-reading-application-settings
status: publish
post_type: post

# Flex/Air Reading application settings

### Reading the application descriptor file

You can read the application descriptor file of the currently running application, as an XML object, by getting the applicationDescriptor property of the NativeApplication object, as in the following:
    
    
    var appXml:XML = NativeApplication.nativeApplication.applicationDescriptor;

You can then access the application descriptor data as an XML (E4X) object, as in the following:
    
    
    var appXml:XML = NativeApplication.nativeApplication.applicationDescriptor;
    var ns:Namespace = appXml.namespace();
    var appId = appXml.ns::id[0];
    var appVersion = appXml.ns::version[0];
    var appName = appXml.ns::filename[0];
    air.trace("appId:", appId);
    air.trace("version:", appVersion);
    air.trace("filename:", appName);

For more information, see [The application descriptor file structure](http://livedocs.adobe.com/flex/3/html/File_formats_1.html#1043434).

 

var fileTypes:XML = appXml.ns::fileTypes[0];   
                    for each ( var fileType:XML in fileTypes.ns::fileType ) {   
                        trace(fileType.ns::name);   
                    }