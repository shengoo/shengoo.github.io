title: iis 7 - IIS7 URL Rewrite - Add "www" prefix
link: http://www.sheng00.com/1177.html
author: admin
description: 
post_id: 1177
created: 2014/07/02 14:16:39
created_gmt: 2014/07/02 06:16:39
comment_status: open
post_name: iis-7-iis7-url-rewrite-add-www-prefix
status: publish
post_type: post

# iis 7 - IIS7 URL Rewrite - Add "www" prefix

<?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <rewrite>
          <rules>
            <!--<rule name="Add www" patternSyntax="Wildcard" stopProcessing="true">
              <match url="*" />
            <conditions>
            <add input="{HTTP_HOST}" pattern="test.com" />
              </conditions>
            <action type="Redirect" url="http://www.test.com/{R:0}" />
            </rule>-->
            <rule name="Add www" patternSyntax="ECMAScript" stopProcessing="true">
          <match url=".*" />
            <conditions>
              <add input="{HTTP_HOST}" pattern="^test.com$" />
            </conditions>
            <action type="Redirect" url="http://www.test.com/{R:0}" />
        </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>