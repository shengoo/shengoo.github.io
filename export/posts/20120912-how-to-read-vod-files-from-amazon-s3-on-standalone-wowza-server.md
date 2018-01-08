title: How to read VOD files from Amazon S3 on Standalone Wowza Server
link: http://www.sheng00.com/423.html
author: admin
description: 
post_id: 423
created: 2012/09/12 15:12:15
created_gmt: 2012/09/12 07:12:15
comment_status: open
post_name: how-to-read-vod-files-from-amazon-s3-on-standalone-wowza-server
status: publish
post_type: post

# How to read VOD files from Amazon S3 on Standalone Wowza Server

From <http://www.wmconsulting.info/read-vod-files-amazon-s3-standalone-wowza-server/>   I’ll explain how to is possible read the files from Amazon S3 Storage but without using a EC2 instance. For example your “localhost” or your Standalone Wowza server running on your own datacenter. I did this for working on my local development environment, I’ll describe the steps for a Linux environment. 1- Download from this URL the 2 Jars, and copy this in **/lib** directories. [download id="5"] [download id="6"] 2- Create the MediaCache folder: 
    
    
    mkdir /mnt/mediacache

3- Insert into the **conf/Server.xml** this lines: 
    
    
    <ServerListeners>
    <ServerListener>
    <BaseClass>com.wowza.wms.plugin.amazonaws.ec2.mediacache.MediaCacheServerListenerAmazonEC2</BaseClass>
    </ServerListener>
    </ServerListeners>
    

4- Insert into the **conf/vods3/Application.xml** (create this first) this lines: 
    
    
    <MediaReader>
    <Properties>
    <Property>
    <Name>randomAccessReaderClass</Name>
    <Value>com.wowza.wms.plugin.amazonaws.ec2.mediacache.MediaCacheRandomAccessReaderAmazonEC2</Value>
    </Property>
    <Property>
    <Name>bufferSeekIO</Name>
    <Value>true</Value>
    <Type>Boolean</Type>
    </Property>
    </Properties>
    </MediaReader>
    

And in the end of the file, add this properties (I don’t know is needed this for read Public content): 
    
    
    <Properties>
    <!-- Set these two properties to do S3 authentication -->
    <Property>
    <Name>awsAccessKeyId</Name>
    <Value>KEY</Value>
    </Property>
    <Property>
    <Name>awsSecretAccessKey</Name>
    <Value>KEY</Value>
    </Property>
    </Properties>
    

5- Restart the Wowza Server and try reading from S3 Bucket. The URL can be like this: **rtmp://localhost/vods3/_definst_/mp4:amazons3/wmconsulting.content/Extremists.m4v**