title: Copy and Paste is not working on my Remote Desktop Connection… what’s wrong?
link: http://www.sheng00.com/1011.html
author: admin
description: 
post_id: 1011
created: 2013/12/03 16:02:45
created_gmt: 2013/12/03 08:02:45
comment_status: open
post_name: copy-and-paste-is-not-working-on-my-remote-desktop-connection-whats-wrong
status: publish
post_type: post

# Copy and Paste is not working on my Remote Desktop Connection… what’s wrong?

A very annoying occurrence that I sometimes suffer is when all of a sudden the copy and paste function stops working when I am connected to a remote machine. Turns out the problem is coming from a little process called rdpclip. Rdpclip (remote desktop clipboard) is responsible for managing a shared clipboard between your local host and the remote desktop (the process runs on the remote machine not your local host). 

#### So what do I do when clipboard stops working?

Luckily fixing the issue is pretty straightforward and involves a few simple steps. 

  1. Load up task manager (right click taskbar and select Task Manager) 
  2. Go to the Processes Tab 
  3. Select rdpclip.exe 
  4. Click End Process 
  5. Go to the Application Tab 
  6. Click New Process 
  7. Type rdpclip 
  8. Click Ok

There, copy and paste should now work normally again. 

#### It happens so often, this process is annoying! What do I do to fix it permanently?

Unfortunately I don’t know why rdpclip stops working nor how to fix it permanently; however, there is a way to make it easier if it happens often. 

  * Create a new bat file and call it whatever you want say, clipboard.bat. 
  * Write the following two commands on separate lines in the new bat file 
    * Taskkill.exe /im rdpclip.exe 
    * Rdpclip.exe 
    * Save the bat file and drag it into the toolbar quick launch section

Now whenever your copy and paste operation fails to restore it, all you need to do is click this new batch file which will kill rdpclip and restart it. Still a workaround but at least it’s a quick procedure. 

\- See more at: http://www.gfi.com/blog/copy-paste-working-remote-desktop-connection-whats-wrong/#sthash.AhDKFvk7.dpuf