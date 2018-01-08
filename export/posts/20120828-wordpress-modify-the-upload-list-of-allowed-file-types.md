title: WordPress: modify the upload list of allowed file types
link: http://www.sheng00.com/388.html
author: admin
description: 
post_id: 388
created: 2012/08/28 16:38:12
created_gmt: 2012/08/28 08:38:12
comment_status: open
post_name: wordpress-modify-the-upload-list-of-allowed-file-types
status: publish
post_type: post

# WordPress: modify the upload list of allowed file types

When you attempt to upload a file in WordPress that is not in the default list of acceptable file types, you will receive the following error: **File type does not meet security guidelines. Try another.** While there’s no admin-based tool for editing list of allowed file types, it’s not at all difficult to add your own or remove any existing. Upload filetypes are checked by the function wp_check_filetype in wp-includes/functions.php. But we will add new file types to the file functions.php in our template due to upgrade WordPress. Open your theme's `functions.php` file and add this line somewhere between the `<?php` and `?>`:  
    
    
    add_filter('upload_mimes', 'custom_upload_mimes');
    function custom_upload_mimes ( $existing_mimes=array() ) {
    // add your extension to the array
    $existing_mimes['deb'] = 'application/x-deb';
    // add as many as you like
    // removing existing file types
    unset( $existing_mimes['exe'] );
    // add as many as you like
    // and return the new full result
    return $existing_mimes;
    }

In this case I allowed upload .deb files and banned upload .exe files. List of MIME Types can be found [here](http://www.w3schools.com/media/media_mimeref.asp), or use google, if your file type is not in the list (e.g. deb or rpm file type).