title: angularjs service factory provider 区别
link: http://www.sheng00.com/1822.html
author: admin
description: 
post_id: 1822
created: 2014/11/19 15:24:41
created_gmt: 2014/11/19 07:24:41
comment_status: open
post_name: angularjs-service-factory-provider-%e5%8c%ba%e5%88%ab
status: publish
post_type: post

# angularjs service factory provider 区别

Services Syntax: module.service( 'serviceName', function ); Result: When declaring serviceName as an injectable argument you will be provided with an instance of the function. In other words new FunctionYouPassedToService(). Factories Syntax: module.factory( 'factoryName', function ); Result: When declaring factoryName as an injectable argument you will be provided with the value that is returned by invoking the function reference passed to module.factory. Providers Syntax: module.provider( 'providerName', function ); Result: When declaring providerName as an injectable argument you will be provided with ProviderFunction().$get(). The constructor function is instantiated before the $get method is called - ProviderFunction is the function reference passed to module.provider.