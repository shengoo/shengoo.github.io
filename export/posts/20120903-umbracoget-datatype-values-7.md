title: Umbraco:get datatype values
link: http://www.sheng00.com/420.html
author: admin
description: 
post_id: 420
created: 2012/09/03 15:34:19
created_gmt: 2012/09/03 07:34:19
comment_status: open
post_name: umbracoget-datatype-values-7
status: publish
post_type: post

# Umbraco:get datatype values

Code:
    
    
    @{
        //var prevalues = umbraco.library.GetPreValues(1235); 
        var prevalues = umbraco.cms.businesslogic.datatype.PreValues.GetPreValues(1235);
    }
    
    
    
    @prevalues.ToString()
    
    
    @if (prevalues.Count > 0)
    {
        for (int i=0;i@prevalue.Id:@prevalue.Value
    
    
            }
        }
    }
    

output:

System.Collections.SortedList

81:国内

82:国外

83:资金

84:技术

85:人才