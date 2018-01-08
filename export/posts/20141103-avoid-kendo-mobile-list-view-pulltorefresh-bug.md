title: avoid kendo-mobile-list-view pullToRefresh bug
link: http://www.sheng00.com/1485.html
author: admin
description: 
post_id: 1485
created: 2014/11/03 14:59:07
created_gmt: 2014/11/03 06:59:07
comment_status: open
post_name: avoid-kendo-mobile-list-view-pulltorefresh-bug
status: publish
post_type: post

# avoid kendo-mobile-list-view pullToRefresh bug

When use kendoui angular mobile list view, there is a bug: [mobile listview is initialized before mobile scroller in angular, making endless scrolling impossible](https://github.com/telerik/kendo-ui-core/issues/280) to fix this, use k-ng-delay , let the list view render after scroller