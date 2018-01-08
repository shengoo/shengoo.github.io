title: git remote url 从https到ssh，从ssh到https
link: http://www.sheng00.com/2057.html
author: admin
description: 
post_id: 2057
created: 2015/01/09 22:18:29
created_gmt: 2015/01/09 14:18:29
comment_status: open
post_name: git-remote-url-%e4%bb%8ehttps%e5%88%b0ssh%ef%bc%8c%e4%bb%8essh%e5%88%b0https
status: publish
post_type: post

# git remote url 从https到ssh，从ssh到https

`git remote set-url` 命令可以改变一个代码库的url. `git remote set-url` 命令可以接受两个参数： The git remote set-url command takes two arguments: 

  * 一个远程名字，比如： `origin`
  * 远程的url，比如 
    * `https://github.com/USERNAME/REPOSITORY_2.git` 如果你想改为使用 HTTPS
    * `git@github.com:USER/REPOSITORY_2.git` 如果你想改为使用SSH

### 远端url从ssh改成https

  1. 打开终端 (Mac 和 Linux) 或者命令行 (Windows).
  2. cd到你的目录里.
  3. 显示现在的远程url. 
    
        git remote -v
    origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
    origin  git@github.com:USERNAME/REPOSITORY.git (push)
    

  4. 使用`remote set-url` 命令切换url. 
    
        git remote set-url origin https://github.com/USERNAME/REPOSITORY_2.git
    

  5. 验证一下是不是已经改变. 
    
        git remote -v
    origin  https://github.com/USERNAME/REPOSITORY2.git (fetch)
    origin  https://github.com/USERNAME/REPOSITORY2.git (push)
    

下一次你使用 `git fetch`, `git pull`, 或者 `git push` 命令的时候，会提示你输入用户名和密码。

### Switching remote URLs from HTTPS to SSH

  1. 打开终端 (Mac 和 Linux) 或者命令行 (Windows).
  2. cd到你的目录里.
  3. 显示现在的远程url. 
    
        git remote -v
    origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
    origin  https://github.com/USERNAME/REPOSITORY.git (push)
    

  4. 使用`remote set-url` 命令切换url. 
    
        git remote set-url origin git@github.com:USERNAME/REPOSITORY2.git
    

  5. 验证一下是不是已经改变. 
    
        git remote -v
    origin  git@github.com:USERNAME/REPOSITORY2.git (fetch)
    origin  git@github.com:USERNAME/REPOSITORY2.git (push)